## 关于死锁的一些概念性问题

----------------------------------------------------


### 什么是死锁？

	所谓死锁： 是指两个或两个以上的进程在执行过程中，由于竞争资源或者由于彼此通信而造成的一种阻塞的现象，若无外力作用，
	
	它们都将无法推进下去。此时称系统处于死锁状态或系统产生了死锁，这些永远在互相等待的进程称为死锁进程。

<br>

### 产生死锁的四个必要条件：

	（1） 互斥条件：一个资源每次只能被一个进程使用。
	（2） 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
	（3） 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
	（4） 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

<br>

### 产生死锁的原因：

	1）竞争资源引起进程死锁
	
	当系统中供多个进程共享的资源如打印机、公用队列的等，其数目不足以满足诸进程的需要时，会引起诸进程对资源的竞争而产生死锁。
	
	2）可剥夺资源和不可剥夺资源
	
	系统中的资源可以分为两类，一类是可剥夺资源，是指某进程在获得这类资源后，该资源可以再被其他进程或系统剥夺。例如，优先权
	高的进程可以剥夺优先权低的进程的处理机。又如，内存区可由存储器管理程序，把一个进程从一个存储区移到另一个存储区，此即剥
	夺了该进程原来占有的存储区，甚至可将一进程从内存调到外存上，可见，CPU和主存均属于可剥夺性资源。另一类资源是不可剥夺资
	源，当系统把这类资源分配给某进程后，再不能强行收回，只能在进程用完后自行释放，如磁带机、打印机等。
	
	3）竞争不可剥夺资源
	
	在系统中所配置的不可剥夺资源，由于它们的数量不能满足诸进程运行的需要，会使进程在运行过程中，因争夺这些资源而陷于僵局。
	例如，系统中只有一台打印机R1和一台磁带机R2，可供进程P1和P2共享。假定PI已占用了打印机R1，P2已占用了磁带机R2，若P2继续要
	求打印机R1，P2将阻塞；P1若又要求磁带机，P1也将阻塞。于是，在P1和P2之间就形成了僵局，两个进程都在等待对方释放自己所需要
	的资源，但是它们又都因不能继续获得自己所需要的资源而不能继续推进，从而也不能释放自己所占有的资源，以致进入死锁状态。

	4）竞争临时资源
	
	上面所说的打印机资源属于可顺序重复使用型资源，称为永久资源。还有一种所谓的临时资源，这是指由一个进程产生，被另一个进程
	使用，短时间后便无用的资源，故也称为消耗性资源，如硬件中断、信号、消息、缓冲区内的消息等，它也可能引起死锁。例如，SI，
	S2，S3是临时性资源，进程P1产生消息S1，又要求从P3接收消息S3；进程P3产生消息S3，又要求从进程P2处接收消息S2；进程P2产生消
	息S2，又要求从P1处接收产生的消息S1。如果消息通信按如下顺序进行：
	
	P1: ···Relese（S1）；Request（S3）； ···
	P2: ···Relese（S2）；Request（S1）； ···
	P3: ···Relese（S3）；Request（S2）； ···
	并不可能发生死锁。但若改成下述的运行顺序：

	P1: ···Request（S3）；Relese（S1）；···
	P2: ···Request（S1）；Relese（S2）； ···
	P3: ···Request（S2）；Relese（S3）； ···
	则可能发生死锁。
	
	2.进程推进顺序不当引起死锁
	
	由于进程在运行中具有异步性特征，这可能使P1和P2两个进程按下述两种顺序向前推进。
	
	1） 进程推进顺序合法
	
	当进程P1和P2并发执行时，如果按照下述顺序推进：P1：Request（R1）； P1：Request（R2）； P1: Relese（R1）；P1: Relese（R2）； <br> P2：Request（R2）； P2：Request（R1）； P2: Relese（R2）；P2: Relese（R1）；这两个进程便可顺利完成，这种不会引起进程死锁的推进顺序是合法的。

	2） 进程推进顺序非法

	若P1保持了资源R1,P2保持了资源R2，系统处于不安全状态，因为这两个进程再向前推进，便可能发生死锁。例如，当P1运行到P1：
	Request（R2）时，将因R2已被P2占用而阻塞；当P2运行到P2：Request（R1）时，也将因R1已被P1占用而阻塞，于是发生进程死锁。

<br>

