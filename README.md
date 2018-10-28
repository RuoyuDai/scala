本次Scala考试包括三个部分：基础语言，函数式编程和编程实战三个类别，题目前会标明类别；本次考试预计需要两小时，包括单选题20道，编程题一道，请把握好时间。
---
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
* C. Scala编译会帮忙实现序列化借口。
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
  a <- List.range(1, 3). 
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
10. [函数式编程] 柯里化是将函数f(x,y)转化为f(x)(y)的过程，如下函数声明：
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
11. [函数式编程] 下面哪种写法是阶乘函数的尾递归实现：

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
12. [函数式编程] 下面哪种写法是foldRight右折叠函数的尾递归实现：

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
  def go(acc: B, aas: List[A]): B= {
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
13. [函数式编程] partial函数用于部分的替换函数入参，函数声明如下：
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
14. [函数式编程] 有如下类型定义：
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
15. [函数式编程] 下面哪个函数定义不存在副作用，即为纯函数：
* A. 
```scala
def partial[A,B,C](a: A, f: (A,B) => C): B => C =
  (b: B) => f(a, b)
```
* B.
```scala
def isGoodEnough(n: Int): Boolean = 
  if (n > 100) true
  esle {
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
16. [函数式编程]关于monad，下面的描述错误的是：
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
17. [函数式编程] 在scala中，哪些类型及定义在之上的操作，实际上构成了一个monad？
* A. 只有Option
* B. 只有List
* C. 只有Future
* D. 以上都是
---
18. [函数式编程] Monad其实是一个Functor，Functor的定义如下：
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
19. [函数式编程] 如果某类型的Monad已经提供了unit和flatMap实现，那么就可以顺带定义一个map2函数
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
20. [函数式编程] 如果某类型Monad已经实现，map2函数也已经定义，尝试定义如下函数：
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
21. [编程实战]
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
