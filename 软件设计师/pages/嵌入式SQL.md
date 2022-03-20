- 嵌入式SQL与主语言之间的通信通常有如下三种方式：
	- SQL通信区（SQL Communication Area，SQLCA）向主语言传递SQL语句执行的状态信息，使主语言能够根据此信息控制程序流程。
	- 主变量也称共享变量。主语言向SQL语句提供参数主要通过主变量，主变量由主语言的程序定义，并用SQL的DECLARE语句说明。引用时，为了与SQL属性名相区别，需在主变量前加“`:`”。
	    ```sql
	    EXEc SQL SELECT sname, age, sec
	    INTO :Msno, :Mcno, :givensno
	    FROM students
	    WHERE sno=:Msno;
	    ```
	- ==游标SQL语言==是面向集合的，一条SQL语句可产生或处理多条记录。而主语言是面向记录的，一组主变量一次只能放一条记录，所以，引入游标，通过移动游标指针来决定取哪一条记录。