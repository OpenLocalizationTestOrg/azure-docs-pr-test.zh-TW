---
title: "從 HDFS 相容 aaaQuery 資料 Azure 儲存體的 Azure HDInsight |Microsoft 文件"
description: "了解如何從 Azure 儲存體和 Azure Data Lake Store toostore tooquery 資料產生您的分析。"
keywords: "blob 儲存體,hdfs,結構化資料,非結構化資料,data lake store,Hadoop 輸入,Hadoop 輸出, hadoop 儲存體, hdfs 輸入,hdfs 輸出,hdfs 儲存體,wasb azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>搭配 Azure HDInsight 叢集使用 Azure 儲存體

tooanalyze HDInsight 叢集中的資料，您可以儲存在 Azure 儲存體、 Azure 資料湖存放區，或兩者的 hello 資料。 這兩個儲存體選項可讓您 toosafely 刪除 HDInsight 叢集所使用的計算，而不會遺失使用者資料。

Hadoop 支援 hello 預設檔案系統的概念。 hello 預設的檔案系統表示預設配置和授權單位。 它也可以使用的 tooresolve 相對路徑。 在 hello HDInsight 叢集建立程序，您可以指定 blob 容器，在 Azure 儲存體為 hello 預設檔案系統，或使用 HDInsight 3.5，您可以選取 Azure 儲存體或 Azure Data Lake Store hello 預設檔案系統，有一些例外狀況。 做為預設 hello 和連結的儲存體使用 Data Lake Store 的 hello 提供支援，請參閱[HDInsight 叢集 Availabilities](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters)。

在本文中，您將了解 Azure 儲存體與 HDInsight 叢集搭配運作的方式。 toolearn Data Lake Store 的 HDInsight 叢集的運作方式查看[使用 Azure 資料湖存放區與 Azure HDInsight 叢集](hdinsight-hadoop-use-data-lake-store.md)。 如需建立 HDInsight 叢集的詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

Azure 儲存體是強大的一般用途儲存體解決方案，其完美整合了 HDInsight。 HDInsight 可用於 blob 容器的 Azure 儲存體中為 hello 預設檔案系統 hello 叢集。 透過 Hadoop 分散式的檔案系統 (HDFS) 介面，直接可以處理結構化或非結構化資料儲存為 blob hello 整組 HDInsight 中的元件。

> [!WARNING]
> 建立 Azure 儲存體帳戶時，有數個選項可供使用。 hello 下表提供與 HDInsight 支援哪些選項的相關資訊：
> 
> | 儲存體帳戶類型 | 儲存層 | 支援 HDInsight |
> | ------- | ------- | ------- |
> | 一般用途的儲存體帳戶 | 標準 | __是__ |
> | &nbsp; | 進階 | 否 |
> | Blob 儲存體帳戶 | 經常性存取 | 否 |
> | &nbsp; | 非經常性存取 | 否 |

我們不建議您儲存商務資料使用 hello 預設 blob 容器。 在每個使用 tooreduce 之後，刪除 hello 預設 blob 容器儲存體成本是很好的作法。 請注意該 hello 預設容器包含應用程式與系統記錄檔。 刪除 hello 容器前請確定 tooretrieve hello 記錄檔。

不支援多個叢集共用一個 Blob 容器。

## <a name="hdinsight-storage-architecture"></a>HDInsight 儲存架構
下列圖表中的 hello 提供 hello HDInsight 的使用 Azure 儲存體的儲存體架構的抽象檢視：

![Hadoop 叢集使用 hello HDFS API tooaccess，並將結構化及未結構化資料儲存在 Blob 儲存體。] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight 儲存體架構")

HDInsight 提供在本機存取 toohello 分散式檔案系統附加 toohello 計算節點。 可以使用來存取此檔案系統 hello 完整格式 URI，例如：

    hdfs://<namenodehost>/<path>

此外，HDInsight 可讓您 tooaccess 資料儲存在 Azure 儲存體中。 hello 語法為：

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

以下是搭配 HDInsight 叢集使用 Azure 儲存體帳戶時的一些考量。

* **Hello 連接的 tooa 叢集的儲存體帳戶中的容器：**因為 hello 帳戶名稱和金鑰相關聯 hello 叢集建立期間，您會有這些容器中的完整存取 toohello blob。

