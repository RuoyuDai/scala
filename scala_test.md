本次Scala考试包括三个部分：基础语言，函数式编程和编程实战三个类别，题目前会标明类别；本次考试预计需要两小时，包括单选题25道，编程题一道，请把握好时间。
--
1. [基础语言] 为什么要使用Scala？

* A. 更高的可维护性和生产率。
* B. 更好的并行支持和错误处理。
* C. 更高的可测试和伸缩性。
* D. 以上都是。
---
2. [基础语言] 下面Scala代码返回值不等于1的是：

* A.  `(1D * 10 / 10).intValue()` 
* B.  `"1".map(x => x - '0').sum`
* C.  `"abcd".foldRight(0)((x, acc) => acc + x)/ 394`
* D.  `List.range(1, 10).reverse.take(3).sum / 10`
---
3. [基础语言] Scala里的case类有什么特点：

* A. Scala编译器会自动补上equals, hashCode, toString, apply, unapply，比较和拷贝方法，无须再编写。
* B. 可以用在模式匹配中。
* C. Scala编译会帮忙实现序列化接口。
* D. 以上都是。
---
4. [基础语言] 如下Scala代码，

```scala
val x = List(1, 2, 3, 4, 5) match {
  case x :: 2 :: 4 ::  _ => x
  case Nil => 42
  case x :: y :: 3 :: 4 :: _ => x + y
  case h :: _ => h
  case _ => 101
}
```
x 最终被赋值为：

* A.  1    
* B.  42     
* C.  3    
* D.  101   
---
5. [基础语言] 如下表达式，返回为 false 的是：

* A.  `().isInstanceOf[Any]` 
* B.  `None.isInstanceOf[Option[_]]`
* C.  `Nil.isInstanceOf[AnyRef]`
* D.  `null.isInstanceOf[Any]`
---
6. [基础语言] 如下for语句
```scala
for {
  a <- List.range(1, 3)
  (_, b) <- Map("a" -> 1)
  c <- Seq(4, 5)
  d <- Some(2)
  if a < 2; if c > 4
} yield(a, b, c - 4, d - 1)
```
返回值为：

* A. (1, 1, 1, 1)
* B. List((1, 1, 1, 1))
* C. 4
* D. 42
---
7. [基础语言] 如下代码定义了三个变量， 
```scala
val a = 1
var b = 1
def c = 1
```
下面哪个语句是能够通过编译的：

* A. a = 2
* B. b = "c"
* C. c = 2
* D. b = 3
---
8. [基础语言] 如下代码定义了一个流：
```scala
val ones: Stream[Int] = Stream.cons(1, ones)
```
对这个定义，说法正确的是：

* A. ones没有被定义就直接使用，无法通过编译。
* B. 能够通过编译，但开始运行时，调用任何流的方法，都会陷入死循环。
* C. 这个定义产生了一个无限长度的流，由于Stream采用传引用来延迟计算，所有的元素都是在引用时才会计算。
* D. 以上说法都不对。
---
9. [基础语言] Scala支持高阶函数(High-Order)，关于高阶函数，错误的说法是：

