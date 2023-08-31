# 0. 题解

`解题人: 杨鹏达`

```
2 ^ 10 = 1024 对应于十进制的 4 位,那么 2 ^ 10000 对应于十进制的多少位呢
```
### 知识点:
  - 智力题
  - 可用Python暴力求解

### 答案:
- 智力解:
```
因为 2^10 对应 10^3
对 2^10000 两边同时取对数
2^10000 = 10^x
lg2^10000 = lg10^x
10000lg2 = x
lg2 约为 0.30100
```
`所以答案为:十进制下约为3011位`

- Python暴力求解:

`print(len(str(2**10000)))`

输出结果为3011,Python语法可与题解不一致,最好现场让跑一下

### 评价标准
A. `智力解法`与`Python`都会为最优

B. 只会`智力解法`

C. 只会`Python`(需写出语法)

D. 说Python可以解,但写不出来语法

# 1. 题解

`解题人：李泉霖`

```
int main(void){
    if((3 + 2 < 2) > (3 + 2 > 2))
        printf("Welcome to Xiyou Linux Group\n");
    else
        printf("%d\n",printf("Xiyou Linux Group - 2%d",printf("")));
}
```

### 知识点:
  <!-- - 运算符号的优先级 -->
  - 关系运算符用于比较运算的返回值
  - printf（）函数的返回值

### 答案:
  - 关系运算符用于比较运算的返回值
```
    关系运算符号包括大于(>)、小于(<)、等于(==)、 大于等于(>=)、小于等于(<=)和不等于(!=)六种。
    他们用于比较的返回指均为1（true）和0 （false）。
```

(3 + 2 < 2)的结果为flase,即0,(3 + 2 > 2)的结果为true,即1，if(0 > 1)为0（false）,所以if语句执行else

 - printf()函数的返回值
```
    printf()的返回值为printf()中字符的个数。输出结果为栈式，先进后出.
```
输出结果为： ` `->`Xiyou Linux Group - 20`->`Xiyou Linux Group - 2022`

### 评价标准
A.能够清楚地讲出`printf()返回值`和`关系运算符用于比较运算的返回值`两个知识点。

B.能够清楚地讲出`printf()返回值`和`关系运算符用于比较运算的返回值`两个知识点，但对于printf()返回值了解不够，比如不知道%d所占的字符数为%d所输出的字符数。

C.能够说出结果，知道关系运算符，但不能清楚讲出printf()的知识。

D.能够说出结果，但不清楚为什么是这么处理的。

#### 提高：了解char字符占位情况（不包括其他字符类型,如wchar_t）：
（答案简述）能说出c语言 char 类型的英文，始终使用 ASCII 编码。对于包括中文的，GCC编译器使用和源文件相同的编码来保存这些字符（其他编译器有相同也有不一样的情况,比如微软编译器使用本地编码），源文件根据IDE和编译器不同选择使用本地编码或默认UTF8。

