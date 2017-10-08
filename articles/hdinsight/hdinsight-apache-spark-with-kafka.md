---
title: "aaaApache Spark Kafka-Azure HDInsight 進行資料流處理 |Microsoft 文件"
description: "深入了解如何 toouse Spark Apache Spark toostream 資料傳入或傳出 Apache Kafka 使用 DStreams。 在此範例中，您使用 Jupyter Notebook 從 HDInsight 上的 Spark 串流資料。"
keywords: "kafka 範例,kafka zookeeper,spark 串流 kafka,spark 串流 kafka 範例"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>在 HDInsight 上使用 Kafka 的 Apache Spark 串流 (DStream) 範例 (預覽)

深入了解如何 toouse 傳入或傳出 Apache Kafka 使用 DStreams HDInsight 上的 Spark Apache Spark toostream 資料。 這個範例會使用 Jupyter 筆記本 hello Spark 叢集上執行。
> [!NOTE]
> 本文件中的 hello 步驟建立包含 HDInsight 上的 Spark 以及 Kafka HDInsight 叢集上的 Azure 資源群組。 這些叢集會同時位於 Azure 虛擬網路，可讓 hello Spark 叢集 toodirectly 與 hello Kafka 叢集通訊。
>
> 當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。

## <a name="create-hello-clusters"></a>建立 hello 叢集

Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。 討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。 例如，hello Kafka 與 Spark 叢集位於 Azure 的虛擬網路中。 hello 下圖顯示 hello 叢集之間通訊流動的方式：

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> 雖然 Kafka 本身是有限的 toocommunication hello 虛擬網路內，hello 叢集上的其他服務例如可以透過存取 SSH 和 Ambari hello 網際網路。 Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。

雖然您可以建立 Azure 虛擬網路，Kafka 和 Spark 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。 使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Spark 叢集 tooyour Azure 訂用帳戶。

1. 使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**。

    > [!WARNING]
    > HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。 此範本會建立包含三個背景工作角色節點的 Kafka 叢集。

    此範本會為 Kafka 和 Spark 建立 HDInsight 3.6 叢集。

2. 使用下列資訊 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **資源群組**：建立群組或選取現有的群組。 此群組包含 hello HDInsight 叢集。

    * **位置**： 選取位置的地理位置關閉 tooyou。

    * **基底叢集名稱**: hello Spark 和 Kafka 叢集 hello 基底名稱為使用此值。 例如，輸入 **hdi** 可建立名為 spark-hdi__ 的 Spark 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。

    * **叢集登入使用者名稱**: hello Spark 和 Kafka 叢集 hello 系統管理員使用者名稱。

    * **叢集登入密碼**: hello Spark 和 Kafka 叢集 hello 管理使用者的密碼。

    * **SSH 使用者名稱**: hello SSH 使用者 toocreate hello Spark 和 Kafka 叢集。

    * **SSH 密碼**: hello hello Spark 和 Kafka 叢集的 hello SSH 使用者密碼。

3. 讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。

4. 最後，檢查**Pin toodashboard** ，然後選取 **購買**。 它會採用約 20 分鐘 toocreate hello 叢集。

一旦已建立 hello 資源，您已重新導向的 tooa 刀鋒視窗中的 hello 資源群組含有 hello 叢集和 web 儀表板。

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> 請注意，hello hello HDInsight 叢集名稱**spark BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。 連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。

## <a name="use-hello-notebooks"></a>使用 hello 筆記本

這份文件中所述的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka)。

Hello 中的 hello 步驟`README.md`檔案 toocomplete 這個範例。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。 正在刪除 hello 群組移除依照此文件、 hello Azure 虛擬網路和 hello 叢集所使用的儲存體帳戶建立的所有資源。

## <a name="next-steps"></a>後續步驟

在此範例中，您將學會如何 toouse 二手 tooread 和撰寫 tooKafka。 使用下列連結 toodiscover hello 其他方式 toowork 與 Kafka:

* [開始使用 Apache Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)
* [在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本](hdinsight-apache-kafka-mirroring.md)
* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](hdinsight-apache-storm-with-kafka.md)

