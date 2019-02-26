# CPP学习会 C++编程规范

（ver.2019.2.26）

CPP学习会遵循本编程规范，以保证代码风格统一，方便多人协作，
适用于多种操作系统和编辑软件。

## 1 格式

### 1.1 余白——缩进

使用空格缩进，每次缩进4个字符。
代码编辑器基本都可以设置将Tab转为空格，请在编码前打开这个设置。
例如，Visual Studio 2015的设置方式为：
	工具 -> 选项 -> 文本编辑器 -> C/C++ -> 制表符 -> 插入空格

### 1.2 余白——间隙

* 运算符两端要各有一个空格。
* 逗号、分号右边有一个空格。
* 单目运算符不要有额外空格。
如：

```C++
for (auto i = 0; i < 100; i++)
{
    printf("%d\n", i);
}
```

### 1.3 指针符号\*，引用符号& 

位置贴近类型名。如：

```C++
ClassName* p = new ClassName();
```

### 1.4 花括号

采用Allman风格，单独占一行。如：

```C++
for (auto i = 0; i < 100; i++)
{
    printf("%d\n", i);
}
```

就算只有一行语句，也强制使用花括号。如：

```C++
if (true)
{
    printf("true");
}
```

### 1.5 长度限制

	每行代码不超过 80 个字符。


## 2 命名

总体上采用驼峰标记法，使用英文单词，不能夹着拼音等其它语言。

### 2.1 类型命名

采用大写驼峰标记法。用名词而非动词，清晰表达类的主要意图。
本条适用于class, struct, typedef, enum。

```C++
ClassName //大写驼峰标记法
```


### 2.2 变量命名

（1）普通变量

名字采用小写的骆驼命名法。

```C++
objectName
```

名字不要加类型前缀。变量名字应该关注用途，而不是它的类型。
如，bool型变量以is开头。

```C++
bool        isEmpty;
const char* name;
Array       teachers;
```

（2）成员变量

访问权限只分成两级，private 和 public，不要用 protected。 

private成员变量，前面加下划线。如：

```C++
class Image
{
public:
    .....

private:
    size_t    _width;
    size_t    _height;
}
```

public成员变量，前面不加下划线。如：

```C++
struct Color4f
{
    float    red;
    float    green;
    float    blue;
    float    alpha;
}
```

（3）静态变量

类中尽量不要出现静态变量，类中的静态变量不用加任何前缀。
源文件中的静态变量统一加s_前缀，并尽可能的详细命名。如：

```C++
static ColorTransformStack s_colorTransformStack;    // 对
static ColorTransformStack s_stack;                  // 错（太简略）
```

（4）全局变量

除非迫不得已，不要使用全局变量。若要使用，加上前缀 g_，并尽可能的详细命名。如：

```C++
Document  g_currentDocument;
```

### 2.3 函数命名

变量名字采用大写的骆驼命名法。（注：这一点有别于参考文献[1]）
防止使用时和变量名混淆，忘记加()导致出错。
函数名称应该是动词或动宾短语，返回bool类型的函数可以是形容词。


### 2.4 命名空间

使用小写加下划线的形式，可以方便跟类型名字区分开来。如：

```C++
lua_wrapper::getField();  // getField是命令空间lua_wrapper的函数
LuaWrapper::getField();   // getField是类型LuaWrapper的静态函数
```

另，头文件不要出现 using namespace 。

### 2.5 宏命名

全部大写，中间加下划线相连接。如：

```C++
#define PI_ROUNDED 3.0
CLOVER_TEST
MAX
MIN
```

```C++
#ifndef __COCOS2D_FLASDK_H__
#define __COCOS2D_FLASDK_H__
....
#endif
```

### 2.6 枚举命名

尽量使用 0x11 风格 enum，如：

```C++
enum class ColorType : uint8_t
{
    Black,
    While,
    Red,
}
```

### 2.7 文件命名

与类名保持一致。

## 3 函数

### 3.1 参数个数

尽可能少，原则上不超过5个。如：求贝塞尔曲线

错误示例：

```C++
void drawQuadBeizer(float startX,   float startY,
                    float controlX, float controlY,
                    float endX,     float endY);

```

正确示例：

```C++
void drawQuadBeizer(const Point& start,
                    const Point& control,
                    const Point& end);
```

### 3.2 参数顺序

传入参数，传出参数。

## 4 其它

### 4.1 不要注释代码，代码不使用就直接删掉


## 参考资料：

本篇主要参考了第一篇参考文献，概要提炼。
个别内容根据个人经验进行了调整和修改。

[1]https://zhuanlan.zhihu.com/p/20326454
[2]http://blog.jobbole.com/64098/
