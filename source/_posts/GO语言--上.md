---

title: GO语言--上

date: 2022-12-14 18:04:10

description: GO语言基础入门--上

keywords: GO

tags: Go

categories: GO

---

## go语言了解-上

#### 1.Go 语言的基础组成有以下几个部分：

*   包声明
*   引入包
*   函数
*   变量
*   语句 & 表达式
*   注释

```go
package main

import "fmt"

func main() {
	/** 这是我的第一个go程序 */
	fmt.Print("Hello World!!!")
}
```

1\). package main 代表此文件为一个可以单独执行的文件
2\). 第二行的import "fmt" 代表引入一个fmt包，此包可以进行io输入出
3\). 第三行的func main() 通常为单个可执行文件的第一行 有init先执行这个，相当于Java中main方法，init相当于静态初始化

#### 2.GO 语言程序的执行

##### 1). go run hello.go

```go
  2). go build hello.go  ./hello
```

#### 3.语法基础

##### 1). go标记

Go 程序可以由多个标记组成，可以是关键字，标识符，常量，字符串，符号。如以下 GO 语句由 6 个标记组成：

```go
fmt.Println("Hello, World!")

6 个标记是(每行一个)：
1. fmt
2. .
3. Println
4. (
5. "Hello, World!"
6. )
```

##### 2). 行分隔符

每一行为一条语句 不必使用分号分割

##### 3). 注释

注释这个基本上大同小异 //  /\*\* \*/

##### 4). 标识符

也基本上大同小异

##### 5). 字符串连接

使用+连接

##### 6). 关键字

| 关键字      |         关键字 |   关键字  |    关键字    |   关键字  |
| -------- | ----------: | :----: | :-------: | :----: |
| break    |     default |  func  | interface | select |
| case     |       defer |   go   |    map    | struct |
| chan     |        else |  goto  |  package  | switch |
| const    | fallthrough |   if   |   range   |  type  |
| continue |         for | import |   return  |   var  |

##### 7). Go 语言的空格

合理使用空格让代码变得更加优雅哦

##### 8). 格式化字符串

Go 语言中使用 fmt.Sprintf 或 fmt.Printf 格式化字符串并赋值给新串

*   Sprintf 根据格式化参数生成格式化的字符串并返回该字符串。
*   Printf 根据格式化参数生成格式化的字符串并写入标准输出。

```go
    // d%表示整型数字， s%表示字符串
	var fmtNums = 123
	var fmtDate = "2022-12-12"
	var fmtStr = "fmtStr=%d&&date=%s"
	fmtStr = fmt.Sprintf(fmtStr, fmtNums, fmtDate)
	fmt.Println(fmtStr)
```

#### 4. 语言类型

| 序号 |                                                     类型和描述                                                     |
| -- | :-----------------------------------------------------------------------------------------------------------: |
| 1  |                            布尔型布尔型的值只可以是常量 true 或者 false。一个简单的例子：var b bool = true。                            |
| 2  |                        数字类型整型 int 和浮点型float32、float64，Go语言支持整型和浮点型数字，并且支持复数，其中位的运算采用补码。                       |
| 3  |             字符串类型:字符串就是一串固定长度的字符连接起来的字符序列。Go的字符串是由单个字节连接起来的。Go 语言的字符串的字节使用 UTF-8 编码标识 Unicode 文本。             |
| 4  | 派生类型:包括：(a) 指针类型（Pointer）(b) 数组类型(c) 结构化类型(struct)(d) Channel 类型(e) 函数类型(f) 切片类型(g) 接口类型（interface）(h) Map 类型 |

##### 数字类型

| 序号 |                             类型和描述                            |
| -- | :----------------------------------------------------------: |
| 1  |                   uint8无符号 8 位整型 (0 到 255)                   |
| 2  |                 uint16无符号 16 位整型 (0 到 65535)                 |
| 3  |               uint32无符号 32 位整型 (0 到 4294967295)              |
| 4  |          uint64无符号 64 位整型 (0 到 18446744073709551615)         |
| 5  |                  int8有符号 8 位整型 (-128 到 127)                  |
| 6  |               int16有符号 16 位整型 (-32768 到 32767)               |
| 7  |          int32有符号 32 位整型 (-2147483648 到 2147483647)          |
| 8  | int64有符号 64 位整型 (-9223372036854775808 到 9223372036854775807) |

###### 浮点型

