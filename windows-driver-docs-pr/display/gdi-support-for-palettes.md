---
title: 调色板的 GDI 支持
description: 调色板的 GDI 支持
ms.assetid: 8c6ebf1e-6c83-45d9-bf83-f0684d28fc32
keywords:
- DrvEnablePDEV
- GDI WDK Windows 2000 显示颜色
- 图形驱动程序 WDK Windows 2000 显示颜色
- 颜色管理 WDK GDI
- 显示调色板 WDK Windows 2000
- 绘制 WDK GDI，颜色
- DrvSetPalette
- 颜色索引 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e700bcc35b583dfc7d0dfda679a225c74395c98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358654"
---
# <a name="gdi-support-for-palettes"></a>调色板的 GDI 支持


## <span id="ddk_gdi_support_for_palettes_gg"></span><span id="DDK_GDI_SUPPORT_FOR_PALETTES_GG"></span>


GDI 可以完成大部分调色板管理方面的工作。 当调用 GDI [ **DrvEnablePDEV** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvenablepdev)函数，该驱动程序返回其默认调色板 GDI 作为的一部分[ **DEVINFO** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构。 该驱动程序必须创建使用此调色板[ **EngCreatePalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)函数。

调色板有效地将映射的 32 位*颜色索引*为 24 位的 RGB 颜色值，这是 GDI 使用调色板的方法。 驱动程序指定其调色板，因此 GDI 可以确定如何将不同颜色索引将显示在设备上。

只要它使用驱动程序不需要处理的大多数调色板操作和计算[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj) GDI 提供。

如果设备支持的可修改的调色板，它应实现该函数[ **DrvSetPalette**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)。 GDI 调用*DrvSetPalette*时应用程序更改控制板的设备，并将生成新的调色板传递给驱动程序。 该驱动程序应设置其内部硬件调色板以尽可能接近地匹配新的调色板。

下表中列出两个不同的格式之一，可以为 GDI 定义调色板。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">调色板格式</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>编制索引</p></td>
<td align="left"><p>颜色索引是一个 RGB 值数组的索引。 数组可以是小，例如，包含 16 色索引，也很大，包含，例如，4096 颜色或更多索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p>位域</p></td>
<td align="left"><p>颜色索引中的位域中的每种颜色指定 R、 G 和 B 的量方面的颜色。 例如，5 位可为每个，提供介于 0 到 31 之间的值为每种颜色。 5 位的值将进行扩展以将转换为 RGB 时覆盖每个组件 0 到 255 的范围。 （常用 RGB 表示形式本身定义的位域中）。</p></td>
</tr>
</tbody>
</table>

 

GDI 相反的顺序通常使用的调色板映射。 也就是说，应用程序指定绘制的 RGB 颜色和 GDI 必须找到会导致设备以显示该颜色的颜色索引。 下一个表中所示，GDI 将两个主要调色板服务功能提供用于创建和删除调色板，以及某些服务函数与相关联[ **PALOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_palobj)和[**XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)用于转换之间两个调色板的颜色索引。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette" data-raw-source="[&lt;strong&gt;EngCreatePalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)"><strong>EngCreatePalette</strong></a></p></td>
<td align="left"><p>创建调色板。 驱动程序通过返回到的调色板的句柄来与设备关联调色板<a href="https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo" data-raw-source="[&lt;strong&gt;DEVINFO&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)"> <strong>DEVINFO</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepalette" data-raw-source="[&lt;strong&gt;EngDeletePalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletepalette)"><strong>EngDeletePalette</strong></a></p></td>
<td align="left"><p>删除给定的调色板。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdithercolor" data-raw-source="[&lt;strong&gt;EngDitherColor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdithercolor)"><strong>EngDitherColor</strong></a></p></td>
<td align="left"><p>返回指定的 RGB 颜色近似于标准 8x8 抖动。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerypalette" data-raw-source="[&lt;strong&gt;EngQueryPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engquerypalette)"><strong>EngQueryPalette</strong></a></p></td>
<td align="left"><p>查询其属性的调色板。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors" data-raw-source="[&lt;strong&gt;PALOBJ_cGetColors&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-palobj_cgetcolors)"><strong>PALOBJ_cGetColors</strong></a></p></td>
<td align="left"><p>使驱动程序从索引调色板下载 RGB 颜色。 中的显示驱动程序通过调用<a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvsetpalette)"> <strong>DrvSetPalette</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_cgetpalette" data-raw-source="[&lt;strong&gt;XLATEOBJ_cGetPalette&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_cgetpalette)"><strong>XLATEOBJ_cGetPalette</strong></a></p></td>
<td align="left"><p>检索 24 位的 RGB 颜色或已索引的源调色板中的颜色的位域格式。 该驱动程序可以使用此函数以从要执行混合颜色的调色板中获取信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform" data-raw-source="[&lt;strong&gt;XLATEOBJ_hGetColorTransform&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform)"><strong>XLATEOBJ_hGetColorTransform</strong></a></p></td>
<td align="left"><p>返回指定的转换对象的颜色转换。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_ixlate" data-raw-source="[&lt;strong&gt;XLATEOBJ_iXlate&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_ixlate)"><strong>XLATEOBJ_iXlate</strong></a></p></td>
<td align="left"><p>将转换为单个源颜色索引到目标颜色索引。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_pivector" data-raw-source="[&lt;strong&gt;XLATEOBJ_piVector&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_pivector)"><strong>XLATEOBJ_piVector</strong></a></p></td>
<td align="left"><p>检索已索引的源调色板中的转换向量。 驱动程序可以使用此向量来执行其自己的目标索引的源索引转换。</p></td>
</tr>
</tbody>
</table>

 

 

 





