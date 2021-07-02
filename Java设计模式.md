# Java类加载

参考：IT老哥https://segmentfault.com/a/1190000037574626

## 一、简介

jvm的启动是通过启动引导类加载器创建一个初始类来完成，这个类是由jvm的具体实现来指定

![image-20210628163455949](C:\Users\25753\Desktop\image-20210628163455949.png)

### 类加载过程

![image.png](https://segmentfault.com/img/bVcHO1t)

1、加载阶段：通过类的全限定名（全部包名+类名），获取该类的.class文件的二进制字节流，将二进制字节流所代表的静态存储结构转化为方法区运行时的数据结构

2、链接阶段：验证class文件中的信息是否符合当前虚拟机的要求，保证被加载类的正确性，不回危害虚拟机的安全；

 						准备：为类中的静态字段分配内存，并设置默认初始化值

​						 解析：解析阶段将常量池内的符号引用转换成直接引用的过程

3、初始化阶段：初始化是执行类的构造器方法init()过程

### 类加载机制

Java类加载机制为双亲委派机制

![image.png](https://segmentfault.com/img/bVcHO1J)

如果一个类加载器收到加载请求，会把请求委托给父类加载器执行，如果父类加载失败则会向下由子类来尝试加载，如果子类加载失败则会抛出ClassNotFound异常

### 类加载顺序

1. 先执行父类静态代码块和静态变量初始化，静态代码块的执行顺序与代码出现的顺序有关
2. 执行子类的静态代码块和静态变量初始化
3. 执行父类的实例变量初始化
4. 执行父类的构造函数
5. 执行子类的实例变量初始化
6. 执行子类的构造函数

# Java设计模式

参考（感谢）：屌丝码农https://www.cnblogs.com/pony1223/p/7608955.html

​		   				C语言中文网http://c.biancheng.net/view/8385.html

​          				  youlookwhathttps://github.com/youlookwhat/DesignPattern

设计模式是一套反复使用、广泛知晓的代码设计经验总结。它的作用是可重用代码，使代码更容易被他人理解、保证代码可靠性。

设计模式的分类：

（1）创建型模式：对象实例化模式，创建型模式用于解耦对象的实例化过程。（单例模式、工厂方法模式、抽象工厂模式、建造者模式、原型模式）

（2）结构型模式：把类和对象结合在一起形成一个更大的结构。（适配器模式、桥接模式、组合模式、装饰模式、外观模式、亨元模式、代理模式）

（3）行为型模式：类和对象如何交互，及划分责任和算法。（访问者模式、模板模式、策略模式、状态模式、观察者模式、备忘录模式、中介模式、迭代器模式、解释器模式、命令模式、责任链模式）

#### static关键字

一个类中如果有成员变量或者方法被static关键字修饰，那么该成员变量或方法将独立于该类的任何对象。不依赖类特定的实例，被类的所有实例共享，只要这个类被加载，该成员变量或者方法就可以通过类名进行访问，即不用创建对象便可以调用方法或者变量。

## 一、单例模式

一个类只能有一个实例，提供一个全局访问点

### 1、饿汉模式

（1）代码示例：

```java
public class Singleton{
    private Singleton(){}
    private static final Singleton singleton=new Singleton();
    
    public static Singleton getInstance(){
        return singleton;
    }
}
```

实际应用代码：

```java
import java.awt.*;
import javax.swing.*;

public class SingletonEager {
    public static void main(String[] args) {
        JFrame jf = new JFrame("饿汉单例模式测试");
        jf.setLayout(new GridLayout(1, 2));
        Container contentPane = jf.getContentPane();
        Bajie obj1 = Bajie.getInstance();
        contentPane.add(obj1);
        Bajie obj2 = Bajie.getInstance();
        contentPane.add(obj2);
        if (obj1 == obj2) {
            System.out.println("他们是同一人！");
        } else {
            System.out.println("他们不是同一人！");
        }
        jf.pack();
        jf.setVisible(true);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    }
}

class Bajie extends JPanel {
    private static Bajie instance = new Bajie();

    private Bajie() {
        JLabel l1 = new JLabel(new ImageIcon("src/Bajie.jpg"));
        this.add(l1);
    }

    public static Bajie getInstance() {
        return instance;
    }
}
```

（2）优缺点：方式简单，在类加载的时候完成了实例化，避免线程同步问题。

缺点：由于在类加载时就已经实例化，所以当我们不需要用到该实例时，会造成一定程度的内存浪费。



### 2、枚举类型

(1)代码示例：

```java
public enum SingletonEnum{
    instance;
    private SingletonEnum(){
    }
    public void whateverMethod(){
        
    }
}
```

(2)借助JDK1.5中添加的枚举来实现单例模式。不仅能避免多线程同步问题，而且还能防止反序列化重新创建新的对象



### 3、内部类

（1）代码示例：

```java
public class SingletonIn(){
     private SingletonIn(){
     }
    
    private static class SingletonInHodler{
        private static SingletonIn singletonIn=new SingletonIn();
    }
    
    public static Singleton getSingletonIn(){
        return SingletonInHodler.singletonIn;
    }
}
```

(2)内部类是需要在实例化时，调用getInstance方法才会装载；优点是避免了线程不安全，延迟加载，效率高。



### 4、懒汉式

(1)代码示例：

```java
public class SingletonLanHan{
    private SingletonLanHan(){
    }
    private static SingletonLanHan sinletonLanHan;
    
    public static SingletonLanHan getSingletonLanHan(){
        if(singletonLanHan==null){
            sychronized (SingletonLanHan.class){
                if(singletonLanHan == null){
                    singletonLanHan =new SingletonLanHan();
                }
            }
        }
        return singletonLanHan;
    }
}
```

实际应用：利用懒汉式单例模拟产生美国当今总统对象

```java
public class SingletonLazy {
    public static void main(String[] args) {
        President zt1 = President.getInstance();
        zt1.getName();    //输出总统的名字
        President zt2 = President.getInstance();
        zt2.getName();    //输出总统的名字
        if (zt1 == zt2) {
            System.out.println("他们是同一人！");
        } else {
            System.out.println("他们不是同一人！");
        }
    }
}

class President {
    private static volatile President instance = null;    //保证instance在所有线程中同步

    //private避免类在外部被实例化
    private President() {
        System.out.println("产生一个总统！");
    }

    public static synchronized President getInstance() {
        //在getInstance方法上加同步
        if (instance == null) {
            instance = new President();
        } else {
            System.out.println("已经有一个总统，不能产生新总统！");
        }
        return instance;
    }

    public void getName() {
        System.out.println("我是美国总统：特朗普。");
    }
}
```

结果：

```
产生一个总统！
我是美国总统：特朗普。
已经有一个总统，不能产生新总统！
我是美国总统：特朗普。
他们是同一人！
```

(2)保证了:延迟加载和线程安全

## 二、工厂模式

### 1、简单工厂模式（静态工厂模式）

一个工厂类根据传入的参量来决定创建出哪一种产品类的实例；

简单工厂包括角色：工厂角色、抽象产品角色、具体产品角色

实例代码：

抽象产品

```java
//抽象
public abstract class RoujiaMo {

    protected String name;

    /**
     * 准备工作
     */
    public void prepare() {
        Log.e("---RoujiaMo:", name + ": 揉面-剁肉-完成准备工作");
    }

    /**
     * 秘制设备--烘烤2分钟
     */
    public void fire() {
        Log.e("---RoujiaMo:", name + ": 肉夹馍-专用设备-烘烤");
    }

    /**
     * 使用你们的专用袋-包装
     */
    public void pack() {
        Log.e("---RoujiaMo:", name + ": 肉夹馍-专用袋-包装---end");
    }
}

```

具体产品：

```java
//辣味产品
public class ZLaRoujiaMo extends RoujiaMo {

    public ZLaRoujiaMo(){
        this.name = "辣味肉夹馍";
    }
}
```

```java
//酸味产品
public class ZSuanRoujiaMo extends RoujiaMo {

    public ZSuanRoujiaMo() {
        this.name = "酸味肉夹馍";
    }
}
```

```java
//甜味
public class ZTianRoujiaMo extends RoujiaMo {

    public ZTianRoujiaMo() {
        this.name = "甜味肉夹馍";
    }
}
```

工厂

```java

public class SimpleRoujiaMoFactory {

    public RoujiaMo creatRoujiaMo(String type) {
        RoujiaMo roujiaMo = null;
        switch (type) {
            case "Suan":
                roujiaMo = new ZSuanRoujiaMo();
                break;
            case "La":
                roujiaMo = new ZLaRoujiaMo();
                break;
            case "Tian":
                roujiaMo = new ZTianRoujiaMo();
                break;
            default:// 默认为酸肉夹馍
                roujiaMo = new ZSuanRoujiaMo();
                break;
        }
        return roujiaMo;
    }
}
```

```java
public class RoujiaMoStore {

    /**
     * 根据传入不同的类型卖不同的肉夹馍
     */
    /*public RoujiaMo sellRoujiaMo(String type) {

        RoujiaMo roujiaMo = null;
        switch (type) {
            case "Suan":
                roujiaMo = new ZSuanRoujiaMo();
                break;
            case "La":
                roujiaMo = new ZLaRoujiaMo();
                break;
            case "Tian":
                roujiaMo = new ZTianRoujiaMo();
                break;
            default:// 默认为酸肉夹馍
                roujiaMo = new SuanRoujiaMo();
                break;
        }
        roujiaMo.prepare();
        roujiaMo.fire();
        roujiaMo.pack();
        return roujiaMo;

    }*/

    private SimpleRoujiaMoFactory factory;

    public RoujiaMoStore(SimpleRoujiaMoFactory factory) {
        this.factory = factory;
    }

    public RoujiaMo sellRoujiaMo(String type) {

        RoujiaMo roujiaMo = factory.creatRoujiaMo(type);
        roujiaMo.prepare();
        roujiaMo.fire();
        roujiaMo.pack();
        return roujiaMo;

    }

}

```

通过专门定义一个类来负责创建其他类的实例，被创建的实例通常都具有共同的父类。当产品增加时，工厂类也需要修改，违背了开放-封闭原则。

### 2、工厂方法模式

1、模式结构：抽象工厂、具体工厂、抽象产品、具体产品

```java
package FactoryMethod;

public class AbstractFactoryTest {
    public static void main(String[] args) {
        try {
            Product a;
            AbstractFactory af;
            af = (AbstractFactory) ReadXML1.getObject();
            a = af.newProduct();
            a.show();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}

//抽象产品：提供了产品的接口
interface Product {
    public void show();
}

//具体产品1：实现抽象产品中的抽象方法
class ConcreteProduct1 implements Product {
    public void show() {
        System.out.println("具体产品1显示...");
    }
}

//具体产品2：实现抽象产品中的抽象方法
class ConcreteProduct2 implements Product {
    public void show() {
        System.out.println("具体产品2显示...");
    }
}

//抽象工厂：提供了厂品的生成方法
interface AbstractFactory {
    public Product newProduct();
}

//具体工厂1：实现了厂品的生成方法
class ConcreteFactory1 implements AbstractFactory {
    public Product newProduct() {
        System.out.println("具体工厂1生成-->具体产品1...");
        return new ConcreteProduct1();
    }
}

//具体工厂2：实现了厂品的生成方法
class ConcreteFactory2 implements AbstractFactory {
    public Product newProduct() {
        System.out.println("具体工厂2生成-->具体产品2...");
        return new ConcreteProduct2();
    }
}
```

实际应用

```java
package FactoryMethod;

import java.awt.*;
import javax.swing.*;

public class AnimalFarmTest {
    public static void main(String[] args) {
        try {
            Animal a;
            AnimalFarm af;
            af = (AnimalFarm) ReadXML2.getObject();
            a = af.newAnimal();
            a.show();
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}

//抽象产品：动物类
interface Animal {
    public void show();
}

//具体产品：马类
class Horse implements Animal {
    JScrollPane sp;
    JFrame jf = new JFrame("工厂方法模式测试");

    public Horse() {
        Container contentPane = jf.getContentPane();
        JPanel p1 = new JPanel();
        p1.setLayout(new GridLayout(1, 1));
        p1.setBorder(BorderFactory.createTitledBorder("动物：马"));
        sp = new JScrollPane(p1);
        contentPane.add(sp, BorderLayout.CENTER);
        JLabel l1 = new JLabel(new ImageIcon("src/A_Horse.jpg"));
        p1.add(l1);
        jf.pack();
        jf.setVisible(false);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);    //用户点击窗口关闭
    }

    public void show() {
        jf.setVisible(true);
    }
}

//具体产品：牛类
class Cattle implements Animal {
    JScrollPane sp;
    JFrame jf = new JFrame("工厂方法模式测试");

    public Cattle() {
        Container contentPane = jf.getContentPane();
        JPanel p1 = new JPanel();
        p1.setLayout(new GridLayout(1, 1));
        p1.setBorder(BorderFactory.createTitledBorder("动物：牛"));
        sp = new JScrollPane(p1);
        contentPane.add(sp, BorderLayout.CENTER);
        JLabel l1 = new JLabel(new ImageIcon("src/A_Cattle.jpg"));
        p1.add(l1);
        jf.pack();
        jf.setVisible(false);
        jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);    //用户点击窗口关闭
    }

    public void show() {
        jf.setVisible(true);
    }
}

//抽象工厂：畜牧场
interface AnimalFarm {
    public Animal newAnimal();
}

//具体工厂：养马场
class HorseFarm implements AnimalFarm {
    public Animal newAnimal() {
        System.out.println("新马出生！");
        return new Horse();
    }
}

//具体工厂：养牛场
class CattleFarm implements AnimalFarm {
    public Animal newAnimal() {
        System.out.println("新牛出生！");
        return new Cattle();
    }
}
```

```java
package FactoryMethod;
import javax.xml.parsers.*;
import org.w3c.dom.*;
import java.io.*;

class ReadXML2 {
    public static Object getObject() {
        try {
            DocumentBuilderFactory dFactory = DocumentBuilderFactory.newInstance();
            DocumentBuilder builder = dFactory.newDocumentBuilder();
            Document doc;
            doc = builder.parse(new File("src/FactoryMethod/config2.xml"));
            NodeList nl = doc.getElementsByTagName("className");
            Node classNode = nl.item(0).getFirstChild();
            String cName = "FactoryMethod." + classNode.getNodeValue();
            System.out.println("新类名：" + cName);
            Class<?> c = Class.forName(cName);
            Object obj = c.newInstance();
            return obj;
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

（2）优缺点：

1、用户只需要只要知道具体工厂名称就可以得到所要的产品，无需知道产品的具体创建过程

2、典型的解耦框架

缺点：类的个数容易过多，增加了复杂度，并提高了系统的抽象性和理解难度。

### 3、抽象工厂模式

1、抽象工厂模式是工厂方法模式的升级，工厂模式只生产一个类别的产品，而抽象工厂模式可生产多个等级、类别的产品

2、抽象工厂模式的结构：抽象工厂、具体工厂、抽象产品、具体产品

应用实例：

**Fruit(interface):**

```java
public interface Fruit {
    public void get();
}
```

**Apple抽象类:**

```java
public abstract class Apple implements Fruit{
    public abstract void get();
}
```

**ChinaApple类:**

```java
public class ChinaApple extends Apple {

    @Override
    public void get() {
        System.out.println("中国的苹果...");
    }
}
```

创建抽象工厂、具体工厂

**抽象工厂：**

```java
public interface FruitFactory {
    //实例化苹果
    public Fruit getApple();
    //实例化香蕉
    public Fruit getBanana();
}
```

**具体工厂：**

```java
public class ChinaFactory implements FruitFactory {

    @Override
    public Fruit getApple() {
        return new ChinaApple();
    }
    
    @Override
    public Fruit getBanana() {
        return new ChinaBanana();
    }
}
```

**MainClass:**

```java
public class MainClass {

    public static void main(String[] args){
        //创建中国工厂
        FruitFactory chinaFactory = new ChinaFactory();
        //通过中国工厂生产中国苹果实例
        Fruit apple = chinaFactory.getApple();
        apple.get();
        //通过中国工厂生产中国香蕉实例
        Fruit banana = chinaFactory.getBanana();
        banana.get();        
        
        //创建英国工厂
        FruitFactory englandFactory = new EnglandFactory();
        //通过英国工厂生产英国苹果实例
        Fruit apple1 = englandFactory.getApple();
        apple1.get();
        //通过英国工厂生产英国香蕉实例
        Fruit banana2 = englandFactory.getBanana();
        banana2.get();
    }
}
```

## 三、适配器模式

1、概述：适配器模式是将一个类的接口转换成客户希望的另外一个接口，使得原本由于接口不兼容而不能工作的变为可一起工作的类；定义：将一个类的接口转换成客户期望的另一个接口，适配器让原本接口不兼容的类可以相互合作。

 * 如题目，手机充电器一般都是5V左右吧，家用交流电压220V，所以手机充电需要一个适配器

2、适配器模式结构：目标接口，适配者类、适配器类

3、代码示例：

类适配器：

```java
package adapter;
//目标接口
interface Target
{
    public void request();
}
//适配者接口
class Adaptee
{
    public void specificRequest()
    {       
        System.out.println("适配者中的业务代码被调用！");
    }
}
//类适配器类
class ClassAdapter extends Adaptee implements Target
{
    public void request()
    {
        specificRequest();
    }
}
//客户端代码
public class ClassAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("类适配器模式测试：");
        Target target = new ClassAdapter();
        target.request();
    }
}
```



对象适配器：

```java
package adapter;
//对象适配器类
class ObjectAdapter implements Target
{
    private Adaptee adaptee;
    public ObjectAdapter(Adaptee adaptee)
    {
        this.adaptee=adaptee;
    }
    public void request()
    {
        adaptee.specificRequest();
    }
}
//客户端代码
public class ObjectAdapterTest
{
    public static void main(String[] args)
    {
        System.out.println("对象适配器模式测试：");
        Adaptee adaptee = new Adaptee();
        Target target = new ObjectAdapter(adaptee);
        target.request();
    }
}
```

示例2：如题目，手机充电器一般都是5V左右吧，咱天朝的家用交流电压220V，所以手机充电需要一个适配器（降压器）

测试类

```java
public class AdapterActivity extends AppCompatActivity {

