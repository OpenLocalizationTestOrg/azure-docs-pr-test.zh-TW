---
title: "aaaAn 簡介 tooApache HDInsight 的 Azure 上 Kafka |Microsoft 文件"
description: "深入了解 HDInsight 上的 Apache Kafka： 它是什麼、 它的功能和 toofind 範例及取得啟動資訊。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>HDInsight 上的 Apache Kafka (預覽) 簡介

[Apache Kafka](https://kafka.apache.org)開放原始碼分散式資料流平台可能是使用的 toobuild 即時串流資料管線和應用程式。 Kafka 也會提供訊息代理程式的功能類似 tooa 訊息佇列，您可以在其中發佈和訂閱 toonamed 資料流。 Kafka HDInsight 上的為您提供 hello Microsoft Azure 雲端中受管理、 高擴充性和高可用性服務。

## <a name="why-use-kafka-on-hdinsight"></a>為何使用 HDInsight 上的 Kafka？

Kafka 提供下列功能的 hello:

* 發行-訂閱訊息模式： Kafka 提供生產者 API，以發行記錄 tooa Kafka 主題。 訂閱 tooa 主題時，會使用 hello 取用者應用程式開發介面。

* 串流處理︰Kafka 通常與 Apache Storm 或 Spark 一起用來處理即時串流。 Kafka 0.10.0.0 (HDInsight 3.5 版) 導入了資料流處理的 API，可讓您串流處理解決方案，而不需要風暴或 Spark toobuild。

* 水平縮放： Kafka hello hello HDInsight 叢集節點之間分割資料流。 取用者處理程序可以與個別資料分割 tooprovide 負載平衡使用的記錄時產生關聯。

* 依序傳遞： 內每個資料分割，記錄會儲存在已收到 hello 順序中的 hello 資料流。 每個資料分割與一個取用者處理序建立關聯之後，就能保證依序處理記錄。

* 容錯： 資料分割可以複寫之間節點 tooprovide 容錯功能。

* Azure 受管理的磁碟與整合： hello hello hello HDInsight 叢集中的虛擬機器所使用的磁碟管理磁碟提供更高規模和輸送量。

    預設會啟用受管理的磁碟的 HDInsight 上 Kafka 和 hello 每個節點使用的磁碟數目可以 HDInsight 建立期間設定。 如需受控磁碟的詳細資訊，請參閱 [Azure 受控磁碟](../virtual-machines/windows/managed-disks-overview.md)。

    如需使用 HDInsight 上的 Kafka 設定受控磁碟的資訊，請參閱[提高 HDInsight 上的 Kafka 延展性](hdinsight-apache-kafka-scalability.md)。

## <a name="use-cases"></a>使用案例

* **傳訊**： 因為它支援 hello 發行-訂閱訊息模式、 Kafka 通常是當做訊息仲介。

* **活動追蹤**： 因為 Kafka 提供的記錄順序中記錄，所以可以使用的 tootrack 且重新建立活動。 例如，網站或應用程式中的使用者動作。

* **彙總**： 使用資料流處理，您可以從不同的資料流 toocombine 資訊彙總並集中管理將操作資料的 hello 資訊。

* **轉換**︰您可以利用串流處理來結合並充實多個輸入主題的資料，而成為一個或多個輸出主題。

## <a name="next-steps"></a>後續步驟

如何使用 hello 下列連結的 toolearn toouse Apache Kafka HDInsight 上：

* [開始使用 HDInsight 上的 Kafka](hdinsight-apache-kafka-get-started.md)

* [在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本](hdinsight-apache-kafka-mirroring.md)

* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](hdinsight-apache-storm-with-kafka.md)

* [使用 Apache Spark 搭配 Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)

* [透過 Azure 虛擬網路連線 tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
