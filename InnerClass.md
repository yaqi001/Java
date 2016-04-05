# 内部类（大头）

参考博客：[http://www.cnblogs.com/chenssy/p/3388487.html](http://www.cnblogs.com/chenssy/p/3388487.html)

* **成员内部类**
  带有内部类的外部类在编译完成后，你会发现不仅仅只有一个 **.class** 文件。

  ~~~ java
  public class Test {
	  class SubTest {
		  int i = 0;
	  }
	  static class StaticSubTest{
		  int j = 9;
	  }
	  public static void main(String[] args) {
		  Test t = new Test();
		  SubTest st = t.new SubTest();
		  Test.StaticSubTest sst = new Test.StaticSubTest();
	  }
  }
  ~~~
 
  ~~~ bash
  [zhangyaqi@localhost LearningByNotepad]$ javac Test.java
  ~~~
   
  ~~~ bash
  [zhangyaqi@localhost LearningByNotepad]$ ll | grep Test.*.class
  -rw-rw-r--. 1 zhangyaqi zhangyaqi  477 3月  23 15:29 Test.class
  -rw-rw-r--. 1 zhangyaqi zhangyaqi  289 3月  23 15:29 Test$StaticSubTest.class
  -rw-rw-r--. 1 zhangyaqi zhangyaqi  329 3月  23 15:29 Test$SubTest.class
  ~~~
  --------
    
  ~~~ java
  public class OutterClass {
	  private String name;
	  private int age;
	  public OutterClass(){
		  System.out.println("OutterClass 构造方法");
	  }
	  public class InnerClass {
		  private double score;
		  public InnerClass(){
			  System.out.println("InnerClass 构造方法");
		  }
	  }
  }
  
  // import com.innerClass.OutterClass.InnerClass;
  public class Test {
	  public static void main(String[] args){
		  OutterClass oc = new OutterClass();
		  OutterClass.InnerClass ic = oc.new InnerClass(); // 这里内部类引用的类型是 OutterClass.InnerClass，如果指明 OutterClass 的话，使用上面的 import 语句也可以！
	  }
  }
  ~~~
  ~~~ bash
  // 运行结果
  OutterClass 构造方法
  InnerClass 构造方法
  ~~~
  
  --------
  ~~~ java
  public class OutterClass { // 定义外部类
	  private int out_v = 1;
	  private int hah = out_v; // 本类中的私有属性不是只能被方法访问，也可以被其他的私有成员变量访问
	  private String same = "外部";
	  private void out_f(){
		  System.out.println("外部类中的成员变量 out_v = " + out_v); // 访问本外部类的私有属性
		  System.out.println("外部类的方法访问内部类中的私有成员变量 name = " + ((new OutterClass()).new InnerClass()).name); // 访问内部类中的非同名私有成员变量
        System.out.println("外部类的方法访问内部类中的同名成员变量 same：" + (this.new InnerClass()).same); // 访问内部类中的同名私有成员变量。输出：内部
        System.out.println("访问自己的有两种方式" + this.same + same); // 输出：外部外部
	  }
	  private class InnerClass{ // 定义内部类
		  private String name = "InnerClass"; 
		  private String same = "内部";
		  private void inner_f(){
			  System.out.println("内部类访问外部类的私有成员变量 out_v = " + out_v + "=====" + hah); // 访问外部类中非同名的私有变量！！！！！
           System.out.println("内部类访问外部类的同名私有成员变量，OutterClass.this.same：" + OutterClass.this.same); // 访问外部类中同名的私有变量！！！！！输出：外部
           System.out.println("OutterClass.this：" + OutterClass.this); // OutterClass.this：staticInnerClass.OutterClass@2a139a55
           System.out.println("InnerClass.this：" + InnerClass.this); // InnerClass.this：staticInnerClass.OutterClass$InnerClass@15db9742
           System.out.println("访问自己的有两种方式" + this.same + same); // 输出：内部内部
		  } 
	  }
	  public OutterClass(){
		  System.out.println("外部类的构造方法");
	  }
	  public static void main(String[] args){
		  OutterClass oc = new OutterClass();
		  System.out.println("oc: " + oc); // oc: staticInnerClass.OutterClass@2a139a55
		  oc.out_f();
		  InnerClass ic = oc.new InnerClass();
		  System.out.println("ic: " + ic); // ic: staticInnerClass.OutterClass$InnerClass@15db9742
		  ic.inner_f(); 
	  }
  }
  ~~~
  ~~~ java
  //运行结果
  外部类的构造方法
  外部类中的成员变量 out_v = 1
  外部类的构造方法
  外部类的方法访问内部类中的私有成员变量 name = InnerClass
  内部类访问外部类的私有成员变量 out_v = 1=====1
  ~~~

* **静态内部类**

  静态内部类是 static 修饰的内部类，这种内部类的特点是：

  1、 静态内部类不能直接访问外部类的非静态成员，但可以通过 new 外部类().成员 的方式访问 

  2、 如果外部类的静态成员与内部类的成员名称相同，可通过“类名.静态成员”访问外部类的静态成员；如果外部类的静态成员与内部类的成员名称不相同，则可通过“成员名”直接调用外部类的静态成员

  3、 创建静态内部类的对象时，不需要外部类的对象，可以直接创建 内部类 对象名= new 内部类();
  
  ~~~ java
  public class OutterClass {
	  private static String name = "外部静态成员变量";
	  private String name_ = "外部非静态成员变量";
	  // 静态内部类
	  public void showStaticInnerClass(){
		  System.out.println("访问静态内部类的同名静态成员变量 name = " + new StaticInnerClass().name);
		  System.out.println("访问静态内部类的同名非静态成员变量 name_ = " + new StaticInnerClass().name_);
	  }
	  public static class StaticInnerClass{
		  private static String name = "内部静态成员变量";
		  private String name_ = "内部非静态成员变量";
		  public void showStaticInnerClass(){
			  System.out.println("访问静态外部类的同名静态成员变量 name = " + new OutterClass().name);
			  System.out.println("访问静态外部类的同名非静态成员变量 name_ = " + new OutterClass().name_);
		  }
	  }
	  public static void main(String[] args) {
		  // TODO Auto-generated method stub
		  OutterClass oc = new OutterClass();
		  StaticInnerClass sic = new StaticInnerClass();
		  oc.showStaticInnerClass();
		  sic.showStaticInnerClass();
	  }
  }
  ~~~

  ~~~ java
  // 运行结果
  访问静态内部类的同名静态成员变量 name = 内部静态成员变量
  访问静态内部类的同名非静态成员变量 name_ = 内部非静态成员变量
  访问静态外部类的同名静态成员变量 name = 外部静态成员变量
  访问静态外部类的同名非静态成员变量 name_ = 外部非静态成员变量
  ~~~


* **匿名内部类**：就是没有名字的内部类，多用于关注实现而不关注（实现类的）名称。

  ~~~ java
  Interface i = new Interface(){
     public void method(){
        System.out.println("匿名内部类");
	  }
  }
  ~~~
