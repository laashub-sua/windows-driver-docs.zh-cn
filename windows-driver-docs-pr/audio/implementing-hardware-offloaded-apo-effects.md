---
title: 实现硬件卸载的 APO 效果
description: 音频处理对象（即）的硬件卸载可提供可能的性能增强功能，还可节省电力。
ms.assetid: 159DFFD2-2434-4EDC-A83C-455BA80F74C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e24d0d5a9b9959fa165aa10a6f7a5910d301bf3
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829026"
---
# <a name="hardware-offloaded-apo-effects"></a>硬件卸载 APO 效果

在 Windows 10 版本1511及更高版本中，支持卸载音频处理对象（is）。 除可能的性能增强外，在使用硬件卸载时，还可以使用很大的电源节约。

在硬件卸载播放期间，可以加载两种类型的。

1. 卸载流效果（OSFX）
2. 卸载模式效果（OMFX）

## <a name="hardware-offloaded-apo-effects-overview"></a>硬件卸载 APO 效果概述

### <a name="hardware-offloaded-audio-processing-and-hardware-offloaded-apos"></a>硬件卸载音频处理和硬件卸载

在 Windows 8 中，音频引擎经过了重新设计，可与已被卸载到独立于计算机主音频系统但连接到计算机的主音频系统的硬件设备一起使用。 这称为硬件卸载。 有关详细信息，请参阅[硬件卸载音频处理](hardware-offloaded-audio-processing.md)。

硬件卸载功能主要针对具有较大缓冲区大小的低功率方案。 例如，在支持的系统中的低功率音频（LPA）播放过程中，音频缓冲区大小或周期设置为1秒，以便 CPU 不会频繁唤醒来处理小型缓冲区（例如，每隔10毫秒）。

实现硬件卸载和硬件卸载音频处理可以最大限度地提高能效。

下图显示音频处理对象的体系结构。 关系图的右侧显示一个应用程序，该应用程序向下传递到硬件卸载的 OSFX 和 OMFX 影响。

![音频驱动程序体系结构，显示应用程序调用到 sfx mfx 和 efx 效果，然后调用驱动程序和音频硬件](images/audio-hardware-offloaded-apo-overview.png)

## <a name="implementing-hardware-offloaded-apo-effects"></a>实现硬件卸载的 APO 效果

硬件卸载的 APO 必须遵循[音频处理对象体系结构](audio-processing-object-architecture.md)和[实现音频处理对象](implementing-audio-processing-objects.md)中所述的相同基本要求和设计原则。

### <a name="supported-audio-format-implementation-guidelines"></a>支持的音频格式实现准则

对于卸载的硬件，还必须考虑到支持的音频格式。

每个 APO 实现[**IAudioProcessingObject：： IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)方法，该方法在音频图形生成过程中用于确定输出音频格式以及是否需要任何格式转换。

```cpp
HRESULT IsInputFormatSupported(
  [in, optional]  IAudioMediaType *pOppositeFormat,
  [in, optional]  IAudioMediaType *pRequestedInputFormat,
  [out, optional] IAudioMediaType **ppSupportedInputFormat
);
```

卸载呈现终结点可以支持多种格式，其中包括主机/系统 pin 呈现支持的默认格式。 卸载 APO 应支持所有这些格式，以便呈现流（支持的格式）不必经过任何其他格式转换。

卸载 SFX 可以实现格式转换，并接受范围更广的格式。 例如，如果卸载 SFX 提供耳机 virtualizations （即，将5.1 通道音频转换为立体声），则应 \_ 在此方法中为相应的输入/输出对返回 S OK。

卸载 SFX 应查看卸载 pin 支持的格式，并同时支持/扩展功能。

卸载 MFX 无法更改输入流的格式，但它仍需要支持卸载终结点提供的各种格式，并消除了任何不必要的格式转换。

在卸载 pin 中呈现时，该 pin 上只有一个流处于活动状态，因此不会混合流。 因此，不需要在流级和模式级别处理音频。 因此，音频效果可能不需要同时作为流效果和模式效果启用。 卸载的终结点将支持更多的流，根据系统处理体系结构的不同，可能需要将卸载处理分解为 SFX/MFX。

### <a name="inf-file-entries"></a>INF 文件条目

实现以下 INF 文件条目，定义卸载播放过程中将加载的效果。 INF 文件属性键指示音频终结点生成器将已卸载的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

|属性键|GUID|
|----|----|
| [PKEY \_ FX \_ 卸载 \_ StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-offload-streameffectclsid)                                                  | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D}，11 |
| [PKEY \_ FX \_ 卸载 \_ ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-offload-modeeffectclsid)                                                      | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D}，12 |
| [\_ \_ \_ \_ 支持 \_ \_ 流式处理的 PKEY SFX 卸载 ProcessingModes](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-offload-processingmodes-supported-for-streaming) | {D3993A3F-99C2-4402-B5EC-A92A0367664B}，11 |
| [PKEY \_ MFX \_ 卸载 \_ ProcessingModes \_ 支持 \_ \_ 流式处理](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-offload-processingmodes-supported-for-streaming) | {D3993A3F-99C2-4402-B5EC-A92A0367664B}，12 |

## <a name="related-topics"></a>相关主题

[实现音频处理对象](implementing-audio-processing-objects.md)  
[Windows 音频处理对象](windows-audio-processing-objects.md)  
