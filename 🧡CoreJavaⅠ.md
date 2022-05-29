输入文件输入输出

```java
Scanner in = new Scanner(Paths.get(""),"UTF-8");
//写入文件
PrintWriter out = new PrinterWriter("","UTF-8");//若不存在则创建文件
```

## LocalDate

输出当月月历 

```java
public class Array_1 {
    public static void main(String[] args){
        LocalDate date = LocalDate.now();
        int month = date.getMonthValue();
        int today = date.getDayOfMonth();

        date =date.minusDays((today-1));//将data设为本月1号
        DayOfWeek weekday = date.getDayOfWeek();
        int value = weekday.getValue();
        System.out.println("Mon Tue Wed Thu Froi Sat Sun");
        for(int i =1;i<value;i++)
            System.out.print("    ");//空4格
        while(date.getMonthValue()==month){
            System.out.printf("%3d", date.getDayOfMonth());
            if(date.getDayOfMonth()==today)
                System.out.print("*");
            else
                System.out.print(" ");
            date = date.plusDays(1);
            if(date.getDayOfWeek().getValue()==1) System.out.println();
        }
        if(date.getDayOfWeek().getValue()!=1) System.out.println();
    }
}
```

## 静态域

静态static只是沿用了c++的说法，静态域称之为类域，属于类，即使没有对象也存在

#### 静态常量

静态常量可以直接通过`类名.常量`获得，比如

```java
Math.PI;
public static final double PI;//在Math类中
```

常用的静态常量还有System.out

```java
public class System{
    public static final PrintStream out = ...;
}
//每个类对象都可以对公有域修改，但公有常量（final 域）没问题
//因此不能将其他打印流赋给它
System.out = new PrintSream();//错误
```

#### 静态方法

不能对对象实施操作，，如`Math.pow()`，不用对象，因此没有隐式参数(this)

#### 工厂方法

静态工厂方法用来构造对象如LocalDate，NumberFormat

```java
NumberFormat currentFormat = NumberFormat.getCurrcyInstance();
NumberFormat percentFormat = NumberFormat.getPercentInstance();
double x = 0.1;
sout(currentFormat.format(x));// $0.10
sout(percentFormat.format(x));// 10%
//为什么不用构造方法呢：
//		无法命名构造器，这里的实例采用的不同名字
//		适用构造器无法改变构造的对象类型
```

#### 方法参数

将参数传递给方法的两种方式：**按值调用**和**按引用调用**

> 按值调用：拷贝一个值
>
> 按引用调用：接受地址

#### 构造器

关键字this引用方法的隐式参数

```java
public Employee(double s){//这是构造方法  Employee(double)
    this("Employee#"+ nextId, s);//调用拎一个构造方法 Employee(String,double)
    nextId++;
}
```

类的初始化有两种初始化数据域的方法

- 在构造器中设置值

- 在声明中赋值

- 还有第三章机制,`初始化块`,只要构造类的对象,这些块就会执行(不常见)

  ```java
  class Employee{
      private static int nextId;
      private int id;
      private String name;
      {//初始化块
          id = nextId;
          nextId++;
      }
      ...;
      public Employee(1);
      public Employee(2);
      //无论用什么构造器,块都会执行
  }
  ```

  #### 对象析构和finalize

  finalize方法将在垃圾回收器清除对象之前调用

  `Runtime.addShutdownHook` 添加关闭钩

## 包,类路径

当了包内含有同一个类时,导入会出现编译错误.

```java
import java.util.*;
import java.sql.*;//错误

//可以直接打全名
java.util.Date deadline = new java.util.Date();
java.sql.Date today = new java.sql.Date();
```

#### 静态导入

```java
import static java.lang.System.*;
//就能使用System类的静态方法和静态域
out.println("");//不必加System.out
```

#### 类路径

java核心技术卷Ⅰ P137

## 继承

#### 超类

子类的方法不能访问超类的私有域，只能通过超类的接口调用，但如果子类和超累的getter方法相同，则需要使用`super`

```java
public double getSalary(){
    double Salary = super.getSalary();
}
```

`super`和`this`不同，`super`不是一个对象的引用。

构造器

```java
public Manager(String name, double salary, int year, int month, int day){
    super(name, salary, year, month, day);//这是调用超类的构造器
    bonus = 0;
}
// super语句必须是子类构造器的第一个语句！
```

如果子类构造器没有调用super语句，则子类构造器会默认调用超类没有参数的构造器，容易出错。

#### 多态

一个对象变量可以指示多种实际类型称为**多态**

在运行时能自动地选择调用哪个方法称为**动态绑定**

```java
for(Employee e :staff){//这里的 e 不仅引用超类的对象，也能引用子类的对象
    ...;
}
```

```java
//可以将一个在子类对象赋给超类变量
Employee e;
e = new Employee();
e = new Manager();
```

```java
//以下为合法的
Manager[] managers = new Manager[10];
Employee[] staff = managers;
```

#### 强制类型转换

将超类转换成子类之前，应该使用`instanceof`检查

```java
if(staff[1] instanceof Manager){
    boss = (Manager) staff[1];
}
```

#### 抽象

只要有一个抽象方法，这个类就是抽象类

可以定义一个抽象类的对象，必须引用非抽象子类的对象：

```java
Person p = new Student("Veu","Science");
```

是否可以省略超类的抽象方法而在子类分别定义呢？

不能，这样无法调用一个同一个方法

```java
Person[] people = new Person[2];
people[1] = new Employee(...);
people[2] = new Student(...);

for(Person p: people)
    sout(p.getDescription())//这样引用p可以调用不同子类的方法
```

#### Object

可以用Object引用所有类型的对象

```java
Object obj = new Employee("Harry");
```

只有基本类型不是对象，如数值、字符、布尔

所有数组类型都扩展了Object类

```java
Employee[] staff = new Employee[10];
obj = staff;
obj = new int[10];//都是可行的
```

Object的**equals方法** ： 用于检测一个对象是否等于另一个对象

本节例子

```java
package com.JavaCore.Extends;
/**
 * @Author: Zhu jinliang
 * @Date: 2022/3/20 - 03 - 20 - 16:31
 * @Description:
 * @Version: 1.0
 */
public abstract class Person {
    private  String name;

    public Person(String name) {
        this.name = name;
    }

    public abstract String getDescription();

    public String getName() {
        return name;
    }
}
```

```java
package com.JavaCore.Extends;
/**
 * @Author: Zhu jinliang
 * @Date: 2022/3/20 - 03 - 20 - 16:33
 * @Description:
 * @Version: 1.0
 */
public class Student extends Person{
    private String major;

    public Student(String name, String major) {
        super(name);
        this.major = major;
    }

    public String getDescription() {
        return "a student major in "+ major;
    }
}
```