    @BindView(R.id.tv_define)
    TextView tvDefine;
    @BindView(R.id.activity_adapter)
    LinearLayout activityAdapter;
    @BindView(R.id.by_adapter)
    Button byAdapter;
    @BindView(R.id.bt_adapter_text)
    Button btAdapterText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_adapter);
        ButterKnife.bind(this);
        setTitle("适配器模式");
        tvDefine.setText(EMTagHandler.fromHtml(AppConstant.ADAPTER_DEFINE));
        btAdapterText.setText("将220V家用电转换为5V");

        btAdapterText.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                /**
                 * 给手机充电
                 */
                Mobile mobile = new Mobile();
                V5Power v5Power = new V5PowerAdapter(new V220Power());
                mobile.inputPower(v5Power);
            }
        });
    }
}
```

```java
public class Mobile {

    // 这里传入的是 v5接口,实现了这个接口的类也可以传入
    public void inputPower(V5Power v5Power) {
        int provideV5Power = v5Power.provideV5Power();
        Log.e("---", "手机(客户端): 我需要的是5V电压充电,现在是" + provideV5Power + "V");
    }
}

```

```java
/**
 * 可以看出，手机依赖一个提供5V电压的接口：
 * 提供5v电压的接口
 */

public interface V5Power {

    public int provideV5Power();
}
```

```java
/**
 * 将200v家用电转换为5v手机用电的适配器
 */

