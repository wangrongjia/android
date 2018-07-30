# what's new in Java 8
## Lambda 表达式
Lambda 允许把函数作为一个方法的参数（函数作为参数传递进方法中）  
以下是lambda表达式的重要特征:

可选类型声明：不需要声明参数类型，编译器可以统一识别参数值。   
可选的参数圆括号：一个参数无需定义圆括号，但多个参数需要定义圆括号。  
可选的大括号：如果主体包含了一个语句，就不需要使用大括号。   
可选的返回关键字：如果主体只有一个表达式返回值则编译器会自动返回值，大括号需要指定明表达式返回了一个数值。  
    
Lambda 表达式主要用来定义行内执行的方法类型接口,免去了使用匿名方法的麻烦    
```java
  interface MathOperation {
    int operation(int a, int b);
  }

  // 类型声明
  MathOperation addition = (int a, int b) -> a + b;

  private int operate(int a, int b, MathOperation mathOperation) {
    return mathOperation.operation(a, b);
  }

  public static void main(String args[]) {
    Java8Tester tester = new Java8Tester();
    System.out.println("10 + 5 = " + tester.operate(10, 5, addition));
  }
```
#### 注意点1 lambda 表达式引用外层局部变量，不能在 lambda 内部修改定义在域外的局部变量，否则会编译错误，也就是说在lambda表达式内部，其引用的外层局部变量默认都被final修饰。  
```java
public class Java8Tester {
  public static void main(String args[]) {
    int num = 1;
    Converter<Integer, String> s = (param) -> {
      System.out.println(String.valueOf(param + num++));//报错：Local variable num defined in an enclosing scope must be final or effectively final
    };
    s.convert(2); // 输出结果为 3
  }

  public interface Converter<T1, T2> {
    void convert(int i);
  }
}
```



