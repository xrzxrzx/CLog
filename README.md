# CLog 简介
这是一个轻量级的C语言日志输出库，包含了四种输出方式：
* 预设输出
* 信息输出
* 警告输出
* 错误输出

且能够使用格式化字符串。
> 因为输出有改变字体颜色的需求，所以我用了windows.h库，所以不支持Windows以外的系统

# CLog使用方法
CLog的使用非常简单，首先肯定是要包含头文件的，还要再调用`init_Log()`函数初始化一下：
```C
#include"Log.h"
int main(void)
{
    init_Log();
    return 0;
}
```
在CLog库中，一共包含了八个日志输出函数，分别是四种输出方式的简单输出和全面输出。<br>
但为了方便全面输出的使用，还定义了四个宏，这样就不必在调用全面输出函数时手动带入大量参数了。所以基本上只会用到这八个函数（宏）：
```C
//预设输出
logPreset();
logPresetAll();
//信息输出
logInfo();
logIngoAll();
//警告输出
logWarn();
logWarnAll();
//错误输出
logErr();
logErrAll();
```
使用的时候，除了预设输出是代入预设的日志类型（enum类型），其余的输出函数（宏）直接带入格式化字符串即可。如下：
```C
logPreset(NULLException);
logInfo("test");
logErr("错误 code: %d", -1);
logWarnAll("有问题%s", "。。。");
```
输出如下：
```
2022-10-20 0:4:47 <WARNING> The pointer is null     //这行是黄色
2022-10-19 23:55:19 <INFO> test                     //这行是蓝色
2022-10-19 23:55:19 <ERROR> 错误 code: -1           //这行是红色
2022-10-19 23:55:19 <WARNING> 有问题。。。          //这行及以下是黄色
function: main
path: E:\tester\main.c
line: 11
```
输出会默认包含年月日和时间，且会自动创建log和temp文件夹（在temp文件夹中会创建一些临时文件并会马上删除），并会将所有日志写入到log文件夹中。<br>
简单输出只包含了日期、时间、日志类型和日志信息，而全面输出还包含了调用该日志函数的函数名，代码行和文件路径（绝对路径）。<br>
当然，你如果有需求，也可以直接在Log.h文件中声明自己的预设级相关信息。
