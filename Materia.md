# kotlin for java developers
## kotlin for java developers
### iniciado em 01/02/2020
### terminado em ANDAMENTO

## kotlin for java developers

### what is kotlin?
kotlin is a general purpose language which supports both functional programming and object-oriented programming paradigms.
it´s a open source project.
like java, kotlin is a statically typed language. however you can omit the types and it often looks as concise as some other dynamically-typed languages.
kotlin is safe, it´s even safer than java in the terms that kotlin compiler can help to prevent even more possible types of errors. 
one of the main characteristics of kotlin is its good interoperability with java and you can use any java library.
kotlin is a pragmatic language for industry, it´s not a research project that just tries some ideas.
it´s based on many existing languages and it tries to reuse what works there.
you often can find what language was the source of inspiration for some kotlin features.
kotlin can be used for android applications but also as a server side language, and you can use kotlin whenever you use java before.
kotlin has other target platforms, like kotlin/jvm, kotlin/js and kotlin/native.
this course focuses on kotlin/jvm

### from java to kotlin
it´s really easy to start using kotlin especially if you are a java developer.
you can use all the existing java frameworks and libraries from kotlin.
you can even mix kotlin and java code in one project.
kotlin is a JVM language, so you can easily call java code from kotlin, and kotlin from java.

kotlin is compile to java bytecode (.class).

you can automatically convert java code into kotlin using the automatic java to kotlin converter.

let´s compare this class:

Person.java
public class Person {
	private final String name;
	private final int age;

	public Person(String name, int age) {
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return name;
	}

	public int getAge() {
		return age;
	}
}

and now the same class in kotlin:
class Person(val name: String, val age: Int)

under the hood, in bytecode, the same constructor and two getters are generated.

so from java point of view it´s the same class.

if you add a data modifier to this class you get the equals, hashCode and to string methods.

data class Person(val name: String, val age: Int)

another difference is the use of the new keyword or the (not) use of semicolons:

java
Person person = new Person("Alice", 27);
System.out.println(person.getName());

kotlin
val person = Person("Alice", 27)
println(person.name)

and now another difference:

java
public void updateWeather(int degrees) {
	String description;
	Color color;
	if(degrees < 10) {
		description = "cold";
		color = BLUE;
	} else if(degrees < 25) {
		description = "mild";
		color = ORANGE;
	} else {
		description = "hot";
		color = RED;
	}
}


if you simply convert it to kotlin it will look like this:
fun updateWeather (degrees: Int) {
	val description: String
	val color: Color
	if(degrees < 10) {
		description = "cold"
		color = BLUE
	} else if(degrees < 25) {
		description = "mild"
		color = ORANGE
	} else {
		description = "hot"
		color = RED
	}
}

but this can be improoved in kotlin:

we have several description assignments repeating themselves. but in kotlin we can avoid it. we can initialize two variables at once by a PAIR of values:

fun updateWeather (degrees: Int) {
	val (description: String, color: Color ) =
	if(degrees < 10) {
		Pair("cold", BLUE)
	} else if(degrees < 25) {
		Pair("mild", ORANGE)
	}  else {
		Pair("hot", RED)
	}
}


now we don´t have to repeat the discription throughout the code.

but we can make another improovement....
when you define a variable in java you have to specify its type. in kotlin you can prefer to omit the type if it´s clear from the context:
when you omit the type specification, the kotlin compiler infers the type automatically:

fun updateWeather (degrees: Int) {
	val (description, color) =
	if(degrees < 10) {
		Pair("cold", BLUE)
	} else if(degrees < 25) {
		Pair("mild", ORANGE)
	}  else {
		Pair("hot", RED)
	}
}

another improovement we can make is replace the 'IF' with 'WHEN'

'when' expression in kotlin is similiar to 'SWITCH' in java, allowing you to enumerate several options, usefull when you have more than two if-else options

fun updateWeather (degrees: Int) {
	val (description, color) = when {
		degrees < 10 -> Pair("cold", BLUE)
		degrees < 25 -> Pair("mild", ORANGE)
		else -> Pair("hot", RED)
	}
}

and now another improovement. we can replace the construicting of 'PAIR' with 'TO', which is an alternative way to create a PAIR in kotlin

fun updateWeather (degrees: Int) {
	val (description, color) = when {
		degrees < 10 -> cold" to BLUE
		degrees < 25 -> "mild" to ORANGE
		else -> "hot" to RED
	}
}

the automatic converter DO NOT CONVERT TO THE BEST KOTLIN CODE, you have to do it manually.

### Introducing Kotlin to an existing project
It´s is recommended that java programmers, when switching to Kotlin, uses real life scenarios because this way you get a real feel of the language and see how it works in the daily work. 

So, pickup a small portion of existing java code and convert it to kotlin using the java to kotlin conversion tool and see if you like the kotlin code better than the existing java code you had before.

then, you can select a feature or class and write it from scratch in kotlin to see how it´s done step by step.

you don´t have to alter any surrounding java code at all, because kotlin and java can coexist in the same project.

you don´t have to convert everything to kotlin, so you can keep the java code forever and convert as you go or pick any strategy you like.

### "Hello, world" example

#### top level functions
let look at this hello world example:

hello, kotlin example

    package intro
    
    fun main () {
    	val name = "Kotlin"
    	println("Hello, $name!")
    }

now let´s try to compare it with the similar code written in java.

the first things that comes to mind is these keywords (fun, val) for functional and variable declaration.

if you look closer you will see that there is no class here. this function is declared at the top level and it is the only content of the file.

> YOU CAN DEFINE FUNCTIONS AT THE TOP LEVEL

in kotlin you can define the function at the package level, so you don´t need to put everything inside a class, to define a lot of static utility functions inside a special util class. if you need general functions without binding to the specific class, you can define them at the package level

#### main with or without arguments
before kotlin version 1.3, you had to use arguments in the main function just like java. but after version 1.3, you can ommit these arguments, if they are never going to be used:

    fun main(args: Array<String>) {...} //before kotlin 1.3
    
    fun main() {...} //after kotlin 1.3
    

in java, the 'main' method always requires the program argument list (public static void (String[] args)) but for simple use-cases, these program arguments are often unused.

let´s do an example. 

if no program arguments are passed we are going to print "kotlin", or "hello" and the value of the first program argument passed.

    package intro
    
    fun main(args: Array<String>) {
    	val name = if (args.size > 0) args[0] else "Kotlin"
    	println("Hello, $name!")
    }
    

there is NO SPECIAL BUILT-IN SYNTAX FOR ARRAYS. under the hood, at the bytecode level, it´s the same as in java. however, in the code, Arrays looks like a REGULAR CLASS WITH GENERIC ARGUMENTS (Array<String))

in kotlkin, 'if'  is an expression. you can assign the result of 'if' into a variable or return it from a function.

'IF' RETURNS YOU THE RESULT VALUE. 

#### strings templates
in kotlin, you can insert a string literal by using a dollar sign ($) and a variable name.
if you need to printout a more complicated expression, like a function call or a getter, or some arithmetic expression you can insert the value of this expression, but you HAVE TOSURROUND IT WITH CURLY BRACES (${function ...})

what happens if the value inserted is a null?
under the hood kotlin uses java.lang.String, and that means that such things work directly as in java.
in java, if you try to add the value 'null' to a string, the word 'null' will be concatenated to the string. in kotlin it´s absolutely the same.

java.lang.Strings transforms 'null' constant into a string 'null'.

if you want an empty string instead of 'null', as in java, you have tod process that explicitly.

### variables
there are 2 main keywords to define variables in kotlin: **val** and **var**

val comes from 'value' and denotes a **read only** or **assign-once** variable, while 

var comes from 'variable' and denotes a **mutable** variable, the one that can be modified.

read only variables can´t be reassigned. if you try to assign a new value to it you´ll get a compiler error.

in essence, 'val' corresponds to a 'final' variable in java.

#### omission of variable types
in kotlin, you can omit the types of variables and the compiler will infer the types for you.
ex.
val greeting = "hi"
val number = 8

here we omitted the types of these 2 variables and they are inferred automatically by the compiler.

kotlin is a statically-typed language, which means that every variable, every expression has a type. even if you omit the type, the compiler just infers it for you, but that doesn´t mean that this variable doesn´t have a type or it´s unknown. it means that the type specification is verbose, it´s clear from the context, and you trust the compiler to infer the type.

YOU CAN´T CHANGE A VAR TYPE AFTER IT HAS BEEN DECLARED

if you do this:
var string = 1
string = "abc"
you´ll get a compiler error.

for the compiler, the string variable is of type int, inferred by the value assigned to it.
when trying to change its value to a string, the compiler doesn´t permit this change because the var string is of type int and not of type String.

#### modify an object stored in val
just as in java final variable, you can modify the object stored in a val.
you can´t change the object to another one, but the properties of the object can be modified.

ex:
val person = Person(name = "name")
person.name = "another name"

it is a valid code.

person = Person(name = "another object") 
it is not a valid code.

#### list and mutable list
in kotlin, we have 2 types of list: a read only list and a mutable list

you can´t modify a read only list. 

read only lists doesn´t have the mutating methods

ex of a read only list:
val list = listOf("java")

list doesn´t have the .add() method

now an example of mutating list:
val mutable = mutableListOf("java")
mutable.add ("kotlin")

it works, because the mutable list has the mutating methods

#### best practices with variables
by default, strive to declare all your new variables with 'val' keyword, nor 'var'.

using immutable references, immutable objects and functions without side effects makes your code closer to the functional style, which is easier to understand and support in the end.

when the type specifications are clear from the context, it´s safe to omit them.
however, if any confusion could appear, it´s best just to have this type specification explicitly.

### functions
let´s use this example:
fun max (a: Int, b: Int) : Int {
	return if (a> b) a else b 
}

note that the parameter type specification is put after the parameter name like for variables. in a similar manner, function return type specification follows the argument list.

#### function with expression body
if your function simply returns one expression, you can use an alternative syntax. the expression that the function returns goes after the 'equals' sign. 

the return type of the function comes rigth after the parameters and de ':' sign (fun max (a: Int, b: Int) : **Int**)

it makes sense to specify types explicitly for public API, for library functions. but if it´s a regular applicaction, and you have a function, specially a private one, and it´s type is clear, for instance, from it´s name, you can safely omit it, like:
fun max (a: Int, b: Int)

note that if  you try to omit the type for a function **with expression body**, it will mean that this function return 'unit'.

#### return Unit
you can think of 'unit' as an analogue of 'void' in java. 

ex:
fun displayMax (a: Int, b: Int) {
	println(max*a, b)
}

this function does not return anything, it´s written for its side effects, and ther compiler considers its return type as 'Unit'.

