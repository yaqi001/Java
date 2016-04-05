# 

~~~ html
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
		Cat cat = new Cat();
		Animal animal = cat;
		Dog dog = (Dog)animal;
	}
}
~~~

> **重要**
> 上面的代码在编译期间是没有错误的，一旦执行会报以下错误：
  ~~~ bash
  Exception in thread "main" java.lang.ClassCastException: com.polymorphism.Cat cannot be cast to com.polymorphism.Dog
  at com.polymorphism.Initail.main(Initail.java:7)
  ~~~

* 针对于以上的问题，我们可以使用 `instanceof` 运算符来避免类型转换的安全性问题

* **instanceof**：用于在运行时指出对象是否是特定类的一个实例。

  ~~~ html
  public class Initail {
	  public static void main(String[] args) {
		  Cat cat = new Cat();
		  Animal animal = cat;
		  if(animal instanceof Dog){
			  Dog dog = (Dog)animal;
		  }
		  else{
			  System.out.println("无法将 animal 对象转换成 Dog 类型");
		  }
	  }
  }
  ~~~
