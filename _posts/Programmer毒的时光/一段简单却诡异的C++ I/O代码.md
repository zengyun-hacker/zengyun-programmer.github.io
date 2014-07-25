Title: 一段简单却诡异的C++ I/O代码

Date: 2011-05-15 00:24:17

URL: /2011/05/15/%e4%b8%80%e6%ae%b5%e7%ae%80%e5%8d%95%e5%8d%b4%e8%af%a1%e5%bc%82%e7%9a%84c-io%e4%bb%a3%e7%a0%81/

Tags: C++ , I/O

C++ primer上的一段代码

主函数为

`

int number;

while(cin&gt;&gt;number, !cin.eof())

{

if(cin.bad())

{

cerr&lt;&lt;"system cin error"&lt;&lt;endl;

}

else if(cin.fail())

{

cerr&lt;&lt;"bad data, try again"&lt;&lt;endl;

cin.clear(istream::failbit);

continue;

}

}

`

在输入字符后，本应该只提示一句“bad data, try again”，接着继续输入。但是运行结果却是一个不断输出“bad data, try again”的死循环。

于是代码修改如下

`

int number;

while(cin&gt;&gt;number, !cin.eof())

{

if(cin.bad())

{

cerr&lt;&lt;"system cin error"&lt;&lt;endl;

}

else if(cin.fail())

{

cerr&lt;&lt;"bad data, try again"&lt;&lt;endl;

cin.clear(istream::failbit);

if(cin.fail())

{

cerr&lt;&lt;"still fail..."&lt;&lt;endl;

}

else

{

cout&lt;&lt;"not fail now"&lt;&lt;endl;

}

continue;

}

}

`

程序依然死循环，不过会输出“still fail...”，是failbit标志没有设置成功。

于是程序再次修改如下

`

int number;

while(cin&gt;&gt;number, !cin.eof())

{

if(cin.bad())

{

cerr&lt;&lt;"system cin error"&lt;&lt;endl;

}

else if(cin.fail())

{

cerr&lt;&lt;"bad data, try again"&lt;&lt;endl;

cin.clear();

if(cin.fail())

{

cerr&lt;&lt;"still fail..."&lt;&lt;endl;

}

else

{

cout&lt;&lt;"not fail now"&lt;&lt;endl;

}

continue;

}

}

`

这次还是死循环，只输出"bad data, try again"，看来clear()成功了。

代码再再修改如下

`

int number;`

` `

` if (cin.good())

{

cout &lt;&gt;number,!cin.eof())

{

if (cin.bad())

{

cerr &lt;&lt; "system cin error\n";

break;

}

if (cin.fail())

{

cerr &lt;&lt; "bad data, try again\n";

//cin.clear(istream::failbit);

cin.clear();

if (cin.fail())

{

cout &lt;&lt; "still fail...\n";

}

else

{

cout &lt;&lt; "not fail now...\n";

}

if (cin.good())

{

cout &lt;&gt; str;

cout &lt;&lt; "cin get something not number:" &lt;&lt; str &lt;&lt; endl;

continue;

}

}

`

终于不再死循环，且"cin get something not number:"会输出。看来原因找到了，正常来说cin只会读入一次，在这里却会被连续读入并且造成死循环。这是什么原因呢？不管怎么说，这是一段很诡异的代码。