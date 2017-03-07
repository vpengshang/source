---
title: c++ vector容器
date: 2017-07-6 16:02:07
tags: 学习 C++ vector
---
## c++容器vetor详细用法
* vetor是c++STL中部分类容，可以自动扩展容量的数组，以循序(Sequential)的方式维护变量集合。  vector以模板(泛型)方式实现，可以保存任意类型的变量
* vector 类别是以==容器（Container）== 模式为基准设计的，也就是说，基本上它有 begin()，end()，size()，max_size()，empty() 以及 swap() 这几个方法
<!-- more -->
* 访问元素的方法
> 1.vec[i] 访问在索引值为i的元素  
2.vec.front(),传回第一元素的引用  
3.vec.back() 传回末尾元素的引用
* 增加或删除数据
> vec.push_back() 在尾端添加元素  
vec.pop_back() 删除尾端的元素  
vec.erase() - 删除 vector 中一个或多个元素  
vec.insert() 插入一个或多个元素在任意位置
vec.clear() 清空所用数据
* 获取vector的长度或容量
> vec.size() 返回元素的个数  
vec.empty()  为空返回true
* 迭代
> vec.begin() 传一个Iterator，它指向 vector 第一个元素  
vec.end() .end() - 回传一个Iterator，它指向 vector 最尾端元素的下一个位置 

* **具体使用方法**  
1.导入#include<vector>  
2.声明： std::vector<T> v  T为数据类型 V为vetor变量名
3.迭代器：iterator  
vector<int>::interator it=v.begin();