### 如何预防死锁：

	理解了死锁的原因，尤其是产生死锁的四个必要条件，就可以最大可能地避免、预防和解除死锁。只要打破四个必要条件之一就能
	有效预防死锁的发生：(可能会导致系统资源利用率和系统吞吐量降低。)
	
	（1）打破互斥条件：改造独占性资源为虚拟资源，大部分资源已无法改造。
	（2）打破不可抢占条件：当一进程占有一独占性资源后又申请一独占性资源而无法满足，则退出原占有的资源。
	（3）打破占有且申请条件：采用资源预先分配策略，即进程运行前申请全部资源，满足则运行，不然就等待，这样就不会占有且申请。
	（4）打破循环等待条件：实现资源有序分配策略，对所有设备实现分类编号，所有进程只能采用按序号递增的形式申请资源。
	
<br>

### 避免死锁：

	该方法同样是属于事先预防的策略，但它并不须事先采取各种限制措施去破坏产生死锁的的四个必要条件，而是在资源的动态分配过程
	中，用某种方法去防止系统进入不安全状态，从而避免发生死锁。

	（1）有序资源分配法：
	
	这种算法资源按某种规则系统中的所有资源统一编号（例如打印机为1、磁带机为2、磁盘为3、等等），申请时必须以上升的次序。系统
	要求申请进程：
		
		1、对它所必须使用的而且属于同一类的所有资源，必须一次申请完；
		2、在申请不同类资源时，必须按各类设备的编号依次申请。例如：进程PA，使用资源的顺序是R1，R2； 进程PB，使用资源的顺序是R2，R1；若采用动态分配有可能形成环路条件，造成死锁。
		
		采用有序资源分配法：R1的编号为1，R2的编号为2；
		PA：申请次序应是：R1，R2
		PB：申请次序应是：R1，R2
		这样就破坏了环路条件，避免了死锁的发生
	
	（2）银行家算法：

	初始化
	由用户输入数据，分别对可利用资源向量矩阵AVAILABLE、最大需求矩阵MAX、分配矩阵ALLOCATION、需求矩阵NEED赋值。
	
	银行家算法
	
	在避免死锁的方法中，所施加的限制条件较弱，有可能获得令人满意的系统性能。在该方法中把系统的状态分为安全状态和不安全状态， <br> 
	只要使系统始终都处于安全状态，便可以避免发生死锁。
	银行家算法的基本思想是分配资源之前，判断系统是否是安全的；若是，才分配。它是最具有代表性的避免死锁的算法。
	
	设进程cusneed提出请求REQUEST [i]，则银行家算法按如下规则进行判断。
	(1)如果REQUEST [cusneed] [i]<= NEED[cusneed][i]，则转（2)；否则，出错。
	(2)如果REQUEST [cusneed] [i]<= AVAILABLE[i]，则转（3)；否则，等待。
	(3)系统试探分配资源，修改相关数据：
		AVAILABLE[i]-=REQUEST[cusneed][i];
		ALLOCATION[cusneed][i]+=REQUEST[cusneed][i];
		NEED[cusneed][i]-=REQUEST[cusneed][i];
	(4)系统执行安全性检查，如安全，则分配成立；否则试探险性分配作废，系统恢复原状，进程等待。
	
	安全性检查算法
	(1）设置两个工作向量Work=AVAILABLE;FINISH;
	(2)从进程集合中找到一个满足下述条件的进程，
		FINISH==false;
		NEED<=Work;
	如找到，执行（3)；否则，执行（4)
	(3)设进程获得资源，可顺利执行，直至完成，从而释放资源。
		Work=Work+ALLOCATION;
		Finish=true;
		GOTO 2
	(4)如所有的进程Finish= true，则表示安全；否则系统不安全。
	

