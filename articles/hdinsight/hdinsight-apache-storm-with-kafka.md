---
title: "aaaUse Storm HDInsight 的 Azure 上使用 Apache Kafka |Microsoft 文件"
description: "Apache Kafka 會隨著 Apache Storm on HDInsight 一起安裝。 了解 toowrite tooKafka，並使用它，然後讀取 hello KafkaBolt 和 KafkaSpout Storm 所提供的元件。 也了解如何 toouse hello 變動 framework toodefine 和提交 Storm 拓撲。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>使用 Apache Kafka (預覽) 搭配 Storm on HDInsight

深入了解如何從 toouse Apache Storm tooread 和寫入 tooApache Kafka。 此範例也示範如何從 HDFS 相容性 Storm 拓撲 toohello toosave 資料檔案使用 HDInsight 的系統。

> [!NOTE]
> 本文件中的 hello 步驟建立包含在 HDInsight 上的 Storm 以及 Kafka HDInsight 叢集上的 Azure 資源群組。 這些叢集會同時位於 Azure 虛擬網路，可讓 hello Storm 叢集 toodirectly 與 hello Kafka 叢集通訊。
> 
> 當您完成這份文件中的 hello 步驟之後時，請記得 toodelete hello 叢集 tooavoid 過多費用。

## <a name="get-hello-code"></a>取得 hello 程式碼

使用這份文件中的 hello 範例的 hello 程式碼將會位於[https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)。

toocompile 此專案中，您需要下列組態的開發環境的 hello:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。 HDInsight 3.5 或更新版本需要 Java 8。

