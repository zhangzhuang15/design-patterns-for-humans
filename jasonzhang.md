# My Content
## 前言
理解设计模式，必须要结合具体的情景来谈。  
譬如理解物理现象，你要制定一套模型，画出一幅示意图，之后就以这幅图为基础，进行探究。  
空洞的概念，无助于理解设计模式。

<br>

---

## 原则
### 单一职责
一个对象只负责一种功能，功能尽可能专一
### 依赖倒转
依赖抽象，不要依赖具体实现
### 迪米特法则
一个类对其他类的感知尽量要少
### 开闭
欢迎扩展，拒绝修改
### 里氏替换
将代码中的父类对象替换为子类对象，程序依旧可以顺畅执行
### 接口隔离
接口不要定义太多内容，保持接口的单一
### 组合原则


<br>

---

## 创建型模式
这类模式解决的是对象使用和创建之间的耦合。使用这种模式之后，对象使用者不用关心对象的创建细节。好处就是修改创建细节的代码后，使用者一方的代码不用修改。

- 简单工厂模式
- 工厂方法模式
- 抽象工厂模式
- 构建者模式
- 单例模式
- 原型模式

## 结构型模式
这类模式解决的是一个对象使用另一个对象时存在的耦合问题。

此类模式的基本思路就是，在两个对象之间加入一个对象（“脚”），利用这个对象去扩展、封装原对象的特性，或者
将原对象的一些功能放在该对象里实现，然后提供给调用方的对象使用。好处显而易见，一个对象发生变动之后，只有
“脚”变化，调用方代码不需要变动。但是这种模式用多了，中间层的对象就会很多，整体结构变得异常复杂。

根据具体耦合的内容，拆分如下模式：

- 代理模式 -> 扩展原对象
- 装饰器模式 -> 扩展原对象
- 门面模式 -> 封装原对象
- 桥接模式 -> 拆去原对象一部分功能
- 组合模式 -> 封装原对象
- 适配器模式 -> 封装原对象


## 行为型模式
这类模式解决的是对象的行为是如何触发、行为和行为之间怎么关联的。

对象的行为就是对象定义的方法。当对象的方法被调用时，对象就触发了行为。

这类模式就是聚焦对象方法被调用的耦合问题。

- 命令模式 
  > 抽象出一个命令的概念，在命令中调用原对象的方法，原对象的方法是由命令被动调用的，不是主动调用的

- 策略模式
  > 和命令模式一个道理，只是在语义上不同罢了，本质都是一样的

- 迭代器模式
  > 关注的是列表这种对象，聚焦的是它的迭代行为，数据遍历的实现不放在原对象，而是拆出来放在迭代器里面实现

- 责任链模式 
  > 聚焦这种行为表现：一个行为触发之后，会触发下一个行为

- 状态模式 
  > 聚焦这种行为表现：一个行为触发之后，对象整体的所有行为实现发生改变

- 访问者模式 
  > 原对象产生什么行为，由访问者对象决定，访问者里面，决定调用原对象的哪个方法

- 观察者模式 
  > 聚焦这种行为表现：一个对象触发行为之后，若干对象的对象被触发 

- 模版方法模式
  > 聚焦这种行为表现：对象的行为触发顺序固定，内容不固定

- 中间者模式
  > 聚焦这种行为表现：对象触发行为之后，需经过中间传导，触发另一个对象的行为

<br>

---

## 核心要点
各种模式啊，都是具体的套路，使用的时候要灵活，不能机械硬搬，你只要理解原则，按照 原则 具体 
问题具体分析 就可以了。

总结下来，就是以下思路：
- 类的功能要单一、稳定
- 如果要修改\扩展类，优先考虑定义另外一个类去搞，不要在类的内部直接修改
- 尽量使用组合去复用类的功能，而不是继承这个类
- 如果要组合，组合的类尽量少
- 产生依赖的地方，尽量使用抽象的类，比如 abstract class 或者 interface 
- 如果存在 A go with B 的行为，不妨在实现的时候，采用 B go with A 的思路，谁更稳定，就 go with 谁


<br>

---

## 具体模式
### 观察者模式(observer)
>Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
>
>GOF

模型： 观察者，被观察物  
情景： 当被观察物变化时，通知观察者，令观察者做出响应  
实现：   
> 观察者 `订阅` 被观察物, 将自身注册到被观察物的列表中；  
> 当被观察物发生变化时，遍历自己的列表，取出各个观察者，调用它已定义的响应函数。

<br>

### 中介者模式(mediator)
>Promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.
>
>GOF

模型： 中介者， 委托者  
情景： 委托者发送信息给中介者，中介者将信息广播给其它委托者，完成委托者到委托者的通信  
实现：  
> 委托者注册中介者到自身的列表中，与此同时，调用中介者以提供的方法，将自身注册到中介者的列表中。 
>  
> 委托者依次遍历列表中的中介者，调用中介者提供的方法广播要传达的信息，而在该方法中，中介者将遍历列表中的委托者，调用委托者的回调函数，将信息传送给他们。

