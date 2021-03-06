# 数组

* 一维数组
步骤：

0. 声明数组：数据类型[] 数组名; or 数据类型 数据名[];

1. 分配空间：数据名 = new 数据类型[数组长度];

   > **重要**：
   > 分配空间后才可以向数组中放数据！

2. 赋值：数据名[下标] = 数组下标对应的值;

3. 直接创建数组的方式（将声明数组，分配空间和覆值合并完成）：

   * 数据类型[] 数据名 = new 数据类型[]{值, 值, ...};
     > **重要**
     > 这里的 [] 里面并没有写明数组的长度。

   * 数据类型[] 数组名 = {值, 值, ...};


* 二维数组
步骤：

0. 声明数组 & 分配空间：数据类型[][] 数组名; or 数据类型 数据名 [][];

                        数据名 = new 数据类型[行的个数][列的个数];

1. 覆值：数据名[行的索引][列的索引] = 值;

2. 需要了解的：在定义二维数组时也可以只指定行的个数，然后再为每一行分别指定列的个数。如果每行的列数不同，则创建的是不规则的二维数组，如下所示：
	
   ~~~ java
	String[][] str = new String[3][];
	str[0] = new String[3];
	str[1] = new String[5];
	str[2] = new String[7];
   ~~~
