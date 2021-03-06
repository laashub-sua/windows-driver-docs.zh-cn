---
title: 空闲状态和活动电源的 GPU 电源管理
description: 一种 GPU 电源管理基础结构，它允许 Windows 显示驱动程序模型（WDDM）1.2 及更高版本的驱动程序管理单个设备或一组设备的强大功能。
ms.assetid: F8096F7E-39EA-45CB-8A1C-60A7A298AFEC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88727c350c3d4c094cf0c0019a05d8be8b8bfd8
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967964"
---
# <a name="gpu-power-management-of-idle-states-and-active-power"></a>空闲状态和活动电源的 GPU 电源管理


从 Windows 8 开始，可以使用可选的 GPU 电源管理基础结构，使 Windows 显示驱动程序模型（WDDM）1.2 和更高版本的驱动程序可以管理单个设备或一组设备的强大功能。 此基础结构提供了一种标准化机制，可支持与 Windows 协作的 F 状态和 P 状态电源管理。

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现**：可选

** [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**：**设备 .。。RuntimePowerMgmt**


 

## <a name="span-idgpu_power_management_device_driver_interface__ddi_spanspan-idgpu_power_management_device_driver_interface__ddi_spanspan-idgpu_power_management_device_driver_interface__ddi_spangpu-power-management-device-driver-interface-ddi"></a><span id="GPU_power_management_device_driver_interface__DDI_"></span><span id="gpu_power_management_device_driver_interface__ddi_"></span><span id="GPU_POWER_MANAGEMENT_DEVICE_DRIVER_INTERFACE__DDI_"></span>GPU 电源管理设备驱动程序接口（DDI）


从 Windows 8 开始，这些新的和更新的函数和结构可用于显示微型端口驱动程序，以转换电源组件的状态并与 Microsoft DirectX 图形内核子系统交流电源事件。

-   [*DxgkCbCompleteFStateTransition*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_completefstatetransition)
-   [*DxgkCbPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_powerruntimecontrolrequest)
-   [*DxgkCbSetPowerComponentActive*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentactive)
-   [*DxgkCbSetPowerComponentIdle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentidle)
-   [*DxgkCbSetPowerComponentLatency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentlatency)
-   [*DxgkCbSetPowerComponentResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_setpowercomponentresidency)
-   [*DxgkDdiPowerRuntimeControlRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)
-   [*DxgkDdiSetPowerComponentFState*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate)
-   [**DXGK \_ DRIVERCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)
-   [**DXGK \_ 电源 \_ 组件 \_ 标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_flags)
-   [**DXGK \_ 电源 \_ 组件 \_ 映射**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_component_mapping)
-   [**DXGK \_ 电源 \_ 组件 \_ 类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_power_component_type)
-   [**DXGK \_ POWER \_ RUNTIME \_ 组件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_power_runtime_component)
-   [**DXGK \_ QUERYADAPTERINFOTYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_queryadapterinfotype)
-   [**DXGKARG \_ QUERYADAPTERINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryadapterinfo)
-   [**DXGK \_ QUERYSEGMENTOUT3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_querysegmentout3)

## <a name="span-idgpu_power_management_scenariosspanspan-idgpu_power_management_scenariosspanspan-idgpu_power_management_scenariosspangpu-power-management-scenarios"></a><span id="GPU_power_management_scenarios"></span><span id="gpu_power_management_scenarios"></span><span id="GPU_POWER_MANAGEMENT_SCENARIOS"></span>GPU 电源管理方案


Gpu 和显示屏幕是便携式计算机、移动设备和台式计算机中最大的电源使用者。

下面是用于减少能耗和延长电池寿命的关键电源管理方案：

-   Mobile 外形设备可以进入空闲状态并节省电能，因为单个系统组件在未使用时将关闭。
-   基于芯片（SoC）的设备上的 Windows 系统的行为类似于消费者设备和移动电话，它们会在需要时立即打开，从而节省能源。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit) **RuntimePowerMgmt**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





