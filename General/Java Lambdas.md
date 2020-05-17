# Java Lambdas
1. Introduced in Java 8. 
2. Lambda is inline function definition and call to itself. 
3. Lambda is defined by the `->`. Method references by operator `::` 
4. Two new packages are added `iava.util.function` and `java.util.streams`
5. Syntax - *(lamba  argumeents)* ->*(lambda body)* 
this is equivalent is a loose sense to 
```
public void somefunction(/* lambda arguments */) {
/* lambda body */
}
```
6. Points to note
    1. **No explicit call** - since we are not defining any function explicity, we are able to omit the call to it. 
    2.  **Arg types**  - They can be provided or compiler infers them. If only one arg is there, the brackets may be omitted. 
7.  Examples 
`(int x, int y) -> x + y`
` () -> "Java 8"` 
` x -> x*x`
8.  Explicit Lamda definition - contrary to intention we can define explicity a lamda function 
` LambdaFunction lambdaFunction = () -> System.out.println("Hello world");`
10. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjk1OTQzMjczLDExNjk3NTg2LDEyMTE0NT
IyNzhdfQ==
-->