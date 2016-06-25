# Java 可以通过初始化块为成员变量赋值。

* **在类的声明中，可以包含多个初始化块，当创建类的实例时，就会依次执行这些代码块。**

* **静态初始化只在类加载时执行，且只会执行一次，同时静态初始化块只能给静态变量赋值，不能初始化普通的成员变量。**
  
* 基础例子

  ~~~ java
  public class A {
	  public A(){
		  System.out.println("--- 父类 A 的无参构造方法 ---");
	  }
	  private String ac = aC();
	  protected static final int ad = 1;
	  public String aC(){
		  System.out.println("--- 父类非静态成员变量 ac 初始化 ---");
		  return null;
	  }
	  {
		  System.out.println("--- 父类非静态代码块开始 ---");
		  System.out.println("--- 父类非静态代码块结束 ---");
	  }
	  private static String aa = aA();
	  static{
		  System.out.println("--- 父类静态代码块开始 ---");
		  System.out.println("--- 父类静态代码块结束 ---");
	  }
	  private static final String ab = aB();
	  public static String aA() {
		  System.out.println("父类静态成员变量 aa 初始化");
		  return null;
	  }
	  public static String aB() {
		  System.out.println("父类静态成员变量 ab 初始化");
		  return null;
	  }
  }
  public class B extends A {
	  static
	  {
		  System.out.println("=== 子类静态代码块开始 ===");
		  System.out.println("=== 子类静态代码块结束 ===");
	  }
	  {
		  System.out.println("=== 子类非静态代码块开始 ===");
		  System.out.println("=== 子类非静态代码块结束 ===");
	  }
	  private static String ba = bA();
	  private static String bA() {
		  System.out.println("=== 子类静态成员变量 ba 初始化 ===");
		  return null;
	  }
	  private String bb = bB();
	  public String bB(){
		  System.out.println("=== 子类非静态成员变量 bb 初始化 ===");
		  return null;
	  }
  } 
  public class Test {
	  public static void main(String[] args){
		  System.out.println("父类 A 的常量 ad： B.ad = " + B.ad);
		  System.out.println("```````````````````````````");
		  A a = new B();
		  System.out.println("```````````````````````````````````````````````````");
		  B b = new B();
		  a.aC();
		  b.aC();
	  }
  }
  ~~~
  ~~~ bash
  // 运行结果
  父类 A 的常量 ad： B.ad = 1
  ```````````````````````````
  父类静态成员变量 aa 初始化
  --- 父类静态代码块开始 ---
  --- 父类静态代码块结束 ---
  父类静态成员变量 ab 初始化
  === 子类静态代码块开始 ===
  === 子类静态代码块结束 ===
  === 子类静态成员变量 ba 初始化 ===
  --- 父类非静态成员变量 ac 初始化 ---
  --- 父类非静态代码块开始 ---
  --- 父类非静态代码块结束 ---
  --- 父类 A 的无参构造方法 ---
  === 子类非静态代码块开始 ===
  === 子类非静态代码块结束 ===
  === 子类非静态成员变量 bb 初始化 ===
  ```````````````````````````````````````````````````
  --- 父类非静态成员变量 ac 初始化 ---
  --- 父类非静态代码块开始 ---
  --- 父类非静态代码块结束 ---
  --- 父类 A 的无参构造方法 ---
  === 子类非静态代码块开始 ===
  === 子类非静态代码块结束 ===
  === 子类非静态成员变量 bb 初始化 ===
  --- 父类非静态成员变量 ac 初始化 ---
  --- 父类非静态成员变量 ac 初始化 ---
  ~~~

  > **结论**
  > 实例化类的时候包含了两个部分：1. 首先可定先加载类，初始化类（初始化类的静态成员）2. 加载完类后，类的初始化就会发生，意味着它会初始化所有类静态成员，and then，因为有 new() 所以为实例分配内存空间就是实例化类了。
  > 初始化类呢，只能看到类层面上的内容，对象层面上的得在实例化之后才能看到。所以初始化类时，就会把所有静态的成员包括静态代码块按照代码的先后顺序全都初始化完（从父类到子类），然后如果实例化了，就初始化父类的非静态成员（包括非静态代码块）才算初始化完毕。
  