| 序号 |           类型和描述          |
| -- | :----------------------: |
| 1  | float32 IEEE-754 32位浮点型数 |
| 2  | float64 IEEE-754 64位浮点型数 |
| 3  |    complex64 32 位实数和虚数   |
| 4  |   complex128 64 位实数和虚数   |

#### 5.GO语言变量

```go
var identifier type    单变量声明  
var identifier1, identifier2 type  多变量声明
```

如果变量已经使用 var 声明过了，再使用 := 声明变量，就产生编译错误，格式：

```go
var intVal int 
intVal :=1 // 这时候会产生编译错误，因为 intVal 已经声明，不需要重新声明
```

```go
intVal := 1 相等于：
var intVal int 
intVal =1 
```

可以将 var f string = "Runoob" 简写为 f := "Runoob"：

```go
实例
package main
import "fmt"
func main() {
    f := "Runoob" // var f string = "Runoob"

    fmt.Println(f)
}
```

多变量声明

```go
//类型相同多个变量, 非全局变量
var vname1, vname2, vname3 type
vname1, vname2, vname3 = v1, v2, v3

var vname1, vname2, vname3 = v1, v2, v3 // 和 python 很像,不需要显示声明类型，自动推断

vname1, vname2, vname3 := v1, v2, v3 // 出现在 := 左侧的变量不应该是已经被声明过的，否则会导致编译错误


// 这种因式分解关键字的写法一般用于声明全局变量
var (
    vname1 v_type1
    vname2 v_type2
)
```

##### 值类型和引用类型

所有像 int、float、bool 和 string 这些基本类型都属于值类型，使用这些类型的变量直接指向存在内存中的值：

当使用等号 = 将一个变量的值赋值给另一个变量时，如：j = i，实际上是在内存中将 i 的值进行了拷贝：

你可以通过 \&i 来获取变量 i 的内存地址，例如：0xf840000040（每次的地址都可能不一样）。

值类型变量的值存储在堆中。

内存地址会根据机器的不同而有所不同，甚至相同的程序在不同的机器上执行后也会有不同的内存地址。因为每台机器可能有不同的存储器布局，并且位置分配也可能不同。

更复杂的数据通常会需要使用多个字，这些数据一般使用引用类型保存。

一个引用类型的变量 r1 存储的是 r1 的值所在的内存地址（数字），或内存地址中第一个字所在的位置。

这个内存地址称之为指针，这个指针实际上也被存在另外的某一个值中。

同一个引用类型的指针指向的多个字可以是在连续的内存地址中（内存布局是连续的），这也是计算效率最高的一种存储形式；也可以将这些字分散存放在内存中，每个字都指示了下一个字所在的内存地址。

当使用赋值语句 r2 = r1 时，只有引用（地址）被复制。

如果 r1 的值被改变了，那么这个值的所有引用都会指向被修改后的内容，在这个例子中，r2 也会受到影响。

##### 简短形式，使用 := 赋值操作符

我们知道可以在变量的初始化时省略变量的类型而由系统自动推断，声明语句写上 var 关键字其实是显得有些多余了，因此我们可以将它们简写为 a := 50 或 b := false。

a 和 b 的类型（int 和 bool）将由编译器自动推断。

这是使用变量的首选形式，但是它只能被用在函数体内，而不可以用于全局变量的声明与赋值。使用操作符 := 可以高效地创建一个新的变量，称之为初始化声明。

###### 注意事项

如果在相同的代码块中，我们不可以再次对于相同名称的变量使用初始化声明，例如：a := 20 就是不被允许的，编译器会提示错误 no new variables on left side of :=，但是 a = 20 是可以的，因为这是给相同的变量赋予一个新的值。

如果你在定义变量 a 之前使用它，则会得到编译错误 undefined: a。

如果你声明了一个局部变量却没有在相同的代码块中使用它，同样会得到编译错误，例如下面这个例子当中的变量 a：

```go
实例
package main

import "fmt"

func main() {
   var a string = "abc"
   fmt.Println("hello, world")
}
```

尝试编译这段代码将得到错误 a declared but not used。

此外，单纯地给 a 赋值也是不够的，这个值必须被使用，所以使用

fmt.Println("hello, world", a)
会移除错误。

但是全局变量是允许声明但不使用的。 同一类型的多个变量可以声明在同一行，如：

var a, b, c int
多变量可以在同一行进行赋值，如：

