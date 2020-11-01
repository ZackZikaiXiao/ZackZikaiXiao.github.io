### 一、讲解视频

[bilibili通道](https://www.bilibili.com/video/BV1YD4y197mg/)

### 二、要点强调

- 请认真研读参考代码，争取做到每一行都可以理解
- 更改参考代码，以实现你想要的程序效果
- 可以在<u>参考资料一</u>网站上学习和进一步研究C语言
- 使用<u>参考资料二</u>来检查代码
- 使用<u>参考资料三或四</u>运行代码

### 三、参考代码

```c
#include <stdio.h>


int add(int x, int y) {
	int sum = x + y;
	return sum;
}


int main() {
	/*一、数据类型部分*/
	char charObject = 'a';
	short shortObject = 254;
	int intObject = 20;
	float floatObject = 30.0;
	double doubleObject = 40.0;

	/*二、运算部分*/
	intObject = intObject + 1;
	intObject = intObject * 3;  

	/*三、输出部分*/
	printf("charObject:\t%c\n", charObject);
	printf("shortObject:\t%x\n", shortObject);
	printf("intObject:\t%d\n", intObject);
	printf("floatObject:\t%.3f\n", floatObject);

	/*四、常见语句部分*/
	// PART4.1	if语句
	if (intObject < 65) {
		intObject = -1;
	}
	else if (intObject == 65) {
		intObject = 0;
	}
	else {
		intObject = 1;
	}
	printf("(IF)intObject:\t%d\n", intObject);
	// PART4.2 for语句
	for (int i = 0; i < 100; i = i + 1) {
		intObject = intObject + i;
	}
	printf("(FOR)intObject:\t%d\n", intObject);
	// PART4.3 while语句
	while (shortObject > 0) {
		shortObject = shortObject - 1;
	}
	printf("(WHILE)shortObject:\t%x\n", shortObject);

	/*五、函数*/
	int sum = add(1, 3); 
	printf("sum:\t%d\n", sum);
}
```

### 四、参考资料

1. [C语言教程](https://www.runoob.com/cprogramming/c-data-types.html)

2. [代码检查](https://gcc.godbolt.org/)

3. [菜鸟工具编译器](https://c.runoob.com/compile/11)

4. [wandbox编译器](https://wandbox.org/)