----------
**类被初始化的场景**
1. 实例通过使用 new() 关键字创建或者使用class.forName()反射，但它有可能导致 ClassNotFoundException。上面的实例验证了场景1 的非反射部分。
2. 类的静态方法被调用
3. 类的静态域被赋值
4. 静态域被访问，而且它不是常量
5. 在顶层类中执行 assert 语句
----------

----------
**类初始化的一些规则**
1. 类从顶至底的顺序初始化，所以声明在顶部的字段的早于底部的字段初始化
2. 超类早于子类和衍生类的初始化
3. 如果类的初始化是由于访问静态域而触发，那么只有声明静态域的类才被初始化，而不会触发超类的初始化或者子类的初始化即使静态域被子类或子接口或者它的实现类所引用。
4. 接口初始化不会导致父接口的初始化。
5. 静态域的初始化是在类的静态初始化期间，非静态域的初始化时在类的实例创建期间。这意味这静态域初始化在非静态域之前。
6. 非静态域通过构造器初始化，子类在做任何初始化之前构造器会隐含地调用父类的构造器，他保证了非静态或实例变量（父类）初始化早于子类
----------

* 提高例子 
  ~~~
  public class A {
	  public A(){
		  System.out.println("--- 父类 A 的无参构造方法 ---");
	  }
	  private static String aa = aA();
	  protected static final String ab = aB();
	  private String ac = aC();
	  protected static final int ad = 1;
	  {
		  System.out.println("--- 父类非静态代码块开始 ---");
		  System.out.println("--- 父类非静态代码块结束 ---");
	  }
	  static{
		  System.out.println("--- 父类静态代码块开始 ---");
		  System.out.println("--- 父类静态代码块结束 ---");
	  }
	  public static String aA() {
		  System.out.println("父类静态成员变量 aa 初始化");
		  return null;
	  }
	  public static String aB() {
		  System.out.println("父类静态成员变量 ab 初始化");
		  return "aB";
	  }
	  public String aC(){
		  System.out.println("--- 父类非静态成员变量 ac 初始化 ---");
		  return null;
	  }
  }

  public class B extends A {
	  static
	  {
		  System.out.println("=== 子类静态代码块开始 ===");
		  System.out.println("=== 子类静态代码块结束 ===");
	  }
	  {
		  System.out.println("=== 子类非静态代码块开始 ===");
		  System.out.println("=== 子类非静态代码块结束 ===");
	  }
	  private static String ba = bA();
	  private static String bA() {
		  System.out.println("=== 子类静态成员变量 ba 初始化 ===");
		  return null;
	  }
	  private String bb = bB();
	  public String bB(){
		  System.out.println("=== 子类非静态成员变量 bb 初始化 ===");
		  return null;
	  }
  }

  public class Test {
	  public static void main(String[] args){
		  System.out.println("父类 A 的常量 ad： B.ad = " + B.ad);
		  System.out.println("```````````````````````````````````````");
		  System.out.println("父类 A 的常量 ab： A.ab 会调用 aB()，结果:" + A.ab);
		  System.out.println("``````````````````````````````````````````````````````````````````````````");
		  System.out.println("子类 B 从 A 继承到的常量 ab： B.ab 会调用 aB()，结果:" + B.ab);
	  }
  }
  ~~~
  ~~~ bash
  // 运行结果
  父类 A 的常量 ad： B.ad = 1
  ```````````````````````````````````````
  父类静态成员变量 aa 初始化
  父类静态成员变量 ab 初始化
  --- 父类静态代码块开始 ---
  --- 父类静态代码块结束 ---
  父类 A 的常量 ab： A.ab 会调用 aB()，结果:aB
  ``````````````````````````````````````````````````````````````````````````
  子类 B 从 A 继承到的常量 ab： B.ab 会调用 aB()，结果:aB
  ~~~

  > **结论**
  > B.ab 没有初始化子类 B 的静态成员，印证了规则 3。
