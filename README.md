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

