---
title: oc中创建类
date: 2018-07-25 10:06:39
tags: [object-c]
---


     @interface Person : NSObject //继承
	 {
       //一定要在大括号中声明类是熟悉（成员变量）
       //命名规则：标识符规则
       //命名规范： 必须以下划线开头，下划线的首字母小写，其他的单词首字母大写

      @public
       char *_name;
       int _age;

     - (void) show;

     }
     @end

     @implementation Person

     - (void) show;
     {
    //对象方法中可以直接访问该对象的成员变量
          NSLog(@"name = %s, age = %d",_name,_age)
     }
 
     @end

OC中类的声明必须以@interface开头，必须以@end结尾
类的实现碧玺以@implementation开头，必须以@end结尾

NSObject: 基类，所有类的祖先类

:NSObject 作用是让Person类具有创建对象的能力 （继承）

注意：如果一个类中只有声明没有实现，那么这个类在链接时就会报错，是不可创建成功.

OC中方法声明的格式
无形参： 方法类型符 （返回值类型） 方法名称
对象方法： 是属于对象的，只能通过对象调用，它的方法类型符是-


    int main(int argc, const char * argv[]){

		/*[类名 new] 作用 通过类创建一个对象
		1.为Person这个对象在堆中分配内存
        2.初始化成员变量
        3.返回指向刚刚创建出来的对象的指针
        */

       Person *p1 = [Person new];
       
       p1->_age = 10;
       p1->_name = "xiaoti";

       NSLog(@"%p,%d",p1,p1->_age);

       [p1 show]; //方法调用

       //NSLog(@"%p,%d",p1,(*p1)._age);

       return 0;
    }

