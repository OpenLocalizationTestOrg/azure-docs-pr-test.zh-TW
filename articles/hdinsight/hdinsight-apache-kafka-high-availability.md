---
title: "使用 Apache Kafka-Azure HDInsight aaaHigh 可用性 |Microsoft 文件"
description: "深入了解如何使用 Azure HDInsight 上的 Apache Kafka tooensure 高可用性。 了解如何 toorebalance 分割 Kafka 的複本，使其在不同容錯網域內 hello 包含 HDInsight 的 Azure 區域。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>使用 HDInsight 上的 Apache Kafka (預覽) 確保您資料的高可用性

了解如何 tooconfigure 磁碟分割複本的基礎硬體 Kafka 主題 tootake 利用機架組態。 此設定可確保資料儲存在 HDInsight 上的 Apache Kafka hello 可用性。

## <a name="fault-and-update-domains-with-kafka"></a>容錯和更新網域與 Kafka

容錯網域是 Azure 資料中心內基礎硬體的邏輯群組。 每個容錯網域會共用通用電源和網路交換器。 hello 虛擬機器和實作 hello 節點內的 HDInsight 叢集的受管理的磁碟的分散這些容錯網域。 此架構會限制 hello 的實體硬體失敗的潛在影響。

每個 Azure 區域有特定數目的容錯網域。 如需網域及它們包含的容錯網域的 hello 數目的清單，請參閱 hello[可用性設定組](../virtual-machines/linux/regions-and-availability.md#availability-sets)文件。

> [!IMPORTANT]
> Kafka 不知道容錯網域。 當您建立主題 Kafka 中時，其可能會將所有資料分割的複本儲存在 hello 相同容錯網域。 toosolve 這個問題，我們提供 hello [Kafka 分割重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)。

## <a name="when-toorebalance-partition-replicas"></a>當 toorebalance 分割複本

tooensure hello 最高的可用性 Kafka 資料，您應該重新 hello 磁碟分割複本平衡的主題在下列時間的 hello:

* 建立新主題或磁碟分割時

* 當您相應增加叢集時

## <a name="replication-factor"></a>複寫因子

> [!IMPORTANT]
> 我們建議使用包含三個容錯網域的 Azure 地區，以及使用複寫因子 3。

如果您必須使用包含只有兩個容錯網域的區域，使用複寫因數的 4 個 toospread hello 複本平均橫跨 hello 兩個容錯網域。

建立主題和設定 hello 複寫因數的範例，請參閱 hello [Kafka HDInsight 上的開頭](hdinsight-apache-kafka-get-started.md)文件。

## <a name="how-toorebalance-partition-replicas"></a>Toorebalance 分割複本的方式

使用 hello [Kafka 分割重新平衡工具](https://github.com/hdinsight/hdinsight-kafka-tools)toorebalance 選取主題。 從 Kafka 叢集的 SSH 工作階段 toohello 前端節點，就必須執行此工具。

如需有關如何連接使用 SSH tooHDInsight 的詳細資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

## <a name="next-steps"></a>後續步驟

* [HDInsight 上的 Kafka 延展性](hdinsight-apache-kafka-scalability.md)
* [使用 HDInsight 上的 Kafka 進行鏡像處理](hdinsight-apache-kafka-mirroring.md)