- 设计与实现方法：
	- 面向对象程序设计主要是根据问题的详细描述，设计出能够被迅速转换为面向对象程序实现的代码，相比本章的第12.3节，其设计与实现更为底层，更接近代码。但是，对面向对象设计结果的衡量没有统一的标准，因此很难衡量针对一个问题所设计的解决方案是否最优，这也正是软件工程领域内分析与设计的难点，更多的情况下，分析与设计的结果是一种经验的总结。
	- 尽管不存在一致的对分析与设计结果的衡量标准，但许多面向对象和软件工程领域内“大师”都根据自己长期的实践经验，总结出了面向对象分析与设计的原则，而这些原则可成为我们在实际问题进行分析与设计时的指导准则。
	- 一般而言，当面临一个具体的问题时，可分为两大阶段：首先根据问题进行设计，其次根据设计进行实现。由于面向对象的实现和面向对象设计之间不存在较大的差异，所不同的是设计更多采用的是UML的标准表示，而实现则是采用面向对象语言表达，因此解决问题的重点应放在面向对象的设计上。
	- 目前，被公认的好的面向对象设计是由前人所总结的设计模式，因此熟练并正确地掌握面向对象设计技术，必须很好地体会并理解常用的23种设计模式。当对23种设计模型运用时，必须做到以下几点。
	  1. 能够根据设计模式的名称画出其对应的类图。
	  2. 理解类图每一个类的作用与功能。
	  3. 能够将现实问题中所描述的各种职责映射到类图中具体的类。
	  4. 能够使用一种面向对象语言实现设计。
- 设计模式的应用：
	- 问题说明：
		- 已知某类库开发商提供了一套类库，类库中定义了Application类和Document类，它们之间的关系如图12-31所示，其中，Application类表示应用程序自身，而Document类则表示应用程序打开的文档。Application类负责打开一个已有的以外部形式存储的文档，如一个文件，一旦从该文件中读出信息后，它就由一个Document对象表示。
		  ![image-20211023073813212](https://img.mhugh.net/typora/image-20211023073813212.png)
		- 当开发一个具体的应用程序时，开发者需要分别创建自己的Application和Document子类，例如图12-31中的类MyApplication和类MyDocument，并分别实现Application和Document类中的某些方法。
		- 已知Application类中的openDocument方法采用了模板方法（Template Method）设计模式，该方法定义了打开文档的每一个主要步骤，如下所示。
		  1. 首先检查文档是否能够被打开，若不能打开，则给出出错信息并返回。
		  2. 创建文档对象。
		  3. 通过文档对象打开文档。
		  4. 通过文档对象读取文档信息。
		  5. 将文档对象加入到Application的文档对象集合中。
	- 根据设计模式的名称画出其对应的类图：
		- 问题描述中已经给出了该设计采用的设计模式为模板方法，因此，首先给出模板方法的类图，如图12-32所示。
	- 理解类图中每一个类的作用与功能：
		- 模板方法类图中，AbstractClass类定义了基本的操作PrimitiveOperation1()和PrimitiveOperation2()，并在TemplateMethod()方法中调用了这两个操作，但这两个操作都并未实现，而是留待子类去实现，从而达到模板方法的目的：定义一个操作中的算法的骨架，而将一些步骤延迟到子类中，使得子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。
		  ![image-20211023075529772](https://img.mhugh.net/typora/image-20211023075529772.png)
	- 能够将现实问题中所描述的各种职责映射到类图中具体的类：
		- 在提出的具体问题中，已经告知了Application类中的openDocument方法采用了模板方法，而openDocument方法的步骤都已经给出，因此，很容易将Applicaiton类对应为模板方法类图中的AbstractClass类，openDocument方法映射为模板方法类图中的TemplateMethod方法，而主要步骤则对应为PrimitiveOperation1()等基本操作。由此可推出，各种主要的步骤中，应该存在某些步骤是由Application的子类实现的。
	- 能够使用一种面向对象语言实现设计：
		- 一旦分析清楚实际问题的设计结果和原始的设计模式类图中类的对应关系，便可采用一种面向对象语言实现。下面分别采用C++和Java语言实现给出的设计。
		  ```c++
		  #include <iostream>
		  #include <vector>
		  using namespace std;
		  - class Document {
		  public:
		  void save() {}
		  void open(string docName) {}
		  void close() {}
		  virtual void read(string docName) = 0;
		  };
		  - class Application {
		  private:
		  vector <Document*> docs;
		  
		  public:
		  bool canOpenDocument(string docName) {}
		  void addDocument(Document* aDocument) {
		    docs.push_back(aDocument);
		  }
		  virtual Document* doCreateDocument() = 0;
		  void openDocument(string docName) {
		    if (!canOpenDocument(docName)) {
		      cout << "文档无法打开！" << endl;
		      return;
		    }
		    Document* adoc = doCreateDocument();
		    adoc->open(docName);
		    adoc->read(docName);
		    addDocument(adoc);
		  }
		  };
		  ```
		- ```java
		  abstract class Document {
		  public void save() {}
		  public void open(String docName) {}
		  public void close() {}
		  public abstract void read(String docName);
		  }
		  - abstract class Application {
		  private Vector<Document> docs;
		  
		  public boolean canOpenDocument(String docName) {}
		  public void addDocument(Document aDocument) {
		    docs.add(aDocument);
		  }
		  public abstract Document doCreateDocument();
		  public void openDocument(String docName) {
		    if (!canOpenDocument(docName)) {
		      System.out.println("文档无法打开！");
		      return;
		    }
		    Document adoc = doCreateDocument();
		    adoc.open(docName);
		    adoc.read(docName);
		    addDocument(adoc);
		  }
		  }
		  ```