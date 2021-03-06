---
title: SR-IOV 的标准化 INF 关键字
description: SR-IOV 的标准化 INF 关键字
ms.assetid: 5CA33B4F-E43A-4EB6-BCAB-365CA1FD3EF2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4a693fb72929b0362e52769cff990a0cb95dd8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841843"
---
# <a name="standardized-inf-keywords-for-sr-iov"></a>SR-IOV 的标准化 INF 关键字


本主题介绍用于单个根 i/o 虚拟化（SR-IOV）接口的标准化 INF 关键字。 这些关键字适用于 SR-IOV 网络适配器 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序的 INF 文件。

以下部分介绍了 SR-IOV INF 关键字：

[启用或禁用 SR-IOV 支持的标准化 INF 关键字](#standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support)

[用于配置默认 NIC 交换机的标准化 INF 关键字](#standardized-inf-keywords-for-configuration-of-the-default-nic-switch)

## <a name="standardized-inf-keywords-for-enabling-or-disabling-sr-iov-support"></a>用于启用或禁用 SR-IOV 支持的标准化 INF 关键字


定义了标准化的 INF 关键字，以启用或禁用对网络适配器的 SR-IOV 功能的支持。

<a href="" id="-sriov"></a> **\*SRIOV**  
描述设备是否已启用或禁用 SR-IOV 功能的值。

安装驱动程序后，管理员可以在网络适配器的 "**高级**" 属性页中更新 **\*SRIOV**关键字值。 有关高级属性的详细信息，请参阅[指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**   中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

<a href="" id="-sriovpreferred"></a> **\*SriovPreferred**  
一个值，该值定义是否应启用 SR-IOV 功能，而不是虚拟机队列（VMQ）或接收方缩放（RSS）功能。

这是一个隐藏的关键字值，不得在 INF 文件中指定，并且不会显示在网络适配器的 "**高级**" 属性页中。

有关如何解释 SR-IOV、VMQ 和 RSS 关键字的详细信息，请参阅[处理 sr-iov、vmq 和 Rss 标准化 INF 关键字](handling-sr-iov--vmq--and-rss-standardized-inf-keywords.md)。

SR-IOV 标准化 INF 关键字是枚举关键字，下表对此进行了说明。 此表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称也会出现在注册表 **NDI\\params\\** 关键网络适配器。

<a href="" id="paramdesc"></a>ParamDesc  
与**SubkeyName**关键字关联的显示文本。

**请注意**   独立硬件供应商 (IHV) 可以为 SubkeyName 定义描述性文本。

 

<a href="" id="value"></a>负值  
与列表中的每个**SubkeyName**关键字关联的枚举整数值。

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">值</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>SRIOV</strong></p></td>
<td align="left"><p>SR-IOV</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Disabled</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1（默认值）</p></td>
<td align="left"><p>已启用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong></em>SriovPreferred</strong></p></td>
<td align="left"><p>此子项的 ParamDesc 和 EnumDesc 条目不能用于 INF 文件或用户界面。</p></td>
<td align="left"><p>0（默认值）</p></td>
<td align="left"><p>基于 <strong><em>VmqOrRssPreferrence</strong> 关键字报告 RSS 或 VMQ 功能。 不要报告 SR-IOV 功能，</p>
<p>有关<strong></em>VmqOrRssPreferrence</strong>关键字的详细信息，请参阅<a href="standardized-inf-keywords-for-vmq.md" data-raw-source="[Standardized INF Keywords for VMQ](standardized-inf-keywords-for-vmq.md)">VMQ 的标准化 INF 关键字</a>。</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1</p></td>
<td align="left"><p>报告 SR-IOV 功能。</p></td>
</tr>
</tbody>
</table>

 

有关标准化 INF 关键字的详细信息，请参阅[网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="standardized-inf-keywords-for-configuration-of-the-default-nic-switch"></a>用于配置默认 NIC 交换机的标准化 INF 关键字


从 Windows Server 2012 开始，SR-IOV 接口仅支持网络适配器上的一个 NIC 交换机。 此开关称为*默认 NIC 交换机*，由 NDIS\_默认\_交换机\_ID 标识符引用。

PF 微型端口驱动程序的 INF 文件必须指定 SR-IOV 网络适配器上默认 NIC 交换机的配置。 这使得网络安装程序可以将默认交换机配置信息从 INF 复制到默认交换机（**NDI\\参数\\NicSwitches\\0**）子项下的微型端口注册表配置。

这些关键字不会显示在网络适配器的 "**高级**" 属性页中，用户不能对其进行配置。 使用 INF 文件的**DDInstall**部分中的**AddReg**指令指定这些关键字。 每个关键字都由单独的**AddReg**指令指定。

下表描述了 SR-IOV 网络适配器的默认 NIC 交换机配置的 INF 关键字。 此表中的列描述了这些关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在网络适配器的**NDI\\参数\\NicSwitches\\0**键的注册表中。

<a href="" id="data-value"></a>数据值  
与**SubkeyName**关键字关联的值。

<a href="" id="data-type"></a>数据类型  
数据值的类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">数据值</th>
<th align="left">数据类型</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em>标志</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>必须为关键字分配此值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchType</strong></p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>必须为关键字分配此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>SwitchId</strong></p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p>必须为关键字分配此值。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong></em>SwitchName</strong></p></td>
<td align="left"><p>"默认开关"</p></td>
<td align="left"><p>REG_SZ</p></td>
<td align="left"><p>必须为关键字分配此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>*NumVFs</strong></p></td>
<td align="left"><p>（0-<em>n</em>），</p></td>
<td align="left"><p>REG_DWORD</p></td>
<td align="left"><p><em>n</em>是 sr-iov 网络适配器支持的最大 PCIe 虚拟函数（VFs）数。</p>
<div class="alert">
<strong>注意</strong> 此注册表项定义网络适配器支持的最大 VFs 数。 当微型端口驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes" data-raw-source="[&lt;strong&gt;NdisMSetMiniportAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)"><strong>NdisMSetMiniportAttributes</strong></a>时，它可以根据网络适配器上的可用硬件资源播发低于此值。 有关详细信息，请参阅<a href="determining-nic-switch-capabilities.md" data-raw-source="[Determining NIC Switch Capabilities](determining-nic-switch-capabilities.md)">确定 NIC 交换机功能</a>。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

下面是 SR-IOV 网络适配器默认 NIC 交换机配置的**AddReg**指令示例：

``` syntax
HKR, NicSwitches\0, *SwitchId,   0x00010001, 0
HKR, NicSwitches\0, *SwitchName, 0x00000000, “Default Switch”
```

有关**AddReg**指令的语法的详细信息，请参阅[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

有关默认 NIC 交换机的详细信息，请参阅[NIC 交换机](nic-switches.md)。

 

 





