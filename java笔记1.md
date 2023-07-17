# java记录day1

## 记录1.print/printf/println区别

1. print为一般输出，同样不能保留精度格式转化，也不能换行输出。
2. printf常用于格式转换，但需要注意不是换行输出，只用于精度转换。
    例  System.out.printf("%12.4f",a);代表输出占12个位宽，精确到4位小数。
3. println为换行输出，不能用于格式转换。  

## 记录2.自减自增

1. x++和++x
  对于第一个（x++），因为x++是先取值后自增，所以（x++）所取得值为3，然后x进行自增，此时x=4；对于第二个（++x），因为++x是先自增后取值，所以（++x）所取得值为5，此时x=5，所以结果为8。
2. --a和a--
  a++ 表示先赋值再进行加运算
  a-- 表示先赋值再进行减运算
  ++a 表示先进行加运算再赋值
  --a 表示先进行减运算再赋值
  注：从上面的概念理解很抽象

## 记录3.异常处理

### 1.捕获与多重捕获    try···catch···

```java
try {
    file = new FileInputStream(fileName);
    x = (byte) file.read();
} catch(FileNotFoundException f) { // Not valid!
    f.printStackTrace();
    return -1;
} catch(IOException i) {
    i.printStackTrace();
    return -1;
}
```

### 2.抛出异常 throw 和 throws 关键字是用于处理异常的

#### throw 关键字

> throw 关键字用于在代码中抛出异常

1. 通常情况下，当代码执行到某个条件下无法继续正常执行时，可以使用 throw 关键字抛出异常，以告知调用者当前代码的执行状态。

2. 例如，下面的代码中，在方法中判断 num 是否小于 0，如果是，则抛出一个 IllegalArgumentException 异常。

3. 实例

  ```java
  public void checkNumber(int num) {
    if (num < 0) {
      throw new IllegalArgumentException("Number must be positive");
    }
  }
  ```

#### throws 关键字

> throws 关键字用于在方法声明中指定可能会抛出的异常类型。

1. 当方法内部抛出指定类型的异常时，该异常会被传递给调用该方法的代码，并在该代码中处理异常。
2. 例如，下面的代码中，当 readFile 方法内部发生 IOException 异常时，会将该异常传递给调用该方法的代码。在调用该方法的代码中，必须捕获或声明处理 IOException 异常。
3. 实例

  ```java
  public void readFile(String filePath) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    String line = reader.readLine();
    while (line != null) {
      System.out.println(line);
      line = reader.readLine();
    }
    reader.close();
  }```

4. 一个方法可以声明抛出多个异常，多个异常之间用逗号隔开。
例如，下面的方法声明抛出 RemoteException 和 InsufficientFundsException：

  ```Java
  import java.io.*;
  public class className
  {
    public void withdraw(double amount) throws RemoteException,
                                InsufficientFundsException
    {
        // Method implementation
    }
    //Remainder of class definition
  }
  ```

#### finally关键字

>finally 关键字用来创建在 try 代码块后面执行的代码块。

1. 无论是否发生异常，finally 代码块中的代码总会被执行。

2. 在 finally 代码块中，可以运行清理类型等收尾善后性质的语句,finally 代码块出现在 catch 代码块最后

3. 实例

  ``` java
  ExcepTest.java 文件代码：
  public class ExcepTest{
    public static void main(String args[]){
      int a[] = new int[2];
      try{
        System.out.println("Access element three :" + a[3]);
      }catch(ArrayIndexOutOfBoundsException e){
        System.out.println("Exception thrown  :" + e);
      }
      finally{
        a[0] = 6;
        System.out.println("First element value: " +a[0]);
        System.out.println("The finally statement is executed");
      }
    }
  }
  ```

#### try-with-resources

1. JDK7 之后，Java 新增的 try-with-resource 语法糖来打开资源，并且可以在语句执行完毕后确保每个资源都被自动关闭 。

2. try-with-resources 是一种异常处理机制，它可以简化资源管理代码的编写。

3. try···catch 与try-with-resources

  ```java
  try  {
      // 使用的资源
    } catch (ExceptionType e1) {
      // 异常块
    }
      try (resource declaration) {
      // 使用的资源
    } catch (ExceptionType e1) {
      // 异常块
    }
    ```

4. 实例

  ```java
  import java.io.*;

  public class RunoobTest {

      public static void main(String[] args) {
      String line;
          try(BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
              while ((line = br.readLine()) != null) {
                  System.out.println("Line =>"+line);
              }
          } catch (IOException e) {
              System.out.println("IOException in try block =>" + e.getMessage());
          }
      }
  }
  ```
