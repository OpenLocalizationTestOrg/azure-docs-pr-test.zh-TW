---
title: "使用 Apache Kafka-Azure HDInsight aaaStart |Microsoft 文件"
description: "了解 toocreate Apache Kafka Azure HDInsight 上的叢集化。 深入了解如何 toocreate 主題、 訂閱者與取用者。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>開始在 HDInsight 上使用 Apache Kafka (預覽)

深入了解如何 toocreate 並用[Apache Kafka](https://kafka.apache.org)上 Azure HDInsight 叢集。 Kafka 是 HDInsight 提供的開放原始碼分散式串流平台。 通常是當做訊息仲介，因為它提供了類似的功能 tooa 發行-訂閱訊息佇列。

> [!NOTE]
> HDInsight 目前提供兩個 Kafka 版本：0.9.0 (HDInsight 3.4) 和 0.10.0 (HDInsight 3.5 和 3.6)。 本文件中的 hello 步驟假設您使用 Kafka HDInsight 3.6 上。

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>建立 Kafka 叢集

使用下列步驟 toocreate Kafka HDInsight 叢集上的 hello:

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增**，**智慧 + 分析**，然後選取**HDInsight**。
   
    ![建立 HDInsight 叢集](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. 從**基本概念**，輸入下列資訊的 hello:

    * **叢集名稱**: hello hello HDInsight 叢集名稱。
    * **訂用帳戶**： 選取 hello 訂用帳戶 toouse。
    * **叢集登入使用者名稱**和**叢集登入密碼**: hello 登入透過 HTTPS 存取 hello 叢集時。 您使用這些認證 tooaccess 服務，例如 hello Ambari Web UI 或 REST API。
    * **安全殼層 (SSH) 的使用者名稱**: hello 透過 SSH 存取 hello 叢集時使用的登入。 根據預設 hello 密碼是 hello hello 叢集登入密碼相同。
    * **資源群組**: hello 資源群組 toocreate hello 叢集中。
    * **位置**: hello Azure 地區 toocreate hello 叢集中。
   
 ![選取訂用帳戶](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. 選取**叢集類型**，然後組 hello 遵循值**叢集設定**:
   
    * **叢集類型**：Kafka

    * **版本**：Kafka 0.10.0 (HDI 3.6)

    * **叢集層**：標準
     
 最後，使用 hello**選取**按鈕 toosave 設定。
     
 ![選取叢集類型](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. 選取 hello 叢集類型後，使用 hello__選取__按鈕 tooset hello 叢集類型。 接下來，使用 hello__下一步__按鈕 toofinish 基本組態。

5. 從 [儲存體]，選取或建立儲存體帳戶。 如需本文件中的 hello 步驟，hello 其他欄位保留在 hello 預設值。 使用 hello__下一步__按鈕 toosave 存放裝置設定。

    ![設定 hello HDInsight 的儲存體帳戶設定](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. 從__應用程式 （選擇性）__，選取__下一步__toocontinue。 這個範例不需要任何應用程式。

7. 從__叢集大小__，選取__下一步__toocontinue。

    > [!WARNING]
    > HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。

    ![設定 hello Kafka 叢集大小](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > hello**磁碟每個背景工作節點**項目控制項 hello Kafka HDInsight 上的延展性。 如需詳細資訊，請參閱[設定 HDInsight 上 Kafka 的儲存體和延展性](hdinsight-apache-kafka-scalability.md)。

8. 從__進階設定__，選取__下一步__toocontinue。

9. 從 hello**摘要**，檢閱 hello hello 叢集組態。 使用 hello__編輯__連結 toochange 任何不正確的設定。 最後，使用 the__Create__ 按鈕 toocreate hello 叢集。
   
    ![叢集組態摘要](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > 它可能會佔用 too20 分鐘 toocreate hello 叢集。

## <a name="connect-toohello-cluster"></a>Toohello 叢集連線

> [!IMPORTANT]
> 在執行下列步驟的 hello 時，您必須使用 SSH 用戶端。 如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

從您的用戶端使用 SSH tooconnect toohello 叢集：

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

取代**SSHUSER**與 hello 您在叢集建立期間所提供的 SSH 使用者名稱。 取代**CLUSTERNAME** hello hello 叢集名稱。

出現提示時，輸入您所使用的 hello SSH 帳戶的 hello 密碼。

如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a id="getkafkainfo"></a>取得 hello 動物園管理員和代理人主機資訊

當使用 Kafka，您必須知道兩個主機的值;hello*動物園管理員*主機和 hello *Broker*主機。 這些主控件用於 Kafka 有 hello Kafka API 和出貨的 hello 公用程式的許多。

使用下列步驟 toocreate 環境變數包含 hello 主機資訊的 hello。 本文件中的 hello 步驟中使用這些環境變數。

1. SSH 連線 toohello 叢集中，從使用 hello 下列的命令 tooinstall hello`jq`公用程式。 此公用程式是使用的 tooparse JSON 文件，並在擷取 hello broker 主機資訊非常有用：
   
    ```bash
    sudo apt -y install jq
    ```

2. 從 Ambari，下列命令使用 hello 擷取 tooset hello 環境變數的資訊：

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > 設定`CLUSTERNAME=`toohello hello Kafka 叢集名稱。 設定`PASSWORD=`toohello （管理員） 登入密碼時建立 hello 叢集所使用。

    hello 下列文字是 hello 內容的範例`$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    hello 下列文字是 hello 內容的範例`$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > hello`cut`命令是使用的 tootrim hello 份主機 tootwo 主機項目。 建立 Kafka 取用者或生產者時不需要主機 tooprovide hello 完整的清單。
   
    > [!WARNING]
    > 請勿依賴 hello 資訊從這個工作階段傳回 tooalways 會精確。 如果您調整 hello 叢集時，新的代理程式加入或移除。 如果發生失敗且節點更換時，可能會變更 hello hello 節點的主機名稱。
    >
    > 使用具有有效的資訊 tooensure 的不久之前，您應該擷取 hello 動物園管理員和代理人主機資訊。

## <a name="create-a-topic"></a>建立主題

Kafka 會將資料串流儲存在名為 *topics* 的類別中。 SSH 連線 tooa 叢集前端節點，從使用 Kafka toocreate 主題所提供的指令碼：

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

此命令會連線使用 hello 主機資訊儲存在 tooZookeeper `$KAFKAZKHOSTS`，然後建立名為 Kafka 主題**測試**。 您可以確認該 hello 主題建立使用下列指令碼 toolist 主題 hello:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

hello 輸出此命令會列出 Kafka 主題，其中包含 hello**測試**主題。

## <a name="produce-and-consume-records"></a>產生和取用記錄

Kafka 會在主題中儲存「記錄」。 記錄是由「產生者」產生，並由「取用者」取用。 產生者會從 Kafka「訊息代理程式」擷取記錄。 HDInsight 叢集中的每個背景工作節點都是 Kafka 訊息代理程式。

使用您先前建立並使用取用者讀取 hello 測試主題到下列步驟 toostore 記錄 hello:

1. 從 hello SSH 工作階段，使用 Kafka toowrite 記錄 toohello 主題所提供的指令碼：
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    您不會傳回 toohello 提示這個命令之後。 相反地，輸入一些文字訊息，然後使用**Ctrl + C** toostop 傳送 toohello 主題。 每一行都會以個別的記錄傳送。

2. 使用 Kafka tooread 記錄從 hello 主題所提供的指令碼：
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    此命令會擷取 hello 主題中的 hello 記錄，並加以顯示。 使用`--from-beginning`hello 開頭 hello 資料流，從告訴 hello 消費者 toostart，因此會擷取所有記錄。

3. 使用__Ctrl + C__ toostop hello 取用者。

## <a name="producer-and-consumer-api"></a>產生者和取用者 API

您也以程式設計方式產生並使用記錄使用 hello [Kafka Api](http://kafka.apache.org/documentation#api)。 toobuild Java 生產者和取用者，請使用下列步驟，從您的開發環境的 hello。

> [!IMPORTANT]
> 您必須擁有下列元件安裝在您的開發環境中的 hello:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 或同等功能版本，例如 OpenJDK。
>
> * [Apache Maven](http://maven.apache.org/)
>
> * SSH 用戶端與 hello`scp`命令。 如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

1. 下載從 hello 範例[https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started)。 Hello 生產者/消費者使用範例的 hello 專案在 hello`Producer-Consumer`目錄。 這個範例包含下列類別的 hello:
   
    * **執行**-啟動 hello 取用者或產生者。

    * **生產者**-存放區 1,000,000 個記錄 toohello 主題。

    * **取用者**-hello 主題會讀取記錄。

2. toocreate jar 封裝時，變更目錄 toohello 位置 hello`Producer-Consumer`目錄，並使用下列命令的 hello:

    ```
    mvn clean package
    ```

    此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-producer-consumer-1.0-SNAPSHOT.jar` 的檔案。

3. 使用 hello 下列命令 toocopy hello`kafka-producer-consumer-1.0-SNAPSHOT.jar`檔案 tooyour HDInsight 叢集：
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    取代**SSHUSER**與您的叢集，以及取代 hello SSH 使用者**CLUSTERNAME**與 hello 叢集的名稱。 出現提示時輸入 hello SSH 使用者 hello 密碼。

4. 一次 hello`scp`命令完成複製 hello 檔案中，使用 SSH toohello 叢集連線。 使用下列命令 toowrite 記錄 toohello 測試主題 hello:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. 一旦完成 hello 程序，使用 hello 主題中的下列命令 tooread hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    會顯示 hello 記錄讀取，以及記錄的計數。 您可能會看到幾個以上的 1000000 記錄，因為傳送數個記錄 toohello 主題在先前步驟中使用指令碼。

6. 使用__Ctrl + C__ tooexit hello 取用者。

### <a name="multiple-consumers"></a>多個取用者

Kafka 取用者會在讀取記錄時使用取用者群組。 搭配多個取用者使用相同群組中的 hello 導致負載平衡主題的讀取次數。 Hello 群組中的每一個取用者會收到 hello 記錄的一部分。 toosee 在動作中，使用 hello 遵循此程序的步驟：

1. 開啟新的 SSH 工作階段 toohello 叢集，讓您有兩個。 在每個工作階段中，使用 hello toostart 下列與取用者 hello 相同取用者群組識別碼：
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    此命令會啟動使用 hello 群組識別碼的消費者`mygroup`。

    > [!NOTE]
    > 使用中 hello hello 指令[取得 hello 動物園管理員和代理人主機資訊](#getkafkainfo)區段 tooset`$KAFKABROKERS`此 SSH 工作階段。

2. 觀看為在收到 hello 主題的每個工作階段計數 hello 記錄。 兩個工作階段的 hello 總數應該 hello 相同一個取用者從先前接收。

用戶端 hello 相同的群組透過 hello 主題的 hello 資料分割內的耗用量。 Hello`test`稍早建立的主題有八個資料分割。 如果您開啟八個的 SSH 工作階段，並在所有工作階段中啟動取用者，每一個取用者會從 hello 主題的單一資料分割讀取記錄。

> [!IMPORTANT]
> 一個取用者群組中的取用者執行個體不得超過資料分割。 在此範例中，一個取用者群組可以包含總 tooeight 取用者，因為這是 hello hello 主題中的資料分割數目。 或者，您可以有多個取用者群組，其各有不超過 8 個取用者。

Kafka 中儲存的記錄會儲存在資料分割內收到 hello 順序。 受 tooachieve 中排序的傳遞記錄*資料分割內*，建立取用者群組取用者執行個體的 hello 數目要比對資料分割的 hello 數目。 受 tooachieve 中排序的傳遞記錄*hello 主題內*，使用只有一個取用者執行個體建立取用者群組。

## <a name="streaming-api"></a>串流 API

資料流 API hello 版已加入 tooKafka 在 0.10.0;舊版依賴 Apache Spark 或 Storm 進行資料流處理。

1. 如果您尚未這樣做，請下載 hello 範例從[https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour 開發環境。 Hello 串流範例，請同時使用 hello 專案 hello`streaming`目錄。
   
    此專案包含一個類別， `Stream`，記錄讀取從 hello`test`先前建立的主題。 它會計算 hello 字讀取，而發出名為每個 word 和計數 tooa 主題`wordcounts`。 hello`wordcounts`建立稍後的步驟，本節中的主題。

2. 從開發環境中的 hello 命令列，變更目錄 toohello 位置 hello`Streaming`目錄，然後使用下列命令 toocreate jar 封裝的 hello:

    ```bash
    mvn clean package
    ```

    此命令會建立名為 `target` 的目錄，其中包含名為 `kafka-streaming-1.0-SNAPSHOT.jar` 的檔案。

3. 使用 hello 下列命令 toocopy hello`kafka-streaming-1.0-SNAPSHOT.jar`檔案 tooyour HDInsight 叢集：
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    取代**SSHUSER**與您的叢集，以及取代 hello SSH 使用者**CLUSTERNAME**與 hello 叢集的名稱。 出現提示時輸入 hello SSH 使用者 hello 密碼。

4. 一次 hello`scp`命令完成 hello 檔案複製，toohello 叢集使用 SSH 連線，並接著使用下列命令 toocreate hello hello`wordcounts`主題：

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. 接下來，啟動串流處理程序使用下列命令的 hello hello:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    此命令啟動 hello 串流中 hello 背景處理程序。

6. 使用 hello 下列命令 toosend 訊息 toohello`test`主題。 Hello 串流範例處理這些訊息：
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. 使用下列命令 tooview hello 輸出寫入 toohello 的 hello `wordcounts` hello 串流處理程序的主題：
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello 資料，您必須告訴 hello 消費者 tooprint hello 索引鍵和 hello 還原序列化程式 toouse hello 索引鍵和值。 hello 索引鍵名稱是 hello 單字，而 hello 索引鍵值包含 hello 計數。
   
    hello 輸出是類似 toohello 下列文字：
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > hello 計數會遞增每次遇到一個字。

7. 使用 hello __Ctrl + C__ tooexit hello 取用者，然後使用 hello `fg` toobring hello 串流處理的背景工作後 toohello 前景的命令。 使用__Ctrl + C__ tooexit 它也。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟

在本文件中，您已經學會使用 Apache Kafka HDInsight 上的 hello 基本。 使用下列詳細資料使用 Kafka toolearn hello:

* [使用 HDInsight 上的 Kafka 確保您資料的高可用性](hdinsight-apache-kafka-high-availability.md)
* [使用 HDInsight 上的 Kafka 設定受控磁碟來提高延展性](hdinsight-apache-kafka-scalability.md)
* kafka.apache.org 上的 [Apache Kafka 文件](http://kafka.apache.org/documentation.html)。
* [在 HDInsight 上使用 MirrorMaker toocreate Kafka 的複本](hdinsight-apache-kafka-mirroring.md)
* [使用 Apache Storm 搭配 HDInsight 上的 Kafka](hdinsight-apache-storm-with-kafka.md)
* [使用 Apache Spark 搭配 Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)
* [透過 Azure 虛擬網路連線 tooKafka](hdinsight-apache-kafka-connect-vpn-gateway.md)
