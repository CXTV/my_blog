# 初识python中的类与对象

## 一、python中类和对象的概念

类可以比作是某种类型集合的描述。

我们把一类相同的事物叫做类，其中用相同的属性（其实就是变量）描述，里面封装了相同的方法。比如，汽车是一个类，它包括价格、品牌等属性。那么我们需要打印某一辆车的价格和品牌，只需要使用一句代码 print "the car's type ‘ford’,price：280000"，但是当我们需要对一百个品种的车打印这句话的时候，怎么办呢？

```python
#函数实现
def CarInfo(type,price):
     print "the car's type %s,price:%d"%(type,price)
  
CarInfo('passat',250000)
CarInfo('ford',280000)
```

```python
#类实现
class Car:
    def __init__(self,type,price):
        self.type = type
        self.price = price
    def printCarInfo(self):
        print "the car's Info in class:type %s,price:%d"%(self.type,self.price)
 
carOne = Car('passat',250000)
carTwo = Car('ford',250000)
carOne.printCarInfo()
carTwo.printCarInfo()
```

​	把这两段代码都分别拿到python里去执行，我们发现实现的功能是一样的。这说明了什么呢？其实类能实现的功能，函数几乎都可以实现，我们都知道C语言中也是没有对象的，但是它还是很厉害的写出了linux操作系统！！！知道了这一点，我们就知道，类是让我们的程序锦上添花的产物，并没那么可怕。

接下来我们来解析这段内容。

![827651-20151203162301861-1405242489](C:\Users\qa\Desktop\Mds\pic\827651-20151203162301861-1405242489.png)

​	这里结合代码来解释什么叫做类和对象，我们知道，ford和passat都是一种车，不同的车又有不同的品牌、价格。

　　所以在这里，“car”就是“类”，表示“车”这一类事物，它有很多属性，比如型号、价格等等。而passat和ford都是车的一种，它是具体的，有固定的品牌和价格，所以passat是car的一个对象，ford是car的另一个对象。

## 二、python类中的函数和普通函数的对比

​	从刚刚的讲解中，我们知道，类能实现的功能我们用函数也完全可以实现，但是我们可以看到他们的实现方式是不同的，现在我们就逐一对比一下。先上图！![827651-20151203174405330-431400410](C:\Users\qa\Desktop\Mds\pic\827651-20151203174405330-431400410.png)

上图中的printCarInfo和CarInfo两个方法都实现了同样的功能，那么他们的差别在哪里呢？

　　1.我们看到两个方法的缩进不同，printCarInfo这个方法是被包裹在car这个类里面的

　　2.两个函数的参数是不同的，CarInfo方法很直接的传了cartype和price这两个参数，而在printCarInfo方法中只传递了一个self。这也直接导致了后面在函数中使用变量的时候也是不同的。

## 三、python类语法的初识

**使用类中的方法**

CarInfo中的方法我们都知道是什么了，那么printCarInfo里面传递的这个‘self’是个什么鬼？

![827651-20151203180303080-1926710033](C:\Users\qa\Desktop\Mds\pic\827651-20151203180303080-1926710033.png)

　　这里的self就表示对象本身。

​	这里我们再来巩固一下类和对象的概念，car是一个类，它拥有品牌和价格两个属性；passat和ford是两个品牌的车，是车的一种，那么他们就拥有车的属性：品牌和价格，不仅拥有，他们的属性还是具体的、有值的：比如passat的品牌是passat，价格就是250000。

　　所以当我们使用passat这个对象去调用printCarInfo这个方法的时候，其实是做了这样一部操作printCarInfo(passat)，把passat这个对象传给了printCarInfo方法，passat这个对象又包含了两个属性cartype、price，我们在python规定这样使用一个对象中的变量：passat.cartype、passat.price。不要问为什么，这是语法，你这么写python就认识，不这么写它就不认识！

