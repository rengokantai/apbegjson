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
    p.name="ben";
    p.age="36";
    p.gender="male";
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
```
```
