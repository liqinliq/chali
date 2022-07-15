1. 静态方法中调用的成员变量或方法一定要求为静态类，相反，既可以调用静态类变量也可以调用普通变量；

2. 静态变量：共用地址，赋值会改变指向改堆的所有变量；

   ![1657882886815](C:\Users\QIN\AppData\Local\Temp\1657882886815.png)

3. 多态运行静态方法，运行父类中的静态方法；运行非静态方法，运行子类的重写方法；成员变量，编译运行的全是父类。

   ~~~java
   package exercise;
   import com.Main;
   class Super{
      public static void m1(){
          System.out.println("m1 in Super");
      }
      public void m2(){
          System.out.println("m2 in Super");
      }
   }
   class Sub extends Super{
       public static void m1(){
           System.out.println("m1 in Sub");
       }
       public void m2(){
           System.out.println("m2 in Sub");
       }
   }
   public class Demo1{
       public static void main(String[] args) {
           Super sup=new Sub();
           sup.m1();
           sup.m2();
           Sub sub=(Sub)sup;
           sub.m1();
           sub.m2();
       }
   }
   ~~~

   ![1657885324555](C:\Users\QIN\AppData\Local\Temp\1657885324555.png)

4. 静态方法

   （1）不能被覆盖（重写）；

   （2）不可以使用this关键字；

   （3）不能调用非静态方法；

   （4）非静态方法中可以调用静态方法；

   （5）可以在不产生任何一个对象的情况下调用静态方法。

   （6）静态方法能够用类名直接调用

   如下：

   子类中的m1()方法不属于重写父类中的m1()，子类中的m2()属于重写父类中的m2()；

   ~~~java
   class Super{
      public static void m1(){
          System.out.println("m1 in Super");
      }
      public void m2(){
          System.out.println("m2 in Super");
      }
   }
   class Sub extends Super{
       public static void m1(){
           System.out.println("m1 in Sub");
       }
       public void m2(){
           System.out.println("m2 in Sub");
       }
   }
   ~~~

   5. final 关键字

   使用final定义变量时一定要初始化；

   6. 使用final将方法覆盖

   ```java
   class Super {
       public final  void m1(){
           System.out.println("m1() in super");
       }
       public void m1(int i){
           System.out.println("m1(int) in super");
       }
       }
       class Sub extends Super{
       public void m1(int i){
           System.out.println("m1(int) in sub");
       }
       public void m1(double d){
           System.out.println("m1(double) in sub");
       }
   
       }
   public class Demo1 {
       public static void main(String[] args) {
         Sub s=new Sub();
         s.m1();
         s.m1(10);
         s.m1(1.5);
   
       }
   }
   ```

​         运行结果如下：

![1657887805829](C:\Users\QIN\AppData\Local\Temp\1657887805829.png)

7. abstract方法覆盖

   ~~~java
   abstract class MyAbstractClass{
       public abstract void m1();
       abstract protected void m2();
   }
   class MySubClass extends MyAbstractClass{
       public void m1(){}
       protected void m2(){}
   }
   ~~~

8. abstract介绍：

   （1）abstract类中可以没有abstract方法；

   （2）abstract类的子类也可以是abstract类

   （3）abstract类不能创建对象，但可以声明引用；

   （4）abstract方法不能有方法体。

   

   

   