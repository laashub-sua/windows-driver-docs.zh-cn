---
title: RunAs System
description: TAEF 作为本地系统运行测试。
ms.assetid: E1138F36-D043-458A-8424-C649854CB7EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906486347f580dab8cb09adac8eeb89cc05d45b9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373019"
---
# <a name="runas-system"></a>RunAs System


TAEF 作为本地系统运行测试。

**请注意**  运行如本地系统不应创建任何用户界面 (UI) 的测试。 如果你的测试需要创建或与 UI 交互，则需要与 UI 相关中的代码移动到单独的可执行文件启动台式机上使用测试[ **CreateProcessAsUser 函数**](https://docs.microsoft.com/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessasusera)。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>在命令行上指定运行方式


``` syntax
te unittests\* /runas:system
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>将标记与运行方式的测试


测试元数据可用于指定程序集、 类或测试方法的运行方式类型。

**请注意**  元数据中指定的运行方式值重写命令行上指定的运行方式值。 例如，测试标有**runas:system**测试元数据仍将运行作为本地系统，即使 **/runas:elevated**命令行上指定。

 

示例 （本机代码）

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(SystemTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[RunAs](runas.md)

 

 






