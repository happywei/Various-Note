### 1、 属性
- 既维持了封装性，又能使用字段风格的语法。
- 看起来像字段，用起来像方法。
- 只写get的属性是只读属性。
- 只写set的属性是只写属性。---->适合对密码这样的数据进行保护。
- 只有在结构或类初始化好之后，才能通过该结构或类的属性来赋值。就是说没new之前属性不能用。
- 不能将属性作为ref或out参数值传给方法。字段可以。
- get和set访问器不能获取任何参数。
- 不能声明const属性。
- 
- 对象初始化器。
- 
- 自动属性：定义带有空白get set的     public int Value{get; set;}

### 2、 使用索引器
- 索引器的本质是有参属性，可被视为一种智能数组。
- 索引器使用this关键字取代方法名，每个类或结构只允许定义一个索引器
- 通过索引器访问此类中的数组。
- 
- 使用String.IsNullOrEmpty判断字符串是否空白或包含null值，是测试字符串是否包含值的首选方法。

### 3、 泛型
- C#通过泛型避免进行强制类型转换，增强类型安全性，减少装箱量，并让程序员更轻松第创建常规化的类和方法。
- 泛型类的具体类型版本，如Queue<int> 称为 已构造类型(Constructed type)
- 
- 定义类时，使用where自居指定约束，对泛型类型的类型参数进行限制。
- 
- IComparable接口，包含CompareTo方法
- 创建泛型类
- 创建泛型方法
- 可变性和泛型接口

### 4、协变性和逆变性--->方便对类型层次结构进行操作

- 协变性：对于泛型接口定义的方法，如果类型参数(T)只在方法的返回值中出现，就可明确地告诉编译器一些隐式转换是合法的，没有必要再强制严格的类型安全性，为此，要在声明类型参数时指定out关键字。这个功能称为协变性Covariance。 
- 只要存在从类型A到类型B的有效转换，或者类型A派生自类型B，就可以。
- 只有作为方法返回类型指定的类型参数才能使用out限定符。用类型参数指定方法的任何参数类型时，使用out限定符就是非法的。另外，协变性只适合引用类型，因为值类型不能建立继承层次结构。
- 定义协变接口：为协变类型参数指定out限定符。协变量泛型类型参数只能出现在输出位置，比如作为方法的返回类型。不能作为方法的参数类型。
- 
- 逆变性Contravariance
- 定义逆变接口：为逆变类型参数指定in限定符。你变量泛型类型参数只能出现在输入位置，比如作为方法的参数。不能作为方法的返回类型。
- 
- 协变性：如果泛型接口中的方法能返回字符串，他们也能返回对象。（所有字符串都是对象）
- 逆变性：如果泛型接口中的方法能获取对象参数，他们也能获取字符串参数（对象能执行的操作字符串也能；所有字符串都是对象。）

### 5、 使用集合

#### 几个比较常用的集合：


---

##### List<T>:类似数组，但提供了其他方法来搜索和排序
- 使用Remove删除指定元素，RemoveAt删除指定位置的项，
- 使用Add在集合尾部添加元素，
- 使用Insert方法在集合中部插入元素，
- 使用Sort方法排序。

---


##### Queue<T>: 队列
- Enqueue入队，Dequeue出队。

---

##### Stack<T>: 栈，后进先出
- push入栈，pop出栈

---

##### LinkedList<T>: 双向链表，可以作为队列，也可以作为栈，还能像列表一样支持随机访问。
- 列表中的每一项除了容纳数据项的值，还容纳了对下一项的应用(Next属性)以及对上一项的引用(Previous属性)，第一项的previous为Null，最后一项的Next为null。
- AddFirst方法，在表头插入元素，下移第一项并将他的Previous属性设置为对新项的引用。
- AddLast方法，在表尾插入元素，将原最后一项的Next指向新项。
- AddBefore方法和AddAfter方法在获取项之后，在指定项的前后插入元素。
- First属性返回对LinkedList<T>集合第一项的引用。
- Last属性返回最后一项的引用。
- 为了遍历链表，可以从它的任何一端开始，查询Next或Previous引用，直到返回Null为止。
- 还可以使用foreach语句正向遍历LinkedList<T>对象，抵达末尾会自动停止。
- Remove, RemoveFirst, RemoveLast方法来删除项。

---