<br>

### 访问者模式(visitor)
>Allows for one or more operation to be applied to a set of objects at runtime, decoupling the operations from the object structure.
>
>GOF

模型： 被访问者， 访问者   
情景： `访问者` 访问 `被访问者`，遍历其信息  
实现：  
> 被访问者拥有属性在内的诸多信息，这些信息需要遍历；  
>   
> 一般思路是被访问者自身提供一个方法，遍历自己的信息，就像一课二叉树，在自身定义处遍历的方法；
> 
> 但是这里，将交给访问者实现，有助于遍历逻辑的灵活定制

<br>

### 命令模式(command)
> Creates objects which encapsulate actions and parameters.

模型： 命令， 执行者  
情景： 执行者执行一系列命令  
实现：  
> 执行一个命令，就是完成一套动作，于是想到将一套动作封装成命令，作为一个对象来理解。按照面向对象的思路，这套动作要被封装到命令对象的方法当中。当命令对象调用这个方法，对应的那一套动作就会执行。  
> 
> 有了上述基础后，在执行者身上注册若干命令到一个列表中，执行者在执行命令时，就可以遍历列表中的命令对象，调用命令对象封装好的方法，做出动作。

<br>

### 状态模式(state)
>A cleaner way for an object to change its behavior at runtime without resorting to large monolithic conditional statements.
>
>GOF

模型： 事物，状态  
情景： 事物发生变化时，其状态由一阶段转换为另一阶段    
实现：  
> 一般情况下，容易将事物的状态作为事物的一个基础属性理解，落实到数据类型上，可能就是整数、枚举、字符串等较简单的情形，而状态的过渡也会在事物的方法中实现。
>    
>  可在这里，要将`状态`单独提取出来，作为一个`对象`来设计，状态的过渡细节也将实现在`状态对象`自身的方法中，而不是事物的方法中。事物充其量调用`状态对象`的方法，促使其发生状态转化。

<br>

### 备忘录模式(memento)
>Capture an object’s internal state and externalize it so that it can be restored to that state later.
>
>GOF

模型： 管理者，备忘录，备忘者  
情景： 备忘者生成备忘录，将备忘录交付给管理者存储；备忘者想回退时，从管理者获取到最近一次的备忘录，从备忘录中存储的信息里，回退到上一个状态  
实现：  
> 备忘者提供一个方法，根据当前各属性值，生成一个备忘录对象；  
> 备忘者提供一个方法，根据备忘录对象，重置自身的属性值；  
> 备忘者提供一个方法，用于注册管理者；  
> 管理者要提供一些方法，用于存储、删除备忘录；

<br>

### 工厂方法模式(factoryMethod)
>Facilitates the creation of other objects.

模型： 工厂， 目标对象  
情景： 定义一个抽象的工厂类，这个工厂只能生产一个产品。通过继承机制，根据具体需要，创建具体的工厂类，生产产品给用户使用。
例子：
> 定义一个ComputerFactory的抽象类，这个类只能生产电脑，表现在类的product方法上。  
> 实际使用时，定义一个AppleComputerFactory继承ComputerFactory，并实现product方法，就可以生产apple电脑了。也可以定义一个DelComputerFactory继承ComputerFactory,并实现product方法，就可以生产del电脑了。

和简单工厂模式的区别很好理解。简单工厂模式中，一个具体的工厂，生产一个具体的对象。如果要生产另一个对象怎么办呢？
你会想到，在具体工厂里再写一个方法，返回另一个对象不就成了？那对象多了怎么办，你的具体工厂是不是就肿了？这样就违背
了单一职责规则，迪米特法则。其实，你想这样写，就还是简单工厂模式的思路。而工厂方法模式就是，我不是往一个工厂里塞
一个方法了，而是再写一个工厂，在这个工厂里去生产另一个对象。由于多了一个具体的工厂，根据依赖倒转原则，使用的时候，
不能再调用具体工厂名了，而是要调用工厂interface或者工厂抽象类了。

<br>

### 抽象工厂模式(abstractFactory)
>Creates an instance of several families of classes.

模型：抽象工厂，工厂，产品
情景：定义一个抽象的工厂类，这个工厂可以生产多种产品。通过继承机制，根据具体需要，创建具体的工厂类，生产产品给用户使用。
例子：
> 定义一个Factory的抽象类，这个类可以生产电脑和手机，表现在类的getComputer，getPhone方法上。  
> 实际使用时，定义一个AppleFactory继承Factory，并实现getComputer, getPhone方法，就可以生产apple电脑和apple手机了。也可以定义一个GoogleFactory继承Factory，并实现getComputer，getPhone方法，就可以生产google电脑和手机了。

