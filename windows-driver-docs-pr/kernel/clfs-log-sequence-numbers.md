---
title: CLFS 日志序列号
description: CLFS 日志序列号
ms.assetid: 4637fa0c-2f19-4f0c-bf13-f4ccac2e7284
keywords:
- 公用日志文件系统 WDK 内核，日志序列号
- CLFS WDK 内核，日志序列号
- 日志序列号 WDK CLFS
- Lsn WDK CLFS
- 基本 Lsn WDK CLFS
- 上次 Lsn WDK CLFS
- 上一个 Lsn WDK CLFS
- 撤消-下一个 Lsn WDK CLFS
- 活动流部分 WDK CLFS
- 流活动部分 WDK CLFS
- 流 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c75c08cd1cf0b278ad21e2677a0f6a770f942353
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828553"
---
# <a name="clfs-log-sequence-numbers"></a>CLFS 日志序列号





在公用日志文件系统（CLFS）中，给定流中的每个日志记录都由一个日志序列号（LSN）唯一标识。 向流中写入记录时，会返回一个 LSN，用于标识该记录以供将来参考。

为特定流创建的 Lsn 构成严格递增的序列。 也就是说，分配给给定流中的日志记录的 LSN 总是大于分配给以前写入同一流的日志记录的 Lsn。 以下函数可用于比较给定流中的日志记录的 Lsn。

[**ClfsLsnNull**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnnull)

[**ClfsLsnEqual**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnequal)

[**ClfsLsnGreater**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsngreater)

[**ClfsLsnLess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfslsnless)

常量 CLFS\_LSN\_NULL 和 CLFS\_LSN\_无效是所有有效 Lsn 的下限和上限。 任何有效的 LSN 都大于或等于 CLFS\_LSN\_NULL。 此外，任何有效的 LSN 严格小于 CLFS\_LSN\_无效。 请注意，CLFS\_LSN\_NULL 是有效的 LSN，而 CLFS\_LSN\_无效不是有效的 LSN。 尽管如此，还可以通过使用上一列表中的函数，将 CLFS\_LSN\_无效的与其他 Lsn 进行比较。

对于每个流，CLFS 跟踪两个特殊 Lsn：基本 LSN 和最后一个 LSN。 此外，每个单独的日志记录都有两个特殊的 Lsn （前一个 LSN 和一个 "撤消下一个" LSN），您可以使用它们来创建相关日志记录的链。 以下各节将详细介绍这些特殊 Lsn。

### <a name="base-lsn"></a>基本 LSN

当客户端写入流中的第一条记录时，CLFS 会将基本 LSN 设置为第一条记录的 LSN。 在客户端更改基本 LSN 之前，此 LSN 将保持不变。 当流的客户端不再需要流中某个点之前的记录时，可以通过调用[**ClfsAdvanceLogBase**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsadvancelogbase)或[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)来更新基本 LSN。 例如，如果客户端不再需要前五个日志记录，则可以将基本 LSN 设置为第六个记录的 LSN。

### <a name="last-lsn"></a>最后一个 LSN

当客户端将记录写入流时，CLFS 将调整最后一个 LSN，使其始终为写入的最后一条记录的 LSN。 如果客户端不再需要流中某个点之后的记录，则可以通过调用[**ClfsSetEndOfLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfssetendoflog)来更新最后一个 LSN。 例如，如果客户端不再需要在第十个记录后写入的任何记录，则可以通过将最后一个 LSN 设置为第10个记录的 LSN 来截断流。

### <a name="active-portion-of-a-stream"></a>流的活动部分

流的*活动部分*是流中以基本 lsn 指向的记录开头的部分，并以最后一个 lsn 指向的记录结束。 下图说明了基本 LSN 和最后一个 LSN 如何描绘出流的活动部分。

![阐释 clfs 流的活动部分的示意图](images/clfsactivelog.gif)

**请注意**   如果流有存档尾部，则流的活动部分将从基本 LSN 或存档尾所指向的记录开始，以较小者为准。 有关存档的详细信息，请参阅[CLFS 支持存档](clfs-support-for-archiving.md)。

 

### <a name="previous-lsn"></a>上一个 LSN

假设两个活动数据库事务（事务 A 和事务 B）同时将记录写入同一流。 每次事务 A 写入一条记录时，都会将记录的前一个 LSN 设置为事务 A 写入的以前的日志记录的 LSN。这构成了一系列日志记录，这些记录属于事务 A，可以按相反的顺序进行遍历。 该链以事务 A 所写入的第一个日志记录结束，该记录将其前一个 LSN 设置为 CLFS\_LSN\_无效。 同样，事务 B 通过设置其写入的每个日志记录的前一个 LSN 来创建自己的日志记录链。

下图中的箭头说明了日志记录的前一个 LSN 如何指向属于特定事务的链中的前一条记录。

![说明前面的 lsn 指针的关系图](images/clfsrecordchains.gif)

### <a name="undo-next-lsn"></a>Undo-下一个 LSN

假设事务对可变内存中的数据对象进行了五次更新，回滚第四个和第五个更新，然后进行第六次更新。 当事务进行更新时，它将写入日志记录1、2、3、4、5、5 "、4" 和6。 日志记录1到5描述了更新1到5所做的更改。 记录 5 "描述了 update 5 回滚过程中所做的更改，记录 4" 描述了在更新4回滚过程中所做的更改。 最后，记录6描述了更新6所做的更改。 请注意，数字1、2、3、4、5、5 "、4" 和6不是日志记录的 Lsn;它们只是用于命名日志记录以供本文使用的编号。

日志记录 5 "和 4"，用于描述回滚，称为 "补偿日志记录" （Clr）。 该事务将每个 CLR 的撤消后续 LSN 设置为其更新刚回滚（撤消）的日志记录的前置任务（在事务写入的记录中）。 在此示例中，"记录 5" 的撤消后续 LSN 是记录4的 LSN，而 "记录 4" 的 "撤消后一个 LSN" 是记录3的 LSN。

普通日志记录（未 Clr 的记录）会将其 "撤消下一个" Lsn 设置为事务写入的以前的日志记录。 也就是说，对于普通记录，撤消下一个 LSN 和前一个 LSN 是相同的。

现在，假设发生系统故障，而且在重新启动恢复期间，必须回滚整个事务。 恢复代码读取日志记录6。 记录6中的数据指示记录6是普通记录（而不是 CLR），因此恢复代码将回滚 update 6。 然后，恢复代码检查记录6的撤消下一 LSN，并发现它指向 "记录 4"。 记录4中的数据指示它是 CLR，因此恢复代码不会回滚 update 4。 相反，它会检查记录4的 "撤消后一个" LSN，并发现它指向 "记录 3"。 记录3不是 CLR，因此恢复代码将回滚 update 3。 在恢复期间，更新5和4不会回滚，因为它们已在普通前处理期间回滚。 最后，恢复代码向后滚动更新2和1。

下图中的箭头说明了 undo next LSN 如何提供一种机制，恢复代码可使用该机制来跳过更新已回滚的记录。

![说明前面的 lsn 和 undo next lsn 指针的关系图](images/clfsundonext.gif)

 

 




