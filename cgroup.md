### 1. cgroup的主要作用.
- 资源限制: cgroups可以对任务需要的资源总额进行限制. 比如设定任务运行时使用的内存上限，一旦超出就发 OOM(Out Of Memory内存溢出)。

- 优先级分配：通过分配的 CPU 时间片数量和磁盘 IO 带宽，实际上就等同于控制了任务运行的优先级。

- 资源统计：cgoups 可以统计系统的资源使用量，比如 CPU 使用时长、内存用量等。这个功能非常适合当前云端产品按使用量计费的方式。

- 任务控制：cgroups 可以对任务执行挂起、恢复等操作。

### cgroups 的概念及原理

**Task(任务)**: 在 linux 系统中，内核本身的调度和管理并不对进程和线程进行区分，只是根据 clone 时传入的参数的不同来从概念上区分进程和线程。这里使用 task 来表示系统的一个进程或线程。

**Cgroup(控制组)**： cgroups 中的资源控制以 cgroup 为单位实现。Cgroup 表示按某种资源控制标准划分而成的任务组，包含一个或多个子系统。一个任务可以加入某个 cgroup，也可以从某个 cgroup 迁移到另一个 cgroup。

**Subsystem(子系统)**：cgroups 中的子系统就是一个资源调度控制器(又叫 controllers)。比如 CPU 子系统可以控制 CPU 的时间分配，内存子系统可以限制内存的使用量。

subsystem 如下( cat /proc/cgroups): 

> blkio 对块设备的 IO 进行限制。   
cpu 限制 CPU 时间片的分配，与 cpuacct 挂载在同一目录。  
cpuacct 生成 cgroup 中的任务占用 CPU 资源的报告，与 cpu 挂载在同一目录。 
cpuset 给 cgroup 中的任务分配独立的 CPU(多处理器系统) 和内存节点.  
devices 允许或禁止 cgroup 中的任务访问设备。  
freezer 暂停/恢复 cgroup 中的任务。  
hugetlb 限制使用的内存页数量。  
memory 对 cgroup 中的任务的可用内存进行限制，并自动生成资源占用报告。  
net_cls 使用等级识别符（classid）标记网络数据包，这让 Linux 流量控制器（tc 指令）可以识别来自特定 cgroup 任务的数据包，并进行网络限制。  
net_prio 允许基于 cgroup 设置网络流量(netowork traffic)的优先级。  
perf_event 允许使用 perf 工具来监控 cgroup。  
pids 限制任务的数量.  
Hierarchy(层级) 层级有一系列 cgroup 以一个树状结构排列而成，每个层级通过绑定对应的子系统进行资源控制。层级中的 cgroup 节点可以包含零个或多个子节点，子节点继承父节点挂载的子系统。一个操作系统中可以有多个层级。  


reference: https://zhuanlan.zhihu.com/p/388101355