```java
package com.JavaCore.Extends;
/**
 * @Author: Zhu jinliang
 * @Date: 2022/3/20 - 03 - 20 - 16:39
 * @Description:
 * @Version: 1.0
 */
public class Employee extends  Person{
    private double salary;

    public Employee(String name, double salary) {
        super(name);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    @Override
    public String getDescription() {
        return String.format("an employee with a salary of $%.2f",salary);//注意格式化输出
    }
}
```

```java
package com.JavaCore.Extends;

/**
 * @Author: Zhu jinliang
 * @Date: 2022/3/20 - 03 - 20 - 16:42
 * @Description:
 * @Version: 1.0
 */
public class PersonTest {
    public static void main(String[] args) {
        Person[] people = new Person[2];
        people[0] = new Employee("Harry",4000);
        people[1] = new Student("Ave","Science");

        for(Person p : people){
            System.out.println(p.getName()+","+p.getDescription());
        }
    }
}
```

```
Harry,an employee with a salary of $4000.00
Ave,a student major in Science

Process finished with exit code 0
```

#### hashCode方法

卷Ⅰ P170  跳过了

#### 泛型数组列表

`ArrayList` 采用**类型参数**的<u>泛型类</u>，采用尖括号

```java
ArrayList<Employee> staff = new ArrayList</*Employee右边参数可省去*/>();
//使用add方法将元素添加到数组列表中
staff.add(new Employee("Harry"));
//数组列表管理着对象引用的一个内部数组。就算add后数组满了，数组列表会创建一个更大的数组，并将所有对象从小数组拷贝到大数组中
//如果确定了大小，可以在填充数组前调用ensureCapacity方法
staff.ensureCapacity(100);
//初始容量可传递给构造器
ArrayLsit<Employee> staff = new ArrayList<>(100);
//size方法返回实际元素数目
staff.size();
```

访问元素采用get和set

```java
//设置第i个元素
staff.set(i, harry);
//!!!!!!!!!!!!!!!!!!!!注意capacity和size的区别
ArrayList<Employee> list = new ArrayList<>(100);//capacity 100, size 0
list.set(0,x);//错误
```

**使用add方法添加新元素，而set是替换以存在元素**

```java
//获取
Employee e = staff.get(i);
//删除
Employee e = staff.remove(n);//且这个位置之后的所有元素向前移动1，数组大小减1
```

#### 对象包装器和自动装箱

基本类型包装成对象：Integer,Long,Float,Double,Short,Byte,Character,Void,Boolean，其中前6个都派生于公共的超类Number

```java
ArrayList<Integer> list = new ArrayList<>();
//每个值包装在对象中，因此效率远低于int[],因此构造小型集合
```

自动装箱：

```java
list.add(3);
//将自动转换成
list.add(Integer.valueOf(3));
```

自动拆箱：

```java
int n = list.get(i);//翻译成
int n = list.get(i).intValue();
```

装箱拆箱是编译器认可的，不是虚拟机。编译器在生成类的字节码时，插入必要的方法调用。虚拟机只是执行字节码

将字符串转化为整型：

```java
int x = Imteger.parseInt(s);//parseInt是 静态方法
```

java是值传递的，包装在包装器中的内容不会变。

#### 参数可变方法

如printf方法

```java
System.out.printf("%d",n);
System.out.printf("wid","sd",a);
//其是这样定义的：
public class PrintStream{
    public PrintStream printf(String fmt, object...args){return format(fmt,args);}//接受格式字符串和对象数组
}
// ... 表示可以接受任意数量的对象
```

自定义：

```java
public static double max(double...values){
    double largest = Double.NEGATIVE_INFINITY;
    for(double v : values) if(v>largest) larget = v;
    return largest;
}//用于若干数值的最大值
```

#### 枚举类

如下：声明定义一个类，刚好有4个**实例**

```java
public enum Size {SMALL, MEDIUM, LARGE, EXTRA_LARGE};
```

比较枚举类型的值时，不要调用equals ，而用==

```java
Size s = Enum.valueOf(Size.class,"SMALL");//所有枚举类都是Enum的子类
//toString 和 valueOf 是互逆的静态方法

//每个枚举类型都有静态values()方法，返回一个包含全部枚举值的数组
Size[] values = Size.values();
//ordinal 方法返回枚举常量的位置
Size.MEDIUM.ordinal();//返回1
```

## 反射

> ```
> 反射核心： 在JVM运行时动态加载或调用方法/访问属性
> 主要用途：开发各类通用框架
> 优点：
> 	可扩展性
> 	类浏览器和可视化开发环境
> 	调试器和测试工具
> 缺点：
> 	性能开销
> 	安全限制
> 	内容暴露
> 	
> ```
>
> 

反射机制用来： 

- 运行时分析类的能力
- 在运行时查看对象，例如，编写一个toString方法供所有类使用
- 实现通用的数组操作代码
- 利用Method对象，这个对象像C++的函数指针

#### Class类

在程序运行期间，Java运行时系统始终为 <u>所有对象</u> 维护一个被称为 **运行时的类型标识**。 这个信息跟踪着每个对象所属的类。 虚拟机利用运行时 <u>类型信息</u> 循着相应的方法执行。，同一个类的所有对象的Class类为同一个。

可以通过专门的Java类访问信息，保存这些信息的类称为Class类。Object类中的getClass()方法返回一个Class类型的实例

```java
Employee e;
...;
Class c1 = e.getClass();
//一个Class对象表示一个特定类的属性，常用的方法getName
sout(e.getClass().getName()+" "+e.getName());
//如果e是雇员，则返回
Employee Harry Hacker
//如果e是经历，则返回
Manager Harry hacker
```

如果类在一个包里，包的名字也作为类的一部分

```java
Random generator = new Random();
Class c1 = generator.getClass();
String name = c1.getName();//  name is set to "java.util.Random"
```

还可以调用静态方法forName 获得类名对应的Class对象

```java
String className = "java.util.Random";
Class c1 = Class.forName(className);//需要类名在字符串中
```

获得Class类对象的第三种方法，

```java
Class c1 = Random.class;
Class c2 = int.class;
Class c3 = Double[].class;
```

**一个Class对象实际上表示一种类型，而类型未必是一种类。例如，int不是类，但int.class 是一个Class类型的对象。**

```java
//Class类实际上是一个类型，如Employee.class 的类型是 Class<Employee>
```

动态地创建一个类的实例：

