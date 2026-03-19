
## 1 什么是封装

**封装（Encapsulation）** 是面向对象编程（OOP）的三大核心特性之一：

- Encapsulation（封装）
    
- Inheritance（继承）
    
- Polymorphism（多态）
    

封装的核心思想：

> **隐藏对象内部数据，只通过方法对外提供访问。**

简单理解：

```
隐藏数据 + 暴露接口
```

目的：

- 保护数据安全
    
- 控制数据修改规则
    
- 降低系统耦合
    
- 提高代码可维护性
    

---

# 2 为什么需要封装

假设我们写一个银行账户类：

```java
public class BankAccount {

    public double balance;

}
```

使用：

```java
BankAccount acc = new BankAccount();
acc.balance = 1000;
acc.balance = -5000;
```

问题：

余额可以被随意修改。

现实世界中：

```
账户余额不可能随便变成负数
```

原因：

```
数据完全暴露
```

解决方法：

```
封装
```

---

# 3 Java 如何实现封装

Java 通过 **访问修饰符 + 方法接口** 实现封装。

### 第一步：隐藏字段

```java
private double balance;
```

`private` 表示：

```
只有当前类可以访问
```

外部代码无法直接访问。

---

### 第二步：提供方法接口

```java
public class BankAccount {

    private double balance;

    public void deposit(double amount){
        if(amount > 0){
            balance += amount;
        }
    }

    public boolean withdraw(double amount){

        if(amount <= balance){
            balance -= amount;
            return true;
        }

        return false;
    }

    public double getBalance(){
        return balance;
    }
}
```

使用：

```java
BankAccount acc = new BankAccount();

acc.deposit(1000);
acc.withdraw(200);

System.out.println(acc.getBalance());
```

现在：

```
余额不能被随意修改
```

必须通过：

```
deposit()
withdraw()
```

---

# 4 Getter / Setter

Java 中常见封装写法：

```java
private int age;
```

Getter：

```java
public int getAge(){
    return age;
}
```

Setter：

```java
public void setAge(int age){
    this.age = age;
}
```

示例：

```java
public class Student {

    private String name;
    private int age;

    public String getName(){
        return name;
    }

    public void setName(String name){
        this.name = name;
    }

    public int getAge(){
        return age;
    }

    public void setAge(int age){
        this.age = age;
    }
}
```

这种结构叫：

```
Java Bean
```

许多框架依赖这种结构，例如：

- Spring
    
- Hibernate
    
- Jackson
    

---

# 5 封装 ≠ Getter / Setter

很多教程会说：

```
封装 = private + getter/setter
```

这是 **不完全正确的**。

封装真正含义：

```
隐藏内部实现 + 暴露合理行为
```

例如银行账户：

错误设计：

```
setBalance()
```

正确设计：

```
deposit()
withdraw()
```

因为：

```
余额不应该被随意设置
```

---

# 6 封装的最大好处

封装允许我们：

```
修改内部实现
而不影响外部代码
```

示例：

初始设计：

```java
private int age;

public int getAge(){
    return age;
}
```

后来需求变化：

```
年龄通过生日计算
```

修改内部实现：

```java
private LocalDate birthday;

public int getAge(){
    return Period.between(birthday, LocalDate.now()).getYears();
}
```

外部代码：

```
user.getAge();
```

完全不用修改。

---

# 7 Java 访问控制级别

Java 提供四种访问控制：

| 修饰符       | 同类  | 同包  | 子类  | 其他包 |
| --------- | --- | --- | --- | --- |
| private   | ✅   | ❌   | ❌   | ❌   |
| default   | ✅   | ✅   | ❌   | ❌   |
| protected | ✅   | ✅   | ✅   | ❌   |
| public    | ✅   | ✅   | ✅   | ✅   |

推荐实践：

```
字段：private
方法：public
```

---

# 8 Docker 类比封装（非常直观）

可以用 Docker 理解封装。

|OOP|Docker|
|---|---|
|Class|Image|
|Object|Container|
|Encapsulation|Container isolation|
|private field|Container 内部文件|
|public method|暴露端口|
|getter|读取 API|
|setter|写入 API|

示例：

```
docker run -p 3306:3306 mysql
```

外部可以访问：

```
localhost:3306
```

但不能访问：

```
/var/lib/mysql
内部实现
数据库存储结构
```

这就是：

```
Encapsulation
```

---

# 9 封装的设计原则

设计类时应该遵循：

### 1 隐藏数据

```
private fields
```

---

### 2 暴露行为而不是数据

坏设计：

```
setBalance()
```

好设计：

```
deposit()
withdraw()
```

---

### 3 在 setter 中进行数据校验

```java
public void setAge(int age){

    if(age < 0 || age > 120){
        throw new IllegalArgumentException("invalid age");
    }

    this.age = age;
}
```

---

### 4 不可变对象（Immutable Object）

有些字段只允许初始化：

```java
private final String orderId;
```

构造函数赋值：

```java
public Order(String orderId){
    this.orderId = orderId;
}
```

只提供 getter：

```java
public String getOrderId(){
    return orderId;
}
```

---

# 10 完整封装示例

```java
public class Student {

    private String name;
    private int age;
    private double score;

    public Student(String name,int age,double score){
        this.name = name;
        setAge(age);
        setScore(score);
    }

    public String getName(){
        return name;
    }

    public int getAge(){
        return age;
    }

    public void setAge(int age){

        if(age < 0 || age > 120){
            throw new IllegalArgumentException("invalid age");
        }

        this.age = age;
    }

    public double getScore(){
        return score;
    }

    public void setScore(double score){

        if(score < 0 || score > 100){
            throw new IllegalArgumentException("invalid score");
        }

        this.score = score;
    }

    public boolean isPass(){
        return score >= 60;
    }
}
```

---

# 11 封装核心总结

封装的本质：

```
隐藏数据
控制访问
暴露行为
```

最重要的一句话：

> **不要暴露数据，暴露行为。**

---

# 12 关键记忆

```
Encapsulation
=
Data Hiding
+
Controlled Access
```

或理解为：

```
Object = Black Box
```

外部只知道：

```
输入
输出
```

不知道内部实现。

---

# 13 面试常见回答

什么是封装？

标准回答：

> 封装是面向对象编程的核心特性之一，通过隐藏对象内部数据，并提供公共方法访问，从而保护数据安全并降低系统耦合。