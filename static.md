* Java 中被 static 修饰的成员称为静态成员或类成员。
  Java 中被 static 修饰的函数成为静态方法或类方法。

* 使用 static 可以修饰变量、方法和代码块。**什么是代码块？**

* 使用方法：static 变量类型 变量名 = "值";
            static 方法类型 方法名(参数0, 参数1, ...){
               ...
            }
  ~~~ java
  // 共有的静态实例变量
  public static 变量类型 变量名 = "值";
  ~~~

* 该类成员，也就是被 static 修饰了的成员变量只要被不管是类调用改变的还是对象调用改变的，只要变了就是变了！
  ~~~ java
  public class Telephone { //1. 定义类
	  //2. 属性（成员变量）
	  static float screen = 100f;
	  float cpu;
	  float memory;
	  //3. 方法
	  public Telephone(){
		  System.out.println("hello world");
	  }
	  public Telephone(double screen, float cpu, float memory){
		  if (screen < 1.5){
			  System.out.println("您输入的参数是有问题的！这里将自动为 screen 进行覆值");
			  this.screen = 3;
		  }else{
			  this.screen = (float)screen;
		  }
		  this.cpu = cpu;
		  this.memory = memory;
	  }
	  void showProperty(){
		  System.out.println("screen:" + screen + "\n" + "cpu:" + cpu);
	  }
  }
	  

  public class InitialTelphone {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			// new 后面的是构造方法，用于创建一个新对象。
			Telephone tp = new Telephone();
			System.out.println(Telephone.screen);
			System.out.println(tp.screen);
			tp.screen = 222;
			System.out.println(Telephone.screen);
			System.out.println("================================");
			Telephone tp1 = new Telephone(999.0, 2, 2);
			System.out.println(tp1.screen);
			System.out.println(Telephone.screen);
		}
	}
   ~~~ 


* 关于静态方法和普通方法的阐述：
  
  0. 静态方法中可以直接调用同类中的静态成员，但不能直接调用非静态成员。
  1. 如果希望在静态方法中调用非静态变量，可以通过创建类的对象，然后通过对象来访问非静态变量。
  2. 在普通成员方法中，则可以直接访问同类的非静态变量和静态变量。
  3. 静态方法中不能直接调用非静态方法，需要通过对象来访问非静态方法。
  4. 普通方法中可以直接调用静态以及非静态方法。


  ~~~ java
  public class Electronics {
	  double price;
	  static String name;
	  public static void beElectricize(){
		  System.out.println("开始充电！");
		  System.out.println(name);
		  System.out.println(price); // 这里有错误！
	  }
	  public void connectInternet(){
		  System.out.println("上网中...");
		  beElectricize();
		  System.out.println(name);
		  System.out.println(price);
	  }
	  public void call(){
		  System.out.println("打电话了哦～～");
	  }
	  public static void getTiny(){
		  beElectricize();
		  call(); // 这里有错误！
	  }
  }

  public class InitialElectronics {
	  public static void main(String[] args) {
		  // TODO Auto-generated method stub
		  Electronics e = new Electronics();
		  e.price = 10000;
		  e.name = "iphone";
		  e.connectInternet();
	  }
  }
  ~~~

* 关于类中的静态方法
  ~~~ java
  public class Father {
	  private String name;
	  private int age;
	  public String getName() {
		  return name;
	  }
	  public void setName(String name) {
		  this.name = name;
	  }
	  public int getAge() {
		  return age;
	  }
	  public void setAge(int age) {
		  this.age = age;
	  }
	  public static void showInfo(){
		  System.out.println("父类静态方法");
	  }
  } 
  public class Son extends Father{
	  public static void showInfo(){
		  System.out.println("子类静态方法");
	  }
  public static void print(){
		  System.out.println("子类独有的静态方法");
	  }
  }
  public class TestClass {
	  public static void main(String[] args) {
		  // TODO Auto-generated method stub
		  Father fSon = new Son();
		  fSon.showInfo(); // fSon 终究是 Father 类型的，所以调用的是 Father 类中的静态方法。
		  //fSon.print(); // The method print() is undefined for the type Father
		  Son son = new Son();
		  son.showInfo();
		  son.print();
	  }
  }
  ~~~
  ~~~ java
  // 运行结果
  父类静态方法
  子类静态方法
  子类独有的静态方法
  ~~~


