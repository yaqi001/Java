# 继承

* 初始化父类对象而后再初始化子类对象

* 先执行初始化对象中的属性，再执行构造方法中的初始化。

~~~ java
public class Animal {
	private String name = showName();
	private static int age = showAge();
   {
	   System.out.println("Animal 代码块");
   }
   static {
	   System.out.println("Animal 静态代码块");
   }
	private static int showAge(){
		System.out.println("Animal 类静态成员变量初始化");
		return 0;
	}
	private String showName(){
		System.out.println("Animal 类非静态成员变量初始化");
		return "动物";
	}
	public Animal(){
		System.out.println("Animal 的构造方法");
	}
}
public class Dog extends Animal {
	private static int birthYear = 2010;
	private static int age = showAge(birthYear);
	private String gender = showGender();
   protected String name = "halo JAVA";
   {
	   System.out.println("Dog 代码块");
   }
   static {
	   System.out.println("Dog 静态代码块");
   }
	public Dog(){
      super();//注意super()必须在第一行，且写不写的效果都是一样的，因为系统会默认调用父类的无参构造方法。
      // super(参数); // 如果想在子类构造方法中调用分类的有参构造方法的话。且只能在第一行写。所以一个方法体中只能写一个关于 super() 的语句。

		System.out.println("Dog 的构造方法");
		birthYear = 2015;
	}
	private String showGender() {
		System.out.println("Dog 类非静态成员变量初始化");
		return "female";
	}
	private static int showAge(int a){
		System.out.println("Dog 类静态成员变量初始化");
		return 2016 - a;
	}
}
public class Test {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Dog d = new Dog();
		System.out.println("----------------");
		Animal aDog = new Dog();
	}
}
~~~
~~~ java
//运行结果
Animal 类静态成员变量初始化
Animal 静态代码块
Dog 类静态成员变量初始化
Animal 静态代码块
Animal 类非静态成员变量初始化
Animal 的构造方法
Dog 类非静态成员变量初始化
Dog 的构造方法
----------------
Animal 类非静态成员变量初始化
Animal 的构造方法
Dog 类非静态成员变量初始化
Dog 的构造方法
~~~

> **总结**
> 当我们创建一个子类对象的时候（Dog dog = new Dog();），那么一定会先创建一个父类的对象，再创建一个子类对象出来。不过我们可以肉眼看到创建的子类对象，没有看到父类对象，那么这个父类对象在哪里呢？我们如何才能看到它呢？？用 super 关键字哦！！！！！
> **如果子类构造方法中既没有调用父类的构造方法，而父类中又没有定义无参的构造方法的话，编译会出错。（这是因为不在子类构造方法中显式调用父类的构造方法的话，会默认调用父类的无参构造方法（定义与否都无所谓）～而如果在父类中定义了一个有参的构造函数的话，系统就不会自动生成无参的构造方法了，没有无参构造函数，又没有在子类中调用 super(参数) 的话就会出错咯！）**


* final 关键字：字面意思就是最终的含义（即，不可修改！）

  final 可以修饰类，属性，方法，变量。
  
1. final 修饰类：该类不允许被继承。

2. final 修饰方法：该方法不允许被重写。
                   可以被重载么？可以。
   static 修饰方法：名义上可以被重写，但没有起到重写所要达到的效果。

	~~~ java
   public class FinalParentClass {
		public static void show(){
			System.out.println("父类 static show()");
		}
		public void print(){
			System.out.println("父类 print()");
		}
	}
   public class FinalSubClass extends FinalParentClass{
		public final static void show(){
			System.out.println("子类 final static show()");
		}
		public final void print(){
			System.out.println("子类 print()");
		}
	}
   public class FinalTest {
		public static void main(String[] args){
			FinalParentClass fpc = new FinalSubClass();
			fpc.show();
			FinalParentClass.show();
			FinalSubClass.show();
			fpc.print();
		}
	}
	~~~
	~~~ java
   // 执行结果
   父类 static show()
	父类 static show()
	子类 final static show()
	子类 print()
	~~~

3. final 属性的使用：
   
   * 使用 final 修饰的属性要么在定义的时候就初始化（如何是非 final 属性系统会自动给一个默认值），要么在构造函数里进行初始化。只能选择一种方式哦！

4. final 修饰变量：
   被 final 修饰的变量就是常量喽！

5. final 可以修饰接口吗？
