# What's new in Java 9 - 14?

## Java 9 (2017-09)
https://openjdk.java.net/projects/jdk9/

* [Jigsaw (modularization)](https://openjdk.java.net/jeps/200)
* [Process API updates](https://openjdk.java.net/jeps/102) Improved ability to interact with OS processes.
* [HTTP/2 Client](https://openjdk.java.net/jeps/110) incubator project, not automatically included in Java 9
  * This [new HTTP client](https://docs.oracle.com/javase/9/docs/api/jdk/incubator/http/package-summary.html) is much more intuitive (HttpClient, HttpRequest, HttpResponse, ..) than the [original java.net API](https://docs.oracle.com/javase/9/docs/api/java/net/package-summary.html) (URL, URLConnection, InputStreamReader, ..)
* [Convenience Factory Methods for Collections](https://openjdk.java.net/jeps/269) like `List.of(...)`, `Set.of(...)` and `Map.of(...)`.
* [jshell](https://docs.oracle.com/javase/9/jshell/introduction-jshell.htm)  the new Java Shell (REPL)

#### JShell

JShell is ideal for prototyping and testing without having to start an IDE and create a main class:

```
$ jshell
|  Welcome to JShell -- Version 11.0.5
|  For an introduction type: /help intro

jshell> 1
$1 ==> 1

jshell> int i = 2
i ==> 2

jshell> i + $1 == 3
$3 ==> true

jshell> /list

   1 : 1
   2 : int i = 2;
   3 : i + $1 == 3

jshell> void helloWorld() {
   ...> System.out.println("Hello!");
   ...> }
|  created method helloWorld()

jshell> helloWorld()
Hello!

jshell> /methods
|    void helloWorld()

jshell> /imports
|    import java.io.*
|    import java.math.*
|    import java.net.*
|    import java.nio.file.*
|    import java.util.*
|    import java.util.concurrent.*
|    import java.util.function.*
|    import java.util.prefs.*
|    import java.util.regex.*
|    import java.util.stream.*

jshell> /exit
|  Goodbye
 $
```

## Java 10 (2018-03)
https://openjdk.java.net/projects/jdk/10/

* [Local-Variable Type Inference](https://openjdk.java.net/jeps/286)
  * `var list = new ArrayList<String>();`

#### Graal

##### Bytecode interpretation and JIT-compilation in the HotSpot JVM
First some background information on the Java compiler and Oracle's HotSpot JVM. The `javac` compiler translates java code (.java) into platform independent bytecode (.class). The (platform dependent) JVM interprets or compiles the bytecode into machine code.

Interpretation is faster than compilation, but compiled code runs faster than interpreted code. In other words, only frequently executed code is worth compiling.

Therefore, by default, HotSpot interprets Java byte code each time it is executed. The JVM keeps track of the number of times each method is called. Only when a method becomes 'hot' (executed for a threshold number of times) it will be compiled into machine code. The compiled machine code is stored somewhere for reuse on subsequent calls. 

This is called Just-In-Time compilation, and this is why the JVM compilers are called JIT-compilers.

HotSpot features two JIT-compilers: The client compiler (C1) and the server compiler (C2). The client compiler features quick startup, quick compilation and has a small memory footprint but the result is not fully optimized. The server compiler is slower but results in the best optimized code, hence provides the best runtime performance once the server has 'warmed up'.

More background information [here](https://docs.oracle.com/javacomponents/jrockit-hotspot/migration-guide/comp-opt.htm#JRHMG117) and [here](https://www.oreilly.com/library/view/java-performance-the/9781449363512/ch04.html). And [JITWatch](https://www.jrebel.com/blog/understanding-java-jit-with-jitwatch) ([github](https://github.com/AdoptOpenJDK/jitwatch)) is a visualization tool for the HotSpot JIT compiler.

Because of platform independence, the JVM has traditionally always used interpretation and JIT-compilation. It would however be much more efficient to compile the full program into machine code before running the application (Ahead-Of-Time or AOT-compilation). This is where GraalVM comes into play.

This is a nice [blog post](https://metebalci.com/blog/demystifying-the-jvm-interpretation-jit-and-aot-compilation/) about interpretation vs. JIT vs. AOT.

##### AOT-compilation with Graal
[GraalVM](https://www.graalvm.org/) is an ecosystem & shared runtime offering [performance advantages](https://www.graalvm.org/docs/examples/java-performance-examples/) for JVM-based languages and other languages (JavaScript, Python, R, ..) and seemless language interoperability. It can run standalone, but can also be embedded in [OpenJDK](https://openjdk.java.net/projects/graal/) (or Node.js platforms, ..) either as a JIT-compiler or as an AOT-compiler.

Graal is still experimental in Java 10. Do not use it in production!

## Java 11 (2018-09)
https://openjdk.java.net/projects/jdk/11/

* [Local-Variable Syntax for Lambda Parameters](https://openjdk.java.net/jeps/323) 
  * `(var x, var y) -> y.process(x)`
  * Also allows for annotations: `(@Nullable var x, var y) -> y.process(x)`
* [HTTP Client](https://openjdk.java.net/jeps/321)
  * Available in [java.net.http](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/module-summary.html) (was incubated in Java 9/10)
  * Completely asynchronous (was blocking in Java 9/10)
* [Launch Single-File Source-Code](https://openjdk.java.net/jeps/330) 
  * `$ java SourceFileWithMain.java` (in Java 10- the class had to be compiled first)
  * Great for small utility programs or trying out a new API (alternative to JShell)
* [Flight Recorder](https://openjdk.java.net/jeps/328) is a low-overhead data collection framework for troubleshooting Java applications and the HotSpot JVM
  * Recorded events can be inspected with [Java Mission Control](https://docs.oracle.com/javacomponents/jmc-5-5/jmc-user-guide/toc.htm)
  * Reduces dependence on 3rd party profiling tools
* [TLS 1.3](https://openjdk.java.net/jeps/332)

## Java 12 (2019-03)
https://openjdk.java.net/projects/jdk/12/

## Java 13 (2019-09)
https://openjdk.java.net/projects/jdk/13/

## Java 14 (2020-03)
https://openjdk.java.net/projects/jdk/14/





