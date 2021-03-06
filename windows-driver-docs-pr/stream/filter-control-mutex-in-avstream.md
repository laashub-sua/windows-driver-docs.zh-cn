---
title: AVStream 中的筛选器控件互斥
description: AVStream 中的筛选器控件互斥
ms.assetid: 402795a0-e567-4e7e-a7d8-b2ce29ffb8fd
keywords:
- 筛选器控件 mutex WDK AVStream
- AVStream mutex WDK
- mutex WDK AVStream
- 同步 WDK AVStream
- 状态转换 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 598698c94e317b226cc55729cb8d99a229d2f84f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834397"
---
# <a name="filter-control-mutex-in-avstream"></a>AVStream 中的筛选器控件互斥





每个 AVStream 筛选器实例都有一个关联的筛选器控件互斥体。 此 mutex 用于同步从筛选器向下到各个 pin 的对象层次结构的访问。 创建和销毁筛选器和 pin 将与此 mutex 同步。

在持有筛选器控件互斥体时，对象层次结构保证*只*从特定筛选器实例稳定。 因此，微型驱动程序必须先获取筛选器控件互斥体，然后再使用 **Ks***xxx***GetFirstChild ** * * Xxx 和 **ks***xxx***GetNextSibling * **

筛选器控件 mutex 还用于同步状态转换。

AVStream 在处理要求层次结构保持稳定的属性（例如在执行描述符修改时）时，将获取筛选器控件互斥体。

请注意，单个筛选器控件互斥体用于每个筛选器下的对象层次结构。 这意味着，当微型驱动程序调用带有固定对象的函数时，pin 对象将使用其父的筛选器控件互斥体。

当调用以下微型驱动程序提供的例程时，AVStream 代表微型驱动程序保存筛选器控件互斥体：

-   [*AVStrMiniFilterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterirp)

-   [*AVStrMiniFilterClose*](https://docs.microsoft.com/previous-versions/ff556307(v=vs.85))

-   [*AVStrMiniPinCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinirp)

-   [*AVStrMiniPinClose*](https://docs.microsoft.com/previous-versions/ff556329(v=vs.85))

-   [*AVStrMiniPinConnect*](https://docs.microsoft.com/previous-versions/ff556332(v=vs.85))

-   [*AVStrMiniPinDisconnect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinvoid)

-   [*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)

-   [*AVStrMiniPinSetDeviceState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdevicestate)

与设备互斥体类似，不能以递归方式获取筛选器控件互斥体。 例如，如果 AVStream 在线程 A 的上下文中对*Create*调度发出了一个微型驱动程序的回调，并且该微型驱动程序稍后尝试从线程 a 中获取互斥体，则会将死锁与自身串接。

如果执行以下操作之一，则会发生死锁：

-   尝试从处理例程中获取筛选器控件互斥体。

-   尝试从睡眠或唤醒回调内获取筛选器控件互斥体。

若要操作筛选器控件互斥体，请使用以下函数：

[**KsAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksacquirecontrol)、 [**KsFilterAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilteracquirecontrol)、 [**KsPinAcquireControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquirecontrol)、 [**KsReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksreleasecontrol)、 [**KsFilterReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterreleasecontrol)、 [**KsPinReleaseControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspinreleasecontrol)

 

 




