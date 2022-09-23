- [new创建类对象与不new区别：](#new%E5%88%9B%E5%BB%BA%E7%B1%BB%E5%AF%B9%E8%B1%A1%E4%B8%8E%E4%B8%8Dnew%E5%8C%BA%E5%88%AB)
    - [如何理解第一句话：](#%E5%A6%82%E4%BD%95%E7%90%86%E8%A7%A3%E7%AC%AC%E4%B8%80%E5%8F%A5%E8%AF%9D)
- [new与delete要相对应](#new%E4%B8%8Edelete%E8%A6%81%E7%9B%B8%E5%AF%B9%E5%BA%94)

## new创建类对象与不new区别：

1.  <u>new创建类对象需要指针接收，一处初始化，多处使用</u>
2.  new创建类对象使用完需delete销毁
3.  new创建对象直接使用堆空间，而局部不用new定义类对象则使用栈空间
4.  new对象指针用途广泛，比如作为函数返回值、函数参数等
5.  频繁调用场合并不适合new，就像new申请和释放内存一样

### 如何理解第一句话：

## 定位new与普通new

```c++
classname & sd = new (buffer) classname;//定位new为指针变量开辟缓存空间
classname & sd = new classname;//普通new
```

1.  定位new在创建第二个对象时，会覆盖掉第一个对象的空间，要使用来个不同的存储空间来确保对象空间不重叠。
2.  delete与new配套使用，但不与定位new使用。正确的释放方法如下：```c++
    char *buffer=new char [100];
    classname *pc1;
    pc1=new (buffer) classname;
    pc1->~classname();//显式的调用，不能直接delete pc1;
    ```

`因为delete pc1;也只是释放了上面的buffer，相当于delete buffer;而不是pc1。`

## new与delete要相对应

- 如果在构造函数中使用new来初始化指针成员，则应在析构函数中使用delete
- new和delete必须相互兼容，new对应于delete，new \[\]对应于delete\[\]
- 如果有多个构造函数，则必须以相同的方式使用new，要么都带中括号，要么都不带，因为只有一个析构函数，所有的构造函数都要与它兼容，然而，若new一个指针并初始化为空指针，delete（无论是带中括号还是不带中括号）都可以。