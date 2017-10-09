---
title: "aaaGet 開始使用 HDInsight 的 Azure 上 HBase 範例 |Microsoft 文件"
description: "請遵循此 Apache HBase 範例 toostart HDInsight 上使用 hadoop。 從 hello HBase 殼層建立資料表，並加以查詢，使用登錄區。"
keywords: "hbasecommand,hbase 範例"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>開始使用 HDInsight 中的 Apache HBase 範例

了解如何建立 HBase 資料表 toocreate 在 HDInsight HBase 叢集，以及使用 Hive 查詢的資料表。 如需一般 HBase 資訊，請參閱 [HDInsight HBase 概觀][hdinsight-hbase-overview]。

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>必要條件
開始嘗試這個 HBase 範例之前，您必須具備下列項目 hello:

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* [安全殼層 (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md)。 
* [cURL](http://curl.haxx.se/download.html)。

## <a name="create-hbase-cluster"></a>建立 HBase 叢集
hello 下列程序會使用 Azure Resource Manager 範本 toocreate 版本 3.4 linux HBase 叢集和 hello 相依的預設 Azure 儲存體帳戶。 toounderstand hello 參數用於 hello 程序和其他叢集建立方法，請參閱[HDInsight 叢集建立 Linux Hadoop](hdinsight-hadoop-provision-linux-clusters.md)。

1. 按一下下列映像 tooopen hello 範本 hello Azure 入口網站中的 hello。 hello 範本位於 公用 blob 容器中。 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. 從 hello**自訂部署**刀鋒視窗中，輸入下列值的 hello:
   
   * **訂用帳戶**： 選取您是使用的 toocreate hello 叢集的 Azure 訂閱。
   * **資源群組**：建立 Azure 資源管理群組，或選取現有的資源管理群組。
   * **位置**： 指定 hello hello 資源群組的位置。 
   * **ClusterName**： 輸入 hello HBase 叢集的名稱。
   * **叢集登入名稱和密碼**: hello 預設登入名稱是**admin**。
   * **SSH 使用者名稱和密碼**: hello 預設使用者名稱是**sshuser**。  您可以將它重新命名。
     
     其他參數都是選擇性的。  
     
     每個叢集都具備 Azure 儲存體帳戶相依性。 刪除叢集之後，hello 資料會保留 hello 儲存體帳戶中。 hello 叢集預設儲存體帳戶名稱是與 「 市集 」 附加 hello 叢集名稱。 它是硬式編碼 hello 範本變數區段中。
3. 選取**toohello 條款和條件前面所述，即表示我同意**，然後按一下**購買**。 它會採用約 20 分鐘 toocreate 叢集。

> [!NOTE]
> 刪除 HBase 叢集之後，您可以使用 hello 來建立另一個 HBase 叢集相同的預設 blob 容器。 hello 新叢集挑選您建立 hello 原始叢集中的 hello HBase 資料表。 tooavoid 不一致，我們建議您刪除 hello 叢集之前，停用 hello HBase 資料表。
> 
> 

## <a name="create-tables-and-insert-data"></a>建立資料表和插入資料
您可以使用 SSH tooconnect tooHBase 叢集，然後使用 HBase 殼層 toocreate HBase 資料表插入資料及查詢資料。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

對大多數人來說，資料會出現在 hello 表格式格式：

![HDInsight HBase 表格式資料][img-hbase-sample-data-tabular]

HBase （BigTable 的實作），在 hello 相同的資料如下所示：

![HDInsight HBase BigTable 資料][img-hbase-sample-data-bigtable]


**toouse hello HBase 殼層**

1. Ssh，執行下列命令 HBase hello:
   
    ```bash
    hbase shell
    ```

2. 使用兩個資料行系列建立 HBase：

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. 插入一些資料：
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![HDInsight Hadoop HBase 殼層][img-hbase-shell]
4. 取得單一資料列
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    您應該看到的 hello 相同的結果做為使用 hello 掃描命令，因為只有一個資料列。
   
    如需 hello HBase 資料表的結構描述的詳細資訊，請參閱[簡介 tooHBase 結構描述設計][hbase-schema]。 如需其他 HBase 命令，請參閱 [Apache HBase 參考指南][hbase-quick-start]。
5. 結束 hello 殼層
   
    ```hbaseshell
    exit
    ```

**toobulk hello 連絡人 HBase 資料表將資料載入**

HBase 包含數個將資料載入資料表的方法。  如需詳細資訊，請參閱 [大量載入](http://hbase.apache.org/book.html#arch.bulk.load)。

您可以在公用 Blob 容器中找到資料檔案範例 (*wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*)。  hello hello 資料檔案內容為：

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

您可以選擇性地建立文字檔，並上傳 hello 檔案 tooyour 自己的儲存體帳戶。 Hello 指示，請參閱[HDInsight 中的 Hadoop 工作的資料上傳][hdinsight-upload-data]。

> [!NOTE]
> 此程序會使用您已建立 hello 最後一個程序中的 hello 連絡人 HBase 資料表。
> 

1. Ssh，執行下列命令 tootransform hello 資料檔案 tooStoreFiles，並儲存在 Dimporttsv.bulk.output 所指定的相對路徑的 hello。  如果您是在 HBase 殼層中，使用 hello 結束命令 tooexit。

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. 執行 hello /example/data/storeDataFileOutput toohello HBase 資料表中的下列命令 tooupload hello 資料：
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. 您可以開啟 hello HBase 殼層，並使用 hello 掃描命令 toolist hello 資料表內容。

## <a name="use-hive-tooquery-hbase"></a>使用 Hive tooquery HBase

您可以使用 Hive 查詢 HBase 資料表中的資料。 在本節中，您建立的 Hive 資料表的對應 toohello HBase 資料表，並使用它 tooquery hello 資料 HBase 資料表中。

1. 開啟**PuTTY**，並連接 toohello 叢集。  請參閱 hello hello 前程序中的指示。
2. 從 hello SSH 工作階段，使用下列命令 toostart Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    如需有關 Beeline 的詳細資訊，請參閱[利用 Beeline 搭配使用 Hive 與 HDInsight 中的 Hadoop](hdinsight-hadoop-use-hive-beeline.md)。
       
3. 執行下列 HiveQL 指令碼 toocreate hello 對應 toohello HBase 資料表的 Hive 資料表。 請確定您已建立使用 hello HBase 殼層，然後再執行此陳述式參考稍早在本教學課程中的 hello 範例資料表。

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. 執行下列 HiveQL 指令碼 tooquery hello 資料 hello HBase 資料表中的 hello:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>使用 Curl 來使用 HBase REST API

hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。 您永遠都應該使用安全 HTTP (HTTPS) toohelp 確保您的認證會安全地傳送 toohello 伺服器提出要求。

2. 使用下列命令 toolist hello 現有 HBase 資料表的 hello:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. 使用下列命令 toocreate 具有兩個資料行家族的新 HBase 資料表的 hello:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    hello 結構描述提供 hello JSon 格式。
4. 使用下列命令 tooinsert hello 某些資料：

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    您必須 base64 編碼 hello hello-d 參數中指定的值。 在 hello 範例：
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [false-資料列索引鍵](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single)可讓您 tooinsert （批次） 的多個值。
5. 使用下列命令 tooget 一個資料列的 hello:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

如需 HBase Rest 的詳細資訊，請參閱 [Apache HBase 參考指南](https://hbase.apache.org/book.html#_rest)。

> [!NOTE]
> Thrift 不受 HDInsight 中的 HBase 所支援。
>
> 當使用 WebHCat Curl 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。 您也必須使用 hello 統一資源識別元 (URI) 的一部分使用 toosend hello 要求 toohello 伺服器 hello 叢集名稱：
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    您應該會收到回應類似 toohello 下列回應：
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>檢查叢集狀態
HDInsight 中的 HBase 隨附於 Web UI，以供監視叢集。 使用 hello Web UI，您可以要求統計資料或區域的相關資訊。

**tooaccess hello HBase 主要 UI**

1. 登入 hello https:// 在 hello Ambari Web UI&lt;Clustername >。.azurehdinsight.net。
2. 按一下**HBase** hello 左側功能表中。
3. 按一下**快速連結**在 hello active 動物園管理員節點連結點 toohello，hello 頁面頂端，然後按一下 **HBase 主要 UI**。  在另一個瀏覽器索引標籤中開啟 hello UI:

  ![HDInsight HBase HMaster UI](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  hello HBase 主要 UI 包含下列各節的 hello:

  - 區域伺服器
  - 備份主機
  - tables
  - 工作
  - 軟體屬性

## <a name="delete-hello-cluster"></a>刪除 hello 叢集
tooavoid 不一致，我們建議您刪除 hello 叢集之前，停用 hello HBase 資料表。

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟
在本文中，您學會如何 toocreate HBase 叢集和 toocreate 資料表和檢視 hello 從這些資料表中的資料 hello HBase 殼層。 您也學到如何 toouse Hive HBase 資料表和如何 toouse hello toocreate HBase REST Api C# 中的資料 HBase 資料表的查詢，並從 hello 資料表擷取資料。

toolearn 詳細資訊，請參閱：

* [HDInsight HBase 概觀][hdinsight-hbase-overview]：HBase 是建置於 Hadoop 上的 Apache 開放原始碼 NoSQL 資料庫，可針對大量非結構化及半結構化資料，提供隨機存取功能和強大一致性。

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