public class V5PowerAdapter implements V5Power {

    private int v220power;

    public V5PowerAdapter(V220Power v220Power) {
        v220power = v220Power.provideV220Power();
    }

    @Override
    public int provideV5Power() {

        Log.e("---", "适配器: 经过复杂的操作,将" + v220power + "v电压转为5v");
        return 5;
    }
}
```

```java
public class V220Power {

    public int provideV220Power() {
        Log.e("---", "现有类: 我们提供的是220v的家用电");
        return 220;
    }
}

```



## 四、代理模式

参考：岑宇http://www.cnblogs.com/cenyu/

1、代理模式定义：由于开发需求，需要给某些对象提供一个代理以控制对该对象的访问。这时访问对象不适合或者不能直接引用目标对象，代理对象作为访问对象和目标对象之间的中介。在代理模式（Proxy Pattern）中，一个类代表另一个类的功能。这种类型的设计模式属于结构型模式。在代理模式中，我们创建具有现有对象的对象，以便向外界提供功能接口。主要解决问题是直接访问对象可能会造成的问题。

（1）优点：

1. 代理模式可以在客户端和目标对象之间起一个中介作用和保护目标对象的作用
2. 代理对象可以扩展目标对象的功能
3. 代理模式能将客户端与目标对象分离，降低了系统的耦合度

（2)缺点:

代理模式会造成系统设计中类的数量增加，提高系统的复杂度

2、代理模式结构：

主要角色：抽象类、真实类、代理类

### 1、静态代理

```java
public class ProxyActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        ActivityProxyBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_proxy);

        setTitle("代理模式");
        binding.tvDefine.setText(EMTagHandler.fromHtml(AppConstant.PROXY_DEFINE));

        // 3. 当被请求时，使用 ProxyImage 来获取 RealImage 类的对象。
        final Image image = new ProxyImage("test_10mb.png");
        binding.btDisk.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 第一次是new的，图像从磁盘加载
                image.display();
            }
        });
        binding.btNoDisk.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // 第二次取缓存，图像不需要从磁盘加载
                image.display();
            }
        });
    }
}