# 2. 题解
`解题人：袁野`
```c
int main(void)
{
    char p0[] = "Hello,Linux";
    char *p1 = "Hello,Linux";
    char p2[11] = "Hello,Linux";
    printf("pO == p1:%d, strcmp(p0, p2):%d\n", p0 == p1, strcmp(p0, p2));
    printf("sizeof(p0):%zu, sizeof(p1):%zu,sizeof(*p2):%zu\n", sizeof(p0), sizeof(p1), sizeof(*p2));
    printf("strlen(p0)：%zu,strlen(p1):%zu\n", strlen(p0), strlen(p1));
}`
```
### 知识点：
- 对sizeof(),strlen()的理解。
- strcmp()的理解。
- 对全局常量区的了解。
### 答案：
```c
p0 == p1:0
strcmp(p0, p2):-72 
sizeof(p0):12
sizeof(p1):8 
sizeof(*p2):1 
strlen(p0):11 
strlen(p1):11
```
注：`strcmp(p0, p2)`的值不一定为-72。
### 评价标准：
A：指出`strcmp(p0, p2)`的值不一定为-72，为-72的原因是因为：编译器在内存分配时，`p2`之后紧挨着`p0`，即`p2[11]`为`p0[0]`的那个`'H'`,而`'H'`的ASCII码值为72。这只是编译器的一种`优化`，并没有保证。
~~Daz: 编译器行为,用clang编译答案还可以是0~~
B：指出`strcmp()`比较两个字符串的过程。本题中`strcmp(p0, p2)`的结果值为`p0[11] - p2[11]`的值。解释出第一个输出，全局常量区。
C：能够准确地解释出使用`sizeof()`和`strlen()`的五个输出的结果，指出*p2是第一个字符。
D：仅运行程序并得到运行结果，仅知道sizeof()和strlen()的用法。

# 3.题解

`解题人：许泽文`

>请结合本题，分别谈一谈C语言中全局变量和局部变量的生命周期的理解
~~~c
int a = 3;
void test()
{
	int a = 1;
	a += 1;
     {
         int a=a+1;
	     printf("a=%d\n", a);
     }
	printf("a=%d\n", a);
	
}
int main()
{
	test();
	printf("a=%d\n", a);
	return 0;
}
~~~


### 知识点
* 局部变量和全局变量的区别
* 局部变量和全局变量的生命周期的区别
* UB行为



### 答案
* 全局的变量a=3，所以在main函数中的a打印结果是3，不受test()影响
* test()里面的在局部作用域前的a=2，在局部作用域里面a=a+1，这是一个UB行为，输出的值不固定
* 局部作用域里的a不影响外面的a，所以下面打印的a=2

* 局部变量的生命周期在自己作用域结束之后，生命周期就结束了
* 全局变量的生命周期不受局部作用域影响，在main函数结束之后，生命周期才结束

```
Daz:
UB行为:Undefined Behaivor
X86-64 gcc 12.2 输出的UB一行的汇编代码为:add     DWORD PTR [rbp-8], 1
就是给一个未初始化的地址的值加了1,所以最终导致什么结果取决于编译器
```

### 评级标准
A. 题目a的输出都会，了解UB行为，懂得全局变量和局部变量生命周期，对拓展问答如流

B. 除UB行为外,其他都会，了解部分全局变量和局部变量生命周期

C. 题目a的输出或者全局变量与局部变量会一些,能说出部分细节

D. 能说出结果，但不懂得为什么这样处理

**提高**
可现场考察static和全局变量与局部变量的结合情况,生命周期的变化

# 4. 题解

`解题人: 郭天宇`

- `union` 与 `struct` 各有什么特点呢，你了解他们的内存分配模式吗。

```c
typedef union {
  long l;
  int i[5];
  char c;
} UNION;

struct data {
  int like;
  UNION coin;
  double collect;
} STRUCT;