var a, b int
var c string
a, b, c = 5, 7, "abc"
上面这行假设了变量 a，b 和 c 都已经被声明，否则的话应该这样使用：

a, b, c := 5, 7, "abc"
右边的这些值以相同的顺序赋值给左边的变量，所以 a 的值是 5， b 的值是 7，c 的值是 "abc"。

这被称为 并行 或 同时 赋值。

如果你想要交换两个变量的值，则可以简单地使用 a, b = b, a，两个变量的类型必须是相同。

空白标识符 \_ 也被用于抛弃值，如值 5 在：\_, b = 5, 7 中被抛弃。

\_ 实际上是一个只写变量，你不能得到它的值。这样做是因为 Go 语言中你必须使用所有被声明的变量，但有时你并不需要使用从一个函数得到的所有返回值。

并行赋值也被用于当一个函数返回多个返回值时，比如这里的 val 和错误 err 是通过调用 Func1 函数同时得到：val, err = Func1(var1)。

#### 6. Go 语言常量

定义格式

```go
const identifier [type] = value
```

*   显式类型定义： const b string = "abc"
*   隐式类型定义： const b = "abc"

常量还可以用作枚举：

```go
const (
    Unknown = 0
    Female = 1
    Male = 2
)
```

常量可以用len(), cap(), unsafe.Sizeof()函数计算表达式的值。常量表达式中，函数必须是内置函数，否则编译不过

```go
package main

import "unsafe"
const (
    a = "abc"
    b = len(a)
    c = unsafe.Sizeof(a)
)

func main(){
    println(a, b, c)
}
```

###### iota 用法

```go
实例
package main

import "fmt"

func main() {
    const (
            a = iota   //0
            b          //1
            c          //2
            d = "ha"   //独立值，iota += 1
            e          //"ha"   iota += 1
            f = 100    //iota +=1
            g          //100  iota +=1
            h = iota   //7,恢复计数
            i          //8
    )
    fmt.Println(a,b,c,d,e,f,g,h,i)
}

以上实例运行结果为：

0 1 2 ha ha 100 100 7 8
```

再看个有趣的的 iota 实例：

```go
实例
package main

import "fmt"
const (
    i=1<<iota
    j=3<<iota
    k
    l
)

func main() {
    fmt.Println("i=",i)
    fmt.Println("j=",j)
    fmt.Println("k=",k)
    fmt.Println("l=",l)
}
以上实例运行结果为：

i= 1
j= 6
k= 12
l= 24
```

iota 表示从 0 开始自动加 1，所以 i=1<<0, j=3<<1（<< 表示左移的意思），即：i=1, j=6，这没问题，关键在 k 和 l，从输出结果看 k=3<<2，l=3<<3。

简单表述:

i=1：左移 0 位，不变仍为 1。
j=3：左移 1 位，变为二进制 110，即 6。
k=3：左移 2 位，变为二进制 1100，即 12。
l=3：左移 3 位，变为二进制 11000，即 24。
注：<\<n==\*(2^n)。

#### 7. Go语言运算符

算术运算符  关系运算符  逻辑运算符 基本一致不过多赘诉

###### 位运算符

| 运算符 |                                           描述                                          | 实例                              |
| --- | :-----------------------------------------------------------------------------------: | ------------------------------- |
| &   |                         按位与运算符"&"是双目运算符。 其功能是参与运算的两数各对应的二进位相与。                        | (A & B) 结果为 12, 二进制为 0000 1100  |
| \|  |                         按位或运算符"\|"是双目运算符。 其功能是参与运算的两数各对应的二进位相或                        | (A \| B) 结果为 61, 二进制为 0011 1101 |
| ^   |               按位异或运算符"^"是双目运算符。 其功能是参与运算的两数各对应的二进位相异或，当两对应的二进位相异时，结果为1。               | (A ^ B) 结果为 49, 二进制为 0011 0001  |
| <<  | 左移运算符"<<"是双目运算符。左移n位就是乘以2的n次方。 其功能把"<<"左边的运算数的各二进位全部左移若干位，由"<<"右边的数指定移动的位数，高位丢弃，低位补0。 | A << 2 结果为 240 ，二进制为 1111 0000  |
| >>  |      右移运算符">>"是双目运算符。右移n位就是除以2的n次方。 其功能是把">>"左边的运算数的各二进位全部右移若干位，">>"右边的数指定移动的位数。      | A >> 2 结果为 15 ，二进制为 0000 1111   |

