1.  extern const value是否是const不确定
    
2.  char* s,相当于const char* s，存储在代码段中，不可按数组方式访问
    
3.  函数后的const含义:- \[ \] 在函数体内不能对类的数据成员做改变- \[ \] 一个const类型的对象只能调用const类型的函数- \[ \] 在const成员函数中，调用其他非const成员函数是非法的  主要原因是:表示成员函数隐含传入的this指针为const指针，决定了在该成员函数中，任意**修改**它所在类的成员的操作都是不允许的(因为隐含了对this指针的const引用)
    
4.  接上面3，非静态成员函数后面要加const(加到非成员函数或静态成员函数后面会产生编译错误)
    
5.  在创建const对象时，要对成员变量做初始化。或者成员变量为const时，在创建对象后要初始化。
    
6.  char(* const)q ,char (const*) q，把*看成**point**然后从**右往左看**。然后第一个就是q const point(q是const point即**指针是不变**的)，第二个就是q point(q是point**指向内容不变**)。即一个是指针**变量**，且指针变量的**内容不可变**，一个是指针**常量**。
    
7.  ,\*q是const，\*q是指针的内容，q是指针，所以指针所指向的内容不变
    
8.  const 变量不能赋给非const指针反之可以，假如赋值给了一个非const指针，意味着一个值拥有两个指针，就可以通过非const指针去更改，就矛盾了。
    
9.  不可对const变量赋值(初始化可以)
    
10. const对象只能调用const函数，非const对象能调用cinst和非const的函数
    
11. 不管形参是const还是非const，它都可接收const和非const