int main(void) {
  printf("sizeof(UNION) = %zu\n", sizeof(UNION));
  printf("sizeof(STRUCT) = %zu\n", sizeof(STRUCT));
}
```

### 知识点:

- 32 位机和 64 位机
- 联合体内存模型
- 结构体内存模型

### 答案:

- Linux64 位机

```
sizeof(UNION) = 24
sizeof(STRUCT) = 40
```

- Linux32 位机

```
sizeof(UNION) = 20
sizeof(STRUCT) = 32
```

- Windows64 位机

```
sizeof(UNION) = 20
sizeof(STRUCT) = 32
```

- Windows32 位机

```
sizeof(UNION) = 20
sizeof(STRUCT) = 32
```

`题解（Linux64位机为例）`

- 32 位机和 64 位机

| c 类型 | 32 位(linux) | 64 位(linux) | 32 位(win) | 64 位(linux) |
| ------ | ------------ | ------------ | ---------- | ------------ |
| char   | 1            | 1            | 1          | 1            |
| short  | 2            | 2            | 2          | 2            |
| int    | 4            | 4            | 4          | 4            |
| long   | 4            | 8            | 4          | 4            |
| 指针   | 4            | 8            | 4          | 8            |

- 联合体内存模型

  >

       1)联合体是一个结构；

       2)它的所有成员相对于基地址的偏移量都为0；

       3)此结构空间要大到足够容纳最"宽"的成员；

       4)其对齐方式要适合其中所有的成员
       (保证是所有成员类型size的最小公倍数)；

如图所示：

![](https://img-blog.csdnimg.cn/7bd1f8023dd746f289377161d1e1d201.png#pic_center)

- 结构体内存模型

>

    1. 第一个成员在结构体变量偏移量为0的地址处。

    2. 其他成员变量要对齐到某个数字（对齐数）的整数倍的地址处。对齐数 = 编译器默认的一个对齐数与该成员大小中的较小值。vs中默认值是8 Linux默认值为4.

    3. 结构体总大小为最大对齐数的整数倍。（每个成员变量都有自己的对齐数）

    4. 如果嵌套结构体，嵌套的结构体对齐到自己的所有成员最大对齐数（就是该嵌套结构体的对齐数）的整数倍处，结构体的整体大小就是所有成员对齐数的最大值（包含嵌套结构体和；联合体的对齐数）的整数倍。

如图所示

![在这里插入图片描述](https://img-blog.csdnimg.cn/7f1f62671c78468ea71d08790ea06066.png#pic_center)

### 评价标准

A. 理解结构体和联合体类型的嵌套，正确计算 STRUCT 大小

B. 理解联合体内存模型和结构体内存模型，正确计算 UNION 大小

C. 只理解联合体和结构体中的一个

D. 只能区分不同机型数据类型所占字节大小，对结构体和联合体的内存模型理解的模模糊糊

# 5.题解

`解题人：胡宇腾` 
   
```
int main(void)
{
    unsigned char a = 4 | 7;
    a <<= 3;
    unsigned char b = 5 & 7;
    b >>= 3;
    unsigned char c = 6 ^ 7;
    c = ~c;
    unsigned short d = (a ^ c) << 3;
    signed char e = -63;
    e <<= 2;
      
    printf("a:%d , b:%d , c:%d , d:%d\n", a, b, c, (char)d);
    printf("e:%#x\n", e);
}
```
### 知识点：
* 位运算相关知识
* 左移运算，无符号右移，最高位补0
* %#x  带格式输出，十六进制前加0x

拓展：
* 有符号右移，如果原最高位为1,则右移后最高位补1
* 无符号最高位为1,右移最高位补0
* 如何用位运算获取相反数？（取反加一）
* %#X 前缀为0X，%#o 前缀为0
```
Daz:
X86_64 的Windows与Linux下，在微软的标准里：
负数的 左移 为UB行为（未定义）
负数的 右移 为implementation-defined（实现定义）
```

### 答案
```
a:56, b:0, c=254, d=48
e:0x4
```
### 解析
a:
```
        0000 0100
        0000 0111
    |   0000 0111
  <<3   0011 1000
  
%d  56
```
b:
```
        0000 0101
        0000 0111
    &   0000 0101
  >>3   0000 0000
  
%d  0
```
c:
```
        0000 0110
        0000 0111
    ^   0000 0001
    ~   1111 1110

c数据类型为unsigned char 输出为正

%d  254
```
d:
```
        0000 0000 0011 1000
        0000 0000 1111 1110
    ^   0000 0000 1100 0110
  <<3   0000 0110 0011 0000
(char)            0011 0000

%d  48
```
e:
```
        1100 0001
  <<2   0000 0100
  