##### HashSet<T>: 无序值列表，为快速数据获取而优化。提供了面向集合的方法来判断他容纳的项是不是另一个HashSet<T>对象中的项的自己，以及计算HashSet<T>对象的交集和并集
- 专为集合操作优化，操作包括设置成员和生成并集/交集等。
- Add插入，Remove删除
- IntersectWith 修改HashSet<T>集合来生成与另一个HashSet<T>相交的新集合。
- UnionWith 合并的新集合
- ExceptWith 不包含其数据项的新集合。
- IsSubsetOf, IsSupersetOf, IsProperSubsetOf, IsProperSupersetOf 判断一个HashSet<T>集合的数据是偶是另一个HashSet<T>集合的超集或者子集
- HashSet<T>集合内部作为哈希表实现，可实现数据项的快速查找。但是，一个大的HashSet<T>集合可能需要消耗大量内存。

---



##### Dictionary<TKey, TValue>: 字典集合允许根据键而不是索引来获取值。
- Dictionary维护两个数组来实现关联数组的功能，一个keys数组容纳要从其映射的键，另一个values容纳映射到的值。在Dictionary<TKey, TValue>集合中插入键值对时，将自动记录那个键和哪个值相关联，从而允许开发人员快速和简单地获取具有指定键的值。
- Dictionary<TKey, TValue>不能包含重复的键。使用Add方法添加会抛出异常。但是使用方括号记号法来添加键值对就不会抛出异常，新的值会覆盖旧的值。
- ContainKey方法测试Dictionary<TKey, TValue>集合是否已包含特定的键。
- Dictionary<TKey, TValue>集合内部采用一种稀疏数据结构，在有大量的内存可用时才最高效。
- 使用foreach遍历Dictionary<TKey, Tvalue>集合返回一个KeyValuePair<TKey, TValue>。该结构包含数据项的键和值拷贝，可通过Key和Value属性访问每个元素，元素是只读的，不能用他们修改Dictionary<TKey, TValue>集合中的数据。


---


##### SortedList<TKey, TValue>: 键/值对的有序列表，必须实现IComparable<T>接口根据Key排好序


### 6、 Lambda表达式
- Lambda表达式只包含参数列表和方法主体，没有定义方法名和返回类型。

### 7、 数组和集合的比较	
- 数组使固定大小，集合可变。
- 数组可以使多维的，集合是线性的。集合中的项可以使集合自身，所以可以来模拟多维数组。
- 数据中的项通过索引来存储和获取。
- 许多集合类都提供了ToArray方法，能创建数组并用集合中的项来填充。复制到数组的项不从集合中删除。另外，这些集合还提供了直接从数组填充集合的构造器。

### 8、 枚举集合

- 可枚举的集合，也就是实现了System.Collections.IEnumerable接口的集合，才能用foreach来遍历。
- IEnumerable接口包含了GetEnumerator方法，方法返回了实现了System.Collections.Ienumerable接口的枚举器对象。枚举器对象用于遍历（枚举）集合中的元素。
- 可将枚举器想象成指向列表中的元素的指针。指针最开始指向第一个元素之前的位置。调用MoveNext方法，如果能实际地移到下一项，MoveNext方法返回true。可用Current属性访问当前指向的那一项；使用Reset方法，则可使指针回到列表第一项之前的位置。使用集合的GetEnumerator方法来创建枚举器，然后反复调用MoveNext方法，并获取Current属性的值，就可以每次在该集合中移动一个元素的位置。这正事foreach语句所做的事情。
- 所以，要自己创建可枚举集合类，就必须实现IEnumerable接口。还要提供IEnumerator接口的一个实现，以便由集合类的GetEnumerator方法返回。
- IEnumerator<T>接口和IEnumerator接口相比，不包含Reset方法，但是扩展了IDisposable接口。

### 9、 迭代器

- 迭代器(iterator)是能生成(yield)已排序值序列的一个代码块。迭代器只是对枚举序列的一个描述。
- yield 关键字指定每一次迭代**要返回的值** ：它临时将方法“叫停”， 将一个值传回调用者。当调用者需要下一个值的时候，GetEnumerator方法就从上次暂停的地方继续，生成下一个值。最终，所有数据都被耗尽，循环结束，GetEnumerator方法终止。迭代过程结束

---

##### 实现IEnumerable<TItem>接口需要实现两个方法
- IEnumerable<T>.GetEnumerator 的泛型版本
- IEnumerable.GetEnumerator 的非泛型版本

---