```go
实例
package main

import "fmt"

func main() {

   var a uint = 60      /* 60 = 0011 1100 */  
   var b uint = 13      /* 13 = 0000 1101 */
   var c uint = 0          

   c = a & b       /* 12 = 0000 1100 */
   fmt.Printf("第一行 - c 的值为 %d\n", c )

   c = a | b       /* 61 = 0011 1101 */
   fmt.Printf("第二行 - c 的值为 %d\n", c )

   c = a ^ b       /* 49 = 0011 0001 */
   fmt.Printf("第三行 - c 的值为 %d\n", c )

   c = a << 2     /* 240 = 1111 0000 */
   fmt.Printf("第四行 - c 的值为 %d\n", c )

   c = a >> 2     /* 15 = 0000 1111 */
   fmt.Printf("第五行 - c 的值为 %d\n", c )
}
以上实例运行结果：

第一行 - c 的值为 12
第二行 - c 的值为 61
第三行 - c 的值为 49
第四行 - c 的值为 240
第五行 - c 的值为 15
```

###### 赋值运算符

| 运算符 |            描述           |               实例              |
| :-: | :---------------------: | :---------------------------: |
|  =  | 简单的赋值运算符，将一个表达式的值赋给一个左值 | C = A + B 将 A + B  表达式结果赋值给 C |
|  += |          相加后再赋值         |      C += A 等于 C = C + A      |
|  -= |          相减后再赋值         |      C -= A 等于 C = C - A      |
| \*= |          相乘后再赋值         |     C \*= A 等于 C = C \* A     |
|  /= |          相除后再赋值         |      C /= A 等于 C = C / A      |
|  %= |          求余后再赋值         |      C %= A 等于 C = C % A      |
| <<= |          左移后赋值          |     C <<= 2 等于 C = C << 2     |
| >>= |          右移后赋值          |     C >>= 2 等于 C = C >> 2     |
|  &= |          按位与后赋值         |      C &= 2 等于 C = C & 2      |
|  ^= |         按位异或后赋值         |      C ^= 2 等于 C = C ^ 2      |
| \|= |          按位或后赋值         |     C \|= 2 等于 C = C \| 2     |

```go
实例
package main

import "fmt"

func main() {
   var a int = 21
   var c int

   c =  a
   fmt.Printf("第 1 行 - =  运算符实例，c 值为 = %d\n", c )

   c +=  a
   fmt.Printf("第 2 行 - += 运算符实例，c 值为 = %d\n", c )

   c -=  a
   fmt.Printf("第 3 行 - -= 运算符实例，c 值为 = %d\n", c )

   c *=  a
   fmt.Printf("第 4 行 - *= 运算符实例，c 值为 = %d\n", c )

   c /=  a
   fmt.Printf("第 5 行 - /= 运算符实例，c 值为 = %d\n", c )

   c  = 200;

   c <<=  2
   fmt.Printf("第 6行  - <<= 运算符实例，c 值为 = %d\n", c )

   c >>=  2
   fmt.Printf("第 7 行 - >>= 运算符实例，c 值为 = %d\n", c )

   c &=  2
   fmt.Printf("第 8 行 - &= 运算符实例，c 值为 = %d\n", c )

   c ^=  2
   fmt.Printf("第 9 行 - ^= 运算符实例，c 值为 = %d\n", c )

   c |=  2
   fmt.Printf("第 10 行 - |= 运算符实例，c 值为 = %d\n", c )

}
以上实例运行结果：

第 1 行 - =  运算符实例，c 值为 = 21
第 2 行 - += 运算符实例，c 值为 = 42
第 3 行 - -= 运算符实例，c 值为 = 21
第 4 行 - *= 运算符实例，c 值为 = 441
第 5 行 - /= 运算符实例，c 值为 = 21
第 6行  - <<= 运算符实例，c 值为 = 800
第 7 行 - >>= 运算符实例，c 值为 = 200
第 8 行 - &= 运算符实例，c 值为 = 0
第 9 行 - ^= 运算符实例，c 值为 = 2
第 10 行 - |= 运算符实例，c 值为 = 2
```

###### 其他运算符

| 运算符 |    描述    |        实例        |
| :-: | :------: | :--------------: |
|  &  | 返回变量存储地址 | \&a; 将给出变量的实际地址。 |
|  \* |   指针变量。  |   \*a; 是一个指针变量   |