* A. 高阶函数就是能够把函数作为参数传入或者作为返回值返回。
* B. Scala把函数作为first-class的值。
* C. 典型的，多数类型的map操作，就支持函数作为参数传入。
* D. Scala不支持在函数内定义子函数。
---
10. [基础语言] 如下代码的执行结果是：
```scala
abstract class AbsIterator {
  type T
  def hasNext: Boolean
  def next(): T
}

class StringIterator(s: String) extends AbsIterator {
  type T = Char
  private var i = 0
  def hasNext = i < s.length
  def next() = {
    val ch = s charAt i
    i += 1
    ch
  }
}

trait RichIterator extends AbsIterator {
  def foreach(f: T => Unit): Unit = while (hasNext) f(next())
}

class RichStringIter extends StringIterator("Scala") with RichIterator
val richStringIter = new RichStringIter
richStringIter foreach println

```
* A. 每行一个字符打印“Scala” 
* B. 直接报错
* C. 打印"Scala"
* D. 打印"Scala"的ASSIC码值
---
11. [基础语言] 如下代码的执行结果是：
```scala
abstract class Animal {
  def name: String
}

case class Cat(name: String) extends Animal
case class Dog(name: String) extends Animal

abstract class Printer[-A] {
  def print(value: A): Unit
}

class AnimalPrinter extends Printer[Animal] {
  def print(animal: Animal): Unit =
    println("The animal's name is: " + animal.name)
    
class CatPrinter extends Printer[Cat] {
  def print(cat: Cat): Unit =
    println("The cat's name is: " + cat.name)
}

object Lesson {
  val myCat: Cat = Cat("Boots")
  def printMyCat(printer: Printer[Cat]): Unit = {
    printer.print(myCat)
  }
  def main(args: Array[String]): Unit = {
    val catPrinter: Printer[Cat] = new CatPrinter
    val animalPrinter: Printer[Animal] = new AnimalPrinter
    printMyCat(catPrinter)
    printMyCat(animalPrinter)
  }
}

```
* A.
```
The cat's name is: Boots
The animal's name is: Boots
``` 
* B.
```
The animal's name is: Boots
The animal's name is: Boots
```
* C.
```
The cat's name is: Boots
The cat's name is: Boots
```
* D. 无法通过编译
---
12.[基础编程] 如下代码：
```scala
import scala.concurrent.{ExecutionContext, Future}

implicit val ec = ExecutionContext.global

for(i <- (1 to 10).reverse) {
  Future {
    Thread.sleep(i * 1000)
    println(i + "done")
  }
}

```
在一台4核机器上执行时，会发生什么：
* A. 没有传入执行的ExecutionContext，根本无法运行。
* B. 在执行时间足够长的情况下，会每次延时相应秒执行四个任务，最终能够执行完成。
* C. implicit变量设置有误，Future运行时无法识别。
* D. Thread.sleep函数会睡眠当前线程，最后死锁，无法退出。
---
13. [基础编程] 如下代码：
```scala
trait User {
  def username: String
}

trait Tweeter {
  this: User =>
  def tweet(tweetText: String) = println(s"$username: $tweetText")
}

class VerifiedTweeter(val username_ : String) extends Tweeter with User { 
  def username = s"real $username_"
}

val realBeyoncé = new VerifiedTweeter("Beyoncé")
realBeyoncé.tweet("Just spilled my glass of lemonade")
```
的描述正确的是：
* A. 输出为：
```
real Beyoncé: Just spilled my glass of lemonade
```
* B. 无法编译通过，里面有非法字符é
* C. 无法编译通过，语法声明有误。
* D. 运行时出错，无法获取username
--- 
14. [基础编程] 如下代码进行正则表达式匹配，
```scala
val Pattern = "(.*)=(.*)".r

val a = "Scala=Powerful" match {
  case Pattern(name, adj) => s"$name is $adj."
  case _ => "Php is the best!"
}

```
变量a最终被赋值为：
* A.
```
Php is the best!
```
* B.
```
name is adj.
```
* C.
```
Scala Powerful.
```
* D.
```
Scala is Powerful.
```
15. [函数式编程] 柯里化是将函数f(x,y)转化为f(x)(y)的过程，如下函数声明：
```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C)
```
这个函数的唯一实现为：

* A. 
```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C) =
  a => b => f(a, b)
```
* B.
```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C) =
  (a, b) => f(a, b)
```
* C.
```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C) =
  a => b => f(a, b)f(a)f(b)
```
* D.
```scala
def curry[A,B,C](f: (A, B) => C): A => (B => C) =
  a => b => f(a)f(b)f(a, b)
```
---
16. [函数式编程] 下面哪种写法是阶乘函数的尾递归实现：

