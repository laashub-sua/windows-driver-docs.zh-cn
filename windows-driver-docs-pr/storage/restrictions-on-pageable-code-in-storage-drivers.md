---
title: 对存储驱动程序中的可分页代码的限制
description: 对存储驱动程序中的可分页代码的限制
ms.assetid: 1958f22f-5563-41e9-9c3f-dec8a4ac80c0
keywords:
- 存储驱动程序 WDK，可分页代码限制
- 可分页代码限制 WDK 存储
- 死锁 WDK 存储
- 分页路径 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7709745645db21eedc8853e7e6068e10145478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842690"
---
# <a name="restrictions-on-pageable-code-in-storage-drivers"></a>对存储驱动程序中的可分页代码的限制


## <span id="ddk_restrictions_on_pageable_code_in_storage_drivers_kg"></span><span id="DDK_RESTRICTIONS_ON_PAGEABLE_CODE_IN_STORAGE_DRIVERS_KG"></span>


若要防止死锁，用于维护读取或写入请求的存储驱动程序的任何部分都应具有可分页的代码，也不会尝试访问可分页的内存。 这是因为驱动程序的[**DispatchRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)和[**DispatchWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程可以 &gt; 被动\_级别的 IRQL 调用，并且用于服务页错误的分页 i/o 发生在 IRQL = APC\_级别。

类似的规则适用于存储驱动程序的设备控制调度例程[**DispatchDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)，具有特定的资格。 存储驱动程序的设备控制调度例程不得包含可分页的代码或访问可分页内存。 调度例程必须能够接收适用于任意 IRQLs 的其他驱动程序的 IOCTL 请求，并将它们沿驱动程序堆栈向下传递。 驱动程序*必须*通过堆栈向下传递所有未处理的 IOCTL 请求，而不会更改该请求的 IRQL 或上下文。

但是，Microsoft 要求在被动\_级别提交所有*存储*IOCTL 请求，因此，尽管调度例程本身并不可以分页，但它可以调用可分页的子例程来处理存储的 IOCTL 请求。 这些子例程还可以访问可分页内存。

[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、重新[**初始化**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)和[**卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)这样的例程（不执行 i/o 操作，并以 IRQL = 被动\_级别运行）也可以有可分页的代码。

特别注意事项适用于在寻呼路径中管理存储设备的驱动程序。 如果驱动程序参与了页面文件的 i/o 操作，则该驱动程序位于 "分页路径" 中。 当存储驱动程序在分页路径中时，\_MJ 的 IRP\_POWER 请求的其[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程不可分页。

默认情况下，内核模式驱动程序的代码是不可分页的，并且内核模式驱动程序使用的全局内存也不能分页。 有关如何使代码可分页的详细信息，请参阅[使驱动程序代码或数据可分页](https://docs.microsoft.com/windows-hardware/drivers/kernel/making-driver-code-or-data-pageable)。

 

 




