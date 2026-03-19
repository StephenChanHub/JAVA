
## 概念速记

- **继承（extends）**：子类继承父类的字段与方法，表示 _is-a_（是一个）关系。
    
- **重写（override）**：子类对父类方法提供新的实现（使用 `@Override` 注解）。
    
- **super**：在子类中调用父类的构造器或方法/字段（`super(...)`、`super.method()`）。
    
- **抽象类（abstract）**：可以包含抽象方法与具体方法，不能实例化，子类必须实现抽象方法。
    
- **接口（interface）**：定义能力契约，类可以实现多个接口；接口可含默认方法（`default`）。
    
- **多态（polymorphism）**：父类型引用指向子类型对象，运行时调用子类实现。
    
- **里氏替换原则（LSP）**：子类必须能替换父类而不改变程序正确性（子类不得违反父类契约）。
    

---

## 为什么要用继承

- **代码复用**：把共同属性与行为放在父类，减少重复。
    
- **建模类型关系**：表达“某物是另一个物的一种”。
    
- **支持多态**：用父类型写通用代码，运行时根据实际对象执行相应行为。
    

---

## 基本语法与示例

### 父类（Base）

```java
public class Animal {
    public void eat() {
        System.out.println("Animal eats");
    }
}
```

### 子类（Subclass）

```java
public class Dog extends Animal {
    public void bark() {
        System.out.println("Woof");
    }
}
```

### 使用

```java
public class Main {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();  // 继承来的方法
        d.bark();
    }
}
```

---

## 方法重写（Override）

- 使用 `@Override` 能让编译器帮你检查签名是否匹配。
    
- 重写要求：方法名、参数类型相同；返回类型可为协变（子类返回类型为父类返回类型的子类型）。
    

```java
public class Animal {
    public void eat() { System.out.println("Animal eats"); }
}

public class Dog extends Animal {
    @Override
    public void eat() { System.out.println("Dog eats dog food"); }
}
```

---

## `super` 的用法

- 在构造器中调用父类构造器：`super(args);`（必须放在构造器第一行）。
    
- 调用父类方法：`super.someMethod()`。
    
- 访问父类字段（若可见）：`super.fieldName`。
    

```java
public class Person {
    protected String name;
    public Person(String name) { this.name = name; }
}

public class Student extends Person {
    private String school;
    public Student(String name, String school) {
        super(name); // 调用父构造器
        this.school = school;
    }
}
```

---

## 构造器与继承细节

- 子类构造器会先调用父类构造器（隐式调用无参父构造器，或用 `super(...)` 显式调用）。
    
- 如果父类只有带参构造器且没有无参构造器，子类必须显式调用 `super(...)`。
    

---

## 抽象类 vs 接口（常用区分）

- 抽象类：用于有**共用实现**的类族；可以有字段、构造器与具体方法，也可以有抽象方法。
    
- 接口：用于定义**能力（能做什么）**；类可实现多个接口。接口方法默认是 `public`，Java 支持默认方法（`default`）与静态方法。
    

---

## 多态（Polymorphism）

- 编译时看引用类型，运行时看实际对象：
    

```java
Animal a = new Dog();
a.eat(); // 调用 Dog 的实现（运行时绑定）
```

- 多态常用于把不同子类统一处理（例如：`List<Animal>` 遍历调用 `speak()`）。
    

---

## 里氏替换原则（LSP）

- 子类应当能替代父类（父类的客户代码对父类的假设不应被子类破坏）。
    
- 违反 LSP 的常见例子：把 `Square` 继承自 `Rectangle` 并让 `setWidth` 与 `setHeight` 相互影响，会破坏父类对行为的假设。
    
- 规则提醒：若 `is-a` 语义不成立或会破坏契约，**不要继承**，优先使用组合或接口。
    

---

## static 与继承

- `static` 成员属于类，不参与运行时多态（静态方法通过类名调用，或引用类型决定调用哪个静态方法）。
    
- 不要用 `static` 期待多态行为。
    

---

## 常见坑与注意事项

1. **在构造器中调用可被重写的方法** —— 子类字段可能尚未初始化，导致不确定行为。
    
2. **滥用继承** —— 继承表示“is-a”，若只是复用实现，应优先考虑组合（has-a）。
    
3. **修改 equals/hashCode 语义** —— 在继承层次中改变相等定义会导致集合异常行为。
    
4. **访问控制** —— 尽量把字段设为 `private`，提供受控的访问方法（getter/setter 或业务方法）。
    
5. **接口冲突** —— 实现多个接口且接口带默认方法出现命名冲突时，需要显式重写并决定使用哪个默认实现（可以用 `A.super.defaultMethod()`）。
    

---

## 常见模式（继承相关）

- **模板方法模式（Template Method）**：在父类定义算法骨架，子类实现具体步骤（使用抽象方法）。
    
- **策略模式（Strategy）**：把可变的行为抽象成接口，用组合替代继承以提高灵活性。
    

---

## 练习

1. **基础练习**：实现抽象类 `Animal`（含 `name` 字段与抽象 `speak()`），实现 `Dog`/`Cat` 并重写 `speak()`，用 `Animal[]` 演示多态。
    
2. **构造链练习**：写 `Vehicle`（带 `brand` 构造器）与 `Car extends Vehicle`（在 Car 构造器里调用 `super` 并设置 `model`），打印 `brand` 与 `model`。
    
3. **LSP 反例**：实现 `Rectangle(width,height)` 与 `Square extends Rectangle`，写一个方法接受 `Rectangle` 并设置宽高，观察并分析为何 `Square` 继承会出问题；改用组合实现 `Square`（包含 `Rectangle`）并修复问题。
    

---

## 练习参考代码

**练习 1 参考**

```java
public abstract class Animal {
    protected String name;
    public Animal(String name){ this.name = name; }
    public abstract void speak();
}

public class Dog extends Animal {
    public Dog(String name){ super(name); }
    @Override public void speak(){ System.out.println(name + " says: Woof"); }
}

public class Cat extends Animal {
    public Cat(String name){ super(name); }
    @Override public void speak(){ System.out.println(name + " says: Meow"); }
}

// Main
public class Main {
    public static void main(String[] args){
        Animal[] arr = { new Dog("Rex"), new Cat("Mimi") };
        for(Animal a : arr) a.speak();
    }
}
```

**LSP 反例简述**

```java
// Rectangle with independent setters
class Rectangle {
    protected int width, height;
    public void setWidth(int w){ width = w; }
    public void setHeight(int h){ height = h; }
    public int area(){ return width * height; }
}

// Square inherits Rectangle and forces width==height in setters -> breaks LSP
```

解决：不要让 `Square` 继承 `Rectangle`，改为两者都实现 `Shape` 接口或用组合。

---

## 小结（记忆要点）

- 继承用于表达类型关系（is-a）并复用共性；若仅为复用实现优先组合。
    
- 多态是继承的关键价值：父类型代码在运行时调用子类实现。
    
- 严格遵守里氏替换原则，避免破坏父类型契约。
    
- 在设计中合理使用抽象类与接口：抽象类用于共享实现，接口用于定义能力。
    

---