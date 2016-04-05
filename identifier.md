* 标识符：
  * 数字
  * $
  * 字母
  * 下划线
  
* JAVA 是大小写敏感的哦！  

* 并没有四舍五入哦！
  ~~~ java
  double d = 19.01;
  double dd = 19.91;
  int i = (int)d;
  int ii = (int)dd;
  System.out.println(d + "," + i);
  System.out.println(dd + "," + ii);
  ~~~
  
  运行结果
  ~~~ java
  19.01,19
  19.91,19
  ~~~
 
  强制类型转换可能会造成数据的丢失哦！

