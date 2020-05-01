# Run down of new features in Java 
## Java 11
1. can use var in lambda
2. HTTPClient - asynchronous, future support for HTTP2. This is class which provides all HTTP methods and feature to make HTTP requests.
3. GC enhancements - Epsilon introduced, scalable low latency Gabage collector. 
4. Java intepretor works on Java files - `java Example.java` works. It must be a single source file. 
5. 
6. Java Flight Recorder - This is java's own profiler, like JProfiler. A continuous and configurable dump of events of the java runtime. Introduces jdk.jfr.Event class with which you can crete custom events. 
7. TLS 1.3 support, ChaCha20 algorithms
8. 
## Java 10
2. Backward compatibilty is present
3. Variable declaration Local variable type inference-  
	1. `List <String> list = new ArrayList<String>();` 
	2. `var = new ArrayList<String>();`  The type is deciphed from how you are initializing it. It means you cannot have `var x;`
	3. Still it is statically typed (not like python);
	4. `var` is a keyword now.
	5.  Cannot use them in lamdas
4. A cleaner interface to garbage collector interface.  GC is parallel
5. CDS - More features -  AppCDS - saves memory
6. Java Safe points - Global Safe Points are points in the code where all threads are at a well described state, All the threads have to reach a safe point before its possible to do a Stop-The-World full garbage collection or a JNI call to native code. More [here](http://robsjava.blogspot.com/2014/02/how-safe-points-effect-jni-and-garbage.html) 
7. Time based release versioning - Six months release cycle.
8. JIT versions - Can enable Graal , AOT experimental

## Java 9 
1. JIT - Graal introduced.
2. JShell introduced - a python like interpreter. 
## Java 8 
1. Lambda - A much awaited one, I must say. 
2. 
## Java 7 
1. Diamond operator
6. 
## New features in Java 5
1. Generics - 
2. CDS 

## Other things
1. CACerts - the Java trust strore, which is the CA. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxNTgwNjI0NCwxMDEzNTIzOTUwLC0xMT
c0MDY3MDQ2LDg1NjY0MzYyNCwtMTQzOTI3Mzc5MywtODY3MDcx
MTg2LDM1NTg2ODMzN119
-->