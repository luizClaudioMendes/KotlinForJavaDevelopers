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