```java
e.getClass().newInstance();//创建了一个与e对象同类型的实例
//newInstance 调用 默认的构造器（无参），如果没有，则抛出异常
```

将forName 与newInstance一起用，可以根据存储在字符串中的类命创建一个对象

```java
String s = "java.util.Random";
Object m = Class.forName(s).newInstance();
```

#### 捕获异常

```java
try{
    String name = ...;
    Class c1 = Class.forName(name);
    ...;
}catch(Exception e)
{
    e.printStackTrace();
}
```

#### 分析类的能力

P197  API

反射机制最重要的内容——检查类的结构

在`java.lang.reflect`包中有三个类 field , Method , Constructor 分别用于描述类的域、方法和构造器。

- 三个类都有getName方法，用来返回项目名称
- Field类有getType方法，返回描述域所属类型的Class对象
- 三个类都有getModifier方法：  判断 public private final 等信息

```java
//Modifier 类的 isPublic isPrivate isFinal方法判断是否含有public、private、final
//Modifier.toString 方法将修饰符打印出来
```

```java
//示例
package com.JavaCore.Reflection;

import java.util.*;
import java.lang.reflect.*;

/**
 * @Author: Zhu jinliang
 * @Date: 2022/3/22 - 03 - 22 - 8:59
 * @Description:   本例测试Reflect，
 * @Version: 1.0
 */
public class ReflectionTest {
    public static void main(String[] args) {
        String name;
        if(args.length> 0) name = args[0];
        else{
            Scanner in = new Scanner(System.in);
            System.out.println("Enter class name(e.g. java.lang.Date):");
            name = in.next();
        }


        try{
            Class c1 = Class.forName(name);//forName 方法通过字符串获取Class类
            String modifiers =Modifier.toString(c1.getModifiers());//获取modifiers并转化为字符串
            if(modifiers.length()>0) System.out.println(modifiers+" ");
            System.out.println("class "+name);

            printConstructors(c1);
            System.out.println();
            /*printMethod(c1);
            System.out.println();
            printField(c1);
            System.out.println("}");*/
        }
        catch(ClassNotFoundException e){
            e.printStackTrace();
        }
        System.exit(0);
    }
    /**
     * Print all constructors of a class
     * @param cl a class
     */
    public static void printConstructors(Class cl){
        Constructor[] constructors = cl.getConstructors();	//获取所有构造器
        for(Constructor c : constructors){
            String name = c.getName();
            System.out.print("   ");
            String modifiers = Modifier.toString(c.getModifiers());// 获取构造器的modifier
            if(modifiers.length()>0) System.out.print(modifiers+" ");
            System.out.print(name +"(");

            // print parameter types
            Class[] paramTypes = c.getParameterTypes(); //参数类型是Class
            for(int j = 0; j<paramTypes.length;j++){
                if(j>0) System.out.print(",");
                System.out.print(paramTypes[j].getName());
            }
            System.out.println(");");
        }
    }
}

```

```
Enter class name(e.g. java.lang.Date):
java.lang.Double
public final 
class java.lang.Double
   public java.lang.Double(double);
   public java.lang.Double(java.lang.String);
```

#### 运行时使用反射

利用反射机制可以查看在编译时不清楚的对象域

采用 Field 类的 get方法，如果f 是Field的的对象，obj是某个包含 f 域的类的对象，f.get(obj)将返回一个对象，其值为obj域的当前值

```java
Employee harry = new Employee("Harry hacker",35000,10,1,1989);
Class cl = harry.getClass();
Field f = cl.getDeclaredField("name");//实际上，name是私有域，该会抛出IllegalAccessException
Object v = f.get(harry);

//需要调用Field，Method，Constructor对象的setAccessible方法
f.setAccessible(true);
//name 域是一个string，可以作为object返回，但类中的salary域属于double类型，则要调用getDouble方法，此时反射机制会自动将域值打包到对象包装器中，这里打包成Double
f.set(obj , value)可以将obj对象的f域设置成新值。
```

跳过

#### 编写泛型数组代码

`java.lang.reflect` 包的Array类允许动态创建数组

```java
Employee[] a = new Employee[100];
...;
//array is full
a.Arrays.copyOf(a, 2*a.length);//用于扩展已经填满的数组
```

尝试编写一个通用方法：

```java
public static Object[] badCopyOf(object[] a, int newLengh){
    Object[] newArray = new Object[newLength];
    System.arraycopy(a, 0 ,newArrayl, 0, Math.min(a.length, newLength));
    return newArray;
}
```

由于创建使用 `new Object`，其对象数组不能转变为`Employee[ ]`，因此在运行时产生`ClassCastException` 异常。

> Employee[] 可以临时转变为Object[] 再转变为Employee[]
>
> 但是初始是Object[]就无法转变成Employee[]

`java.lang.reflect`的Array类的newInstance静态方法：

```java
Object newArray = Array.newInstance(componentType, newLength);
//通过获取数组长度
Array.getLength(a);
//获取元素类型：
//1.首先获得a数组的类对象
//2.确认它是一个数组
//3.使用Class类的 getComponentType方法确定数组对应类型
```

```java
public static Object goodCopyOf(Object a, int newLength){
    Class cl = a.getClass();
    if(!cl.isArray()) return null;
    Class componentType = cl.getComponentType();
    int length = Array.getLength(a);
    Object newArray = Array.newInstance(componentType, newLength);
    System.arraycopy(a, 0, newArray, 0, Math.min(length,newLength));
    return newArray;
}//这个方法可以扩展任意类型的数组，不仅是对象数组
```

```java
int[] a = (1,2,3,4);
a = (int[]) goodCopyOf(a,10);
```

#### 调用任意方法

卷Ⅰ P206

```java
public class MathodTableTest{
    public static void main(String[] args) throw Excepyion{
        Method suqare = MethodTableTest.class.getMethod("square",double.class);
        Method sqrt = Math.class.getMethod("sqrt",double.class);
        
        printTable(1,10,10,square);
        printTable(1,10,10,sqrt);
    }
    
    public static double square(double x){
        return x*x;
    }
    
    public static void printTable(double form, double to, int n, Method f){
        System.out.println(f);
        double dx = (to-gform)/(n-1);
        for(double x =form;x<=to;x+=dx){
            try{
                double y = (Double) f.invoke(null, x);
                System.out.printf("%10.4f| %10.4f%n",x,y);
            }catch(Exception e){
                e.printStackTrace();
            }
        }
    }
}
```

## 接口

接口的所有方法自动属于public ，域为`public static final`，省略不写

#### 接口

Comparable接口已经改进为泛型

```java
public interface Comparable<T>{
    int compareTo(T other);
}
```

