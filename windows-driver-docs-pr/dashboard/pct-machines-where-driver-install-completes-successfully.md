---
title: 驱动程序安装过程成功完成的计算机的百分比
description: 该度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序的计算机所占的百分比
ms.topic: article
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: d90a27a98cdf940469a11066070a0aff0ed00d0f
ms.sourcegitcommit: d7b5e6049db3109fdcbe83279875f24f3fa6acdd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "84108606"
---
# <a name="percent-of-machines-where-the-driver-install-process-completes-successfully"></a>驱动程序安装过程成功完成的计算机的百分比

## <a name="description"></a>说明

当未能正确安装驱动程序时，目标组件会失去功能并阻止用户访问组件功能。 用户必须解决该问题以重新获取功能。 PNP 错误代码列表位于[设备管理器问题代码](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)和 [Windows 支持](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|展开|
|时间段|30 天滑动窗口|
|度量标准|计算机的聚合|
|最小总体数量|100 台计算机|
|通过标准|>= 95% 的计算机已成功安装驱动程序|
|已启用队列|是|
|每队列最小总体数量|500 台计算机|
|度量 ID|10042840|

## <a name="calculation"></a>计算

1. 该度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序的计算机所占的百分比。
2. 成功安装数 = 计数（包含成功 PNP 事件的计算机数）
3. 总安装数 = 计数（启动驱动程序安装过程的计算机数）

### <a name="final-calculation"></a>最终计算

PNP 成功率 = 成功安装数/总安装数
