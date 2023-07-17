# 笔记3

## 源码查看

 1.查询api手册
 2.idea连点两下 shift 打开搜索 勾选include non-project item

## 泛型

### 泛型方法

1. java 中泛型标记符：

   >E - Element (在集合中使用，因为集合中存放的是元素)
   >T - Type（Java 类）
   >K - Key（键）
   >V - Value（值）
   >N - Number（数值类型）
   >？ - 表示不确定的 java 类型

2. 使用泛型方法打印不同类型的数组元素：

   ```java
   public class GenericMethodTest
   {
      // 泛型方法 printArray                         
      public static < E > void printArray( E[] inputArray )
      {
         // 输出数组元素            
            for ( E element : inputArray ){        
               System.out.printf( "%s ", element );
            }
            System.out.println();
      }
   
      public static void main( String args[] )
      {
         // 创建不同类型数组： Integer, Double 和 Character
         Integer[] intArray = { 1, 2, 3, 4, 5 };
         Double[] doubleArray = { 1.1, 2.2, 3.3, 4.4 };
         Character[] charArray = { 'H', 'E', 'L', 'L', 'O' };
   
         System.out.println( "整型数组元素为:" );
         printArray( intArray  ); // 传递一个整型数组
   
         System.out.println( "\n双精度型数组元素为:" );
         printArray( doubleArray ); // 传递一个双精度型数组
   
         System.out.println( "\n字符型数组元素为:" );
         printArray( charArray ); // 传递一个字符型数组
      } 
   }
   ```

3. "extends"如何使用在一般意义上的意思"extends"（类）或者"implements"（接口）

   ```java
   public class MaximumTest
   {
      // 比较三个值并返回最大值
      public static <T extends Comparable<T>> T maximum(T x, T y, T z)
      {                     
         T max = x; // 假设x是初始最大值
         if ( y.compareTo( max ) > 0 ){
            max = y; //y 更大
         }
         if ( z.compareTo( max ) > 0 ){
            max = z; // 现在 z 更大           
         }
         return max; // 返回最大对象
      }
      public static void main( String args[] )
      {
         System.out.printf( "%d, %d 和 %d 中最大的数为 %d\n\n",
                     3, 4, 5, maximum( 3, 4, 5 ) );
   
         System.out.printf( "%.1f, %.1f 和 %.1f 中最大的数为 %.1f\n\n",
                     6.6, 8.8, 7.7, maximum( 6.6, 8.8, 7.7 ) );
   
         System.out.printf( "%s, %s 和 %s 中最大的数为 %s\n","pear",
            "apple", "orange", maximum( "pear", "apple", "orange" ) );
      }
   }
   ```

### 泛型类

泛型类的声明和非泛型类的声明类似，除了在类名后面添加了类型参数声明部分。

和泛型方法一样，泛型类的类型参数声明部分也包含一个或多个类型参数，参数间用逗号隔开。一个泛型参数，也被称为一个类型变量，是用于指定一个泛型类型名称的标识符。因为他们接受一个或多个参数，这些类被称为参数化的类或参数化的类型。

```java
public class Box<T> {
   
  private T t;
 
  public void add(T t) {
    this.t = t;
  }
 
  public T get() {
    return t;
  }
 
  public static void main(String[] args) {
    Box<Integer> integerBox = new Box<Integer>();
    Box<String> stringBox = new Box<String>();
 
    integerBox.add(new Integer(10));
    stringBox.add(new String("菜鸟教程"));
 
    System.out.printf("整型值为 :%d\n\n", integerBox.get());
    System.out.printf("字符串为 :%s\n", stringBox.get());
  }
}
```

### 类型通配符

1. 类型通配符一般是使用 ? 代替具体的类型参数。例如 List<?> 在逻辑上是 List< String >,List< Integer > 等所有 List<具体类型实参> 的父类。

   ```java
   import java.util.*;
   
   public class GenericTest {
      
      public static void main(String[] args) {
         List<String> name = new ArrayList<String>();
         List<Integer> age = new ArrayList<Integer>();
         List<Number> number = new ArrayList<Number>();
         
         name.add("icon");
         age.add(18);
         number.add(314);
   
         getData(name);
         getData(age);
         getData(number);
         
      }
   
      public static void getData(List<?> data) {
         System.out.println("data :" + data.get(0));
      }
   }```

2. 类型通配符上限通过形如List来定义，如此定义就是通配符泛型值接受Number及其下层子类类型。

   ```java
   import java.util.*;
   
   public class GenericTest {
      
      public static void main(String[] args) {
         List<String> name = new ArrayList<String>();
         List<Integer> age = new ArrayList<Integer>();
         List<Number> number = new ArrayList<Number>();
         
         name.add("icon");
         age.add(18);
         number.add(314);
   
         //getUperNumber(name);//1
         getUperNumber(age);//2
         getUperNumber(number);//3
         
      }
   
      public static void getData(List<?> data) {
         System.out.println("data :" + data.get(0));
      }
      
      public static void getUperNumber(List<? extends Number> data) {
            System.out.println("data :" + data.get(0));
         }
   }
   ```
