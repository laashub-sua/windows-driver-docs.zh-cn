---
title: Bug 检查 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
description: SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD bug 检查的值为0x000000D4。 这表明驱动程序在卸载之前未取消挂起的操作。
ms.assetid: 4c0e69d1-737c-4dd7-b52a-4cd5eeadcbb9
keywords:
- Bug 检查 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 80f123048cf7401d5631084a5c9a7822b8cff495
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534566"
---
# <a name="bug-check-0xd4-system_scan_at_raised_irql_caught_improper_driver_unload"></a>Bug 检查0xD4： \_ \_ 引发的 IRQL 系统扫描 \_ \_ \_ 捕获到不 \_ 正确的 \_ 驱动程序 \_ 卸载


出现系统 \_ 扫描 \_ 时 \_ 引发的 \_ IRQL，出现不 \_ \_ 正确 \_ 的驱动程序 \_ 卸载 bug 检查的值为0x000000D4。 这表明驱动程序在卸载之前未取消挂起的操作。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="system_scan_at_raised_irql_caught_improper_driver_unload-parameters"></a>系统 \_ 扫描 \_ \_ 引发的 \_ IRQL \_ 捕获到不 \_ 正确的 \_ 驱动程序 \_ 卸载参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>引用时为 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0：</strong>读取</p>
<p><strong>1：</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>对引用的内存进行寻址</p></td>
</tr>
</tbody>
</table>

 

如果可以识别负责错误的驱动程序，则会在蓝色屏幕上打印其名称，并将其存储在内存中的位置（PUNICODE \_ 字符串） **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

此驱动程序在卸载之前未能取消后备链表列表、Dpc、工作线程或其他此类项。 然后，系统尝试访问驱动程序以前在引发的 IRQL 时的位置。

<a name="resolution"></a>解决方法
----------

若要开始调试，请使用内核调试器获取堆栈跟踪： [**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因，然后使用[**Kb （显示 stack Backtrace）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令获取堆栈跟踪。 如果已确定导致错误的驱动程序，请激活驱动程序验证程序并尝试复制此 bug。

有关[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)的完整详细信息，请参阅 Windows 驱动程序工具包。

 

 




