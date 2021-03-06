---
title: OID_WWAN_UICC_RESET
description: OID_WWAN_UICC_RESET
ms.assetid: D6654B8D-8700-437B-A944-BB273C7D31A1
keywords:
- MB UICC reset，Mobile 宽带 UICC reset，Mobile 宽带微型端口驱动程序 UICC reset
ms.date: 08/17/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e98216d93d7987aa2831ae2f9a0cd34dfcd2e27
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917006"
---
# <a name="oid_wwan_uicc_reset"></a>OID_WWAN_UICC_RESET

移动宽带主机将 OID_WWAN_UICC_RESET 发送到调制解调器微型端口适配器，以重置 UICC 智能卡，并指定重置后 UICC 的传递状态，或查询适配器的直通状态。

调制解调器小型端口驱动程序必须异步处理查询请求，最初将 NDIS_STATUS_INDICATION_REQUIRED 返回给原始请求，然后再发送包含[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)结构的[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)通知，后者又包含一个表示适配器的直通状态的[WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_reset_info)结构。

对于 set 请求，OID_WWAN_UICC_RESET 使用[NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)结构，后者又包含一个[WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_uicc_reset)结构，该结构表示主机在重置 UICC 之后为微型端口适配器指定的直通操作。 重置完成后，微型端口适配器将使用**NDIS_STATUS_WWAN_UICC_RESET_INFO**通知进行响应，该通知又包含[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)结构，以指示其传递状态。

未经请求的事件不适用。

有关传递操作和传递状态的详细信息，请参阅[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)。

## <a name="requirements"></a>要求

**版本**： Windows 10，版本 1709**头**： Ntddndis （包括 Ndis .h）

## <a name="see-also"></a>另请参阅

[NDIS_WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_uicc_reset_info)

[WWAN_UICC_RESET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_uicc_reset_info)

[NDIS_WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_uicc_reset)

[WWAN_SET_UICC_RESET](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_set_uicc_reset)

[NDIS_STATUS_WWAN_UICC_RESET_INFO](ndis-status-wwan-uicc-reset-info.md)

[MB 低级别 UICC 访问](mb-low-level-uicc-access.md)

