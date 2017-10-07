---
title: "使用 Azure HDInsight aaaTroubleshoot Storm |Microsoft 文件"
description: "取得有關 Azure HDInsight 搭配使用 Apache Storm 的 toocommon 問題的解答。"
keywords: "Azure HDInsight, Storm, 常見問題集, 疑難排解指南, 常見問題"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>使用 Azure HDInsight 為 Storm 進行疑難排解

了解 hello 最常發生的問題以及其使用中 Apache Ambari Apache Storm 承載的解析度。

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>如何存取在叢集上的 hello Storm UI
您有兩個選項可從瀏覽器存取 hello Storm UI:

### <a name="ambari-ui"></a>Ambari UI
1. 移 toohello Ambari 儀表板。
2. 在 hello 服務清單中，選取  **Storm**。
3. 在 hello**快速連結**功能表上，選取**Storm UI**。

### <a name="direct-link"></a>直接連結
您可以存取下列 URL 的 hello 在 hello Storm UI:

https://\<叢集 DNS 名稱\>/stormui

範例：

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>如何在從一個拓撲 tooanother 轉移 Storm 事件中樞 spout 檢查點資訊

在開發時從 Azure 事件中心使用 hello HDInsight Storm 事件中樞 spout 檔案的讀取的拓撲，您必須部署有相同的名稱，在新叢集的 hello 的拓撲。 不過，您必須保留 hello 已認可的 tooApache 動物園管理員 hello 舊叢集上的檢查點資料。

### <a name="where-checkpoint-data-is-stored"></a>檢查點資料的儲存位置
位移的檢查點資料會儲存 hello 事件中樞 spout 動物園管理員在兩個根路徑中：
- 非交易式 Spout 檢查點會儲存在 /eventhubspout 中。
- 交易式 Spout 檢查點資料會儲存在 /transactional 中。

### <a name="how-toorestore"></a>如何 toorestore
tooget hello 指令碼和程式庫使用 tooexport 動物園管理員中的資料，然後匯入 hello 資料回復 tooZooKeeper 以新名稱，請參閱[HDInsight Storm 範例](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0)。

hello lib 資料夾有包含 hello hello 匯出/匯入作業之實作的 d 檔案。 hello bash 資料夾已經示範如何從 tooexport 資料 hello 動物園管理員伺服器 hello 舊叢集上的範例指令碼，並將它匯入後 toohello 動物園管理員伺服器 hello 新叢集上。