%#x  0x4
```
### 评价标准

A: 所有知识点以及拓展第1,2，3条完全掌握（第4条测试学习相关知识的宽度，不作记录）

B：题目中的知识点以及拓展第1,2，3条可以说出答案但不熟悉

C：仅可以说出知识点内容，但不太清楚拓展内容

D：很少有相关知识储备

# 6. 题解

`解题人: 封宇腾`

```
说说下面数据类型的含义。 A. char *const p。 
B. char const *p。 C. const char *p。 
```
### 知识点:
  - 指针
  - 指针常量
  - 常量指针
  - const

### 答案:
- 解:

 * char *const p 定义一个指向字符常量的指针，这里，ptr是一个指向 char* 类型的常量，所以不能用ptr来修改所指向的内容，p指向的内容是可以修改的，p的地址不能改变

* char const *p  我们可以看到const是修饰 指针p指向char类型，p的地址是可以修改的，p指向的内容不能改变
* 同上放置的顺序不一样但是效果一致


### 评价标准
A. 能清晰流利的说出两种用法的区别

B. 对其中一种可以清晰说出，另一种含糊不清

C. 能大致说出

D. 解释含糊不清，禁不住反问就改口

提高：
     了解c语言的中const关键字会申请内存空间吗？
```
在c语言中，用const定义一个常量的时候，编译器会直接开辟一个内存空间存放该常量，不会进行优化。 
并且当我们用一个指针去指向该变量的时候我们是可以对该变量进行修改的。
我们可以利用一个指针去指向该变量，然后间接修改该空间的值
```

# 7. 题解

`解题人: 封宇腾`

```
用变量 p 给出下面的定义： 
A. 含有 10 个指向 int 的指针的数组。
B. 指向含有 10 个 int 数组的指针。
C. 含有 3 个『指向函数的指针』的数组，被指向的函数有 1 个 int 参数并返回 int。
```
### 知识点:
  - 指针
  - 指针数组
  - 数组指针
  - 函数指针

### 答案:
```
基础：对于产生指针数组，与数组指针的符号优先级问题

(*p)[n]：根据优先级，先看括号内，则p是一个指针，这个指针指向一个一维数组，数组长度为n，这是“数组的指针”，即数组指针；

*p[n]：根据优先级，先看[]，则p是一个数组，再结合*，这个数组的元素是指针类型，共n个元素，这是“指针的数组”，即指针数组。