```go
实例
package main

import "fmt"

func main() {
   var a int = 4
   var b int32
   var c float32
   var ptr *int

   /* 运算符实例 */
   fmt.Printf("第 1 行 - a 变量类型为 = %T\n", a );
   fmt.Printf("第 2 行 - b 变量类型为 = %T\n", b );
   fmt.Printf("第 3 行 - c 变量类型为 = %T\n", c );

   /*  & 和 * 运算符实例 */
   ptr = &a     /* 'ptr' 包含了 'a' 变量的地址 */
   fmt.Printf("a 的值为  %d\n", a);
   fmt.Printf("*ptr 为 %d\n", *ptr);
}
以上实例运行结果：

第 1 行 - a 变量类型为 = int
第 2 行 - b 变量类型为 = int32
第 3 行 - c 变量类型为 = float32
a 的值为  4
*ptr 为 4
```

###### 运算符优先级

| 优先级 |        运算符        |
| :-: | :---------------: |
|  5  | \* / % << >> & &^ |
|  4  |      + - \| ^     |
|  3  |  == != < <= > >=  |
|  2  |         &&        |
|  1  |        \|\|       |

#### 8. Go 语言条件语句

和其他语言的条件控制基本一致，讲讲不一致的
1.Switch 的fallthrough
使用 fallthrough 会强制执行后面的 case 语句，fallthrough 不会判断下一条 case 的表达式结果是否为 true。

```go
func main() {

    switch {
    case false:
            fmt.Println("1、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("2、case 条件语句为 true")
            fallthrough
    case false:
            fmt.Println("3、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("4、case 条件语句为 true")
    case false:
            fmt.Println("5、case 条件语句为 false")
            fallthrough
    default:
            fmt.Println("6、默认 case")
    }
}
结果：
2、case 条件语句为 true
3、case 条件语句为 false
4、case 条件语句为 true
```

1.  select 语句
    select 是 Go 中的一个控制结构，类似于用于通信的 switch 语句。每个 case 必须是一个通信操作，要么是发送要么是接收。
    select 随机执行一个可运行的 case。如果没有 case 可运行，它将阻塞，直到有 case 可运行。一个默认的子句应该总是可运行的。

```go
select {
    case communication clause  :
       statement(s);      
    case communication clause  :
       statement(s);
    /* 你可以定义任意数量的 case */
    default : /* 可选 */
       statement(s);
}
```

*   每个 case 都必须是一个通信
*   所有 channel 表达式都会被求值
*   所有被发送的表达式都会被求值
*   如果任意某个通信可以进行，它就执行，其他被忽略。
*   如果有多个 case 都可以运行，Select 会随机公平地选出一个执行。其他不会执行。
    否则：
    *   如果有 default 子句，则执行该语句。
    *   如果没有 default 子句，select 将阻塞，直到某个通信可以运行；Go 不会重新对 channel 或值进行求值。

```go
实例
package main

import "fmt"

func main() {
   var c1, c2, c3 chan int
   var i1, i2 int
   select {
      case i1 = <-c1:
         fmt.Printf("received ", i1, " from c1\n")
      case c2 <- i2:
         fmt.Printf("sent ", i2, " to c2\n")
      case i3, ok := (<-c3):  // same as: i3, ok := <-c3
         if ok {
            fmt.Printf("received ", i3, " from c3\n")
         } else {
            fmt.Printf("c3 is closed\n")
         }
      default:
         fmt.Printf("no communication\n")
   }    
}
以上代码执行结果为：

no communication
```

#### 9. Go 语言循环语句

###### 1.for

和 C 语言的 for 一样：

```go
for init; condition; post { }
```

和 C 的 while 一样：

```go
for condition { }
```

和 C 的 for(;;) 一样：

```go
for { }
```

*   init： 一般为赋值表达式，给控制变量赋初值；
*   condition： 关系表达式或逻辑表达式，循环控制条件；
*   post： 一般为赋值表达式，给控制变量增量或减量。

for语句执行过程如下：

1、先对表达式 1 赋初值；

2、判别赋值表达式 init 是否满足给定条件，若其值为真，满足循环条件，则执行循环体内语句，然后执行 post，进入第二次循环，再判别 condition；否则判断 condition 的值为假，不满足条件，就终止for循环，执行循环体外语句。