you can explicitly put 'Unit' in the function return but no one does that.
ex:
fun displayMax (a: Int, b: Int): Unit {

#### places where you can define functions in kotlin
in kotlin you can define functions everywhere.

ex:
fun topLevel() = 1

or

class A {
	fun member() = 2
}

or 

fun other() {
	fun local() = 3
}

so you can declare it as a top level, a member or a local function

#### calling a top level function from java
from java, you call a top level function as a static function. all top level functions under the hood are implemented as static functions.

imagine this top level function:

MyFile.kt
package intro

fun foo() = 0

the top level function is define in the file called 'MyFile.kt'

at the bytecode, the underlying static function belongs to a class named '**MyFileKt**'

from java you can import a class by it´s name, or simply use 'import static'. in this last syntax gives you the same 'foo()' invocation as in kotlin.

ex:
package other
import intro.MyFileKt;

public class UsingFoo {
	public static void main (String[] args) {
		MyFileKt.foo();
	}
	
#### changing the name of a class that contains top level functions
if you want you can change the name of the class that contains all the top level functions as 'static' functions. for that you use a '**@JVMName**' annotation. you annotate the file contents and put the annotation right before the package name.

@file:JVMName("Utill")
MyFile.kt
package intro

fun foo() = 0
}

### Named & default arguments
println(listOf('a','b','c').joinToString(separator = "", prefix = "(", postfix = ")"))

this will print (abc)

the 'joinToString' function joins the contents of a string in the desired way. you can specify a separator, prefix and postfix.  the output should be quite straightfoward, it simply join the content of the list by using empty string as a separator, and surrounding it by the specified prefix and postfix.

you can specify the names of the arguments directly in the code, just like we did it. that often makes the invocation more readable. it´s easier to understand what the arguments are supposed to do, specially for arguments of basic types such as Int, Boolean or String.
named arguments are often used together with default arguments, like the joinToString, so that you can pass only what you need. say you only need to pass the postfix, and keep the rest default, you only pass that value, named as 'postfix', and the rest will be filled by default.

#### how to declare a function with default values for arguments
fun foo (a: String ="first argument", b: String = "second argument")

just after the type of the argument you put '=' and the default value

note that if you need to provide only the value for the second argument, then you have to use named arguments syntax.

by default, there is the direct correspondence between unnamed arguments and parameters according to their order.

just imagine this function:
fun foo(number: Int = 0, string : String = "String")

you can´t use it like this:
foo("blabla", 3)

this won´t compile, because the arguments doesn´t match the order they are declared.

if you pass the arguments by name, you can change their order easily

in java if you want to achieve the same behaviour, you will use the overload methods. to provide the functionality of default arguments, you will define several different overloads, and call one inside another by specifying default values. in kotlin you use the default arguments feature directly. you no longer need to provide several overloads.

#### how to call a function with default arguments from java?
when you call a kotlin function with default arguments from java, you have to specify the values for all the arguments.
that happens to minimize the number of functions which are generated under the hood.

by default, kotlin generates the function with all the arguments, and only one additional auxiliary function containing information about all the dafault values, which you can´t call from java.

if you wanto to call the kotlin function with default arguments from java in a convenient way, then you can add '**@JvmOverloads**' annotation. after you annotate the function with default argument with @JvmOverloads, you can specify only some of the arguments when you call it from java.

@JvmOverloads
fun foo(number: Int = 0, string : String = "String")

### Conditionals: if & when
#### if
if is an expression in kotlin. that means if returns a value which you can assign to a variable.
ex:
val max = if (a > b) a else b

in kotlin there is no ternary operator like in java. if you need the logic, you use if expression.

#### when
it migth be considered as an analogous of java switch.
when you have enum class with some values, you can perform actions or return a specific expression depending on the enum constant. when then takes enum value as an argument and checks all the enum constants.
in java , you have to use break or return if you want to stop operating inside the switch branch. otherwise, you´ll get the unexpected results. in kotlin you no longer need to use break to say that the operation should stop here. if the rank condition is satisfied, the result of their corresponding branch is returned.
note that you have to specify the paths to the enum constants explicitly, unless you import them. by default, you say, color blue, color orange, etc.  but you can import enum constant, and in this case you no longer need the explicit class specification, using constants simply by it´s names.

you can check whether when argument equal to one of the values:
fun respondToInput(input: String) = when (input) {
	"y", "yes" -> "i´m glad that you agree"
	"n", "no" -> "sorry to hear that"
	else -> "i don´t understand you"
}

you list several values separated by comma.

you can use any expression, not only constatns as branch conditions:
...
when(setOf(c1, c2)) {
	setOf(RED, YELLOW) -> ORANGE
	setOf(YELLOW, BLUE) -> GREEN
	else -> throw Exception()
}
here we created a set of two colors and compared with two predefined sets. when kotlin compares us by equality under the who did call set equals, which compares the content.
we used sets here to ignore the order of the colors.

somethimes you have to type a hierarchy, and neet to check whether it´s the sub-type or that sub-type and do actions accordingly.
in kotlin, you can use when for this. it´s checks whether an argument is of a specific type.

ex:
when (pet) {
	is Cat -> pet.meow()
	is Dog -> pet.woof()
}
note that you don´t have to cast explicitly, the variable after you checked it´s type, it´s automatically **smart** cast to the rigth type.

#### smart cast
ex:
if( pet instanceof Cat) {
	((Cat) pet).meow()
}else if (pet instanceof Dog){
	Dog dog = (Dog) pet;
	dog.woof()
}

in java you cast the variable to the type after checking instance of.
in kotlin, you simply access its members as it was of the right type

before kotlin 1.3 you had to do this:
val pet = getMyFavouritePet()
when (pet) {
	is Cat -> pet.meow()
	is Dog -> pet.woof()
}
now we have the opportunity to introduce a new variable for when subject direclty side of when expression. you often want to use thge whole expression as the when subject. however, the complicated expression can´t then be accessed as one variable inside when, and since there is no variable, nothing will be smart cast even if you check its type.
ex:

when (getMyFavouritePet()) {
	is Cat -> pet.meow()
	is Dog -> pet.woof()
}
this won´t work because you don´t have a pet variable

you need to explicitly introduce a new variable name like pet:
val pet = getMyFavouritePet()
when (pet) {
	is Cat -> pet.meow()
	is Dog -> pet.woof()
}
the problem is that this pet variable continues to be accessible even after the when expression is over.

now it is improoved and you can introduce a new variable name right inside the when parentesis by using val keyword:
when (val pet = getMyFavouritePet() ) {
	is Cat -> pet.meow()
	is Dog -> pet.woof()
}

now it is contained only within when scope

### Loops
in kotlin we have the same basic loops as in java: for, while and do-while

#### while and do-while loops
while (condition) {
	...
}

do {
	...
}while (condition)
in kotlin we have the same while and do-while loops, just like java

#### for loop
val list = listOf("a", "b", "c")
for (s in list) {
	print(s)
}

for loop looks a bid diferent.
first, a different keyword is used to express iteration over something - **in**.
second, we can omit the element type but you can specify the element type explicitly:
val list = listOf("a", "b", "c")
for (s: String in list) {
	print(s)
}

##### iterating over map
val map = mapOf( 1 to "one",
								2 to "two",
								3 to "three")
for ((key, value) in map) {
	println("$key = $value")
}

another difference is that in kotlin you can iterate over the contents of a map. here we assign key and value separately at each iteration loop, then printed the result.

this sintax works not only for maps, it can be used to iterate over a collection with index.

##### iteration with index
val list = listOf("a", "b", "c")
for ((index, element) in list.withIndex()) {
	println("$index: $element")
}

after we say **withIndex()" we can assign both index and element on each iteration turn.

##### iterating over ranges
for (i in 1..9) {
	...
}

if you need to work with indexes directly, you can use ranges. there is no full form of loop as in java, you use over ranges instead.
here we interate over range of numbers from 1 to 9.

you can also buit over range using until function. 
for (i in 1 until 9) {
	...
}

note that using until, the last number will be excluded, (like i < 9)
using 1..9 includes the last number (like i <= 9)

##### iterating with a step
for (i in 9 downTo 1 step 2) {
	print(i)
}
if you want you can build more complicated rangers like iterating back first or over a step.
using step will step over the number inserted, like in the example, when i = 2 it will not do anything and jump to i = 1

##### iterating over a string
for (ch in "abc") {
	print(ch + 1)
}

when iterating over a string, each character will be iterated, and it´s type will be char.

in the example, it will print 'bcd' because at each step it will get the next char (ch + 1), so when ch = 'a' will print 'b'

### 'in' checks & ranges
now we will discuss ranges. ti´s a very convenient feature that has no direct analogous in java.

#### in
in is used for two different cases:
the first one we already seen it in the previous topic about iterations:
for ( i **in** 'a'..'z') {...}

it is used for iteration

in can also be used to check for belongin:
c **in** 'a'..'z'

##### in a range
fun isLetter (c: Char) = c in 'a'..'z' || c in 'A'..'Z'

isLetter('q') //true 
isLetter('*') // false

here we check whether a character is a lower case or upper case letter.
by checking if it belongs to either the range of lowercase letters or the range of upper case letters.

##### NOT in a range
you can use not in, rechecks whether an element is not in the range
fun isNotDigit (c: Char) = c **!in** '0'..'9'

isNotDigit('x') // true

##### in as a when condition
you can use in as one condition like this:
fun recognize (c: Char) = when (c) {
	**in** '0'..'9' -> "it´s a digit"
	**in** 'a'..'z', in 'A'..'Z' -> "it´s a letter"
	else -> "don´t know"
}

#### different ranges
you can create ranges of different elements. it´s clear what a range of integer numbers or a range of character means but what about the range of strings?

1..9
1 until 10
'a'..'z'
"ab".."az"
startDate..endDate

you can store a range in a variable of the corresponding range type, such range is a regular object.
note that under the hood, the check for primitive types is optmized.

val intRange: IntRange = 1..9
val anotherIntRange: IntRange = 1 until 10
val charRange: CharRange = 'a'..'z'
val stringRange: ClosedRange<String> = "ab".."az"
val dateRange: ClosedRange<MyDate> = startDate..endDate

##### check if a string is in a set of strings
"kotlin" **in** setOf("Java", "Scala")

we can check if a string is present in a set of strings. in this case it is false.

##### check if a string is within the alfabetical order of the range
"kotlin" **in** "Java".."Scala"

**in** check is combined to the code simply by checkin its bounds.
like in java, strings are comparative lexicographically by default or in other words by the alphabetical order.

so, using our example, k from kotlin is within the range created by J from java and S from Scala


### exercise
#### Checking identifier
Implement the function that checks whether a string is a valid identifier. A valid identifier is a non-empty string that starts with a letter or underscore and consists of only letters, digits and underscores.

    fun isValidIdentifier(s: String): Boolean {
        if(s == "") return false
        
        var counter = 0
        for (str in s) {
            if(counter == 0) {
                if (str !in 'a'..'z' && str !in setOf('_')) return false
            }else {
                if (str !in 'a'..'z' && str !in setOf('_') && str !in '0'..'9') return false
            }
            counter = counter + 1
        }
        
        return true
    }
    
    fun main(args: Array<String>) {
        println(isValidIdentifier("name"))   // true
        println(isValidIdentifier("_name"))  // true
        println(isValidIdentifier("_12"))    // true
        println(isValidIdentifier(""))       // false
        println(isValidIdentifier("012"))    // false
        println(isValidIdentifier("no$"))    // false
    }

### Exceptions
in kotlin, exceptions are very similar to java with one important difference: kotlin doesn´t differentiate **checked** and **unchecked** exceptions.
in kotlin you may or may not handle any exception, and your function does not need to specify which exception it can throw.

the experience show us that in java rules for checked exceptions are often require you to write a logic meaningless code to withdraw or ignore exceptions and this rule doesn´t really help you to prevent possible errors.

#### throw
throw is an expression in kotlin. you can assign this result to a variable.

val percentage = 
	if( number in 0..100) {
		number
	}else {
		throw IllegalArgumentException ("A percentage value should be between 0 and 100")
	}

in this case, if the number belongs to the range from 0-100, this number becomes the result of the expression, otherwise, we throw an exception. you can assign throw to a variable of any type which is very convenient, specially to use that in if or when branches.

#### try
try can catch an exception if it was thrown inside, check it for being of a certain type, and perform the corresponding actions.

try is also an expression . that meas we can assign the result to a variable.

#### checked and unchecked exceptions
there are **no checked exceptions** in kotlin, so there is no need to specify that a functions throws an exception. however, we have the throws annotation (@Throws).
we use this annotation to possibilitate the use of this function in a java class.
if a functions throws an exception and you use it from a java class this annotation is mandatory to tell java that this function may throw an exception.

ex:
@Throws {IOException::class}
fun bar() { 
	throw IOException()
}

if you use this function in a java code without annotate it, it will not complie.

### Extension Functions
what are extension functions? why are they so important?

**Extensions functions extends the class, giving them more methods that suits our needs**

it is defined outside of the class but they can be called as a regular member to this class.

ex:
fun String.lastChar() = this.get(this.length - 1)

here we define an extension function to string called lastChar and we can use it as a member function.

it´s visible in code completion, so it can be easily discovered. it´s like a regular utility function define outside of the class. but on the other hand, thanks to code completion, it can be easily found and used like it was a member.

#### how we define an extension function
the time that the functions extends is called a Receiver.

ex:
fun String.lastChar() = this.get(this.length - 1)

here, String is the receiver of the lastChar function. in the body of this function, we can access the receiver by **this** reference. in this exemple, **this** refers to String. as usual for this reference we can omit it.

ex:
fun String.lastChar() = get(length - 1)

we can call members of the receiver inside an extension function withou explicit **this.** something specification.

an important thing to notice is that you can´t define an extension and use it everywhere. **you have to import it explicitly**.

if you define an extension functions lastChar somewhere and need to use it, you´ll need to import it either as one function, or inside the whole contents of the package.

by default, an extension functions is not accessible in the whole project. it´s visible in code completion but to use it you have to put the explicit input.

#### how to call an extension function from java?
when you call a top-level function from java, it´s simply a static function. for extension it works in the same way.

ex:
StringExtensions.kt
	fun String.lastChar() = get(length - 1)
	
JavaClass.java
	import static StringExtensionsKt.lastChar;
	char c = lastChar("abc");
	
	
when you interate in the parameter passed, like we did in the lastChar(), the parameter when you call it from java is just this one.

but let´s say you want to repeat a string some n times.
in kotlin the extension functions it´s just like this:
fun String.repeat (n: Int) : String {
	val sb = StringBuilder (n + length) // length of the string you want to repeat
	for (i in 1..n) {
		sb.append(this) //this is the string you want to repeat
	}
	return sb.toString()
}

and in kotlin you´ll use it like this:
"abc".repeat(3)

and the result will be : ababab

from java you have to pass also the object that in kotlin will be omited, like in this case, the string:

StringUtilsKt.repeat("ab", 3)

when you call these extensions functions from java, you pass String expression explicitly as the **first argument**

##### is it possible to call a private member from a class using extensions?
no, it´s not possible.
as in java, it´sonly possible to call a private member inside the same class.

kotlin extensions functions are most of the time top-level functions defined in a special extra file which content is compile to the corresponding extra class. therefore, it´s not possible to call a private member of a class from an extension to this class.

**Extensions functions doesn´t give you any additional access rights to the class contents.**

### Examples from the Standard Library
now let´s take a more deeper look in the extensions library.
Extensions play an important role in the language. 
kotlin standard library is just java standard library and a bunch of extensions that provides very smooth interoperability between java code and kotlin code. 

in kotlin, java standard collection classes from java.util package are used under the hood. when you create a collection using the functions from the kotlin standard library, instances of java standard classes are created.

** kotlin library simply provides extensions for regular java collections.

there is no suvh thing as kotlin SDK. it´s just java library with extensions. that givers us a couple of important benefits. at first, the size of the runtime jar that you have to add to your application when it starts using kotlin is relatively small. the kotlin doesn´t duplicate the standard implementations from java. it tries to reuse them.
if your application doesn´t use some of these extensions, they can be eliminated so that the added jar can get even smaller. 

the second important benefit is that using standard java collections provides very easy interoperability with java. you don´t have to convert one collection type to another, they are the same types under the hood. if you call java API from kotlin or vice versa, that´s very easy.

#### joinToString
the joinToString function allows you to get a nice string representation of a collection. in java, the square brackets are added by default, which is not always what you need. joinToString allows you to change the default behaviour by specifying the values for some of the algorithms.

it´s a regular extension function from the kotlin library

#### getOrNull
under the hood, kotlin array is the same as in java, but java array lacks this getOrNull method.
that´s also a extension in kotlin.

the similar function is available for list. it returns either an element of null if your index is wrong and the list contains fewer elements.

#### withindex()
the withIndex functions is also an extension. the important thing is that the withIndex is a function that is also provided as an extension.

having extensions in a language allows us to the new, nice syntatic features for standard java types. extensions are very powerfull.

#### until
until is also an extension. the until functions is defined as **infix**. 

infix fun Int.until(to: Int): IntRange

so this allow us to call it in a regular way, like this:
1.until(10)

or you can call it in an infix form by omitting dot and parenthesis.
1 until 10

until looks like a built-in syntax, but it´s not. it´s just an extension functions called in an infix form.

#### to
another function that are also an infix extension is the **to** function.
to in kotlin simply returns a pair of values. agaim you can use it in a regular form, but no one does that. everybody uses the nice infix form

#### char extensions
there are many useful extension functions on Char, like isLetter or isDigit.
you can look at what is available in the library using the completion list or just browsing the library

#### String extensions
kotlin String is like Java String with extensions

##### triple quoted strings literals
triple quoted string literals is another interesting feature in kotlin.
an alternative way to call them is the **multiline** strings. you can´t use any special characters there, but you can use strings templates to place inside them.

val q = """to code,
		or not to code?.."""

if you try to form a triple-quoted strins in your code, you´ll probably wanto to add the indent. by default, this indent **becomes part of the string**. there are some ways to crop this indent, and one of these ways is using the function **trimMargin()**. here the default margin is used, but you can specify another margin prefix if needed. the marginPrefix is automatically cut out together with indent.

val q = """to code,
		#or not to code?..""".trimMargin(marginPrefix = "#")

you can call the **trimIndent**() function directly, like the last example. if there is the same ident for all the lines in your string, it will be automatically removed.

both trimIndent and trimMargin functions are defined as extensions.

another useful extension is the **toRegex** function. you can convert a string to the regex clause to present in regular expressions. after that, you can call, for instance, matches method on this regular expression clause. 

val regex = "\\d{2}.\\d{2}\\.d{4}".toRegex()
regex.matches("15.02.2016) // true
regex.matches("15.02.16") // false

note that for regular expressions, it´s very convenient to use triple-quoted strings, so you don´t need to skip special characters there, including the backslash. the regular expression often becomes shorter.

val regex = """\d{2}.\d{2}\.d{4}""".toRegex()

#### conversion to number extensions
**toInt** and **toDouble** extensions functions will try to convert string representations to Int and Double accordingly. Note, however, that if you try to convert somthing that doesn´t make sense to an Integer, you´ll get NumberFormatException.

but ther is another extension available, toIntOrNull, which returns null if the string cannot be converted to an integer.

#### eq extension
the **eq** extension allow us test what is going on. it´s defined as a very simple extension function which checks whether the receiver equals its arguments. it prints OK if they are equal or prints an error if they´re not.

### Exercise
#### Sum as an extension function
Change the 'sum' function so that it was declared as an extension to List<Int>.

Question:
fun sum(list: List<Int>): Int {
    var result = 0
    for (i in list) {
        result += i
    }
    return result
}

fun main(args: Array<String>) {
    val sum = sum(listOf(1, 2, 3))
    println(sum)    // 6
}

Answer:
fun List<Int>.sum(): Int {
    var result = 0
    for (i in this) {
        result += i
    }
    return result
}

fun main(args: Array<String>) {
    val sum = listOf(1, 2, 3).sum()
    println(sum)    // 6
}

### Calling Extensions
in this chapter, we will see how extensions interact with inheritance and whether extensions can hide members.

#### inheritance
let´s say we have two classes, Parent and Child.
we can define two similar extensions functions. the first one to parent and the second one to child. we create a instance of child and store it in a reference of the parent type. which foo function will be called in this case?

openc class Parent
class Child : Parent{}

fun Parent.foo() = "parent"
fun Child.foo() = "child"

fun main(args: Array<String>) {
	val parent: Parent = Child()
	println(parent.foo())
}

an important thing to keep in mind is that extensions under the hood are regular java static  functions.

so, "parent" is printed here. 

**the resolution of which functions should be called here works in similar manner as for java static function**

Under the hood, these extension functions are compiled to java static functions, so 2 static methods are created:

public static String foo(Parent parent) { return "parent"}
public static String foo(Child child) { return "child"}

java resolves static functions statically. it finds the right function to be called during compilation. it only uses the type of the argument to choose the right function, thus the parent functions is chosen here since the parent variable has the parent type.

in general case, we don´t know what is stored in the parent variable. it can be an instance of child, parent or other class that extends parent. 

the actual stored object at runtime doesn´t change anything because the function to be called is already chosen during compilation. 

in kotlin, it works the same way as for static functions.

as mentioned, extensions are static functions under the hood, so **there is no override for extensions**.

when the compiler chooses the rigth function to be called, it only uses the type of the receiver expression, not the actual stored value.

#### what happens if we try to define an extension which duplicates a member of a class?

for instance, the string class has a member function 'get', which simply returns a character by it´s index.

we tried to define an extension with the same signature:
fun String.get(index: Int) = "*"

fun main (args: Array<String>) {
	println("abc".get(1))
}

it will print 'b'

**MEMBER ALWAYS HAS THE PREFERENCE OVER EXTENSIONS**

the indexation of string release contents starts with zero as in java. so in this case, the character returned by the first index is 'b'.

if you try to define extensions with the same signature as a member, then you get a warning that as extension is shadowed, so the member will always be used.

#### overload a member in extensions
if you define a extension with a different signature, different parameter types or the different number of parameters, your new function will be called if it fits better

### Importance of extensions
extensions are often named among the most important or lovable features of kotlin. why are they so important?

extensions have proven to be one of the most useful abstractions features of kotlin.

i think their main purpose is to keep your classes and interfaces API´s minimal. 

this is really important because this keeps the abstractions or things you´d try to describe to module with your class interfaces understandable. so, it´s important to capture the essence of the abstraction with this small set of members that covers the essential functionality.

all the auxilliary functions, all the utilities convenience methods can be written as extensions calling to this public API.

so, this the main principle. 

as an example, you can take the string class from the kotlin library. so, what´s a string? essentially, it´s a collection of characters that can be indexed. so string has only a handful of methods like take a length, take a character by index, and so forth and everything else like the huge number of utility methods available on the string, like everythiung about regular expressions, matching, splitting, so on and so forth, converting to uppercase, lowercase, and many more are all extensions.
so you can see what a string is, and then express everything else through it API. doesn´t mean principle and i think we should develop all our abstractions this way. so, when you have this division like members for instrinsic things and extensions for everything else, it makes sense to put them closer to each other so that it´s easy to discover extensions in the code.

so when you use extensions for your own classes, define them close to the class itself if they are general-purpose.

of course, if you have something specific to a sub-domain in your application, like in a different module, you have something specific to add to this class then keep that extension there in the module where it belongs to, but still group extensions to the same class together.

another important situation to use extensions is when you don´t control some class or interface because it sits in the library or it´s in another module or something like this, but you still want to extend its API somehow. so, through this, you can even extend the API of existing java libraries. so, even if something has no knowledge, no awereness of kotlin at all, you can turn it into a kotlin-like ergonomic idiomatic API through simply adding a couple of extensions. that´s proven to be a very useful thing. 

### mastermind game

Mastermind game
Mastermind is a board game for two players. The first player invents a code and the second player tries to guess this code. A code is made up 4 coloured pins and their position. There are 6 colours to choose from and the same colour can be repeated multiple times.

Examples of different codes:

Red Green Blue Yellow
Red Green Yellow Blue
Black White Red Orange
Red Red Blue White
(note that while the first two codes use the same colours, they are different as Blue and Yellow occupy different positions)

The game play is as follows:

The second player (the one that is guessing) sets out a series of pins in order to guess the code. The first player (that defined the code) then provides some feedback to the player in light of how close they are to the correct combination.

The feedback is as follows:

Number of pins that are both the right colour and position
Number of pins that are correct in colour but in the wrong position
Note that the rest pins in the code will pins that are neither correct in colour or position.

Your task is to evaluate a guess made by player two of the code set by player one. For the sake of simplicity, we use uppercase letters from A to F instead of colours.

You can test your solution and play as a second player using playMastermind.

Different Letters
Example 1
Secret ABCD and guess ABCD must be evaluated to: rightPosition = 4, wrongPosition = 0. All letters are guessed correctly in respect to their positions.

Example 2
Secret ABCD and guess CDBA must be evaluated to: rightPosition = 0, wrongPosition = 4. All letters are guessed correctly, but none has the right position.

Example 3
Secret ABCD and guess ABDC must be evaluated to: rightPosition = 2, wrongPosition = 2. A and B letters and their positions are guessed correctly. C and D letters are guessed correctly, but their positions are wrong.

At first, you can implement this easier task, when all the letters are different, and only after that start with the next part, when letters can be repeated. Run MastermindTestDifferentLetters to make sure you've implemented this part correctly.

Repeated Letters
Example 4
Secret AABC and guess ADFE must be evaluated to: rightPosition = 1, wrongPosition = 0. A at the first position is guessed correctly with its position. If we remove the first A from consideration (comparing the remaining ABC and DFE only), that will give us no more common letters or positions.

Example 5
Secret AABC and guess ADFA must be evaluated to: rightPosition = 1, wrongPosition = 1. The first A letter is guessed correctly with its position. If we remove this letter from consideration (comparing the remaining ABC and DFA), we find the second A letter which is guessed correctly but stays at the wrong position.

Example 6
Secret AABC and guess DFAA must be evaluated to: rightPosition = 0, wrongPosition = 2. No letters are guessed correctly concerning their positions. When we compare the letters without positions, A is guessed correctly. Since A is present twice in both guess and secret, it must be counted two times.

Example 7
Secret AABC and guess DEFA must be evaluated to: rightPosition = 0, wrongPosition = 1. The letter A occurs only once in the second string, that's why it counted only once as staying at the wrong position.

After implementing the task for repeated letters, run MastermindTestDifferentLetters to make sure it works correctly.

answer:
	
	
	
package mastermind

data class Evaluation(val rightPosition: Int, val wrongPosition: Int)

data class ResultIndex(val position: Int, val letter: Char, val isCorrect: Boolean, var secretContains: Boolean? = null)

fun evaluateGuess(secret: String, guess: String): Evaluation {

    val resultIndexList = mutableListOf<ResultIndex>()
    var index = 0

    var wrongSecret : String = ""
    var wrongGuess : String = ""
    while (index < 4) {
        if(secret[index] == guess[index]) {
            resultIndexList.add(ResultIndex(
                    position = index,
                    letter = guess[index],
                    isCorrect = true,
                    secretContains = true))
        } else {
            resultIndexList.add(ResultIndex(
                    position = index,
                    letter = guess[index],
                    isCorrect = false))
            wrongSecret += secret[index]
            wrongGuess += guess[index]
        }
        index += 1
    }

    var wrongPosition = 0
    var wrongGuessDoubleList = mutableListOf<Char>()

    for (wg in wrongGuess) {
        if(wrongSecret.contains(wg) && wrongSecret.contains(""+wg+wg)) {
            wrongPosition += 1
        }else if(wrongSecret.contains(wg) && wrongGuess.contains(""+wg+wg)) {
            wrongGuessDoubleList.add(wg)
        }else if(wrongSecret.contains(wg)){
            wrongPosition += 1
        }
    }

    for (dg in wrongGuessDoubleList.toSet()){
        wrongPosition += 1
    }


    val rightPosition = resultIndexList.filter { f -> f.isCorrect }.size
    return Evaluation(rightPosition, wrongPosition)
}

playMastermind

package mastermind

import kotlin.random.Random

val ALPHABET = 'A'..'F'
const val CODE_LENGTH = 4

fun main() {
    val differentLetters = false
    playMastermind(differentLetters)
}

fun playMastermind(
        differentLetters: Boolean,
        secret: String = generateSecret(differentLetters)
) {
    var evaluation: Evaluation

    do {
        print("Your guess: ")
        var guess = readLine()!!
        while (hasErrorsInInput(guess)) {
            println("Incorrect input: $guess. " +
                    "It should consist of $CODE_LENGTH characters from $ALPHABET. " +
                    "Please try again.")
            guess = readLine()!!
        }
        evaluation = evaluateGuess(secret, guess)
        if (evaluation.isComplete()) {
            println("The guess is correct!")
        } else {
            println("Right positions: ${evaluation.rightPosition}; " +
                    "wrong positions: ${evaluation.wrongPosition}.")
        }

    } while (!evaluation.isComplete())
}

fun Evaluation.isComplete(): Boolean = rightPosition == CODE_LENGTH

fun hasErrorsInInput(guess: String): Boolean {
    val possibleLetters = ALPHABET.toSet()
    return guess.length != CODE_LENGTH || guess.any { it !in possibleLetters }
}

fun generateSecret(differentLetters: Boolean): String {
    val chars = ALPHABET.toMutableList()
    return buildString {
        for (i in 1..CODE_LENGTH) {
            val letter = chars[Random.nextInt(chars.size)]
            append(letter)
            if (differentLetters) {
                chars.remove(letter)
            }
        }
    }
}

### Mastermind in a functional style
even though we can skip this resolution for now, because we haven´t had working functional style before, here is the complete implementation of 'evaluateGuess()' function in a functional style. we can compare our solution with the solution in functional style:

how we implemented it:
    fun evaluateGuess(secret: String, guess: String): Evaluation {
    
        val resultIndexList = mutableListOf<ResultIndex>()
        var index = 0
    
        var wrongSecret : String = ""
        var wrongGuess : String = ""
        while (index < 4) {
            if(secret[index] == guess[index]) {
                resultIndexList.add(ResultIndex(
                        position = index,
                        letter = guess[index],
                        isCorrect = true,
                        secretContains = true))
            } else {
                resultIndexList.add(ResultIndex(
                        position = index,
                        letter = guess[index],
                        isCorrect = false))
                wrongSecret += secret[index]
                wrongGuess += guess[index]
            }
            index += 1
        }
    
        var wrongPosition = 0
        var wrongGuessDoubleList = mutableListOf<Char>()
    
        for (wg in wrongGuess) {
            if(wrongSecret.contains(wg) && wrongSecret.contains(""+wg+wg)) {
                wrongPosition += 1
            }else if(wrongSecret.contains(wg) && wrongGuess.contains(""+wg+wg)) {
                wrongGuessDoubleList.add(wg)
            }else if(wrongSecret.contains(wg)){
                wrongPosition += 1
            }
        }
    
        for (dg in wrongGuessDoubleList.toSet()){
            wrongPosition += 1
        }
    
    
        val rightPosition = resultIndexList.filter { f -> f.isCorrect }.size
        return Evaluation(rightPosition, wrongPosition)
    }
    
	
	
how we could implemented it using fucntional style:
    data class Evaluation(val rightPosition: Int, val wrongPosition: Int)
    
    fun evaluateGuess(secret: String, guess: String): Evaluation {
    
        val rightPositions = secret.zip(guess).count { TODO() }
    
        val commonLetters = "ABCDEF".sumBy { ch ->
    
            Math.min(secret.count { TODO() }, guess.count { TODO() })
        }
        return Evaluation(rightPositions, commonLetters - rightPositions)
    }
    
    fun main(args: Array<String>) {
        val result = Evaluation(rightPosition = 1, wrongPosition = 1)
        evaluateGuess("BCDF", "ACEB") eq result
        evaluateGuess("AAAF", "ABCA") eq result
        evaluateGuess("ABCA", "AAAF") eq result
    }
	
	
pretty cool, right?

now let´s to the explanation:
"Let's see how the mastermind task can be solved in the functional style. We have an incomplete solution, where we need to fill the remaining parts. 
At first, we need to **count the number of letters guessed right with their positions**.
The number of letters that occur at the same place as both in secret and guess strings. 
##### the zip function
The zip function is really helpful for that. **When you zip two strings, it returns your list of pairs, where each pair consists of the characters at the same places from these strings.** We zip secret and guess. 
**If any pair in the resulting list consists of two similar characters, that means this character is guessed correctly with this position**. Thus, to count the number of right positions, we need to count the number of pairs where the first character from secret is equal to the second character from guess.
That's the solution for counting right positions.

After that, we need to **count the number of wrong positions, letters that are guessed correctly, but stay not in their correct positions.** 

We first **find the number of common letters, the letters that are overall guessed correctly ignoring their positions.** 

In the end, **we'll just subtract the number of right positions from common letters to get to the number of wrong positions**. 

To **find the number of common letters, we analyze each letter in our alphabet and see how many times it's present in the common letters set**. 

Let's see how it works for an example first. 

Our first sample doesn't contain the repetitive letters. For each letter, we mark whether it's present in secret and guess, and then find the letters that are present in both strings. One means the letter is present in a string, zero, that it's not there. In our case, the common letters are B and C.

Now let's check the more complicated sample with repetitive letters. We'll take the A character first and see how many times it occurs in secret and guess. It's repeated three times in secret and twice in guess. The minimum of these two numbers gives us the number of A occurrences in the common letters set. All the rest letters are found only in one of the strings. So for B, C, and F, the same counting gives zero as a result. The resulting common letters set consists then only of two A's. 

Now it's time to complete the function implementation. We check for each letter how many times it occurs in secret and guess, then we compare these numbers to get a minimum. To count the occurrences of letter, we compare it with it, which refers to letters in a string. 

First letters in secret, then letters in guess. That gives us the desired implementation. 

We can check these samples to make sure it works for them."

### Solution: Checking identifier
in this exercise, we will make a function that validates an identifier.
the rules to be true are:
* it has to start with a letter or underscore
* it can´t contain simbols

so this is our main fuctions with our expected results:
    
    fun main(args: Array<String>) {
    	println(isValidIdentifier(s: "name// true
    	println(isValidIdentifier(s: "_name/ true
    	println(isValidIdentifier(s: "_12 // true
    	println(isValidIdentifier(s: "")) // false
    	println(isValidIdentifier(s: "012 // false
    	println(isValidIdentifier(s: "no$ // false
    }
    
    so, let´s start with our function
        
        fun isValidIdentifier (s: String) : Boolean {
        	fun isValidCharacter(ch: Char) = 
        		ch == '_' ||
        		ch in '0'..'9' || //checks if it´s in the range from 0 to 9
        		ch in 'a'..'z' || //checks if it´s a letter in lowercase
        		ch in 'A'..'Z' //checks if it´s a letter in uppercase
        		
        	//check if the string is empty or if the first character is a digit
        	if(s.isEmpty() || s[0] in '0'..9') return false
        	
        	//now for every character in the string, we check if its a valid character, if one of them is not, then return false
        	for (ch in s) {
        		if(!isValidCharacter(ch)) return false
        	}
        	return true
        }
    	
`
	ok, now the results is what we expected
	this task was designed to exercise the use of ranges, but now we will rewrite it using the kotlin functions that help us with that:
    
    	  fun isValidIdentifier (s: String) : Boolean {
        	fun isValidCharacter(ch: Char) = 
        		ch == '_' ||
        		**ch.isLetterOrDigit() ** //checks if it´s a letter or digit
        		
        	//check if the string is empty or if the first character is a digit
        	if(s.isEmpty() ||** s[0].isDigit() **//false 
        	
        	//now for every character in the string, we check if its a valid character, if one of them is not, then return false
        	for (ch in s) {
        		if(!isValidCharacter(ch)) return false
        	}
        	return true
        }
	
### Solution: Sum as an extension function

in this task we will convert a function to a extension. it´s too easy in intelij IDE but you can also do it by hand:

here we have a function that returns the sum of a list of integers,
ex. if you pass (1,1,1) it will return 3

    fun sum (list: List<Int>) : Int {
    	var result = 0
    	for (i in list) {
    		result += i
    	}
    	return result
    }
    
    fun main (args: Array<String>) {
    	val sum = sum(listOf(1,2,3))
    	println( sum) //6
    }
	

very straightfoward

so let´s now covert it to an extension:
    
      fun** List<Int>.sum()** : Int {
        	var result = 0
        	for (i in **this**) {
        		result += i
        	}
        	return result
        }
        
        fun main (args: Array<String>) {
        	val sum = **listOf(1,2,3).sum()**
        	println( sum) //6
        }
	

At first, row function is defined as an extension, **so our list became the receiver**. Now, we access this list by** this** reference inside the function body, and also** the way how we call the function changed because now we call it as an extension.** It looks like it was a member.


### Nullable types
The problem of nullability is sometimes referred as billion dollar mistake. That's how Sir Tony Hoare the inventor of null reference later called his invention. 

The problem is that these null point exceptions problems **are really hard to fix** and even if you go for details, you often can see just this message: **"sorry null point exception was thrown"**. But where and why? 

The current approach, the **modern approach** which is not unique to cutling is to **convert these exceptions, from run-time exceptions to compile time errors**, to make it a compile time problems, **so that we could prevent these exceptions when we write the code and compile it rather than later in production**. Kotlin distinguishes nullable types and non-nullable types. 

#### nullable type in kotlin
 Kotlin distinguishes nullable types and non-nullable types. 
 
 If you use a regular type like string, you can **only store non-nullable objects there**, you can't store null references. 
 
** If you try to initialize a variable of a non-nullable type with null, the Kotlin compiler will complain**. 

If you want to **store null, you need to declare a variable of a nullable type**. 

To make a type nullable add a question mark **(?)** at end of his name.

ex:

    val s1 : String = "always not null"
    val s2: String? = null
    
In this example, after adding a question mark to string, you can store either **null or non-null** string value there.

now let´s see another example:

s1.length

if you try to dereference a variable of a non-nullable type namely access its members or call extensions everything is fine, just like we use s1, that will never be null.

The Kotlin compiler doesn't complain because it's sure that the exact value is not null. 

s2.length

However, if you try to dereference a variable of a **nullable type, the Kotlin compiler says it's not possible**. 

The value of the nullable type can be null under the hood, and such dereference operation will then **throw null pointer exception**.

#### What can you do if you want to dereference an object of a Nullable Type? 
The easiest way is to check explicitly that your reference is not Null. After such a check, you can simply dereference the variable and access its members. 
ex:

val s: String?

    if (s != null) {
    	s.length
    }

this will work fine, because it will only access the property length if the string value is not null

However, IDE, you will suggest you have a **better way to express the same logic**. You can replace the if expression with a safe access expression, just like this:
    
    s?.length
    

Safe access, or in other words, a safe call, consists of two characters: 

* The question mark and the dot (**?.**). 

It allows you to dereference a value in a safe manner. 

**This operator first checks whether the receiver is not null. If it is the case, then the safe access operator calls the required member and returns the result. If the receiver is null, then null becomes the result.**

When you use the result of a safe call like return it or assign it to a variable, that is the same as using the following explicit if expression.

what will be the type of the length value in this code?
    
    val s: String?
    val length: Int? = if(s != null) s.length else null
    
    val length: Int? = s?.length

There answer is nullable Int. 

The length property of String returns to you a variable of Int type.

But when you use safe access, that makes the results nullable. 

If a variable stores its value now, length will also be null, Because null might be stored only in variables of nullable types, the result type is nullable Int.

If you want to make the type of lengths **not nullable,** you need to provide the **default value for the case when s is null**. 

    val s: String?
    val length: Int = if(s != null) s.length else 0
    
    val length: Int = s?.length ?: 0

When using** if expression**, you can simply say else 0. 

When using **safe access**, you can use so called **Elvis operator** and provide the default value that will be used when your expression is null. 

#### Elvis operator
 elvis operator is something like this:
 val a = b ?: c
 
 it will assign to a the value of b if it isn´t null. it it is null, it will assign the value of c.
 


the next question is, what will be printed here?

    val a: Int? = null 
    val b: Int? = 1 
    val c: Int = 2
    
    val s1 = (a ?: 0) + c 
    val s2 = (b ?: 0) + c 
    print("$s1$s2")

 In the s1, we sum up 0 and 2, having 2 as a result. 
  val s1 = (a ?: 0) + c  //2
 
 In the s2, because b is not null, we sum up 1 and 2, having 3 as the result. 
  val s2 = (b ?: 0) + c  // 3
  
 So the answer to what will be printed is 23. 
  print("$s1$s2") // 23
 
 Let's now go back to our discussion of how we can work with expressions of Nullable types.
     
     val s: String?
     if(s == null) fail() // or use return instead of fail
	 s.lenght
 
 the Kotlin compiler supposed to the control flow analysis. If you explicitly check that the reference is null and co-fail function which throws an exception or simply return, then afterward you can accessed without safe access. 
     
     s.lenght
 
 The compiler knows that s verbal is smart cost to a null nullable type. 
 
 #### how to throw the null pointer exception in kotlin?
 If you want you can explicitly throw called the null pointer exception. 
 
 For this, you use this not null assertion (**!!**) , an operator consisting of two exclamation marks. 
 
 It throws a null pointer exception if it's operand is null and returns the operand if it's not null. 
 
 Note that after a not-null assertion, the value smart cost to a non-nullable type. And you can dereference it safely without the need to repeat this assertion. 
 
     s.length
 
 what happens is that the compiler already know that if it wasn´t throw a null pointer exception when we used **!!** it´s beacause the value is not null, so there is no need to check it again.
 
 ##### WARNING
** It's worth to warn against not-null assertion operator. By default, try to avoid it.** 

We have it in the language,** especially for other use cases where the Kotlin compiler isn't smart enough to infer the right time.**

There are situations when you have an assumption that the expression is not null but the kotlin compiler cannot infer that for you. And you would rather prefer an exception if for some reasons the assumption is not correct. 

The logic of assumption must then be localized so that it was hard to break it, or it can depend on external frameworks. 

    class MyAction {
    	fun isEnabled() : Boolean =
    		list.selectdValue != null
    		
    	fun action performed() {
    		val value = list.selectedValue!!
    		//..
    	}
    }
    
    if (action.isEnabled()) {
    	action.actionPerformed()
    }

In this example, the actionPerformed function is called only if the isEnabled function returns true. And we can safely use not-null assertion because the condition is checked is in another place. 

#### BAD USE OF NOT NULL ASSERTION

    person.company!!.address!!.contry

With not-null assertion operator, you explicitly emphasize where null pointer exception can be thrown. 

And if it's thrown, you can see directly what might be the cause. 

That means **it doesn't make sense to put two or more not-null assertion operators in one line**. 

As you won't to be able to say which one cause the exception. 

In general prefer using safe operators. Safe access. Elvis separator or explicit checks to cope with nullability. 

Use not null assertion only with care.

------------------------
now, lets see some more errors using null and not null

    #1 fun isFoo1(n: Name) = n.value == "foo"
    #2 fun isFoo2(n: Name?) = n.value == "foo"
    #3 fun isFoo3(n: Name?) = n != null && n.value == "foo"
    #4 fun isFoo4(n: Name?) = n?.value == "foo"
    
       fun main(args: Array<String>) { 
    #5   isFoo1(null)
    #6   isFoo2(null) 
    #7   isFoo3(null) 
    #8   isFoo4(null)
       }


The question for you to get used to nullable types is** which lines won't compile?** 
**Which lines will produce compiler errors?** 

Let's do it one by one. 
    
     #1 fun isFoo1(n: Name) = n.value == "foo"
     #5   isFoo1(null)
  
  The first function takes the parameter of non-nullable type. 
  The function is fine. But **the problem is that we can't pass null whenever a non-nullable type is expected.** 
  The compiler error tells us that null cannot be a value of a non-nullable type name here : "   *#5   isFoo1(**null**)*"
  If passing null to non-nullable parameter was allowed then we would have null point exception on the reference. The coding compiler doesn't allow that.
      
    #2 fun isFoo2(n: Name?) = n.value == "foo"
    #6   isFoo2(null) 
	 
'

Let's now take a look at the second function, which takes the parameter type null. 
Now, the implication is fine. It compiles. 

However, there is **an error in the function body**. 

Only safe calls or non-null asserted calls are allowed. You can't access expressions of nullable types without additional checks. 
it should be this way:

     #2 fun isFoo2(n: Name?) = n?.value == "foo"

So the line number two doesn't compile unless we use a null check
	 
    	 
    #3 fun isFoo3(n: Name?) = n != null && n.value == "foo"
    #7   isFoo3(null) 

The third function fixes this problem and this one is fine. We check explicitly that name is not null and then use smart cost value. 

    
    #4 fun isFoo4(n: Name?) = n?.value == "foo"
    #8   isFoo4(null)

The fourth function also compiles because we use safe access to get the value and then we compare it to the string, everything is fine thus the right answer is lines two and five don't compile.

--------------------------

Another question for you. This one is not trivial. Such code might be confusing and sometimes called a puzzler. What will be printed here?

val x: Int? = 1
val y: Int = 2
val sum = x ?: 0 + y
println(sum)


The answers are rather unexpected, keep that in mind. 
The possible options are **one, two or three.** 

The right answer is **one**. 

*Operator precedence plays an important role here*. 
    
    val sum = x ?: 0 + y

some operators take higher precedence than others 



If you need the parentheses, some operators take higher precedence than the other operators. 

That means that by default, the parenthesis surround plus, not Elvis operator.

so, as it is now, it works this way: 
0 + y and then it checks the elvis operator.
it´s like we have it like this:
    
        val sum = x ?: (0 + y)

**If you want to call Elvis separator first, then you put the parentheses explicitly. **
    
    val sum = (x ?: 0) + y


**If you are not sure about the right amount of precedence and to make the code more readable, prefer the parentheses in all such confusing use cases.** 


### Nullable types under the hood

Under the hood, nullable types are implemented using annotations.
@Nullable, @NotNull annotations

The Kotlin compilers simply adds **Nullable** and **NotNullable** annotations to the corresponding types usages. **Which gives us no performance overheads when using Nullable types**. 

There is another solution to the same Nullability problem which is called **Optional** or Option types. 

#### Optional objects
They are** special library classes that store value or absence of of the value and you can check whether the value is available or not**. 

That solves the same problem as nullable types because optional allow you to say explicitly whether the variable can have no value option similar to null or not. 

Despite nullable types and optional solve the same problem, **they are very different in terms of the performance**. 

**Optional** type is a **wrapper that stores the reference to the initial object**. 

For each optional value an **extra object is created**. 

At the same time, **nullable** types **don't create any wrappers**. 

They are implemented by annotations.

To make sure understand it answer these questions. 

**How many objects are created to store the value of a nullable string?** 

The answers options are either** two objects** or **only one**. 

*Only one object is created to store string value, there is no additional wrapper as with optionals.* 

When you use nullable types under the hood, the Kotlin compiler adds additional annotations which are only checked at the compilation time. 
    
    fun foo(): String = "foo"

is unde the hood
    
    @NotNull
    public static final String foo() {
    	return "foo";
    }

and 
    
    fun bar(): String? = "bar"

is under the hood
    
    @Nullable
    public static final String bar () {
    	return "bar";
    }


**At run time, nullable string is the same string as our Java string. **

Both types, string and nullable string corresponds to Java string type in Java, but with different annotations. A run time is one string, there is no wrap. 
All the checks going on at the compilation time with the help of annotations. 

That's the end of the first story. 

Now the story not about annotations but about nullability and generics. 

in case a, List<Int?> means that the list is created and never null. the content of the list is what changes. it can be Int or null.

so accessing list a, the values can be an integer or null.

now case b, List<Int>?, that means that the list can be null (never created) but since it was created, the values inside can only be integers and never null

with this in mind, you can see the difference between **a list of nullable elements and a nullable list**. 

When you use a list of ints, you can put the question mark after int, or after list itself, or in both places. 

The first one means that every element might be either null or not null. 

And the second one means the whole list might be either null or not null.


To better understand that mark the lines that need a question mark to make the code compile. Of course, you can add a question mark to each line to make every access save and to make every int nullable int, but that's not the question. **The question is which are the minimum amount of questions marks to make this compile**. Add only the question that are really needed.
    
      fun foo(list1: List<Int?>, list2: List<Int>?) { 
    #1  list1.size
    #2  list2.size
    
    #3  val i: Int = 
    #4    list1.get(0)
    #5  val j: Int = 
    #6    list2.get(0)
      }

answer:
    
    #2, #3, #5, #6


Let's do the cases one by one, 
* the first list is the list of nullable values, we can reference it without a problem because it's a not null reference. But when we try to assign the first element into a variable, we see an error. The inferred type is nullable int, but int was expected. The content of the list was nullable ints and the type of the first element nullable int. That means that we need to add a question mark to the type of the i variable. That's all for the first choice.

* For the second case, it's a little bit more complicated. We have a nullable list and that means that both accesses won't compile. We need here safe access, we can add a couple of question marks to fix that. And now here's the tricky place because we've added a question mark that makes line 6 uncompiled. We have the type mismatch, infer type is nullable int, but regular intervals expected. That makes us add another question mark to line 5.


So the answer is lies, 2,3, 5, and 6.


### exercise - isEmptyOrNull()
Add and implement an extension function 'isEmptyOrNull()' on the type String?. It should return true, if the string is null or empty.

answer:


    fun String?.isEmptyOrNull(): Boolean {
       if(this == null) {
           return true
       }else if(this.length == 0){
           return true
       }else {
           return false
       }
       
    }
    
    fun main(args: Array<String>) {
        val s1: String? = null
        val s2: String? = ""
        s1.isEmptyOrNull() eq true
        s2.isEmptyOrNull() eq true
    
        val s3 = "   "
        s3.isEmptyOrNull() eq false
    }
    
    
    
    //OK
    //OK
    //OK
	

### Safe casts

type cast: as
    
    if(any is String) {
    	val s = any as String
    	s.toUpperCase()
    }

In Java, you use a common pattern to do something with the variable only if it is of specific type. 

First, you use instanceof (or in the example above, 'is') to check whether the variable is of the required type, then you cast it to this type(as in above, any 'as' String) of restoring the result in a new variable (val s). 
Eventually, you call members of this type on this new variable. 

In Kotlin, you can do absolutely the same. 

'Is' is the analog of 'instanceof' and s is the typecast. 

However, the explicit cast s is not really needed. 

**You can simply use the initial variable afterward, because it's smart cast to the right type.** 
ex:
if (any is String) {
	any.toUpperCase()
}

In this case, you can** call String members on the any variable directly**. 

This example can be further improved. **You can replace type cast with a safe cast**. 

ex:
    
    (any as? String)?.toUpperCase()

#### Type Casts
**Type cast as, throws an exception if the expression can't be cast**, while** safe cast as question mark returns null in this case**. 

#### Safe Casts
**The safe cast returns either the smart cast value or null as the result.** 

If the value can be cast to the required type, then it is returned.

Another way to express the same logic is to use if expression explicitly returning either the same expression or null. 



### exercise Safe casts
Type cast as throws ClassCastException, if the cast is unsuccessful. Safe cast as? returns null, if the cast is unsuccessful. Declare the s variable to make the first line print null and the second one throw an exception.
    
    fun main(args: Array<String>) {
        val s = 1.0
        println(s as? Int)    // null
        println(s as Int?)    // exception
    }
    

result:
*null
Exception in thread "main" java.lang.ClassCastException: java.lang.Double cannot be cast to java.lang.Integer
 at FileKt.main (File.kt:4) 
 at sun.reflect.NativeMethodAccessorImpl.invoke0 (NativeMethodAccessorImpl.java:-2) 
 at sun.reflect.NativeMethodAccessorImpl.invoke (NativeMethodAccessorImpl.java:62) *
 


### Importance of nullability
"Why nullability is so important? 

Nullability in the type system is also one of the key features of Kotlin.

It's important because there are a lot of nulls around us. 

**The introduction of null to earlier programming languages, is known to be called "billion dollar mistake"**.  Because nulls are ubiquitous, NullPointerExceptions, attempts to dereference null pointers, are very common as an issue. Like, so many stack traces that you collect from any application will be NullPointerExceptions.

Of course, it's something that occurs so often, that it's worth controlling better. Like not overlooking such exceptions or at least possibility of having such an exception, makes a lot of sense. 

So, this is why we support a control for nullability in the type system itself and not like in a library or somewhere. 

We try to integrate this as a very small number of language features, that are tightly connected together. 

We have non-null and nullable types, and handful operators that help you work with nullability, plus there is smart cast and so on, so forth. 

This machinery makes it easy to control nulls and also makes 'null' a first-class citizen, basically in the language. Because, before, like if you don't have this controller, the type system, it's an outlaw: using nulls for representing absence of things is an anti-pattern. In Kotlin it's a legitimate pattern, you can use it because the type system helps you track it.

There is an important distinction in the approaches of tracking absences of things in different languages. One could think of creating like an 'Option' type for example, or 'Optional'. That's a class that wraps something and just represents existence or absence of something, Like an Optional of T, right? So, **the biggest difference between the nullable types in Kotlin and this Optional, is that in Kotlin, we don't have to wrap anything**. There is no extra object around your payload for one thing. Then, there was an important distinction regarding sub-typing. If you have a nullable type in Kotlin somewhere, then you can take a non-null value and simply assign there. With Optional, it doesn't work this way. If you have an Optional of String, you cannot simply assign a string into it, you have to wrap it first. Right. So, it makes many manipulations with types a lot smoother in Kotlin. 

I guess this is one of the most successful features in Kotlin. It's proven to be really useful and relevant one for real-life programming."


### Lambdas

**Lambda is an anonymous function that can be used as an expression**, for instance, passed as an argument to another function vacation. 
ex: 

    button.addActionListener { println("hi")}

In older versions of Java, anonymous classes were used for the same purpose. 

this java code:
    
    button.addActionListener( new ActionListener() {
    	@Override
    	public void actionPerformed(ActionEvent e) {
    		System.out.println("hi");
    	}
    })

can be replaced by:
    
    button.addActionListener { println("hi")};


Modern developed languages including Kotlin as well as Java starting from **Java 8**, support Lambdas which provide more concise syntax for the same functionality.

Having Lambdas in a language also makes it possible to work with collections in a functional style. 

You can use such functions as **filter** or **map** which make the overall code more readable. 

ex:
what´s an average age of employees working in Prague?
    
    val employees: List<Employee>
    
    data class Employee (
    	val city: City, val age: Int
    )
    
    employees.filter {it.city == City.PRAGUE}
    	.map { it.age} 
    	.average()
    	
    	

First, let's focus on the Lambda syntax. In Kotlin, **Lambda always goes in curly braces**. 
#### Lambda syntax
**{** x: Int, y: Int -> x + y **}**

To distinguish regular curly braces, for instance, for if expression, from curly braces used in Lambdas, IDE highlights in bold curly braces for Lambdas. 

When you see highlighted in bold curly braces, that means you see a Lambda. 

Inside curly braces, **first you specify the parameters**, then **the arrow**, then** the.Lambda body**. 

ex:
**{** x: Int, y: Int -> x + y **}**
x: Int, y: Int -- are the parameters
-> -- arrow
 x + y -- lambda body


If you pass a Lambda as an argument, you can put the whole Lambda inside the parentheses. 
ex:
list.any ({ i: Int -> i > 0})

that´s a full syntax of lambda

However, there is a better way to express that. 

**You can move Lambda out with parentheses, if the Lambda is the last argument**.
ex:
list.any () { i: Int -> i > 0}

**and if the parentheses are empty, you can omit them. **
list.any  { i: Int -> i > 0}

This way you have the nicer syntax. 

At first, the same syntactic convention of moving Lambda out of parentheses was used in groovy and it worked quite well there. Kotlin reuses the same idea which is proven to be really convenient. 

**If the type of the argument can be inferred, if it's clear from the context, it can be omitted. **
ex:
list.any  { i -> i > 0}

**If your Lambda has their own argument, you can replace its name with '*it*'. 
It's an automatically generated name for your Lambda, if it has only one argument, and you don't specify a different argument name. **
ex:
list.any  { it> 0}

**If you want to express some complicated logic and need a multi-line Lambda, then you just write several lines of code inside the parentheses. The last expression of this Lambda is the result. **

list.any  { 
	println("processing $it" )
	it> 0 -- *the last expression is the result*
}

I want to highlight another mostly syntactic feature. 

**If your Lambda takes a pair of values as an argument or as in this case map entry, you can use so-called destructuring syntax. **
ex:
map.mapValues { entry -> "${entry.key} -> ${entry.value} !" }

OBS: entry in this case use destructing declarations syntax instead


The same syntax was used to **iterate over a map** in a for loop, by assigning a key and a value to separate variables.

**Instead of declaring one Lambda parameter entry, you can declare two parameters at once by put them inside extra parentheses. **
ex:
map.mapValues { (key, value) -> "${entry.key} -> ${entry.value} !" }

The compiler will automatically destruct entry to key and value. 

That's quite convenient many functions take map entries in argument, and you can use this nicer syntax to work with such functions. 

**If one of the Lambda parameters is not used, you can replace its name with the underscore. **
map.mapValues { (**_**, value) -> "${entry.value} !" }

OBS: you can omit parameter name if the parameter is unused

It's more readable and you don't need to invent a name for the parameter if it's not used. 


### Common Operations on collections

As we've already discussed, the Kotlin standard library consists mostly of extensions on Java collections. 

A lot of these extensions work with the collections in a functional style and use lambdas. 

For instance, filter and map are defined in the Kotlin standard library as extension functions. 

Now, we'll discuss the most common operations and how exactly do they behave. 

#### Filter
initial list --- 1, 2, 3, 4
lambda --- { it % 2 == 0}
result list --- 2, 4

Let's start with filter.** It filters out the content of the list and keeps only their elements that satisfy the given predicate**. 

In this case, we have the predicate checking that a number is even and only even numbers that are present in the resulting list. 

#### Map
initial list --- 1, 2, 3, 4
lambda --- { it  * it }
result list --- 1, 4, 9, 16

**Map transform each element in a collection and stores all the resulting elements in a new list**. 

Here, we find the square of each given number and the result is a list of squares. 

Note to that, **the resulting list contains as many elements as the initial collection**. 

#### any (all, none)
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result list --- true
**There are several predicates checking whether the given facts about the elements are true**. 

##### any
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result  --- true

it´s true because at least one element of the list is true

For instance,** any checks that there is at least one element satisfying the given predicate, here, we check whether there is at least one even number in the list and the result is true.** 

##### all
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result  --- false 

**All checks whether all elements satisfy the predicate** 

##### none
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result  --- false 

**none makes sure that none of the elements satisfies the given predicate.** 

#### find
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result list --- 2

**Find finds an element satisfying the given predicate and returns it as a result. **

**If there is no required element, find returns null. **

You can use another name for the same predicate. This anonymous function is called **firstOrNull**. 

#### First / FirstOrNull
**FirstOrNull does the same as find**, it returns you an element or null as a result. 

**First takes a predicate and throws an exception if no elements satisfying the predicate was found.** 

#### count
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result  --- 2

**Count counts the number of elements that satisfy the given predicate**. 

#### partition
initial list --- 1, 2, 3, 4
lambda --- { it  % 2 == 0 }
result list 1  --- 2, 4
result list 2 --- 1, 3

**Partition divides the collection into two collections.** 

Filter returns only the elements that satisfy the predicate, and in a sense, throws out all the elements that don't satisfy the predicate. **If you need to keep both groups of elements that satisfy or do not satisfy the predicate, you can use the partition**. 

**It returns two collections, for the good elements and the remaining ones.** 

#### groupBy
initial list --- [{Alice, 31}, {Bob, 29}, {Carol, 31}]
lambda --- { it.age }
result list 1 (age 29)  --- {Bob, 29}
result list 2 (age 31) --- [{Alice, 31}, {Carol, 31}]

**If you need to divide your collection into more than two groups, you can use GroupBy**. 

**As an argument, you provide the way how to group the elements. **

What should be the grouping key? For instance, here we group personal elements by their age. 

The result is, map from the given key to a list of elements that satisfy this key. 

Here, **the result is a map from the age to a list of all people of this age**. 

This often the case that, as a result of grouping, **you'd prefer ONE element instead of a list**. 

If the** key is unique**, then it's **more useful to have a map of the key to this unique element as a result**. 

That's what they **associateBy** function does for you. 

#### associateBy
initial list --- [{Alice, 31}, {Bob, 29}, {Carol, 31}]
lambda --- { it.name }
result map 1  --- Alice - {Alice, 31}
result map 2  --- Bob - {Bob, 29}
result map 3 ---  carol - {Carol, 31}

It also performs groping, **but it returns you one element as the map value**. 

**Note that, associateBy should be used to run the keys unique.** 

**If it's not**, pay attention that** duplicates are removed**, so the last element will be chosen. 

If you key isn't unique, it's safer to use groupBy to avoid losing some of the elements. 

#### associate
initial list --- 1, 2, 3, 4
lambda --- { 'a' + it to 10 * it }
result map 1  --- a,10
result map 2 --- b, 20
result map 3 --- c, 30
result map 4 --- d, 40

**You can use as associate to build a map based on a list.** 

**As an argument, you pass allowed to creating the key value pair based on each list element, then associate builds a map by filling in specified keys and values.** 

The first value in a pair becomes key in the map, the second becomes the value. 

Here, a plus it specifies how to create keys, while 10 multiply, it is the way to create values. 

Note that, it's often convenient to use the least element as a key and provide a way to fetch the value in the lambda.

#### zip
initial list 1 --- 1, 2, 3, 4
initial list 2 --- a, b, c, d
result list of pairs --- [{1,a}, {2,b}. {3,c} , {4,d}]

**Zip provides you with a way to organize a couple of lists.** 

It zips like a zipper the elements from two lists. It returns you a list of pairs where each pair contains one element from the first list and another element from the second list.

IMPORTANT
**If their initial list have different sizes, then the resulting list of pairs will have the length of the shortest list, the remaining elements from the longest list will be ignored.**

#### zipWithNext
initial list 1 --- 1, 2, 3, 4
result list of pairs --- [{1,2}, {2,3}. {3,4}]

The frequent use case is to** zip neighboring elements in the list**. 

That can be done with the help of the zipWithNext function.
**It returns you a list of pairs where each pair consists of neighboring elements is from the initial list**. 

Note that, each element except the first and the last one will belong two pairs. Like three in this example list is the second element in the second pair and the first element in the third pair. 

Both zip and zipWithNext have overloaded versions taking a lambda as an argument that specifies how each pair of elements must be transformed. 


#### flatten
initial --- [ [a, b,c], [d, e], [f, g, h i] ]
result --- [a, b, c, d, e, f, g, h, i]

**Flatten is an extension function that must be called on a list of lists.** 

**It combines all the elements from the nested list and returns you a list of these elements as the result.** 

We can say, it flattens the list of lists contents. 

#### flatMap - combines map and flat
initial string 1 --- "abc"
initial string 2 --- "def"
apply **map**
result of map 1 --- [{a}, {b}, {c}]
result of map 2 --- [{d}, {e}, {f}]
apply **flatten**
result --- [{a}, {b}, {c}, {d}, {e}, {f}] 

Another useful function is flatMap. 

**It combines two operations, map and flat.** 

**The argument to flatMap must be a lambda that converts each initial element to a list**. 

Here, we first map each string into a list of characters. 

In the middle layer after applying the first map operations, we have at list of lists.

**Often, you'd prefer list of elements as a result instead and flatten does that. **

Here, flatMap returns a list of characters obtained from initial strings. 


### Operations Quiz - I

In this quiz, we'll use the class Hero. 
It has name, age, and gender properties. 
Gender might be male or female or if it is unspecified, then null is stored. 

    data class Hero(
    	val name: String,
    	val age: Int,
    	val gender: Gender?
    )
    
    enum class Gender {MALE, FEMALE}

We will use the following values that are specified in the list. Your tasks for most of the questions will be to find the result of the expression. These heroes are based on the card game, Lifeboat. 
    
    val heroes = listOf (
    	Hero("The Captain", 60, MALE),
    	Hero("Frenchy", 42, MALE),
    	Hero("The Kid", 9, null),
    	Hero("Lady Lauren", 29, FEMALE),
    	Hero("First Mate", 29, MALE),
    	Hero("Sir Stephen", 37, MALE)
    )

#### last()
The first task is to find the result of this first expression. 

    heroes.last().name

The answer is Sir Stephen. 

We obtain the last element in the list and, then we get his name. 

The Kotlin Standard Library contains useful functions. 

**First**, **last**, also **firstOrNull**, and **lastOrNull**. 

* **First and last throw an exception if there are no elements.**

* **FirstOrNull and lastOrNull return null if the list is empty. **

All these functions are overloaded and are available as the functions with predicates. 

Here, we use at the last function without arguments. 
But there is a similar one that takes a Lambda as an argument. 

For instance here, what is the result? 
    
    heroes.firstOrNull { it.age == 30 }?.name

The result is null because there is no elements satisfying the given predicate. 

There is no hero of age 30. 

FirstOrNull returns null. Then we use safe access and null is returned as the result of the whole expression. 

If we use the first function with the predicate, then we'll get no such element exception as a result. 
    
    heroes.first { it.age == 30}.name
    //NoSuchElementException

**First must return no nullable element**. 

So when there is no required element, it can only throw an exception. 

#### distinct()
The next question uses the function that we haven't yet discussed, but I think you can guess what it is doing by its name. 
    
    heroes.map { it.age }.distinct().size


**Distinct function returns only the elements which are distinct, different. **

Let's see step-by-step what is going on in this example.

First, we map the heroes to a list of their ages. 

//[60, 42, 9 , 29, 29, 37]

Then we call distinct on it. 

//[60, 42, 9 , 29, 37]

It returns a new list which contains only **non-repetitive** elements. 

In this case, the duplicate of 29 was removed. 

At last, we get the size of the resulting list which is five. 

#### filter { }
The next question uses the filter function. 
    
    heroes.filter { it.age < 30 }.size


Here, filter returns all the heroes whose age is less than 30.

There are three such elements so the result is three. 

#### partition { }
The next question is about partition. 

**We use the partition function that divides the list of elements into two lists.** 
    
    val (youngest, oldest) = heroes.partition { it.age < 30 }
    oldest.size

* **The first list contains the elements that satisfy the predicate, heroes that are younger than 30. **

8 **The second list contains all the rest elements, heroes that are not younger than 30**. 

In our case, the size of both lists is three. 

#### maxBy {} , minBy{}
The next question employs the function maxBy. 
    
    heroes.maxBy { it.age }?.name

You can use **maxBy** and **minBy** functions if the elements are not comparable themselves, but they can be compared by a property or in another specified way. 

Here, we compare elements by comparing the corresponding values of the age property. 

We find the maximum by comparing ages. 

**This maxBy function returns the first element with the maximum value of the property or null if the collection is empty**. 

Here, we find the oldest Hero which is The Captain. His name is the result. 

#### all { }
The next question is about predicates. 
We use all function. 
    
    heroes.all { it.age < 50 }
	
The result is false. 

**We check whether all the heroes are younger than 50.** 

That's not true because we have The Captain who is older. 

#### any { }
The next question is about the any predicate. 
    
    heroes.any { it.gender == FEMALE }

The answer is **true**. 

We check whether any element in the collection satisfies the given predicate. 

There is the hero, Lady Lauren, which specifies female gender, as it therefore, satisfies this predicate.



### Operations Quiz - II

Let´s continue the quiz. 

#### groupBy { }
The next question uses the function groupBy. 
    
    val mapByAge: Map<Int, List<Hero>> = 
      heroes.groupBy { it.age }
    val (age, group) = mapByAge.maxBy { (_, group) -> 
      group.size
    }!!
    println(age)

What is printed here? 

Let's look at this example step-by-step and understand what's going on here. 

**val mapByAge: Map<Int, List<Hero>> = 
      heroes.groupBy { it.age }**

When we group elements by their ages, the groupBy returns a **map from the age to a list of heroes of this age**.
ex:
**mapOf( 
	60 to listOf (Hero("the captain", 60, MALE)),
	42 to listOf (Hero("frenchy", 42, MALE)),
	9 to listOf (Hero("the kid", 9, null)),
	29 to listOf (
		Hero("Lady Lauren", 29, FEMALE),
		Hero("first mate", 29, MALE)),
	37 to listOf (Hero("sir stephen", 37, MALE))
)**


Then we call maxBy on the resulting map. 
ex:
**val (age, group) = mapByAge.maxBy { (_, group) -> 
      group.size
    }!!
    println(age)**

It finds the entry with the maximum value of the provided expression. 

In this case, group size. 

Here, the maximum group size is two elements for the age 29. 

Thus, it makes By function will return 29 as the age, and the highlighted list as the corresponding group. 

Group print age 29. 


#### associateBy { }
The next question uses the function associateBy. 
    
    val mapByName: Map<String, Hero> = 
      heroes.associateBy { it.name }
    mapByName["Frenchy"]?.age

Now, regroup the elements by their names, by using their **associateBy** function. 

In our case, the name property is a unique key. 

The resulting map is the map from name to hero object where it says the element by the name friendship, and get his age. 

He's 42. 

I want to highlight here two different ways to access elements in a map. 

#### access elements in a map
You can either use **square brackets**, or map** getValue** function to access the specific element. 
ex:
**mapByName["Frenchy"]?.age** // 42
or
**mapByName.getValue("Franchy").age** // 42

OBS:
**The access via square brackets can return null as a result. **

Here, you see that to access age later we use save collaborator. 
**mapByName["Frenchy"]*?***

**GetValue function, will throw 'noSuchElementException'**, if there is no such element.

You don't need to use safe access afterward, but you see that the exception might be thrown.
**mapByName.getValue("Franchy").age**

#### getOrElse( ) { }
The next example builds a map using the associate function and illustrate how getOrElse works. What is the result of the last expression? 
    
    val mapByName = heroes.associateBy { it.name }
    val unknownHero = Hero("Unknown", 0, null)
    mapByName.getOrElse("unknown") { unknownHero }.age

The **associate** function builds a **map** creating a **key value pair** from each element in the list. 

In this case, it builds a map from string from names to ages. 

**The getOrElse function returns the value corresponding to the given key, if the key is present in the map. **

**Otherwise, it computes the provided Lambda and returns the result of this Lambda. **


It's a very useful function because if the element is already present in the map, then nothing will be computed.

The default value pass inside of the Lambda will be calculated only if needed. 

In these case, it's needed and the getOrElse function returns zero since unknown key is not present in the map.

#### BAD PRACTICE -- BAD CODE HARD TO READ
The next question is much less straightforward than the previous ones. It tries to illustrate how the code **should not be written with Lambdas**, is an example of batch code which is hard to read. 

You can spend some time trying to understand what's going on here and guess the answer. 

    val (first, second) = heroes
      .flatMap { heroes.map { hero -> it to hero } } 
      .maxBy { it.first.age - it.second.age }!!
    first.name


Let's gradually note what are the problems here. 

* At first, we used **it** in two neighboring clients but **it in the first line has a different type from it in the second line**. 

ex:
   .flatMap { heroes.map { hero -> **it** to hero } } 
      .maxBy { **it**.first.age - **it**.second.age }!!

We have the same name because of this syntactic convention that you can replace one argument with it, but these arguments in two different Lambdas have different types, and that is really confusing. 

**Just don´t write code like this**. 


To fix that, let's replace the first it with an explicit parameter, and then try to understand what's going on. 

    val (first, second) = heroes
      .flatMap { first -> 
	  		heroes.map { hero -> first to hero } } 
      .maxBy { it.first.age - it.second.age }!!
    first.name


We call flatMap on heroes. 

At first, it builds a list of pairs corresponding to each hero, then it flattens all the pairs.

Let's replace hero parameter name with second to highlight that we are building **pairs of heroes**. 
      
       val (first, second) = heroes
          .flatMap { first -> 
    	  		heroes.map { second -> first to second } } 
          .maxBy { it.first.age - it.second.age }!!
        first.name

**The list corresponding to the first element, the captain, will contain all combinations of two hero elements where the captain is the first element. The similar list will correspond to the second element branch and so on. **

ex:
"The Captain" to "The Captain"
"The Captain" to "Frenchy"
...
"The Captain" to "Sir Stephen"

	"Frenchy" to "The Captain"
	"Frenchy" to "Frenchy"
	...
	"Frenchy" to "Sir Stephen"
		...
						"Sir Stephen" to "The Captain"
						"Sir Stephen" to "Frenchy"
						...
						"Sir Stephen" to "Sir Stephen"



The unification of all such lists and flattening it will produce the list of all possible pairs. 

Thus the flatMap code here:
**heroes
.flatMap { first -> 
heroes.map { second -> first to second } } **
constructs the least of all possible pairs of heroes. 

Now, we can extract it to a variable and give it the explicit name, all possible pairs. 

**val allPossiblePairs = heroes
.flatMap { first -> 
heroes.map { second -> first to second } } **
val (first, second) = allPossiblePairs
	.maxBy { it.first.age - it.second.age } !!
first.name

Now, it's easier to understand what's going on here. This code is better. 

Now, let's continue and look at the next line. 
**val (first, second) = allPossiblePairs
	.maxBy { it.first.age - it.second.age } !!
first.name**


We call **maxBy** on all possible pairs. 

The maxBy function returns a nullable pair which will then assign to two variables (**first** and **second**), similar to how we assigned an pair to two variables. 

We need not an assertion here to make the resulting pair nullable to be able to the structure and assign it in this way.  So we can continue to use the 'it'

 **it**.first.age - **it**.second.age

**MaxBy finds the maximum of all differences in ages of two heroes in one pair**. 

But maximum of the age differences will be reached for pair consisting of the oldest and the youngest heroes.

Basically, this **first** and **second** are just **oldest** and **youngest**. 

ex:
**val (oldest, youngest) = allPossiblePairs
	.maxBy { it.first.age - it.second.age } !!
first.name**

The maximum difference in ages gives us the maximum and the minimum ages. 

**The whole piece of code might be replaced with finding the oldest and the youngest heroes. **

ex:
val (oldest, youngest) = allPossiblePairs
	.maxBy { it.first.age - it.second.age } !!
first.name

can be replaced by:
ex:
**val oldest = heroes.maxBy {it.age }
val youngest = heroes.minBy {it.age }
oldest.name**


Since we don't really use the youngest in this example, we can only find the oldest, excluding the val youngest

**val oldest = heroes.maxBy {it.age }
oldest.name**

His name is the captain and that's the result that is printed.

The main point of this task, was to **illustrate an example of badly written code so that in the future you could avoid it**, and try to write your code so that it was readable and comprehensible. 

To sum up what we saw in this last example, there are some pieces of advice on what could be done in order to improve readability. 

* At first, we have this problem with 'it' variable. Try not to use it if it has different types in neighboring lines. The it parameter name is good if the Lambda is trivial and straightforward. But if it's going to be more complicated, for instances, in module and Lambdas, it's often better to use explicit parameters. 
* In any case, when any confusion is possible, prefer using explicit parameter names so that the code was easier to understand. 
* It´s a good idea to learn the library to know it and not try to re-implement all the methods. Is often possible to find the function that will do the job for you. 


### Interchangeable predicates challenge

Functions '**all**', '**none**' and '**any**' are interchangeable, you can use one or the other to implement the same functionality.

Implement the functions '**allNonZero**' and '**containsZero**' using all three predicates in turn.

'allNonZero' checks that all the elements in the list are non-zero; 'containsZero' checks that the list contains zero element.

Add the negation before the whole call (right before 'any', 'all' or 'none') when necessary, not only inside the predicate.

    
    fun List<Int>.allNonZero() =  all { it != 0 }
    fun List<Int>.allNonZero1() =  none { it == 0 }
    fun List<Int>.allNonZero2() =  !any { it == 0  }
    
    fun List<Int>.containsZero() =  any { it == 0 }
    fun List<Int>.containsZero1() =   !all { it != 0 }
    fun List<Int>.containsZero2() =  !none { it == 0}
    
    fun main(args: Array<String>) {
        val list1 = listOf(1, 2, 3)
        val list2 = listOf(0, 1, 2)
        list1.allNonZero() eq true
        list2.allNonZero() eq false
        list1.allNonZero1() eq true
        list2.allNonZero1() eq false
        list1.allNonZero2() eq true
        list2.allNonZero2() eq false
        list1.containsZero() eq false
        list2.containsZero() eq true
        list1.containsZero1() eq false
        list2.containsZero1() eq true
        list1.containsZero2() eq false
        list2.containsZero2() eq true
    }


### Function Types

Now, you'll learn about function types. We'll also discuss how you can pass Lambda as an argument to Java method, and also touch a topic of function types and probability. 

#### function type

val sum = { x: Int, y: Int -> x + y }

In Kotlin, you can store Lambda in a variable like above, but you can specify which type does the variable have, like this:

val sum **(Int, Int) -> Int** = { x, y -> x + y }

If we specify this type explicitly, we'll see a so-called function type. 

this means that sum receives 2 parameters of type Int ((Int, Int)) and returns an Int (**-> Int**). 


First, parameter types are written inside the parentheses and then an arrow, then the return type. 

In this case, is the type that takes two integer parameters and returns an integer as a result. 

so, if we have this:

val isEven = {i: Int -> i % 2 == 0} 

What will be the type of isEven variable here? 

it will be** (int) -> Boolean**

so we can write this lambda this way:

**val isEven: (Int) -> Boolean =  {i: Int -> i % 2 == 0} **

In this case, we have a Lambda that takes Int as a parameter and returns Boolean as a result, you can see the corresponding function type. 

Note the difference between storing a Lambda and storing the result of applying this Lambda. 

**val isEven: (Int) -> Boolean =  {i: Int -> i % 2 == 0} ** -- stores the lambda

**val result: Boolean = isEven(42)** // true -- stores the result of the application of the lambda passing the parameter, in this case, 42


* **Lambda is the whole function containing the logic of how to compute the Boolean result from the given Int argument**, 

* **the result, in this case,  is simply a Boolean value. **

You can call a variable of function type as a regular function, providing all the necessary arguments. 

In this case, you call a variable is even as it was a regular function isEven(). 

To call a Lambda stored in a variable might be convenient if you want to postpone calling a Lambda, store it somewhere and call it on later. 

**When you store a Lambda in a variable, you can pass this variable whenever an expression of function type is expected**. 

val isEven: (Int) -> Boolean =  {i: Int -> i % 2 == 0}

val list = listOf(1, 2, 3, 4)
**list.any(isEven)** //true
**list.filter(isEven)** [2,4]

For instance, to all the functions working with collections in a functional style like any or filter. 

#### calling directly a lambda
You can even call a Lambda directly, putting parentheses right after lambdas curly braces, like this:

{ println("hey") } **()**

**However, such invocation looks a bit strange**. 

If you need to call a Lambda right in place, better user run.

**run** { println("hey") }

The version with run does exactly the same, but it's much more readable than the code above. 

#### SAM interfaces in java

    void postponeComputation (int delay, Runnable computation)

**In Java, you can pass a Lambda instead of a SAM interface**, an interface with only one single abstract method. 

**SAM means Single Abstract Method**
and have this structure:
    
    public interface Runnable {
    	public abstract void run();
    }

#### Mixing Kotlin and Java -- lambdas
In Kotlin, you can use the function types directly, but when you mix Kotlin and Java, you'd want to do the same as in Java. 

Whenever you call a method that takes SAM interface as a parameter, you can pass a Lambda as an argument to this method instead, like this:

**postponeComputation(1000) { println(42) }**

In Kotlin, if you want to create an instance of such interface explicitly, you can use the **outer generated SAM constructor** like in this case, a runnable and pass a Lambda as its only argument. 

**val runnable = Runnable {}**

#### functions types of lambdas and nullability
Now, let's talk about function types and nullability. 

I want to highlight the difference between **function type that returns nullable value** and **nullable function type**. 

**( ) -> Int?** vs **(( ) -> Int)?**

To better understand that, answer, which lines here don't compile? 
    
    #1 val f1: () -> Int? = null
    #2 val f2: () -> Int? = { null } 
    #3 val f3: (() -> Int)? = null
    #4 val f4: (() -> Int)? = { null }
    

What is the difference between these types? 

**( ) -> Int?** vs **(( ) -> Int)?**

* The first one means that, return type is nullable. That's a possible mistake when you simply add a question mark after the function type. It means that you make the return type of this function type nullable, not the whole type itself.

* the second one, is the whole type nullable, and to use that, you need to use the parentheses around the type of the lambda. 

#### lambda returning null
    
     val f2: () -> Int? = { null } 
In the example, you saw null in curly braces. 

**It's a Lambda without arguments that always returns null.** 
    
    val f3: (() -> Int)? = null
this line shows that **the variable which can store either null reference** or **Lambda returning Int value**. 

Let's go back to the task. 
    
    val f1: () -> Int? = null

**this line doesn't compile** because you can't store null in a variable of a non nullable type. 

**To store null, you need to declare a variable of a nullable type** as in here:  
    
    val f3: (() -> Int)? = null
----------
    
    val f2: () -> Int? = { null } 

This line is fine because you have here a Lambda that can't return nullable Int. 

The Lambda in this line always returns null, so it fits. 

-------
val f4: (() -> Int)? = { null }
**This line doesn't compile** because the compiler expects the Lambda that returns only integer values. 

But here, we tried to assign there a Lambda which returns null, that is not allowed, instead of assingning a null value like this:

**val f4: (() -> Int)? =  null **

#### working with a nullable function type 
    
    val f: (() -> Int)? = null

You can ask, how you should call a variable of a nullable function type? 

You can't call it as a regular function because it's nullable.

So which options do you have? 

    if( f != null) {
    	f()
    }

You can **check the variable explicitly for being not null**, then you can simply call it because smart cast applies here and the value is smart cast to the value of non nullable type. 



An alternative is to **use the safe access syntax**, 
    
    f?.invoke()

but in this case, you call a variable of function type by calling its **invoke** function. 


Each variable or function type can be called by invoke, but regularly you don't need that since there is a simpler alternative, **the syntax to call it directly**. 

### Member References

Now, you'll learn about member references, and we'll discuss what is the difference between bound and unbound references. 

#### member references
    class Person(val name: String, val age: Int)
    people.maxBy { it.age }

Like Java, Kotlin has member references, **which can replace simple Lambdas that only call a member function or return a member property**, it can convert Lambda to member reference automatically when it's possible, like this:

** people.maxBy { it.age }**
*convert lambda to reference*
** people.maxBy { Person::age }**

The syntax for member reference is the same as in Java.

#### syntax
**First goes the class name, then the double colon, then the member which we refer. **

As we've previously discussed in Kotlin, **you can store Lambda in a variable, however, you can't store a function in a variable. **

**val isEven: (Int) -> Boolean = { i: Int -> i % 2 == 0 }**


**It's not like in a truly functional language where each function is a variable. **

No, in Kotlin **there is a clear distinction between functions and variables**, that are connected with how JVM works under the hood. 

#### you can´t store a function in a variable

**fun isEven (i: Int) : Boolean = i % 2 == 0**
val predicate = **isEven**

this won´t compile.


**If you try to assign a function to a variable, you'll get a compiler error**. 

To fix this issue, use the function reference syntax. 

**Function references allow you to store a reference to any defined function in a variable to be able to store it and call it later.**

so, like in the example above, that won´t compile, you have to do this:

**val predicate = ::isEven**

now it will compile.

Keep in mind that this syntax is just another way to call a function inside the Lambda, underlying implementation are the same. 

so, this:
**val predicate = ::isEven**
is the same as this:
**val predicate = { i: Int -> isEven(i) }**


Here, the full analogous syntax is a Lambda that only calls is even faction. 

If a reproach member is a **property**, or it's a **function that takes zero or one argument**, then *member reference syntax isn't that concise in comparison with the explicit Lambda syntax*. 

However,** if the reproached function takes several arguments, you have to repeat all the parameter names as Lambda parameters, and then explicitly pass them through**, that makes this syntax robust. 
    
    val action = { person: Person, message: String -> sendEmail(person, message) }
    
    val action = ::sendEmail

Member references allow you to hide all the parameters, because the compiler infers the types for you, just like above.

#### passing function reference as an argument
    
    fun isEven (i: Int) : Boolean = i % 2 == 0
    
    val list = listOf (1, 2, 3, 4)
    list.any(::isEven)  //true
    list.filter(::isEven) // [2, 4]

You can **pass a function reference as an argument**, whenever your Lambda tends to grow too large and to become too complicated, it makes sense to extract Lambda code into a separate function, then you use a reference to this function instead of a huge Lambda. 

so, imagine that the isEven lambda is a big one, there is no need to replicate it here
**list.any(::isEven)  //true**
and
**list.filter(::isEven) // [2, 4]**

#### Bound and non-bound references
bound means that the referece has a bound to an instace of a object, that it only exists correctly for that specific instance of the object. other instance of the same object will have a different value, so it has another bound.

non-bound refereces means that the reference is a global reference, not attached to the instance itself but attached to the object type.
    
    class Person (val name: String, val age: Int) {
    	fun isOlder (ageLimit: Int) = age > ageLimit
    }
    
    val agePredicate = Person::isOlder // stored the function by reference (regular non-bound reference)
    
    val alice = Person("Alice", 29)
    agePredicate(alice, 21)  // true // called the function stored, passing the arguments required, in this case, the instanciation of the Person object (alice) and the value for comparison required by the function

Now, I want to highlight the difference between bound and non-bound references. 

In Kotlin, **you can create a bound reference**, let's us discuss what it is. 

In the example above, we use a regular non-bound reference, which refers to a member of the person class. 

If we check what type this member reference has, we see that the first argument of the function type is person.
so, this:
  ** agePredicate(alice, 21) **
   
   is equal as having:
    ** agePredicate : (Person, Int) -> Boolean = Person::isOlder**


Whenever we want to call this variable of function type, we need to pass the person instance explicitly. 

If we look under the hood and check what Lambda does correspond to this member reference, we'll find that this Lambda takes two arguments, person and age limit:
 
 ** agePredicate : (Person, Int) -> Boolean = { person, ageLimit -> person.isOlder(ageLimit) }**

it simply calls the member function isOlder inside on the person element. 

This reference is called **non bound**, since it's **not bound to any specific instance, you can call it on any object of the person class.** 

so, no-bound references you have to pass the object instance as an argument to have it´s result.


**Bound reference is a member reference that is attached to a specific instance of the class.** 
so going back to this:


    
    class Person (val name: String, val age: Int) {
    	fun isOlder (ageLimit: Int) = age > ageLimit
    }
    
    val agePredicate = Person::isOlder // stored the function by reference (regular non-bound reference)
    
    val alice = Person("Alice", 29)
    agePredicate = alice::isOlder  // true 

Here, the **alice variable is an instance of the class person, and you can bound member efforts to these specific instance.** 

If we look at the type of the bound member reference:

val agePredicate: **(Int) -> Boolean** = alice::IsOlder

we see that now there is **no person parameter because the person instance is already set**, the isOlder function takes int as a parameter, and the bound reference also expect only int as an argument. 

If we check which Lambda corresponds to this member reference to the hood, we'll find the Lambda that calls the member is older on the bound instance.

val agePredicate: (Int) -> Boolean = **{ ageLimit -> alice.isOlder(ageLimit) }**

In this case, this bound instance is Alice variable. 

#### Bound to 'this' reference

class Person (val name: String, val age: Int) {
	fun isOlder(ageLimit: Int) = age > ageLimit
	
	fun getAgePredicate() = this::isOlder
}

Member reference can be bound to these reference. 

Here, we'll return a predicate directly from the class person. 

This predicate is a member reference to isOlder function, where 'this' is the object of which this member reference is bound to, and is usual for these we can emit it, like this:

    fun getAgePredicate() = ::isOlder

Now, we have this nice short syntax **without left-hand side**, just reference to the member. 

To make sure you understand it, answer the question, what is the type of this member reference here? 
We have two options, either taking person or without person as an argument. 
    
    class Person(val name: String, val age: Int) {
      fun isOlder(ageLimit: Int) = age > ageLimit
      fun getAgePredicate() = ::isOlder
    }


The right answer is '(Int) -> Boolean', it is a bound reference which stores the person of this instance inside, the reference will always be bound to a specific instance of the person class. 

We can call getAgePredicate only at the specific instance, like this:
    
    val predicate = alice.getAgePredicate()

which becomes the bound object for member reference.

Now the question for you, is isEven in this example a bound reference or not? Yes or no are the possible answers.
    
    fun isEven(i: Int): Boolean = i % 2 == 0
    
    val list = listOf(1, 2, 3, 4) 
    list.any(::isEven) 
    list.filter(::isEven)
    

The answer is no, because here it's just a reference to a top-level function. 

There is no stored object in which this function is bound to.

**Whenever you see the function and reference without the left-hand side, it's either a reference to a top-level function or a bound reference. **

In IDE you can always navigate and see which faction that this function reference refers to, it's a very convenient. 

Now you can use both bound and unbound references in your code. 

Bound reference store the object on which the member can be later called, while not bound reference can be called on any object of a given type. 


### return from Lambda

Now, you'll learn what does **return** expression inside the lambda do, why it works like that, and how to safely use it for your purposes. 

Let's start with an example that sometimes might be really confusing. It's a puzzler, so you can expect something surprising as a result. 
    
    fun duplicateNonZero(list: List<Int>) : List<Int> {
    	return list.flatMap {
    		if ( it == 0) return listOf()
    		listOf (it, it)
    	}
    }
    
    println(duplicateNonZero( listOf (3, 0, 5)))

The duplicate non-zero function is intended to duplicate all the elements except zero. 

The question is, what does it produce as a result?

You can try to guess what's going on and later we'll discuss the details. 

The options are:
- [[3, 3], [], [5,5]]
- [3, 3, 5, 5]
- []

The right answer here is an empty list which is really unexpected. 

You can easily write similar code and expect this function to print duplicated non-zero elements.

Let's see what's going on here. 

**'Return' Kotlin always returns from a function marked with fun. **

That sound, you may consider as a rule. 

It explains an empty list here as a result. 

When the function finds the '0' element, it returns an empty list but** it returns an empty list from the whole function**. 

in other words, the return keyword will always return for the function, so when it get´s to the '0' it will return a empty list as the function result.


That's why an empty list is printed out as a result. 

Let's discuss why it works this way. 

#### why 'return' returns from function?
Why in Kotlin 'return' returns from the outer function? Consider the following example when you have a regular for loop and inside this for loop you use return. 
    
    fun containsZero(list: List<Int>) : Boolean {
    	for (i in list) {
    		if( i== 0) return true
    	}
    	return false
    }

**Return simply returns from the function. **
it´s like you saying: 

**if any of the elements of this list is '0', stop processing and return the value true, because in the list exists a number that is equal to zero.**

If you convert the for loop to foreach, then you can expect that return continue to behave in the same way. 
    
    fun containsZero(list: List<Int>) : Boolean {
    	list.forEach {
    		if( it == 0) return true
    	}
    	return false
    }


Return inside foreach returns from the whole function as well. 

In this scenario, we are glad that return returns from the whole function not from the lambda. 

That explains the motivation of a white box like this. 

A lot of functions in Kotlin like forEach behave like language constructs and we want to provide such almost language construct experience. 

What can you do if you need to return from an lambda instead of the function? 

#### return from the lambda, not the function
You can use the labels returns syntax. 
    
    list.flatMap {
    	if(it == 0) return@flatMap listOf<Int>()
    	listOf (it, it)
    }

**Here, the labeled return will return from the corresponding lambda (return@flatMap). **

By default, you can use the name of the function that calls this lambda as a label, like in the example, we use flatMap so we can use @flatMap.

#### solution using labels
But if you want, you can specify any label name put it right before the lambda followed by at sign. 

    
    list.flatMap k@{
    	if(it == 0) return@k listOf<Int>()
    	listOf (it, it)
    }

Here we provided the custom name just K to label the Lambda. 

You then use this name in a labeled Return. 

Now that duplicate non zero function implementation uses labels, each returns, what do we expect? 

The flattened least of duplicated non zero numbers.

[3, 3, 5, 5]

#### solution using local function
There is another solution to the same problem. 

Instead of lambda, you can use a local function and then pass the reference to this local function. 
    
    fun duplicatesNonZeroLocalFunction (list: List<Int>) : List<Int> {
    	fun duplicateNonZeroElement(e: Int): List<Int> {
    		if (e == 0) return listOf( )
    		return listOf( e, e)
    	}
    	return list.flatMap(::duplicateNonZeroElement)
    }
    
    println ( duplicateNonZeroLocalFunction ( listOf (3, 0, 5)))
    
    [3, 3, 5, 5]
    
In this case, return behaves as expected.

It returns from the local function marked with the fun keyword. 

so, it return the emptyList when the element is zero, but when flatMap joins all the result lists, it rejects the empty one generated by the '0' element.
it worked like a 'continue', when passing by the elements, not returning from the outer function, but returning from the inner function and continuing to the next element in the list.

#### solution using anonymous function

Now, the alternative solution is to use an anonymous function. 

If you don't want to invent a name for a local function, you can use an anonymous function instead. 

    
    fun duplicatesNonZero (list: List<Int>) : List<Int> {
    	return list.flatMap( fun (e) : List<Int>{
		if ( e == 0 ) return listOf()
		return listOf( e, e)
	})   
}
    
    println ( duplicateNonZero ( listOf (3, 0, 5)))
    
    [3, 3, 5, 5]

You can define an anonymous function in place, similar to the lambda when you pass it as an argument.

In essence, it's simply an alternative syntax for lambdas. 

**under the hood, the implementation compiled bytecode will be the same for lambda and an anonymous function, and the only difference is syntactic. **

You can now use a return which returns from the anonymous function marked with the fun keyword. 

What's more you can specify the return type for an anonymous function which is not possible for a lambda. 

#### another solution -- no 'return'
Sometimes, it's possible to simply avoid using  'return'. 

fun duplicateNonZero (list: List<Int>) : List<Int> {
	return list.flatMap {
		if (it == 0)
			listOf()
		else 
			listOf(it, it)
	}
}

println (duplicateNonZero (listOf (3, 0, 5)))

[3, 3, 5, 5]


**In this case, we use the result of if instead of return and we get what we expect as a result. **

#### does labeled return inside forEach correspond to break or continue inside a for loop?

What do you think does labeled return inside foreach correspond to break or continue inside for loop? 

it corresponds to 'continue'.

**so, when used inside a forEach loop, when it encounters the 'return' keyword, it will behave like a continue in a for loop and continue to the next element.**


Breaks stops the for loop completely while continue stops only the current iteration and goes to the next one. 

Like continue, return from a lambda only stops the current iteration, the current lambda, but doesn't stop the whole loop.

**Note that the regular return doesn't correspond to break. **

They are the same only if the forEach iteration or for loop is the last statement in the function. 

Otherwise, they differ in whether this statement is following right afterword are called. 

so this:
    
    fun foo (list: List<Int>) {
    	list.forEach {
    		if(it == 0) return
    		print (it)
    	}
    	println("###") //won´t be printed if list contains 0
    }

IS NOT THE SAME AS:
    
    fun bar (list: List<Int>) {
    	for (element in list) {
    		if(element == 0) break
    		print(element)
    	}
    	println("###") // this will be printed because when element == 0 it will exit the for loop and continue processing
    }

Return returns from the whole function, while break completes only the for loop iteration. 

There is no direct analogs to break other than extracting the for each call to a separate function. 

This explanation of how to use return inside lambda completes our discussion of functional programming so far. 

	
### Is Kotlin a functional language?

Would you call Kotlin a functional language? 

Well, it's not so easy to define what a functional language is for practical purposes. 

Kotlin is definitely not a purely functional language like Haskell for example.

Modern mainstream languages tend to combine ideas from different paradigms, and Kotlin does so as well. 

So, we have OOP ideas, we have structural ideas, we have functional programming ideas combined in the same design. 

So, when you're using classes and interfaces, you're on the OOP side. But at the same time when you're using our function types and lambdas, and other functional features of Kotlin, you are doing something functional already.

I would say it's more of a style issue, so it's not about being a functional language but it's about enabling the functional style of programming. 

For example, Kotlin promotes immutable data, so you are encouraged to use immutable things. 

But immutable things are also first-class citizens in Kotlin, you can use them freely whenever you like, it's a matter of style.

So, I would say if you rely on immutability, if you use higher-order functions, and lambdas, and function types of course, you're doing Kotlin in the functional style. 

And it's very often beneficial, so I totally recommend it.


	
### Nice String
A string is nice if at least two of the following conditions are satisfied:

It doesn't contain substrings bu, ba or be;
It contains at least three vowels (vowels are a, e, i, o and u);
It contains a double letter (at least two similar letters following one another), like b in "abba".
Your task is to check whether a given string is nice. Strings for this task will consist of lowercase letters only. Note that for the purpose of this task, you don't need to consider 'y' as a vowel.

Note that any two conditions might be satisfied to make a string nice. For instance, "aei" satisfies only the conditions #1 and #2, and ```"nn"` satisfies the conditions #1 and #3, which means both strings are nice.

Example 1
"bac" isn't nice. No conditions are satisfied: it contains a ba substring, contains only one vowel and no doubles.

Example 2
"aza" isn't nice. Only the first condition is satisfied, but the string doesn't contain enough vowels or doubles.

Example 3
"abaca" isn't nice. The second condition is satisfied: it contains three vowels a, but the other two aren't satisfied: it contains ba and no doubles.

Example 4
"baaa" is nice. The conditions #2 and #3 are satisfied: it contains three vowels a and a double a.

Example 5
"aaab" is nice, because all three conditions are satisfied.

Run TestNiceString to check your solution.
    
    
    package nicestring
    
    fun String.isNice(): Boolean {
        var conditionsSatisfied = 0
    
        if(!conditionContainsSubstrings(this)) {
            conditionsSatisfied += 1
        }
    
        if(conditionContainsVowels(this)) {
            conditionsSatisfied += 1
        }
    
        if(conditionDoubleLetter(this)) {
            conditionsSatisfied += 1
        }
        return conditionsSatisfied >= 2
    }
    
    fun conditionDoubleLetter(s: String): Boolean {
        for (i in s.indices) {
            if(i == 0) continue
            if(s[i] == s[i - 1]) return true
        }
        return false
    }
    
    fun conditionContainsVowels(s: String): Boolean {
        var vowelCounter = 0
        s.forEach {
            when (it) {
                'a', 'e', 'i', 'o', 'u' -> {
                    vowelCounter += 1
                }
            }
        }
        return vowelCounter >= 3
    }
    
    fun conditionContainsSubstrings(s: String): Boolean {
        return s.contains("bu") || s.contains("ba") || s.contains("be")
    }
    
### Solution: Nice String

the response i gave in the above topic, it´s one solution which works and passes all the tests but doesn't use the full power of the Kotlin functional features. 

It represents what can be submitted as a solution. 

Let's try to improve it and make it more functional. 

So, let´s see if we can improove it further.

#### check if a string doesn´t contain another string

i´ve made it this way:
    fun conditionContainsSubstrings(s: String): Boolean {
            return s.contains("bu") || s.contains("ba") || s.contains("be")
        }
    

 Let's improve this solution and start with the first condition. 
 
 Here, we check that a string doesn't contain any of the specified substrings.
 
Instead of repeating this check for every substring, we can put all the substrings in a set and then check the condition for each element in the set. 
    
    val noBadSubstrings = setOf("ba", "be", "bu").all { !this.contains(it) }
    

so, this compares the original string (this) to all of the strings in the set (it)

For all the substrings, the following must be satisfied. 

The initial string doesn't contain this substring. 

**this** refers to the string, receiver of the function, to string itself and it refers to each of the substrings in turn. 

We use not in the condition, but one exclamation mark is often not very noticeable. 

Thus, we can use another predicate that doesn't need this exclamation mark.

Instead of all, we can use none. It performs the same check. None of the substrings is the part of the initial strength. 

    
    val noBadSubstrings = setOf("ba", "be", "bu").none { this.contains(it) }
    


These are our improved results for the first check. 

#### count the number of vowel letters in a string
For the second check, we need to count the number of vowel letters.

i have done it this way:
    
    var vowelCounter = 0
            s.forEach {
                when (it) {
                    'a', 'e', 'i', 'o', 'u' -> {
                        vowelCounter += 1
                    }
                }
            }
            return vowelCounter >= 3
    		

But instead of checking every vowel letters separately, we can again put them all in a set. 
    
    val hasThreeVowels = count {
    	it in setOf('a', 'e', 'i', o', 'u') } >= 3
    

Then we can check for each character in the initial string whether it belongs to this set or not. 

If it's a vowel, we count it. 

We can simplify this logic even more and check whether a character belongs to a string consisting of all vowel letters.

    
    val hasThreeVowels = count {
    	it in "aeiou" } >= 3
	

**Probably, the check for belonging to a set is slightly better in terms of performance** but since we only have five characters, that's not a noticeable difference. 

We are mostly interested in how to make the code more readable now and this last version looks really nice. 

#### check if a letter is equal than the next letter in a string
    
     for (i in s.indices) {
                if(i == 0) continue
                if(s[i] == s[i - 1]) return true
            }
            return false
    		

well, i have complicated a little bit. Let's see what we can do here. 

We need to check whether a string contains a double letter. 

At first, we can work with indexes directly. 

We check all the indexes in the string by saying from zero to the last index. For each index, we get two characters. By **this** index and by the **next** one, and compare these two neighboring characters.
    
    var hasDouble = ( 0 until lastIndex).any { this[it] == this[it + 1]}
    
In this way, we compare all pairs of neighboring characters and find the result. 

But there must be a better way to express that.

You can use the **zipWithNext** function.

ZipWithNext zips each character in a string with the next character and returns a list of pairs. 

Each pair consists of two neighboring characters. 

To check that there are two similar letters following one another, you simply check that there is a pair with two equal characters. 

Specifically, you check that the first element in the pair equals the second element. 
    
    var hasDouble = zipWithNext().any { it.first == it.second }
    

ZipWithNext works for lists of any elements. 

There is also another possible solution using the function specific for strings, I mean the windowed function. 

#### windowed function
    
    val str = "abcdefg"
    
    str.windowed(4) //[abcd, bcde, cdef, defg]
    
    str.windowed(3) //[abc, bcd, cde, def, efg]
    
    str.windowed(2) //[ab, bc, cd, de, ef, fg]
    
**The windowed function returns a list of slices of the given size obtained from the initial string.** 

You can see the results for the slices of the size four, three, and two. 

Note that you can also specify a step between the **starting points** of the neighboring slices. 
    
    str.windowed(2, step = 4) // [ab, ef]
    
    str.windowed(3, step = 4) // [abc, efg]
    


**If we get the slices of the size two, it gives us basically the same result as zipWithNext, but as a list of strings not a list of pairs. **

--------------------

To solve the initial task, we do a similar thing. 

We check whether the first character in the string equals the second one which is also the last one.
    
    var hasDouble = windowed(2).any { it[0] == it[1] }
    
Both solutions are possible.

I'll pick the one with the zipWithnext as a result. 

Note that we no longer need the mutable variable now because double is val. 
    
    val hasDouble = zipWithNext().any { it.first == it.second }
    
	
It's only one line of code instead of the whole for loop. 

#### counting conditions with result true
At last, we need to count the number of satisfied conditions. 

so what have i done?

each time a condition was true, it incremented the variable conditionsSatisfied
    
    conditionsSatisfied += 1
    

this solution can be further improved. 

There are many ways to solve this last part.

You can count the numbers explicitly like here or you can write several if errors expressions but that will be code repetition.

The nicer way to do it would be to build a list of all the conditions, a list of three Boolean values, and see how many true values this list contains. 

Let's try to use filter for that. 

For each Boolean element, you check whether it's true or false and you are only interested in true values. Then you get the size of the resulting list and compare it with two. 
    
    return listOf(noBadSubstring, hasThreeVowels, hasDouble).filter { it == true}.size >= 2

**Note that you can filter simply it, you don't need to compare it with true since the least element is a Boolean value. **
    
    return listOf(noBadSubstring, hasThreeVowels, hasDouble).filter { it }.size >= 2


However, there is one more important improvement. 

**You can replace the combination of filtering size with only one function count. **

    
    return listOf(noBadSubstring, hasThreeVowels, hasDouble).count { it } >= 2


It counts the number of true values among our Boolean conditions in one iteration. 


That's our resulting function. 

You can see how we simplified this solution and how much shorter it became.

### Taxi Park
The TaxiPark class stores information about registered drivers, passengers, and their trips. Your task is to implement six functions which collect different statistics about the data.

Task 1
fun TaxiPark.findFakeDrivers(): Collection<Driver>
Find all the drivers who didn't perform any trips.

Task 2
fun TaxiPark.findFaithfulPassengers(minTrips: Int): List<Passenger>
Find all the clients who completed at least the given number of trips.

Task 3
fun TaxiPark.findFrequentPassengers(driver: Driver): List<Passenger>
Find all the passengers who were driven by a certain driver more than once.

Task 4
fun TaxiPark.findSmartPassengers(): Collection<Passenger>
If we consider "smart", a passenger who had a discount for the majority of the trips they made or took part in (including the trips with more than one passenger), find all the "smart" passengers. A "smart" passenger should have strictly more trips with discount than trips without discount, the equal amounts of trips with and without discount isn't enough.

Note that the discount can't be 0.0, it's always non-zero if it's recorded.

Task 5
fun TaxiPark.findTheMostFrequentTripDurationPeriod(): IntRange?
Find the most frequent trip duration period among minute periods 0..9, 10..19, 20..29, and so on. Return any suitable period if many are the most frequent, return null if there're no trips.

Task 6
fun TaxiPark.checkParetoPrinciple(): Boolean
Check whether no more than 20% of the drivers contribute 80% of the income. The function should return true if the top 20% drivers (meaning the top 20% best performers) represent 80% or more of all trips total income, or false if not. The drivers that have no trips should be considered as contributing zero income. If the taxi park contains no trips, the result should be false.

For example, if there're 39 drivers in the taxi park, we need to check that no more than 20% of the most successful ones, which is seven drivers (39 * 0.2 = 7.8), contribute at least 80% of the total income. Note that eight drivers out of 39 is 20.51% which is more than 20%, so we check the income of seven the most successful drivers.

To find the total income sum up all the trip costs. Note that the discount is already applied while calculating the cost.

response:
    
    package taxipark
    
    /*
     * Task #1. Find all the drivers who performed no trips.
     */
    fun TaxiPark.findFakeDrivers(): Set<Driver> {
        if(this.trips.isEmpty()) {
            return this.allDrivers
        }
    
        val setDriverWithTrips = mutableSetOf<Driver>()
    
        for (trip in this.trips) {
            setDriverWithTrips.add(trip.driver)
        }
    
        val setFakeDrivers = mutableSetOf<Driver>()
    
        for (driver in this.allDrivers) {
            if(setDriverWithTrips.none{it == driver}) setFakeDrivers.add(driver)
        }
    
        return setFakeDrivers
    }
    
    /*
     * Task #2. Find all the clients who completed at least the given number of trips.
     */
    fun TaxiPark.findFaithfulPassengers(minTrips: Int): Set<Passenger> {
        val mapPassengerQtyTrips = mutableMapOf<Passenger, Int>()
    
        for (passenger in this.allPassengers) {
            mapPassengerQtyTrips[passenger] = this.trips.filter { it.passengers.contains(passenger) }.count()
        }
    
        return mapPassengerQtyTrips.filter {
            it.value >= minTrips
        }.keys
    }
    
    
    /*
     * Task #3. Find all the passengers, who were taken by a given driver more than once.
     */
    fun TaxiPark.findFrequentPassengers(driver: Driver): Set<Passenger> {
        val listTrips = this.trips.filter { it.driver == driver }
    
        val mapPassengerQtyTrips = mutableMapOf<Passenger, Int>()
    
        for (passenger in this.allPassengers) {
            mapPassengerQtyTrips[passenger] = listTrips.filter { it.passengers.contains(passenger) }.count()
        }
    
        return mapPassengerQtyTrips.filter { it.value > 1 }.keys
    }
    
    /*
     * Task #4. Find the passengers who had a discount for majority of their trips.
     */
    fun TaxiPark.findSmartPassengers(): Set<Passenger> {
        val mapPassengerQtyTrips = mutableMapOf<Passenger, Int>()
    
        for (passenger in this.allPassengers) {
            mapPassengerQtyTrips[passenger] = this.trips.filter { it.passengers.contains(passenger) }.count()
        }
    
        val mapPassengerQtyTripsWithDiscount = mutableMapOf<Passenger, Int>()
    
        for (passenger in this.allPassengers) {
            mapPassengerQtyTripsWithDiscount[passenger] = this.trips.filter { it.passengers.contains(passenger) && it.discount != null }.count()
        }
    
        val result = mutableSetOf<Passenger>()
    
        for (passenger in this.allPassengers) {
            val qtyTrips = mapPassengerQtyTrips[passenger]
            val qtyTripsWithDiscount = mapPassengerQtyTripsWithDiscount[passenger]
            if(qtyTripsWithDiscount!! >  (qtyTrips!! - qtyTripsWithDiscount)) result.add(passenger)
        }
    
        return result
    }
    
    /*
     * Task #5. Find the most frequent trip duration among minute periods 0..9, 10..19, 20..29, and so on.
     * Return any period if many are the most frequent, return `null` if there're no trips.
     */
    fun TaxiPark.findTheMostFrequentTripDurationPeriod(): IntRange? {
        if (this.trips.isEmpty()) return null
    
        val mapRangeQty = mutableMapOf<IntRange, Int>()
    
        val maxDuration = this.trips.maxByOrNull { it.duration }?.duration
        for (i in 0..maxDuration!!) {
            val start = i * 10
            val end = start + 9
    
            mapRangeQty.put(IntRange(start, end), this.trips.filter { it.duration in start..end }.count())
        }
        return mapRangeQty.maxByOrNull { it.value }?.key
    }
    
    /*
     * Task #6.
     * Check whether 20% of the drivers contribute 80% of the income.
     */
    fun TaxiPark.checkParetoPrinciple(): Boolean {
        if (this.trips.isEmpty()) return false
    
        val mapDriverTotalIncome = mutableMapOf<Driver, Double>()
        var totalAmountByAllDrivers = 0.0
    
        for (driver in this.allDrivers) {
            val trips = this.trips.filter { it.driver == driver }
            var totalAmount = 0.0
    
            for (trip in trips) {
                totalAmount += trip.cost
            }
            mapDriverTotalIncome[driver] =  totalAmount
            totalAmountByAllDrivers += totalAmount
        }
    
        val mapDriverTotalIncomeSorted =  mapDriverTotalIncome.toList().sortedByDescending { (_, value) -> value}.toMap()
    
        val qtyTopDrivers = (this.allDrivers.size * 20) / 100
    
        var amountTopDrivers = 0.0
    
        var counter = qtyTopDrivers
    
        for (map in mapDriverTotalIncomeSorted) {
            if(counter == 0) break
            amountTopDrivers += map.value
            counter --
        }
    
        return ((amountTopDrivers * 100) / totalAmountByAllDrivers) >= 80.0
    
    }
    
    
### Solution: Taxi Park, tasks 1-3

Let's discuss how we can solve the taxi park assignment. 

The first task is to find the drivers that didn't perform any trips. There are two basic ways to solve this task. You can use either drivers or trips as a starting point.

The first solution starts with all drivers, and you filter out those drivers who performed some trips.

The drivers without trips stay in the resulting list. 

#### filter one list with results from another list
    
    allDrivers.filter { d -> trips.none { it.driver == d}}.toSet()
    

Finally, you need to convert it to a set because it requires set as a result. 

In the second case, you find the drivers that performed some trips and then you subtract the resulting collection from set of all drivers. 
    
    allDrivers.minus(trips.map {it.driver})
    
Thus you get the drivers that performed no trips.

    
    allDrivers - (trips.map {it.driver})
    

Note that in Kotlin, you can use minus syntax directly instead of calling the minus function. 

We'll discuss the details of how exactly it works in the next module.

**Note that the second solution, subtracting the drivers that performed some trips from the set of all drivers, is slightly better since it does only one iteration via map. The first solution calls none for each driver. **

In the worst-case scenario, the number of iterations will then be the multiplication of the number of drivers and the number of trips.

However, the difference between these two solutions isn't that noticeable for not the worst-case scenario. 

----------------

The second task is to find faithful passengers. 

The passengers that performed at least the required number of trips.

There again two basic ways to solve this task. 

Either start with trips, or start with passengers. 

Let's look at two sample solutions and try to improve them. 
    
    trips
    	.flatMap { it.passengers } //all passengers in trips list
    	.groupBy { it }
    	.filter { it.value.size >= minTrips}
    	.map {it.key }
    	.toSet()
    

The first solution starts with trips. 

At first, we use flatMap to get the list of all the passengers that made some trips.

**Each passenger is present in this list as many times as the number of trips he or she performed**. 

Then by grouping the same passengers elements, we can find how many trips each passenger performed. 

The solution works and passes all the tests; however, it's not very readable. 

**It makes the common readability mistake. **

**It uses several it in neighboring lines and it in different lines have different types. **

Because of that, it's not clear what's going on here.

It's counter-intuitive that the variable of the same name will have different types and different meanings in indifferent lines. 

How we can improve that? 

In the first case, I would convert Lambda a reference. 
    
    	.flatMap(Trip::passengers)
    
**Then it's clear that we get passengers for each trip. **

When we group it, I would rather say passenger, passenger. 
    
    	.groupBy { passenger -> passenger }
    
There is nothing wrong in repeating it if it improves the readability. 

Then I would again introduce an explicit parameter for it, on the filter line.


Here it, is map entry, but we are only interested in the value of this entry to access the group of equal passengers elements.
    
    	.filter { (_, group) -> group.size >= minTrips }
    
I would say that everywhere destruction declaration syntax is better than one variable for entry.

We don't use key here, so we can replace its name with underscore.

This exactly use case might be also simplified.

**Filter can be replaced with filter values**, and now we have group as the only argument. 
    
    	.filterValues { group -> group.size >= minTrips }
    
The last simplification. 

Instead of first transforming entries to the keys, and then converting the resulting list to a set , you can access keys directly.
 so you change this:
     
    	.map {it.key }
        .toSet()

into only this:

	.keys

------------------
    
    allPassengers
    	.partition { p ->
    		trips.sumBy { t ->
    			if (p in t.passengers) 1 else 0
    		} >= minTrips
    	}
    	.first
    	.toSet()
    
The second solution starts with the list of passengers and keeps only those who satisfy the given predicate. 

This solution uses functional features but it somehow over uses them. 

For instance, it uses partition here where filter would be null.

**Partitions splits the initial list of passengers into two lists.** 

But then only the first list is later used. 

There is no sense to use partition if you are interested only in one of the parts. 

so the code will look like this:
    
    allPassengers
    	.filter { p ->
    		trips.sumBy { t ->
    			if (p in t.passengers) 1 else 0
    		} >= minTrips
    	}
    	.toSet()
    

You have the specific filter function for that. 

By the way, if you're interested in the remaining part in the elements that do not satisfy the given predicate, you can use filterNot. 

Then, this solution uses a rather complicated way to count the number of passengers that satisfy the given condition, as seen here:

  		trips.sumBy { t ->
    			if (p in t.passengers) 1 else 0
    		} >= minTrips

It sums either zero or one, depending on whether a passenger took part in a specific trip. 

The direct way to express that is to use count, like this:
    
    trips.count { p in it.passengers } >= minTrips

There's our final solution. 

    
    allPassengers
    	.filter { p ->
    		trips.count { p in it.passengers) >= minTrips
    	}
    	.toSet()
    


It simply uses filter and count.

That was my simplification for the solutions. 


------------------

The next function finds all the passengers who performed more than one trip, with a specific driver. 

Again, you can start either with passengers or with trips. 

Since the solutions are very similar to the previous task, I'm only showing the improved versions.

solution 1:
    
    trips
    	.filter { trip -> trip.driver == driver}
    	.flatMap ( Trip::passengers)
    	.groupBy { passenger -> passenger }
    	.filterValues { group -> group.size > 1 }
    	.keys

solution 2:
    
    allPassengers
    	.filter { p ->
    		trips.count { it.driver == driver && p in it.passengers} > 1
    	}
    	.toSet()

### Solution: Taxi Park, tasks 4 & 5

Now let's talk about the next task finding smart passengers. 

The passengers who pay from the majority of their trips with a discount. 

I will start with some sample solution first and we'll try to improve them. 

Let's look at the first solution.
    
    val pair = trips.partition { it.discount is Double }
    return allPassengers
    	.filter { passenger ->
    		pair.first.count { it.passengers.contains(passenger) }
    	}
    	.toSet()
    
Here we petition the whole list with of trips into two list. 

The first one contains all the trips with the discount, and the second contains the trips without discount. 

**Note that the partition result is stored in a pair here**. 

And given the variable is called simply pair, it's not at all obvious what is stored inside. 

We need to check the variable type explicitly. 

It's always better to use decoration syntax with partition and give meaningful names to the variables rather than use pair.

In this case we'll do trips with discount and trips without discount. so it will be like this:

    
    val (tripsWithDiscount, tripsWithoutDiscount) = trips.partition { it.discount is Double }
    return allPassengers
    	.filter { passenger ->
    		tripsWithDiscount.count { it.passengers.contains(passenger) } > tripsWithoutDiscount.count {
			it.passengers.contains (passenger)}
    	}
    	.toSet()
    

Then we apply filter to all the passengers and for each passenger compare the number of trips he or she made with discount and without discount. 

Only the passengers with the majority of the trips with discount remain. 

Another thing I want to highlight the solution is using is Double check for basically checking something for being not null, like here:
    
    = trips.partition { it.discount is Double }

The more easy and straightforward check you can apply the better, so it is better this way:
    
    val (tripsWithDiscount, tripsWithoutDiscount) = trips.partition { it.discount != null }
    return allPassengers
    	.filter { passenger ->
    		tripsWithDiscount.count { it.passengers.contains(passenger) } > tripsWithoutDiscount.count {
			it.passengers.contains (passenger)}
    	}
    	.toSet()
    

Try not to overcomplicate things.

The intention might be not clear when you use is Double here, you automatically as the reader assumes that it's not just null-able types and believes much probably something else like integer,
so other types that's confusing.

**The most straightforward way to check something for being not null is unsurprisingly just to check for being not null without overcomplication.**

The last thing we can improve here is to replace contains call with in.

    
    val (tripsWithDiscount, tripsWithoutDiscount) = trips.partition { it.discount != null }
    return allPassengers
    	.filter { passenger ->
    		tripsWithDiscount.count { passenger in it.passengers) } > tripsWithoutDiscount.count {
			passenger in passengers}
    	}
    	.toSet()
    

In also checks whether you element belongs to a collection or list. 

Under the hood in calls contains, so basically they are the same.

We can even navigate in and see that indeed contains is called. 

After you get used to it in looks more concise.

--------------

Now let's look at the alternative solution. 
    
    allPassengers
    	.groupBy (
    		{ it },
    		{ p -> trips.filter { t -> p in t.passengers } }
    	)
    	.entries
    	.filter {
    		val group = it.value.first()
    		val (withDiscount, withoutDiscount) = group
    			.partition { it.discount != null }
    		withDiscount.size > withoutDiscount.size
    	}
    	.map { it.key }
    	.toSet()
    

It's a bit overcomplicated solution. 

But it can exist, I will suggest just some small improvements here.


We start with allPassengers and build the maps storing all the trips performed by each passenger, in here:

    
    allPassengers
    	.groupBy (
    		{ it },
    		{ p -> trips.filter { t -> p in t.passengers } }
    	)

Then for each passenger we can pair the number of trips with the discount that here she made with the number of of trips without a discount, like here:

.entries
    	.filter {
    		val group = it.value.first()
    		val (withDiscount, withoutDiscount) = group
    			.partition { it.discount != null }
    		withDiscount.size > withoutDiscount.size
    	}
		
In the end, we keep only the passengers that have more trips with the discount.

    	.map { it.key }
    	.toSet()
    

Let's see which we can improve here.

The used groupBy function is the overloaded version of groupBy which takes not only the key selector as an argument, but also the way to fetch the value. 

In this way, instead of grouping the elements, we group the transformed values. 

The result is a map from a passenger to all the trips he or she performed. 

Note that groupBy here is probably not the best choice, because the key passenger is unique. 

But groupBy doesn't know that, and returns a map from passenger to a list of list of trips.

To avoid this list of list of elements as the result value, it's better to use associateBy function.

associateBy returns a map from key to the correspondent value directly. 

Note that we no longer need to call first letter to get the first element. 
    
    allPassengers
    	.associateBy (
    		{ it },
    		{ p -> trips.filter { t -> p in t.passengers }}
    	)
		.entries
		.filter {
			val group = it.value.first
			...
		

**First** was used here because the med value is released with only one element. 

So **first** was used to get this element.

Now it's no longer needed.

    
    allPassengers
    	.associateBy (
    		{ it },
    		{ p -> trips.filter { t -> p in t.passengers }}
    	)
		.entries
		.filter {
			val group = it.value
			...
		


But for this usecase, I would rather use another function, not associateBy but simply associate.

It takes one lambda as an argument. 

    
    allPassengers
    	.associate { p -> 
		p to trips.filter { t -> p in t.passengers }
    	}
		.entries
		.filter {
			val group = it.value
			...
		

You specify the pair from key to value which builds the values in the resulting map. 

In our case, the key is the passenger, and the value is all the trips that this passenger made.

This way it's a bit more readable.

The next simplification for the solution concerns this **entries** line.



Associate returns as map and entries returns as set of address.

But you rarely need to convert a map to a collection of entries of pairs since the majority of operations are available from maps directly.

Instead of converting a map to a list of entries, you can call filter on a map directly, so we can remove the 
    
    .entries

Then I would replace it with explicit parameter, because it's not that clear what is the type of it, like this:
    
    .filter { entry -> 
    	val group = entry.value
    	val (withDiscount, withoutDiscount) = group
    	.partition ...
    
    
Then I would use distraction declaration index instead of entry.

Since we use only entry value we don't need a separate variable for entry key. 

And as we've already seen at the previous task, we can use filterValues instead, so it will be like this:
    
    .filterValues { (_, group)  ->
    	val (withDiscount, withoutDiscount) = group
    	.partition ....
    

First we grouped the transformed values then we filtered map contains. 

    
    .filterValues {  group  ->
    	val (withDiscount, withoutDiscount) = group
    	.partition ....
    
	
At last we're interested in the set of keys in the resulting map. 

so, we change this:
    
    	.map { it.key }
        	.toSet()

to this:
    
    .keys

As before, we can directly use keys instead of mapping keys and calling to set.

It's important to understand the difference between groupBy and associateBy. 

**Prefer associate or associateBy if your key is unique.**

-------
The last solution tries to be very concise. Probably too concise.
    
    allPassengers.filter { p -> trips.count { t -> p in t.passengers && t.discount != null} > trips.count { t -> p in t.passengers && t.discount == null}}.toSet()


Don't strive to put the whole function at one line. 

Even if we can do it doesn't mean you should. 

In this case is really unreachable.

Even if you have a huge monitor reading it from another place is inconvenient. 

Even if you use self drops intelligent feature which might be switched on by view active editor use of traps, it's still not readable in comparison with a properly formatted solution. 

After we've be formatted this solution it became better. 

Don't neglect their possibility to extract variables with clear names.

Even if you can't make this solution very concise and functional is important not to lose readability. 

And good variable names can great help to understand what's going on in a piece of code. 
    
    allPassengers.filter { p -> 
    	val withDiscount = trips.count { t -> p in t.passengers && t.discount != null}
    	val withoutDiscount =trips.count { t -> p in t.passengers && t.discount == null}
    	withDiscount > withoutDiscount
    }.toSet()

Here we count the number of trips with discount and without discount for each passenger and compare these numbers. With clear names, the intention is easier to understand in comparison with version when you in line all the expressions. 

The resulting function is much better than the initial version written in one line.

---------------------

The next function findTheMostFrequentTripDurationPeriod. 

Again, I will show you a sample solution which we'll improve.
    
    return trips
    	.groupBy { it.duration / 10 * 10..it.duration / 10 * 10 + 9 }
    	.toList()
    	.sortedByDescending { it -> it.second.size }
    	.firstOrNull
    	?.first

Here we start with trips. 

Then we group trips by the duration period. 

However, there is a small repetition here. You repeat the expression of find the start of the duration. 

Extracting it into a variable and giving it a clearer name helps to understand what's going on here.

instead of this:
    
    .groupBy { it.duration / 10 * 10..it.duration / 10 * 10 + 9 }

we have this:
    
    .groupBy { 
    	val start = it.duration / 10 * 10
    	start..start + 9 }

I would also introduce another variable. 

    
    .groupBy { 
    	val start = it.duration / 10 * 10
		val end = start + 9
    	start..end }


And here now it's more clear that you group your trips by the range from start to end.

Another thing I sometimes find on the code, I don't really understand why someone uses this syntax. 

You define a separate parameter name for lambda but you name it as it. 
    
    .sortedByDescending { it -> it.second.size }

That's not needed, if the name of your parameter is clear from the context, simpler and meet the parameter name it use it inside.
    
    .sortedByDescending { it.second.size }
    
In this case, another it refers to a trip in the other line. 

But here it means something else, so it's better to introduce a new name. 

Or whenever you see such, it -> syntax, you either base it with a specific name or leave only it inside.

We even have the inspection for that which tell redundant lamda arrow. 

Don't ignore such inspections. 

If they work wrong for your use case file an issue which the Kotlin team will fix but don't ignore the suggestions.
    
    .sortedByDescending { (_, group) -> group.size }

Note that to list here which converts a map to at list is needed because there is no sorted function on a map. 
    
    .toList()

toList returns list of entries as a list of pairs. 

Because we are only interested in the second value, we again can use distraction declaration syntax and specify the explicit name.

Each group of trips corresponds to the specific trip duration.

Another simplification here. 

There is no need to use sortedByDescending only to find the first value. 

    
    .sortedByDescending { (_, group) -> group.size }


Basically what we are doing here is where finding maximum. 

You don't need to sort all the rest element when you just need to the first value. 

Max or maxBy well be more perfomant for that. 

    
    .maxBy { (_, group) -> group.size }


And you can call maxBy directly on a map.

so we ended like this:

    
    return trips
    	.groupBy { 
			val start = it.duration / 10 * 10
			val end = start + 9
			start..end
			}
    	.maxBy { (_, group) -> group.size }
    	?.key

### exercise Taxi Park. Pareto Principle

Complete the implementation of the function 'checkParetoPrinciple'.
This function should check whether no more than 20% of the drivers contribute 80% of the income. It should return true if the top 20% drivers (meaning the top 20% best performers) represent 80% or more of all trips total income, or false if not. The drivers that have no trips should be considered as contributing zero income. If the taxi park contains no trips, the result should be `false`.
For example, if there're 39 drivers in the taxi park, we need to check that no more than 20% of the most successful ones, which is seven drivers (39 * 0.2 = 7.8), contribute at least 80% of the total income. Note that eight drivers out of 39 is 20.51% which is more than 20%, so we check the income of seven the most successful drivers.
To find the total income sum up all the trip costs. Note that the discount is already applied while calculating the cost.
    
    
    fun TaxiPark.checkParetoPrinciple(): Boolean {
        if (trips.isEmpty()) return false
    
        val totalIncome = trips.sumByDouble(TODO())
        val sortedDriversIncome: List<Double> = trips
                .groupBy(TODO())
                .map { (_, tripsByDriver) -> tripsByDriver.sumByDouble(TODO()) }
                .sortedDescending()
    
        val numberOfTopDrivers = (0.2 * allDrivers.size).toInt()
        val incomeByTopDrivers = sortedDriversIncome
                .take(TODO())
                .sum()
    
        return incomeByTopDrivers >= 0.8 * totalIncome
    }
    
    fun main(args: Array<String>) {
        taxiPark(1..5, 1..4,
                trip(1, 1, 20, 20.0),
                trip(1, 2, 20, 20.0),
                trip(1, 3, 20, 20.0),
                trip(1, 4, 20, 20.0),
                trip(2, 1, 20, 19.0))
                .checkParetoPrinciple() eq true
    
        taxiPark(1..5, 1..4,
                trip(1, 1, 20, 20.0),
                trip(1, 2, 20, 20.0),
                trip(1, 3, 20, 20.0),
                trip(1, 4, 20, 20.0),
                trip(2, 1, 20, 21.0))
                .checkParetoPrinciple() eq false
    }
    
    data class TaxiPark(
            val allDrivers: Set<Driver>,
            val allPassengers: Set<Passenger>,
            val trips: List<Trip>)
    
    data class Driver(val name: String)
    data class Passenger(val name: String)
    
    data class Trip(
            val driver: Driver,
            val passengers: Set<Passenger>,
            // the trip duration in minutes
            val duration: Int,
            // the trip distance in km
            val distance: Double,
            // the percentage of discount (in 0.0..1.0 if not null)
            val discount: Double? = null
    ) {
        // the total cost of the trip
        val cost: Double
            get() = (1 - (discount ?: 0.0)) * (duration + distance)
    }
    
    fun driver(i: Int) = Driver("D-$i")
    fun passenger(i: Int) = Passenger("P-$i")
    fun drivers(range: IntRange) = range.toList().map(::driver).toSet()
    
    fun passengers(indices: List<Int>) = indices.map(::passenger).toSet()
    fun passengers(range: IntRange) = passengers(range.toList())
    fun passengers(vararg indices: Int) = passengers(indices.toList())
    
    fun taxiPark(driverIndexes: IntRange, passengerIndexes: IntRange, vararg trips: Trip) =
            TaxiPark(drivers(driverIndexes), passengers(passengerIndexes), trips.toList())
    
    fun trip(driverIndex: Int, passenger: Int, duration: Int = 10, distance: Double = 3.0, discount: Double? = null) =
            Trip(driver(driverIndex), passengers(passenger), duration, distance, discount)
    
    infix fun <T> T.eq(other: T) {
        if (this == other) println("OK")
        else println("Error: $this != $other")
    }
    

my response:
    
    fun TaxiPark.checkParetoPrinciple(): Boolean {
        if (trips.isEmpty()) return false
    
        val totalIncome = trips.sumByDouble(Trip::cost)
        val sortedDriversIncome: List<Double> = trips
                .groupBy(Trip::driver)
                .map { (_, tripsByDriver) -> tripsByDriver.sumByDouble(Trip::cost) }
                .sortedDescending()
    
        val numberOfTopDrivers = (0.2 * allDrivers.size).toInt()
        val incomeByTopDrivers = sortedDriversIncome
                .take(numberOfTopDrivers)
                .sum()
    
        return incomeByTopDrivers >= 0.8 * totalIncome
        return false
    }
    
    fun main(args: Array<String>) {
        taxiPark(1..5, 1..4,
                trip(1, 1, 20, 20.0),
                trip(1, 2, 20, 20.0),
                trip(1, 3, 20, 20.0),
                trip(1, 4, 20, 20.0),
                trip(2, 1, 20, 19.0))
                .checkParetoPrinciple() eq true
    
        taxiPark(1..5, 1..4,
                trip(1, 1, 20, 20.0),
                trip(1, 2, 20, 20.0),
                trip(1, 3, 20, 20.0),
                trip(1, 4, 20, 20.0),
                trip(2, 1, 20, 21.0))
                .checkParetoPrinciple() eq false
    }
    
	### Solution: Taxi Park, task 6

Let's see how we can complete this solution for the last task. 

I suppose that you've already solved that in the playground.
    
    fun TaxiPark.checkParetoPrinciple(): Boolean {
            if (trips.isEmpty()) return false
        
            val totalIncome = trips.sumByDouble(TODO())
            val sortedDriversIncome: List<Double> = trips
                    .groupBy(TODO())
                    .map { (_, tripsByDriver) -> tripsByDriver.sumByDouble(TODO()) }
                    .sortedDescending()
        
            val numberOfTopDrivers = (0.2 * allDrivers.size).toInt()
            val incomeByTopDrivers = sortedDriversIncome
                    .take(TODO())
                    .sum()
        
            return incomeByTopDrivers >= 0.8 * totalIncome
        }

This task is to check whether 20 percent of the drivers contribute 80 percent of the income.

To check that, at first we need to count the total income of all the drivers. 

For that, we use the cost of each trip, trip has a property cost. 

We sum up all the cost of all the trips and that is the total income.
    
     val totalIncome = trips.sumByDouble(Trip::cost)

Note that we can use property references. 

After that, we build a sorted list of drivers income. 

We are not interested in which exact drivers are the top drivers and contributed to the majority of the income. 

We are okay with sorting quantity income values. 

Thus, here we have the list of doubles as the result. 

First, we group the trips by drivers to build a map from driver to all trips by these driver, then map function transforms each entry in this map. 

The first parameter represents driver, but we are interested in under the trips by this driver.
    
          .groupBy(Trip::driver)
                    .map { (_, tripsByDriver) -> tripsByDriver.sumByDouble(Trip::cost) }

We find the overall income of the specific driver.

For that, we sum up the income for all the trips made by this specific driver. 

Again, we simply sum up the values returned by trip cost. 

Now, we have the total income and the list of sorted incomes for all the drivers. 

At last, we'll need to compare two numbers, the income of top drivers with 80 percent of the total income. 

Thus, we need to find the income of 20 percent of the top drivers.

For this, we use sortedDriversIncome. 

#### take function
The **take** function returns us the required number of the first elements in the list.

We wanted the list consisting of only the first top drivers.
    
     .take(numberOfTopDrivers)

We've already found this numberOfTopDrivers in the previous slide. 

Thus, we take the list consisting of only the income for the top drivers and count the sum of all the elements to find the total income of this top drivers.
    
     .sum()

At last, we just compare these numbers and that gives us the result. 

That's how we can solve this checkParetoPrinciple function in a rather concise fashion.

Other solutions are also possible.

There are many ways to solve this task. I just wanted to share one possible solution.

### Solution: Checking whether string is null or empty

The task here is to implement an extension function IsEmpyOrNull.

And the most interesting thing here is that the receiver might be nullable. 

Here we have a nullable string, and we want to call this function on a nullable string.
    
    val s1: String? = null
    val s2: String? = ""
    
    s1.isEmptyOrNull() eq true
    s2.isEmpttOrNull() eq true
    
    val s3  = "   "
    s3.isEmptyOrNull () eq false
    

Indeed,** in Kotlin, you can define functions on a nullable receiver, like extension functions.** 

That's not a problem, we just mark this receiver as nullable. 

And then you may implement your function. 
    
    fun String?.isEmptyOrNull()

When you consider a receiver as just an extra parameter, with this very nice special syntax to call it, it becomes very easy to understand what's going on.

And to implement it, you can simply check your parameter for null or being empty. 

    
    fun isEmptyOrNull(s: String?) = s == null || s.isEmpty()


You will do the same jig. 

We convert parameter to receiver.

And now you see there are. 

Also, note how we can explicitly check this for being null. 

So instead of the extension function to nullable, this might be null. 

Here, the smart-cast is used, because now this is converted to a non-null type after the check.

    
    fun String?.isEmptyOrNull() = this == null || this.isEmpty()
	
Note that is very useful for such simple cases like strings. 

**The library actually contains functions isNullOrEmpty, and isNullOrBlank, which checks whether string is null, or empty, or blank. **

OBS: Specifically for this task, I have to swap the name in order to let you implement it yourself. 

But you use such functions in Kotlin from the standard library by default. 

Indeed, when you use the code and you see that something is called just as a regular reference.

That doesn't always mean that the variable is not null.

So for most of the cases, that's true.

But note that there is this special case when there is a function on a nullable receiver. 

In this case you just call it like a regular reference without, say, success. 

That's something to keep in mind. 

**Because this confusion is possible when you define your own such functions, you may define your own functions on a nullable receiver.**

But do it with care, because it's better if your function explicitly tells in its name that this receiver might be null. 

Because in this case, it's easier to understand what's going on. 

And you don't have to guess how it checks null.

Or whether it checks, whether it's possible to call it on null or not. 

I can use it, but I do it with care in order not to confuse the readers of your code.

### Solution: Safe casts

In this task, we need to define a variable so that the first cast returned as null and the second one, cast to a nullable type throw an exception. 
    
    val s = "abc"
    println (s as? Int) //null
    println (s as Int?) //exception

This task is a good illustration for the difference between safe cast and there regular cast to an nullable type. 
    
     println (s as? Int) //null
        println (s as Int?) //exception

Any variable that stores not an integer value will do the job. 

So for instance, in this example you define a string, and after that, if you just use safe cast, then you get null as a result because that's how safe cast work.

If it doesn't cast, it's simpler transfer null. 

But the difference with the custom nullable type is that if your variable cannot be casted to a nullable type, then you'll have here ClassCastException that the cast is impossible. 

So there's the difference between this safe cast and the custom nullable type.

### Solution: Interchangeable predicates

Our task is to complete the implementations of these functions using different predicates. 
    
    fun List<Int>.allNonZero() = all { TODO() }
    fun List<Int>.allNonZero1() = none { TODO() }
    fun List<Int>.allNonZero2() = any { TODO() }
    
    fun List<Int>.containsZero() = any { TODO() }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = none { TODO() }
	fun main (args: Array<String>) {
		val list1 = listOf (1,2,3)
		list1.allNonZero() eq true
		list1.allNonZero1() eq true
		list1.allNonZero2() eq true
		
		list1.containsZero() eq false
		list1.containsZero1() eq false
		list1.containsZero2() eq false
	}
    
And the purpose of this task is to illustrate that the predicates **all**, **none**, and **any** are interchangeable. 

So let's start, the first function is rather straightforward because we need to check that all the elements are non zero. 

And we have this explicit all function, so we just check that all the elements are non zero, as written, as expected. 

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { TODO() }
    fun List<Int>.allNonZero2() = any { TODO() }
    
    fun List<Int>.containsZero() = any { TODO() }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = none { TODO() }

    

With the next function, that's a bit less trivial, when we check that there is one element that is non zero, that's the same as saying that there is no zero element, no zero is present in the list. 

That's exactly what **none** function checks, that there is no zero element.

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { it == 0 }
    fun List<Int>.allNonZero2() = any { TODO() }
    
    fun List<Int>.containsZero() = any { TODO() }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = none { TODO() }

So you see that these predicates are interchangeable, these functions are interchangeable, you just need to negate the predicate in order to use the different function. 

And that's just the boolean logic, so it's rather straightforward. 

With **any**, it's a little bit less trivial because we have to negate the result of the function.

When you think about it, **none** says there is no element, and it's the same as saying **not any**.

Not any means there is no such element, as none also says, there is no such element. 

So if we say not any zero, that's the same as saying no zero, that's the same as saying none zero.

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { it == 0 }
    fun List<Int>.allNonZero2() = !any { it == 0 }
    
    fun List<Int>.containsZero() = any { TODO() }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = none { TODO() }

Let's move on to the second task. 

The first one is again straightforward because it simply duplicates the function name. 

We say we are checking that this list contains zero, zero that means that any, we check that it contains any zero element. 

So when we use any, we explicitly check that the list contains zero.

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { it == 0 }
    fun List<Int>.allNonZero2() = !any { it == 0 }
    
    fun List<Int>.containsZero() = any {it == 0 }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = none { TODO() }

Then we know already that none is not any, so we can negate it the other direction as well. 

And we'll have here this not very easy idea of not none.

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { it == 0 }
    fun List<Int>.allNonZero2() = !any { it == 0 }
    
    fun List<Int>.containsZero() = any {it == 0 }
    fun List<Int>.containsZero1() = all { TODO() }
    fun List<Int>.containsZero2() = !none { it == 0 }

And we know again that all and  none are interchangeable, just with different predicates. 

So we can replace here, we can use the same none, so here we already have this solution. 

When we replace none to all, in this case, we just need to negate the predicate, and that's what we do.

    
    fun List<Int>.allNonZero() = all { it != 0 }
    fun List<Int>.allNonZero1() = none { it == 0 }
    fun List<Int>.allNonZero2() = !any { it == 0 }
    
    fun List<Int>.containsZero() = any {it == 0 }
    fun List<Int>.containsZero1() = !all { it != 0 }
    fun List<Int>.containsZero2() = !none { it == 0 }

Conceptionally, this is the same as containsZero, because if all are no zero, that means that there is no zero. 

And in order to check that it has at least one zero, then we have to negate this predicate.

The main purpose of this task is for you, **once you have the idea that all these predicates are interchangeable, and the most important thing is it's better to use the most simple predicate for the case. **

There's something that I've seen in the code, that's a good idea to keep in mind, that there's no need to negate the whole expression.

There is always the way to simplify the code without using the negation, because the negation is really, really hard to read and understand, as you can see here. 

But here we have our task, where you have to specifically write such code. 

But if you see the code like this in the code, you may ask like, why it's originally is so complicated manner, why just not simply I replace it with other function and a more simple predicate?

That's something to keep in mind, that it's often possible to simplify your logic. We can run the code to make sure that we have all okay.

Yes, yes, so we've done everything correctly.

### Properties

In this section, we're going to discuss properties in Kotlin. 

You might already know the concept of Java property.

Unlike Java where a property is not a language construct. Kotlin supports it as a separate language feature.

In a most common scenario for a trivial case, property syntaxes are really concise. 

But you can customize it if needed.
    
    java property
    
    public class JavaClass {
    	private int foo = 0;
    	public int getFoo() {
    		return foo;
    	}
    	
    	public void setFoo (int foo) {
    		this.foo = foo
    	}
    }

**Java classes contains fields and methods inside. They don't have the direct feature of property.**

However, **if you define a field with the corresponding getter and setter in Java, that concept will be considered a property.**

*so, java has fields and methods. but if you define a getter and setter for a field, then it is considered a property.*

For instance, **a field foo together with getFoo and setFoo methods is called the foo property.**
    
    kotlin property
    
    class KotlinClass {
    	var foo = 0
    }

In Kotlin, a property is absolutely the same idea, the same concept.

The syntax is different. 

You define the property itself rather than separately fields and accessors.

*because kotlin implements under the hood the getters and setters for the field, it is automatically an property.*

But under the hood, the implementation doesn't change. It's the same field and accessors as in Java.

**Read-only & mutable properties**

**property = field + accessor(s)
val = field + getter
var = field + getter + setter**


When you use a property in Kotlin, you don't call getters or setters.

You use properties directly and access it like a variable. 

**When you access the property by its name, the getter is called under the hood**. **If you want to change its value to call a setter**, you do it like it was a variable. Under the hood, the setter is called.


If you use the Kotlin properties from Java, you will need to call getters and setters explicitly like in Java. And Java code looks like Java.

Interestingly, there is no difference whether this contact class is defined in Kotlin or in Java.

If you define a Java class with a field getter and its probably setter following the convention, then in the Kotlin you can use it as a regular Kotlin property.

You access Java properties from Kotlin by their names not via getters and setters. 

The usage of properties now looks much nicer.

The question for you. How many methods does the class Person have under the hood? Note that we don't count the constructors here.
    
    class Person (val name: String, var age: Int)

We have one on the property name, which has the corresponding getter under the hood (*because it´s a val property, so it only allow a getter*) and a mutable property age, which has a getter and setter, getAge and setAge, that makes it 3 as a result.


This is the Person class written in Java and at the same time, that's what's going on under the hood.
    
    public final class Person {
    	@NotNull
    	private final String name;
    	private int age;
    	
    	public person(@NotNull String name, int age) {
    		this.name = name;
    		this.age = age;
    	}
    	
    	@NotNull
    	public final String getName() {
    		return this.name;
    	}
    	
    	public int getAge() {
    		return this.age;
    	}
    	
    	public final void setAge(int age) {
    		this.age = age;
    	}
    }

At the bytecode level, we have the same implementation as in Java, two fields, constructor, two getters and a setter. 

The Kotlin syntax looks nice, straightforward and concise, while the bytecode stays the same.

#### properties without fields
You can define properties without fields. 

Like in Java, when you can only define getFoo method that returns a value.

If you don't need a field, you omit it.

You can do define the accessors behavior without the necessity to store a value in a field.

**backing field might be absent**

**property = accessor(s)
val = getter
var = getter + setter**

Here, we define a custom getter for the isSquare property, which is calculated on each access. 
    
    class Rectangle (val height: Int, val width: Int) {
    	val isSquare: Boolean
    		get() {
    			return height == width
    		}
    }

**From Kotlin, you use the isSquare property as a regular property, there is no difference.**


The question for you is, how many times the phrase, calculating the answer, will be printed in this example?
    
    val foo1 = run {
      println("Calculating the answer...")
      42
    }
    
    val foo2: Int 
      get() {
        println("Calculating the answer...")
        return 42 
      }
    
    fun main(args: Array<String>) { 
      println("$foo1 $foo1 $foo2 $foo2")
    }

We use the run function that we've discussed in the previous module.

It runs the lambda and returns it's result, the last expression. 

We assign 42 to a variable foo1 and print calculating the answer on the way. 

**The lambda result is calculated only once when we assign it, then the property value is used.**

Therefore, the phrase calculating the answer is printed only once here. 

In the second example, the foo2 property has a custom getter which is called on each access.

**Every time we call the property, the getter is called and the calculating the answer phrase is printed. **

That gives us 3 as the number of times the phrase will the printed.

#### fields
Let's now talk about fields.

In Kotlin, you don't work with fields directly, you work with properties.

However, if you need, you can access a field inside its property accessors.

**you can access field only inside accessors**
    
    class StateLogger {
    	var state = false
    		set(value) {
    			println("state has changed: $field -> $value")
    			field = value
    		}
    }
    
**It's not visible for other methods of the class. **

You access a field inside its getter or setter by using the **field** keyword. 

Here, we have access a field inside a custom setter. 

We had log in to mark the situation when the property value was changed.

    No backing field
    
    enum class State { ON, OFF }
    
    class StateLogger {
    	private var boolState = false
    	
    	var state: State
    		get() = if (boolState) ON else OFF
    		set(value: State) {
    			boolState = value = ON
    		}
    }
    
Note that no backing field is generated by the compiler if you define acessors and don't use field keyword there. 

Here, **state mutable property uses another private property boolState to store the data. **

State only delegates to it. 

**Because state doesn't use field keyword inside its getter and setter, no baking field is generated for it.**

If you don't define accesors for a property, the compiler generates a trivial getter that returns the field value, and a trivial setter updating the value, if the property is mutable. 

You don't access field's getters or setters directly, you only use properties both inside and outside of the class. 

*so, you don´t use exampleClass.getProperty in kotlin, you use exampleClass.property*

I want to highlight here that under the hood the getters and setters are called. 

When you access counter here, then as the bytecode, getCounter is called instead. 

However, inside of the class, the optimization takes place. 

If the property accessors are trivial, their default ones, which return you the value or assign it, then the call is optimized by the compiler, and replaced with accessing the field directly. 

It's not safe to perform this optimization for code outside of the class. 

You might want to change the implementation of the getter, making it non trivial. 

Then you will need to recompile the depending code so that it use the getter instead of the field.

However, in general case, you can use different versions of the class and the depending code so such property change won't be safe.

The older depending code will continue to use the old trivial property implementation. To prevent such problems, outside of the class getters and setters are always called in the generated bytecode. 

But inside the class, optimization performed by the compiler are possible, but only for the trivial properties.

#### accessors visibility
Sometimes you want a var mutable property to be accessible only as a read-only property outside of the class. For that, you can make a setter private. 

    changing visibility of a setter
    
    class LengthCounter {
    	var counter: Int = 0
    		private set
    		
    	fun addWord(word: String) {
    		counter += word.length
    	}
    }

Then the getter is accessible everywhere. 

And therefore the property is accessible everywhere. 

But it's allowed to modify it only inside the same class. 

Note that we change only the visibility of the setter, but use the default implementation.

We've discussed redundant mutable properties, how to define custom getters and setters, and how to mix Kotlin properties and Java. 

### Unstable val
Implement the property 'foo' so that it produced a different value on each access. Note that you can modify the code outside the 'foo' getter (e.g. add additional imports or properties).
    
    val foo: Int
        get() = TODO()
    
    fun main(args: Array<String>) {
        // The values should be different:
        println(foo)
        println(foo)
        println(foo)
    }
	

solution:

    
    var bar = 1
    val foo: Int
        get() {
            bar ++
            return bar
        }
		
### More about Properties

now you'll see examples of how to define properties in interfaces and how to define extension properties. 

#### property in interface
You can define a property in an interface. Why not? 

Under the hood, it's just a getter.
    
    interface User {
    	val nickname: String
    }

Then you can redefine this getter in subclasses in the way you want.

    
    interface User {
    	val nickname: String
    }
	
	class FacebookUser (val accountId: Int) : User {
		override val nickname = getFacebookName(accountId)
	}
	
	class SubscribingUser(val email: String ) : User {
		override val nickname: String
			get() = email.substringBefore('@')
	}
	
A question for you here. Which property among these two is calculated on each access? 

The **nickname** property with a **custom getter** in subscribingUser **calculates the value each time you access it**. 

The property in FacebookUser stores the value in a field. 

The property with a custom getter doesn't have the corresponding field. 

OBS: Note that** all the properties in interfaces are open** and **can't be used** in smart casts.
    
    open property can´t be used in smart casts
    
    interface Session {
    	val user: User
    }
    
    fun analyzeUserSession (session: Session) {
    	if(session.user is FacebookUser) {
    	println(session.user.accountId)
    	}
    }


#### open properties
**Open means that they can be written in subclasses, they are not final. **

When you check whether the session user property is of type FacebokUser and afterward try to use a smart cast to access the account ID property of FacebookUser. 

The compiler shows you an error.

*compiler error: Smart cast to 'FacebookUser' is impossible, because 'session.user' is a property that has open or custom getter*

It's impossible because this property has an open or custom getter.

If a property has a custom getter, **it's not safe to use it in a smart cast because the custom getter can return your new value on each access. **

There is no guarantee that after you cast there will be the same value.

If the property is open, then the actual implementation in a subclass may have the custom getter which will return your different values on each access.

So, it's also not safe. 

What you can do here, you can introduce a local variable, then this much cost applies.

    interface Session {
    	val user: User
    }
    
    fun analyzeUserSession (session: Session) {
		val user = session.user
    	if(user is FacebookUser) {
    	println(user.accountId)
    	}
    }
	

**this works!**

Alternatively, you can use other language mechanisms which we'll discuss later. 

**Note also that smart casts don't also work for mutable properties, because the mutable property might be changed in a different thread after you have checked it for being of a specific type.** 

To fix this, you again introduce a local variable. 

Sometimes smart casts will work from mutable local variables. 

#### extension properties
In Kotlin, you can define extension properties. 

The syntax is very similar to the one of defining extension functions. 
    
    extension properties
    
    val String.lastIndex: Int
    	get() = this.length - 1
    
    val String.indices: IntRange
    	get() = 0..lastIndex
    	
    

**You simply define a property, but specify their stereotypes first.**

You can access the receiver as **this** reference inside accessories. 

Or you can emit **this** reference and call members as in the second example. 

You can call extension properties as they were member properties.

The syntax looks nicer in the same way as it works for extension functions. 

The question for you. What do you think does the extension property perform any optimizations in terms of the stored value? 

Here, we have this ABC string and we call an extension property twice on it. 
How many times the getter will be cold? 

Probably, it's somehow optimized and the value is stored. 

What's your guess? 
    
    val String.medianChar 
      get(): Char? {
        println("Calculating...")
        return getOrNull(length / 2) 
      }
    
    fun main(args: Array<String>) { 
      val s = "abc"
      println(s.medianChar) 
      println(s.medianChar)
    }

Of course, **there are no optimizations. **

This extension property is compiled to the get medianChar static method with an extra parameter under the hood which is called on each access. 

There is no magic here. 

Extension properties are very similar to extension functions, but their only difference is the difference syntax. 

**The one without parenthesis when you call it´s a property**.

#### mutable extensions properties
You can define mutable extension properties.
    
    var StringBuilder.lastChar: Char
    	get() = get(length - 1)
    	set(value:  Char) {
    		this.setCharAt(length -1, value)
    	}

Here, we define the mutable extension property lastChar on StringBuilder.

It allow us to get or update the last character. 

You then can use it as a regular property with the concise syntax to access setChar that just assigns a value to a property. 

You've learned that you can define a property in an interface and why it can't be smart casts.

You now know how to define a read-only or even mutable extension property. 

### Lazy or late initialization
now you'll learn how to define a Lazy Property. 

Also how to define the property that should be initialized not in the constructor, but sometime later. 

#### Lazy Property
Lazy Property is a property which values are computed only on the first success.

It's lazy in a sense that it won't do anything unless the result is really needed. 

In Kotlin, you define a Lazy Property using** by lazy** syntax.
**
val lazyValue: String by lazy {
	println("computed!")
	"Hello"
}**

It's an example of applying the future delegated properties which we'll discuss in the next course.

But even now you can use it for defining lazy properties. 

**Lazy is a function that takes lambda as an argument. **

Inside this lambda, you provide a way to compute a value that should be stored in this property.

When you access this property, you see that** its value is computed only once**, when we access it for the first time.

After that, the stored value is returned.

*so, with the example above, if we call it 2 times, it will print:*

*computed!
Hello
Hello*

The question for you is, how many times computed will be printed in this example when we don't access the property at all?

The options are as zero or one.
    
    val lazyValue: String by lazy { 
      println("computed!")
      "Hello" 
    }
    
    fun main(args: Array<String>) {
      // no lazyValue usage
    }

The right answer is of course zero, because **the lazy property is lazy in a sense that it won't do anything unless it's needed**.

In this case, the result is not needed and that's why it's not computed at all. 

#### late initialization -- lateinit
Our next topic is late initialization.

It's very useful for some frameworks. 

For instance for Android activities initializing of unit tests or dependency injection frameworks.

Sometimes, we want to initialize the property not in the constructor, but in a specially designated for that purpose method.
    
    class KotlinActivity: Activity() {
    	var myData: MyData? = null
    	
    	override fun onCreate (savedInstanceState: Bundle?) {
    		super.onCreate(savedInstanceState)
    		
    		myData = intent.getParcelableExtra("MY_DATA")
    	}
    }

Here, we initialized the myData property in onCreate method, but not in the constructor. 

We can't define it as a known nullable property, because we don't have an initial value. 

We can use null as an initial value.

But in this case, we have to make the property nullable. 

Then, every time we access it, we have to cope with nullability. 

*like:*
    
    .... myData?.foo ....

*and that´s bad.*

But we know that this property cannot be null after it was properly initialized. 

That's where lateinit properties can be really helpful.

    
    class KotlinActivity: Activity() {
    	lateinit var myData: MyData
    	
    	override fun onCreate (savedInstanceState: Bundle?) {
    		super.onCreate(savedInstanceState)
    		
    		myData = intent.getParcelableExtra("MY_DATA")
    	}
    }
	

We can define the properties **lateinit**. 

After that, we can use it as a **value of a non-nullable type**. 

What happens if the property wasn't initialized properly? 

We access it as a regular known nullable property. 

Nullpointer exceptions are possible. 

In fact at runtime, an exception is indeed thrown, but a runtime exception with a detailed message of what was wrong. 

*kotlin.UnintializedPropertyAccessException: lateinit property myData has not been initialized*

In this case, we get the message that the myData property wasn't initialized, and we see what caused these alternative more detailed version of NullPointerException.

##### constraints using lateinit properties
There are some constraints that apply to lateinit properties.

For instance, it can't be val.

###### lateinit has to be var
it has to be **var**

That is connected with how the lateinit properties are implemented under the hood.

**Lateinit variable can't be final at the bytecode level. **

Because it is initialized not in the constructor, but later.

It doesn't conform to the final constraint. 

Because of that, it can be changed from Java. 

Because it can be changed from Java if it was val, it would be confusing.

Imagine val property which can't be modified from Kotlin but can be modified from Java. Because of that, it was decided that it's safer to explicitly say that **this property is always mutable**. 

##### lateinit can not be nullable
Another constraint obvious is that, the type of this property is non-nullable. 

Thus a purpose of lateinit to make the type of the variable non-nullable, so that we won't have to cope with nullability issues.

##### lateinit can not be primitive type
Another constraint, is that lateinit property can't have a primitive type. 

That's also connected with the underlying implementation. 

**Only reference types might be initialized with null **under the hood. 

The compiler could possibly initialize integer values with some constants. 

But which exact constants?

Is unclear. 

That's not how it works.

If you know which our value, the primitive can be initialized with, you can do it by hand. 

Use zero for an integer for instance. 

**Thus the lateinit modifier can be only applied to non-nullable reference types.**

#### checking whether lateinit var was initialized
It's possible to check whether lateinit property was or wasn't initialized. 
    
    class MyClass {
    	lateinit var lateinitVar: String
    	
    	fun initializationLogic() {
    		println(this::lateinitVar.isInitialized)  // false
    		lateinitVar = "value"
    		println(this::lateinitVar.isInitialized)  // true
    	}
    }

To do that, you call **isInitialized** on the property reference. 

We saw examples of member references including property references in the previous module. 

That is another case when property references might be useful, when you check whether your lateinit property was or was not initialized. 

You've learned about lazy and lateinit properties. 

This conclude our discussion of properties so far. 

We'll also cover the nuances of how to define constants as properties, at the end of the next section. 


### Using lateinit property
Without modifying the class 'A' complete the code in 'main' so that an exception UninitializedPropertyAccessException was thrown. Then fix the newly added code in 'main' so that no exception was thrown.
    
    class A {
        private lateinit var prop: String
    
        fun setUp() {
            prop = "value"
        }
    
        fun display() {
            println(prop)
        }
    }
    
    fun main(args: Array<String>) {
        val a = A()
    
    }

solution:
    
    fun main(args: Array<String>) {
        val a = A()
        //a.display() // Exception in thread "main" kotlin.UninitializedPropertyAccessException: lateinit property prop has not been initialized
        
        a.setUp()
        a.display() // value
    }
	
### OOP in Kotlin

In this section, we'll focus on object-oriented programming in Kotlin. 

Overall, Kotlin doesn't introduce anything conceptually new here, the experience is very similar.

However, Kotlin brings many small concepts and practical improvements.

Note that in this course, we assume that you already understand such concepts as inheritance or method riding. 

So I want to explain you the familiar ideas, but just show you the different syntax. 

The defaults in Kotlin are different.

**Any declaration is public and final by default**. 

**If you want to make it non-final, you explicitly need to mark it as open.**

Also,** there is no package private visibility in Kotlin**. 

There is new one, **internal**.

That means that declaration is visible inside **this same module**. 

A module is a set of Kotlin files compiled together. 

It can be an intelliJ IDEA module, a Maven project, or Gradle source set.


#### final modifier
Final means that the declaration cannot be overridden, 

#### open modifier
open is that they're opposite and it should be marked explicitly.

#### abstract modifier
Abstract is the same as in Java, it means that the declaration must be overridden. 

#### override modifier
You explicitly added override modifier to member that override another member from the superclass. 

To avoid accidental overriding classes, **override now is mandatory.** 

You can't override something accidentally and not notice it. 


#### visibility modifiers
##### public
Public is visible everywhere,

##### internal
internal is visible in the same module, 

##### protected
protected is the same as in Java, it means that the declaration is visible in subclasses. 

However, there is a small difference with java.** In Java, protected is also visible inside the same package, in Kotlin, it's no longer the case, protected is only about subclasses**. 

##### private
Private differs in meaning for a class member and a top-level declaration, 

**class members is visible inside the class** 

and private 

**top-level declaration is visible inside the same file.** 

*so, a property private, is a class member, so it is visible only on the class itself.

a class private, is a top-level, so it is visible only inside the same file (.kt)*

You may ask what happens under the hood at the bytecode level.

**For public and protected declarations, it's clear that there is the direct correspondence. **

**Private functions and properties also stay private.**

**A private class is converted to a package private class, because there is no such thing in Java as a private class.** 

The main question is what happens with internal? 

A package private is different, it's not the same as the same module.

Under the hood, **internal is transformed to a public declaration. However, the names of internal members at mangled.**


At the bytecode, this function has a really long name which you can't accidentally use from Java. 

*so, when the compiler creates the bytecode, when we use internal the declaration is transformed into public but it creates a really long name, and thus, it cannot be confused with the normal declaration.*

#### package structure
There is also difference with package structure. 

##### several classes in one file
**In Java, every class should be located in its own separate file even if the class is very small.**

**In Kotlin**, it's no longer the case, **you can put several classes into one file**, is especially useful if your classes are data classes that is small and simple. 

You can combine several classes connected to each other in one file. 

You can also put top-level declarations functions and properties and the class into one file.

It makes sense to unite the class and all the utility members connects through this class and put them all together into one file. 

#### package name and directory structure
There is one more difference, in Kotlin, **the package name doesn't need to correspond to the directory structure**, your package name can be any name

However, the Kotlin style guide still recommends you to omit on the first prefix, the company name from the directory structure, and keep everything else so that it was easier to navigate your code.

After watching this video, you know that public and final used by default and override is mandatory. 

You've also learned that you no longer need to create a separate file to store small simple class.







































































































		

