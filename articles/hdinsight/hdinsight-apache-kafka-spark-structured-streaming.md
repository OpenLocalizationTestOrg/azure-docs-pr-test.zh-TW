---
title: "aaaApache Spark 結構化以資料流處理 Kafka-Azure HDInsight |Microsoft 文件"
description: "深入了解如何 toouse Apache Spark 資料流 (DStream) tooget 資料傳入或傳出 Apache Kafka。 在此範例中，您使用 Jupyter Notebook 從 HDInsight 上的 Spark 串流資料。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>搭配 HDInsight 上的 Kafka (預覽) 使用 Spark 結構化串流

深入了解如何 toouse Apache Kafka Azure HDInsight 上的 Spark 結構化資料流 tooread 資料。

Spark 結構化串流是建置在 Spark SQL 上的串流處理引擎。 它允許您 tooexpress 資料流計算 hello 與批次計算相同的靜態資料。 如需有關結構化資料流處理的詳細資訊，請參閱 hello[結構化資料流程式設計手冊 [Alpha]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org 在。

> [!IMPORTANT]
> 此範例使用 HDInsight 3.6 上的 Spark 2.1。 結構化串流在 Spark 2.1 上會視為 __alpha__。
>
> 本文件中的 hello 步驟建立包含 HDInsight 上的 Spark 以及 Kafka HDInsight 叢集上的 Azure 資源群組。 這些叢集會同時位於 Azure 虛擬網路，可讓 hello Spark 叢集 toodirectly 與 hello Kafka 叢集通訊。
>
> 當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。

## <a name="create-hello-clusters"></a>建立 hello 叢集

Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。 討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。 例如，hello Kafka 與 Spark 叢集位於 Azure 的虛擬網路中。 hello 下圖顯示 hello 叢集之間通訊流動的方式：

![Azure 虛擬網路中的 Spark 和 Kafka 叢集圖表](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> hello Kafka 服務是有限的 toocommunication hello 虛擬網路內。 例如，可以透過存取 SSH 和 Ambari hello 網際網路，hello 叢集上的其他服務。 Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。

雖然您可以建立 Azure 虛擬網路，Kafka 和 Spark 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。 使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Spark 叢集 tooyour Azure 訂用帳戶。

1. 使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**。

    此範本會建立 hello 下列資源：

    * HDInsight 3.5 叢集上的 Kafka。
    * HDInsight 3.6 叢集上的 Spark。
    * Azure 虛擬網路，其中包含 hello HDInsight 叢集。

    > [!IMPORTANT]
    > hello 結構化的資料流筆記本用於這個範例需要 HDInsight 3.6 上的 Spark。 如果您在 HDInsight 上使用較早版本的 Spark，使用 hello 筆記本時收到錯誤。

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

一旦已建立 hello 資源，您已重新導向的 toohello 資源群組 刀鋒視窗。

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> 請注意，hello hello HDInsight 叢集名稱**spark BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。 連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。

## <a name="get-hello-kafka-brokers"></a>取得 hello Kafka 代理程式

hello 在此範例中的程式碼會連接 toohello Kafka broker hello Kafka 叢集中的主機。 toofind hello Kafka broker 主機，請使用下列 PowerShell 或 Bash 範例 hello:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> 這個範例預期`$PASSWORD`toocontain hello hello 叢集登入，密碼和`$CLUSTERNAME`toocontain hello hello Kafka 叢集名稱。
>
> 這個範例會使用 hello [jq](https://stedolan.github.io/jq/) hello JSON 文件中的公用程式 tooparse 資料。

hello 輸出是類似 toohello 下列文字：

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

儲存這項資訊，，因為它正使用 hello 下列各節的這份文件中。

## <a name="get-hello-notebooks"></a>取得 hello 筆記本

這份文件中所述的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming)。

## <a name="upload-hello-notebooks"></a>上傳 hello 筆記本

Hello 專案 tooyour Spark 中的下列步驟 tooupload hello 筆記本，HDInsight 叢集上使用 hello:

1. 在您的 web 瀏覽器連接 toohello Jupyter 筆記本，您的 Spark 叢集上。 在 hello 下列 URL，取代`CLUSTERNAME`hello Kafka 叢集名稱：

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    出現提示時，輸入 hello 叢集登入 （管理員） 和建立 hello 叢集時所使用的密碼。

2. Hello 上方右側的 hello 頁面上，從使用 hello__上傳__按鈕 tooupload hello__資料流推文 To_Kafka.ipynb__檔案 toohello 叢集。 選取__開啟__toostart hello 上傳。

    ![使用 hello 上傳按鈕 tooselect 並上傳筆記本](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![選取 hello KafkaStreaming.ipynb 檔案](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. 尋找 hello__資料流推文 To_Kafka.ipynb__ hello 筆記型電腦，然後選取清單中的項目__上傳__旁邊的按鈕。

    ![使用 hello 上傳按鈕 hello KafkaStreaming.ipynb 項目 tooupload 它 toohello 筆記本伺服器](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. 重複步驟 1-3 tooload hello __Spark-結構化的資料流-從-Kafka.ipynb__筆記型電腦。

## <a name="load-tweets-into-kafka"></a>將推文載入到 Kafka

Hello 檔案已上傳，一旦選取 hello__資料流推文 To_Kafka.ipynb__項目 tooopen hello 筆記型電腦。 到 Kafka 遵循 hello 筆記本 tooload 推文中的 hello 步驟。

## <a name="process-tweets-using-spark-structured-streaming"></a>使用 Spark 結構化串流處理推文

從 hello Jupyter 筆記本首頁上，選取 hello __Spark-結構化的資料流-從-Kafka.ipynb__項目。 從 Kafka 使用 Spark 結構化資料流處理，請遵循 hello 筆記本 tooload 推文中的 hello 步驟。

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toouse Spark 結構化資料流，請參閱下列文件 toolearn 深入了解使用 Spark 和 Kafka hello:

* [如何 toouse 二手串流 (DStream) 與 Kafka](hdinsight-apache-spark-with-kafka.md)。
* [開始使用 Jupyter Notebook 與 HDInsight 上的 Spark](hdinsight-apache-spark-jupyter-spark-sql.md)