### 10、 委托 delegate
- 委托是对方法的引用，之所以成为委托，是因为一旦被调用，就“委托”所引用的方法进行处理。将方法引用赋值给委托对象
- 委托和C++的函数指针和类似。但是委托是类型安全的；只能让委托引用与委托签名匹配的方法。尚未引用有效方法的委托是不能调用的。



#### .NET Framework类库的委托例子
- List<T>类的Find和Exist方法，返回匹配项或测试匹配项是否存在
- Average, Max, Min, Count, Sum



#### 声明委托
- 先写关键字delegate， 再写返回类型，在写委托类型的名称，然后在()中添加参数列表
```
delegate void stopMachineryDelegate();
```
- 要使用delegate关键字
- 委托定义了它所引用的方法的“形式”。要指定返回类型，委托名称，以及任何参数。

#### 调用委托
- 使用和调用方法一样的语法。
```
myDelegate del;
...
del();
```



##### 将方法加在委托中，并没有实际调用方法。只需指定方法名，不要包含任何圆括号或者参数。

```
class Controller
{
    private FoldingMachine folder;
    private WeldingMachine welder;
    private PaintingMachine painter;

    //声明委托类型， 
    delegate void stopMachineryDelegate();

    //创建委托实例
    private stopMachineryDelegate stopMachinery;

    public Controller()
    {
        //这句
        this.stopMachinery += folder.StopFolding;
    }
}
```

- 还可以使用new 关键字显式初始化委托，让他引用一个特定的方法。

```
this.stopMachinery = new stopMachineryDelegate(folder.StopFolding);
```


---

### 11、Lambda表达式
- 适配器是指一个特殊方法，他能转换或者说适配一个方法，为他提供不同的签名。


#### Lambda表达式的形式
- 他提供了对函数进行表述的一种表示法。

```
//一个简单表达式，返回参数值的平方。参数x的类型根据上下文推导
x => x * x 

//和上一个一样
x => { return x * x; }

//返回参数值除以2的结果，参数x的类型显式指定
(int x) => x / 2 

//调用一个方法，表达式不获取参数，表达式可能会、也可能不会有返回值
() => folder.StopFolding(0) 

//多个参数；编译器自己推断参数类型
//参数x以值的形式传递
//所以++操作的效果是局部于表达式的
(x, y) => {x++; return x / y;}

//多个参数，都显式指定类型
//参数x以引用的形式传递
//所以++操作的效果是永久性的
(ref int x, int y) => {x++; return x / y;}

```

---

### 12、事件

- 事件：可以定义并捕捉特定的时间，并在发生特定时间时调用委托来进行处理。
- **公共事件**只能由定义它的那个类中的方法引发。在类的外部引发时间会造成编译时错误。

#### 声明事件
- 事件在准备作为事件来源的类中声明。
- **事件来源**类监视其环境，在发生某件事情时引发事件。
- 事件维护这方法列表，引发事件将调用这些方法。有时将这些方法称为**订阅者**。
- 把方法添加到事件中--这个过程称之为**订阅时间**或者**向事件登记**，而不是添加到事件基于的委托中。

##### 声明事件的语法
- 由于时间随同委托使用，所以时间的类型必须是委托，而且必须在声明前附加event前缀。
- 先写关键字event, 再写类型名称(必须是委托类型)， 再写事件名称。
```
event delegateTypeName eventName;

这个更全

delegate void myDelegate();

class MyClass
{
    public event myDelegate MyEvent;
}
```

##### 订阅事件
- 用new操作符创建委托实例(委托具有与事件相同的类型)， 使用+=操作符将委托实例同事件关联

```
class MyEventHandlingClass
{
    private MyClass myClass = new MyClass();
    ...
    public void Start()
    {
        myClass.MyEvent += new myDelegate(this.eventHandlingMethod);
    }
    
    private void eventHandlingMethod(){...}
}

还可以像下面这样直接指定订阅方法，让编译器自动生成新的委托
public void Start()
{
    MyClass.MyEvent += this.eventHandlingMethod;
}
```

##### 引发事件
- 像调用方法那样“调用”事件（在事件名称后面添加一对圆括号）。如果定义事件的委托要求参数，那么还要提供对应的实参。引发事件之前，不要忘记检查事件是否为null

```
class MyClass
{
    public event myDelegate MyEvent;
    ...
    private void RaiseEvent()
    {
        if(this.MyEvent != null)
        {
            this.MyEvent();
        }
    }
}
```

---


































