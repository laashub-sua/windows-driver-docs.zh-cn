---
title: GetDisplayConfigBufferSizes 摘要和方案
description: GetDisplayConfigBufferSizes 摘要和方案
ms.assetid: b0d14ba7-fe61-49e9-81c5-097e6e07a51a
keywords:
- 连接显示 WDK Windows 7 显示 GetDisplayConfigBufferSizes 在 CCD Api
- 连接显示 WDK Windows Server 2008 R2 显示 GetDisplayConfigBufferSizes 在 CCD Api
- 配置显示 WDK Windows 7 显示 GetDisplayConfigBufferSizes 在 CCD Api
- 配置显示 WDK Windows Server 2008 R2 显示 GetDisplayConfigBufferSizes 在 CCD Api
- CCD 概念 WDK Windows 7 显示 GetDisplayConfigBufferSizes
- CCD 概念 WDK Windows Server 2008 R2 显示 GetDisplayConfigBufferSizes
- GetDisplayConfigBufferSizes WDK Windows 7 显示
- GetDisplayConfigBufferSizes WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd7f0b58de1cdd9fba79e238ffa530e4e439b16d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379986"
---
# <a name="getdisplayconfigbuffersizes-summary-and-scenarios"></a>GetDisplayConfigBufferSizes 摘要和方案


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

以下部分汇总了如何使用调用方[ **GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes) CCD 函数，并提供了有关使用方案**GetDisplayConfigBufferSizes**。

### <a name="span-idgetdisplayconfigbuffersizessummaryspanspan-idgetdisplayconfigbuffersizessummaryspangetdisplayconfigbuffersizes-summary"></a><span id="getdisplayconfigbuffersizes_summary"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SUMMARY"></span>GetDisplayConfigBufferSizes 摘要

可以使用调用方[ **GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)若要获取调用方需要的信息[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)CCD 函数。

### <a name="span-idgetdisplayconfigbuffersizesscenariosspanspan-idgetdisplayconfigbuffersizesscenariosspangetdisplayconfigbuffersizes-scenarios"></a><span id="getdisplayconfigbuffersizes_scenarios"></span><span id="GETDISPLAYCONFIGBUFFERSIZES_SCENARIOS"></span>GetDisplayConfigBufferSizes 方案

[**GetDisplayConfigBufferSizes** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-getdisplayconfigbuffersizes)调用之前，始终将调用[ **QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)。

 

 





