---
title: "使用 Apache Storm 和 HBase aaaAnalyze 感應器資料 |Microsoft 文件"
description: "深入了解如何 tooconnect tooApache Storm 與虛擬網路。 使用 Storm HBase tooprocess 感應器資料，從事件中心並視覺化與 D3.js。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>在 HDInsight (Hadoop) 中使用 Apache Storm、事件中樞和 HBase 分析感應器資料

深入了解如何 toouse Apache Storm 的 HDInsight tooprocess 感應器資料是來自 Azure 事件中心。 hello 資料會儲存到在 HDInsight 上的 Apache HBase，並使用 D3.js 以視覺化方式檢視。

本文件中使用的 hello Azure Resource Manager 範本會示範如何 toocreate 資源群組中的多個 Azure 資源。 hello 範本會建立 Azure 虛擬網路、 兩個的 HDInsight 叢集 （Storm 和 HBase） 和 Azure Web 應用程式。 即時 web 儀表板的 node.js 實作是自動部署的 toohello web 應用程式。

> [!NOTE]
> 此文件和範例，在這份文件中的 hello 資訊需要 HDInsight 3.6 版。
>
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="prerequisites"></a>必要條件

* Azure 訂用帳戶。
* [Node.js](http://nodejs.org/)： 使用的 toopreview hello web 儀表板在您的開發環境的本機上。
* [Java 和 hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html)： 使用 toodevelop hello Storm 拓撲。
* [Maven](http://maven.apache.org/what-is-maven.html)： 使用的 toobuild 和編譯 hello 專案。
* [Git](http://git-scm.com/)： 從 GitHub 使用的 toodownload hello 專案。
* **SSH**用戶端： 使用 tooconnect toohello 以 Linux 為基礎的 HDInsight 叢集。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。


> [!IMPORTANT]
> 您不需刪除現有的 HDInsight 叢集。 本文件中的 hello 步驟建立 hello 下列資源：
> 
> * Azure 虛擬網路
> * Storm on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)
> * HBase on HDInsight 叢集 (以 Linux 為基礎，兩個背景工作節點)
> * Azure Web 應用程式裝載 hello web 儀表板

## <a name="architecture"></a>架構

![架構圖表](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

這個範例包含下列元件的 hello:

* **Azure 事件中樞**：包含從感應器收集的資料。
* **Storm on HDInsight**：即時處理事件中樞的資料。
* **HBase on HDInsight**：針對 Storm 所處理過的資料，提供持續的 NoSQL 資料存放區。
* **Azure 虛擬網路服務**: hello HDInsight 上的 Storm 之間 HBase HDInsight 叢集上的安全通訊。
  
  > [!NOTE]
  > 使用 hello Java HBase 用戶端應用程式開發介面時，需要虛擬網路。 它不會顯示 hello 公用閘道 HBase 叢集的移轉。 安裝 HBase 和 Storm 叢集至相同虛擬網路可讓的 hello hello Storm 叢集 （或任何其他 hello 虛擬網路上的系統） toodirectly 存取 HBase 使用用戶端應用程式開發介面。

* **儀表板網站**：即時建立資料圖表的範例儀表板。
  
  * Node.js 被實作 hello 網站。
  * [Socket.io](http://socket.io/)用於 hello Storm 拓撲與 hello 網站之間的即時通訊。
    
    > [!NOTE]
    > 使用 Socket.io 進行通訊是實作細節。 您可以使用任何通訊架構，例如原始 WebSockets 或 SignalR。

  * [D3.js](http://d3js.org/)傳送 toohello 網站使用的 toograph hello 資料。

> [!IMPORTANT]
> 因為沒有任何支援的方法 toocreate 一個 HDInsight 叢集的 Storm 和 HBase 需要，這兩個叢集。

hello 拓樸，讀取事件中心使用 hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html)類別，並將資料寫入至 HBase 使用 hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html)類別。 與 hello 網站的通訊透過使用[socket.io client.java](https://github.com/nkzawa/socket.io-client.java)。

hello 下列圖表說明拓撲 hello 的 hello 版面配置：

![拓撲圖](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> 此圖表是 hello 拓撲的簡化的檢視。 系統會針對事件中樞的每個分割區，為各元件建立執行個體。 這些執行個體分散於 hello hello 叢集中的節點和資料之間路由它們，如下所示：
> 
> * 負載平衡來自 hello spout toohello 剖析器的資料。
> * Hello 剖析器 toohello 儀表板和 HBase 中資料的分組依據裝置識別碼，以便從訊息 hello 相同的裝置一律流程 toohello 同一個元件。

### <a name="topology-components"></a>拓撲元件

* **事件中樞 Spout**: hello spout 是在提供的 Apache Storm 版本 0.10.0 及更高版本。
  
  > [!NOTE]
  > 此範例中使用的 hello 事件中心 spout 需要 HDInsight 叢集版本 3.5 或 3.6 上的出現。

* **ParserBolt.java**: hello spout 發出的 hello 資料未經處理的 JSON，而且有時候多個事件，就會發出一次。 此閃電讀取 spout hello hello 所發出的資料，並剖析 hello JSON 訊息。 hello 閃電再發出 hello 資料當做元組，其中包含多個欄位。
* **DashboardBolt.java**： 此元件會示範如何 toouse hello Socket.io Java toosend 資料即時 toohello web 儀表板中的用戶端程式庫。
* **否 hbase.yaml**: hello 在本機模式中執行時所使用的拓撲定義。 這不會使用到 HBase 的元件。
* **與 hbase.yaml**: hello hello 叢集上執行 hello 拓撲時所使用的拓撲定義。 這會使用到 HBase 的元件。
* **dev.properties**: hello hello 事件中心 spout、 HBase 閃電和儀表板元件的組態資訊。

## <a name="prepare-your-environment"></a>準備您的環境

使用此範例之前，您必須建立 Azure 事件中心，從讀取的 hello Storm 拓撲。

### <a name="configure-event-hub"></a>設定事件中樞

事件中心是此範例中的 hello 資料來源。 使用下列步驟 toocreate 事件中心的 hello。

1. 從 hello [Azure 入口網站](https://portal.azure.com)，選取**+ 新增** -> **物聯網** -> **事件中心**。
2. 在 hello**建立命名空間**區段中，執行下列工作的 hello:
   
   1. 輸入**名稱**hello 命名空間。
   2. 選取定價層。  就已足夠。
   3. 選取 hello Azure**訂用帳戶**toouse。
   4. 選取現有的資源群組，或建立一個新的群組。
   5. 選取 hello**位置**hello 事件中心。
   6. 選取**Pin toodashboard**，然後按一下**建立**。

3. Hello 建立程序完成時，會顯示 hello 事件中樞命名空間的資訊。 從這裡選取 [+ 新增事件中樞] 。 在 hello**建立事件中樞**區段中，輸入名稱**sensordata**，然後選取**建立**。 保留 hello hello 預設值，其他欄位。
4. 從 hello 事件中樞命名空間，選取的檢視**事件中心**。 選取 hello **sensordata**項目。
5. 從 hello sensordata 事件中樞，選取**共用存取原則**。 使用 hello **+ 加**連結 tooadd hello 下列原則：

    | 原則名稱 | Claims |
    | ----- | ----- |
    | devices | 傳送 |
    | storm | 接聽 |

1. 選取這兩個原則，並記下 hello**主索引鍵**值。 您需要在未來的步驟中這兩個原則 hello 值。

## <a name="download-and-configure-hello-project"></a>下載並設定 hello 專案

使用 hello GitHub 中的下列 toodownload hello 專案。

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Hello 命令完成之後，您會有下列目錄結構的 hello:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> 這份文件不討論 toofull hello 本範例中包含的程式碼的詳細資料。 不過，完整註解 hello 程式碼。

從事件中樞，開啟 hello tooconfigure hello 專案 tooread`hdinsight-eventhub-example/TemperatureMonitor/dev.properties`檔案，然後加入您的事件中樞資訊 toohello 下列行：

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>編譯並在本機測試

> [!IMPORTANT]
> 在本機使用 hello 拓撲需要使用 Storm 開發環境。 如需詳細資訊，請至 Apache.org 參閱[設定 Storm 開發環境](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html)。

> [!WARNING]
> 如果您使用的 Microsoft 開發環境，您可能會收到`java.io.IOException`時在本機執行 hello 拓撲。 如果是這樣，移動 toorunning hello 拓樸 HDInsight 上。

在測試之前，必須開始 hello hello 拓樸的儀表板 tooview hello 輸出，然後產生資料 toostore 在事件中樞。

> [!IMPORTANT]
> 在本機測試時，這種拓撲的 hello HBase 元件未啟用。 無法從外部 hello 包含 hello 叢集的 Azure 虛擬網路中存取 hello Java 應用程式開發介面 hello HBase 叢集。

### <a name="start-hello-web-application"></a>啟動 hello web 應用程式

1. 開啟命令提示字元，然後將目錄變更太`hdinsight-eventhub-example/dashboard`。 使用下列命令 tooinstall hello 相依性 hello web 應用程式所需的 hello:
   
    ```bash
    npm install
    ```

2. 使用下列命令 toostart hello web 應用程式的 hello:
   
    ```bash
    node server.js
    ```
   
    您會看到下列文字的訊息類似的 toohello:
   
        Server listening at port 3000

3. 開啟網頁瀏覽器並輸入`http://localhost:3000/`hello 位址。 會顯示下列影像頁面類似 toohello:
   
    ![Web 儀表板](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    不要關閉命令提示字元。 測試之後，使用 Ctrl + C toostop hello web 伺服器。

### <a name="generate-data"></a>產生資料

> [!NOTE]
> hello 本節中的步驟使用 Node.js 以便它們可以用於任何平台上。 如需其他語言的範例，請參閱 hello`SendEvents`目錄。

1. 開啟新的提示字元、 殼層或終端機，並將目錄變更太`hdinsight-eventhub-example/SendEvents/nodejs`。 tooinstall hello 相依性所需的 hello 應用程式，使用下列命令的 hello:

    ```bash
    npm install
    ```

2. 開啟 hello`app.js`檔案文字編輯器中，並新增您稍早取得的事件中樞資訊 hello:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > 這個範例假設您已經使用`sensordata`做為事件中樞 hello 名稱。 而且`devices`hello hello 原則具有名稱為`Send`宣告。

3. 使用下列命令 tooinsert 新的項目事件中樞中的 hello:
   
    ```bash
    node app.js
    ```
   
    您會看到的輸出包含 hello 資料的數行傳送 tooEvent 中樞：
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>建置和啟動 hello 拓樸

1. 開啟新的命令提示字元，然後將目錄變更太`hdinsight-eventhub-example/TemperatureMonitor`。 toobuild 和套件 hello 拓撲，請使用下列命令的 hello: 

    ```bash
    mvn clean package
    ```

2. 在本機模式中，下列命令使用 hello toostart hello 拓撲：

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`在本機模式中啟動 hello 拓撲。
    * `--filter`使用 hello`dev.properties`檔案 toopopulate 參數在 hello 拓撲定義。
    * `resources/no-hbase.yaml`使用 hello`no-hbase.yaml`拓撲定義。
 
   一旦啟動，hello 拓撲從事件中心讀取項目，並將它們傳送 toohello 儀表板在您的本機電腦上執行。 您應該會看到顯示 hello web 儀表板，類似 toohello 下列映像中的行：
   
    ![儀表板與資料](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. 當執行 hello 儀表板時，使用 hello`node app.js`命令，從上一個 hello 步驟 toosend 新資料 tooEvent 集線器。 Hello 溫度值會隨機產生，因為 hello 圖形應該更新 tooshow 大量變更的溫度。
   
   > [!NOTE]
   > 您必須在 hello **hdinsight-eventhub-範例/SendEvents/Nodejs**目錄時使用 hello`node app.js`命令。

3. 確認該 hello 儀表板更新時，使用 Ctrl + C 停止 hello 拓撲之後。 您也可以使用 Ctrl + C toostop hello 本機 web 伺服器。

## <a name="create-a-storm-and-hbase-cluster"></a>建立 Storm 和 HBase 叢集

此區段的使用中的 hello 步驟[Azure Resource Manager 範本](../azure-resource-manager/resource-group-template-deploy.md)toocreate hello 虛擬網路上的 Azure 虛擬網路的 Storm 和 HBase 叢集。 hello 範本也會建立 Azure Web 應用程式，並部署到它的 hello 儀表板的複本。

> [!NOTE]
> 虛擬網路使用，以便與 hello HBase 叢集使用 hello HBase Java 應用程式開發介面，即可直接通訊 hello 拓撲 hello Storm 叢集上執行。

使用這份文件中的 hello Resource Manager 範本位於公用 blob 容器**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**。

1. 按一下下列按鈕 toosign 中 tooAzure 和開啟 hello Resource Manager 範本 hello Azure 入口網站中的 hello。
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. 從 hello**自訂部署**區段中，輸入下列值的 hello:
   
    ![HDInsight 參數](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **基底叢集名稱**: hello hello Storm 和 HBase 叢集的基底名稱為使用此值。 例如，輸入 **abc** 會建立名為 **storm-abc** 的 Storm 叢集以及名為 **hbase-abc** 的 HBase 叢集。
   * **叢集登入使用者名稱**: hello Storm 和 HBase 叢集的 hello 系統管理員使用者名稱。
   * **叢集登入密碼**: hello Storm 和 HBase 叢集 hello 管理使用者的密碼。
   * **SSH 使用者名稱**: hello SSH 使用者 toocreate hello Storm 和 HBase 叢集。
   * **SSH 密碼**: hello hello Storm 和 HBase 叢集的 hello SSH 使用者密碼。
   * **位置**: hello 區域 hello 叢集所建立的。
     
     按一下**確定**toosave hello 參數。

3. 使用 hello**基本概念**區段 toocreate 資源群組，或選取現有的我的最愛。
4. 在 hello**資源群組位置**下拉式功能表中，選取 hello 相同的位置，您選取 hello**位置**中 hello 參數**設定**> 一節。
5. 讀取 hello 條款和條件，，然後選取  **toohello 條款和條件前面所述，即表示我同意**。
6. 最後，檢查**Pin toodashboard** ，然後選取 **購買**。 它會採用約 20 分鐘 toocreate hello 叢集。

一旦已建立 hello 資源，則會顯示 hello 資源群組的相關資訊。

![Hello vnet 與叢集資源群組](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> 請注意，hello hello HDInsight 叢集名稱**storm BASENAME**和**hbase BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。 連接 toohello 叢集時，您可以使用稍後步驟中的這些名稱。 請注意，hello hello 儀表板網站的名稱也是**basename 儀表板**。 本文件稍後將使用此值。

## <a name="configure-hello-dashboard-bolt"></a>設定 hello 儀表板閃電

toosend 資料 toohello 儀表板部署為 web 應用程式，您必須修改下列一行 hello hello`dev.properties`檔案：

```yaml
dashboard.uri: http://localhost:3000
```

變更`http://localhost:3000`太`http://BASENAME-dashboard.azurewebsites.net`儲存 hello 檔案。 取代**BASENAME**與 hello hello 上一個步驟中所提供的基底名稱。 您也可以使用先前建立 tooselect hello 儀表板和檢視 hello URL hello 資源群組。

## <a name="create-hello-hbase-table"></a>建立 hello HBase 資料表

對 HBase 中的 toostore 資料，我們必須先建立資料表。 預先建立 Storm 需要 toowrite 到的資源，因為嘗試 toocreate 從內部資源 Storm 拓撲可能會導致多個執行個體嘗試 toocreate hello 相同的資源。 建立 hello hello 拓撲之外的資源並使用 Storm 讀取/寫入與分析。

1. 使用 SSH tooconnect toohello HBase 叢集使用 hello SSH 使用者名稱和您在叢集建立期間提供 toohello 範本的密碼。 例如，如果連接使用 hello`ssh`命令時，您可以使用下列語法的 hello:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    取代`sshuser`hello SSH 使用者名稱與您在建立時提供 hello 叢集。 取代`clustername`與 hello HBase 叢集的名稱。

2. 從 hello SSH 工作階段，啟動 hello HBase 殼層。
   
    ```bash
    hbase shell
    ```
   
    當載入 hello 殼層時，您會看到`hbase(main):001:0>`提示字元。

3. 從 hello HBase 殼層中，輸入下列命令 toocreate 資料表 toostore hello 感應器資料的 hello:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. 請確認已建立該 hello 資料表使用 hello 下列命令：
   
    ```hbase
    scan 'SensorData'
    ```
   
    這會傳回的資訊類似 toohello 下列範例中，指出 hello 資料表中有 0 個資料列。
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. 輸入`exit`tooexit hello HBase 殼層：

## <a name="configure-hello-hbase-bolt"></a>設定 hello HBase 閃電

toowrite tooHBase 從 hello Storm 叢集，您必須提供 hello HBase 閃電 HBase 叢集的 hello 設定詳細資料。

1. 使用下列範例 tooretrieve hello 動物園管理員仲裁 HBase 叢集的 hello 的其中一個：

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > 取代`your_HDInsight_cluster_name`hello 名稱，為您的 HDInsight 叢集。 如需有關安裝 hello`jq`公用程式，請參閱[https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)。
    >
    > 出現提示時，輸入 hello 密碼 hello HDInsight admin 登入。

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > 取代 ' your_HDInsight_cluster_name hello 名稱，為您的 HDInsight 叢集。 出現提示時，輸入 hello 密碼 hello HDInsight admin 登入。
    >
    > 此範例需要 Azure PowerShell。 如需進一步了解 Azure PowerShell 之使用，請參閱 [Azure PowerShell 使用者入門](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)

    這些範例中所傳回的 hello 資訊是類似 toohello 下列文字：

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    與 hello HBase 叢集的 Storm toocommunicate 會使用這項資訊。

2. 修改 hello`dev.properties`檔案，然後加入下列行 hello 動物園管理員仲裁資訊 toohello:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>建置、 封裝和部署 hello 方案 tooHDInsight

在開發環境中，使用下列步驟 toodeploy hello Storm 拓撲 toohello storm 叢集 hello。

1. 從 hello`TemperatureMonitor`目錄下，使用 hello 下列命令 tooperform 新的組建，並從您的專案建立 JAR 封裝：
   
        mvn clean package
   
    此命令會在專案的目標目錄中建立名為 `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` 的檔案。

2. 使用 scp tooupload hello`TemperatureMonitor-1.0-SNAPSHOT.jar`和`dev.properties`檔案 tooyour Storm 叢集。 Hello 在下列範例，取代`sshuser`與 hello 建立 hello 叢集時，您所提供的 SSH 使用者和`clustername`hello Storm 叢集名稱。 出現提示時，輸入 hello SSH 使用者 hello 密碼。
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > 它可能需要幾分鐘的時間 tooupload hello 檔案。

    如需有關使用 hello`scp`和`ssh`命令與 HDInsight，請參閱[搭配使用 SSH 和 HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Hello 檔案已上傳，一旦連接使用 SSH toohello Storm 叢集。
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    取代`sshuser`hello SSH 使用者名稱。 取代`clustername`與 hello Storm 叢集名稱。

4. toostart hello 拓撲，請使用下列命令從 hello SSH 工作階段的 hello:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`送出 hello 拓撲 toohello Nimbus 服務，將其發佈 hello 叢集中的 toohello 監督員節點。
    * `--filter`使用 hello`dev.properties`檔案 toopopulate 參數在 hello 拓撲定義。
    * `-R /with-hbase.yaml`使用 hello `with-hbase.yaml` hello 封裝中包含的拓撲。

5. 啟動 hello 拓撲後，開啟您在 Azure，然後使用 hello 發行瀏覽器 toohello 網站`node app.js`命令 toosend 資料 tooEvent 中樞。 您應該會看到 hello web 儀表板更新 toodisplay hello 資訊。
   
    ![儀表板](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>檢視 HBase 資料

使用下列步驟 tooconnect tooHBase hello，並確認 hello 資料，已寫入 toohello 資料表：

1. 使用 SSH tooconnect toohello HBase 叢集。
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    取代`sshuser`hello SSH 使用者名稱。 取代`clustername`與 hello HBase 叢集的名稱。

2. 從 hello SSH 工作階段，啟動 hello HBase 殼層。
   
    ```bash
    hbase shell
    ```
   
    當載入 hello 殼層時，您會看到`hbase(main):001:0>`提示字元。

3. Hello 資料表中的檢視資料列：
   
    ```hbase
    scan 'SensorData'
    ```
   
    此命令會傳回下列文字，表示 hello 資料表中沒有資料的資訊類似 toohello。
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > 這項掃描作業會傳回最多 10 個資料列 hello 資料表中。

## <a name="delete-your-clusters"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello 叢集、 存放裝置，以及 web 應用程式一次刪除 hello 包含它們的資源群組。

## <a name="next-steps"></a>後續步驟

若需更多搭配 HDInsight 的 Storm 拓撲範例，請參閱 [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)。

如需 Apache Storm 的詳細資訊，請參閱 hello [Apache Storm](https://storm.incubator.apache.org/)站台。

如需 HDInsight HBase 的相關詳細資訊，請參閱 hello[概觀 HDInsight HBase](hdinsight-hbase-overview.md)。

如需 Socket.io 的詳細資訊，請參閱 hello [socket.io](http://socket.io/)站台。

如需關於 D3.js 的詳細資訊，請參閱 [D3.js：資料驅動型文件](http://d3js.org/)(英文)。

如需關於以 Java 建立拓撲的詳細資訊，請參閱 [為 Apache Storm on HDInsight 開發 Java 拓撲](hdinsight-storm-develop-java-topology.md)。

如需關於以 .NET 建立拓撲的詳細資訊，請參閱 [使用 Visual Studio 為 Apache Storm on HDInsight 開發 C# 拓撲](hdinsight-storm-develop-csharp-visual-studio-topology.md)。

[azure-portal]: https://portal.azure.com