for 循环的 range 格式可以对 slice、map、数组、字符串等进行迭代循环。格式如下：

```go
for key, value := range oldMap {
    newMap[key] = value
}
```

以上代码中的 key 和 value 是可以省略。

如果只想读取 key，格式如下：

```go
for key := range oldMap
或者这样：

for key, _ := range oldMap

如果只想读取 value，格式如下：

for _, value := range oldMap
```

计算 1 到 10 的数字之和：

实例

```go
package main

import "fmt"

func main() {
   sum := 0
      for i := 0; i <= 10; i++ {
         sum += i
      }
   fmt.Println(sum)
}
输出结果为：

55
```

init 和 post 参数是可选的，我们可以直接省略它，类似 While 语句。

以下实例在 sum 小于 10 的时候计算 sum 自相加后的值：

实例

```go
package main

import "fmt"

func main() {
   sum := 1
   for ; sum <= 10; {
      sum += sum
   }
   fmt.Println(sum)

   // 这样写也可以，更像 While 语句形式
   for sum <= 10{
      sum += sum
   }
   fmt.Println(sum)
}
输出结果为：

16
16
```

无限循环:

```go
实例
package main

import "fmt"

func main() {
   sum := 0
   for {
      sum++ // 无限循环下去
   }
   fmt.Println(sum) // 无法输出
}
```

For-each range 循环

```go
这种格式的循环可以对字符串、数组、切片等进行迭代输出元素。

实例
package main
import "fmt"

func main() {
   strings := []string{"google", "runoob"}
   for i, s := range strings {
      fmt.Println(i, s)
   }


   numbers := [6]int{1, 2, 3, 5}
   for i,x:= range numbers {
      fmt.Printf("第 %d 位 x 的值 = %d\n", i,x)
   }  
}
以上实例运行输出结果为:

0 google
1 runoob
第 0 位 x 的值 = 1
第 1 位 x 的值 = 2
第 2 位 x 的值 = 3
第 3 位 x 的值 = 5
第 4 位 x 的值 = 0
第 5 位 x 的值 = 0
```

for 循环的 range 格式可以省略 key 和 value，如下实例：

```go
实例
package main
import "fmt"

func main() {
    map1 := make(map[int]float32)
    map1[1] = 1.0
    map1[2] = 2.0
    map1[3] = 3.0
    map1[4] = 4.0
   
    // 读取 key 和 value
    for key, value := range map1 {
      fmt.Printf("key is: %d - value is: %f\n", key, value)
    }

    // 读取 key
    for key := range map1 {
      fmt.Printf("key is: %d\n", key)
    }

    // 读取 value
    for _, value := range map1 {
      fmt.Printf("value is: %f\n", value)
    }
}
以上实例运行输出结果为:

key is: 4 - value is: 4.000000
key is: 1 - value is: 1.000000
key is: 2 - value is: 2.000000
key is: 3 - value is: 3.000000
key is: 1
key is: 2
key is: 3
key is: 4
value is: 1.000000
value is: 2.000000
value is: 3.000000
value is: 4.000000
```

###### 嵌套循环

语法
以下为 Go 语言嵌套循环的格式：

```go
for [condition |  ( init; condition; increment ) | Range]
{
   for [condition |  ( init; condition; increment ) | Range]
   {
      statement(s);
   }
   statement(s);
}
```

实例

```go
以下实例使用循环嵌套来输出 2 到 100 间的素数：

实例
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var i, j int

   for i=2; i < 100; i++ {
      for j=2; j <= (i/j); j++ {
         if(i%j==0) {
            break; // 如果发现因子，则不是素数
         }
      }
      if(j > (i/j)) {
         fmt.Printf("%d  是素数\n", i);
      }
   }  
}
以上实例运行输出结果为:

2  是素数
3  是素数
5  是素数
7  是素数
11  是素数
13  是素数
17  是素数
19  是素数
23  是素数
29  是素数
31  是素数
37  是素数
41  是素数
43  是素数
47  是素数
53  是素数
59  是素数
61  是素数
67  是素数
71  是素数
73  是素数
79  是素数
83  是素数
89  是素数
97  是素数
```

###### 循环控制语句

1.break

*   用于循环语句中跳出循环，并开始执行循环之后的语句。
*   break 在 switch（开关语句）中在执行一条 case 后跳出语句的作用。
*   在多重循环中，可以用标号 label 标出想 break 的循环。

