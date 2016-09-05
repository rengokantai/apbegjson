### apbegjson
####CHAPTER 2 Special Objects
#####Access Notation
######Bracket Notation vs. Dot Notation
Bracket notation has a particular advantage.  
Bracket notation relies on string values, whereas dot notation utilizes identifiers.  
Identifiers can’t start with numbers, use whitespace, or be a reserved word in the language. Bracket notation can.
```
var k=new Object();
k['1']="1" //legal
k.1="1" //illegal
```
####CHAPTER 3 String Manipulation
#####Creating String Objects
```
var k = new String( "test" );
console.log(k) ;   //String { 0="t", 1="e", 2="s", 3="t" }
```
#####toString
It is worth noting that the toString method does not return a string object, but rather the primitive-type string.

######The Implicit String Object
####CHAPTER 5 Creating JSON
#####The JSON Object
######stringify
The stringify method doesn’t acknowledge a few values. First and foremost, you may have realized that an undefined value is handled in one of two possible manners. If the value undefined is found on a property, the property is removed entirely from the JSON text. If, however, the value undefined is found within an ordered list, the value is converted to 'null'.
```
JSON.stringify( { prop:undefined } );   //"{}"
JSON.stringify( [ undefined ] );        //"[null]"
JSON.stringify( 1/0 );                  //"null"
JSON.stringify( Infinity );             //"null"
JSON.stringify( [ function(){ return "A"} ] );    //"[null]"
```
replacer Array (only serialize fields we want to serialize)
```
JSON.stringify(k,[f1,f2]);
```
padding (only works on objects and strings
####CHAPTER 6 Parsing JSON
#####JSON.parse
######reviver
```
var p=new Person();
    p.name="ke";
Person.prototype.getName=function(){
    return this.name;
};
```
reviver function
```
var serializedPerson=JSON.stringify(p);

var reviver = function(k,v){
// if the key is an empty string we know its our top level object
    if(k===""){
        //set object’s inheritance chain to that of a Person instance
        v.__proto__ = new Person();
    }
    return v;
}

var parsedJSON = JSON.parse( serializedPerson , reviver );
console.log(parsedJSON instanceof Person); // true
console.log(parsedJSON.getName()); // "ke"
```
####CHAPTER 7 Persisting JSON: I
#####HTTP Cookie
######expires
The value supplied is required to be in UTC Greenwich Mean Time format. 
```
var date= new Date("Jan 1 2015 12:00 AM");
var UTCdate= date.toUTCString() ;
console.log( UTCdate );  // "Thu, 01 Jan 2015 06:00:00 GMT"
```
If the value supplied to the expires attribute occurs in the past, the cookie is immediately purged from memory. On the other hand, if the expires attribute is omitted, then the cookie will be discarded the moment the session has ended.   
######max-age
max-age specifies the life span of the cookie in seconds.  
######domain  
Explicitly defines the domain(s) to which the cookie is to be made available.  
to broaden the scope of cookies, we can use . to precede our domain. set domain attribute to
```
.yd.me
```
######path
The path attribute further enforces to which subdirectories a cookie is available. If a path attribute is not explicitly specified, the value is defaulted to the current directory that set the cookie.  
(check with the examples)  
######httponly
Cookies set with the httponly flag can only be set by the server.
#####document.cookie
```
document.cookie= "ourFirstCookie=123";
document.cookie= "ourSecondCookie=456";
document.cookie= "ourThirdCookie=789";
```
The name/value pairs are not being overridden with each new assignment.  
[mdn doc](https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie)  
Rather, they stored safely within the cookie jar. 

######Extracting the Value from a Specified Key Among Many
```
function getCookie(name) {
     var regExp = new RegExp(name + "=[^\;]*", "mgi");
     var matchingValue = (document.cookie).match(regExp);
     console.log( matchingValue )   // "k=v" array
     for(var key in matchingValue){  //iterate all (k,v) pairs
         var replacedValue=matchingValue[key].replace(name+"=",""); //remove "k="
         matchingValue[key]=replacedValue;  //assign "v
     }
     return matchingValue;
 };
 getCookie("ourFourthCookie");  // ["That would bring us back to Doe"] the line numbers.
```
If store an object to cookie, must convert to json first.
```
function Person() {
    this.name;
    this.age;
};
Person.prototype.getName = function() {
    return this.name;
};
Person.prototype.getAge = function() {
    return this.age;
};

var p = new Person();
p.name = "ke";
p.age = "1";

var serializedPerson = JSON.stringify(p);
setCookie("person", serializedPerson, new Date("Jan 1 2017"),"/",".yd.me",null);
console.log( getCookie( "person" )); "{"name":"ke","age":"1",}"
```