```

- 解:

* 含有 10 个指向 int 的指针的==数组==
```c
int* p[10]；
```
* 指向含有 10 个 int 数组的==指针==
```c
int arr[10] = {0};    int (*parr)[10] = &arr;
```

*  含有 3 个『指向函数的指针』的数组，被指向的函数有 1 个 int 参数并返回 int。
```c
int (*p[3])(int )
Daz:
declare p as array 3 of pointer to function (int) returning int
```

```
p[3]代表了它是一个数组，该数组有三个元素，int(*)(int)说明了数组的每一个元素是一个函数指针，该指针指向的函数有一个int型参数，返回值为int
```

### 评价标准
A. 能清晰的说出符号优先级顺序，并指明3种区别,会调用函数指针

B. 能指明3种区别，但对符号优先级别无法清晰说明

C. 对符号的优先级顺序不了解，能写出三种类型

D. 无法写出

# 8. 题解：

解题人：`姚思远`

```
你对排序算法了解多少呢？谈谈你所了解的排序算法的思想、稳定性、时间复杂度、空间复杂度。动动你的小手敲出来更好哦~~~
```

## 知识点：

- 排序算法的思想
- 排序算法的时间复杂度和空间复杂度

## 答案：

```c
//冒泡排序
//平均时间复杂度:O(n²)
//空间复杂度：O(1)
void sort(int *a, int length){
    int i, j;
    int temp;
    for (int i = 0; i < length; i++) {
        //关键是两次趟数的分析
        for(int j = 0; j < length-i-1; j++) {
            if (a[j] < a[j+1]) {
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
            }
        }
    }
}
//冒泡优化
void sort(int *a, int length) {
    int i ,j, temp;
    int flag = true;
    for (i = 0; i < length && flag; i++) {
        flag = false;
        for (j = 0; j < length-i-1; j++) {
           if (a[j] < a[j+1]) {
                temp = a[j];
                a[j] = a[j+1];
                a[j+1] = temp;
                flag = true;
            }
        }
    }
}
//选择排序
//平均时间复杂度：O(n²)
//空间复杂度：O (1)
void sort(int *a, int length) {
    int i, j, min;
    for (i = 0; i < length; i++) {
        min = i;
        //每一次都找出来比当前值小的下标
        for (j = i + 1; j < length; j++) {
            if (a[min] > a[j]) {
                min = j;
            }
        }
        //如果两者不等，说明找到最小值
        if (i != min ) {
            swap(a, i, min);
        }
    }
}
//快速排序
//平均时间复杂度：O(nlog n)
//空间复杂度：O (log n)
void Quick_Sort(int *arr, int begin, int end){
    if(begin > end)
        return;
    int tmp = arr[begin];
    int i = begin;
    int j = end;
    while(i != j){
        while(arr[j] >= tmp && j > i)
            j--;
        while(arr[i] <= tmp && j > i)
            i++;
        if(j > i){
            int t = arr[i];
            arr[i] = arr[j];
            arr[j] = t;
        }
    }
    arr[begin] = arr[i];
    arr[i] = tmp;
    Quick_Sort(arr, begin, i-1);
    Quick_Sort(arr, i+1, end);
}
```

## 评价标准：

A:在B的基础上，可以分析出排序的时间复杂度和空间复杂度，能对排序作出优化或者写出快排

B:能完整说清冒泡或者简单选择排序的思路（或者说清任意两种排序，不限于给出的两种），可以完整手写出来两者

C:能大概说清排序的思路，并且可以手写出来一个

D:根本不知道排序

# 9. 题解

`解题人： 高鹏`


实现ConvertAndMerge函数：
拼接输入的两个字符串，并翻转拼接后得到的新字符串中所有字母的大小写。
提示：你需要为新字符串分配空间。
```c
char* convertAndMerge(/*补全签名*/);
int main(void){
    char words[2][20] = {"Welcome to Xiyou","Linux Group 2022"};
    printf("%s\n",words[0]);
    printf("%s\n",words[1]);
    char* str = convertAndMerge(words);
    printf("str=%s\n",str);
    free(str);
}
```

### 知识点：
 - 二维数组传参
 - 数组和指针关系
 - 字符串操作
 - 内存分配与释放

### 答案：
```c
char* convertAndMerge(char str1[2][20]){
    char*s=(char*)malloc(sizeof(char)*40);
    //memset(s, 0, sizeof(char)*40);
    for (int i = 0; i < 40; i++) {
      s[i] = '\0';
    }
    strcat(s,str1[0]);  //or *str1        or &str1[0][0]
    strcat(s,str1[1]);  //or *(str1+1)    or &str1[1][0]
    printf("%s\n",s);
    for(int i=0;s[i]!='\0';i++){
        if(s[i]>='a'&&s[i]<='z') 
            s[i]-=32;
        else if(s[i]>='A'&&s[i]<='Z') 
            s[i]+=32;
    }
    return s;
}
```
注：1、可改为char* convertAndMerge(char str1[2][20]){}
      char* convertAndMerge(char str1[][20]){}//只能省第一维
      char* convertAndMerge(char (*str1)[20]){}//这里注意括号
   
   2、char* convertAndMerge(char *str1){//这里传的地址  
    char*s=(char*)malloc(sizeof(char)*40);
    strcat(s,str1);//这里注意要降维  or  strcat(s,&str[0]);
    strcat(s,str1+1);//            or  strcat(s,&str[1]);   
    for(int i=0;s[i]!='\0';i++){
        if(s[i]>='a'&&s[i]<='z') 
            s[i]-=32;
        else if(s[i]>='A'&&s[i]<='Z') 
            s[i]+=32;
    }
      return s;
    }
    3、大小写转换可用C的函数toupper
    4、字符串连接也可自己写，但注意\0的处理


输出：
```c
Welcome to Xiyou
Linux Group 2022
str=wELCOME TO xIYOUlINUX gROUP 2022
```


### 评价标准
A. 能说出代码细节，能说出其他的改法，并能对所考知识点的相关拓展对答如流

B. 能说出一种代码细节，并能回答部分知识点

C. 能说出思路和要部分要注意的细节

D. 只能说出大概思路

Daz:
- 扩展:
问下最后的 `free` 是什么意思, 关于内存分配和内存泄漏都了解多少(主要问内存分配)

# 10.题解
`解题人:许泽文`
- 程序的输出有点奇怪，请尝试解释一下输出
~~~c
int main(int argc, char **argv)
{
  int arr[5][5];
  int a = 0;
  for (int i = 0; i < 5; i++) {
    int *temp = *(arr+i);
    for(; temp < arr[5]; temp++) {
      *temp = a++;
    }
  }

  for(int i = 0; i < 5; i++) {
    for(int j = 0; j < 5; j++) {
      printf("%d\t", arr[i][j]);
    }
    printf("\n");
  }
}
~~~

### 知识点
* 指针的理解
* 二维数组
* 

### 答案
输出结果
~~~c
0       1       2       3       4
25      26      27      28      29
45      46      47      48      49
60      61      62      63      64
70      71      72      73      74
~~~

**题解**

1. arr数组名是二级数组的地址也就是首行的地址，第一次进入,(arr+i)，就是首行的地址， 
2. (arr+i)就是首元素的地址，这里的temp就是首元素的地址，对temp进行操作会影响arr数组
3. temp< arr[5],就是到二维数组最后一个元素地址的下一个地址截止,a++,先赋值再++，所以第一个位置是0，后面依次增加，第一次遍历的结果是从0-24
4. 进入第二次循环i=1，temp指向的是第二行首元素的地址，再进入到temp < arr[5]的循环中,从第二行首元素开始遍历数组，就是从25-44
5. 同理，依次类推，i=2，就从第3行首元素开始,遍历数组，就是45-59
6. i=3就从第4行开始，i=4从第5行开始，重复上述的操作,最终的结果就是上面输出的结果

### 评价标准

A. 能够完整的解出题目，了解这里不同值出现的原因，懂得其他的问法，对拓展问答如流

B. 懂得二维数组的数组名含义，对二维数组数组名+i，指向的地址，能够了解部分原理，非拓展部分

C. 能说出思路和注意的细节

D. 知道答案，不清楚原理

# 11. 题解

`解题人: 郭天宇`

- 直接运行程序 `argc` 的值为什么是 1？
- 程序会出现死循环吗？
- 你了解 `argc` 和 `argv` 吗？

```c
int main(int argc, char **argv) {
  printf("argc = %d\n", argc);
  while (1) {
    argc++;
    if (argc < 0) {
      printf("%s\n", (char *)argv[0]);
      break;
    }
  }
}
```
### 知识点:
- argc和argv的含义和用法
- 整型的溢出  

### 答案:
1. argc表示传入main函数的参数个数。
2. argv表示传入main函数的参数序列或指针。
3. 参数包括程序本身，所以argc至少为1,argv[0]表示这个程序的名字.
4. 不会出现死循环，argc为int类型, 能表示的最大正整数为2的32次方减1，当超过这个范围后就会发生溢出，变成-2147483648



### 评价标准
1. 能清楚理解argc和argv的含义和用法，知道int能表示最大的整数范围
2. 知道argc和argv的含义和用法，但不知道第一个参数是这个程序本身
3. 只是大致知道argc和argv
4. 不知道argc和argv，只知道超过一定范围会溢出变成负数


### 提高
能正确分析出int为什么会发生溢出，溢出后会变成负数

1. 向上溢出的原理（默认int是32位的）：有符号位的Int第一位是符号位，所以其实际上只能存储31个有效位。当他的后31位全部是1的时候，就是int的最大值。
然后如果在加一，就变成了100000000000...（31个0）第一位符号位是1表示负数，然后后31位为0，表示负数的最小值为-2147483648.如果在加一，则数字为-2147483647.

2. 向下溢出的原理：32全部被置为1，但是由于第一位是符号位，所以只有后面31位有效，表示第2147483647小的负数，就是-1.

# 12. 题解

` 解题人：楚梦凡`

```
int main(int argc, char **argv)
{
    int data[2][3] = {{0X636c6557, 0X20656d6f, 0X78206f74},
                      {0X756f7969, 0X6e694c20, 0x00000000}};
    int data2[] = {0X67207875, 0X70756f72, 0X32303220, 0X00000a32};

    char *a = (char *)data;
    char *b = (char *)data2;
    char buf[1024];
    strcpy(buf, a);
    strcat(buf, b);

    printf("%s\n", buf);

    return 0;
}
```

### 知识点

- 大小端
- 强制类型转换

### 答案

Welcome to xiyou Linux group 2022

先创建一个二维数组和一个一维数组，并在里面填入十六进制的数据，这些数据拼接后以字符形式将会输出Welcome to xiyou Linux group 2022，将int **data1指针强转成char *a，int *data2强转成char *b，然后使用strcpy函数将a所指向的区域拷贝到一个缓冲区中，再使用strcat将a和b指向的区域拼接起来。然后将结果输出。

考察了整形在计算机中的存储方式（大小端问题），考察了将int *强转为char * ，考察了将int **转换为char *考察了C语言二维数组的存储方式（按行存储），考察了字符数组是以'\0'结尾，考察了C语言中的两个函数strcpy和strcat。

### 评分标准

A. 答出大小端，并能说出C语言数组在计算机中存储方式

B.成功解释程序的输出

C.理解强制类型转换

D.能讲清楚二维数组为什么要在结尾添加0x00000000

# 13. 题解

`解题人: 楚梦凡`

```c
#define SWAP(a, b, t) t = a; a = b; b = t
#define SQUARE(a) a * a 
#define SWAPWHEN(a, b, t ,cond) if (cond) SWAP(a, b, t)

