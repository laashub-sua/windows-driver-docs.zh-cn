---
title: 流同步
description: 流同步
ms.assetid: bbf589f1-ca4b-41a2-970d-b31c7761eb1a
keywords:
- 同步 WDK DVD 解码器
- 流同步 WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cbcbe2183865a56b20e51b71950953338ed36df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561875"
---
# <a name="stream-synchronization"></a>流同步





可能的两个或多个流组成 DVD 的数据流输入。 Stream 类驱动程序可以处理同步以透明方式代表 DVD 解码器微型驱动程序。 有关详细信息，请参阅[微型驱动程序同步](minidriver-synchronization.md)。 编程人员仍必须注意的几个因素会影响 DVD 流，包括：

-   音频流必须提供主时钟，并且必须合成时钟时没有任何数据。 当音频数据停止时，音频流使用基于速率的匹配和时钟频率，所返回的系统时钟[ **KeQueryPerformanceCounter**](https://msdn.microsoft.com/library/windows/hardware/ff553053)。 所有其他流必须作为对音频的从属项。 也就是说，它们同步到音频流其性能。

-   必须在用户模式下支持软件音频解码器。 时钟转发器 DirectShow 筛选器将 DirectShow 时钟转发给微型驱动程序。 这是透明的微型驱动程序。

-   解码器不应主要针对基本流 (PES) 标头中使用的时间戳。

-   同步过程中不使用系统时钟引用 (SCRs)。 DVD 包的 SCR 字段设置为零，因为 Microsoft 的 DVD 体系结构为音频和视频同步使用的"主时钟"模式。

-   微型驱动程序看不到时间戳不连续性。 DVD 导航器/拆分器可以连续所有时间戳。

如果解码器提供音频和视频解码的功能，解码器可能硬件同步仅当使用作为系统主时钟打开音频流。 如果音频流不是主时钟，视频流必须同步到的流类主时钟的视频解码。

 

 