接口不是类，不能通过new来实例化一个接口，但是可以声明接口变量：

```java
Comparable x;
//通过instanceof检查某对象是否实现了接口：
if(anObject instanceof Comparable){}
```

接口也可以扩展：

```java
public interface Moveable{}
//扩展
public interface Powered extends Moveable(){}
//接口中不能包含实例域或静态方法， 但可以包含常量
public interface Powered extends Moveable(){ double SPEED = 100;}
//有些接口没有定义方法，只定义了常量，如SwingConstants
```

每个类只能有一个超类，但可以实现多个接口

##### 静态方法

Java8允许在接口中增加静态方法，但通常的做法是将静态方法放在伴随类中，标准库中的**接口和实用工具类**如：

`Collection/Collections`  或 `Path/Paths`

```java
//Paths类只包含两个工厂方法，由一个字符串序列构造一个文件或目录路径。如
Paths.get("jdk1.8.0","jre","bin");
//在Java8中增加了接口的方法：
public interface Path{
    public static Path get(String first, String... more){
        return FileSystem.getDefault().getPath(first, more);
    }
    ...
}
```

##### 默认方法

可以为接口方法提供一个默认实现，必须用default修饰

```java
public interface Comparable<T>{
    default int compareTo(T other){return 0;}
}
```

声明了默认方法后， 就可以不用在类中实现，如`MouseListener`的所有接口，有时候不需要实现。

默认方法是接口演化的重要用法，当很久以前提供了一个类继承了接口，在Java更新后接口新增了方法，如果不是默认方法，则就会出现编译失败。

**方法冲突**：如果两个接口定义了相同方法或在超类中定义了同名方法，Java的处理规则：

- 超类优先
- 接口冲突：如果多个超接口提供了默认方法，则必须覆盖这个方法

##### Comparator接口

复习如何对一个对象数组排序，使用Comparator接口

##### Arrays.sort方法

> sort()是Java中用来排序的一个方法,在我们专心学习各种经典排序算法的时候,其实在代码中一个sort()就可以解决,并且时间复杂度和空间复杂度相对都不会过高.其实sort()不光可以对数组进行排序,基本数据类型的数组都可以,并且可以实现对对象数组的排序.接下来介绍一下用法.
>
> 1基本数据类型
>
> (1)数字类型:
>
> ```java
>     int[] a = {1, 3, 4, 67, 78, 9, 90, 6, 3, 2};
>     Arrays.sort(a);//对数组进行排序
>     System.out.println(Arrays.toString(a));//遍历并输出整个数组
> ```
> 数字类型很简单了,就是从小到大排序(浮点类型与整形同理),输出结果如下:
>
> [1, 2, 3, 3, 4, 6, 9, 67, 78, 90]
>
> (2)字符串类型:
>
> ```java
>     String[] strArray = new String[]{"Zs","ZA", "aa", "Az","D","w","A","z"};
>     Arrays.sort(strArray);
>     System.out.println(Arrays.toString(strArray));
> ```
> 运行结果如下:
>
> ```
> A, D, Hello, Hello kity, hello, hello kity, w, z
> ```
>
> 对于字符串类型的数组,sort()则是将字符串的开头字母进行排序,排列顺序为:大写在小写前,从A~Z依次往下排,若第一位相同则比较第二位,规则相同,若第三位也相同,依次往下比较.
>
> 还有一种按照字母表排序,忽略大小写的方式
>
> ```java
>     String[] strArray = new String[]{"hello","Hello", "Hello kity", "hello kity","D","w","A","z"};
>     Arrays.sort(strArray ,String.CASE_INSENSITIVE_ORDER);
>     System.out.println(Arrays.toString(strArray));
> ```
> 运行结果如下:
>
> ```
> A, D, hello, Hello, Hello kity, hello kity, w, z
> ```
>
>2.对象数组
> 
>对象怎么进行排序呢?这时候就需要我们自己制定排序规则了(比如说,给student对象排序,是将学号id进行排序),但是如果是每个不同的类型的对象,我们都需要去分析数据,自己手动敲规则的话,过于麻烦.所以我们用到Comparable或者Comparator接口.
>  
>拿Comparator为例,里面有个方法
> 
>int compare(T o1,T o2);
> 
>用法举例说明:
> 
>```java
> public class Student  {
>  private int id;
>     private int age;
>     @Override
>     public String toString() {
>         return "Student{" +"id=" + id +", age=" + age +'}';
>     }
>     public Student(int id, int age){
>         this.id = id;
>         this.age = age;
>     }
>    //通过id排序
>     public static class SortById implements Comparator<Student>{
>         @Override
>      public int compare(Student o1, Student o2) {
>             return o1.id - o2.id;
>         }
>     }
>    //通过age排序
>     public static class SortByAge implements Comparator<Student>{
>         @Override
>      public int compare(Student o1, Student o2) {
>             return o1.age - o2.age;
>         }
>     }
>     public static void main(String[] args) {
>         Student s1 = new Student(11110,13);
>         Student s2 = new Student(11112,12);
>         Student[] ss = {s1, s2};
>         Arrays.sort(ss,new SortById()); //Arrays.sort 传入了实现了Comparator接口的对象
>         for (Student s : ss) {
>             System.out.print(s);
>         }
>         System.out.println();
>         Arrays.sort(ss,new SortByAge());
>         for (Student s : ss) {
>             System.out.print(s);
>         }
>     }
>    }
>    ```
>    
>    运行结果如下:
> 
> ```
>Student{id=11110, age=13}Student{id=11112, age=12}
> Student{id=11112, age=12}Student{id=11110, age=13}
>```
> 
> Conparable原理类似,在这里不做介绍.
> 
> 原理:
>
> 为什么sort()都可以排序呢?而且时间和空间复杂度都还比较优良,有没有人想过sort()里面是怎么实现的呢?
>
> 其实sort()是根据需要排序的数组的长度进行区分的:
>
> 当你的数组长度是小于60的,它会直接进行一个插入排序;
>
> 当长度大于60时,有可能会merge排序或者是quick排序,merge和quick会将整个数组进行划分,进行递归,一旦划分的子数组长度小于60时,将不再递归划分,直接进行插入排序.为什么会这么排序呢?
>
> 原因是,在数据量小的时候.插入排序的常数代价非常低,虽然时间复杂度是O(n平方),但是常数项比较低.此时此刻,在数据量比较小的时候,优势就展现出来了.
>
> 那么问题又来而来,当数据量比较大需要进行划分的时候,什么时候用merge,什么时候用quick呢?
>
> 这就要取决数组的类型了,当是基本数据类型的时候,会用quick,当是对象类型的时候会用merge.
>
> 因为当是基本数据类型的时候不需要考虑稳定性的因素,但是对象类型就要考虑了,因为对象不止用来排序的这一个属性,可能已经在其他属性已经排好序了,在此番排序之后还需要保证数组的稳定性.\
>
> _______________________________________________________________________________________________________________
>
> 以上就是Arrays.sort()的使用方法以及原理
>————————————————
> 版权声明：本文为CSDN博主「小哈灬」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
>原文链接：https://blog.csdn.net/qq_39411607/article/details/80224103

