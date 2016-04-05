# Java 可以通过初始化块为成员变量赋值。

* **在类的声明中，可以包含多个初始化块，当创建类的实例时，就会依次执行这些代码块。**

* **静态初始化块只在类加载时执行，且只会执行一次，同时静态初始化块只能给静态变量赋值，不能初始化普通的成员变量。**
  ~~~ java
  public class Electronics {
	  double price;
	  static String name;
	  {
		  System.out.println("代码块开始...");
		  price = 998;
		  name = "Kaven";
		  System.out.println("代码块结束...");
	  }
	  static {
		  System.out.println("静态代码块开始...");
		  name = "Lisa";
		  Electronics e = new Electronics();
		  e.price = 10101;
		  System.out.println(name + e.price);
		  System.out.println("静态代码块结束...");
	  }
	  public Electronics(){
		  System.out.println("构造函数");
	  }
	  public Electronics(String s){
		  System.out.println("hello" + s);
	  }
  }
  public class InitialElectronics {
	  public static void main(String[] args) {
		  // TODO Auto-generated method stub
		  Electronics e = new Electronics("World");
	  }
  }
  ~~~  
  ~~~ java
  //运行结果
  静态代码块开始...
  代码块开始...
  代码块结束...
  构造函数
  Kaven10101.0
  静态代码块结束...
  代码块开始...
  代码块结束...
  helloWorld
  ~~~
