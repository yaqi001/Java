任务
判断一个数（小于10位）的位数。
输入999，则输出 “它是个3位的数！”

~~~ java
public class helloWorld {
	public static void main(String[] args){
		int num = 1000000000;
		int count = 0;
		for (int i = 1; i <= 1000000000; i *= 10 ){
		    if (num % i != num){
		        count ++;
		        continue;
		    }
		    //else{
				System.out.println("位数：" + count);
				break;
		    //}
		}
	}
}
~~~

