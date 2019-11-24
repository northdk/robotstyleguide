***该文档几目录用于阐述、规范及存储关于工程代码注释风格的相关内容。***

[TOC]

# 1. 概述

### 1.1 为何

我们以终为始，倒推注释的意义。假设工程中存在一份优秀的注释，那么：

##### 1.1.1 维护角度

代码维护氛围需求扩展，bug fix以及局部重构，也可按照人员区分为开发者直接维护和二次开发或FAE（现场技术支持），随着时间的推移，除了代码本身，只有注释可以帮助快速且准确地理解代码的意图。

e.g.

```C++
constexpr int32_t BufferSize = 65536;
constexpr int32_t PollingRate = 100;		///< 该消息订阅自X， X的刷新间隔为10ms；

void foo()
{
  char _buf[BufferSize];
  while(true){
    // do something, like commu with X
    std::this_thread::sleep_for(std::chrono::milliseconds(1 / PollingRate * 1000));
  }
}
```

显然地，我们很容易理解"PolliRate"的含义，但是对于"BufferSize"的设计目的，为何大小选择这样一个数字，是模糊的。那么在迭代中，修改可能带来的问题也就是不确定的。



##### 1.1.2 代码review

严格的工程，少不了代码的review环节，reviewer无论+1还是+2，都需要对代码质量作出快速判断。

在commit message之外，注释就是一份更详尽的讲解。

e.g.

```C++
// old version

/**
* @brief 解析命令，并分发至相应处理函数
* @param data 采用模板实现的待解析内容
* @return 解析是否成功
* @details data中须包含"type"字段，该字段依据协议进行分发
*/
template<typename T>
bool ParseCmd(const T& data)
{
  using namespace rapidjson;
  Document d;
  d.Parse(data);
  if(! d.HasMember("type")){
    fprintf(stderr, "parser throw an error with invalid type!\n"); 
   	return false;
  }
  switch(d["type"].GetInt()){
      // do something
  }
  return true;
}


// new version

/**
* @brief 解析命令，并分发至相应处理函数
* @param data 采用模板实现的待解析内容
* @return 解析是否成功
* @details data中须包含"cmd"字段，该字段依据协议进行分发
* @details data会首先被CheckValid函数检测合法性，具体看参考该函数声明
*/
template<typename T>
bool ParseCmd(const T& data)
{
  if(! CheckValid(data)){
   fprintf(stderr, "parser throw an error with invalid input!\n"); 
   return false;
  }
	
  using namespace rapidjson;
  Document d;
  d.Parse(data);
  if(! d.HasMember("cmd")){
    fprintf(stderr, "parser throw an error with invalid type!\n"); 
   	return false;
  }
  switch(d["cmd"].GetInt()){
      // do something
  }
  return true;
}

```

如上代码，reviewer只需要确认函数内部实现了注释所描述的即可。

##### 1.1.3 合作开发

当存在模块间调用，且由不同的开发人员完成时，注释将会尤其必要。即，产生了上下游关系。

e.g.

```C++
/**
* @brief one method of data output , ensure sequential execution
*
* @param dst the address for the data which will be output
* @param timeout if the datapool is empty; timeout < 0 ,wait forever;
* timeout = n > 0 wait n milliseconds timeout, timeout = 0 return false
* immidiately.default =0
*
* @return success return true , other case return false
*/
bool DeQueue(T* dst, int timeout = 0) __nonnull((2));
```

上述代码是一个封装的消息队列的出队函数，如果没有注释，那么只看头文件的话，"timeout"的理解将是灾难性的。

##### 1.1.4 新人加入

这一点很容易理解，团队人员迭代，由新同事接手老的代码，再详细的交接和讲解，也不如一份好的注释，然后可以在工作中反复阅读。

##### 1.1.5 工作交接

同上。

### 1.2 风格

风格亦是一份约定，旨在保证团队内成员有一个基本一致的习惯。

- 不排斥中文，但是推荐使用简短的英文；
- 只要求外部注释， 内部由developer视具体而自由处理；
- 只要求关键函数， 而非每一个函数均注释；
- 在有更好的工具之前，推荐doxygen风格，详见下文；
- 在表明语义的基础上，我们希望注释尽量客观、平和，不推荐带有感情色彩的词汇及大量的人称词汇，如"I think"， "you maybe" 或者 "So terrible with this shit code to support".

### 1.3 工具

基于linux直接使用， doxygen 1.8及以上。

```shellshe l
 sudo apt-get install doxygen
```

查看注释，则任一浏览器均可，推荐 chrome.



# 2. doxygen指南

在第一节中，注释已经完成了基本使用。该小节主要阐述如果想利用doxygen工具更好地查看注释，要怎么做。

### 2.1 配置

##### 2.1.1 配置文件

doxygen采用一份写好规则的配置文件来生成注释文档，该文档已经预设于工程根目录，文件名为"Doxyfile"，不推荐随意更改。

生成该文档的方法：

```shellshe l
doxygen -s -g $configfilename
```

应用该文档生成注释文档

```shellshe l
doxygen ./$configfilename
```

所生成的文档，位于语法规则中"OUTPUT_DIRECTORY"字段所指向的目录，本工程为"doc/comment/html"目录，该目录在gitignore中已经忽略。

##### 2.1.2 语法规则

同样的，语法规则已经预先写好，如果感兴趣可以参考同级目录下"regulation.md"，这里不再详细说明。



### 2.2 规范

##### 2.2.1 