```

接口

```java
 /**
 * 1. 创建一个接口。
 */
public interface Image {
    void display();
}

```

实体类代码

```java
/**
 * 创建实现接口的实体类。
 */
public class ProxyImage implements Image {

    private String fileName;
    private RealImage realImage;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}

```

```java
/**
* 实体类
*/
public class RealImage implements Image {

    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(fileName);
    }

    private void loadFromDisk(String fileName) {
        Log.e("RealImage", "loading " + fileName);
    }

    @Override
    public void display() {
        Log.e("RealImage", "Displaying " + fileName);
    }
}

```

示例代码2：

```
package proxy;

public class ProxyTest {
    public static void main(String[] args) {
        Proxy proxy = new Proxy();
        proxy.Request();
    }
}

//抽象主题
interface Subject {
    void Request();
}

//真实主题
class RealSubject implements Subject {
    public void Request() {
        System.out.println("访问真实主题方法...");
    }
}

//代理
class Proxy implements Subject {
    private RealSubject realSubject;

    public void Request() {
        if (realSubject == null) {
            realSubject = new RealSubject();
        }
        preRequest();
        realSubject.Request();
        postRequest();
    }

    public void preRequest() {
        System.out.println("访问真实主题之前的预处理。");
    }

    public void postRequest() {
        System.out.println("访问真实主题之后的后续处理。");
    }
}
```

### 2、动态代理

1、动态代理对象特点：代理对象不需要实现接口，目标对象应该实现接口。

2、动态代理实现需要使用newProxyInstance方法

```java
static Object newProxyInstance(ClassLoader loader, Class<?>[] interfaces,InvocationHandler h )
```

里面的三个参数含义：

- `ClassLoader loader,`:指定当前目标对象使用类加载器,获取加载器的方法是固定的
- `Class<?>[] interfaces,`:目标对象实现的接口的类型,使用泛型方式确认类型
- `InvocationHandler h`:事件处理,执行目标对象的方法时,会触发事件处理器的方法,会把当前执行目标对象的方法作为参数传入

3、代码示例

```java
/**
 * 创建动态代理对象
 * 动态代理不需要实现接口,但是需要指定接口类型
 */
