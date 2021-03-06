---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS 是一种 TLV，其中包含 Equals （SAE）身份验证失败错误状态的同时身份验证。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_SAE_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d6ff2992c617a0b486db8023ec1f42682044fb42
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916834"
---
# <a name="wdi_tlv_sae_status"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**是一种 TLV，其中包含 EQUALS （SAE）身份验证失败错误状态的同时身份验证。

此 TLV 用于[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)和[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)的负载数据中的命令参数。

## <a name="tlv-type"></a>TLV 类型

0x14C

## <a name="length"></a>长度

UINT32 的大小（以字节为单位）。

## <a name="values"></a>值

| 类型 | 说明 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) | SAE authentication 失败错误状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903**支持的最低服务器**： Windows server 2016**标头**： Wditypes. hpp
