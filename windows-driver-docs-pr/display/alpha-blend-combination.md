---
title: Alpha 混合组合
description: Alpha 混合组合
ms.assetid: 567810da-ad8d-4ceb-b914-868632384d09
keywords:
- alpha-blend 组合 WDK DirectX VA
- 混合图片 WDK DirectX VA
- alpha-blend 组合 WDK DirectX VA，关于 alpha blend 组合
- 混合图片 WDK DirectX VA，关于 alpha blend 组合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f553355f3f661cb8bc1df711e399e0c454f605cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839074"
---
# <a name="alpha-blend-combination"></a>Alpha 混合组合


## <span id="ddk_alpha_blend_combination_gg"></span><span id="DDK_ALPHA_BLEND_COMBINATION_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)等于3时，指定的操作是一个 alpha blend 组合。 Alpha blend 组合采用最后加载的 alpha blend 源信息，并将其与参考图片组合在一起，创建要显示的混合图片。

由[**DXVA\_BufferDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)结构的**dwTypeIndex**成员指定的 alpha blend 组合缓冲区用于根据源图片和 alpha 混合信息生成混合图片。 如果源和目标图片的格式不是4:4:4，则会将 AYUV alpha 混合表面或等效项的每个第二个示例（例如，第一个、第三个、第五个和第三个）与）源色度信息在垂直或水平方向上（如果适用），以产生混合结果。

以下结构用于实现 alpha blend 组合。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription" data-raw-source="[&lt;strong&gt;DXVA_BufferDescription&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)"><strong>DXVA_BufferDescription</strong></a></p></td>
<td align="left"><p>指定要使用的 alpha blend 组合缓冲区。 此缓冲区控制来自源图片和 alpha 混合信息的混合图片的生成。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination" data-raw-source="[&lt;strong&gt;DXVA_BlendCombination&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_blendcombination)"><strong>DXVA_BlendCombination</strong></a></p></td>
<td align="left"><p>指定如何从 alpha blend 组合缓冲区生成混合图片。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine" data-raw-source="[&lt;strong&gt;DXVA_ConfigAlphaCombine&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)"><strong>DXVA_ConfigAlphaCombine</strong></a></p></td>
<td align="left"><p>建立用于执行 alpha 混合组合操作的方式的配置。</p></td>
</tr>
</tbody>
</table>

 

 

 