* **公用容器或公用 blob 儲存體帳戶不在連線 tooa 叢集：**您有唯讀權限 toohello blob hello 容器中的。
  
  > [!NOTE]
  > 公用容器可讓您 tooget 可用該容器中，並取得容器中繼資料的所有 blob 的清單。 公用 blob 可讓您 tooaccess hello blob 才知道 hello 正確的 URL。 如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">限制存取 toocontainers 和 blob</a>。
  > 
  > 
* **無法儲存體帳戶中的私用容器連接 tooa 叢集：**您無法存取 hello 容器中的 hello blob，除非您定義 hello 儲存體帳戶，當您送出 hello WebHCat 作業。 稍後在本文中會加以說明。

hello hello 建立程序和它們的索引鍵中所定義的儲存體帳戶會儲存在 %HADOOP_HOME%/conf/core-site.xml hello 叢集節點上。 HDInsight hello 預設行為是 toouse hello core-site.xml 檔案中定義的 hello 儲存體帳戶。 您可以使用 [Ambari](./hdinsight-hadoop-manage-ambari.md) 來修改此設定

多個 WebHCat 工作 (包括 Hive、MapReduce、Hadoop 資料流和 Pig) 可隨身夾帶儲存體帳戶的說明和中繼資料。 (目前適用於含儲存體帳戶的 Pig，但不適用於中繼資料)。如需詳細資訊，請參閱 [在其他儲存體帳戶和 Metastores 上使用 HDInsight 叢集](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx)。

Blob 可使用於結構化和非結構化資料。 Blob 容器以機碼/值組來儲存資料，沒有目錄階層。 不過，可用於 hello 斜線字元 （/） hello 起來當做檔案儲存在目錄結構內的索引鍵名稱 toomake。 例如，Blob 的機碼可能是 *input/log1.txt*。 實際*輸入*目錄存在，但 toohello hello 索引鍵名稱中的 hello 斜線字元顯示，因為它有 hello 外觀的檔案路徑。

## <a id="benefits"></a>Azure 儲存體的優點
hello 隱含不共計算叢集和儲存體資源的效能成本，只要 hello hello 計算叢集建立 hello Azure 區域，其中 hello 高速網路可讓內關閉 toohello 儲存體帳戶資源的方式hello 運算節點時很有效率 tooaccess hello Azure 儲存體內的資料。

有數個優點，而不是 HDFS 的 Azure 儲存體中儲存 hello 資料相關聯：

* **資料重複使用及共用：** HDFS 中的 hello 資料則位於 hello 運算叢集。 只有 hello 應用程式具有存取 toohello 運算叢集可以使用 HDFS Api 使用 hello 資料。 可以存取 Azure 儲存體中的 hello 資料，透過 hello HDFS 應用程式開發介面或是透過 hello [Blob Storage REST Api][blob-storage-restAPI]。 因此，應用程式 （包括其他 HDInsight 叢集） 和工具的較大的集可以是使用的 tooproduce 及取用 hello 資料。
* **資料封存：**將資料儲存在 Azure 儲存體可讓用來安全地刪除而不會遺失使用者資料的計算 toobe hello HDInsight 叢集。
* **資料儲存體成本：** DFS 中儲存資料，如 hello 長期會比將 hello 資料儲存在 Azure 儲存體，因為運算叢集的 hello 成本高於 Azure 儲存體 hello 成本。 此外，因為 hello 資料並沒有重新載入，每個計算叢集產生 toobe，您也會儲存資料載入成本。
* **彈性向外延展：**雖然 HDFS 提供向外延展檔案系統、 hello 小數位數取決於您所建立的叢集節點的 hello 數目。 變更 hello 標尺可能會變得更複雜的程序比依賴 hello 彈性調整自動取得 Azure 儲存體中的功能。
* **異地複寫：**Azure 儲存體可以進行異地複寫。 雖然這可讓您地理修復與資料冗餘，容錯移轉 toohello 進行地理複寫的位置會嚴重影響效能，而且它可能會產生額外費用。 讓我們的建議是好好 toochoose hello 地理複寫，只有當 hello 資料值的 hello 值得 hello 額外成本。