对象克隆跳过

##### lambda表达式

```java
class LengthComparator implements Comparatoe<String>{
    public int compare(String first, String second){
        return first.length() - second.length();
    }
}

//转化为lambda为
(String first, String second) ->
    first.length() - second.length();
//
参数   ->
{...代码块}//必须包含显式的return
```

即使没有参数，也要有空括号

```java
() -> { for(int i =100;i>=0;i--)  System.out.println(i); }
```

如果参数类型可推到出，则可省略

```java
Comparator<String> comp  = (first, second) ->{//参数可不写
    first.length() - second.length();
}
```

如果只有一个参数，且可以推导出，可以省略小括号

```java
ActionListener listener = event ->
    System.out.println("xx");
```

**函数式接口**

对于**<u>只有一个抽象方法的接口</u>**，需要使用这种接口的对象时，就可以提供一个lambda表达式，称为函数式接口

```java
//Arrays.sort方法在对对象数组排序，需要第二个参数传递实例
Arrays.sort(words,
           (first, second)-> first.length() -second.length());
```

提高代码可读性

```java
Timer t = new Timer(1000,event ->
                    {
                        System.out.println("xx");
                        Toolkit.getDefaultToolkit().beep();
                    });
//相比于原来需要创建一个对象，而对象实现接口，再传入Timer参数中
```

Java API在`java.util.function` 定义了许多函数式接口，如 `BiFunction<T,U,R>` 描述了参数为T，U和返回类型R的函数

**方法引用**

`System.out::println` 等价于 `x -> System.out.prinln(x)`

`Math::pow` 等价于 `(x,y) -> Math.pow(x, y)`

如果想对字符串排序，而不考虑字母大小写

```java
Arrays.sort(strings, String::compareToIgnoreCase)
```

采用 :: 操作符分隔方法名与对象名或类名：

- `object :: instanceMethod`
- `Class::staticMethod`
- `Class::instanceMethod`

在前两种，方法引用等价于提供方法参数的lambda表达式。第三种，第一个参数会成为方法的目标，例如 `String::compareToIgnoreCase`等同于 `(x,y) -> x.comparaToIgnoreCase(y)`

**构造器引用**

```java
//假设要将字符串列表转化为Person对象数组，要在各个字符串上调用构造器
ArrayList<String> names = ...;
Stream<Person> stream = names.stream().map(Person::new);
List<Person> people = stream.collect(Collectors.toList());
```

map方法会为各个列表元素调用Person(String)构造器，根据上下文推导选择有String参数的构造器

可以用数组类型建立构造器引用，例如 `int[]::new` 是一个构造器引用，它有一个参数：数组长度，等价与  `x -> new int[x]`

lambda表达式的重点是**延迟执行**

如果要重复一个动作n次，将这个动作和次数重复传递到方法：

`repeat(10,() -> System.out.println("hello"));`

需要选择函数式接口，Runnable

```java
public static void repeat(int n, Runnable action){
    for(int i = 0;i<n;i++) action.run();
}
```

#### 内部类跳过

内部类的对象有一个隐式引用，指向创建它的外部类对象

```java
//由于内部类没有定义构造器，编译器默认生成构造器
public 内部类(外部类  外部类对象){
    ....;
}
//如果要在内部类使用外部域
public class 内部类
{
    public void 方法(){
        if(外部类.this.外部类变量名)
    }
}
//在外部类的作用域外，这样引用内部类
外部类名.内部类名
```

**内部类所有静态域都必须是final**，**且不能有static方法**

跳过

#### 代理跳过

### 异常

常见处理方式

```java
try{
    ...;
}catch (SQLException e){
    throw new ServletEcxeption("database error: "+e.getMessage());
}
```

更好的异常处理方法：让用户抛出子系统中的高级异常，而不会丢失原始异常的细节

```java
try{
    ...;
}catch(SQLException e){
    Throwable  se = new ServletException("database error");
    se.initCause(e);
    throw s;
}
//当捕获到异常时，利用下面语句重新得到原始异常
Throwable e = se.getCause();
```

```java
//如果想先记录再抛出异常
logger.log(level, message, e);
throw e;
```

####  分析堆栈轨迹元素

可以调用Throwable类的printStackTrace

```java
Throwable t = new Throwable();
StringWriter out = new StringWriter();
t.printStackTrace(new PrintWriter(out));
String description = out.toString;
```

一种更灵活的方法使使用`getStackTrace`方法，它会得到`StackTraceElemen`t对象的一个数组

```java
Throwable t= new Throwable();
StackTraceElement[] frames =t.getStackTrace();
for(StrckTraceElement frame:frames){
    //analys frame;
}
```

静态的`Thread.getAllStackTrace`方法，可以产生所有线程的堆栈轨迹

```java
Map<Thread, StackTraceElement[]> map = Thread.getAllStackTraces();
for(Thread t = map.keyset()){
    StackTraceElement[] frames = map.get(t);
    //analyse frames;
}
```

例子

```java
public class StackTraceTest {
    // 阶乘函数
    public static int factorial(int n){
        System.out.println("factorial("+"n"+"):");
        Throwable t = new Throwable();
        StackTraceElement[] frames = t.getStackTrace();
        for(StackTraceElement frame : frames){
            System.out.println(frame);
        }
        int r;
        if(n <= 1) r= 1;
        else r = n *factorial(n-1);
        System.out.println("return " +r);
        return r;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.println("Enter n:");
        int n = in.nextInt();
        factorial(n);
    }
}
```

```
Enter n:
4
factorial(n):
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:15)
com.JavaCore.Exception.StackTraceTest.main(StackTraceTest.java:31)
factorial(n):
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:15)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.main(StackTraceTest.java:31)
factorial(n):
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:15)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.main(StackTraceTest.java:31)
factorial(n):
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:15)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.factorial(StackTraceTest.java:22)
com.JavaCore.Exception.StackTraceTest.main(StackTraceTest.java:31)
return 1
return 2
return 6
return 24
```

#### 断言

如果要执行`double y = Math.sqrt(x)` 如果需检查x不为负，添加异常抛出 

