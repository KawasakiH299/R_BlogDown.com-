---
title: KVM-Linux内核虚拟化技术
author: Xin Lu
date: '2023-08-02'
slug: []
categories: []
tags: []
---

虚拟化技术发展到今天已经非常成熟，再加上DPDK代码的开源化、KVM也好、其他Hypervisor也好，在转发性能的优化和硬件辅助虚拟化的支撑上都半斤八两，但由于KVM的开源性特性以及社区的热度，使得其在云计算领域解决方案一枝独秀。甚至，华为在其FusionSphere6.3版本也开始拥抱KVM而抛弃了Xen。要知道，华为在剑桥大学可是专门有一支团队在研究Xen虚拟化。



因为 KVM 是硬件辅助的虚拟化技术，主要负责 比较繁琐的 CPU 和内存虚拟化，而 Qemu 则负责 I/O 虚拟化，两者合作各自发挥自身的优势，相得益彰。



首先KVM（Kernel Virtual Machine）是Linux的一个内核驱动模块，它能够让Linux主机成为一个Hypervisor（虚拟机监控器）。在支持VMX（Virtual Machine Extension）功能的x86处理器中，Linux在原有的用户模式和内核模式中新增加了客户模式，并且客户模式也拥有自己的内核模式和用户模式，虚拟机就是运行在客户模式中。KVM模块的职责就是打开并初始化VMX功能，提供相应的接口以支持虚拟机的运行。

QEMU（quick emulator)本身并不包含或依赖KVM模块，而是一套由Fabrice Bellard编写的模拟计算机的自由软件。QEMU虚拟机是一个纯软件的实现，可以在没有KVM模块的情况下独立运行，但是性能比较低。QEMU有整套的虚拟机实现，包括处理器虚拟化、内存虚拟化以及I/O设备的虚拟化。QEMU是一个用户空间的进程，需要通过特定的接口才能调用到KVM模块提供的功能。从QEMU角度来看，虚拟机运行期间，QEMU通过KVM模块提供的系统调用接口进行内核设置，由KVM模块负责将虚拟机置于处理器的特殊模式运行。QEMU使用了KVM模块的虚拟化功能，为自己的虚拟机提供硬件虚拟化加速以提高虚拟机的性能。

KVM只模拟CPU和内存，因此一个客户机操作系统可以在宿主机上跑起来，但是你看不到它，无法和它沟通。于是，有人修改了QEMU代码，把他模拟CPU、内存的代码换成KVM，而网卡、显示器等留着，因此QEMU+KVM就成了一个完整的虚拟化平台。

KVM只是内核模块，用户并没法直接跟内核模块交互，需要借助用户空间的管理工具，而这个工具就是QEMU。KVM和QEMU相辅相成，QEMU通过KVM达到了硬件虚拟化的速度，而KVM则通过QEMU来模拟设备。对于KVM来说，其匹配的用户空间工具并不仅仅只有QEMU，还有其他的，比如RedHat开发的libvirt、virsh、virt-manager等，QEMU并不是KVM的唯一选择。

所以简单直接的理解就是：QEMU是个计算机模拟器，而KVM为计算机的模拟提供加速功能。



**libvirt实际上是一个连接底层Hypervisor与上层应用的中间适配层。**

1. Libvirt：Libvirt是一个开源的管理工具集和库，用于管理和监控虚拟化平台。它提供了一套统一的API和管理工具，用于管理不同的虚拟化技术，如KVM、QEMU、Xen、LXC等。Libvirt允许用户通过统一的接口来管理虚拟机、存储、网络等资源，并提供了多种编程语言的API供开发者使用。
2. Hypervisor：Hypervisor（也称为虚拟机监视器或虚拟机管理程序）是一种软件或硬件层，负责管理和运行虚拟机。Hypervisor直接与物理硬件交互，并将物理资源（如CPU、内存、存储）虚拟化为多个虚拟机，从而使每个虚拟机能够运行独立的操作系统和应用程序。常见的Hypervisor包括KVM、VMware ESXi、Hyper-V等





KVM虚拟机要使用快照功能，磁盘格式必须为qcow2

```
[root@localhost qemu]# virsh snapshot-create test01
//对虚拟机test01创建快照
[root@localhost qemu]# virsh snapshot-list test01
//查看快照信息
 名称               生成时间              状态
------------------------------------------------------------
 1560191837           2019-06-11 02:37:17 +0800 shutoff
[root@localhost qemu]# virsh snapshot-revert test01 1560191837
//恢复虚拟机状态至1560191837
[root@localhost qemu]# virsh snapshot-delete test01 1560191837
//删除快照

快照存放路径
/var/lib/libvert/qemu/snapshot/
```