某些 MapReduce 作業和封裝可能會建立不真的想 toostore Azure 儲存體中的中繼結果。 情況下，您可以選擇在 toostore hello 資料 hello 本機 HDFS。 事實上，在 Hive 工作和其他程序中，HDInsight 會使用 DFS 來儲存許多這些中繼結果。

> [!NOTE]
> 大部分 HDFS 命令 (例如，<b>ls</b>、<b>copyFromLocal</b> 和 <b>mkdir</b>) 仍可正常運作。 只有 hello 命令特定 toohello 原生 HDFS 實作 （此為參考的 tooas DFS），例如<b>fschk</b>和<b>dfsadmin</b>，在 Azure 儲存體中顯示不同的行為。
> 
> 

## <a name="create-blob-containers"></a>建立 Blob 容器
toouse blob，您先建立[Azure 儲存體帳戶][azure-storage-create]。 這個過程，您可以指定 hello 儲存體帳戶建立所在的 Azure 區域。 hello 叢集和 hello 儲存體帳戶必須裝載在 hello 相同的區域。 hello Hive 中繼存放區的 SQL Server 資料庫和 Oozie 中繼存放區的 SQL Server 資料庫必須也位於 hello 相同的區域。

它存在的話，每當您建立每個 blob 所屬 tooa Azure 儲存體帳戶中的容器。 此容器可能是在 HDInsight 外建立的現有 Blob，也可能是為 HDInsight 叢集建立的容器。

hello 預設 Blob 容器儲存叢集特定資訊，例如作業歷程記錄和記錄檔。 不要與多個 HDInsight 叢集共用預設 Blob 容器。 這可能會損毀作業歷程記錄。 建議的 toouse 不同的容器，每個叢集，並將共用的資料放在部署的所有相關的叢集，而不是 hello 預設儲存體帳戶中指定的連結儲存體帳戶。 如需如何設定連結儲存體帳戶的詳細資訊，請參閱[建立 HDInsight 叢集][hdinsight-creation]。 不過您之後可以重複使用的預設儲存體容器 hello 原始的 HDInsight 叢集已被刪除。 HBase 叢集，您實際上可以藉由建立使用已刪除 HBase 叢集所用的 hello 預設 blob 容器的新 HBase 叢集保留 hello HBase 資料表的結構描述和資料。

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>使用 hello Azure 入口網站
當從 hello 入口網站中建立的 HDInsight 叢集，您可以 hello 選項 （如下所示） tooprovide hello 儲存體帳戶詳細資料。 您也可以指定是否要與 hello 叢集相關聯的額外儲存體帳戶，以及若是如此，選擇 從資料湖存放區或另一個 Azure 儲存體 blob，作為 hello 額外的存放裝置。