int main(void) {
  int tmp;
  int x = 1;
  int y = 2;
  int z = 3;
  int w = 3;

  SWAP(x, y, tmp);
  printf("x = %d, y = %d, tmp = %d\n", x, y, tmp);

  if (x > y) SWAP(x, y, tmp);
  printf("x = %d, y = %d, tmp = %d\n", x, y, tmp);

  SWAPWHEN(x, y, tmp, SQUARE(1 + 2 + z++ + ++w) == 100);
  printf("x = %d, y = %d\n", x, y);
  
  printf("z = %d, w = %d, tmp = %d\n", z, w, tmp);

  return 0;
}
```

### 预处理后的代码

```c
int main(void) {
  int tmp;
  int x = 1;
  int y = 2;
  int z = 3;
  int w = 3;

  tmp = x; x = y; y = tmp;
  printf("x = %d, y = %d, tmp = %d\n", x, y, tmp);

  if (x > y) tmp = x; x = y; y = tmp;
  printf("x = %d, y = %d, tmp = %d\n", x, y, tmp);

  if (1 + 2 + z++ + ++w * 1 + 2 + z++ + ++w == 100) tmp = x; x = y; y = tmp;
  printf("x = %d, y = %d\n", x, y);

  printf("z = %d, w = %d, tmp = %d\n", z, w, tmp);

  return 0;
}
```



### 知识点:

  - 宏的使用和理解

### 答案:

```
x = 2, y = 1, tmp = 1
x = 1, y = 2, tmp = 2
x = 2, y = 2
z = 5, w = 5, tmp = 2
```

1. 交换x和y
2. 交换后x大于y，if判断成立，tmp = x;会执行然后执行x = y; y = tmp; 整个执行完相当于交换了x和y
3. 表达式中含有2个z++和++w，z++和++w无法确定是先求值再运算还是先运算再求值，但无论如何==左边的求出来的值一定不等于100，所以if中判断条件不成立:`不执行tmp = x，而执行x = y; 和 y = tmp;`

### 评价标准

A. 能讲清楚（写出）此题的这行代码的展开式：SWAPWHEN(x, y, tmp, SQUARE(1 + 2 + z++ + ++w) == 100);
Daz:
同时解释清楚答案第三行,x = 2,y = 2(if 只和最近的一个匹配)
**试题中最难的一道题了,最好让现场手写展开**

B. 能完完整整的讲清楚此题输出和逻辑

C.宏函数和普通函数的优缺点

D.能讲出宏函数和普通函数的区别

E.预处理做了什么（ 可以问预处理编译链接汇编四个阶段）