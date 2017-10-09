---
title: "Hadoop 叢集的 Azure 上的 aaaUse 指令碼動作 tooinstall Solr |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集 Solr 使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a>在 Windows 型 HDInsight 叢集上安裝和使用 Solr

了解如何使用指令碼動作 Solr toocustomize Windows 為基礎的 HDInsight 叢集以及如何 toouse Solr toosearch 資料。

> [!IMPORTANT]
> hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。 Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需搭配以 Linux 為基礎的叢集使用 Solr 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)](hdinsight-hadoop-solr-install-linux.md)


您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Solr。 範例指令碼 tooinstall Solr 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。

hello 範例指令碼僅適用於 HDInsight 叢集版本 3.1。 如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。

使用本主題中的 hello 範例指令碼會建立 windows Solr 叢集使用特定的組態。 如果您想具有不同的集合、 分區、 結構描述、 複本和等等的 tooconfigure hello Solr 叢集中，您必須修改 hello 指令碼和 Solr 二進位檔。

**相關文章**

* [在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)

## <a name="what-is-solr"></a>什麼是 Solr？
<a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> 是可對資料執行強大全文搜尋作業的企業搜尋平台。 雖然 Hadoop 可讓儲存和管理大量的資料，Apache Solr 提供 hello 搜尋功能 tooquickly 擷取 hello 資料。

## <a name="install-solr-using-portal"></a>使用入口網站安裝 Solr
1. 啟動 建立叢集使用 hello**自訂建立**選項，依照[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-provision-clusters.md)。
2. 在 [hello**指令碼動作**頁面 hello 精靈] 中，按一下**加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：

    ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "使用指令碼動作 toocustomize 叢集")

    <table border='1'>
        <tr><th>屬性</th><th>值</th></tr>
        <tr><td>名稱</td>
            <td>指定 hello 指令碼動作的名稱。 例如，<b>安裝 Solr</b>。</td></tr>
        <tr><td>指令碼 URI</td>
            <td>指定 hello 統一資源識別元 (URI) toohello 指令碼會叫用的 toocustomize hello 叢集。 例如，<i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></td></tr>
        <tr><td>節點類型</td>
            <td>指定 hello hello 自訂指令碼執行所在的節點。 您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。
        <tr><td>參數</td>
            <td>指定 hello 參數，如果 hello 指令碼所需。 hello 指令碼 tooinstall Solr 不需要任何參數，因此您可以讓此處空白。</td></tr>
    </table>

    您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。 加入 hello 指令碼之後，按一下 建立 hello 叢集 hello 核取記號 toostart。

## <a name="use-solr"></a>使用 Solr
您必須從以某些資料檔案編製 Solr 的索引來開始。 然後，您可以使用 Solr toorun 搜尋查詢 hello 編製索引的資料。 執行下列步驟 toouse Solr HDInsight 叢集中的 hello:

1. **使用遠端桌面通訊協定 (RDP) tooremote 成 hello HDInsight 叢集安裝 Solr**。 Hello Azure 入口網站，為您建立與 Solr 安裝，且再到遠端 hello 叢集 hello 叢集啟用遠端桌面。 如需指示，請參閱[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。
2. **上傳資料檔案以對 Solr 編製索引**。 當您建立索引 Solr 時，您放入您可能需要 toosearch 上的文件。 tooindex Solr，使用 RDP tooremote 到 hello 叢集中，瀏覽 toohello 桌面，開啟 hello Hadoop 命令列，並瀏覽過**C:\apps\dist\solr-4.7.2\example\exampledocs**。 執行下列命令的 hello:

        java -jar post.jar solr.xml monitor.xml

    您會看到下列輸出 hello 主控台上的 hello:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    hello post.jar 公用程式索引兩份範例文件，Solr **solr.xml**和**monitor.xml**。 hello post.jar 公用程式和 hello 範例文件會提供與 Solr 安裝。
3. **使用 hello Solr hello 內的儀表板 toosearch 編製索引的文件**。 在 hello RDP 工作階段 toohello HDInsight 叢集化，開啟 Internet Explorer 中，並啟動 hello Solr 儀表板在**http://headnodehost:8983/solr #/**。 從 hello 左窗格中，從 hello**核心選取器**下拉式清單中，選取**collection1**，內，按一下 **查詢**。 範例、 以及 tooselect 傳回 Solr 中的所有 hello 文件會都提供下列值的 hello:

   * 在 hello **q**文字方塊中，輸入 **\*:**\*。 這會傳回所有的 hello 文件會編製索引 Solr 中。 如果您想要 toosearch hello 文件中的特定字串，您可以輸入該字串。
   * 在 hello **wt**文字方塊中，選取 hello 輸出格式。 預設值是 [ **json**]。 按一下 [ **執行查詢**]。

     ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Solr 儀表板上執行查詢")

     hello 輸出傳回 hello 我們用於索引 Solr 的兩個文件。 hello 輸出看起來像下列 hello:

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
4. **建議使用： Hello 備份編製索引資料從 Solr tooAzure hello HDInsight 叢集相關聯的 Blob 儲存體**。 很好的作法是，您應該備份到 Azure Blob 儲存體的 hello Solr 叢集節點 hello 編製索引的資料。 執行下列步驟 toodo 因此 hello:

   1. 從 hello RDP 工作階段中，開啟 Internet Explorer 中，並點 toohello 下列 URL:

           http://localhost:8983/solr/replication?command=backup

       您應該會看到如下所示的回應：

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. 在 hello 遠端工作階段中，瀏覽過 {SOLR_HOME}\{集合} \data 中。 透過 hello 範例指令碼建立 hello 叢集中，這應該是**C:\apps\dist\solr-4.7.2\example\solr\collection1\data**。 在這個位置，您應該會看到快照集資料夾，以建立一個名稱類似太**快照集。*時間戳記** *。
   3. 壓縮 hello 快照集資料夾，並將它上傳 tooAzure Blob 儲存體。 從 hello Hadoop 命令列使用下列命令的 hello 巡覽 toohello hello 快照集資料夾位置：

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       此命令，複製 hello 快照集太/範例/資料/hello 預設儲存體中的 hello 容器下的帳戶與 hello 叢集相關聯。

## <a name="install-solr-using-aure-powershell"></a>使用 Azure PowerShell 安裝 Solr
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。  hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。

## <a name="install-solr-using-net-sdk"></a>使用 .NET SDK 安裝 Solr
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。 hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1)。

## <a name="see-also"></a>另請參閱
* [在 HDInsight Hadoop 叢集上安裝和使用 Solr (Linux)](hdinsight-hadoop-solr-install-linux.md)
* [在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)
* [在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。
* [在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。
* [在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：關於安裝 Giraph 的指令碼動作範例。

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