```go
 // 不使用标记
   fmt.Println("---- break ----")
   for i := 1; i <= 3; i++ {
      fmt.Printf("i: %d\n", i)
      for i2 := 11; i2 <= 13; i2++ {
         fmt.Printf("i2: %d\n", i2)
         break
      }
   }

   // 使用标记
   fmt.Println("---- break label ----")
   re:
      for i := 1; i <= 3; i++ {
         fmt.Printf("i: %d\n", i)
         for i2 := 11; i2 <= 13; i2++ {
         fmt.Printf("i2: %d\n", i2)
         break re
      }
   }
```

2.continue

*   和break类似 相比Java也有标记label

3.goto
Go 语言的 goto 语句可以无条件地转移到过程中指定的行。

goto 语句通常与条件语句配合使用。可用来实现条件转移， 构成循环，跳出循环体等功能。

但是，在结构化程序设计中一般不主张使用 goto 语句， 以免造成程序流程的混乱，使理解和调试程序都产生困难。
语法
goto 语法格式如下：

```go
goto label;
..
.
label: statement;
```

实例

```go
package main

import "fmt"

func main() {
   /* 定义局部变量 */
   var a int = 10

   /* 循环 */
   LOOP: for a < 20 {
      if a == 15 {
         /* 跳过迭代 */
         a = a + 1
         goto LOOP
      }
      fmt.Printf("a的值为 : %d\n", a)
      a++    
   }  
}
以上实例执行结果为：

a的值为 : 10
a的值为 : 11
a的值为 : 12
a的值为 : 13
a的值为 : 14
a的值为 : 16
a的值为 : 17
a的值为 : 18
a的值为 : 19
```

###### 无限循环

如果循环中条件语句永远不为 false 则会进行无限循环，我们可以通过 for 循环语句中只设置一个条件表达式来执行无限循环：

实例

```go
package main

import "fmt"

func main() {
    for true  {
        fmt.Printf("这是无限循环。\n");
    }
}
```

#### 10. Go 语言函数
###### 函数定义
Go 语言函数定义格式如下：
```go
func function_name( [parameter list] ) [return_types] {
   函数体
}
```
**函数定义解析**：

* func：函数由 func 开始声明
* function_name：函数名称，参数列表和返回值类型构成了函数签名。
* parameter list：参数列表，参数就像一个占位符，当函数被调用时，你可以将值传递给参数，这个值被称为实际参数。参数列表指定的是参数类型、顺序、及参数个数。参数是可选的，也就是说函数也可以不包含参数。
* return_types：返回类型，函数返回一列值。return_types 是该列值的数据类型。有些功能不需要返回值，这种情况下 return_types 不是必须的。
函数体：函数定义的代码集合。

**实例**
以下实例为 max() 函数的代码，该函数传入两个整型参数 num1 和 num2，并返回这两个参数的最大值：

```go
/* 函数返回两个数的最大值 */
func max(num1, num2 int) int {
   /* 声明局部变量 */
   var result int

   if (num1 > num2) {
      result = num1
   } else {
      result = num2
   }
   return result
}
```

**函数多个返回值**
```go
实例
package main

import "fmt"

func swap(x, y string) (string, string) {
   return y, x
}

func main() {
   a, b := swap("Google", "Runoob")
   fmt.Println(a, b)
}
```
**函数参数**
|传递类型|	描述|
|:---:|:---:|
|值传递	|值传递是指在调用函数时将实际参数复制一份传递到函数中，这样在函数中如果对参数进行修改，将不会影响到实际参数。|
|引用传递	|引用传递是指在调用函数时将实际参数的地址传递到函数中，那么在函数中对参数所进行的修改，将影响到实际参数。|

**Go 语言函数闭包**
```go
package main

import "fmt"

func getSequence() func() int {
   i:=0
   return func() int {
      i+=1
     return i  
   }
}

func main(){
   /* nextNumber 为一个函数，函数 i 为 0 */
   nextNumber := getSequence()  

   /* 调用 nextNumber 函数，i 变量自增 1 并返回 */
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
   
   /* 创建新的函数 nextNumber1，并查看结果 */
   nextNumber1 := getSequence()  
   fmt.Println(nextNumber1())
   fmt.Println(nextNumber1())
}
执行结果：
1
2
3
1
2
```
