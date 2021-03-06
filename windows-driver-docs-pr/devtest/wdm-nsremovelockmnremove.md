---
title: NsRemoveLockMnRemove 规则（wdm）
description: '\_ \_ 当 \_ \_ 使用 MinorFunction IRP \_ MN \_ REMOVE 设备处理 IRP MJ PNP 时，NsRemoveLockMnRemove 规则将验证驱动程序是否未返回状态 \_ 。 此规则仅适用于 FDO 和 FIDO 驱动程序。'
ms.assetid: 1151343D-9CFD-4808-A885-D477F199C004
ms.date: 05/21/2018
keywords:
- NsRemoveLockMnRemove 规则（wdm）
topic_type:
- apiref
api_name:
- NsRemoveLockMnRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb997e35cd930cb9b1a20bd94a9f8b3e051d3c95
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917264"
---
# <a name="nsremovelockmnremove-rule-wdm"></a>NsRemoveLockMnRemove 规则（wdm）


**NsRemoveLockMnRemove** \_ \_ 当 \_ \_ 使用 MINORFUNCTION IRP \_ MN \_ REMOVE 设备处理 IRP MJ PNP 时，NsRemoveLockMnRemove 规则将验证驱动程序是否未返回状态 \_ 。 此规则仅适用于 FDO 和 FIDO 驱动程序。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>NsRemoveLockMnRemove</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**IoAcquireRemoveLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)
 

 





