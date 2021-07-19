Java编程思想 示例代码：https://github.com/Scott-Zou-Developer/thinking-In-Java
Java编程思想 习题答案：http://greggordon.org/java/tij4/solutions.htm

## 1 对象导论

### 1.1 面向对象编程思想五个基本特性：

（1）**万物皆对象：** 对象是奇特的变量，可以存储数据，还可以要求它在自身上进行操作。理论上讲，你可以抽取待求解问题的任何概念化构件（狗、建筑物、服务等），将其表示为程序中的对象。

（2）**程序是对象的集合，他们通过发送消息来告知彼此所要做的：** 可以把消息理解为对某个特定对象的调用请求。

（3）**每个对象都有自己的有其他对象所构成的存储：** 可以通过创建包含现有对象的包的方式来创建新类型的对象。因此，可以在程序中构建复杂的体系，同时将其复杂性隐藏在对象的简单性背后。

（4）**每个对象都拥有其类型：** 每个对象都是每个类的一个实例。

（5）**某一特定类型的所有对象都可以接受同样的消息：** 这种可替代性是OOP中最重要的概念。

### 1.2 类和数据类型的异同？

类描述了具有相同特性（数据元素）和行为（功能）的对象集合，所以一个类实际是一个数据类型。例如所有浮点型数字具有相同的特性和行为集合。两者的差距在于，程序员通过定义类来适应问题，而不再被迫只能使用现有的用来表示机器中的存储单元的数据类型。可以根据新的需求，通过添加新的数据类型来扩展编程语言。编程系统欣然接受新的类，并且像对待内置类型一样地照管它们和进行类型检查。

### 1.3 容器

创建另一种对象类型，这种新的对象类型持有对其他对象的引用。

### 1.4 参数化类型？

参数化类型就是一个编译器可以自动定制作用于特定类型上的类。例如，通过参数化类型，编译器可以定制一个只接纳和取出Shape对象的容器。

```java
ArraryList<Shape> shapes = new ArrayList<Shape>();
```

### 1.5 对象的创建和生命周期？

Java采用动态内存分配方式，每当想要创建新对象时，就要使用new关键字来构建此对象的动态实例。

## 2 一切皆对象

### 2.1 用引用操纵对象？

尽管一切皆对象，但是操纵的标识符实际上是对象的一个引用。可以类比成遥控（引用）操纵电视（对象）。一旦创建一个引用，就希望它与一个对象相关联。

### 2.2 Java基本类型

|  基本类型   |  大小   |  最小值   |      最大值      |     默认值     |  包装器类型   |
| :---------: | :-----: | :-------: | :--------------: | :------------: | :-----------: |
| **boolean** |   --    |    --     |        --        |     false      |  **Boolean**  |
|  **char**   | 16 bits | Unicode o | Unicode 2^16 - 1 | '\uoooo'(null) | **Character** |
|  **byte**   | 8 bits  |   -128    |       +127       |    (byte)0     |   **Byte**    |
|  **short**  | 16 bits |   -2^15   |     +2^15-1      |    (short)0    |   **Short**   |
|   **int**   | 32 bits |   -2^31   |     +2^31-1      |       0        |    **Int**    |
|  **long**   | 64 bits |   -2^63   |     +2^63-1      |       0L       |   **Long**    |
|  **float**  | 32 bits |  IEEE754  |     IEEE754      |      0.0f      |   **Float**   |
| **double**  | 64 bits |  IEEE754  |     IEEE754      |      0.0d      |  **Double**   |
|  **void**   |   --    |    --     |        --        |                |   **Void**    |

基本类型具有的包装器类型，使得可以在堆中创建一个非基本对象，用来表示对应的基本类型。例如：

```Java
Character ch = new Character("x");
```

### 2.3 变量的作用域？

作用域决定了在其定义的变量名的可见性和生命周期，**Java变量的作用域由花括号决定**，在作用域里定义的变量只可用于作用域之前。

### 2.4 对象的作用域？

Java对象不具备和基本类型一样的生命周期，当用new创建一个Java对象时，它可以存活于作用域以外。比如代码：