`if(x< 0) throw new IllegalArgumentException("x<0");`

持续含有大量检查会导致速度变慢。

**断言机制允许在测试期间向代码插入检查语句，而代码发布时这些语句会自动移走**，使用关键字assert

assert对条件进行检测，如果结果为false，则抛出`AssertionError`异常

要断言x是非负数值：  `assert x>=0;`

或者将x的实际值传递给AssertionError对象，从而在后面显示出来：  `assert x >=0 : x;`

启用和禁用断言不需要编译，这是类加载器的功能。

断言检测只用于开发和测试阶段。

#### 记录日志

##### 基本日志

使用全局日志记录器（global logger）并调用info方法

```java
Logger.getGlobal().info("File->Open menu item selected");
```

在main调用`Logger.getGlobal().setLevel(Level.OFF);`会取消所有的日志

##### 高级日志

不要将所有日志记录到一个全局日志记录器中，可以定义记录器

调用getLogger 方法创建或获取记录器：

```java
private static final Logger myLogger = Logger.getLogger("com.mycompany.myapp");
//未被任何变量引用的日志记录器可能会被垃圾回收，需要像上面一样用一个静态变量存储记录器的一个引用。
```

记录日志的常见用途是记录不可预料的异常

```java
void throwing(String className, String methodName, Throwable t);
void log(level 1, String message, Throwable t);
//典型用法是
if(...){
    IOException exception = new IOException("...");
    logger.throwing("com.mycompany.mylib.reader", "read", exception);
    throw exception;
}
```

##### 后续跳过

不一定需要捕获异常来生成堆栈轨迹，只需调用以下语句

`Thread.dumpStack();`

也可利用它 printStackTrace(PrintWriter s) 方法将它发送到一个文件中。像记录或显示堆栈轨迹，可以采用下面的方式，将它捕获到字符串中：

```java
StringWriter out = new StringWriter();
new Throwable().printStackTrace(new PrintWriter(out));
String description = out.toString();
```

## 泛型程序设计

> ```
> 泛型：即“参数化类型”
> 泛型只在*编译*阶段有效
> 泛型通配符：  ？
> 	不能用作参数变量，即 ? t = p.getT();
> 	上界：<? extends 实参>
> 	下界：<? super 实参>
> ```

#### 泛型方法

```java
class ArrayAlg{
    public static <T> T getMiddle(T... a){//public static 类型变量 返回类型 方法名
        return a[a.length/2];
    }
}
//调用：
String middle = ArrayAlg.<String>getMiddle("Hof","T","goss");//一般可省略 <String>
```

#### 类型变量的限定

例子：需要计算数组中最小元素

```java
class ArrayAlg{
    public static <T> T min(T[] a){//有点小错
        if(a==null||a.length==0) return null;
        T smallest = a[0];
        for(int i = 1;i<a.length;i++)
            if(smallest.compareTo(a[i])>0) smallest = a[i];
        return smallest;
    }
}
//类型 T 说明它可以是任何一个类的对象，但是在函数中用到了compareTo方法，
//因此需要限制 T 具有compareTo方法：
 	public static <T extends Comparable> T min(T[] a){}
```

例子：返回数组中的最大最小值

```java
class ArrayAlg{//返回pair<T>
    public static <T extends Comparable> Pair<T> minmax(T[] a){
        if (a==null||a.length==0) return null;
        T max = a[0];
        T min = a[0];
        for(int i = 1; i<a.length;i++){
            if(max.compareTo(a[i])<0) max = a[i];
            if(min.compareTo(a[i])>0) min = a[i];
		}
        return Pair<>(min,max);
    }
}
```

#### 泛型代码和虚拟机

跳过

## 集合

#### Collection接口

两个基本方法：

```java
public interface Collection<E>{
    boolean add(E element);
    Iterator<E> iterator();
    ...
}
```

#### Iterator接口

```java
public interface Iterator<E>{
    E next();
    boolean hasNext();
    void remove();
    default void forEachRemaining(Consumer<? super E> action);
}
```

使用：

```java
Collection<String> c = ...;
Iterator<String> iter = c.iterator();
//建议使用增强for
for(String element : c){
    ...;
}
```

在1.8中，可不用写循环，调用forEachRemaining 方法并提供lambda 

```java
iterator.forEachRemaining(element -> ...);
```

注意Vector：Vector是同步的，可以由两个线程访问一个Vector对象，但是只有一个线程时会耗费大量时间在同步上，因此选择ArrayList。

#### 映射

更新映射项：

```java
//当想记录出现的词的次数
counts.put(word, counts.get(word)+1);
//但是第一次会Null Pointer Exception 异常，因此使用getOrDefault方法
counts.put(word, counts.getOrDefault(word,0)+1);
//还有  putIfAbsent方法
counts.putIfAbsent(word,0);
//更好的方法，merge方法可以简化
counts.merge(word, 1, Integer::sum);
```

##### 视图

三种视图，键集，值集，键值对集

> `Set<K> keySet()`
>
> `Collection<V> values()`
>
> `Set<Map.Entry<K,V>> entrySet()`

```java
//可以枚举一个映射的所有键
Set<String> keys = map.keySet();
for( String key:keys)
    ...;
```

```java
//如果想查看键和值，通过枚举条目来避免查找值
for(Map.Entry<K,V> entry : staff.entrySet()){
    K k = entry.getKey();
    V v = entrty.getValue();
    ...;
}
//如今有更高效的方法
counts.forEach((k,v)->{
    ...;
})
```

P380跳过

## 10-12跳过

## 部署跳过

创建JAR文件（jdk/bin）通过常用命令格式

清单文件(manifest.MF)

```java
import javax.swing.*;
import java.awt.*;
import java.net.*;
import java.io.*;
import java.util.*;

/**
* @Author: Zhu jinliang
* @Date: 2022/4/8 - 04 - 08 - 14:23
* @Description:
* @Version: 1.0
*/public class ResourceTest {
    public static void main(String[] args) {
        EventQueue.invokeLater(()->{
            JFrame frame = new ResourceTestFrame();
            frame.setTitle("ResourceTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }
}

class ResourceTestFrame extends JFrame{
    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 300;

    public ResourceTestFrame(){
        setSize(DEFAULT_WIDTH,DEFAULT_HEIGHT);
        URL aboutURL = getClass().getResource("about.jif");
        Image img = new ImageIcon(aboutURL).getImage();
        setIconImage(img);

        JTextArea textArea = new JTextArea();
        InputStream stream = getClass().getResourceAsStream("about.txt");
        try(Scanner in = new Scanner(stream,"UTF-8")){
            while(in.hasNext())
                textArea.append(in.nextLine()+"\n");
        }
        add(textArea);
    }
}
```