* A. 
```scala
def fac(n: Int): Int = {
  if (n < 2) 1
  else n * f(n - 1)
}
```
* B.
```scala
def fac(n: Int): Int = {
  def go(n: Int, acc: Int): Int = 
    if (n <= 0) acc
    else go(n - 1, n * acc)
  go(n, 1)
}
```
* C.
```scala
def fac(n: Int): Int = {
  if (n < 2) 1
  else f(n * (n - 1))
}
```
* D.
```scala
def fac(n: Int): Int = {
  def go(n: Int, acc: Int): Int = 
    if (n <= 0) acc
    else go(n - 1, n * acc)
}
```
---
17. [函数式编程] 下面哪种写法是foldRight右折叠函数的尾递归实现：

* A. 
```scala
def foldRight[A, B](as: List[A], z: B)(f: (A, B) => B): B = {
  as match {
    case Nil => z
    case (h :: t) => f(h, foldRight(t, z, f))
  }
}
```
* B.
```scala
def foldRight[A, B](as: List[A], z: B)(f: (A, B) => B): B = {
  def go(acc: B, aas: List[A]): B = {
    aas match {
      case Nil => acc
      case (h :: t) => go(f(h, acc), t)
    }
  }
  go(z, as)
}
```
* C.
```scala
def foldRight[A, B](as: List[A], z: B)(f: (A, B) => B): B = {
  as match {
    case Nil => z
    case (h :: t) => f(h, f(h, foldRight(t, z, f)))
  }
}
```
* D.
```scala
def foldRight[A, B](as: List[A], z: B)(f: (A, B) => B): B = {
  def go(acc: B, aas: List[A]): B= {
    aas match {
      case Nil => acc
      case (h :: t) => go(f(h, acc), t)
    }
  }
}
```
---
18. [函数式编程] partial函数用于部分的替换函数入参，函数声明如下：
 ```scala
 def partial[A,B,C](a: A, f: (A,B) => C): B => C
 ```
这个函数的唯一实现如下：

* A. 
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B) => f(b, a)
```
* B.
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B, a: A) => f(a, b)
```
* C.
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B) => f(a, f(a, b))
```
* D.
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B) => f(a, b)
```
---
19. [函数式编程] 有如下类型定义：
```scala
  type Result = (Boolean, String, Int)
  type Rule = (Int, String) => Result
```
下面哪个函数定义，符合Rule类型:

* A. 
```scala
(n: Int, ctx: String) => {
  if (n > 1 ) (true, ctx, n)
  else (false, ctx, n)
}
```
* B.
```scala
(n: Int, ctx: String) => {
  if (n > 1 ) n
  else (false, ctx, n)
}
```
* C.
```scala
(n: Int, ctx: String) => {
  if (n > 1 ) n
  else (false, n, n)
}
```
* D.
```scala
(n: Int, ctx: String) => {
  if (n > 1 ) n
  else (false, ctx)
}
```
---
20. [函数式编程] 下面哪个函数定义不存在副作用，即为纯函数：
* A. 
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B) => f(a, b)
```
* B.
```scala
def isGoodEnough(n: Int): Boolean = 
  if (n > 100) true
  else {
    println("Not enough!")
    false
  }
```
* C.
```scala
def buyBreakfast(money: Int): Boolean = 
  val successed = PayService.buyBreakfast(money)
  successed == 1
```
* D.
```scala
def notifyFollower(msg: String) = 
  val notifyMsg = msg + ", from leader"
  NettyNofitier.send(msg)
```
---
21. [函数式编程]关于monad，下面的描述错误的是：
* A. Monad在Scala中，通常以如下的定义实现：
```scala
trait Monad[M[_]] {
  def unit[A](a: A): M[A]
  def flatMap[A, B](fa: M[A])(f: A => M[B]): M[B]
}
```
* B. Monad需要满足Identity法则，如下：
```scala
unit(x).flatMap(f) == f(x)
m.flatMap(unit) == m
```
* C. Monad需要满足结合率，如下：
```scala
m.flatMap(f).flatMap(g) == m.flatMap(x => f(x).flatMap(g))
```
* D. 以上都错误
---
22. [函数式编程] 在scala中，哪些类型及定义在之上的操作，实际上构成了一个monad？
* A. 只有Option
* B. 只有List
* C. 只有Future
* D. 以上都是
---
23. [函数式编程] Monad其实是一个Functor，Functor的定义如下：
```scala
trait Functor[F[_]] {
  def map[A,B](a: F[A])(f: A => B): F[B]
}
```
如果某类型的Monad已经提供了unit和flatMap实现，那么map可以实现为：
* A.
```scala
def map[A,B](a: F[A])(f: A => B): F[B] =
  flatMap(a)(a => unit(f(a)))
