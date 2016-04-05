# 自增

  ~~~ java
  [zhangyaqi@localhost LearningByNotepad]$ cat addadd.java 
  public class addadd{
	  public static void main(String[] args){
		  int a = 5;
		  int b = a++;
		  System.out.println("a = " + a);		
		  System.out.println("b = " + b);	
	  }
  }
  [zhangyaqi@localhost LearningByNotepad]$ javac addadd.java 
  [zhangyaqi@localhost LearningByNotepad]$ java addadd
  a = 6
  b = 5
  ~~~

  一定要注意哦！自增和自减运算符只能用于操作变量，不能直接用于操作数值或常量！例如 5++ 、 8-- 等写法都是错误滴！
