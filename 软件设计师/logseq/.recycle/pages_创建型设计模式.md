- 创建型模式抽象了实例化过程，它们帮助一个系统独立于如何创建、组合和表示它的那些对象。一个类创建型模式使用继承改变被实例化的类，而一个对象创建型模式将实例化委托给另一个对象。
- 随着系统演化得越来越依赖于对象复合而不是类继承，创建型模式变得更为重要。当这种情况发生时，重心从对一组固定行为的硬编码（hard-coding）转移为定义一个较小的基本行为集，这些行为可以被组合成任意数目的更复杂的行为。这样创建有特定行为的对象要求的不仅仅是实例化一个类。
- 在这些模式中有两个不断出现和主旋律。第一，它们都将关于该系统使用哪些具体的类的信息封装起来。第二，它们隐藏了这些类的实例是如何被创建和放在一起的。整个系统关于这些对象所知道的是由抽象类所定义的接口。因此，创建型模式在什么被创建，谁创建它，它是怎样被创建的，以及何时创建这些方面给予了很大的灵活性。它们允许用结构和功能差别很大的“产品”对象配置一个系统。配置可以是静态的（即在编译时指定），也可以是动态的（在运行时）。
- 【例10.8】Singleton模式。
	- 通常情况下，用户可以对应用系统进行配置，并将配置信息保存在配置文件中。应用系统在启动时首先将配置文件加载到内存中，这些内存配置信息应该有且仅有一份。应用单身模式（Singleton）以保证Configure类只能有一个实例。这样，Configure类的使用者无法定义该类的多个实例，否则会产生编译错误。程序如下：
	- ```c
	  #include <iostream.h>
	  class Configure {
	  protected:
	  Configure(){};
	  
	  public:
	  static Configure* Instance();
	  
	  public:
	  int GetConfigureData() {return data;}
	  int SetConfigureData(int m_data) {data = m_data; return data;}
	  
	  private:
	  static Configure* _instance;
	  int data;
	  }
	  - Configure::_instance = NULL;
	  Configure *Configure::Instance() {
	  if (_instance == NULL) {
	    _instance = new Configure();
	  }
	  return _instance;
	  }
	  - void main() {
	  Configure* t = NULL;
	  t = Instance();
	  int d = t->GetConfigureData();
	  }
	  ```
- Abstract Factory 抽象工厂：
- Builder 生成器：
- Factory Method 工厂方法：
- Prototype 原型：
- Singleton 单例：
- 创建型模式比较：