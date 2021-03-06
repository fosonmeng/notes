- TODO 存储器的层次结构：
	- ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9ukdR6qwOLJsUkuDBIYbTm3WXzsjRwidd5ouPPpwUiUBg-1IGFaqnCpaW5ivxis8sgxqNZb6TpTZrVtFXyzWmqcPQDG9cdhPr0cSSDZUXA75A1Be6w1W00)
	- Cache和主存之间的交互功能全部由硬件实现，而主存与辅存之间的交互功能可由硬件和软件结合起来实现。
- 存储器的分类：
	- 位置：内存；外存；
	- 构成材料：
		- 磁存储器：
		- 半导体存储器：双极型、MOS型；数据是否需要刷新：静态、动态
		- 光存储器
	- 工作方式：
		- 读写：RAM：
		- 只读：
		  > 1. 固定只读存储器Read Only Memory，ROM
		  > 2. 可编程的只读存储器Programmable Read Only Memory，PROM
		  > 3. 可擦除可编程的只读存储器Erasable Programmable Read Only Memory，EPROM
		  > 4. 电擦除可编程的只读存储器Electrically Erasable Programmable Read Only Memory，EEPROM
		  > 5. 闪速存储器Flash Memory
	- 访问方式：按地址，按内容
	- 按寻址方式：
	  > 1. 随机存储器Random Access Memory，RAM
	  > 2. 顺序存储器Sequentially Addressed Memory，SAM：磁带
	  > 3. 直接存储器Direct Addressed Memory，DAM：磁盘
- 相联存储器：
	- ![bec269437da3ddc001d94a1d7bf07567.png](https://img.mhugh.net/typora/89b16742a4fc41d38b09e429345b6eb7.png)
	- 高速缓冲存储器；在虚拟存储器中用来作段表、页表或快表存储器；用在数据库和知识库中
- 高速缓存：
	- TODO 高速缓存的组成：
	  :LOGBOOK:
	  CLOCK: [2022-03-18 Fri 22:10:13]--[2022-03-18 Fri 22:10:14] =>  00:00:01
	  CLOCK: [2022-03-18 Fri 22:10:30]--[2022-03-18 Fri 22:10:31] =>  00:00:01
	  CLOCK: [2022-03-18 Fri 22:10:33]--[2022-03-18 Fri 22:10:34] =>  00:00:01
	  :END:
	- 高速缓存中的地址映像方法:
		- 直接映像：主存的块与Cache中块的对应关系是固定的
			- 地址变换简单；但是灵活性差：不同区号中块号相关的块无法同时调入Cache存储器，即使Cache存储器中有空着的块也只能空着
		- ^^全相联映像^^：
			- ![ec2ab2373d63b64b3a7eb4d235cb494d.png](https://img.mhugh.net/typora/7c4cda0ad2094e2c8697077ee1d09457.png)
			- > 1. 优点：主存的块调入Cache的位置不受限制，十分灵活
			  > 2. 缺点：无法从主存块号中直接获得Cache的块号，变换比较复杂，速度比较慢
		- 组相联映像：
	- 替换算法： ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9uDdl_izv5pzTDVxPvAfUMLhp2ordzp-RimX1-sjhnOlzi8FcqVHUIy8lz4v_DcVziJiFJ3HEVxDt_VCeA9CadUsOyxPc6OfH3Aj1cgEq0)
	- Cache的性能分析：
		- `H_c` 为Cache的命中率，`t_c` 为Cache的存取时间，`t_m`为主存的访问时间
		  $$
		  t_{存} = H_c t_c + (1-H_c) t_m = t_c + (1-H_c)(t_m-t_c)
		  $$
		- 降低Cache失效率： ![](http://www.plantuml.com/plantuml/svg/SoWkIImgoStCIybDBE3Yqb9uERFtoTu-vyJaZDIdIpO-czhnlA-TIqihNk5bG-UpxfNF6ZSytJlv-QoMftEdFrstysLxFrZoMV-4bwjdW7M1v719F9-zuqNZbAUxbd4vf09jXDeA0000)
	- 多级Cache：
- TODO 虚拟存储器：
- 外存储器：
	- 磁盘存储器：
		- #硬盘
	- 光盘：
	  > 1. 只读CD-ROM
	  > 2. 只写一次型WORM
	  > 3. 可擦除型
	- 固态硬盘：
		- 存储介质：闪存；DRAM。
		- 基于闪存的固态硬盘：主控芯片的主要作用，一是合理调配数据在各个闪存芯片上的负荷，二则是承担数据中转的作用，连接闪存芯片和外部SATA接口。不同**主控芯片**的能力相差非常大，在数据处理能力、算法，对闪存芯片的读取写入控制上会有非常大的不同，直接会导致固态硬盘产品在性能上差距很大。
- 磁盘阵列技术：
	- 廉价冗余磁盘阵列 Redundant Array of Independent Disk，或者 独立冗余磁盘阵列, #RAID
- 存储域网络：
	- Storage Area Network, #SAN