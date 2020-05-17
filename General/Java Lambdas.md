# Java Lambdas
1. Introduced in Java 8. 
2. Intros - 
	  1. [Lambda: A Peek Under the Hood](https://www.youtube.com/watch?v=C_QbkGU_lqY)
3. Lambda is inline function definition and call to itself. This is treating code / method like data. 
4. Lambda is defined by the `->`. Method references by operator `::` 
5. Two new packages are added `iava.util.function` and `java.util.streams`
6. Syntax - *(lamba  argumeents)* ->*(lambda body)* 
this is equivalent is a loose sense to 
```
public void somefunction(/* lambda arguments */) {
/* lambda body */
}
```
7. Points to note
    1. **No explicit call** - since we are not defining any function explicity, we are able to omit the call to it. 
    2.  **Arg types**  - They can be provided or compiler infers them. If only one arg is there, the brackets may be omitted. `var` keyword can be used in Java 11.
8.  Examples 
`(int x, int y) -> x + y`
` () -> "Java 8"` 
` x -> x*x`
9.  Explicit Lamda definition - contrary to intention we can define explicity a lamda function 
` LambdaFunction lambda = () -> System.out.println("Hello Lambda");`
and call it using 
`lambdaFunction.call();` 
10. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI2MzUyNTk0LDUwNzM5NDk3NywxMjIyMD
UxMjcxLDExNjk3NTg2LDEyMTE0NTIyNzhdfQ==
-->