public class ProxyFactory{

    //维护一个目标对象
    private Object target;
    public ProxyFactory(Object target){
        this.target=target;
    }

   //给目标对象生成代理对象
    public Object getProxyInstance(){
        return Proxy.newProxyInstance(
                target.getClass().getClassLoader(),
                target.getClass().getInterfaces(),
                new InvocationHandler() {
                    @Override
                    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                        System.out.println("开始事务2");
                        //执行目标对象方法
                        Object returnValue = method.invoke(target, args);
                        System.out.println("提交事务2");
                        return returnValue;
                    }
                }
        );
    }

}

```

```java
**
 * 测试类
 */
public class App {
    public static void main(String[] args) {
        // 目标对象
        IUserDao target = new UserDao();
        // 【原始的类型 class cn.itcast.b_dynamic.UserDao】
        System.out.println(target.getClass());

        // 给目标对象，创建代理对象
        IUserDao proxy = (IUserDao) new ProxyFactory(target).getProxyInstance();
        // class $Proxy0   内存中动态生成的代理对象
        System.out.println(proxy.getClass());

        // 执行方法   【代理对象】
        proxy.save();
    }
}
```

### 3、Cglib代理

1、概述：静态代理和动态代理模式都是要求目标对象是实现一个接口的目标对象,但是有时候目标对象只是一个单独的对象,并没有实现任何的接口,这个时候就可以使用以目标对象子类的方式类实现代理,这种方法就叫做:Cglib代理

2、Cglib子类代理实现方法:
1.需要引入cglib的jar文件,但是Spring的核心包中已经包括了Cglib功能,所以直接引入`pring-core-3.2.5.jar`即可.
2.引入功能包后,就可以在内存中动态构建子类
3.代理的类不能为final,否则报错
4.目标对象的方法如果为final/static,那么就不会被拦截,即不会执行目标对象额外的业务方法.

3、代码示例：

```java
/**
 * 目标对象,没有实现任何接口
 */