和工厂方法模式的区别。你一定困惑，抽象工厂模式里有 工厂抽象类， 工厂方法里也有，二者有什么区别呢？
区别在于，抽象工厂模式里的工厂，生产多种对象，多个对象之间是配套的。工厂方法里只生产一种对象。这
里边最核心的就是多种对象的配套。

工厂方法模式里，一个工厂生产电脑，另一个工厂生产显示器。

抽象工厂模式里，一个工厂生产苹果电脑和苹果屏幕，另一个工厂生产Dell电脑和Dell屏幕。

<br>

### 建造者模式(builder)
>Solves the problem of telescoping constructor.

模型： 建造者，基础组件  
情景： 建造者对基础组件实行不同的组合，构建不同的对象  
实现：  
> 和工厂方法模式一样，建造者要提供一个目标对象给客户使用；
>   
> 不同的是，目标对象是基于 基础组件 重组构成的，基础组件是固定的； 
>  
> 建造者要提供不同的方法，用于生成不同的目标对象，每个方法中，表现为对基础组件的重组逻辑。

<br>

### 责任链模式(chainOfResponsibility)
> Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.
>
> GOF

模型： 责任者，任务  
情景： 责任者处理任务后，将任务继续传递给下一个责任者处理  
实现： 
> 责任者要提供一个方法，用于注册下一个责任者；   
> 
> 责任者要提供一个方法，入参是任务，方法内完成对任务的处理，以及任务像下一个责任者的派发；  
> 
> 不过，更常见的实现是使用 handler 队列来处理任务。

<br>

### 桥接模式(bridge)  
> decouple an abstraction from its implementation so that the two can vary independently.
> by GOF

模型： 功能对象， 扩展对象  
情景： 有一部分功能，功能对象没有，但是扩展对象有，功能对象要利用扩展对象补充这些功能  
实现：  
> 只需将扩展对象 组合到 功能对象中即可；  
> 功能对象内部保留一个扩展对象类型的成员属性；  
> 这个成员属性，就是桥；  

<br>

### 组合模式(composition)
> lets clients treat individual objects and compositions uniformly.
>
> by GOF

模型： 节点、叶子节点  
情景： 按照树结构的思路处理类似于公司组织结构的问题  
实现：  
> 按照树的思路去设计对象和对象的结构；  
> 节点拥有一个列表，存储子节点；  
> 节点提供一个方法，注册子节点；  
> 叶子节点不包含列表，因为它没有子节点；
> 
> 如果一个事物符合这种树型结构，那么就可以用组合模式去处理这种事物。

<br>

### 代理模式(proxy)
>Provide a surrogate or placeholder for another object to control access to it.
>
>GOF


模型： 代理者，被代理者，调用者   
情景： 调用者不直接访问被代理者，而是通过代理者访问被代理者   
实现：  
> 代理者应保留一个被代理者对象的成员属性；   
> 代理者提供的功能，都是基于被代理者，自身不存在什么独创功能；  
> 代理者可以提供一些数据预处理的功能，将预处理后的数据交由被代理者处理；

<br>

### 门面模式(facade)  
>Substitute the interfaces of a set of classes by the interface of one class. Facade hides implementation classes behind one interface.
>
>by GOF

模型： 门面，子系统功能   
情景： 子系统提供了若干功能，但是它的接口函数不友好，无法直接供给调用者使用，门面对子系统功能做了一层封装，提供更友好的调用接口  

<br>

### 适配器模式(adapter)
> Convert the interface of class into another interface clients expect. Adapter lets class work together that couldn't otherwise because of incompatible interfaces.
>
> By GOF

模型： 原功能对象，适配器   
情景： 调用方按照接口规范使用功能，但是原功能对象的接口不符合规范，此时适配器对原功能对象做一层封装，转换为调用方可接受的接口形式。

<br>

### 享元模式(flyweight)
>Facilitates the reuse of many fine grained objects, making the utilization of large numbers of objects more efficient.
>
>GOF

情景： 已使用过的对象暂存起来，供下一次使用；  
实现：  
>  提供一个对象池；  
>  每次生成一个对象时，先从对象池中取，没有就新建一个，并加入到对象池；

<br>

### 原型模式(prototype)
>It lets you copy existing objects without making your code dependent on their classes.

情景： 提供一个已有对象的完全复制品  
实现：  
> 一定是深拷贝；  
> 复制品的各个属性值和原对象一样；


<br>

### 单例模式(singleton)
>A class of which only a single instance can exist.

情景： 提供一个全局的对象，避免重复创建对象；  
实现： 
> 在类的构造函数中，查询全局的对象是否初始化，如果没有初始化，则
将全局对象初始化返回；如果初始化了，直接返回这个全局对象。
>  
> 注意，在并发情况下会出现错误，要加入双重检测；  

缺点： 对于一些不需要频繁创建和销毁的对象，单例模式降低系统的性能。  