---
title: IrqlIoPassive4 规则（wdm）
ms.assetid: 2bdfa09d-0777-4eaf-85ff-d5accc0f31de
ms.date: 05/21/2018
description: ''
keywords:
- IrqlIoPassive4 规则（wdm）
topic_type:
- apiref
api_name:
- IrqlIoPassive4
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 398974880a1e7480133e4580531cac978fa9be6f
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968566"
---
# <a name="irqliopassive4-rule-wdm"></a>IrqlIoPassive4 规则（wdm）


**IrqlIoPassive4**规则指定仅当驱动程序在 IRQL = 被动级别执行时才调用以下例程 \_ ：

-   [**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)

-   [**IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent)

-   [**IoCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)

-   [**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent)

-   [**IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink)

-   [**IoDeassignArcName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeassignarcname)

-   [**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller)

-   [**IoDeleteSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink)

-   [**IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)

**驱动程序模型： WDM**

**找到了具有此规则的 bug 检查**： [**bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)（0x0002000D）


<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrqlIoPassive4</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">驱动程序验证程序</a>，并选择 " <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](https://docs.microsoft.com/windows-hardware/drivers/devtest/ddi-compliance-checking)">DDI 相容性检查</a>" 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile) 
[**IoCreateNotificationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent) 
[**IoCreateSynchronizationEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesynchronizationevent) 
[**IoCreateUnprotectedSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreateunprotectedsymboliclink) 
[**IoDeleteController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iodeletecontroller) 
[**IoDeleteSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletesymboliclink) 
[**IoDisconnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iodisconnectinterrupt)
 

 





