## 需求
- 参考[《四个程序员的一天》](http://www.cnblogs.com/linkcd/archive/2005/07/19/196087.html)
- 你，一个DotNet程序员，刚刚加入一个新项目组。除了你之外，其他的成员包括：
	- Ceer，一直从事C项目的程序员，他刚刚转入C#不到一个月
	- Jally，整天抱着本Design Pattern（没错，就是GoF的那本）在啃的前Java程序员
	- 以及Semon，你对他完全不了解，只是听PM介绍说他是搞Scheme的
		- 传说中的第二古老的语言LISP的方言之一
		- 不过你也没在意，毕竟计算机这玩意，老东西是不吃香的
- 周一，刚打开电脑，老板就跑到你们组的办公座面前：“好吧，伙计们，现在有个function需要你们来搞定。具体是这样的：用户输入2个数，并输入一个操作符。你根据输入的情况来得出相应的运算结果。“

		Example： Foo(+, 1, 2) = 3; Foo(*, 3, 6) = 18; Foo(/, 2, 4) = 0.5

### C++
- Ceer最先作出反应，简单嘛，判断一下输入的操作符就好了。说着，他很快在白板上写出如下代码：
    
		public class CStyle_Calculator
    	{
    	    static public double Foo(char op, double x, double y)
    	    {
    	        switch(op)
    	            case '+': return x + y; break;
    	            case '-': return x - y; break;
    	            case '*': return x * y; break;
    	            case '/': return x / y; break;
    	            default: throw new Exception(”What the Hell you have input?");
    	    }
    	}

### Java
- Jally只看了一遍，就捂着鼻子连连摇头：好一股的代码臭味。还不如看我用OO的方法来解决

		public interface I操作符 //谁说代码不能写中文的？恩恩
		{
		    double 运算(double x, double y);
		}
		
		public class OO_Calculator
		{
		    private I操作符 m_op;
		    public OO_Calculator(I操作符 op)
		    {
		        this.m_op = op; //依赖注入
		    }
		    
		    public double Foo(double x, double y)
		    {
		        return this.m_op.运算(x, y);
		    }
		}
		
		public class 加法:I操作符
		{
		    public double 运算(double x, double y)
		    {
		        return x + y;
		    }
		}
		
		public class 减法:I操作符
		{
		    public double 运算(double x, double y)
		    {
		        return x - y;
		    }
		}
		
		public class 乘法:I操作符
		{
		    public double 运算(double x, double y)
		    {
		        return x * y;
		    }
		}
		
		public class 除法:I操作符
		{
		    public double 运算(double x, double y)
		    {
		        return x / y;
		    }
		}
		
		public class TheMainClass
		{
		    static public void Main()
		    {
		        I操作符 我的加法 = new 加法();
		        OO_Calculator 我的加法器 = new OO_Calculator(我的加法);
		        double sum  = 我的加法器.Foo(3, 4);
		        System.Console.WriteLine(sum);
		        //sum = 7
		       
		        //其他3个我就不废话了
		    }
		}

### CSharp
- 你看着Jally把白板写得密密麻麻之后，耸耸肩，暗叹，你们这些用java的废柴，就一个运算器还搞出Interface这些东西，烦不烦啊。 让你们见识见识DotNet的强大吧。那个运算符我直接用delegate传进去不就好了么。

		public delegate double TheOperator(double x, double y);
		
		public class Operators
		{
		    static public double Add(double x, double y)
		    {
		        return x + y;
		    }
		    
		    static public double Sub(double x, double y)
		    {
		        return x - y;
		    }
		    
		    //乘，除法 我也懒得废话了
		}
		
		public class DotNet_Calculator
		{
		    public double Foo(TheOperator op, double x, double y)
		    {
		        return op(x, y);
		    }
		}
		
		public class TheMainClass
		{
		    static public void Main()
		    {
		        TheOperator myAdd = new TheOperator(Operators.Add);
		        TheOperator mySub = new TheOperator(Operators.Sub);
		        
		        DotNet_Calculator dc = new DotNet_Calculator();
		        double sum = dc.Foo(myAdd, 2, 4); //sum = 6
		        System.Console.WriteLine(sum);
		        double sub = dc.Foo(mySub, 3, 7); //sub = -4
		        System.Console.WriteLine(sub);
		    }
		}
		//dot net 下面还可以用CodeDom动态构造C＃代码，然后在内存编译运行。
		//如果觉得专门写个Operators很烦的话，可以试试C＃2.0的匿名方法
- 很好，当你写完代码之后，挑衅的看着Jally，Ceer却开始抱怨起来：”这不就是C里面的函数指针么，我也会...“
- “然则DotNet下面的Delegate是类型安全滴...”你继续洋洋得意.

### Scheme
- 而Semon，看了看你们3位华丽的代码，啥也没说，只是在键盘上敲下了2行代码

		(define (Foo op x y)
		    (op x y))
- 然后就下班了...
- scheme的代码稍微解释下：

		(+ 1 2) = 3, (* 3 4) = 12
		// 至于Semon的解法：
		(define (Foo op x y)
		    (op x y))
- 看明白了么，上面的代码只有一个作用：
	- 第一行是函数头，定义了一个叫Foo的函数。该函数接受3个参数op, x, y
	- 第二行定义了函数的行为：把第一个参数op当作运算符，计算后面2个参数
	- 所以：（Foo + 1 2) = 3. (Foo / 12 6) = 2.

### 结论
- 好了好了，不编故事了
	- 我只是想简单的让大家在繁忙的工作之余，也瞅瞅Function Programming世界的美妙
	- 函数编程，最大的特点是它是将函数作为语言里1st class的元素来对待的
	- 一个函数可以接受另一个函数作为参数，也可以把一个函数作为结果来返回
	- 这样的函数我们称为Higher-order function
- 那么，Function Programming和我们传统的面向对象有啥区别捏？
	- 恩，这个嘛，扯得远可以扯到图灵机和冯·诺以曼这2种体系的差异...@_@
	- 不过那个太学术性，俺就不说了。
	- 不过有句话可以较好的概括FP和OO的区别（好吧，这个也是抄“紫皮书”上面的）：

			“Pascal是为了建造金字塔...Lisp是为了建造有机体...”
			“作为Lisp的内在数据结构，表对于这种可用性起着重要的提升作用...”
			“采用100函数在一个数据结构上操作，远远优于采用10个操作在十个数据结构上工作”
			“金字塔矗立在那里千年不变，而有机体则必须演化，否则就会消亡”。
	- 而另一个总结得比较好的话是：（同样是抄来的）
		- 一个对象：一组相同的运算上面，外加不同的数据。（想想你的object，是不是这样的？）
		- 一个Closure：一组相同的数据，外加不同的操作。（Delegate就是这样的思想，有兴趣的话也可以去看看Ruby）
- 基本上，恩，没啥说的了。 
	- 如果你感兴趣的话，可以去看MIT SICP的课程（有在线版的，MIT也作为Open Course开设了的）