```Java
{
	String s = new String("a string");
}// End of Scope
```

引用s在作用域终点消失，然而，s指向的String对象仍继续占据内存空间。在这一段代码之后，我们无法在作用域之后访问这个对象，因为对它唯一的引用超出了作用域的范围。、

### 2.5 变量默认值

若类的某个基本成员是基本数据类型，即使没有初始化，Java也会确保它获得一个默认值（当变量作为类的成员使用时，Java才确保给定其默认值，以确保那些是基本类型的成员变量得到初始化，防止产生程序错误）。

然而上述初始化方法不适用于“局部”变量，例如某个方法中定义 int x ; ,那么变量x得到的值可能是任意值，而不会被自动初始化为零。所以在使用x变量前，应先对其赋一个适当的值。如果忘记了这么做，Java会在编译时返回一个错误，告诉你此变量没有初始化。

### 2.6 方法

方法的基本构成：方法的返回值类型、方法名称、参数列表、方法体

## 3 操作符

### 3.1 对象的赋值

对一个对象操作时，我们真正操作的是对象的引用，所以对象的赋值是将“引用”从一个地方赋值到另一个地方。

### 3.2 “别名现象”经典案例

代码示例：

```java
class Tank{
	int level;
}

public class Assignment{
	public static void main(String[] args){
		Tank t1 = new Tank();
		Tank t2 = new Tank();
		t1.level = 9;
		t2.level = 47;
		print("1: t1.level: "+ t1.level +", t2.level: " + t2.level);
		
		t1 = t2;
		print("1: t1.level: "+ t1.level +", t2.level: " + t2.level);
		
		t1.level = 27;
		print("1: t1.level: "+ t1.level +", t2.level: " + t2.level);
		
	}
}

/**output**/
1:  t1.level: 9, t2.level: 47
2:  t1.level: 47, t2.level: 47
3:  t1.level: 27, t2.level: 27
```

**分析：**t1和t2是Tank两个实例，对每个Tank类对象都赋予了一个不同的值，赋值操作的是一个对象的引用，所以3操作，t1.leval和t3.level值相同（修改t1的同时也改变了t2，这是由于t1和t2包含的是相同的引用，他们指向相同的对象，原本t1包含的对对象的引用，是指向一个值为9的对象，在对t1赋值的时候，这个引用被覆盖，也就是丢失了，而那个不再被引用的对象会由“垃圾回收器”自动清理）。**这种现象称为“别名现象”。**

**别名问题的解决办法：**t1.level = t2.level

这样可以保持两个对象彼此独立，而不是将t1和t2绑定到相同的对象。

### 3.3 方法调用中的别名问题

代码：

```java
class Letter{
    char c;
}

public class PassObject{
    static void f(Letter y){
        y.c = 'z';
    }
    public static void main(String[] args){
        Letter x = new Letter();
        x.c = 'a';
        print("1: x.c: " + x.c);
        f(x);
        print("2: x.c: " + x.c);
    }
}
/output/
1: x.c: a
2: x.c: z
```

在许多编程语言中，方法f()似乎要在它的作用域内复制其参数Letter y的一个副本，但实际只是传递了一个引用，所以代码行，y.c =  'z'，实际改变的是f()之外的对象。

### 3.4 对象的等价性

==和!=比较的就是对象的引用，如果要比较两个对象的实际内容是否相同，可以使用方法equals()。

equals()方法不适用于“**基本类型**”，基本类型直接使用==和!=。

代码例子：

```java
class Value{
	int i;
}

public class EqualsMethod{
	public static void main(String[] args){
    	Value v1 = new Value();
        Value v2 = new Value();
        v1.i = v2.i = 100;
        System.out.println(v1.equals(v2));
	}
}
/output/
false
```

解析：equals()的默认行为是比较引用。

## 5 初始化和清理

### 5.1 构造器

可以假想为编写的每一个类都定义一个initialize()方法，该方法的名称提醒你在使用其对象之前，应先调用initialize()。在Java中，通过提供构造器，类的设计者可确保每个对象都会得到初始化。创建对象时，如果其类具有构造器，Java就会在用户有能力操作对象之前自动调用相应的构造器，从而保证了初始化的进行。

