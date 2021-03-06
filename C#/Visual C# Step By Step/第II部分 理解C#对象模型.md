### 1、 匿名类
- 匿名类只能包含公共字段，字段必须全部初始化，不可以是静态，不能定义任何方法。

### 2、 可空值类型：是它可以容纳值类型的值
- int? i = null;
- 可空类型的Value属性是只读的。可利用这个属性来读取变量的值，但不能修改它。更改可控变量的值要使用普通的赋值语句。

```
static void Main(string args[])
{
    int? i = null;
    if(!i.HasValue)
    {
        i = 99;
    }
    else
    {
        Console.WriteLine(i);
    }
}
```


### 3、 ref和out参数
- ref是把形参用引用类型来传递，但是不能传递没被初始化的形参。
- out用来传递未初始化的形参。

### 4、装箱
- 数据项从栈自动复制到堆。将值赋给object类型的变量。

### 5、拆箱
- 反过来。将引用了已装箱值的object引用强制转换成值类型。

### 6、is和as操作符
- 对对象进行安全的类型转换。
- 用is判断是否合法

### 7、用于初始化枚举字面值的整数值必须是编译时能确定的常量值

### 8、结构
- 结构不能包含显式的无参构造函数，因为编译器始终都会自动生成一个。而在类中，自己没有写，编译器才会自动生成一个。
- 结构不允许在实例字段声明的时候初始化。

### 9、数组
- 数组始终是引用类型，只在栈中分配一块用于存储引用的内存。
- 隐式数组 var names = new[]{"liuwei", "shandongwa"};
- foreach语句是遍历数组的首选方式
- 如果数据在初始化之后便不发生改变，就适合用只读字段来建模。


### 10、参数数组
- 只能为一维数组使用params关键字
- 不是方法签名的一部分
- 不允许为参数数组指定ref或out修饰符
- params数组必须是方法的最后一个参数
- 非params方法总是优先于params方法

### 11、虚方法和重写方法
- 故意设计成被重写的方法称为虚方法virtual
- 派生类用override关键字重写基类的虚方法
- 虚方法不能是私有的
- 虚方法和重写方法的签名必须完全一致
- 只能重写override 虚方法
- 如果派生类不用override关键字声明方法，那就不是重写基类方法，而是隐藏方法。
- 两个方法必须有相同的可访问性。
- 重写方法隐式地称为虚方法，可在派生类中被重写


### 12、理解受保护的访问 protected
- A是B的子类，A能访问B中被保护的成员。A要不是B的子类，就不能。
- 受保护的字段在派生类中实际就是公共字段。


### 13、扩展方法
- 扩展方法允许添加静态方法来扩展现有的类型。引用被扩展类型的数据即可调用扩展方法。
- 只能在静态类中定义扩展方法。


### 14、接口和抽象类
- 接口永远不会包含任何实现。
- 和基类变量能引用派生类对象一样，接口变量也能引用实现了该接口类的对象。
- 当一个类使用两个含有相同方法但是含义并不相同的接口的时候，需要显示实现接口。需要注意的是方法没有用Public标记，在实现接口的类的方法中，方法名的格式为     接口名.方法名。访问这些方法的时候需要通过恰当的接口来引用对象来实现。 因为对象直接点出来的方法不确定是哪个接口的。
- 尽量显式实现接口。


- 为了明确声明不允许创建某各类的实例，必须将那个类显式声明为抽象类。
- 抽象类可以包含抽象方法。
- 抽象方法的适用条件：一个方法在抽象类中提供默认实现没有意义，但又需要继承类提供该方法的实现。

### 15、密封类
- 如果一个类不想作为基类适用，可以使用sealed防止类被用作基类
- 密封类中不能声明任何虚方法。

### 16、垃圾回收
- 销毁对象并将内存归还给堆的过程称为 垃圾回收
- 析构器只适合引用类型，不能指定访问修饰符
- 
- using语句--->以一场安全的方式清理资源
- using语句声明的变量类型必须实现IDisposable接口，接口只包含一个Dispose方法。






