---
title: IRP_MJ_DEVICE_CONTROL （IFS）
description: IRP\_MJ\_DEVICE\_CONTROL
ms.assetid: 7a7f7372-ed69-42c1-95e2-b5a593d77d22
keywords:
- IRP_MJ_DEVICE_CONTROL 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_DEVICE_CONTROL
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8eee8a6cc6521adf0a25dfec1c110e66ff4d0ab
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141335"
---
# <a name="irp_mj_device_control-ifs"></a>IRP \_ MJ \_ 设备 \_ 控制（IFS）


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 设备 \_ 控制请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 通常，此 IRP 代表用户模式应用程序发送，该应用程序已调用 Microsoft Win32 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)函数或代表已调用[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)的内核模式组件。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定是否已在打开的句柄上发出请求。 如果是这种情况，则文件系统驱动程序应将 IRP 传递到用于装入卷的存储设备的设备驱动程序。 否则，该驱动程序应该会使 IRP 失败。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应执行任何所需的处理，并根据筛选器的性质，完成 IRP，或将其向下传递到堆栈上的下一个较低版本的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序为给定的 IRP 调用[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的*IrpSp*[**堆栈位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。 （IRP 显示为*irp*。）驱动程序可以使用 IRP 的下列成员中设置的信息，并使用 IRP 堆栈位置来处理设备控制请求：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
指向系统提供的输入缓冲区的指针，该缓冲区将传递给目标设备的设备驱动程序。 用于方法 \_ 缓冲或方法 \_ 直接 i/o。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--iostatus"></a>*Irp- &gt; IoStatus*  
指向[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)的*IoStatusBlock*参数说明。

<a href="" id="irp--mdladdress"></a>*Irp- &gt; MdlAddress*  
描述要传递到目标设备的设备驱动程序的输出缓冲区的内存描述符列表（MDL）的地址。 用于方法 \_ 直接 i/o。 此参数是否是必需的取决于特定的 i/o 控制代码。

<a href="" id="irp--requestormode"></a>*Irp- &gt; irp->requestormode*  
指示请求操作的进程的执行模式，可以是**KernelMode**或**UserMode**。

<a href="" id="irp--userbuffer"></a>*Irp- &gt; UserBuffer*  
一个指针，指向要传递给目标设备的设备驱动程序的调用方提供的输出缓冲区。 用于方法 \_ 缓冲或方法 \_ 都不是 i/o。 此参数是可选的还是必需的取决于特定的 i/o 控制代码。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt; FileObject*  
指向与*DeviceObject*关联的文件对象的指针。

*IrpSp- &gt; FileObject*参数包含指向**RelatedFileObject**字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的**RelatedFileObject**字段在 \_ 处理 IRP \_ MJ 设备控件期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt; MajorFunction*  
指定 IRP \_ MJ \_ 设备 \_ 控制。

<a href="" id="irpsp--parameters-deviceiocontrol-inputbufferlength"></a>*IrpSp- &gt; DeviceIoControl. InputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位） * &gt;AssociatedIrp.SystemBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-iocontrolcode"></a>*IrpSp- &gt; DeviceIoControl. IoControlCode*  
要传递给目标设备的设备驱动程序的 IOCTL 函数代码。

有关 IOCTL 请求的详细信息，请参阅 Microsoft Windows SDK 文档中的使用*内核模式体系结构指南*中的[i/o 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)和 "设备输入和输出控制代码"。

<a href="" id="irpsp--parameters-deviceiocontrol-outputbufferlength"></a>*IrpSp- &gt; DeviceIoControl. OutputBufferLength*  
Irp 所指向的缓冲区大小（以字节为单位）。 * &gt; UserBuffer*。

<a href="" id="irpsp--parameters-deviceiocontrol-type3inputbuffer"></a>*IrpSp- &gt; DeviceIoControl. Type3InputBuffer*  
使用方法的内核模式请求的输入缓冲区 \_ 。

## <a name="see-also"></a>另请参阅


[**IO \_ 堆栈 \_ 位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

[**IoGetCurrentIrpStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IoGetFunctionCodeFromCtlCode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetfunctioncodefromctlcode)

[**IRP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设备 \_ 控制（WDK 内核参考）**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)

[使用 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)

[**ZwDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566441)

 

 