以下就是一个带有构造器的简单类：

```java
class Rock{
	Rock(){
		System.out.print("Rock");
	}
}

public class SimpleConstructor{
	public static void main(String[] args){
		for(int i = 0; i < 10; i++){
			new Rock();
		}
	}
}
/**output**/
Rock Rock Rock Rock Rock Rock Rock Rock Rock Rock
```

构造器特点：

（1）构造器的名称必须与类名完全相同，所以“每个方法首字母小写”的编码风格并不适用于构造器。

（2）不接受任何参数的构造器叫做**默认构造器**，Java中使用的术语又称**无参构造器**。

（3）构造器中也可以带有**形式参数**，以便指定如何创建对象。

（4）构造器是一种特殊类型的方法，因为它没有返回值，这和普通方法返回值为空（void）明显不同。对于空返回值，尽管方法本身不会自动返回什么，但仍可选择让它返回别的东西。构造器则不会返回任何东西。 

### 5.2 this关键字

**this关键字只能在方法内部使用，表示对“调用方法的那个对象”的引用。**

this的用法和其它对象引用并无不同，但要注意如果在方法内部调用同一个类的另一个方法，就不必使用this，直接调用即可。

例如：

```java
public class Leaf{
	void pick(){}
	void pit(){
		pick();
	}
}
```

在pit()内部，你可以写this.pick()但是没有必要，编译器能够帮你自动添加，只有当需要明确指出当前对象的引用时，才需要使用this关键字，例如，当需要返回当前对象的引用时，就常常在return中这样写：

```java
public class Leaf{
	int i = 0;
	Leaf increment(){
		i++;
		return this;
	}
}
```

### 5.3 static关键字

**在static方法的内部不能调用非static方法，在非static方法的内部可以调用static方法。**

可以在没有创建对象的前提下，仅仅通过类本身来调用static方法。

Java中禁止使用全局方法，但是你类中使用static方法就可以访问其它static方法和static域。

### 5.4 构造器初始化的顺序

构造器初始化案例代码：

```java
//: initialization/OrderOfInitialization.java
package initialization; /* Added by Eclipse.py */
// Demonstrates initialization order.
import static net.mindview.util.Print.*;

// When the constructor is called to create a
// Window object, you'll see a message:
class Window {
  Window(int marker) { print("Window(" + marker + ")"); }
}

class House {
  Window w1 = new Window(1); // Before constructor
  House() {
    // Show that we're in the constructor:
    print("House()");
    w3 = new Window(33); // Reinitialize w3
  }
  Window w2 = new Window(2); // After constructor
  void f() { print("f()"); }
  Window w3 = new Window(3); // At end
}

public class OrderOfInitialization {
  public static void main(String[] args) {
    House h = new House();
    h.f(); // Shows that construction is done
  }
} /* Output:
Window(1)
Window(2)
Window(3)
House()
Window(33)
f()
*///:~
```

在类的内部，变量定义的先后顺序决定了初始化的顺序。即使变量的定义散布于方法定义之间，它们仍旧会在任何方法（包括构造器）被调用之前得到初始化。

### 5.5 静态数据的初始化

无论创建多少个对象，静态数据都只占用一份存储区域。

static关键字不能应用于局部变量，因此它只能作用于域。

