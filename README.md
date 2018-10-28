本次考试包括三个部分：基础语言，函数式编程和编程实战三个类别，题目前会标明类别；本次考试预计需要两小时，包括单选题20道，多选题10道，编程题一道，请把握好时间。

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

2. [基础语言] 如下表达式，返回为 false 的是：

* A.  `().isInstanceOf[Any]` 
* B.  `None.isInstanceOf[Option[_]]`
* C.  `Nil.isInstanceOf[AnyRef]`
* D.  `null.isInstanceOf[Any]`

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

4.  
