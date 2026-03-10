**Java 第一课 Markdown 笔记**

````markdown
# Java 学习笔记 — Lesson 01 基础语法

## 1 Java 程序基本结构

一个最简单的 Java 程序：

```java
public class Main {
    public static void main(String[] args) {

        System.out.println("Hello Java");

    }
}
````

### 结构说明

|代码|说明|
|---|---|
|`public class Main`|定义一个类|
|`main()`|Java 程序入口|
|`System.out.println()`|控制台输出|

Java 程序执行流程：

```
main() → 从上往下执行
```

---

# 2 变量（Variable）

变量可以理解为 **存储数据的盒子**。

### 语法

```java
数据类型 变量名 = 值;
```

### 示例

```java
int age = 25;
double price = 19.99;
char grade = 'A';
boolean isStudent = true;
```

说明：

|类型|含义|
|---|---|
|`int`|整数|
|`double`|小数|
|`char`|单个字符|
|`boolean`|true / false|

---

# 3 基本数据类型

Java 一共有 **8 种基本数据类型**，但初学只需要先掌握 4 个：

|类型|示例|说明|
|---|---|---|
|int|10|整数|
|double|3.14|小数|
|char|'A'|字符|
|boolean|true|布尔|

### 示例

```java
int age = 20;
double height = 1.75;
char gender = 'M';
boolean isStudent = true;
```

---

# 4 字符串 String

字符串用于存储文本。

### 示例

```java
String name = "Stephen";
```

注意：

```
String 使用双引号 ""
char 使用单引号 ''
```

### 字符串拼接

```java
String name = "Stephen";
int age = 25;

System.out.println(name + " is " + age);
```

输出：

```
Stephen is 25
```

---

# 5 运算符

## 算术运算

```java
int a = 10;
int b = 5;

System.out.println(a + b);
System.out.println(a - b);
System.out.println(a * b);
System.out.println(a / b);
```

输出：

```
15
5
50
2
```

---

## 比较运算

```java
int a = 10;
int b = 5;

System.out.println(a > b);
System.out.println(a < b);
System.out.println(a == b);
```

输出：

```
true
false
false
```

---

# 6 条件判断 if

### 基本语法

```java
if (条件) {
    执行代码
}
```

### 示例

```java
int age = 18;

if (age >= 18) {
    System.out.println("Adult");
}
```

---

## if else

```java
int age = 16;

if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

---

# 7 for 循环

用于重复执行代码。

### 示例

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

输出：

```
1
2
3
4
5
```

---

# 8 while 循环

当条件成立时持续执行。

```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

输出：

```
1
2
3
4
5
```

---

# 9 switch 语句

用于多条件判断。

```java
int day = 2;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    default:
        System.out.println("Other day");
}
```

---

# 10 练习

创建文件：

```
Practice1.java
```

代码：

```java
public class Practice1 {

    public static void main(String[] args) {

        String name = "Stephen";
        int age = 25;

        if (age >= 18) {
            System.out.println(name + " is adult");
        } else {
            System.out.println(name + " is minor");
        }

    }

}
```

运行后输出示例：

```
Stephen is adult
```

---

# 本课总结

今天学习了 Java 最基础的 5 个知识点：

```
变量
基本数据类型
String
if 条件判断
循环（for / while）
```

这些内容是 **Java 编程的基础**。