---
title: "aaaInstall 和使用 Giraph 在 Hadoop 叢集 HDInsight 的 Azure 中 |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集 Giraph，以及如何 toouse Giraph。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>在 Windows 型 HDInsight 叢集上安裝和使用 Giraph

了解如何使用指令碼動作 Giraph toocustomize Windows 依據 HDInsight 叢集以及如何 toouse Giraph tooprocess 大規模圖形。 如需搭配以 Linux 為基礎的叢集使用 Giraph 的詳細資訊，請參閱 [在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)。

> [!IMPORTANT]
> hello 中此文件僅搭配 Windows 為基礎的 HDInsight 叢集的步驟。 Windows 上的 HDInsight 只提供低於 HDInsight 3.4 的版本。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。 如需詳細資訊 tooinstall Giraph 於 linux 的 HDInsight 叢集上，請參閱[HDInsight Hadoop 叢集 (Linux) 上的安裝 Giraph](hdinsight-hadoop-giraph-install-linux.md)。


您也可以使用「指令碼動作」 ，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 Giraph。 範例指令碼 tooinstall Giraph 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。 hello 範例指令碼僅適用於 HDInsight 叢集版本 3.1。 如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。

**相關文章**

* [在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)

## <a name="what-is-giraph"></a>什麼是 Giraph？
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a>可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。 圖形物件，例如大型網路 hello 網際網路，類似於各路由器間 hello 連接之間的關聯性模型化，或者 (有時候參照 tooas 社交圖形) 的社交網路上的人員之間的關聯性。 圖表處理可讓您 hello 在圖形中，物件之間的關聯性的相關 tooreason 例如：

* 根據目前的人際關係找出可能的朋友。
* 用來識別網路中的兩部電腦之間的 hello 最短路由。
* 計算 hello 頁面順位的網頁。

## <a name="install-giraph-using-portal"></a>使用入口網站安裝 Giraph
1. 啟動 建立叢集使用 hello**自訂建立**選項，依照[在 HDInsight 中的建立 Hadoop 叢集](hdinsight-provision-clusters.md)。
2. 在 [hello**指令碼動作**頁面 hello 精靈] 中，按一下**加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：

    ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "使用指令碼動作 toocustomize 叢集")

    <table border='1'>
        <tr><th>屬性</th><th>值</th></tr>
        <tr><td>名稱</td>
            <td>指定 hello 指令碼動作的名稱。 例如，<b>安裝 Giraph</b>。</td></tr>
        <tr><td>指令碼 URI</td>
            <td>指定 hello 統一資源識別元 (URI) toohello 指令碼會叫用的 toocustomize hello 叢集。 例如，<i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>節點類型</td>
            <td>指定 hello hello 自訂指令碼執行所在的節點。 您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。
        <tr><td>參數</td>
            <td>指定 hello 參數，如果 hello 指令碼所需。 hello 指令碼 tooinstall Giraph 不需要任何參數，因此您可以讓此處空白。</td></tr>
    </table>

    您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。 加入 hello 指令碼之後，按一下 建立 hello 叢集 hello 核取記號 toostart。

## <a name="use-giraph"></a>使用 Giraph
我們使用 hello SimpleShortestPathsComputation 範例 toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a>尋找 hello 圖形中的物件之間最短的路徑實作。 使用下列步驟 tooupload hello 範例資料和 hello 範例 jar，以便使用 hello SimpleShortestPathsComputation 範例中，然後按一下 檢視 hello 結果執行工作的 hello。

1. 上傳範例資料檔案 tooAzure Blob 儲存體。 在本機工作站上，建立名為 **tiny_graph.txt** 的新檔案。 它應該包含下列行 hello:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    上傳 hello tiny_graph.txt 檔案 toohello 主要儲存體您的 HDInsight 叢集。 如需有關指示 tooupload 資料，請參閱 < [HDInsight 中的 Hadoop 工作的資料上傳](hdinsight-upload-data.md)。

    這項資料會描述一種導向圖形，藉由使用 hello 格式中的物件之間的關聯性 [來源\_識別碼、 來源\_值] [[目的地\_識別碼]，[邊緣\_值]，...]]。每一行代表 **source\_id** 物件和一或多個 **dest\_id** 物件之間的關聯性。 hello**邊緣\_值**（或加權） 可以視為 hello 強度或 hello 連線之間的距離**source_id**和**目的地\_識別碼**.

    繪製出，且使用 hello 值 （或加權），做為 hello 物件之間的距離，hello 上方資料看起來可能像這樣：

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. 執行 hello SimpleShortestPathsComputation 範例。 使用下列 Azure PowerShell cmdlet toorun hello 範例利用 hello tiny_graph.txt 檔案做為輸入 hello。

    > [!IMPORTANT]
    > 使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。 此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。
    >
    > 請依照中的 hello 步驟[安裝和設定 Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello 最新版的 Azure PowerShell。 如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    在上述範例中的 hello，取代**clustername** hello 您已安裝的 Giraph 的 HDInsight 叢集名稱。
3. 檢視 hello 結果。 一旦 hello 工作已完成，hello 結果將會儲存在兩個輸出檔案中 hello **wasb: / 範例/out/shotestpaths**資料夾。 hello 檔案被稱為**一部分-m-00001**和**一部分-m-00002**。 執行下列步驟 toodownload 和檢視 hello 輸出 hello:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    這會建立 hello**範例/輸出/shortestpaths** hello 等您的工作站，下載 hello 兩個輸出檔案 toothat 位置的目前目錄中的目錄結構。

    使用 hello **Cat** hello 檔案的 cmdlet toodisplay hello 內容：

        Cat example/output/shortestpaths/part*

    hello 輸出應該看起來類似 toohello 下列：

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    hello SimpleShortestPathComputation 範例是硬式編碼的 toostart 與物件識別碼為 1，並尋找 hello 最短路徑 tooother 物件。 因此 hello 輸出應該會讀取成`destination_id distance`距離所在 hello 值 （或加權） 旅行 hello 邊緣的物件識別碼為 1 與 hello 目標 id。

    將此視覺化，您可以確認 hello 結果識別碼 1 和所有其他物件之間旅行 hello 最短的路徑。 請注意，hello 識別碼 1 和識別碼 4 之間的最短路徑為 5。 這是 hello 總之間的距離<span style="color:orange">識別碼 1 和 3</span>，然後<span style="color:red">ID 為 3 和 4</span>。

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>使用 Aure PowerShell 安裝 Giraph
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。  hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。

## <a name="install-giraph-using-net-sdk"></a>使用 .NET SDK 安裝 Giraph
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。 hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1)。

## <a name="see-also"></a>另請參閱
* [在 HDInsight Hadoop 叢集上安裝 Giraph (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [在 HDInsight 叢集中建立 Hadoop](hdinsight-provision-clusters.md)：建立 HDInsight 叢集的一般資訊。
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：關於使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)
* [在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：關於安裝 Spark 的指令碼動作範例。
* [在 HDInsight 叢集上安裝 R][hdinsight-install-r]：關於安裝 R 的指令碼動作範例。
* [在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install.md)：關於安裝 Solr 的指令碼動作範例。

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