執行 hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello 動物園管理員節點 tooexport 從指令碼，然後匯入資料。 更新 hello 指令碼 toohello 正確 Hortonworks Data Platform (HDP) 版本。 (我們正致力於讓這些指令碼在 HDInsight 中成為泛型。 泛型指令碼可以從任何節點上執行而不需修改 hello 使用者 hello 叢集。）

hello 匯出命令寫入 hello 中繼資料 tooan Apache Hadoop 分散式檔案系統 (HDFS) 路徑 （在 Azure Blob 儲存體或 Azure Data Lake Store 市集中） 在您設定的位置。

### <a name="examples"></a>範例

#### <a name="export-offset-metadata"></a>匯出位移中繼資料
1. 從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。
2. Hello 執行的下列命令 （在您更新 HDP 版本字串 hello） 之後 tooexport 動物園管理員位移資料 toohello /stormmetadta/zkdata HDFS 路徑：

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>匯入位移中繼資料
1. 從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。
2. 執行 hello 下列命令 （在您更新 hello HDP 版本字串） 之後 tooimport 動物園管理員位移 hello HDFS 路徑/stormmetadata/zkdata toohello 動物園管理員伺服器 hello 目標叢集上的資料：

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>刪除位移的中繼資料，以便拓撲可以開始處理 hello 開頭的資料，或該 hello 使用者選擇的時間戳記
1. 從哪些 hello 檢查點位移必須 toobe 匯出的 hello 叢集上使用 SSH toogo toohello 動物園管理員叢集。
2. 執行 hello 下列命令 （在您更新 hello HDP 版本字串） 之後所有 toodelete 動物園管理員位移 hello 目前叢集中的資料：

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>如何找出叢集上的 Storm 二進位檔
Hello 目前 HDP 堆疊的 storm 二進位檔位於 /usr/hdp/current/storm-client。 hello 位置是 hello 相同的前端節點和背景工作節點。
 
/usr/hdp 中可能會有特定 HDP 版本的多個二進位檔 (例如 /usr/hdp/2.5.0.1233/storm)。 hello /usr/hdp/current/storm-client 資料夾是 symlinked toohello 最新版本 hello 叢集上執行。

如需詳細資訊，請參閱[使用 SSH 連線 tooan HDInsight 叢集](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)和[Storm](http://storm.apache.org/)。
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>我要如何判斷 hello Storm 叢集部署拓撲
首先，找出所有與 HDInsight Storm 一起安裝的元件。 Storm 叢集包含四個節點類別：

* 閘道節點
* 前端節點
* ZooKeeper 節點
* 背景工作節點
 
### <a name="gateway-nodes"></a>閘道節點
閘道節點是閘道和反向 proxy 服務，可讓公用存取 tooan active Ambari 管理服務。 它也可以處理 Ambari 前置選擇。
 
### <a name="head-nodes"></a>前端節點
Storm 前端節點執行下列服務的 hello:
* Nimbus
* Ambari 伺服器
* Ambari 計量伺服器
* Ambari 計量收集器
 
### <a name="zookeeper-nodes"></a>ZooKeeper 節點
HDInsight 隨附一個三節點的 ZooKeeper 仲裁。 hello 仲裁大小固定，且無法重新設定。
 
Hello 叢集中的 storm 服務是設定的 tooautomatically 使用 hello 動物園管理員仲裁。
 
### <a name="worker-nodes"></a>背景工作節點
Storm 背景工作節點執行下列服務的 hello:
* 監督員
* 背景工作 Java 虛擬機器 (JVM)，用於執行拓樸
* Ambari 代理程式
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>如何找出用於開發的 Storm 事件中樞 Spout 二進位檔
 
如需搭配使用 Storm 事件中樞 spout d 檔案與您的拓撲的詳細資訊，請參閱下列資源的 hello。
 
### <a name="java-based-topology"></a>Java 型拓撲
[使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C# 型拓撲 (HDInsight 3.4+ Linux Storm 叢集上的 Mono)
[利用 Storm on HDInsight 處理 Azure 事件中樞的事件 (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>適用於 HDInsight 3.5+ Linux Storm 叢集的最新 Storm 事件中樞 Spout 二進位檔
toolearn 如何 toouse hello 最新出現事件中樞 spout HDInsight 3.5 + 適用於 Linux Storm 叢集，請參閱 hello mvn 儲存機制[讀我檔案](https://github.com/hdinsight/mvn-repo/blob/master/README.md)。
 
### <a name="source-code-examples"></a>原始程式碼範例
請參閱[範例](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)方式的 tooread 從 Azure 事件中心的 Azure HDInsight 叢集上使用 （以 Java 撰寫的） Apache Storm 拓樸和寫入。
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>如何找出叢集上的 Storm Log4J 設定檔
 
tooidentify Apache Log4J Storm 服務的組態檔。
 
### <a name="on-head-nodes"></a>在前端節點上
讀取 hello Nimbus Log4J 組態 libodbc/hdp/\<HDP 版本\>/storm/log4j2/cluster.xml。
 
### <a name="on-worker-nodes"></a>在背景工作節點上
讀取 hello 監督員 Log4J 組態 libodbc/hdp/\<HDP 版本\>/storm/log4j2/cluster.xml。
 
讀取 hello 工作者 Log4J 組態檔 libodbc/hdp/\<HDP 版本\>/storm/log4j2/worker.xml。
 
範例：/usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