public class UserDao {

    public void save() {
        System.out.println("----已经保存数据!----");
    }

```

代理工厂

```java
/**
 * Cglib子类代理工厂
 * 对UserDao在内存中动态构建一个子类对象
 */
public class ProxyFactory implements MethodInterceptor{
    //维护目标对象
    private Object target;

    public ProxyFactory(Object target) {
        this.target = target;
    }

    //给目标对象创建一个代理对象
    public Object getProxyInstance(){
        //1.工具类
        Enhancer en = new Enhancer();
        //2.设置父类
        en.setSuperclass(target.getClass());
        //3.设置回调函数
        en.setCallback(this);
        //4.创建子类(代理对象)
        return en.create();

    }

    @Override
    public Object intercept(Object obj, Method method, Object[] args, MethodProxy proxy) throws Throwable {
        System.out.println("开始事务...");

        //执行目标对象的方法
        Object returnValue = method.invoke(target, args);

        System.out.println("提交事务...");

        return returnValue;
    }
}
```

测试类

```java
/**
 * 测试类
 */
public class App {

    @Test
    public void test(){
        //目标对象
        UserDao target = new UserDao();

        //代理对象
        UserDao proxy = (UserDao)new ProxyFactory(target).getProxyInstance();

        //执行代理对象的方法
        proxy.save();
    }
}
```



## 五、观察者模式

参考：码头小渔夫https://www.cnblogs.com/porotin/p/7825656.html

1、概念：对象之间定义了依赖关系，当一个对象改变状态，依赖它的对象会收到通知并自动更新

2、模式角色：抽象被观察者角色、抽象观察者角色、具体被观察者、具体观察者

3、代码示例：

```java
package com.jstao.observer;

/***
 * 抽象被观察者接口
 * 声明了添加、删除、通知观察者方法
 * @author jstao
 *
 */
public interface Observerable {
    