```
* B. 别闹，根本无法定义
* C. 
```scala
def map[A,B](a: F[A])(f: A => B): F[B] =
  flatMap(a)(a => f(unit(a)))
```
* D.
```scala
def map[A,B](a: F[A])(f: A => B): F[B] =
  flatMap(a)(a => f(a))
```
---
24. [函数式编程] 如果某类型的Monad已经提供了unit和flatMap实现，那么就可以顺带定义一个map2函数
```scala
def map2[A,B,C](ma: F[A], mb: F[B])(f: (A,B) => C): F[C]
```
这个函数能够将两个Monad合并为一个新的Monad，定义正确的是：
* A.
```scala
def map2[A,B,C](ma: F[A], mb: F[B])(f: (A, B) => C): F[C] =
  flatMap(ma)(a => map(mb)(b => f(a, b)))
```
* B.
```scala
def map2[A,B,C](ma: F[A], mb: F[B])(f: (A, B) => C): F[C] =
	ma.flatMap(a => mb.flatMap(b => f(a, b)))
```
* C.
```scala
def map2[A,B,C](ma: F[A], mb: F[B])(f: (A, B) => C): F[C] =
	ma.map(a => mb.map(b => f(a, b)))
```
* D.
```scala
def map2[A,B,C](mb: F[B])(f: (A, B) => C): F[C] =
	flatMap(b => ma.map(a => f(a, b)))
```
---
25. [函数式编程] 如果某类型Monad已经实现，map2函数也已经定义，尝试定义如下函数：
```scala
def sequence[A](lma: List[M[A]]): M[List[A]]
```
这个函数将列表中的容器类型，转换为容器中的列表类型，正确的实现是：
* A.
```scala
def sequence[A](lma: List[F[A]]): F[List[A]] =
  lma.foldRight(unit(List[A]()))((ma, mla) => map(mla)(_ :: _))
```
* B.
```scala
def sequence[A](lma: List[F[A]]): F[List[A]] =
  map2(ma, mla)(_ :: _)
```
* C.
```scala
def sequence[A](lma: List[F[A]]): F[List[A]] =
  lma.foldRight(unit(List[A]()))((ma, mla) => map2(ma, mla)(_ :: _))
```
* D.
```scala
def sequence[A](lma: List[F[A]]): F[List[A]] =
  lma.foldRight(unit(List[A]()))((ma, mla) => map2(mla, ma)(_ :: _))
```
---
26. [编程实战]
* 写一个程序模拟报数，从1到n
* 如果数字是3的倍数，不输出数字，替换为“Fizz”；如果是5的倍数，不输出数字，替换为“Buzz”；如果是7的倍数，替换为“Wizz”。
* 如果有一个数字，同时是多个数字的倍数，则依次替换为对应的字符；如，21同时是3和7的倍数，替换为“FizzWizz”；  
  如，15同时是3和5的倍数，替换为“FizzBuzz”；105同时是3,5,7的倍数替换为“FizzBuzzWizz”
* 如果数字中含有3,5,7中的任何一个，则忽略上述规则，直接以第一个含有的数字对应的字符来表达，比如35替换为“Fizz” 
请编写一个函数，实现上述4项描述，函数定义为：
```scala
def count(i: Int): Any
```
测试用例为（包括但不限于）：
```scala
def test() = {
    assert("Fizz".equals(count(9)))
    assert("Buzz".equals(count(5)))
    assert("Wizz".equals(count(7)))
    assert("Buzz".equals(count(15)))
    assert("Fizz".equals(count(35)))
    assert("FizzWizz".equals(count(21)))
    assert("FizzBuzzWizz".equals(count(210)))
    assert(4.equals(count(4)))
}
```  
