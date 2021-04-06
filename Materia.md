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



