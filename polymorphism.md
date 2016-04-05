# 多态

* 对象的多种形态

1. 引用多态：
   父类引用可以指向本类的对象。
   父类引用可以指向子类的对象。

2. 方法多态：
   创建本类对象时，调用的方法为本类方法。
   创建子类对象时，调用的方法为子类重写的方法或者继承的方法。Q: 那子类独有的方法可以被调用么？不可以！！！

------
~~~ java
public class Animal {
	public void eat(){
		System.out.println("Animal is eating");
	}
}

public class Dog extends Animal {
	public void eat(){
		System.out.println("Dog is eating meat!");
	}
	public void play(){
		System.out.println("Dog is playing ball.");
	}
}

public class Cat extends Animal {
	public void sleep(){
		System.out.println("Cat is sleeping!");
	}
}

public class Initail {
	public static void main(String[] args) {
		// Dog dd = (Dog)new Animal(); 意义何在？
		Animal d = new Dog(); // 父类引用可以指向子类对象（引用多态）
		d.eat();
		// d.play(); //！！！如果指向子类对象的父类引用去调用子类独有的方法的话是不可以的！！！
		Dog dog = new Dog();
		dog.eat();
		dog.play();
		System.out.println("-----------------------------------");
		Animal c = new Cat();
		Cat cat = new Cat();
		cat.eat();
		c.eat();
	}
}
     
