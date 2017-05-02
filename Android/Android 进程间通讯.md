#  Android 进程间通讯

* Linux IPC: Pipe Signal,Trace(父子进程，兄弟进程)，Name Pipe (所有进程)，Socket

* Android IPC: Binder 机制

### 组成

运行于用户空间：Client ,Server, Service Manager（提供辅助管理）； 运行于内核：Binder驱动

C-S通讯基于Binder驱动和Service Manager

Server Manager 是Binder机制的守护进程，管理开发者创建的各种Server，并向Client提供查询Server远程接口的功能。（也作为一种特殊Server）

Server Manager成为Binder机制守护进程的过程：

1. 打开/dev/binder ：open("/dev/binder",O_RDWR)
2. 建立128KB内存映射 mmap(NULL,mapsize,PROT_READ,MAP_PRIVATE,bs->fd,0),bs = binder_state结构体
3. 通知Binder驱动，“我”是守护进程： binder_become_context_manager(bs);
4. 进入循环等待请求的到来： binder_loop(bs,svcmgr_handler);

* __几个主要的结构体:__

1. binder_proc:保存打开设备文件的/dev/binder的进程的上下文信息

   ​


Client 通过IServerManager::getService 而Server通IServerMangager::addService获得Binder的驱动交互