* [Maven 3.x](https://maven.apache.org/download.cgi)

* 將 SSH 用戶端 (您需要 hello`ssh`和`scp`命令)-如需資訊，請參閱[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。

* 文字編輯器或整合式開發環境 (IDE)。

hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。 不過，您應該檢查其存在且包含您系統的 hello 正確值。

* `JAVA_HOME`-應該指向 toohello hello JDK 安裝的目錄。
* `PATH`-應包含下列路徑的 hello:
  
    * `JAVA_HOME`（或 hello 等路徑）。
    * `JAVA_HOME\bin`（或 hello 等路徑）。
    * hello Maven 安裝所在的目錄。

## <a name="create-hello-clusters"></a>建立 hello 叢集

Apache Kafka HDInsight 上不提供存取 toohello Kafka broker 透過 hello 公用網際網路。 討論 tooKafka 必須在 hello 與 hello 節點中的相同 Azure 虛擬網路的任何項目 hello Kafka 叢集。 例如，hello Kafka 與 Storm 叢集位於 Azure 的虛擬網路中。 hello 下圖顯示 hello 叢集之間通訊流動的方式：

![Azure 虛擬網路中的 Storm 和 Kafka 叢集圖表](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> 例如，可以透過存取 SSH 和 Ambari hello 網際網路，hello 叢集上的其他服務。 Hello 公用連接埠適用於 HDInsight 上的詳細資訊，請參閱[連接埠和 Uri 使用 HDInsight](hdinsight-hadoop-port-settings-for-services.md)。

雖然您可以建立 Azure 虛擬網路，Kafka，和 Storm 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。 使用 hello 下列步驟 toodeploy Azure 虛擬網路，Kafka，，和 Storm 叢集 tooyour Azure 訂用帳戶。

1. 使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**。 它會建立 hello 下列資源：
    
    * Azure 資源群組
    * Azure 虛擬網路
    * Azure 儲存體帳戶
    * HDInsight 版本 3.6 上的 Kafka (三個背景工作角色節點)
    * HDInsight 版本 3.6 上的 Storm (三個背景工作角色節點)

  > [!WARNING]
  > HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。 此範本會建立包含三個背景工作角色節點的 Kafka 叢集。

2. 使用下列指引 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：
   
    ![HDInsight 自訂部署](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **資源群組**：建立群組或選取現有的群組。 此群組包含 hello HDInsight 叢集。
   
    * **位置**： 選取位置的地理位置關閉 tooyou。

    * **基底叢集名稱**: hello Storm 和 Kafka 叢集 hello 基底名稱為使用此值。 例如，輸入 **hdi** 可建立名為 **storm-hdi** 的 Storm 叢集以及名為 **kafka-hdi** 的 Kafka 叢集。
   
    * **叢集登入使用者名稱**: hello Storm 和 Kafka 叢集 hello 系統管理員使用者名稱。
   
    * **叢集登入密碼**: hello Storm 和 Kafka 叢集 hello 管理使用者的密碼。
    
    * **SSH 使用者名稱**: hello SSH 使用者 toocreate hello Storm 和 Kafka 叢集。
    
    * **SSH 密碼**: hello hello Storm 和 Kafka 叢集的 hello SSH 使用者密碼。

3. 讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。

4. 最後，檢查**Pin toodashboard** ，然後選取 **購買**。 它會採用約 20 分鐘 toocreate hello 叢集。

一旦已建立 hello 資源，會顯示 hello 資源群組的 hello 刀鋒視窗。

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> 請注意，hello hello HDInsight 叢集名稱**storm BASENAME**和**kafka BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。 連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。

## <a name="understanding-hello-code"></a>了解 hello 程式碼

此專案包含兩種拓撲︰

* **KafkaWriter**: hello 所定義**writer.yaml**檔案，此拓撲寫入使用 hello KafkaBolt 隨附 Apache Storm 的隨機句子 tooKafka。

    此拓撲會使用自訂**SentenceSpout**元件 toogenerate 隨機句子。

* **KafkaReader**: hello 所定義**reader.yaml**檔案，此拓撲，讀取 Kafka 使用 hello KafkaSpout 隨附 Apache Storm 則記錄檔 hello 資料 toostdout。

    此拓撲會使用 hello Storm HdfsBolt toowrite 資料 toodefault 儲存 hello Storm 叢集。
### <a name="flux"></a>Flux

使用定義 hello 拓撲[變動](https://storm.apache.org/releases/1.1.0/flux.html)。 中導入變動 Storm 0.10.x，並讓您從 hello 碼 tooseparate hello 拓撲組態。 如需使用 hello 變動架構的拓撲，hello 拓撲 YAML 檔案中定義。 hello YAML 檔案可以是 hello 拓撲的一部分。 它也可以使用當您送出 hello 拓撲的獨立檔案。 Flux 也支援執行階段的變數替代 (在此範例中使用)。

hello 設定下列參數是在執行階段針對這些拓撲：

* `${kafka.topic}`: hello hello Kafka 主題 hello 拓撲讀名稱。

* `${kafka.broker.hosts}`: hello 裝載該 hello Kafka 居間處理上執行。 hello KafkaBolt 撰寫 tooKafka 時，會使用 hello broker 資訊。

* `${kafka.zookeeper.hosts}`： 動物園管理員在執行中的 hello 主機 hello Kafka 叢集。

如需 Flux 拓撲的詳細資訊，請參閱 [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。

## <a name="download-and-compile-hello-project"></a>下載並編譯 hello 專案

1. 在開發環境中，下載 hello 專案從[https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka)，開啟 命令列，並變更您已經下載 hello 專案目錄 toohello 位置。

2. 從 hello **hdinsight storm-java kafka**目錄下，使用 hello 下列命令 toocompile hello 專案，並建立部署的套件：

  ```bash
  mvn clean package
  ```

    hello 封裝程序會建立名為`KafkaTopology-1.0-SNAPSHOT.jar`在 hello`target`目錄。

3. 使用下列命令 toocopy hello 封裝 tooyour Storm HDInsight 叢集上的 hello。 取代**USERNAME** hello 叢集 hello SSH 使用者名稱。 取代**BASENAME** hello 基底名稱與您在建立時使用 hello 叢集。

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    出現提示時，輸入 hello 建立 hello 叢集時所使用的密碼。

## <a name="configure-hello-topology"></a>設定 hello 拓撲

1. 使用其中一種下列方法 toodiscover hello hello Kafka broker 主機：

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > hello Bash 範例假設`$CLUSTERNAME`包含 hello hello HDInsight 叢集名稱。 它也假設已安裝 [jq](https://stedolan.github.io/jq/)。 出現提示時，輸入 hello 密碼 hello 叢集登入帳戶。

    傳回的 hello 值是類似 toohello 下列文字：

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > 雖然可能會有兩個以上的 broker 主機叢集，您不需要 tooprovide 所有主機 tooclients 的完整清單。 列出一兩個主機便已足夠。

2. 使用下列方法 toodiscover hello Kafka 動物園管理員主機 hello 的其中一個：

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > hello Bash 範例假設`$CLUSTERNAME`包含 hello hello HDInsight 叢集名稱。 它也假設已安裝 [jq](https://stedolan.github.io/jq/)。 出現提示時，輸入 hello 密碼 hello 叢集登入帳戶。

    傳回的 hello 值是類似 toohello 下列文字：

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > 兩個以上的動物園管理員節點時，您不需要 tooprovide 所有主機 tooclients 的完整清單。 列出一兩個主機便已足夠。

    儲存這個值以便稍後使用。

3. 編輯 hello `dev.properties` hello hello 專案根目錄中的檔案。 此檔案中加入 hello Broker 和動物園管理員主機資訊 toohello 相符的行。 hello 下列範例會使用設定 hello 先前步驟中的 hello 範例值：

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. 儲存 hello`dev.properties`檔案，然後使用 hello 下列命令 tooupload 它 toohello Storm 叢集：

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    取代**USERNAME** hello 叢集 hello SSH 使用者名稱。 取代**BASENAME** hello 基底名稱與您在建立時使用 hello 叢集。

## <a name="start-hello-writer"></a>啟動 hello 寫入器

1. 使用 hello 遵循使用 SSH tooconnect toohello Storm 叢集。 取代**USERNAME** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。 取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    出現提示時，輸入 hello 建立 hello 叢集時所使用的密碼。
   
    如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 從 hello SSH 連線，使用下列命令 toocreate hello Kafka 主題 hello 拓撲所使用的 hello:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    取代`$KAFKAZKHOSTS`hello 動物園管理員與裝載您擷取 hello 前一節中的資訊。

2. 從 hello SSH 連線 toohello Storm 叢集，使用下列命令 toostart hello 寫入器拓撲 hello:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    此命令搭配使用的 hello 參數如下：

    * `org.apache.storm.flux.Flux`： 使用變動 tooconfigure，並執行此拓撲。

    * `--remote`： 送出 hello 拓撲 tooNimbus。 hello 拓撲會分佈在 hello hello 叢集中的背景工作節點。

    * `-R /writer.yaml`： 使用 hello`writer.yaml`檔案 tooconfigure hello 拓撲。 `-R`表示此資源包含在 hello jar 檔案。 它是在 hello jar hello 根目錄中因此`/writer.yaml`是 hello 路徑 tooit。

    * `--filter`: Hello 中的項目填入`writer.yaml`使用 hello 中值的拓樸`dev.properties`檔案。 例如，hello hello 值`kafka.topic`hello 檔案中的項目是使用的 tooreplace hello `${kafka.topic}` hello 拓撲定義項目。

5. Hello 拓撲啟動之後，使用下列命令 tooverify 其正寫入資料 toohello Kafka 主題 hello:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    取代`$KAFKAZKHOSTS`hello 動物園管理員與裝載您擷取 hello 前一節中的資訊。

    此命令會使用隨附於 Kafka toomonitor hello 主題的指令碼。 隨後，它應該開始傳回隨機句子已寫入 toohello 主題。 hello 輸出是 toohello 類似下列範例程式碼：

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    使用 Ctrl + c toostop hello 指令碼。

## <a name="start-hello-reader"></a>啟動 hello 讀取器

1. 從 hello SSH 工作階段 toohello Storm 叢集，使用下列命令 toostart hello 讀取器拓撲 hello:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. 一旦 hello 拓樸開始，開啟 hello Storm UI。 此 Web UI 位於 https://storm-BASENAME.azurehdinsight.net/stormui。 取代__BASENAME__ hello hello 叢集建立時使用的基底名稱。 

    出現提示時，使用 hello 管理員登入名稱 (預設值， `admin`) 和 hello 叢集建立時使用的密碼。 您會看到下列映像網頁類似 toohello:

    ![Storm UI](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. 從 hello Storm UI 中，選取 hello __kafka 讀取器__hello 中的連結__拓撲摘要__區段 toodisplay 資訊 hello __kafka 讀取器__拓撲。

    ![拓樸 hello Storm web UI 的 [摘要] 區段](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay 資訊 hello 元件的執行個體 hello 記錄器閃電，選取 hello__記錄器閃電__hello 中的連結__攻擊 （所有時間）__ > 一節。

    ![Hello 發射區段中的記錄器閃電連結](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. 在 hello__執行程式__區段中，選取 hello 中的連結__連接埠__hello 元件的這個執行個體的資料行 toodisplay 記錄資訊。

    ![執行程式連結](./media/hdinsight-apache-storm-with-kafka/executors.png)

    hello 記錄檔會包含讀取自 hello Kafka 主題的 hello 資料的記錄檔。 hello 記錄檔中的 hello 資訊是類似 toohello 下列文字：

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>停止 hello 拓撲

從 SSH 工作階段 toohello Storm 叢集中，使用下列命令 toostop hello Storm 拓撲 hello:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。 正在刪除 hello 資源群組中移除遵循本文件所建立的所有資源。

## <a name="next-steps"></a>後續步驟

如需更多可搭配 Storm on HDInsight 使用的拓撲範例，請參閱 [Storm 拓撲和元件範例](hdinsight-storm-example-topology.md)。

如需部署和監視以 Linux 為基礎的 HDInsight 上的拓撲相關資訊，請參閱[部署和管理以 Linux 為基礎的 HDInsight 上的 Apache Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)