## 并发

### 线程

线程于进程区别：

- 每个进程有自己整套变量
- 线程共享数据，线程更轻量级，通信更高效

注意：用Runnable接口创建一个实例`Runnable r =() ->{ task code};`，再用此创建一个对象`Thread t = new Thread(r);`

​		而不是构建Thread类的子类来定义一个线程，应该要将*并行运行的任务和运行机制**解耦合***

### 同步异常代码

```java
package com.JavaCore.unscynch;

/**
 * @Author: Zhu jinliang
 * @Date: 2022/4/16 - 04 - 16 - 16:18
 * @Description:线程不同步出现问题的实例 的测试
 * @Version: 1.0
 */
public class BankTest {
    public static final int NACCOUNTS = 100;
    public static final double INITIAN_BALANCE = 1000;
    public static final double MAX_AOUNT =1000;
    public static final int DELAY = 10;

    public static void main(String[] args) {
        Bank bank = new Bank(NACCOUNTS,INITIAN_BALANCE);
        for(int i = 0;i<NACCOUNTS;i++){
            int fromAccount = i;
            Runnable r =()->{
                try{
                    while(true){
                        int toAccount = (int) (bank.size()*Math.random());
                        double amount = MAX_AOUNT * Math.random();
                        bank.transfer(fromAccount,toAccount,amount);
                        Thread.sleep((int)(DELAY*Math.random()));
                    }
                }
                catch (InterruptedException e){
					//这里是空的
                }
            };
            Thread t = new Thread(r);
            t.start();
        }
    }
}
```

```java
package com.JavaCore.unscynch;
import java.util.Arrays;

/**
 * @Author: Zhu jinliang
 * @Date: 2022/4/16 - 04 - 16 - 16:18
 * @Description:    线程不同步出现问题的实例
 * @Version: 1.0
 */
public class Bank {
    private final double[] accounts;

    public Bank(int n, double initialBalance){
        accounts = new double[n];
        Arrays.fill(accounts,initialBalance);
    }
    //转账
    public void transfer(int from, int to, double amount){
        if(accounts[from]<amount) return;
        System.out.println(Thread.currentThread());
        accounts[from] -= amount;
        System.out.printf("%10.2f from %d to %d",amount,from,to);
        accounts[to] +=amount;//该操作不是原子操作
        System.out.printf("Total Balance: %10.2f%n",getTotalBalance());

    }
    private Object getTotalBalance() {
        double sum=0;
        for(double a : accounts)
            sum+=a;
        return  sum;
    }
    public int size(){
        return accounts.length;
    }
}
```

运行片段：

```
Thread[Thread-69,5,main]
    166.58 from 69 to 70Total Balance:   99899.28
Thread[Thread-69,5,main]
    781.05 from 69 to 84Total Balance:   99899.28
    100.72 from 14 to 21Total Balance:  100000.00
Thread[Thread-32,5,main]
    329.21 from 32 to 44Total Balance:  100000.00
Thread[Thread-45,5,main]
    970.02 from 45 to 67Total Balance:  100000.00
Thread[Thread-45,5,main]
    187.60 from 45 to 77Total Balance:  100000.00
Thread[Thread-73,5,main]
    250.92 from 73 to 49Total Balance:  100000.00
Thread[Thread-41,5,main]
    531.48 from 41 to 1Total Balance:  100000.00
Thread[Thread-24,5,main]
    566.64 from 24 to 20Total Balance:  100000.00
Thread[Thread-56,5,main]
    323.68 from 56 to 81Total Balance:  100000.00
Thread[Thread-26,5,main]
    265.86 from 26 to 91Total Balance:  100000.00
Thread[Thread-66,5,main]
    203.78 from 66 to 46Total Balance:  100000.00
Thread[Thread-66,5,main]
    843.57 from 66 to 65Total Balance:  100000.00
Thread[Thread-57,5,main]
Thread[Thread-19,5,main]
Thread[Thread-5,5,main]
    297.14 from 5 to 52Total Balance:   99592.80
    219.22 from 19 to 99Total Balance:   99812.02
Thread[Thread-63,5,main]
    851.85 from 63 to 50Total Balance:   99812.02
Thread[Thread-31,5,main]
    993.25 from 31 to 88Total Balance:   99812.02
Thread[Thread-31,5,main]
    156.27 from 31 to 56Total Balance:   99812.02
Thread[Thread-53,5,main]
    177.10 from 53 to 47Total Balance:   99812.02
Thread[Thread-71,5,main]
      1.63 from 71 to 37Total Balance:   99812.02
Thread[Thread-20,5,main]
    463.60 from 20 to 29Total Balance:   99812.02
Thread[Thread-78,5,main]
    490.19 from 78 to 17Total Balance:   99812.02
Thread[Thread-84,5,main]
    644.02 from 84 to 58Total Balance:   99812.02
    187.98 from 57 to 1Total Balance:  100000.00
```

找出问题：问题在于`account[to]+=amount;`不是原子操作

如果我们反编译`Bank.class`，其中`account[to]+=amount;`将会转化为多行字节码，而中断可能会在任意一行。

#### 锁对象

ReentrantLock 保护代码块的基本结构

```java
myLock.lock();
try{
    ...;
}
finally{
    myLock.unlock();
}
```

```java
//实例中
private Lock bankLock = new ReentrantLock();
//在try之前
bankLock.lock();
//添加finally
bankLock.unlock();
```

添加完后运行

```java
Thread[Thread-4,5,main]
    514.67 from 4 to 39Total Balance:  100000.00
Thread[Thread-4,5,main]
    541.84 from 4 to 94Total Balance:  100000.00
Thread[Thread-73,5,main]
    789.71 from 73 to 45Total Balance:  100000.00
Thread[Thread-96,5,main]
    314.98 from 96 to 37Total Balance:  100000.00
Thread[Thread-20,5,main]
    165.19 from 20 to 8Total Balance:  100000.00
Thread[Thread-78,5,main]
    725.58 from 78 to 58Total Balance:  100000.00
Thread[Thread-15,5,main]
    158.01 from 15 to 94Total Balance:  100000.00
Thread[Thread-53,5,main]
     70.25 from 53 to 99Total Balance:  100000.00
Thread[Thread-36,5,main]
    136.01 from 36 to 49Total Balance:  100000.00
Thread[Thread-49,5,main]
    177.36 from 49 to 26Total Balance:  100000.00
Thread[Thread-89,5,main]
    968.83 from 89 to 89Total Balance:  100000.00
Thread[Thread-12,5,main]
    526.71 from 12 to 47Total Balance:  100000.00
Thread[Thread-65,5,main]
    467.34 from 65 to 55Total Balance:  100000.00
Thread[Thread-18,5,main]
    971.08 from 18 to 16Total Balance:  100000.00
Thread[Thread-97,5,main]
    815.17 from 97 to 96Total Balance:  100000.00
Thread[Thread-55,5,main]
     85.70 from 55 to 23Total Balance:  100000.00
Thread[Thread-68,5,main]
     94.35 from 68 to 88Total Balance:  100000.00
Thread[Thread-68,5,main]
```

