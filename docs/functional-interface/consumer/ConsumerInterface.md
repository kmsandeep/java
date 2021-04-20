## Consumer Interface in JAVA-8

Consumer Interface is part of *java.util.function* package. It is a functional-interface.

A functional interface is one which has only one abstract method. The only abstract method present in Consumer Interface is **accept** method. Let us see what Consumer interface looks like:

```java
@FunctionalInterface
public interface Consumer<T> {
    
    void accept(T t);
    
    default Consumer<T> andThen(Consumer<? super T> after) {
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```

- Here @FunctionalInterface is annotation which restrict us to declare more than one abstract method. If you are using a interface as Functional Interface, you should use this annotation to restrict any future addition of abstract method in it.
- Here Consumer interface is a generic interface, that means while implementing the apply method, the *type* of argument have to be specified.

*We have two ways to implement our Consumer interface*

1. By using anonymous  class

   ```java
   Consumer<Integer> consumerImpl = new Consumer<Integer>() {
   			@Override
   			public void accept(Integer t) {
   				System.out.print("Accepting "+t);
   			}
   		};
   consumerImpl.accept(5)
   //Output:
   //Accepting 5
   ```

   This is not recommended way of implementing Consumer interface as there is lot of unnecessary code.

2.  By using Lambda expression

   ``` java
   Consumer<Integer> lambdaFunc1 = (n) -> System.out.print("Accepting "+n);
   lambdaFunc1.accept(5)
   //Output:
   //Accepting 5
   ```

   **Passing lambda as functional argument**

   We can see that lamdaFunc stores our implementation of  Consumer interface. We can pass this behavior to any function. Let us see how:

   ```java
   //Define a function which accept lambdaFunc as its arguement
   void foo(Consumer<Integer> func,Integer n){
       func.accept(n);
   }
   foo(lambdaFunc,10)
   //>> Accepting 10
   Consumer<Integer> lambdaFunc2 = (n) -> System.out.print("Printing "+n);
   foo(lambdaFunc2,10)
   //>> Printing 10
   ```

   

   

   

   