```java
//: initialization/StaticInitialization.java
package initialization; /* Added by Eclipse.py */
// Specifying initial values in a class definition.
import static net.mindview.util.Print.*;

class Bowl {
  Bowl(int marker) {
    print("Bowl(" + marker + ")");
  }
  void f1(int marker) {
    print("f1(" + marker + ")");
  }
}

class Table {
  static Bowl bowl1 = new Bowl(1);
  Table() {
    print("Table()");
    bowl2.f1(1);
  }
  void f2(int marker) {
    print("f2(" + marker + ")");
  }
  static Bowl bowl2 = new Bowl(2);
}

class Cupboard {
  Bowl bowl3 = new Bowl(3);
  static Bowl bowl4 = new Bowl(4);
  Cupboard() {
    print("Cupboard()");
    bowl4.f1(2);
  }
  void f3(int marker) {
    print("f3(" + marker + ")");
  }
  static Bowl bowl5 = new Bowl(5);
}

public class StaticInitialization {
  public static void main(String[] args) {
    print("Creating new Cupboard() in main");
    new Cupboard();
    print("Creating new Cupboard() in main");
    new Cupboard();
    table.f2(1);
    cupboard.f3(1);
  }
  static Table table = new Table();
  static Cupboard cupboard = new Cupboard();
} /* Output:
Bowl(1)
Bowl(2)
Table()
f1(1)
Bowl(4)
Bowl(5)
Bowl(3)
Cupboard()
f1(2)
Creating new Cupboard() in main
Bowl(3)
Cupboard()
f1(2)
Creating new Cupboard() in main
Bowl(3)
Cupboard()
f1(2)
f2(1)
f3(1)
*///:~
```

初始化的顺序：

（1）静态对象

（2）非静态对象

## 6 访问权限控制

## 7 复用类

### 7.1 初始化基类

当创建一个导出类的对象时，该对象包含了一个基类的子对象，这个子对象与你用基类直接创建的对象是一样的，二者区别在于，后者来自于外部，而基类的子对象被包装在导出类对象内部。

```java
//: reusing/Cartoon.java
package reusing; /* Added by Eclipse.py */
// Constructor calls during inheritance.
import static net.mindview.util.Print.*;

class Art {
  Art() { print("Art constructor"); }
}

class Drawing extends Art {
  Drawing() { print("Drawing constructor"); }
}

public class Cartoon extends Drawing {
  public Cartoon() { print("Cartoon constructor"); }
  public static void main(String[] args) {
    Cartoon x = new Cartoon();
  }
} /* Output:
Art constructor
Drawing constructor
Cartoon constructor
*///:~
```

构建过程从基类"向外"扩展，所以基类在导出类构造器可以访问它之前，就已经完成了初始化。

即使你不为Cartoon()创建构造器，编译器也会为你合成一个默认的构造器，该构造器将调用基类的构造器。

### 7.2 final关键字

#### 7.2.1 final数据

final数据的 使用场景：

- （1）一个永不改变的编译时常量
- （2）一个在运行时被初始化的值，而你不希望它被改变

**一个既是static又是final的域只占据一段不能改变的存储空间。**

 final数据的特点：**定义为static，说明强调只有一份；定义为final，则说明它是一个常量。**

带有**final static**基本类型全部用大写字母命名，并且字与字之间用下划线隔开。

final数据代码案例：

```java
//: reusing/FinalData.java
package reusing; /* Added by Eclipse.py */
// The effect of final on fields.
import java.util.*;
import static net.mindview.util.Print.*;

class Value {
  int i; // Package access
  public Value(int i) { this.i = i; }
}

public class FinalData {
  private static Random rand = new Random(47);
  private String id;
  public FinalData(String id) { this.id = id; }
  // Can be compile-time constants:
  private final int valueOne = 9;
  private static final int VALUE_TWO = 99;
  // Typical public constant:
  public static final int VALUE_THREE = 39;
  // Cannot be compile-time constants:
  private final int i4 = rand.nextInt(20);
  static final int INT_5 = rand.nextInt(20);
  private Value v1 = new Value(11);
  private final Value v2 = new Value(22);
  private static final Value VAL_3 = new Value(33);
  // Arrays:
  private final int[] a = { 1, 2, 3, 4, 5, 6 };
  public String toString() {
    return id + ": " + "i4 = " + i4 + ", INT_5 = " + INT_5;
  }
  public static void main(String[] args) {
    FinalData fd1 = new FinalData("fd1");
    //! fd1.valueOne++; // Error: can't change value
    fd1.v2.i++; // Object isn't constant!
    fd1.v1 = new Value(9); // OK -- not final
    for(int i = 0; i < fd1.a.length; i++)
      fd1.a[i]++; // Object isn't constant!
    //! fd1.v2 = new Value(0); // Error: Can't
    //! fd1.VAL_3 = new Value(1); // change reference
    //! fd1.a = new int[3];
    print(fd1);
    print("Creating new FinalData");
    FinalData fd2 = new FinalData("fd2");
    print(fd1);
    print(fd2);
  }
} /* Output:
fd1: i4 = 15, INT_5 = 18
Creating new FinalData
fd1: i4 = 15, INT_5 = 18
fd2: i4 = 13, INT_5 = 18
*///:~
```

