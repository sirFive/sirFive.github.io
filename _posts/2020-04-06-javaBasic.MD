---
layout: post
title: "Java 基础"
date: 2020-04-06
description: "复习--Java基础"
tag: 复习
---
### 1.java的九种基本数据类型和它们的封装类
```
基本类型  大小(字节)  默认值          封装类
byte        1       (byte)0       Byte
short       2       (short)0      Short
int         4       0             Integer
long        8       0L            Long
float       4       0.0f          Float
double      8       0.0d          Double
boolean     -       false         Boolean
char        2       \u0000(null)  Character
void        -       -             Void
```
### 2.equals和==的区别
```
通俗来说：==是看左右是不是同一个东西，equals是看看左右是不是长的一样。
==等于   equals相同
专业来说：
Java中的数据类型可以分为两类：基本数据类型和复合数据类型。
基本数据类型：byte,short,,char,int,long,float,double,boolean
它们之间的比较使用==，比较的是它们的值是否相等。
复合数据类型：当它们用==进行比较的时候比较的是它们在内存中存放的地址。所以除非new出来的是同一个对象，
	否则结果都为false。Java中所有的类都继承于Object类，该类中有方法equals，这个方法最开始比较的也是对象的内存地址，
	但有些类会重写该方法，因此有些不是比较内存地址。因此对于复合数据类型的比较，
	如果该类没有重写equals方法，那么equals和==的比较结果是相同的。
总结来说：基本数据类型的比较用==，字符串和对象的比较用equals
```
### 3.hashCode()方法
```
hashcode()方法和euqals()方法一样都是比较两个对象是否相等。存在hashCode()方法的原因：
	euqals()方法比较复杂效率低，而hashCode()方法只要生成一个hashCode值可以进行比较了，
	但问题是hashCode值相等的对象他们并不一定相等，因此要加上equals进行比较。
	因此结论是：hashCode值相同对象不一定相等，但是对象相等hashCode值则相同。
应用：每当需要对比的时候，首先用hashCode()去对比，如果hashCode()不一样，
则表示这两个对象肯定不相等（也就是不必再用equal()去再对比了）,如果hashCode()相同，
此时再对比他们的equal()，如果equal()也相同，则表示这两个对象是真的相同了，
这样既能大大提高了效率也保证了对比的绝对正确性。
```
### 4.string,stringBuffer,stringBuilder的区别
```
String: 字符串常量(final修饰，不可被继承)
StringBuffer:字符串变量（线程安全）
StringBuilder:字符串变量（非线程安全）
简单来说String和StringBuffer的主要区别在于string是不可变的对象，
	因此每次对string进行操作都会新建一个新的对象如String s1=”aa”,String s2=”bb” String s3=a+b。
	这里就新建了3个变量（注意String s4=”aa”+”bb”+”cc”只是一个变量，因为他会默认识别成String s4=”aabbcc”）。
	但是StringBuffer和StringBuilder每次都是只对一个对象进行操作。
StringBuilder sb = new StringBuilder(“This is only a”).append(“ simple”).append(“ test”);
因此在字符串常量经常改变的情况下推荐用stringBuffer或stringBuilder(非线程安全首选)
```
### 5.hashMap和hashTable的区别
```
Public class hashTable extends dictonary implments map,cloneable,serializable{}
Public class hashMap extends AbstractMap implments map,cloneable,serializable{}
hashMap非线程安全，hashTable线程安全。
HashMap的key和value允许NULL,hashTable的key和value允不允许NULL
hashTable的contains方法在hashMap中替换成了containsValue和containsKey

```
### 6.collection和map
```
collection分为list接口和set接口
List接口是有序的collection，使用该接口能精确的判断每个元素的位置，允许重复值。
List接口包括arrayList,linkedList，vector，stack
ArrayList：数组大小可变，因为每一个ArrayList实例都有一个容量来存储对象，并且这个容量可以随着元素的增加而变化，
	但无法计算它的变化大小。如果插入大量的数据可以通过ensureCapacity来增加容量而保证插入的效率
LinkedList:它可以从中间插入和删除，这个效率比ArrayList快，但是查询没有ArrayList快。
Vector：vector和ArrayList类似，但是vector是同步的，而ArrayList不是同步的。
Stack：继承自vector，但是他是后进先出的栈。
Queue是一个先进先出的队列。
Set接口是继承自collection的，它不能包含重复的元素。实现的类有hashset，linkedHshSet，treeSet。
HashSet:不保证排序；允许NULL，但只能一个；非同步。
LinkedHashSet:
TreeSet是sortedSet的接口的唯一实现类，可以保证元素的排序。

Map包括：hashMap,hashTable,sortedMap,treeMap.

```
### 7.java面向对象的三个特征和含义
```
封装、继承、多态
封装：将对象的状态信息尽可能的隐藏在对象内部，只保留有限的接口和方法与外部进行交互，从而避免了外界对内部属性的破坏。
	通过访问控制符实现：default同包可见（子孙类不可见）、Private同类可见、
	protected同包可见、public所有类可见
继承：通过继承创建分层次的类，可理解为一个类从另一个类获取属性的方法。通过extends和implements实现
多态:同一个类中的同一个方法有不同的表现形式。
```
### 8.Object公用的方法
```
1.getclass()  final方法，获得运行时类型
2.toString()方法，返回该对象字符串
3.equals()方法，比较
4.clone()方法，创建并返回该对象的一个副本
5.finalize()方法，用于垃圾回收时调用
6.hashCode()方法，用于hash查找
7.wait()方法，使当前线程等待该对象的锁（会一直等待直到获得锁或者被中断）
8.notify()方法，该方法唤醒在该对象上等待的某个线程
9.notifyAll()方法，该方法唤醒该对象上等待的所有线程
```
### 9.List
#### 1.数组和 List 之间的转换
```
List转换成为数组：调用ArrayList的toArray方法。
数组转换成为List：调用Arrays的asList方法。
```
#### 2.ArrayList 和 Vector 的区别
```
Vector是同步的，而ArrayList不是。然而，如果你寻求在迭代的
    时候对列表进行改变，你应该使用CopyOnWriteArrayList。
ArrayList比Vector快，它是异步，不会过载。
```
#### 3.Array 和 ArrayList 的区别
```
ArrayList默认初始化大小为10，每次扩容加一半。`（oldCapacity+(oldCapacity>>1):10-->15-->24）`
Array可以容纳基本类型和对象，而ArrayList只能容纳对象。
Array是指定大小的，而ArrayList大小可以不是固定的。
ArrayList的默认扩容大小是10。
```
### 10.hashMap的底层实现
[参考文章](http://blog.csdn.net/tuke_tuke/article/details/51588156)
#### 1.实现原理
```
首先有一个每个元素都是链表的数组（`Node<k,v>[] tab`），当添加一个元素（key-value）时，就首先计算元素key的hash值，
以此确定插入数组中的位置，但是可能存在同一hash值的元素已经被放在数组同一位置了，这时就添加到同一hash值的元素的后面(`p.next`)，
他们在数组的同一位置(`tab[i]`)，但是形成了链表，同一各链表上的Hash值是相同的，所以说数组存放的是链表。而当链表长度太长(>=7)时，链表就转换为红黑树，
这样大大提高了查找的效率。当链表数组的容量超过初始容量的0.75(16*0.75=12)时，再散列将链表数组扩大2倍，把原链表数组的搬移到新的数组中。
```
#### 2.扩容
```
构造hash表时，如果不指明初始大小，默认大小为16（即Node数组大小16），
    如果Node[]数组中的元素达到（填充比*Node.length）（第一次放元素进来也会扩容）重新调整HashMap大小 
    变为原来2倍大小,扩容很耗时。
    加载因子：0.75
因为如果填充多，说明表空间很大，如果不扩容说明链表会越来越长，这样查询起来效率比较低。
扩容之后将原来的链表数组的每一个链表分成奇偶两个分别挂在链表的数组的散列位置，
这样就减少了每个链表的长度，增加查找效率。
```
#### 3.Get方法原理
```
get(key)方法时先获取key的hash值，计算hash&(n-1)得到在链表数组中的位置first=tab[hash&(n-1)],
先判断first的key是否与参数key相等，
不等就遍历后面的链表找到相同的key值返回对应的Value值即可。
```
#### 4.put(key,value)的过程
```
1，判断键值对数组Node<K,V>[] tab是否为空或为null，为空以默认大小resize()；
2，根据键值key计算hash值得到插入的数组索引i，如果tab[i]==null，直接新建节点添加，否则转入3
3，判断当前数组中处理hash冲突的类型为链表还是红黑树(check第一个节点类型即可),分别处理。
当为链表时，遍历判断p.next是否为空，为空则插入，如果判断过程长度大于8转为红黑树，有相同的key也结束。
```
### 11.collection和collections的区别
```
collection是集合类的上级接口，主要子接口有：set,list
collections是针对集合类的一个帮助类，提供了操作集合的工具和方法,
一系列静态方法，主要用于对各种集合的排序、搜索、线程安全化等操作。
```
### 12.Exception和error的包结构
```
Throwable是Java语言中所有错误和异常的超类，它包含两个子类error和exception。
	Throwable包含了其线程创建时线程执行堆栈的快照，它提供了printStackTrace()等接口用于获取堆栈跟踪数据等信息。
Exception及其子类是throwable的一种形式，它指出了合理的应用程序想要捕获的条件。
RuntimeException是那些可能在java虚拟机正常运行时抛出的类。编译器不会检查运行时异常，例如：除数为0
Error和Exception一样也是throwable的子类，它指出合理的应用程序不应该试图捕获的异常。
Java将可抛出的（throwable）的结构分为3种类型：运行时异常（runtimeException），被检查异常（checked exception）和错误（error）
运行时异常：
RuntimeException及其子类都称为运行时异常，如除数为0,数组下标越界 。java.lang.classCastException;indexOutOfBoundsException;NullPointerException
被检查异常：
exception以及exception子类中除了runtimeexception之外 的其它子类都称为检查异常，编译器会检查它。
	Java认为Checked异常都是可以被处理的异常，一般用try..catch或者抛出异常。Java.lang.classNotfoundException;java.lang.NosuchMethodException;java.io.IOexception
错误：
error及其子类，编译器也不会检查错误。例如：虚拟机错误，资源不足，约束失败。
OOM：
	OutofMemoryError异常、虚拟机和本地方法栈溢出（Stack Overflow），运行时常量池溢出、方法区溢出
```
### 13.overLoad和overwrite(override)的区别
```
Overload：重载，参数类型、参数个数、参数顺序至少有一个不同。只有返回值不同不算重载（存在于父类、子类和同类之间）。
Override(overwrite)：重写（覆盖），在子类中重写和覆盖父类的方法，而且和父类方法中的返回值、参数类型、方法名相同，
	子类方法不能缩小父类的访问权限，子类方法不能比父类抛出更多的异常，方法被定义为final的不能重写。（存在于父类和子类之间）。

```
### 14.interface和abstract类的区别
```
abstract类:
用关键字abstract修饰   abstract class  aa{}
类中可以出现抽象方法，也可以包含普通方法。（有抽象方法的类一定是抽象类）
不能创建abstract类的实例，然而可以创建一个变量，其类型是一个抽象类，并让它指向具体子类的一个实例。
Abstract 类的子类为它们父类中的所有抽象方法提供实现，否则它们也是抽象类。
abstract方法：只允许声明，不能再添加final和static关键字修饰，即抽象方法必须是实例方法
Interface：
接口中可以有常量和方法体：public interface  aa{int a=1;void getName(); }
常量和方法的访问权限都是public的（可以省略public不写）
当一个普通类实现了该接口时，那么必须重写该接口的所有方法。
若父类实现了某个接口，那么子类也就自然实现了该接口，子类也不必再显示地使用关键字implements声明实现这个接口。
接口可以被继承，通过关键字extends
1.相同点 
A. 两者都是抽象类，都不能实例化。 
B. interface实现类及abstrctclass的子类都必须要实现已经声明的抽象方法。

2. 不同点 
A. interface需要实现，要用implements，而abstract class需要继承，要用extends。 
B. 一个类可以实现多个interface，但一个类只能继承一个abstract class。 
C. interface强调特定功能的实现，而abstractclass强调所属关系。 
D. 尽管interface实现类及abstrct class的子类都必须要实现相应的抽象方法，但实现的形式不同。interface中的每一个方法都是抽象方法，
	都只是声明的(declaration,没有方法体)，实现类必须要实现。而abstractclass的子类可以有选择地实现

```
### 15.写出单例模式
```
/**
 * 懒汉式单例（线程安全），类加载时不初始化
 * Created by Administrator on 2018/3/12.
 */
public class TestSingleton {
    private static TestSingleton testSingleton;
    private TestSingleton(){}
    public static synchronized TestSingleton a(){
        if(testSingleton==null){
            new TestSingleton();
        }
        return testSingleton;
    }
}
/**
 * 饿汉式单例，类加载时初始化
 * Created by Administrator on 2018/3/12.
 */
public class TestSingleton2 {
    private  static  TestSingleton2 testSingleton2=new TestSingleton2();
    private TestSingleton2(){}
    public static TestSingleton2 aa(){
        return  testSingleton2;
    }
}
```