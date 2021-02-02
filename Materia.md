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

