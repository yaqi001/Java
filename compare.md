# 比较运算符

1、  > 、 < 、 >= 、 <= 只支持左右两边操作数是数值类型。

2、  == 、 != 两边的操作数既可以是数值类型，也可以是引用类型。

~~~ java
[zhangyaqi@localhost LearningByNotepad]$ cat compare.java 
public class compare{
	public static void main(String[] args){
		//String a = "a";
      //String b = "b";
      int a = 1;
      int b = 2;
      boolean c = a > b;
      System.out.println(c);
	}
}
[zhangyaqi@localhost LearningByNotepad]$ javac compare.java 
[zhangyaqi@localhost LearningByNotepad]$ java compare 
false
~~~