![HDinsight hadoop 建立資料來源](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。


### <a name="use-azure-powershell"></a>使用 Azure PowerShell
如果您[安裝及設定 Azure PowerShell][powershell-install]，您可以使用儲存體帳戶和容器中的 hello Azure PowerShell 提示 toocreate 下列 hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>使用 Azure CLI

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

如果您有[安裝並設定 hello Azure CLI](../cli-install-nodejs.md)，hello 下列命令可以使用的 tooa 儲存體帳戶和容器。

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> hello`--type`參數表示 hello 儲存體帳戶複寫的方式。 如需詳細資訊，請參閱 [Azure 儲存體複寫](../storage/storage-redundancy.md)。 請勿使用 ZRS，因為 ZRS 不支援分頁 Blob、檔案、資料表或佇列。
> 
> 

您必須提示的 toospecify hello 地理區域中建立 hello 儲存體帳戶。 您應該建立 hello 儲存體帳戶中 hello 您計劃建立您的 HDInsight 叢集的同一個地區。

Hello 儲存體帳戶建立之後，請使用下列命令 tooretrieve hello 儲存體帳戶金鑰的 hello:

    azure storage account keys list <storageaccountname>

toocreate 容器，使用下列命令的 hello:

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>定址 Azure 儲存體中的檔案
存取 Azure 儲存體中的檔案從 HDInsight hello URI 配置為：

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

hello URI 配置提供未加密的存取 (以 hello *wasb:*前置詞)，SSL 加密存取 (使用*wasbs*)。 我們建議您使用*wasbs*只要做得到，即使在存取內部的資料 hello Azure 中相同的區域。

hello &lt;BlobStorageContainerName&gt;識別 hello Azure 儲存體中的 hello blob 容器名稱。
hello &lt;StorageAccountName&gt;識別 hello Azure 儲存體帳戶名稱。 需要使用完整網域名稱 (FQDN)。

如果沒有&lt;BlobStorageContainerName&gt;也&lt;StorageAccountName&gt;已指定，會使用 hello 預設檔案系統。 Hello hello 預設檔案系統上的檔案，您可以使用相對路徑或絕對路徑。 例如，hello *hadoop-mapreduce-examples.jar*隨附的 HDInsight 叢集的檔案可以參考的 tooby 使用 hello 下列其中一種：

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> hello 檔案名稱為<i>hadoop examples.jar</i>中 2.1 和 1.6 版的 HDInsight 叢集。
> 
> 

hello&lt;路徑&gt;hello 檔案或目錄 HDFS 路徑名稱。 因為 Azure 儲存體中的容器僅是機碼值存放區，所以並沒有真正的階層式檔案系統。 Blob 機碼內的斜線字元 ( / ) 會被解釋為目錄分隔符號。 例如，hello blob 名稱*hadoop-mapreduce-examples.jar*是：

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> 當使用 HDInsight 外部 blob，大部分的公用程式不要辨識 hello WASB 格式和改為預期為基本的路徑格式，例如`example/jars/hadoop-mapreduce-examples.jar`。
> 
> 

## <a name="access-blobs"></a>存取 blob 


### <a name="access-blobs-using-azure-powershell"></a> 使用 Azure PowerShell
> [!NOTE]
> 本章節中的 hello 命令提供使用 PowerShell tooaccess 資料儲存在 blob 中的基本範例。 如需更完整範例使用 HDInsight 的自訂，請參閱 hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools)。
> 
> 

使用下列命令 toolist hello 與 blob 相關 cmdlet hello:

    Get-Command *blob*

![與 Blob 相關的 Power Shell Cmdlet 清單。][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>上傳檔案
請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。

#### <a name="download-files"></a>下載檔案
hello 下列指令碼下載的區塊 blob toohello 目前資料夾。 執行 hello 指令碼，才能變更 hello 目錄 tooa 資料夾具有寫入權限。

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

提供 hello 資源群組名稱和 hello 叢集名稱，您可以使用下列程式碼的 hello:

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>刪除檔案
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>列出檔案
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>使用未定義的儲存體帳戶執行 Hive 查詢
這個範例會示範如何 toolist 期間未定義的儲存體帳戶中的資料夾 hello 建立程序。
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>使用 Azure CLI
使用下列命令 toolist hello 與 blob 相關命令的 hello:

    azure storage blob

**使用 Azure CLI tooupload 檔案的範例**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**使用 Azure CLI toodownload 檔案的範例**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**使用 Azure CLI toodelete 檔案的範例**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**使用 Azure CLI toolist 檔案的範例**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>使用其他儲存體帳戶

在建立時的 HDInsight 叢集，您可以指定您想要與其 tooassociate hello Azure 儲存體帳戶。 此外 toothis 儲存體帳戶，您可以加入額外的儲存體帳戶從 hello 相同 Azure 訂用帳戶或不同的 Azure 訂閱 hello 建立程序期間，或在建立叢集之後。 如需關於新增其他儲存體帳戶的指示，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同位置中使用額外的儲存體帳戶。

## <a name="next-steps"></a>後續步驟
在本文中，您學到如何 toouse HDFS 相容與 HDInsight 的 Azure 儲存體。 這可讓您 toobuild 可擴充、 長期來看，保存資料擷取方案和使用 HDInsight toounlock hello 內部資訊 hello 儲存結構化和非結構化的資料。

如需詳細資訊，請參閱：

* [開始使用 Azure HDInsight][hdinsight-get-started]
* [開始使用 Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]
* [使用 Azure 儲存體共用存取簽章 toorestrict 存取 toodata 與 HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
