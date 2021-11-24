## docker原理
> 文件系统

1. docker文件系统AUFS（联合文件系统union File System）
2. 将多个文件联合在一起成为一个统一的视图
3. 只有第一个文件有修改权限，不会影响后续文件，本质上是对其他文件的覆盖

> 镜像层
1. 镜像层为可读层，每一个下层镜像都有指针指向上层镜像，统一文件系统将所有镜像整合成文件系统
2. 每一个镜像层包含一个元数据，可以让docker获取到运行与构建时的信息，还包括父层的层次信息，只读层与读写层都包含元数据

> 容器层 + 镜像层
1. 容器层是可读写层，所有的镜像层都只是可读层
2. 容器中，上层镜像记录对下层镜像所作的更改


> docker命令对镜像与容器的操作
1. docker create 为指定的镜像添加可读写层，构成新容器，但并未运行
2. docker start 为容器创建一个进程隔离空间，每一个容器只有一个
3. docker run = docker create + docker start