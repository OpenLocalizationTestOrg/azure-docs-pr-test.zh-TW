---
title: "aaaApache Storm 寫入 tooStorage 資料湖存放區-Azure HDInsight |Microsoft 文件"
description: "了解 toouse hdinsight hello Apache Storm toowrite toohello HDFS 相容存放裝置的方式。 Azure 儲存體或 Azure Data Lake Store 的 HDInsight 提供 hello HDFS comptabile 儲存體。 此文件和 hello 相關聯的範例，示範如何 hello HdfsBolt 元件可使用的 toowrite toohello 預設儲存體的 HDInsight 叢集上出現。"
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>撰寫從 Apache Storm 的 tooHDFS HDInsight 上

了解 toouse Storm toowrite 資料 toohello HDFS 相容儲存體使用 Apache Storm HDInsight 上的方式。 HDInsight 可以同時使用 Azure 儲存體以及 Azure Data Lake Store 作為 HDFS 相容儲存體。 提供 storm [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html)寫入資料 tooHDFS 的元件。 本文件提供從 hello HdfsBolt 撰寫 tooeither 類型的儲存體的資訊。 

> [!IMPORTANT]
> 本文件中使用的拓樸 hello 範例依賴隨附於 Storm HDInsight 上的元件。 它可能需要修改 toowork 與 Azure 資料湖存放區時使用與其他 Apache Storm 叢集。

## <a name="get-hello-code"></a>取得 hello 程式碼

包含此拓撲中的 hello 專案是從下載[https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store)。

toocompile 此專案中，您需要下列組態的開發環境的 hello:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 或更新版本。 HDInsight 3.5 或更新版本需要 Java 8。

