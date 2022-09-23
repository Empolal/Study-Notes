cin
程序的输入都建有一个缓冲区，即输入缓冲区。一次输入过程是这样的，当一次键盘输入结束时会将输入的数据存入输入缓冲区，而cin函数直接从输入缓冲区中取数据。
正因为cin函数是直接从缓冲区取数据的，所以有时候当缓冲区中有残留数据时，cin函数会直接取得这些残留数据而不会请求键盘输入。

输入结束条件：space,tab,ENTER
char str[20],str1[20];
    cin>>str;
    cin>>str1;
    cout<<str;
    cout<<str1;
    system("pause");
    return 0;
当str输入qwer（两个空格）asdf
输出qwerasdf(中间没空格）

由此可见:    cin输入遇到结束符停止，并且求其丢弃空格。缓冲区有残留数据时，读入操作直接从缓冲区中取数据。

cin.get