    public void registerObserver(Observer o);
    public void removeObserver(Observer o);
    public void notifyObserver();
    
}
```

```java
package com.jstao.observer;

/***
 * 抽象观察者
 * 定义了一个update()方法，当被观察者调用notifyObservers()方法时，观察者的update()方法会被回调。
 * @author jstao
 *
 */
public interface Observer {
    public void update(String message);
}
```

```java
package com.jstao.observer;

import java.util.ArrayList;
import java.util.List;

/**
 * 被观察者，也就是微信公众号服务
 * 实现了Observerable接口，对Observerable接口的三个方法进行了具体实现
 * @author jstao
 *
 */
public class WechatServer implements Observerable {
    
    //注意到这个List集合的泛型参数为Observer接口，设计原则：面向接口编程而不是面向实现编程
    private List<Observer> list;
    private String message;
    
    public WechatServer() {
        list = new ArrayList<Observer>();
    }
    
    @Override
    public void registerObserver(Observer o) {
        
        list.add(o);
    }
    
    @Override
    public void removeObserver(Observer o) {
        if(!list.isEmpty())
            list.remove(o);
    }

    //遍历
    @Override
    public void notifyObserver() {
        for(int i = 0; i < list.size(); i++) {
            Observer oserver = list.get(i);
            oserver.update(message);
        }
    }
    
    public void setInfomation(String s) {
        this.message = s;
        System.out.println("微信服务更新消息： " + s);
        //消息更新，通知所有观察者
        notifyObserver();
    }

}
```

```java
package com.jstao.observer;

/**
 * 观察者
 * 实现了update方法
 * @author jstao
 *
 */
public class User implements Observer {

    private String name;
    private String message;
    
    public User(String name) {
        this.name = name;
    }
    
    @Override
    public void update(String message) {
        this.message = message;
        read();
    }
    
    public void read() {
        System.out.println(name + " 收到推送消息： " + message);
    }
    
}
```

测试类

```java
package com.jstao.observer;

public class Test {
    
    public static void main(String[] args) {
        WechatServer server = new WechatServer();
        
        Observer userZhang = new User("ZhangSan");
        Observer userLi = new User("LiSi");
        Observer userWang = new User("WangWu");
        
        server.registerObserver(userZhang);
        server.registerObserver(userLi);
        server.registerObserver(userWang);
        server.setInfomation("PHP是世界上最好用的语言！");
        
        System.out.println("----------------------------------------------");
        server.removeObserver(userZhang);
        server.setInfomation("JAVA是世界上最好用的语言！");
        
    }
}
```

