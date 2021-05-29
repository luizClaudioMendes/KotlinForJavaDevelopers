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





































		

