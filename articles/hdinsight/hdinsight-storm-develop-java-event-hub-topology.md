---
title: "從事件中樞與使用 Java 的 HDInsight 上的 Storm aaaProcess 事件 |Microsoft 文件"
description: "了解與 Maven tooprocess Java Storm 拓撲與事件中心資料的建立方式。"
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>使用 Storm on HDInsight 處理 Azure 事件中樞的事件 (Java)

深入了解如何 toouse Storm HDInsight 上使用的 Azure 事件中心。 這個範例會使用在 Azure 事件中心 Java 為基礎的元件 tooread 及寫入資料。

Azure 事件中心可讓您 tooprocess 從網站、 應用程式和裝置的資料量很大。 hello spout 事件中心可讓您輕鬆 toouse Apache Storm HDInsight tooanalyze 上此即時資料。 您也可以撰寫從出現的資料 tooEvent 集線器使用事件中心閃電的 hello。

## <a name="prerequisites"></a>必要條件

* Apache Storm on HDInsight 叢集 3.6 版。 如需詳細資訊，請參閱[開始使用 Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md)。

    > [!IMPORTANT]
    > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* [Azure 事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)。

* [Oracle Java Developer Kit (JDK) 第 8 版](http://www.oracle.com/technetwork/java/javase/downloads/index.html)或同等版本，例如 [OpenJDK](http://openjdk.java.net/)。

* [Maven](https://maven.apache.org/download.cgi)：Maven 是 Java 專案的專案建置系統。

* 文字編輯器或整合開發環境 (IDE)。

    > [!NOTE]
    > 您的編輯器或 IDE 可能具有處理 Maven 的特定功能，但未記載在這份文件中。 編輯環境的 hello 功能的相關資訊，請參閱您使用的 hello 產品的 hello 說明文件。

    * SSH 用戶端。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

* hello`ssh`和`scp`命令。 這些是使用的 toocopy 檔案 toohello HDInsight 叢集。 在 Windows 上，您可以透過 Windows 10 的 Bash 執行這些命令。

## <a name="understanding-hello-example"></a>了解 hello 範例

hello [hdinsight java storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)範例包含兩種拓撲：

hello`resources/writer.yaml`拓撲寫入隨機資料 tooan Azure 事件中心。 會產生 hello hello 資料`DeviceSpout`元件，且為隨機的裝置識別碼，裝置的值。 所以它是模擬會發出字串識別碼和數值的部分硬體。

關於`resources/reader.yaml`拓撲讀取自事件中心 （由 EventHubWriter，寫入 hello 資料） 的資料剖析 hello JSON 資料，並再記錄 hello`deviceId`和`deviceValue`資料。

hello 資料會格式化為 JSON 文件它是撰寫 tooEvent 中樞，並由 hello 讀取器讀取時才能進行剖析從 JSON 移至 tuple。 hello JSON 格式如下所示：

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>專案組態

hello`POM.xml`檔案包含這個 Maven 專案的組態資訊。 hello 興趣︰

#### <a name="event-hub-components"></a>事件中樞元件

可讀取和寫入 tooAzure 事件中心 hello 元件位於 hello [HDInsight 儲存機制](https://github.com/hdinsight/mvn-rep)。 下列各節 hello hello`POM.xml`這個儲存機制從檔案載入 hello 元件

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>hello EventHubs Storm Spout 相依性

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

這段 xml 會定義包含 spout 從事件中樞進行讀取和寫入 tooit 閃電 hello eventhubs 封裝的相依性。

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

這段 xml 會設定 hello 專案 toogenerate 輸出 for Java 8 中，會使用 HDInsight 3.5 或更高版本。

#### <a name="hello-maven-shade-plugin"></a>hello maven 陰影外掛程式

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

這段 xml 會設定成超級 jar hello 方案 toopackage hello 輸出。 hello jar 包含 hello 專案程式碼和必要的相依性。 它也用來：

* 重新命名 hello 相依性的授權檔案。
* 排除安全性/簽章。
* 請確定多個實作 hello 相同介面會合併成一個項目。

這些組態設定可防止執行階段錯誤。

#### <a name="topology-definitions"></a>拓撲定義

這個範例會使用 hello[變動](https://storm.apache.org/releases/1.1.0/flux.html)架構。 此架構會使用 YAML toodefine hello 拓撲。 hello 主要優點是您不是硬式編碼在 Java 程式碼中的 hello 拓撲。 由於 hello 定義 YAML，您可以變更它提交 hello 拓撲，而不需要 toorecompile 的所有項目之前。

__writer.yaml__：

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__reader.yaml__：

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>事件中樞的相關分辨 hello 拓樸

在執行階段，hello`dev.properties`檔案是使用的 toopass hello 事件中樞設定 toohello 拓撲。 hello 下列範例是 hello 檔案 hello 預設內容：

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>設定環境變數

hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。 不過，您應該檢查其存在且包含您系統的 hello 正確值。

* **JAVA_HOME** -應該指向 toohello hello Java runtime environment (JRE) 安裝所在的目錄。 例如，在 Unix 或 Linux 的分佈，它應該有一個值類似太`/usr/lib/jvm/java-7-oracle`。 在 Windows 中，就會類似的值太`c:\Program Files (x86)\Java\jre1.7`
* **路徑**-應該包含下列路徑的 hello:

  * **JAVA_HOME** （或 hello 相等路徑）
  * **JAVA_HOME\bin** （或 hello 相等路徑）
  * hello Maven 安裝所在的目錄

## <a name="configure-event-hub"></a>設定事件中樞

事件中心是此範例中的 hello 資料來源。 使用下列步驟 toocreate 事件中心的 hello。

1. 從 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，選取**新增** > **Service Bus** > **事件中心** > **自訂建立**。

2. 在 hello**新增新的事件中樞**畫面上，輸入**事件中樞名稱**。 選取 hello**區域**toocreate hello 中樞中，然後再建立命名空間或選取現有的我的最愛。 最後，按一下 hello**箭號**toocontinue。

    ![精靈頁面 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > 選取 hello 相同**位置**為您 Storm HDInsight 伺服器 tooreduce 延遲和成本。

3. 在 hello**設定事件中樞**畫面上，輸入 hello**分割計數**和**訊息保留**值。 在此範例中，資料分割計數使用 10，訊息保留使用 1。 請注意 hello 資料分割計數，因為您稍後需要這個值。

    ![精靈頁面 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Hello 事件中心已建立，請選取 hello 命名空間之後，請選取**事件中心**，然後選取您稍早建立的 hello 事件中心。
5. 選取**設定**，然後使用下列資訊的 hello 建立兩個新的存取原則：

    <table>
    <tr><th>名稱</th><th>權限</th></tr>
    <tr><td>寫入器</td><td>傳送</td></tr>
    <tr><td>讀取者</td><td>接聽</td></tr>
    </table>

    建立 hello 權限之後，請選取 hello**儲存**在 hello hello 頁面底部的圖示。 這些共用的存取原則使用的 tooread 並寫入 tooEvent 中樞。

    ![原則](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. 儲存 hello 原則之後，使用 hello**共用存取金鑰產生器**底部 hello hello 頁面 tooretrieve hello 金鑰 hello**寫入器**和**讀取器**原則。 儲存這些金鑰。

## <a name="download-and-build-hello-project"></a>下載並建置 hello 專案

1. 從 GitHub 下載 hello 專案： [hdinsight java storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub)。 您可以下載為 zip 封存，hello 封裝，或使用[git](https://git-scm.com/) tooclone hello 專案在本機。

2. 修改 hello`dev.properties`包含事件中心的 hello 組態檔。

3. 使用下列 toobuild 和套件 hello 專案 hello:

        mvn package

    這個命令會下載必要的相依性，建置並封裝然後 hello 專案。 hello 輸出會儲存在 hello **/目標**目錄做為**EventHubExample-1.0-SNAPSHOT.jar**。

## <a name="test-locally"></a>本機測試

因為這些拓撲只讀取和寫入 tooEvent 中樞，您可以測試它們，如果您有[Storm 開發環境](http://storm.apache.org/releases/current/Setting-up-development-environment.html)。 使用下列步驟 toorun hello 開發環境中的本機 hello:

1. 執行 hello 寫入器：

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. 執行 hello 讀取器：

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Hello 拓撲中執行本機模式 （非分散式）。
> * `-R /writer.yaml`： 從 hello 載入 hello 拓撲定義`resources`封裝在 hello jar。 如果 hello 拓撲 hello 本機檔案系統上的檔案，請改為 hello 最後一個參數為指定 hello 路徑 tooit。
> * `--filter dev.properties`： 使用 hello 內容`dev.properties`toofill hello hello 拓撲定義中的值。 例如： `${eventhub.read.policy.name}`。

在本機執行時，輸出會是記錄的 toohello 主控台。 使用__Ctrl + C__ toostop hello 拓撲。

## <a name="deploy-hello-topologies"></a>部署 hello 拓撲

1. 使用 SCP toocopy hello jar 封裝 tooyour HDInsight 叢集。 取代為您的叢集 hello SSH 使用者使用者名稱。 以您的 HDInsight 叢集 hello 名稱取代 CLUSTERNAME:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    如果您使用 SSH 帳戶密碼，則提示的 tooenter hello 密碼。 如果您使用 SSH 金鑰與 hello 帳戶時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 金鑰檔。 例如， `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    此命令會將複製 SSH 使用者 hello 叢集上的 hello 檔案 toohello 主的目錄。

2. Hello 檔案已完成上傳，一旦使用 SSH tooconnect toohello HDInsight 叢集。 取代**USERNAME** hello SSH 登入名稱。 將 **CLUSTERNAME** 取代為 HDInsight 叢集名稱：

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > 如果您使用 SSH 帳戶密碼，則提示的 tooenter hello 密碼。 如果您使用 SSH 金鑰與 hello 帳戶時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 金鑰檔。 hello 下列範例會載入 hello 私密金鑰`~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. 使用下列命令 toostart hello 拓撲 hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`： 送出 hello 拓撲 toohello Nimbus 服務，就會開始在 hello hello 叢集中的背景工作節點上。

4. tooview hello 記錄資料，請移 toohttps://CLUSTERNAME.azurehdinsight.net/stormui，其中__CLUSTERNAME__ hello 您的 HDInsight 叢集名稱。 選取 hello 拓樸，然後向下切入 toohello 元件。 選取 hello__連接埠__元件 tooview 的執行個體的項目會記錄資訊。

5. 使用下列命令 toostop hello 拓撲 hello:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>後續步驟

* [Storm on HDInsight 的範例拓撲](hdinsight-storm-example-topology.md)
