---
title: 接收段合并的示例
description: 本部分通过使用按顺序接收并在单个延迟的过程调用（DPC）中处理的段的示例来说明合并算法。
ms.assetid: BC4C3216-683B-4E86-B2DF-F75FFCA7DACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b953da7fd4c14447be22a63df76ff4ea3996d61b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834754"
---
# <a name="examples-of-receive-segment-coalescing"></a>接收段合并的示例


本部分通过使用按顺序接收并在单个延迟的过程调用（DPC）中处理的段的示例来说明合并算法。

此页使用 X 和 X 来标记连续段。 所有其他段和单个合并单元（SCU）字段如[用于合并 Tcp/ip 段的规则](rules-for-coalescing-tcp-ip-packets.md)中所述。

## <a name="example-1-data-segments"></a>示例1：数据段


### <a name="segment-description"></a>段说明

将处理属于同一 TCP 连接的10个连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
### <a name="result"></a>结果

单个 SCU 由10个段组成。 这在单个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中被指示为单个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)。

## <a name="example-2-data-segments-followed-by-an-exception-followed-by-data-segments"></a>示例2：数据段，后跟异常，后跟数据段


### <a name="segment-description"></a>段说明

5处理属于同一 TCP 连接的连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
第六段是带有 TCP SACK 选项的重复 ACK 段，并基于规则编号3生成一个例外，[用于合并 Tcp/ip 段](rules-for-coalescing-tcp-ip-packets.md)。

**请注意**  在这种情况下，处理 TCP 选项的异常规则优先，因此会替代合并规则。

 

2将处理属于同一 TCP 连接的连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
### <a name="result"></a>结果

单个 SCU 由前5个段组成。 第六段不形成 SCU。

第七个和第8个段共同构成了 SCU。

[**Net\_缓冲器\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)链使用三个**网络\_\_缓冲区**指示，其中每个都有一个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)。 将保留已接收段的顺序。

## <a name="example-3-data-segments-followed-by-multiple-window-updates"></a>示例3：数据段，后跟多个窗口更新


### <a name="segment-description"></a>段说明

5处理属于同一 TCP 连接的连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
第六段是一个纯确认，它是具有 SEG 的窗口更新。WND = 65535，如以下流程图中所示。

![描述用于将段与 tcp 时间戳选项合并的规则的流程图](images/rsc-rules2.png)

第7段是一个纯确认，它是具有 SEG 的窗口更新。WND = 131070，如同一流程图中所示。

### <a name="result"></a>结果

单个 SCU 是由7段组成的。 这在单个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中被指示为单个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)。

SCU。WND = 131070，并且根据该值更新校验和。

## <a name="example-4-piggybacked-acks-mixed-with-data-segments"></a>示例4：与数据段混合的 Piggybacked Ack


### <a name="segment-description"></a>段说明

3处理属于同一 TCP 连接的连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
2将处理属于同一 TCP 连接的连续段。 对于每个条件均为 true：

-   X '。SEQ = = X。 NXT

-   X'SEQ &gt;

-   X '。ACK = = X。 ACK

这些段都不会产生异常。
### <a name="result"></a>结果

单个 SCU 是由5段组成的。 这在单个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)中被指示为单个[**网络\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)。 SCU。ACK 设置为最后一个 SEG。

 

 





