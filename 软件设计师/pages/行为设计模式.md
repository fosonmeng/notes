- 行为模式涉及到算法和对象间职责的分配。行为模式不仅描述对象或类的模式，还描述它们之间的通信模式。这些模式刻画了在运行时难以跟踪的复杂的控制流。它们将用户的注意力从控制流转移到对象间的联系方式上来。
- 行为类模式使用继承机制在类间分派行为。本章包括两个这样的模式，其中TemplateMethod较为简单和常用。模板方法是一个算法的抽象定义，它逐步地定义该算法，每一步调用一个抽象操作或一个原语操作，子类抽象操作以具体实现该算法。另一种行为类模式是Interpreter，它将一个文法表示为一个类层次，并实现一个解释器作为这些类的实例上的一个操作。
- 行为对象模式使用对象复合而不是继承。一些行为对象模式描述了一组对等的对象怎样相互协作以完成其中任一个对象都无法单独完成的任务。这里一个重要的问题是对等的对象。
- 如何互相了解对方。对等对象可以保持显式的对对方的引用，但那会增加它们的耦合度。在极端情况下，每一个对象都要了解所有其他的对象。Mediator在对等对象间引入一个mediator对象以避免这种情况的出现。mediator提供了松耦合所需的间接性。
- Chain of Responsibility提供更松的耦合。它让用户通过一条候选对象链隐式地向一个对象发送请求。根据运行时刻情况任一候选者都可以响应相应的请求。候选者的数目是任意的，可以在运行时刻决定哪些候选者参与到链中。
- Observer模式定义并保持对象间的依赖关系。典型的Observer的例子是Smalltalk中的模型/视图/控制器，其中一旦模型的状态发生变化，模型的所有视图都会得到通知。
- 其他的行为对象模式常将行为封装在一个对象中并将请求指派给它。Strategy模式将算法封装在对象中，这样可以方便地指定和改变一个对象所使用的算法。Command模式将请求封装在对象中，这样它就可作为参数来传递，也可以被存储在历史列表里，或者以其他方式使用。State模式封装一个对象的状态，使得当这个对象的状态对象变化时，该对象可改变它的行为。Visitor封装分布于多个类之间的行为，而Iterator则抽象了访问和遍历一个集合中的对象的方式。
- 【例10.9】Observer模式。
	- 在一公文处理系统中，开发者定义了一个公文类OfficeDoc，其中定义了公文具有的属性和处理公文的相应方法。当公文的内容或状态发生变化时，关注此OfficeDoc类对象的相应的DocExplorer对象的内容或状态发生变化时，所有与之相关联的DocExplorer对象都将得到通知，这种应用被称为观察者模式。
	- 程序如下：
	  ```c
	  #include <iostream>
	  const OBS_MAXNUM=20; // 最多与OfficeDoc对象相关联的DocExplorer对象的个数
	  class OfficeDoc;
	  - class DocExplorer {
	  public:
	  DocExplorer(OfficeDoc *doc);
	  virtual void update(OfficeDoc *doc) = 0; // 更新自身状态的函数
	  //其他相关属性和方法省略
	  }
	  - class OfficeDoc {
	  private:
	  DocExplorer *myObs[OBS_MAXNUM];
	  // 关注此公文类的DocExplorer类对象指针数组
	  int index; // 与OfficeDoc对象关联的DocExplorer对象的个数
	  
	  public:
	  OfficeDoc(){
	    index=0;
	  }
	  void attach(DocExplorer *o) {
	    // 将一DocExplorer对象与OfficeDoc对象相关联
	    if(index >= OBS_MAXNUM || o == NULL) return;
	    for (int loop = 0; loop < index; loop++)
	      if(myObs[loop] == 0) return;
	    myObs[index] = 0;
	    index++;
	  }
	  void detach(DocExplorer *o) {
	    // 解除某DocExplorer对象与OfficeDoc对象的关联
	    if(o == NULL) return;
	    for(int loop = 0; loop < index; loop++) {
	      if (myObs[loop] == o) {
	        if (loop <= index-1) myObs[loop] = myObs[index-1];
	        myObs[index-1] = NULL;
	        index--;
	        break;
	      }
	    }
	  }
	  
	  private:
	  void notifyObs() {
	    for(int loop = 0; loop < index; loop++) {
	      myObs[loop]->update(this); // DocExplorer对象更新自身状态
	    }
	  }
	  
	  // 其他公文类的相关属性和方法
	  };
	  - DocExplorer::DocExplorer(OfficeDoc *doc) { // DocExplorer类对象的构造函数
	  doc->attach(this); // 将此DocExplorer对象与doc对象相关联
	  }
	  ```
- **Chain of Responsibility 责任链**：
- **Command 命令**：
- **Interpreter 解释器**：
- **Mediator 中介者**：
- **Memento 备忘录**：
- **Observer 观察者**：
- **State 状态**：
- **Strategy 策略**：
- **Template Method 模板方法**：
- **Visitor 访问者**：
- 行为模式比较：