　　此时我们就可以整理一下思路了：我们调用函数时传的passat对象的参数passat.cartype、passat.price被类中printCarInfo函数以self的身份接收，所以我们在使用参数的时候自然就变成了self.cartype、self.price。

**类的初始化**

实例化时先告诉python每个对象对应的属性，我们叫做对象的初始化，如下图：

![827651-20151204140321518-1806784974](C:\Users\qa\Desktop\Mds\pic\827651-20151204140321518-1806784974.png)

其实这两句话每句话都完成了两个功能：

​	第一，从car类中实例化出了一个对象——passat/ford；

​	第二：给新对象的属性赋了值。

```python
#初始化的另一种写法
passat = Car()
passat.cartype = 'passat'
passat.cartype = 250000
```

**类中方法的定义和使用**

![827651-20151204151728596-2119214831](C:\Users\qa\Desktop\Mds\pic\827651-20151204151728596-2119214831.png)

​	我们根据上图来比较，先来看函数的定义，从图中很明显就可以看出，CarInfo中的参数在printCarInfo方法中的换成了self，在方法的调用中，就是用self.属性名来调用了。

​	再来看方法的调用，普通函数的调用直接调用就可以了，而类中的函数调用之前应该先进行类的实例化——创建一个对象，然后给这个对象的属性赋值，然后才可以调用类中的方法，调用方式是 对象名.方法名()。

## 四、类存在的意义及对象的应用

​	我们在本文的开篇就说过，类能实现的功能，用函数也可以实现，那么类的存在还有什么特殊的意义呢？我们都知道函数存在的意义是为了避免代码的重用，我们举个栗子：我有一辆车passat，你有一辆车ford，他们都有计算里程这个功能，因此我们写了一个方法，叫做“DriveDistance”，passat和ford都可以调用它，那么问题来了，我们怎么知道是谁跑了多少里程呢？从函数的角度来讲，我们当然可以自己定义变量来解决这个问题，但是类又是怎么实现的呢？

![827651-20151204165055361-1158833264](C:\Users\qa\Desktop\Mds\pic\827651-20151204165055361-1158833264.png)

​	先看方法的定义，我们看到橘色框框中标出了两个方法的参数不同，现在我们已经知道self是对象，在类方法中，对象是必须的参数，因为我们在之前讲到过，都是使用 对象名.方法名 调用方法，passat.DriverDistance()的意思是DriverDistance(passat),那么 passat.DriverDistance(20)的意思翻译过来就是DriverDistance(passat,20),所以无论如何self参数是必须的，这个记着就行。

​	再来看看类中的实现方式，是用对象原本的dictance加上新参数的dictance，并赋值给了这个对象的dictance属性，因为我们修改的是对象的属性，在其类方法中修改了，我们再使用的时候就是使用了修改后的值。

## 五、内存眼中的类与对象

![827651-20151204175945658-1727788981](C:\Users\qa\Desktop\Mds\pic\827651-20151204175945658-1727788981.png)

![827651-20151204175957455-1056983956](C:\Users\qa\Desktop\Mds\pic\827651-20151204175957455-1056983956.png)

​	看上面的图，上面是代码，下面是执行结果。把能打印的都打印了，我们挑有意义的来说，首先我们看passat，ford初始化之后，我分别打印了两个对象的地址，发现两个对象虽然都是Car实例化的结果，但是实例化之后，都分别有了自己的内存地址，但是在at之前有表明了是car的实例。这说明什么？同一个类实例化出来对象之间的内存是独立的，所以passat.cartype和ford.cartype是两个独立的变量，他们都和自己的对象放在一起，不会混乱。接下来我们来看这两个变量调用方法的地址，我们看到at前面的内容都是一样的，表示是Car类中的printCarInfo方法，而at后面的内容我们仔细对比之后就可以发现是和前面对象的地址一样的，那么这个时候我们就知道，尽管函数我们只定义了一个，但是函数确是和对象绑定的，函数里面用到的参数也是对象地址中存储的参数。