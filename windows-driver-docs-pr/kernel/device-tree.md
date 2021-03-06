---
title: 设备树
description: 设备树
ms.assetid: 3220389a-06cc-4a43-8164-b785d1a16365
keywords:
- devnodes WDK 即插即用
- 虚幻设备 WDK
- 即插即用 WDK 内核，设备树
- 插 WDK 内核，设备树
- 删除关系 WDK 即插即用
- 弹出关系 WDK 即插即用
- 设备树 WDK 即插即用
- 树 WDK 即插即用
- 设备节点 WDK 即插即用
- 子 WDK 即插即用设备
- 层次结构 WDK 即插即用
- WDK 即插即用的关系
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58a2fd8e0044f23057831c2a5eda0d958cb2c9d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385008"
---
# <a name="device-tree"></a>设备树





PnP 管理器维护跟踪系统中的设备的设备树。 下图显示了示例系统配置的设备树。

![示例即插即用设备树](images/devtree.png)

设备树包含系统上存在的设备的相关信息。 PnP 管理器时在计算机启动时，使用驱动程序和其他组件中的信息和更新树，添加或删除设备时生成此树。

设备树的每个节点都称为一个设备节点中，或*devnode*。 Devnode 组成*设备对象*设备的驱动程序，以及由系统维护的内部信息。 因此，没有为每个 devnode*设备堆栈*。

已要求总线驱动程序 PnP 管理器提供有关其子级的列表使用的设备[ **IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)请求。 总线驱动程序确定其根据其总线协议的子级的列表。 例如， [Windows ACPI 驱动程序](acpi-driver.md)、 Acpi.sys，看起来在 ACPI 名称空间，PCI 驱动程序查询 PCI 配置空间，和 USB 集线器驱动程序遵循 USB 总线协议。

设备树是分层的与表示为"子级"总线适配器、 控制器或其他的总线上的设备*总线设备*。 （总线设备为其他物理、 逻辑，或虚拟设备可以附加到任何设备。）您可以看到在设备树中使用设备管理器并选择视图选项，您可以通过连接来查看设备的设备的层次结构。

设备树的层次结构反映了在其中的设备连接在计算机中的结构。 PnP 管理器使用此层次结构，如它所管理设备。 例如，如果用户请求时要拔出 USB 控制器从上一图中表示的计算机，即插即用管理器确定此操作会导致其他的三个设备，也被拔出设备树中 (USB 集线器、 游戏杆和照相机）。 当 PnP 管理器查询来确定它是否可以安全地删除控制器的 USB 控制器的驱动程序时，也会查询该控制器的后代 （中心、 游戏杆和照相机） 的驱动程序。

设备树是动态的。 添加和从计算机中删除设备时，（以及驱动程序） 的即插即用管理器维护系统上的设备当前的图片。

除了设备树中表示的层次结构关系在计算机上的设备之间有其他关系。 其中包括*删除关系*并*弹出关系*。 请参阅的参考页[ **IRP\_MN\_查询\_设备\_关系**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)有关详细信息。

只不过总线设备配置的任何其子设备之前，不能进行任何假设生成设备树顺序。 例如，不应假定一个总线上的另一台设备之前配置的总线上的设备。

 

 