```cpp
		
		//---------------头文件----------------------
		# ifndef __BANKER_FILE__
		# define __BANKER_FILE__
		 
		# define _CRT_SECURE_NO_WARNINGS 1
		 
		 
		# include <stdio.h>
		# include <stdlib.h>
		# include <assert.h>
		 
		# define TRUE 1       //状态位
		# define FAULSE 0      //状态位
		# define PCB_NUM 5      //进程数
		# define RESOURCE_NUM 5   //资源种类
		 
		size_t Menu();         //菜单
		void InitPCB();        //初始化程序
		size_t SafeCheck();      //安全性算法
		void RequestResource();    //发出资源请求
		 
		 
		# endif   //__BANKER_FILE__
		
		
		//--------------源代码-------------------
		# include "BANKER.h"
 
		size_t g_max[PCB_NUM][RESOURCE_NUM] = { 0 };        //最大需求矩阵
		size_t g_allocation[PCB_NUM][RESOURCE_NUM] = { 0 };    //已分配矩阵
		size_t g_need[PCB_NUM][RESOURCE_NUM] = { 0 };       //需求矩阵
		size_t g_available[RESOURCE_NUM] = { 0 };         //可利用资源向量
		 
		size_t g_work[RESOURCE_NUM] = { 0 };            //可利用资源数目
		size_t g_finish[RESOURCE_NUM];                 //状态
		size_t g_safe_order[PCB_NUM];                 //安全序列
		size_t g_request[RESOURCE_NUM] = { 0 };          //请求向量
		size_t g_pcb_num = 0, g_resource_type = 0;        //实际的进程数和资源种类
		 
		 
		//菜单函数
		size_t Menu()
		{
		    size_t choose = 0;
		 
		    printf("\t*-*-*-*-*-*- Banker's  Algorthm -*-*-*-*-*-*\n");
		    printf("\t*-*-*-                                -*-*-*\n");
		    printf("\t*-*-*-       1. 初始化进程            -*-*-*\n");
		    printf("\t*-*-*-       2. 安全性算法            -*-*-*\n");
		    printf("\t*-*-*-       3. 银行家算法            -*-*-*\n");
		    printf("\t*-*-*-       0. 退      出            -*-*-*\n");
		    printf("\t*-*-*-                                -*-*-*\n");
		    printf("\t*-*-*-*--*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*\n\n");
		 
		    printf("请选择->: ");
		    scanf("%d", &choose);
		 
		    return choose;
		}
		 
		//检查初始化是否正确
		static int _CheckInit()
		{
		    size_t i = 0, j = 0;
		 
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        for (j = 0; j < g_resource_type; j++)
		        {
		            if (g_allocation[i][j] + g_need[i][j] > g_max[i][j])
		            {
		                return -1;         
		            }
		        }
		    }
		    return 1;
		}
		 
		//初始化程序
		void InitPCB()
		{
		    size_t i = 0, j = 0;
		     
		    printf("\n请输入进程数量和资源种类的个数：\n");
		    fflush(stdin);
		    scanf("%d%d", &g_pcb_num, &g_resource_type);
		    printf("pcb_num = %d  resource_type = %d \n", g_pcb_num, g_resource_type);
		 
		 
		    printf("\n输入各个进程的最大需求矩阵：\n");
		    fflush(stdin);
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        printf("P[%d]:", i + 1);
		        for (j = 0; j < g_resource_type; j++)
		        {
		            scanf("%d", &g_max[i][j]);
		        }
		    }
		    printf("输入各个进程的已分配矩阵：\n");
		    fflush(stdin);
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        printf("P[%d]:", i + 1);
		        for (j = 0; j < g_resource_type; j++)
		        {
		            scanf("%d", &g_allocation[i][j]);
		        }
		    }
		    printf("输入各个进程的需求矩阵：\n");
		    fflush(stdin);
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        printf("P[%d]:", i + 1);
		        for (j = 0; j < g_resource_type; j++)
		        {
		            scanf("%d", &g_need[i][j]);
		        }
		    }
		    //求Available
		    printf("输入剩余各类资源：\n");
		    fflush(stdin);
		    for (i = 0; i < g_resource_type; i++)
		    {
		        printf("P[%d]:", i + 1);
		        scanf("%d", &g_available[i]);
		    }
		 
		    int ret = _CheckInit();
		    if (-1 == ret)
		    {
		        printf("初始化失败，分配矩阵与需求矩阵之和大于最大需求矩阵！\n\n");
		    }
		    else
		        printf("初始化成功！\n\n");
		 
		}
		 
		//打印安全序列
		static void _Print()
		{
		    size_t i = 0;
		 
		    printf("\n在该时刻存在一个安全序列： ");
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        printf("P[%d]", g_safe_order[i]);
		        if (i != g_pcb_num - 1)
		            printf("->");
		    }
		    printf("\n\n");
		}
		 
		//安全性算法
		size_t SafeCheck()
		{
		    size_t i = 0, j = 0, k = 0;
		    size_t count, flag;
		    size_t suffix = 0;           //安全序列的下标
		 
		    //初始化向量Work和Finish
		    for (i = 0; i < g_resource_type; i++)
		    {
		        g_work[i] = g_available[i];
		    }
		    for (j = 0; j < g_pcb_num; j++)
		    {
		        g_finish[j] = FAULSE;
		    }
		 
		    //查找安全序列
		    while (1)
		    {
		        for (i = 0; i < g_pcb_num; i++)
		        {
		            count = 0;
		            flag = 0;
		 
		            for (j = 0; j < g_resource_type; j++)
		            {
		                if (g_work[j] >= g_need[i][j])
		                {
		                    count++;
		                }
		                else
		                    break;
		            }
		 
		            //可以进行分配并完成该进程
		            if ((count == g_resource_type) && (g_finish[i] != TRUE))
		            {
		                flag = 1;
		 
		                for (k = 0; k < g_resource_type; k++)
		                {
		                    g_work[k] = g_work[k] + g_allocation[i][k];
		                }
		                g_finish[i] = TRUE;
		                g_safe_order[suffix++] = i + 1;
		 
		                if (suffix == g_pcb_num)
		                {
		                    _Print();
		                    return 1;
		                }
		            }
		        }
		        //遍历完之后没有符合的进程则跳出循环
		        if (0 == flag)
		        {
		            printf("\n不存在安全序列!\n\n");
		            return 0;
		        }
		        else
		            i = 0;
		    }
		}
		 
		//打印分配后的进程资源表
		static void _PrintPcbList()
		{
		    size_t i = 0, j = 0;
		 
		    printf("进程\tMax\tAllo\tNeed\tAvail\n");
		    for (i = 0; i < g_pcb_num; i++)
		    {
		        printf("P[%d]：", i + 1);
		 
		        for (j = 0; j < g_resource_type; j++)
		        {
		            printf("%d ", g_max[i][j]);
		        }
		        printf("\t");
		        for (j = 0; j < g_resource_type; j++)
		        {
		            printf("%d ", g_allocation[i][j]);
		        }
		        printf("\t");
		        for (j = 0; j < g_resource_type; j++)
		        {
		            printf("%d ", g_need[i][j]);
		        }
		        printf("\t");
		        if (0 == i)
		        {
		            for (j = 0; j < g_resource_type; j++)
		            {
		                printf("%d ", g_available[j]);
		            }
		        }
		        printf("\n");
		    }
		    printf("\n\n");
		}
		 
		//试分配
		static void _TryAllocation(size_t PCB_ORDER)
		{
		    size_t i = 0, j = 0;
		    size_t ret;
		 
		    for (i = 0; i < g_resource_type; i++)
		    {
		        g_available[i] -= g_request[i];
		        g_allocation[PCB_ORDER][i] += g_request[i];
		        g_need[PCB_ORDER][i] -= g_request[i];
		    }
		     
		    ret = SafeCheck();
		    //分配失败
		    if (0 == ret)
		    {
		        g_need[PCB_ORDER][i] += g_request[i];
		        g_allocation[PCB_ORDER][i] -= g_request[i];
		        g_available[i] += g_request[i];
		        printf("该分配不安全，进程P[%d]须等待！\n\n", PCB_ORDER + 1);
		         
		        return;
		    }
		 
		    //打印分配后的进程资源表 
		    _PrintPcbList();
		}
		 
		 
		//发出资源请求
		void RequestResource()
		{
		    size_t i = 0;
		    size_t PCB_ORDER = 0;
		 
		    printf("\n请输入进程名和各个资源的数量：\n");
		    scanf("%d", &PCB_ORDER);
		    PCB_ORDER -= 1;
		    fflush(stdin);
		    for (i = 0; i < g_resource_type; i++)
		    {
		        printf("Request_%c:", 64 + i + 1);
		        scanf("%d", &g_request[i]);
		    }
		 
		     
		    for (i = 0; i < g_resource_type; i++)
		    {
		        //当Request>Need的情况
		        if (g_request[i]>g_need[PCB_ORDER][i])
		        {
		            printf("\n需要的资源已经超出所宣布的最大值！\n\n");
		            return;
		        }
		        //当Request>Available的情况
		        if (g_request[i]>g_available[i])
		        {
		            printf("\n尚无足够资源，P[%d]须等待！\n\n", PCB_ORDER+1);
		            return;
		        }
		    }
		     
		    //试分配
		    _TryAllocation(PCB_ORDER);
		 
		}
		
		
		//-----------主函数---------------------
		# include "BANKER.h"
 
		int main()
		{
		    size_t ret = 0;
		 
		    while (1)
		    {
		        switch (ret = Menu())
		        {
		        case 1:
		            InitPCB();
		            break;
		        case 2:
		            SafeCheck();
		            break;
		        case 3:
		            RequestResource();
		            break;
		        case 0:
		            exit(EXIT_SUCCESS);
		            break;
		        default:
		            break;
		        }
		    }
		 
		    system("pause");
		    return 0;
		}
		
		

```

<br>

### 如何检测死锁：

	


### 如何解除死锁：


	1) 资源剥夺法。挂起某些死锁进程，并抢占它的资源，将这些资源分配给其他的死锁进程。但应防止被挂起的进程长时间得不到
	   资源，而处于资源匮乏的状态。

	2) 撤销进程法。强制撤销部分、甚至全部死锁进程并剥夺这些进程的资源。撤销的原则可以按进程优先级和撤销进程代价的高低进行。
	
	3) 进程回退法。让一（多）个进程回退到足以回避死锁的地步，进程回退时自愿释放资源而不是被剥夺。要求系统保持进程的历史信
	   息，设置还原点。
	
	
	
	
	
	
	
	
	
	
	
	
	
	












