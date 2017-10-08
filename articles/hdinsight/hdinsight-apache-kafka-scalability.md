---
title: "aaaApache Kafka 增加小數位數-Azure HDInsight |Microsoft 文件"
description: "了解如何 tooconfigure 管理 Azure HDInsight tooincrease 延展性 Apache Kafka 叢集的磁碟。"
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
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>在 HDInsight 上設定 Apache Kafka 的儲存體和延展性

了解如何 tooconfigure hello 數目受管理的磁碟使用 Apache Kafka HDInsight 上。

HDInsight 上的 Kafka hello HDInsight 叢集中使用 hello hello 虛擬機器的本機磁碟。 因為 Kafka 是非常 I/O， [Azure 受管理磁碟](../virtual-machines/windows/managed-disks-overview.md)使用的 tooprovide 高輸送量，並提供每個節點的更多儲存空間。 如果 Kafka 用於傳統的虛擬硬碟 (VHD)，每個節點是有限的 too1 TB。 受管理的磁碟，您可以使用多個磁碟 tooachieve 16 TB hello 叢集中的每個節點。

hello 下列圖表提供 Kafka HDInsight 之前受管理的磁碟上和 Kafka 之間的比較在 HDInsight 上使用受管理的磁碟：

![圖表顯示 HDInsight 上的 Kafka 每個 VM 使用單一 VHD 與每個 VM 使用多個受控磁碟](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>設定受控磁碟：Azure 入口網站

1. Hello 中的 hello 步驟[建立的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)toounderstand hello 通用步驟 toocreate 使用 hello 入口網站的叢集。 不會完成 hello 入口網站的建立程序。

2. 從 hello__叢集大小__刀鋒視窗中，使用 hello__磁碟每個背景工作節點__欄位磁碟 tooconfigure hello 數目。

    > [!NOTE]
    > hello 的受管理的磁碟類型可以是__標準__(HDD) 或__Premium__ (SSD)。 進階磁碟會與 DS 和 GS 系列搭配使用。 所有其他的 VM 類型是使用標準磁碟。

    ![Hello 叢集大小刀鋒視窗中的每個反白顯示的背景工作節點 hello 磁碟的映像](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>設定受控磁碟：Resource Manager 範本

toocontrol hello 磁碟數目 Kafka 叢集中，使用 hello 遵循 hello 範本區段中的 hello 背景工作節點使用：

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

您可以找到完整的範本示範如何 tooconfigure 管理磁碟在[https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json)。

## <a name="next-steps"></a>後續步驟

與 HDInsight 上 Kafka 需使用詳細資訊，請參閱下列文件的 hello:

* [在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本](hdinsight-apache-kafka-mirroring.md)
* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](hdinsight-apache-storm-with-kafka.md)
* [使用 Apache Spark 搭配 Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)
* [透過 Azure 虛擬網路連線 tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [使用 Kafka 之受控磁碟的 HDInsight 部落格](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)