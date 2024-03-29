# C++ coding style

### 1. 综述

​	该文档旨在对软件工程代码的C++部分进行规范层面的约束.

​	若无特殊情况, 则本文中的"要求"部分为必须遵守项, 在必要时, 可以此为据驳回代码提交.

​	文中的另外"建议", 是为了保证风格的统一, 为非必须性条款.

​	**另, 在必要的时间长度下, 本规范应当进行review并修正, 以适配系统架构和开发工作的高效推进.**



### 2. 头文件

​	**要求:**

- 所有头文件要求自给自足

  ```
  用户和重构工具不需要为特别场合而包含额外的头文件.
  例如, 如果提供了日志库,那么只需要下面一条语句:
  #include "log.h"
  即可使用所有的相关API
  ```

- 要有 #define 或者 #program once 保护

  ```C++
  首先, #program once并不能无缝代替 #define, 如果不理解, 慎用.
  
  对于#define保护机制, 禁止以下划线开头, 避免同系统库命名冲突
  要求使用如下方式:
  <PROJECT>_<PATH>_<FILE>_H_
  或
  <PATH>_<FILE>_H_
  e.g.
  #ifdndef PROJECT_TOOLS_LOG_H_
  #define PROJECT_TOOLS_LOG_H_
  #endif // PROJECT_TOOLS_LOG_H_
  ```

- 避免使用前置声明

  ```
  所谓「前置声明」（forward declaration）是类、函数和模板的纯粹声明，没伴随着其定义.
  
  优点是节省编译时间,缺点是以藏了依赖关系, 系统crash风险骤增.
  
  形如:
  Class A;
  
  void Foo(A* pa){};
  
  要求必须写作:
  #include "a.h" //a.h为Class A的定义头文件
  
  void Foo(A* pa)();
  ```

- 头文件引用

  ```c++
  1. 包含顺序, 要求为定义头文件, C系统文件,C++系统文件,外部库头文件,本项目内头文件；
  2. 包含路径, 禁止使用Unix快捷目录, 如 ./ 或 ../../ 等, 要求从工程一级子目录开始按照文件路径包含.
  
  e.g.
  // log.cpp, 用于实现日志库代码
  #inlucde "tools/log/log.h"
  #include <stdio.h> 	// c lib
  #include <mutex> 	// c++ lib
  #include "commen.h" // local head file
  ```


**建议**

- 尽可能使用类型确定的代码方式来替代宏

  ```
  例如,
  使用C++11特性constexpr代替常量宏
  使用内联函数代替宏函数
  使用enum或enum class代替一组关联的宏
  ```

- 超过10行的代码, 不用内联函数

- 在#include中插入空行来分割不同来源的头文件,  是一个好习惯

- 不提倡使用-inl.h来插入文件

  

### 3.  作用域

**要求**

- 本地基础方法库要求放在命名空间内

  ```
  使用命名空间来代替冗长的函数或类的名称
  
  将ArmOSLog()
  写作
  arm::Log()
  ```

  

- 函数变量尽可能置于最小作用域内

  ```c++
  C++ 允许在函数的任何位置声明变量. 我们提倡在尽可能小的作用域中声明变量, 离第一次使用越近越好. 
  
  int i;
  i = f(); // 坏——初始化和声明分离
  
  vector<int> v = {1, 2}; // 好——v 一开始就初始化
  ```

**建议**

- 慎用匿名或者内联命名空间
- 推荐简洁的空间写法,最好不要超过3个字符

  

### 4. 类

**要求**

- 构造函数禁止使用虚函数, 禁止进行可能失败的初始化

  ```
  对于类需要初始化一系列依赖句柄, 如硬件和网络的初始化等
  要求提供Init()方法,并显示地返回结果, 而非在构造函数内进行
  避免返回一个失败的实例指针
  ```

- 禁止进行隐式转换

  ```
  例如, 将一个char或bool返回函数用作int型调用等
  必要时,使用explicit关键字
  所有的转换, 应当显示的使用cast等实现转换
  ```

- 显示处理拷贝和移动构造函数

  ```
  如果类需要被拷贝或移动, 则显示的提供该函数接口
  如果不需要,则显示的禁止它们, 使用delete关键字实现
  如果有更进一步的需求, 例如内部要用到, 则将之设为私有方法
  ```

- 提供API组时, 禁止使用结构体

  ```
  结构体用来定义包含数据的被动式对象
  最多提供一个构造函数
  ```

- 禁止菱形继承

  ```
  如存在A和B, 继而使用C同时继承自A和B
  该行为会导致A和B的重名API混乱
  要求使用 C持有A和B的指针来实现
  ```

  

### 5. 函数

**要求**

- 输入参数在前, 使用引用, 用const限定

- 输出参数在后, 使用指针

  ```
  以上均针对具有复杂内存结构的参数, 简单参数不必如此
  ```

- 存在失败可能的函数, 要求显示返回bool值

  ```
  例如, 消息队列出队操作
  使用
  bool DeQueue(Msg* msg)
  而非
  Msg DeQueue()
  ```

**建议**

- 编写简短的函数
- 调用者多数时不必设置的参数, 使用缺省值
- 重载要简单明确
- 后置返回类型, 尽可能不使用, 除非匿名函数等绕不开的情况

### 6. 命名

**要求**

- 禁止使用缩写, 除非函数内部临时变量或极其通用的名字；

- 文件名全部小写,使用下划线连接

- 类名大写开头, 每个单词首字母均为大写

- 变量名小写, 下划线连接

- 类成员变量使用小写, 下划线连接, 下划线结尾；类方法大写开头, 首字母大写连接;

- 常量使用字母k开头, 如枚举或全局常量;

  ```
  manager_status.cpp	// file
  Class Manager;		// class
  Struct MsgData;		// struct
  int clock_counter;	// variable
  
  Class Manager{
  public:
  	bool is_running_; 
      bool Status(){
      	return is_running_;
      }
  };
  
  enum LogLevel{
  	kInfo = 0,
  	kDebug = 1
  }
  ```

**建议**

- 必要时, 变量后加注释
- 关键的名字,  尽可能通过字面表达明确的含义
- 尽可能结合命名空间使用一系列命名

### 7. C++特性

特指C++11心特性, 本小节均为建议性质内容;

- 用好右值, 如std::move和std::forward
- auto是一个好东西
- constexpr实现了真常量
- C++11 中，任何对象类型都可以被列表初始化。
- 对于指针, 使用nullptr代替NULL

等等;

### 8. 注释

注释部分有另外的文档来详细阐述;

推荐使用doxygen风格;

### 9. 规则特例

任何优秀的规则都会允许特例, 规范是为了提高效率, 而非反过来.

必要时的特别用法, 请使用注释特别注明.



### 10. 参考

[GoogleStyle](https://github.com/google/styleguide)

[译文](https://zh-google-styleguide.readthedocs.io/en/latest/)

[github托管](https://github.com/zh-google-styleguide/zh-google-styleguide)



