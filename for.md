~~~ java
public class helloWorld {
	public static void main(String[] args){
		for(int i = 0, j = 1; i < 5 || j < 5; i ++, j ++){
			System.out.println(i + "---" + j);
		}
	}
}
~~~

> **注意**：
> 1、 for 关键字后面括号中的三个表达式必须用 “;” 隔开，三个表达式都可以省略，但 “;” 不能省略。

		a. 省略“循环变量初始化”，可以在 for 语句之前由赋值语句进行变量初始化操作。

		b. 省略“循环条件”，可能会造成循环将一直执行下去，也就是我们常说的“死循环”现象。

			在编程过程中要避免“死循环”的出现，因此，对于这种情况可以在循环体中使用 break 强制跳出循环（关于 break 的用法会在后面介绍）。

		c. 省略“循环变量变化”，可以在循环体中进行循环变量的变化。

  2、 for 循环变量初始化和循环变量变化部分，可以是使用 “,” 同时初始化或改变多个循环变量的值，如：

  3、 循环条件部分可以使用逻辑运算符组合的表达式，表示复杂判断条件，但一定注意运算的优先级，祥见上面的例子程序。

~~~ java
public class HelloWorld {
    //完成 main 方法
    public static void main(String[] args) {
        for(int i = 0; i < 9; i ++){
			int j = 0;
			System.out.println(i + "===" + j);
			j ++;
        }
    }
}
~~~

注意，这里 for 循环里可以有 int j = 0; 因为对于每次循环来说都是第一次见到 int j = 0;

