Title: 如何停止GCD中正在执行的block

Date: 2013-01-11 10:41:59

URL: /2013/01/11/%e5%a6%82%e4%bd%95%e5%81%9c%e6%ad%a2gcd%e4%b8%ad%e6%ad%a3%e5%9c%a8%e6%89%a7%e8%a1%8c%e7%9a%84block/

Tags: iOS

GCD中的suspend和release方法都只能停止队列下一个block的执行，而对于如何停止正在执行的block，GCD似乎没有提供相应的方法。当block中有一个较费时的循环却想随时停止它怎么办？能实现（但不是最佳）的方法是，在block外增加一个判断变量，block中每次循环执行时判断变量的值，若为YES循环才执行，若想终止循环，只需在block外部改变判断变量的值即可。

示例代码如下

BOOL isDoSomething = YES;

dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{

        if(isDoSomething){

               loop{}

        }

});

若需要循环变量停止，只需设置"isDoSomething = NO"即可