（1）示例部分展示了将final数值定义为静态和非静态的区别，当程序运行时就可以看到这个区别，在fd1和fd2中，i4的值是唯一的，但是INT_5的值是不可能通过创建第二个FinalData对象加以改变的，这是因为它是static的，在装载时已经被初始化，而不是每次创建新对象都被初始化。

（2）v1到VAL_3这些变量说明了final引用的意义，正如在main()中看到的，不能因为v2是final的，就认为无法改变它的值。由于它只是一个引用，final意味着无法将v2再次指向另一个新的对象。这对数组具有同样的意义，数组是另一种引用。

## 8 多态

### 8.1 构造器和多态

只有基类的构造器才具有恰当的知识和权限来对自己的元素进行初始化。因此，必须令所有的构造器都得到调用，否则就不能正确构造完整对象。这也是编译器为什么要强制导出类部分都必须调用构造器的原因。在导出类的构造器主体中，如果没有明确指定调用某个基类构造器，它就会“默默”的调用默认构造器。如果不存在默认构造器，编译器就会报错。

代码示例：

```java
//: polymorphism/Sandwich.java
// Order of constructor calls.
package polymorphism;
import static net.mindview.util.Print.*;

class Meal {
  Meal() { print("Meal()"); }
}

class Bread {
  Bread() { print("Bread()"); }
}

class Cheese {
  Cheese() { print("Cheese()"); }
}

class Lettuce {
  Lettuce() { print("Lettuce()"); }
}

class Lunch extends Meal {
  Lunch() { print("Lunch()"); }
}

class PortableLunch extends Lunch {
  PortableLunch() { print("PortableLunch()");}
}

public class Sandwich extends PortableLunch {
  private Bread b = new Bread();
  private Cheese c = new Cheese();
  private Lettuce l = new Lettuce();
  public Sandwich() { print("Sandwich()"); }
  public static void main(String[] args) {
    new Sandwich();
  }
} /* Output:
Meal()
Lunch()
PortableLunch()
Bread()
Cheese()
Lettuce()
Sandwich()
*///:~
```

## 9 接口

接口和内部类为我们提供了一种将接口与实现分离的更加结构化的方法。

### 9.1 抽象类

包含抽象方法的类叫做抽象类。如果一个类包含一个或者多个抽象方法，该类必须被限定为**抽象**的。

### 9.2 接口

**interface**关键字使抽象的概念更向前迈进一步了。**abstract**关键字允许人们在类中创建一个或多个没有任何定义的方法——提供了接口部分，但是没有提供任何相应的具体实现，这些实现是由此类的继承者创建的。

**interface**这个关键字产生一个完全抽象的类，他根本就没有提供任何具体实现，他允许创建者提供方法名、参数列表和返回类型，但是没有任何方法体。接口只提供了形式，而未提供任何具体实现。

### 9.3 策略设计模式

策略设计模式代码示例：

```java
//: interfaces/classprocessor/Apply.java
package interfaces.classprocessor;
import java.util.*;
import static net.mindview.util.Print.*;

class Processor {
  public String name() {
    return getClass().getSimpleName();
  }
  Object process(Object input) { return input; }
}	

class Upcase extends Processor {
  String process(Object input) { // Covariant return
    return ((String)input).toUpperCase();
  }
}

class Downcase extends Processor {
  String process(Object input) {
    return ((String)input).toLowerCase();
  }
}

class Splitter extends Processor {
  String process(Object input) {
    // The split() argument divides a String into pieces:
    return Arrays.toString(((String)input).split(" "));
  }
}	

public class Apply {
  public static void process(Processor p, Object s) {
    print("Using Processor " + p.name());
    print(p.process(s));
  }
  public static String s =
    "Disagreement with beliefs is by definition incorrect";
  public static void main(String[] args) {
    process(new Upcase(), s);
    process(new Downcase(), s);
    process(new Splitter(), s);
  }
} /* Output:
Using Processor Upcase
DISAGREEMENT WITH BELIEFS IS BY DEFINITION INCORRECT
Using Processor Downcase
disagreement with beliefs is by definition incorrect
Using Processor Splitter
[Disagreement, with, beliefs, is, by, definition, incorrect]
*///:~
```

