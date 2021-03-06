---
title: GUID_DEVINTERFACE_KEYBOARD
description: GUID_DEVINTERFACE_KEYBOARD
ms.assetid: ae434c45-07f6-4aa1-b9d3-e4ceca8cc81c
keywords:
- GUID_DEVINTERFACE_KEYBOARD 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_KEYBOARD
api_location:
- Ntddkbd.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d5c2db5b637df53b94ca267207e29019069dd7d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372701"
---
# <a name="guiddevinterfacekeyboard"></a>GUID_DEVINTERFACE_KEYBOARD


GUID_DEVINTERFACE_KEYBOARD[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)定义的键盘设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_KEYBOARD</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{884b96c3-56ef-11d1-bc8c-00a0c91405dd}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

键盘设备的驱动程序注册通知的系统和应用程序的键盘设备存在此设备接口类的实例。

系统提供[键盘类驱动程序](../hid/keyboard-and-mouse-class-drivers.md)注册键盘设备将此设备接口类的实例。 通过使用键盘类驱动程序支持的 I/O 接口中访问此设备接口类的实例。

有关支持键盘的设备的常规信息，请参阅[HID 体系结构](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))并[Kbdclass 和 Mouclass 驱动程序的功能](../hid/keyboard-and-mouse-class-drivers.md)。

WDK 包含系统提供键盘类驱动程序的示例代码。 在键盘类驱动程序使用已过时的标识符[ **GUID_CLASS_KEYBOARD** ](guid-class-keyboard.md)若要注册此实例[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)。

鼠标设备的设备接口类有关的信息，请参阅[ **GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Microsoft Windows 2000 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntddkbd.h （包括 Ntddkbd.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_CLASS_KEYBOARD**](guid-class-keyboard.md)

[**GUID_DEVINTERFACE_MOUSE**](guid-devinterface-mouse.md)

 

 






