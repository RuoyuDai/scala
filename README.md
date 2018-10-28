本次Scala考试包括三个部分：基础语言，函数式编程和编程实战三个类别，题目前会标明类别；本次考试预计需要两小时，包括单选题20道，编程题一道，请把握好时间。
---
1. [基础语言] 如下Scala代码，

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
2. [基础语言] 如下表达式，返回为 false 的是：

* A.  `().isInstanceOf[Any]` 
* B.  `None.isInstanceOf[Option[_]]`
* C.  `Nil.isInstanceOf[AnyRef]`
* D.  `null.isInstanceOf[Any]`
---
3. [基础语言] 如下for语句
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
4. [基础语言] 如下代码定义了三个变量， 
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
5. [函数式编程] 柯里化之将函数f(x,y)转化为f(x)(y)的过程，如下函数声明：
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
6. [函数式编程] 下面哪种写法是阶乘函数的尾递归实现：

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
7. [函数式编程] 下面哪种写法是foldRight右折叠函数的尾递归实现：

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
8. [函数式编程] partial函数用于部分的替换函数入参，函数声明如下：
 ```scala
 def partial1[A,B,C](a: A, f: (A,B) => C): B => C
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
9. [函数式编程]有如下类型定义：
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
10. [函数式编程]下面哪个函数定义不存在副作用，即为纯函数：
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
