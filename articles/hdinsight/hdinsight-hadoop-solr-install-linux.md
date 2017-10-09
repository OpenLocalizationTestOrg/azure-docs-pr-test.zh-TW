---
title: "aaaUse 指令碼動作 tooinstall 以 Linux 為基礎的 HDInsight 的 Azure 上 Solr |Microsoft 文件"
description: "了解如何 tooinstall Solr 上以 Linux 為基礎的 HDInsight Hadoop 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>在 HDInsight Hadoop 叢集上安裝和使用 Solr

深入了解如何使用指令碼動作 tooinstall Solr Azure HDInsight 上。 Solr 是強大的搜尋平台，可對 Hadoop 管理的資料執行企業級搜尋功能。

> [!IMPORTANT]
    > 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

> [!IMPORTANT]
> 這份文件中使用的 hello 範例指令碼會使用特定的組態安裝 Solr 4.9。 如果您想具有不同的集合、 分區、 結構描述、 複本和等等的 tooconfigure hello Solr 叢集中，您必須修改 hello 指令碼和 Solr 二進位檔。

## <a name="whatis"></a>什麼是 Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) 是可對資料執行強大全文搜尋作業的企業搜尋平台。 雖然 Hadoop 可讓儲存和管理大量的資料，Apache Solr 提供 hello 搜尋功能 tooquickly 擷取 hello 資料。

> [!WARNING]
> Microsoft 完全支援元件時附上 hello HDInsight 叢集。
>
> 自訂元件，例如 Solr，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 Microsoft 支援服務可能不是自訂元件無法 tooresolve 發生問題。 您可能需要 tooengage hello 開放原始碼社群尋求協助。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。

## <a name="what-hello-script-does"></a>哪些 hello 指令碼會執行

此指令碼會進行下列變更 toohello HDInsight 叢集的 hello:

* 將 Solr 4.9 安裝至 `/usr/hdp/current/solr`
* 建立使用者**solrusr**，也就是使用的 toorun hello Solr 服務
* 設定**solruser**做為 hello 擁有者`/usr/hdp/current/solr`
* 加入會自動啟動 Solr 的 [Upstart](http://upstart.ubuntu.com/) 組態。

## <a name="install"></a>使用指令碼動作安裝 Solr

範例指令碼 tooinstall Solr 在 HDInsight 叢集上的將會位於下列位置的 hello:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate 具有 Solr 安裝的叢集，hello 步驟使用 hello[建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)文件。 在 hello 建立過程中，使用下列步驟 tooinstall Solr hello:

1. 從 hello__叢集摘要__刀鋒視窗，select__Advanced settings__，然後__編寫指令碼動作__。 使用下列資訊 toopopulate hello 表單 hello:

   * **名稱**： 輸入 hello 指令碼動作的易記名稱。
   * **SCRIPT URI**：https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**：勾選此選項
   * **WORKER**：勾選此選項
   * **動物園管理員**： 檢查 hello 動物園管理員節點上的這個選項 tooinstall
   * **參數**：將此欄位保留空白

2. 在 hello 底部 hello**編寫指令碼動作**刀鋒視窗中，使用 hello**選取**按鈕 toosave hello 組態。 最後，使用 hello**下一步**按鈕 tooreturn toohello__叢集摘要__

3. 從 hello__叢集摘要__頁面上，選取__建立__toocreate hello 叢集。

## <a name="usesolr"></a>如何在 HDInsight 中使用 Solr

> [!IMPORTANT]
> 本節中的 hello 步驟示範基本的 Solr 功能。 如需有關使用 Solr 的詳細資訊，請參閱 hello [Apache Solr 網站](http://lucene.apache.org/solr/)。

### <a name="index-data"></a>索引資料

使用下列步驟 tooadd 範例資料 tooSolr hello，然後進行查詢：

1. 連線使用 SSH toohello HDInsight 叢集：

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

     > [!IMPORTANT]
     > 在本文件稍後的步驟會使用 SSL 通道 tooconnect toohello Solr web UI。 toouse 這些步驟，您必須建立 SSL 通道，然後再設定您的瀏覽器 toouse 它。
     >
     > 如需詳細資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。

2. 使用下列命令 toohave Solr 索引範例資料的 hello:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    hello 會傳回下列輸出 toohello 主控台：

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    hello`post.jar`公用程式將 hello **solr.xml**和**monitor.xml**文件 toohello 索引。
  
3. 使用下列命令 tooquery hello Solr REST API 的 hello:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    此命令會搜尋**collection1**針對比對任何文件 **\*:\***  (編碼為\*%3a\* hello 查詢字串中)。 下列 JSON 文件的 hello 是 hello 回應的範例：

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>使用 hello Solr 儀表板

hello Solr 儀表板是 web UI，讓您透過網頁瀏覽器與 Solr toowork。 hello Solr 儀表板不會直接在從您的 HDInsight 叢集的 hello 網際網路上公開。 您可以使用 SSH 通道 tooaccess 它。 如需有關如何使用 SSH 通道的詳細資訊，請參閱 hello[使用 SSH 通道，與 HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)文件。

一旦您已建立的 SSH 通道，請使用下列步驟 toouse hello Solr 儀表板的 hello:

1. 判斷 hello hello 主要叢集前端節點的主機名稱：

   1. 使用 SSH tooconnect toohello 叢集前端節點。 例如： `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`。

       如需有關如何使用 SSH 的詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)。

   2. 使用下列命令 tooget hello 完整主機名稱的 hello:

        ```bash
        hostname -f
        ```

        此命令會傳回下列主機名稱值類似 toohello:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        儲存 hello 值傳回，稍後使用。

2. 在瀏覽器中，連接太**http://HOSTNAME:8983/solr #/**，其中**HOSTNAME**是您決定在 hello 先前步驟中的 hello 名稱。

    hello 要求路由傳送 hello SSH 通道 toohello Solr web UI 上您的叢集。 hello 頁面會顯示下列影像類似 toohello:

    ![Solr 儀表板的映像](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. 從 hello 左窗格中，使用 hello**核心選取器**下拉式 tooselect **collection1**。 數個項目應該會出現在 **collection1** 底下。

4. 從下列項目 hello **collection1**，選取**查詢**。 使用下列值 toopopulate hello 搜尋頁面的 hello:

   * 在 hello **q**文字方塊中，輸入 **\*:**\*。 此查詢會傳回 Solr 中所有的 hello 文件會編製索引。 如果您想要 toosearch hello 文件中的特定字串，您可以輸入該字串。
   * 在 hello **wt**文字方塊中，選取 hello 輸出格式。 預設值是 [ **json**]。

     最後，選取 hello**執行查詢**在 hello hello 搜尋 pate 底部的按鈕。

     ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     hello 輸出傳回的 hello 兩份文件，就像加入 toohello 先前索引。 hello 輸出類似 toohello 之後，JSON 文件：

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>啟動和停止 Solr

使用下列命令 toomanually 停止和啟動 Solr hello:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>備份已編製索引的資料

使用下列步驟 tooback Solr toohello 預設儲存體叢集 hello:

1. Toohello 叢集使用 SSH 連線，然後使用下列命令 tooget hello hello 前端節點的主機名稱的 hello:

    ```bash
    hostname -f
    ```

2. 使用下列命令 toocreate hello 編製索引資料的快照集的 hello。 取代**HOSTNAME** hello hello 前一個命令所傳回的名稱：

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    hello 回應是類似 toohello 下列 XML:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. 將目錄變更太`/usr/hdp/current/solr/example/solr`。 在這裡每個集合有一個子目錄。 每個集合目錄包含`data`包含 hello hello 集合快照集目錄。

4. toocreate 經過壓縮的封存的 hello 快照集資料夾，使用 hello 下列命令：

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    取代 hello `snapshot.20150806185338855` hello 的集合名稱的 hello 快照集的值。

    此命令會建立名為封存**snapshot.20150806185338855.tgz**，其中包含 hello hello 內容**snapshot.20150806185338855**目錄。

5. 然後，您可以儲存 hello 封存 toohello 叢集的主要儲存體使用 hello 下列命令：

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

如需有關使用 Solr 備份和還原的詳細資訊，請參閱 [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups)。

## <a name="next-steps"></a>後續步驟

* [在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。 使用叢集自訂 tooinstall Giraph 上 HDInsight Hadoop 叢集。 Giraph 可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。

* [在 HDInsight 叢集上安裝 Hue](hdinsight-hadoop-hue-linux.md)。 使用 HDInsight Hadoop 叢集上的叢集自訂 tooinstall 色調。 色調是一組 Web 應用程式使用 toointeract 與 Hadoop 叢集。

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