* [Maven 3.x](https://maven.apache.org/download.cgi)

hello 下列環境變數設定當您在開發工作站上安裝 Java 和 hello JDK。 不過，您應該檢查其存在且包含您系統的 hello 正確值。

* `JAVA_HOME`-應該指向 toohello hello JDK 安裝的目錄。
* `PATH`-應包含下列路徑的 hello:
  
    * `JAVA_HOME`（或 hello 等路徑）。
    * `JAVA_HOME\bin`（或 hello 等路徑）。
    * hello Maven 安裝所在的目錄。

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>如何 toouse hello 與 HDInsight HdfsBolt

> [!IMPORTANT]
> 在使用之前 hello HdfsBolt Storm HDInsight 上使用，您必須先使用指令碼動作所需的 toocopy jar 檔案到 hello `extpath` Storm 的。 如需詳細資訊，請參閱 hello[設定 hello 叢集](#configure)> 一節。

hello HdfsBolt 使用 hello 檔案配置如何提供 toounderstand toowrite tooHDFS。 與 HDInsight，使用其中一種 hello 下列配置：

* `wasb://`：搭配使用 Azure 儲存體帳戶。
* `adl://`：搭配使用 Azure Data Lake Store。

hello 下表提供不同的情況下使用 hello 檔案配置的範例：

| 配置 | 注意事項 |
| ----- | ----- |
| `wasb:///` | hello 預設儲存體帳戶是 Azure 儲存體帳戶中的 blob 容器 |
| `adl:///` | hello 預設儲存體帳戶是 Azure 資料湖存放區中的目錄。 叢集建立期間，您可以指定 hello 目錄是 hello 叢集的 HDFS hello 根的資料湖存放區中。 例如，hello`/clusters/myclustername/`目錄。 |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Hello 叢集相關聯的非預設 （其他） 的 Azure 儲存體帳戶。 |
| `adl://STORENAME/` | hello 的 hello hello 叢集所使用的資料湖存放區的根目錄。 這種配置允許 tooaccess 資料位於包含 hello 叢集檔案系統的 hello 目錄外。 |

如需詳細資訊，請參閱 hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) Apache.org 上的參考。

### <a name="example-configuration"></a>設定範例

hello 下列 YAML 是摘錄自 hello `resources/writetohdfs.yaml` hello 範例中包含的檔案。 此檔案會定義使用 hello hello Storm 拓撲[變動](https://storm.apache.org/releases/1.1.0/flux.html)Apache Storm 的架構。

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

此 YAML 會定義下列項目 hello:

* `syncPolicy`： 定義檔案時同步/排清 toohello 檔案系統。 在此範例中，為每 1000 個 Tuple。
* `fileNameFormat`： 定義 hello 路徑和檔案名稱模式 toouse 時寫入檔案。 在此範例中，在執行階段使用篩選器，提供 hello 路徑和 hello 副檔名是`.txt`。
* `recordFormat`： 定義 hello hello 寫入的檔案的內部格式。 此範例中，欄位會分隔 hello`|`字元。
* `rotationPolicy`： 定義當 toorotate 檔案。 在此範例中，不會執行輪替。
* `hdfs-bolt`： 使用 hello 做為 hello 的組態參數的舊版元件`HdfsBolt`類別。

如需有關 hello 變動架構的詳細資訊，請參閱[https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html)。

## <a name="configure-hello-cluster"></a>Hello 叢集設定

根據預設，在 HDInsight 上的 Storm 不包含 hello 元件，HdfsBolt 使用 toocommunicate 搭配 Azure 儲存體或資料湖存放區中出現的 classpath。 使用 hello 下列指令碼動作 tooadd 這些元件 toohello `extlib` Storm 的叢集上目錄：

|指令碼 URI |節點 tooapply 它 |參數 | |`https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` |Nimbus、 監督員 |None |

如需使用此指令碼與您的叢集資訊，請參閱 hello[使用指令碼動作的自訂 HDInsight 叢集](./hdinsight-hadoop-customize-cluster-linux.md)文件。

## <a name="build-and-package-hello-topology"></a>建置並封裝 hello 拓樸

1. 下載 hello 範例專案，從[https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour 開發環境。

2. 從命令提示字元中，終端機或殼層工作階段中，變更目錄 toohello 根的 hello 已經下載專案。 toobuild 和套件 hello 拓撲，請使用下列命令的 hello:
   
        mvn compile package
   
    Hello 建置和封裝完成之後，沒有名為的新目錄`target`，其中包含名為`StormToHdfs-1.0-SNAPSHOT.jar`。 此檔案包含編譯 hello 拓撲。

## <a name="deploy-and-run-hello-topology"></a>部署和執行 hello 拓樸

1. 使用下列命令 toocopy hello 拓撲 toohello HDInsight 叢集的 hello。 取代**使用者**hello SSH 使用者名稱與您在建立時使用 hello 叢集。 取代**CLUSTERNAME** hello hello 叢集名稱。
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    出現提示時，輸入 hello 建立 hello SSH 使用者 hello 叢集時所使用的密碼。 如果您使用公開金鑰而不使用密碼時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 相符的私密金鑰。
   
   > [!NOTE]
   > 如需搭配 HDInsight 使用 `scp` 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](./hdinsight-hadoop-linux-use-ssh-unix.md)。

2. Hello 上傳完成之後，請使用下列 tooconnect toohello HDInsight 叢集使用 SSH hello。 取代**使用者**hello SSH 使用者名稱與您在建立時使用 hello 叢集。 取代**CLUSTERNAME** hello hello 叢集名稱。
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    出現提示時，輸入 hello 建立 hello SSH 使用者 hello 叢集時所使用的密碼。 如果您使用公開金鑰而不使用密碼時，您可能需要 toouse hello`-i`參數 toospecify hello 路徑 toohello 相符的私密金鑰。
   
   如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

3. 一旦連接之後，使用 hello 下列命令 toocreate 名為`dev.properties`:

        nano dev.properties

4. 使用 hello 文字之後做為 hello 內容的 hello`dev.properties`檔案：

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > 這個範例假設您的叢集使用的 Azure 儲存體帳戶，做為 hello 預設儲存體。 如果叢集使用 Azure Data Lake Store，請改為使用 `hdfs.url: adl:///`。
    
    toosave hello 檔案，使用__Ctrl + X__，然後__Y__，最後再__Enter__。 此檔案中的 hello 值設定 hello 資料湖存放區 URL 和 hello 資料寫入的目錄名稱。

3. 使用下列命令 toostart hello 拓撲 hello:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    此命令啟動 hello 拓撲使用 hello 變動 framework 提交它 toohello Nimbus hello 叢集節點。 hello 拓撲由 hello`writetohdfs.yaml`納入 hello jar 檔案。 hello`dev.properties`檔案會傳遞做為篩選條件，並且 hello 檔案中所包含的 hello 值被讀取的 hello 拓撲。

## <a name="view-output-data"></a>檢視輸出資料

tooview hello 資料，請使用下列命令的 hello:

    hdfs dfs -ls /stormdata/

此拓撲中所建立的 hello 檔案的清單隨即出現。

hello 下列清單是 hello hello 先前命令所傳回的資料的範例：

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>停止 hello 拓樸

Storm 拓撲執行之前停止，或刪除 hello 叢集。 toostop hello 拓撲，請使用下列命令的 hello:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>刪除叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>後續步驟

既然您已經學會如何 toouse Storm toowrite tooAzure 儲存體和 Azure 資料湖存放區，找出其他[Storm 範例 hdinsight](hdinsight-storm-example-topology.md)。