像本例这样，创建一个能够根据所传递的参数对象的不同而具有不同行为的方法，被称为**策略设计模式**。

这类方法包含所要执行的算法中固定不变的部分，而“策略”包含变化的部分。策略就是传递进去的参数对象，它包含要执行的代码。

### 9.4 接口与工厂

接口是实现多重继承的途径，生成遵循某个接口的对象的典型方法就是**工厂方法设计模式**，这与直接调用构造器不同，我们在工厂对象上调用的是创建方法，而该工厂对象将生成接口的某个实现的对象。理论上，通过这种方式，我们的代码将完全与接口的实现分离，这就使得我们可以透明的将某个实现替换为另一个实现。

工厂模式代码示例：

```java
//: interfaces/Factories.java
package interfaces; /* Added by Eclipse.py */
import static net.mindview.util.Print.*;

interface Service {
  void method1();
  void method2();
}

interface ServiceFactory {
  Service getService();
}

class Implementation1 implements Service {
  Implementation1() {} // Package access
  public void method1() {print("Implementation1 method1");}
  public void method2() {print("Implementation1 method2");}
}	

class Implementation1Factory implements ServiceFactory {
  public Service getService() {
    return new Implementation1();
  }
}

class Implementation2 implements Service {
  Implementation2() {} // Package access
  public void method1() {print("Implementation2 method1");}
  public void method2() {print("Implementation2 method2");}
}

class Implementation2Factory implements ServiceFactory {
  public Service getService() {
    return new Implementation2();
  }
}	

public class Factories {
  public static void serviceConsumer(ServiceFactory fact) {
    Service s = fact.getService();
    s.method1();
    s.method2();
  }
  public static void main(String[] args) {
    serviceConsumer(new Implementation1Factory());
    // Implementations are completely interchangeable:
    serviceConsumer(new Implementation2Factory());
  }
} /* Output:
Implementation1 method1
Implementation1 method2
Implementation2 method1
Implementation2 method2
*///:~
```

 

## 10 内部类

内部类：将一个类的定义放在另一个类的定义内部，这就是内部类。

### 10.1 创建内部类

```java
//: innerclasses/Parcel1.java
package innerclasses; /* Added by Eclipse.py */
// Creating inner classes.

public class Parcel1 {
  class Contents {
    private int i = 11;
    public int value() { return i; }
  }
  class Destination {
    private String label;
    Destination(String whereTo) {
      label = whereTo;
    }
    String readLabel() { return label; }
  }	
  // Using inner classes looks just like
  // using any other class, within Parcel1:
  public void ship(String dest) {
    Contents c = new Contents();
    Destination d = new Destination(dest);
    System.out.println(d.readLabel());
  }
  public static void main(String[] args) {
    Parcel1 p = new Parcel1();
    p.ship("Tasmania");
  }
} /* Output:
Tasmania
*///:~
```

### 10.2 为什么需要内部类

内部类使得多重继承的解决方案变得完整，接口解决了部分问题，**而内部类有效实现了“多重继承”，也就是说，内部类允许继承多个非接口类型（类或者抽象类）。**

**如果拥有的是抽象的类或具体的类，而不是接口，那就只能使用内部类才能实现多重继承。**



## 13 字符串

### 13.1 不可变String

String对象是不可变的，String类中每一个看起来可以修改String值的方法，实际上都是创建一个全新的String对象，以包含修改后的字符串内容。



## 15 泛型

泛型实现了参数化类型的概念，使代码可以应用于多种类型。
