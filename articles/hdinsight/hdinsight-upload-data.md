---
title: "在 HDInsight Hadoop 工作的 aaaUpload 資料 |Microsoft 文件"
description: "了解如何在使用 HDInsight Hadoop 工作的 tooupload 和存取資料 hello Azure CLI、 Azure 儲存體總管、 Azure PowerShell、 hello Hadoop 命令列或 Sqoop。"
keywords: "etl hadoop、將資料上傳到 hadoop、hadoop 載入資料"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a>在 HDInsight 上將 Hadoop 工作的資料上傳
Azure HDInsight 在 Azure Blob 儲存體上提供了全功能的 Hadoop 分散式檔案系統 (HDFS)。 其設計目的是為 HDFS 延伸 tooprovide 順暢的體驗 toocustomers。 它可讓 hello 整組 hello Hadoop 生態系統 toooperate 直接在其所管理的 hello 資料中的元件。 Azure Blob 儲存體和 HDFS 是不同的檔案系統，但經過最佳化後，都非常適合儲存資料以及計算儲存的資料。 使用 Azure Blob 儲存體的 hello 優點的相關資訊，請參閱[使用 Azure Blob 儲存體與 HDInsight][hdinsight-storage]。

**必要條件**

請注意下列需求，在您開始前的 hello:

* Azure HDInsight 叢集。 如需指示，請參閱 [Azure HDInsight 使用者入門][hdinsight-get-started]或[佈建 HDInsight 叢集][hdinsight-provision]。

## <a name="why-blob-storage"></a>為什麼要使用 Blob 儲存體？
Azure HDInsight 叢集通常是部署 toorun MapReduce 工作，而且這些工作完成之後，會卸除 hello 叢集。 將 hello 資料保留 hello HDFS 叢集計算完成之後會高度耗費資源的方式 toostore 這項資料。 Azure Blob 儲存體是高可用性、 高擴充性、 高容量、 toobe 使用 HDInsight 處理資料的低成本，並可共用的存放裝置選項。 將資料儲存在 blob 可讓用來安全地釋放，而不會遺失資料的計算 toobe hello HDInsight 叢集。

### <a name="directories"></a>目錄
Azure Blob 儲存體容器會以機碼/值組來儲存資料，而且沒有目錄階層。 不過 hello"/"字元可以用它出現當做檔案儲存在目錄結構中的 hello 索引鍵名稱 toomake 內。 HDInsight 會將它們視為就像是實際的目錄一樣。

例如，Blob 的機碼可能是 *input/log1.txt*。 沒有實際的 「 輸入 」 目錄存在，但因為 toohello 與否 hello"/"字元在 hello 索引鍵的名稱，它有 hello 外觀的檔案路徑。

因此，當您使用 Azure Explorer 工具時，可能會注意到一些 0 位元組的檔案。 這些檔案有兩種用途：

* 如果空的資料夾，它們標示的 hello hello 資料夾存在。 Azure Blob 儲存體是呼叫 foo/列 blob 存在，是否有一個名為資料夾的不夠聰明 tooknow **foo**。 但 hello 稱為空資料夾的唯一方式 toosignify **foo**是就地具有此特殊 0 位元組的檔案。
* 它們具有特殊的中繼資料所需的 hello Hadoop 檔案系統，值得注意的是 「 hello 權限 」 和 「 hello 資料夾的擁有者。

## <a name="command-line-utilities"></a>命令列公用程式
Microsoft 提供下列公用程式使用 Azure Blob 儲存體的 toowork hello:

