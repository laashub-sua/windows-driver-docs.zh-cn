---
title: 生成 MIP 贴图纹理的子级别
description: 生成 MIP 贴图纹理的子级别
ms.assetid: fbfb0d1b-468d-4e7f-865e-bdc7d19f5516
keywords:
- MIP map 纹理 WDK DirectX 9.0，生成子级别
- MIP 地图9.0 纹理的子层
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a55a6966a81061e7d3fa9448f160571ff4a7238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838934"
---
# <a name="generating-sublevels-of-mip-map-textures"></a>生成 MIP 贴图纹理的子级别


## <span id="ddk_generating_sublevels_of_mip_map_textures_gg"></span><span id="DDK_GENERATING_SUBLEVELS_OF_MIP_MAP_TEXTURES_GG"></span>


显示驱动程序通过设置[**DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**DWCAPS2**成员的 DDCAPS2\_CANAUTOGENMIPMAP 位，来指示支持自动生成 MIP 地图纹理的子级别。 驱动程序在[**DD\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**ddCaps**成员中指定此 DDCORECAPS 结构。 DD\_HALINFO 由驱动程序的[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)函数返回。 显示驱动程序还指示特定的 surface 格式是否支持通过设置[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)的**dwOperations**成员中的 D3DFORMAT\_OP\_AUTOGENMIPMAP 标志来自动生成子层。格式的结构。

创建纹理图面后，Direct3D 运行时会将 DDSCAPSEX （[**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))）结构的**DWCAPS3**成员的 DDSCAPS3\_AUTOGENMIPMAP 位设置为，以指示可以自动由此. 如果 Direct3D 指示某些纹理自动生成其 MIP 地图子级别，而某些纹理未自动生成，则驱动程序只能对这些纹理执行 array.blit 操作（D3DDP2OP\_TEXBLT），如下所述各种

-   驱动程序无法从自动生成 MIP 映射的源纹理 array.blit 到不会生成的目标纹理。

-   如果驱动程序从不自动生成 MIP 映射的源纹理 blits，则该驱动程序仅 blits 最顶层的匹配级别。 将忽略源纹理的子级别。 可以生成目标子级别。

-   同样，如果驱动程序 blits 从源到目标的纹理，这两种类型都自动生成 MIP maps，则驱动程序仅 blits 最顶层的匹配级别。 将忽略源纹理的子级别。 可以生成目标子级别。

为了生成 MIP 地图纹理的子级别，驱动程序将接收 D3DDP2OP\_GENERATEMIPSUBLEVELS 命令和[**D3DHAL\_DP2GENERATEMIPSUBLEVELS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2generatemipsublevels)结构。 为了接收此命令，纹理的表面格式必须公开 D3DFORMAT\_OP\_AUTOGENMIPMAP 标志。

对于[驱动程序管理的资源](driver-managed-resources.md)，当驱动程序逐出并替换视频内存中的资源时，驱动程序必须使用最后一次设置的筛选器类型来自动生成子级别。 因为 Direct3D 不控制资源的逐出和替换，所以 Direct3D 不会向驱动程序发送 D3DDP2OP\_GENERATEMIPSUBLEVELS 命令。

Direct3D 运行时无法调用驱动程序的[*DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)函数，也无法使用任何其他[DDI](direct3d-driver-ddi.md)来访问自动生成的 MIP 地图纹理的子级别。 这意味着，自动生成的 MIP 地图纹理的子级别（如轻型 MIP 地图纹理）是 "隐式的"，可根据需要由驱动程序指定。 驱动程序无需指定 "complete" 表面数据结构。 但请注意，Direct3D 必须能够调用驱动程序的*DdLock*或[*DdBlt*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数，发送 D3DDP2OP\_BLT 命令，或使用任何其他 DDI （仅适用于[驱动程序托管的纹理](driver-managed-textures.md)、动态纹理或仅供应商特定格式）若要访问自动生成的 MIP 地图纹理的顶级。

 

 