注意每个Bank对象都有自己的ReentrantLock对象。

锁是**可重入**的，线程可以重复获得已持有的锁

#### 条件对象

细化银行：在账户金额不足时不能转账

```java
if(bank.getBalance(from)>=amount)
    bank.transfer(from, to ,amount);
//错误，有可能在transfer 前中断
```

添加锁

```java
public void transfer(int from,int to, double amount){
    bankLock.lock();
    try{
        while(){
            ..;
        }
    }
    finally{
        bankLock.unlock();
    }
}
//排他性访问，使得其他线程对该账户没有存款机会，
//因此需要引入 条件对象
```

一个锁对象可以拥有一或多个条件对象，用 `newCondition`获得

```java
class Bank{
    private Condition sufficientFunds;
    ...;
    public Bank(){
        ...;
        sufficientFunds = bankLock.newCondition();
    }
}
//如果transfer 方法发现余额不足，将调用 sufficientFunds.await();
```

#### synchronized

每一个对象里都有一个内部锁。使用synchronized关键字声明方法

```java
public synchronized void method()
{
    wait();
    ...;
    notifyAll();
}
```

Bank实例 的synchronized用法

```java
//这是没有保护的转账方法///////////////////////////////////////////////
public void transfer(int from, int to, double amount){
        if(accounts[from]<amount) return;
        System.out.println(Thread.currentThread());
        accounts[from] -= amount;
        accounts[to] +=amount;
    }

//这是采用ReentrantLock////////////////////////////////////////////////////
public void transfer(int from, int to ,double amount) throws InterruptedException{
    bankLock.lock();  		//构造函数中定义 private Lock bankLock;
    try{
        while(account[from]<amount)
            sufficientFunds.await();//构造函数中定义 private Condition sufficientFunds;   创建一个与锁相关的条件对象，将线程放到等待集中
        System.out.println(Thread.currentThread());
        accounts[from] -= amount;
        accounts[to] +=amount;
        sufficientFunds.signAll();//解除该条件的等待集所有线程的阻塞状态
    }finally{
        bankLock.unlock();//
    }
}

//这是采用synchronized 关键字////////////////////////////////////////////////////
public synchronized void transfer(int from, int to, double amount) throws InterruptedException{
    while(account[from]<amount)
        wait();//导致线程进入等待状态直到它被通知，该方法只能在一个同步方法中调用，wait可有参数毫秒数，纳秒数
    accounts[from] -= amount;
    accounts[to] +=amount;
    notifyAll();//
}

```

#### volatile域

> 线程的共享变量存储在主内存中，每个线程可以把变量的副本保存在(私有的)本地内存中，比
> 如机器的寄存器中，而不是直接在主存中进行读写，这就可能造成一个线程在主存中修改了一个
> 变量的值，但是另外一个线程还继续使用它在寄存器中的变量值的拷贝，造成数据不一致
>
> volatile关键字是线程同步的轻量级实现，比synchronized要好。但只能关于修饰变量
>
> volatile不能保证数据原子性，只能保证数据可见性，而synchronized都可以
>
> ```
> 告诉JVM这个变量是共享的，不稳定的，需要在主存中读取
> 防止JVM指令重拍
> ```
>
> 并发编程的三个重要特征：
>
> 1. 原子性：synchronized关键字
> 2. 可见性：volatile关键字
> 3. 有序性：

声明为volatile，编译器和虚拟机就知道该域是可能被另一个线程并发更新的。

```java
//如果一个变量被一个线程设置，被另一个线程查看，可以使用锁：
private boolean done;
public synchronized boolean isDone(){return done;}
public synchronized void setDone(){done = true;}
//可将域声明为volatile
private volatile boolean done;
//注意：该声明不能提供原子性：
public void flip(){done = !done;}//不能保证读取、反转、写入不被中断
```

除非使用volatile域或锁，否则不能从多个线程安全读出一个域。

还有`final`

#### 原子性

`java.util.concurrent.atomic`包中有很多高效的机器级指令来保证原子性，例如 `AtomicInteger`类的方法`incrementAndGet`和`decrementAndGet`以原子方式实现整数自增和自减

```java
public static AtomicLong nextNumber = new AtomicLong();
//
long id = nextNumber.incrementAndGet();//自增1且返回，可保证多个线程并发访问
```

compareAndSet 在书P660，在循环中检查和计算保证安全，在java8中更新：

```java
largest.updateAndGet(x -> Math.max(x, observed));
```

#### 线程局部变量

使用ThreadLocal辅助类提供各自的实例

```java
//要为每一个线程构造一个实例，
public static final ThreadLocal<SimpleDateFormat> dateFormat=
    ThreadLocal.whtiInitial(()-> new SimpleDateFormat("yyyy-MM-dd"));
//要访问具体的格式化方法:
String dateStamp = dateFormat.get().format(new Date());
```

#### 锁测试与超时

线程在调用lock方法来获取另一个线程所持有的锁对象，很可能发生阻塞，应当更谨慎地申请锁。

tryLock 方法视图申请一个锁，在成功获得后返会true：

```java
if(myLock.tryLock()){
    //now the thread own the lock
    try{...;}
    finally{myLock.unLock();}
}else{
    //do something else;
}
```

调用tryLock时，使用参数：

```java
if(myLock.tryLock(100,TimeUnit.MILLISECONDS))...
```

TimeUnit 是枚举类型，取值包括 SECOND、MILLISECONDS、MICROSECONDS、NANOSECONDS

#### 读\写锁

必要步骤

```java
//1.构造一个ReentrantReadWriteLock对象：
private ReentrantReadWriteLock rwl = new ReentrantReadWriteLock();
//2.抽取读锁和写锁
private Lock readLock = rwl.readLock();
private Lock writeLock = rwl.writeLock();
//3.对所有的获取方法加读锁
public double getTotalBalance(){
    readLock.lock();
    try(){}
    finally{readLock.unlock();}
}
//4.对所有的修改方法加写锁
public void trnsfer(){
writeLock.lock();
try(){}
finally{writeLock.unlock();}
}
```

### 阻塞队列

