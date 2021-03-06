---
title: 视频微型端口驱动程序中的电源管理和 PnP （XDDM）
description: 视频微型端口驱动程序中的电源管理和即插即用（Windows 2000 模型）
ms.assetid: e5b2ac53-e492-43de-91a3-5b02c26ee9a3
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，即插即用
- 视频微型端口驱动程序 WDK Windows 2000，电源管理
- 即插即用 WDK 视频微型端口
- PnP WDK 视频微型端口
- 电源管理 WDK 视频微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 245bbfbc216941fe009476bea7bef558b21fefb6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829786"
---
# <a name="power-management-and-plug-and-play-in-video-miniport-drivers-windows-2000-model"></a>视频微型端口驱动程序中的电源管理和即插即用（Windows 2000 模型）


## <span id="ddk_plug_and_play_and_power_management_in_video_miniport_drivers_windo"></span><span id="DDK_PLUG_AND_PLAY_AND_POWER_MANAGEMENT_IN_VIDEO_MINIPORT_DRIVERS_WINDO"></span>


所有 Windows 2000 和更高版本的微型端口驱动程序都必须支持即插即用和电源管理。 这包括枚举子设备（如*DDC*监视器、集成线路（I i2c）设备和辅助适配器）的功能。

视频端口驱动程序管理微型端口驱动程序的大部分 PnP 要求，包括创建 FDO （功能设备对象）并在代表微型端口驱动程序的情况下接收和调度 PnP 特定的 IRP 代码（请参阅[IRP 主要功能代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)）.

微型端口驱动程序必须实现以下功能，以支持 PnP 和电源管理：

[*HwVidSetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_set)

[*HwVidGetPowerState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_power_get)

[*HwVidGetVideoChildDescriptor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)

当系统正在运行时，不能从系统中删除旧微型端口驱动程序的图形适配器，也不能在添加到正在运行的系统时，自动检测到旧版微型端口驱动程序。

有关检测适配器的子设备并与之通信的详细信息，请参阅[显示适配器的子设备（Windows 2000 型号）](child-devices-of-the-display-adapter--windows-2000-model-.md) 。 有关即插即用驱动程序的常规信息，请参阅[即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。

 

 