| 工具 | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Azure 命令列介面][azurecli] |✔ |✔ |✔ |
| [Azure PowerShell][azure-powershell] | | |✔ |
| [AzCopy][azure-azcopy] | | |✔ |
| [Hadoop 命令](#commandline) |✔ |✔ |✔ |

> [!NOTE]
> 雖然 hello Azure CLI、 Azure PowerShell 及 AzCopy 可以在所有可用於從外部 Azure hello Hadoop 命令只有在 hello HDInsight 叢集上使用，且只允許 hello 本機檔案系統從 Azure Blob 儲存體將資料載入。
>
>

### <a id="xplatcli"></a>Azure CLI
hello Azure CLI 是跨平台工具，可讓您 toomanage Azure 服務。 使用下列步驟 tooupload 資料 tooAzure Blob 儲存體的 hello:

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. [安裝及設定 Mac、 Linux 和 Windows hello Azure CLI](../cli-install-nodejs.md)。
2. 開啟命令提示字元、 bash 或其他殼層中，並使用 hello 遵循 tooauthenticate tooyour Azure 訂用帳戶。

        azure login

    出現提示時，輸入您的訂用帳戶 hello 使用者名稱和密碼。
3. 輸入下列命令 toolist hello 訂用帳戶的儲存體帳戶的 hello:

        azure storage account list
4. 選取包含您想要 toowork hello blob hello 儲存體帳戶，然後使用下列命令 tooretrieve hello 索引鍵，此帳戶的 hello:

        azure storage account keys list <storage-account-name>

    此時應該會傳回**主要**和**次要**金鑰。 複製 hello**主要**機碼值，因為它會用在 hello 接下來的步驟。
5. 使用下列命令 tooretrieve hello 儲存體帳戶內的 blob 容器的清單中的 hello:

        azure storage container list -a <storage-account-name> -k <primary-key>
6. 使用下列命令 tooupload hello 和下載檔案 toohello blob:

   * tooupload 檔案：

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * toodownload 檔案：

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> 如果您將一律在 hello 與相同儲存體帳戶，您可以設定下列環境變數，而不是指定 hello 帳戶 hello 和機碼的每個命令：
>
> * **AZURE\_儲存體\_帳戶**: hello 儲存體帳戶名稱
> * **AZURE\_儲存體\_存取\_金鑰**: hello 儲存體帳戶金鑰
>
>

### <a id="powershell"></a>Azure PowerShell
Azure PowerShell 是您可以使用 toocontrol 並自動化 hello 部署和管理您的工作負載在 Azure 中的指令碼環境。 設定您的工作站 toorun Azure PowerShell 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

**tooupload 本機檔案 tooAzure Blob 儲存體**

1. 開啟 hello Azure PowerShell 主控台中的指示[安裝和設定 Azure PowerShell](/powershell/azure/overview)。
2. 在 hello 下列指令碼中設定 hello hello 值前五個變數：

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. 貼上 hello 其撰寫指令碼至 hello Azure PowerShell 主控台 toorun toocopy hello 檔案。

如需範例 PowerShell 指令碼建立 toowork 與 HDInsight，請參閱[HDInsight tools](https://github.com/blackmist/hdinsight-tools)。

### <a id="azcopy"></a>AzCopy
AzCopy 是命令列工具，設計 toosimplify hello 工作的 Azure 儲存體帳戶中來回傳送資料。 您可以將它當做獨立工具來使用，也可以將此工具納入現有的應用程式中。 [下載 AzCopy][azure-azcopy-download]。

hello AzCopy 語法是：

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

如需詳細資訊，請參閱 [AzCopy - 上傳/下載 Azure Blob 的檔案][azure-azcopy]。

### <a id="commandline"></a>Hadoop 命令列
hello Hadoop 命令列僅適用於當 hello 資料已存在於 hello 叢集前端節點上，將資料儲存到 blob 儲存體。

在順序 toouse hello Hadoop 命令，您必須先連接 toohello 叢集前端節點使用其中一種 hello 下列方法：

* **Windows 架構的 HDInsight**： [使用遠端桌面連線](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)
* **以 Linux 為基礎的 HDInsight**： 使用 SSH 連線 ([hello SSH 命令](hdinsight-hadoop-linux-use-ssh-unix.md)或[PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))

一旦連接之後，您可以使用下列語法 tooupload 檔案 toostorage hello。

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

例如， `hadoop fs -copyFromLocal data.txt /example/data/data.txt`

因為 hello 預設檔案系統，HDInsight 的 Azure Blob 儲存體，/example/data.txt 實際上是 Azure Blob 儲存體中。 您也可以參考 toohello 檔案儲存為：

    wasb:///example/data/data.txt

或

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

如需其他可用來處理檔案的 Hadoop 命令清單，請參閱 [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)

> [!WARNING]
> HBase 叢集上寫入資料是 256 KB 使用 hello 預設區塊大小。 雖然這適合使用 HBase 應用程式開發介面或 REST Api 時，使用 hello`hadoop`或`hdfs dfs`命令 toowrite 大於 ~ 12 GB 的資料會導致錯誤。 請參閱 hello[寫入 blob 上的儲存體例外狀況](#storageexception)下面章節，如需詳細資訊。
>
>

## <a name="graphical-clients"></a>圖形化用戶端
其他還有數個應用程式也會提供可搭配 Azure 儲存體使用的圖形化介面。 hello 以下是幾個這些應用程式的清單：

| 用戶端 | Linux | OS X | Windows |
| --- |:---:|:---:|:---:|
| [Microsoft Visual Studio Tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |✔ |✔ |✔ |
| [Azure 儲存體總管](http://storageexplorer.com/) |✔ |✔ |✔ |
| [Cloud Storage Studio 2](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |✔ |
| [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) | | |✔ |
| [Azure Explorer](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |✔ |
| [Cyberduck](https://cyberduck.io/) | |✔ |✔ |

### <a name="visual-studio-tools-for-hdinsight"></a>Visual Studio Tools for HDInsight
如需詳細資訊，請參閱[瀏覽 hello 已連結的資源](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources)。

### <a id="storageexplorer"></a>Azure 儲存體總管
*Azure 儲存體總管*是有用的工具，可檢查及更改 blob 中的 hello 資料。 它是免費開放原始碼工具，可從 [http://storageexplorer.com/](http://storageexplorer.com/)下載。 使用此連結，以及從 hello 原始程式碼。

使用 hello 工具之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。 取得這項資訊的相關指示，請參閱 hello"如何： 檢視、 複製和重新產生儲存體存取金鑰 」 一節[建立、 管理或刪除儲存體帳戶][azure-create-storage-account]。

1. 執行 Azure 儲存體總管。 如果這是 hello 第一次您有執行 hello 存放裝置總管，將會提示您輸入 hello **（_s） 帳戶名稱**和**儲存體帳戶金鑰**。 如果您有執行它之前，請使用 hello**新增**按鈕 tooadd 新的儲存體帳戶名稱和金鑰。

    輸入名稱和您的 HDInsight 叢集所使用的 hello 儲存體帳戶金鑰，然後選取 hello**儲存和開啟**。

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. Hello 在清單中的 hello 介面的容器 toohello 左側，按一下 hello 與您的 HDInsight 叢集相關聯的 hello 容器名稱。 根據預設，這是 hello hello HDInsight 叢集名稱，但如果您輸入特定名稱建立 hello 叢集時可能會不同。
3. 從 [hello] 工具列上，選取 hello 上傳的圖示。

    ![工具列和反白顯示的上傳圖示](./media/hdinsight-upload-data/toolbar.png)
4. 指定檔案 tooupload，，然後按一下**開啟**。 出現提示時，選取**上傳**tooupload hello 檔案 toohello 根目錄 hello 儲存體容器。 如果您想 tooupload hello 檔案 tooa 特定路徑，輸入 hello 路徑 hello**目的地**欄位，然後選取 **上傳**。

    ![檔案上傳對話方塊](./media/hdinsight-upload-data/fileupload.png)

    在 hello 檔案已上傳完成時，您可以使用它從 hello HDInsight 叢集上的作業。

## <a name="mount-azure-blob-storage-as-local-drive"></a>將 Azure Blob 儲存體掛接為本機磁碟機
請參閱 [將 Azure Blob 儲存體掛接為本機磁碟機](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx)。

## <a name="services"></a>服務
### <a name="azure-data-factory"></a>Azure Data Factory
hello Azure Data Factory 服務是完全受管理的服務，以便撰寫成有效率、 可擴充且可靠的資料實際執行管線的資料儲存體、 資料處理和資料移動服務。

Azure Data Factory 可以使用的 toomove 資料到 Azure Blob 儲存體，或直接使用 HDInsight 功能，例如 toocreate 資料管線 Hive 和 Pig。

如需詳細資訊，請參閱 hello [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)。

### <a id="sqoop"></a>Apache Sqoop
Sqoop 是 Hadoop 和關聯式資料庫之間所設計的工具 tootransfer 資料。 您可以使用它 tooimport 資料從關聯式資料庫管理系統 (RDBMS)，例如 SQL Server、 MySQL 或 Oracle hello Hadoop 分散式檔案系統 (HDFS)，到 Hadoop MapReduce 或登錄區，使用中的 hello 資料轉換，然後匯出成的 hello 資料RDBMS。

如需詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。

## <a name="development-sdks"></a>開發 SDK
Azure Blob 儲存體也可以使用下列的程式語言的 hello 從 Azure SDK 來存取：

* .NET
* Java
* Node.js
* PHP
* Python
* Ruby

如需安裝 hello Azure Sdk 的詳細資訊，請參閱[Azure 下載](https://azure.microsoft.com/downloads/)

## <a name="troubleshooting"></a>疑難排解
### <a id="storageexception"></a>在 Blob 上寫入時的儲存體例外狀況
**徵狀**： 當使用 hello`hadoop`或`hdfs dfs`toowrite 檔案的命令是 ~ 12 GB 或更大 HBase 叢集上，您可能會遇到下列錯誤 hello:

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

**可能的原因**： 撰寫 tooAzure 儲存體時，在 HDInsight HBase 叢集預設 tooa 區塊大小為 256 KB。 雖然這適用於 HBase 應用程式開發介面或 REST Api，它會導致發生錯誤時使用 hello`hadoop`或`hdfs dfs`命令列公用程式。

**解析**： 使用`fs.azure.write.request.size`toospecify 較大的區塊大小。 您可以在每次使用基礎上使用 hello`-D`參數。 hello 的範例如下使用此參數以 hello`hadoop`命令：

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

您也可以增加 hello 值`fs.azure.write.request.size`全域利用 Ambari。 hello 下列步驟可以是 hello Ambari Web UI 中用於 toochange hello 值：

1. 在您的瀏覽器，移 toohello Ambari Web UI，針對您的叢集。 這是 https://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME**是 hello 叢集的名稱。

    出現提示時，輸入 hello 叢集 hello 管理員名稱和密碼。
2. 從 hello 囉 」 畫面的左側，選取**HDFS**，然後選取 [hello **Configs** ] 索引標籤。
3. 在 hello**篩選...**欄位中，輸入`fs.azure.write.request.size`。 這會顯示 hello 欄位和目前的值，在 hello hello 頁面中間。
4. 變更 hello 262144 (256 KB) toohello 新值。 例如，4194304 (4 MB)。

![變更 Ambari Web UI 的 hello 寶貴的映像](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

如需有關使用 Ambari 的詳細資訊，請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。

## <a name="next-steps"></a>後續步驟
既然您了解 HDInsight tooget 資料的讀取方式 hello 如何遵循文章 toolearn tooperform 分析：

* [開始使用 Azure HDInsight][hdinsight-get-started]
* [以程式設計方式提交 Hadoop 工作][hdinsight-submit-jobs]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Pig][hdinsight-use-pig]

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
