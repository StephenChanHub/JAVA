

````markdown
# Java 学习笔记 — Lesson 02 方法（Method）

## 1 什么是方法

方法（Method）是一段 **可以重复使用的代码块**。

它的作用是：

- 提高代码复用性
- 让程序结构更清晰
- 减少重复代码

方法类似于其他语言中的 **函数（function）**。

示例：

```java
public static void sayHello() {
    System.out.println("Hello");
}
````

调用方法：

```java
sayHello();
```

输出：

```
Hello
```

---

# 2 为什么需要方法

如果没有方法：

```java
System.out.println("Hello");
System.out.println("Hello");
System.out.println("Hello");
System.out.println("Hello");
```

使用方法：

```java
sayHello();
sayHello();
sayHello();
sayHello();
```

优点：

```
代码复用
结构清晰
方便维护
```

---

# 3 方法基本语法

方法结构：

```java
返回值类型 方法名(参数) {

    方法体

}
```

示例：

```java
public static void sayHello() {

    System.out.println("Hello Java");

}
```

结构说明：

|部分|说明|
|---|---|
|public|访问修饰符|
|static|静态方法|
|void|无返回值|
|sayHello|方法名称|
|()|参数列表|
|{}|方法体|

---

# 4 方法调用

完整示例：

```java
public class Main {

    public static void sayHello() {
        System.out.println("Hello Java");
    }

    public static void main(String[] args) {

        sayHello();
        sayHello();

    }
}
```

输出：

```
Hello Java
Hello Java
```

---

# 5 带参数的方法

方法可以接收输入数据（参数）。

示例：

```java
public static void sayHello(String name) {

    System.out.println("Hello " + name);

}
```

调用：

```java
sayHello("Stephen");
sayHello("Tom");
```

输出：

```
Hello Stephen
Hello Tom
```

---

# 6 多个参数

```java
public static void add(int a, int b) {

    System.out.println(a + b);

}
```

调用：

```java
add(3,5);
add(10,20);
```

输出：

```
8
30
```

---

# 7 有返回值的方法

有些方法需要返回结果。

语法：

```java
return 返回值;
```

示例：

```java
public static int add(int a, int b) {

    return a + b;

}
```

调用：

```java
int result = add(3,5);

System.out.println(result);
```

输出：

```
8
```

---

# 8 方法执行流程

示例方法：

```java
public static int add(int a, int b) {

    return a + b;

}
```

调用：

```
add(3,5)
```

执行流程：

```
3 → a
5 → b
a+b → 8
return → 返回调用处
```

---

# 9 方法命名规范

Java 方法命名遵循 **小驼峰命名法（camelCase）**。

正确：

```
getUserName
calculateTotalPrice
printStudentInfo
```

错误：

```
GetName
PRINTNAME
get_name
```

---

# 10 小项目示例：计算器

```java
public class Calculator {

    public static int add(int a, int b) {

        return a + b;

    }

    public static int subtract(int a, int b) {

        return a - b;

    }

    public static void main(String[] args) {

        int result1 = add(10,5);
        int result2 = subtract(10,5);

        System.out.println(result1);
        System.out.println(result2);

    }

}
```

输出：

```
15
5
```

---

# 11 常见错误

## 忘记 return

错误：

```java
public static int add(int a, int b) {

    a + b;

}
```

正确：

```java
return a + b;
```

---

## 参数类型错误

错误：

```java
add("hello",5);
```

正确：

```java
add(5,10);
```

---

## 方法写在 main 里面

错误：

```java
public static void main(String[] args) {

    public static void test() {

    }

}
```

方法必须写在：

```
类内部
main 方法外部
```

---

# 12 练习

### 练习1

编写方法：

```
printMessage(String message)
```

输出 message。

---

### 练习2

编写方法：

```
multiply(int a,int b)
```

返回 a*b。

---

### 练习3

编写方法：

```
isAdult(int age)
```

返回：

```
true
false
```

---

# 本课总结

本课学习内容：

```
方法概念
方法语法
方法参数
返回值
方法调用
```

方法是 **Java程序结构的基础**。

---
