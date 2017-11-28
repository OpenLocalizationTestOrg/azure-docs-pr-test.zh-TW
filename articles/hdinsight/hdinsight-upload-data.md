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
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="7b574-104">在 HDInsight 上將 Hadoop 工作的資料上傳</span><span class="sxs-lookup"><span data-stu-id="7b574-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="7b574-105">Azure HDInsight 在 Azure Blob 儲存體上提供了全功能的 Hadoop 分散式檔案系統 (HDFS)。</span><span class="sxs-lookup"><span data-stu-id="7b574-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="7b574-106">其設計目的是為 HDFS 延伸 tooprovide 順暢的體驗 toocustomers。</span><span class="sxs-lookup"><span data-stu-id="7b574-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="7b574-107">它可讓 hello 整組 hello Hadoop 生態系統 toooperate 直接在其所管理的 hello 資料中的元件。</span><span class="sxs-lookup"><span data-stu-id="7b574-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="7b574-108">Azure Blob 儲存體和 HDFS 是不同的檔案系統，但經過最佳化後，都非常適合儲存資料以及計算儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="7b574-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="7b574-109">使用 Azure Blob 儲存體的 hello 優點的相關資訊，請參閱[使用 Azure Blob 儲存體與 HDInsight][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="7b574-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="7b574-110">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="7b574-110">**Prerequisites**</span></span>

<span data-ttu-id="7b574-111">請注意下列需求，在您開始前的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="7b574-112">Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b574-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="7b574-113">如需指示，請參閱 [Azure HDInsight 使用者入門][hdinsight-get-started]或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="7b574-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="7b574-114">為什麼要使用 Blob 儲存體？</span><span class="sxs-lookup"><span data-stu-id="7b574-114">Why blob storage?</span></span>
<span data-ttu-id="7b574-115">Azure HDInsight 叢集通常是部署 toorun MapReduce 工作，而且這些工作完成之後，會卸除 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b574-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="7b574-116">將 hello 資料保留 hello HDFS 叢集計算完成之後會高度耗費資源的方式 toostore 這項資料。</span><span class="sxs-lookup"><span data-stu-id="7b574-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="7b574-117">Azure Blob 儲存體是高可用性、 高擴充性、 高容量、 toobe 使用 HDInsight 處理資料的低成本，並可共用的存放裝置選項。</span><span class="sxs-lookup"><span data-stu-id="7b574-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="7b574-118">將資料儲存在 blob 可讓用來安全地釋放，而不會遺失資料的計算 toobe hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="7b574-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="7b574-119">目錄</span><span class="sxs-lookup"><span data-stu-id="7b574-119">Directories</span></span>
<span data-ttu-id="7b574-120">Azure Blob 儲存體容器會以機碼/值組來儲存資料，而且沒有目錄階層。</span><span class="sxs-lookup"><span data-stu-id="7b574-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="7b574-121">不過 hello"/"字元可以用它出現當做檔案儲存在目錄結構中的 hello 索引鍵名稱 toomake 內。</span><span class="sxs-lookup"><span data-stu-id="7b574-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="7b574-122">HDInsight 會將它們視為就像是實際的目錄一樣。</span><span class="sxs-lookup"><span data-stu-id="7b574-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="7b574-123">例如，Blob 的機碼可能是 *input/log1.txt*。</span><span class="sxs-lookup"><span data-stu-id="7b574-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="7b574-124">沒有實際的 「 輸入 」 目錄存在，但因為 toohello 與否 hello"/"字元在 hello 索引鍵的名稱，它有 hello 外觀的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="7b574-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="7b574-125">因此，當您使用 Azure Explorer 工具時，可能會注意到一些 0 位元組的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b574-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="7b574-126">這些檔案有兩種用途：</span><span class="sxs-lookup"><span data-stu-id="7b574-126">These files serve two purposes:</span></span>

* <span data-ttu-id="7b574-127">如果空的資料夾，它們標示的 hello hello 資料夾存在。</span><span class="sxs-lookup"><span data-stu-id="7b574-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="7b574-128">Azure Blob 儲存體是呼叫 foo/列 blob 存在，是否有一個名為資料夾的不夠聰明 tooknow **foo**。</span><span class="sxs-lookup"><span data-stu-id="7b574-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="7b574-129">但 hello 稱為空資料夾的唯一方式 toosignify **foo**是就地具有此特殊 0 位元組的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b574-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="7b574-130">它們具有特殊的中繼資料所需的 hello Hadoop 檔案系統，值得注意的是 「 hello 權限 」 和 「 hello 資料夾的擁有者。</span><span class="sxs-lookup"><span data-stu-id="7b574-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="7b574-131">命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="7b574-131">Command-line utilities</span></span>
<span data-ttu-id="7b574-132">Microsoft 提供下列公用程式使用 Azure Blob 儲存體的 toowork hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="7b574-133">工具</span><span class="sxs-lookup"><span data-stu-id="7b574-133">Tool</span></span> | <span data-ttu-id="7b574-134">Linux</span><span class="sxs-lookup"><span data-stu-id="7b574-134">Linux</span></span> | <span data-ttu-id="7b574-135">OS X</span><span class="sxs-lookup"><span data-stu-id="7b574-135">OS X</span></span> | <span data-ttu-id="7b574-136">Windows</span><span class="sxs-lookup"><span data-stu-id="7b574-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="7b574-137">[Azure 命令列介面][azurecli]</span><span class="sxs-lookup"><span data-stu-id="7b574-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="7b574-138">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-138">✔</span></span> |<span data-ttu-id="7b574-139">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-139">✔</span></span> |<span data-ttu-id="7b574-140">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-140">✔</span></span> |
| <span data-ttu-id="7b574-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="7b574-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="7b574-142">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-142">✔</span></span> |
| <span data-ttu-id="7b574-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="7b574-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="7b574-144">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-144">✔</span></span> |
| [<span data-ttu-id="7b574-145">Hadoop 命令</span><span class="sxs-lookup"><span data-stu-id="7b574-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="7b574-146">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-146">✔</span></span> |<span data-ttu-id="7b574-147">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-147">✔</span></span> |<span data-ttu-id="7b574-148">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="7b574-149">雖然 hello Azure CLI、 Azure PowerShell 及 AzCopy 可以在所有可用於從外部 Azure hello Hadoop 命令只有在 hello HDInsight 叢集上使用，且只允許 hello 本機檔案系統從 Azure Blob 儲存體將資料載入。</span><span class="sxs-lookup"><span data-stu-id="7b574-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="7b574-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b574-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="7b574-151">hello Azure CLI 是跨平台工具，可讓您 toomanage Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7b574-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="7b574-152">使用下列步驟 tooupload 資料 tooAzure Blob 儲存體的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="7b574-153">[安裝及設定 Mac、 Linux 和 Windows hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="7b574-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="7b574-154">開啟命令提示字元、 bash 或其他殼層中，並使用 hello 遵循 tooauthenticate tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b574-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="7b574-155">出現提示時，輸入您的訂用帳戶 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7b574-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="7b574-156">輸入下列命令 toolist hello 訂用帳戶的儲存體帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="7b574-157">選取包含您想要 toowork hello blob hello 儲存體帳戶，然後使用下列命令 tooretrieve hello 索引鍵，此帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="7b574-158">此時應該會傳回**主要**和**次要**金鑰。</span><span class="sxs-lookup"><span data-stu-id="7b574-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="7b574-159">複製 hello**主要**機碼值，因為它會用在 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="7b574-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="7b574-160">使用下列命令 tooretrieve hello 儲存體帳戶內的 blob 容器的清單中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="7b574-161">使用下列命令 tooupload hello 和下載檔案 toohello blob:</span><span class="sxs-lookup"><span data-stu-id="7b574-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="7b574-162">tooupload 檔案：</span><span class="sxs-lookup"><span data-stu-id="7b574-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="7b574-163">toodownload 檔案：</span><span class="sxs-lookup"><span data-stu-id="7b574-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="7b574-164">如果您將一律在 hello 與相同儲存體帳戶，您可以設定下列環境變數，而不是指定 hello 帳戶 hello 和機碼的每個命令：</span><span class="sxs-lookup"><span data-stu-id="7b574-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="7b574-165">**AZURE\_儲存體\_帳戶**: hello 儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="7b574-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="7b574-166">**AZURE\_儲存體\_存取\_金鑰**: hello 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="7b574-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="7b574-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b574-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="7b574-168">Azure PowerShell 是您可以使用 toocontrol 並自動化 hello 部署和管理您的工作負載在 Azure 中的指令碼環境。</span><span class="sxs-lookup"><span data-stu-id="7b574-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="7b574-169">設定您的工作站 toorun Azure PowerShell 的相關資訊，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7b574-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="7b574-170">**tooupload 本機檔案 tooAzure Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="7b574-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="7b574-171">開啟 hello Azure PowerShell 主控台中的指示[安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7b574-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="7b574-172">在 hello 下列指令碼中設定 hello hello 值前五個變數：</span><span class="sxs-lookup"><span data-stu-id="7b574-172">Set hello values of hello first five variables in hello following script:</span></span>

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
3. <span data-ttu-id="7b574-173">貼上 hello 其撰寫指令碼至 hello Azure PowerShell 主控台 toorun toocopy hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7b574-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="7b574-174">如需範例 PowerShell 指令碼建立 toowork 與 HDInsight，請參閱[HDInsight tools](https://github.com/blackmist/hdinsight-tools)。</span><span class="sxs-lookup"><span data-stu-id="7b574-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="7b574-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="7b574-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="7b574-176">AzCopy 是命令列工具，設計 toosimplify hello 工作的 Azure 儲存體帳戶中來回傳送資料。</span><span class="sxs-lookup"><span data-stu-id="7b574-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="7b574-177">您可以將它當做獨立工具來使用，也可以將此工具納入現有的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="7b574-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="7b574-178">[下載 AzCopy][azure-azcopy-download]。</span><span class="sxs-lookup"><span data-stu-id="7b574-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="7b574-179">hello AzCopy 語法是：</span><span class="sxs-lookup"><span data-stu-id="7b574-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="7b574-180">如需詳細資訊，請參閱 [AzCopy - 上傳/下載 Azure Blob 的檔案][azure-azcopy]。</span><span class="sxs-lookup"><span data-stu-id="7b574-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="7b574-181"><a id="commandline"></a>Hadoop 命令列</span><span class="sxs-lookup"><span data-stu-id="7b574-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="7b574-182">hello Hadoop 命令列僅適用於當 hello 資料已存在於 hello 叢集前端節點上，將資料儲存到 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b574-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="7b574-183">在順序 toouse hello Hadoop 命令，您必須先連接 toohello 叢集前端節點使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="7b574-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="7b574-184">**Windows 架構的 HDInsight**： [使用遠端桌面連線](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="7b574-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="7b574-185">**以 Linux 為基礎的 HDInsight**： 使用 SSH 連線 ([hello SSH 命令](hdinsight-hadoop-linux-use-ssh-unix.md)或[PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="7b574-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="7b574-186">一旦連接之後，您可以使用下列語法 tooupload 檔案 toostorage hello。</span><span class="sxs-lookup"><span data-stu-id="7b574-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="7b574-187">例如， `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="7b574-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="7b574-188">因為 hello 預設檔案系統，HDInsight 的 Azure Blob 儲存體，/example/data.txt 實際上是 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="7b574-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="7b574-189">您也可以參考 toohello 檔案儲存為：</span><span class="sxs-lookup"><span data-stu-id="7b574-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="7b574-190">或</span><span class="sxs-lookup"><span data-stu-id="7b574-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="7b574-191">如需其他可用來處理檔案的 Hadoop 命令清單，請參閱 [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="7b574-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="7b574-192">HBase 叢集上寫入資料是 256 KB 使用 hello 預設區塊大小。</span><span class="sxs-lookup"><span data-stu-id="7b574-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="7b574-193">雖然這適合使用 HBase 應用程式開發介面或 REST Api 時，使用 hello`hadoop`或`hdfs dfs`命令 toowrite 大於 ~ 12 GB 的資料會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b574-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="7b574-194">請參閱 hello[寫入 blob 上的儲存體例外狀況](#storageexception)下面章節，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7b574-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="7b574-195">圖形化用戶端</span><span class="sxs-lookup"><span data-stu-id="7b574-195">Graphical clients</span></span>
<span data-ttu-id="7b574-196">其他還有數個應用程式也會提供可搭配 Azure 儲存體使用的圖形化介面。</span><span class="sxs-lookup"><span data-stu-id="7b574-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="7b574-197">hello 以下是幾個這些應用程式的清單：</span><span class="sxs-lookup"><span data-stu-id="7b574-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="7b574-198">用戶端</span><span class="sxs-lookup"><span data-stu-id="7b574-198">Client</span></span> | <span data-ttu-id="7b574-199">Linux</span><span class="sxs-lookup"><span data-stu-id="7b574-199">Linux</span></span> | <span data-ttu-id="7b574-200">OS X</span><span class="sxs-lookup"><span data-stu-id="7b574-200">OS X</span></span> | <span data-ttu-id="7b574-201">Windows</span><span class="sxs-lookup"><span data-stu-id="7b574-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="7b574-202">Microsoft Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b574-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="7b574-203">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-203">✔</span></span> |<span data-ttu-id="7b574-204">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-204">✔</span></span> |<span data-ttu-id="7b574-205">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-205">✔</span></span> |
| [<span data-ttu-id="7b574-206">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="7b574-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="7b574-207">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-207">✔</span></span> |<span data-ttu-id="7b574-208">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-208">✔</span></span> |<span data-ttu-id="7b574-209">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-209">✔</span></span> |
| [<span data-ttu-id="7b574-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="7b574-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="7b574-211">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-211">✔</span></span> |
| [<span data-ttu-id="7b574-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="7b574-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="7b574-213">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-213">✔</span></span> |
| [<span data-ttu-id="7b574-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="7b574-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="7b574-215">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-215">✔</span></span> |
| [<span data-ttu-id="7b574-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="7b574-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="7b574-217">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-217">✔</span></span> |<span data-ttu-id="7b574-218">✔</span><span class="sxs-lookup"><span data-stu-id="7b574-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="7b574-219">Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b574-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="7b574-220">如需詳細資訊，請參閱[瀏覽 hello 已連結的資源](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources)。</span><span class="sxs-lookup"><span data-stu-id="7b574-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="7b574-221"><a id="storageexplorer"></a>Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="7b574-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="7b574-222">*Azure 儲存體總管*是有用的工具，可檢查及更改 blob 中的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7b574-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="7b574-223">它是免費開放原始碼工具，可從 [http://storageexplorer.com/](http://storageexplorer.com/)下載。</span><span class="sxs-lookup"><span data-stu-id="7b574-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="7b574-224">使用此連結，以及從 hello 原始程式碼。</span><span class="sxs-lookup"><span data-stu-id="7b574-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="7b574-225">使用 hello 工具之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="7b574-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="7b574-226">取得這項資訊的相關指示，請參閱 hello"如何： 檢視、 複製和重新產生儲存體存取金鑰 」 一節[建立、 管理或刪除儲存體帳戶][azure-create-storage-account]。</span><span class="sxs-lookup"><span data-stu-id="7b574-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="7b574-227">執行 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="7b574-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="7b574-228">如果這是 hello 第一次您有執行 hello 存放裝置總管，將會提示您輸入 hello **（_s） 帳戶名稱**和**儲存體帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7b574-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="7b574-229">如果您有執行它之前，請使用 hello**新增**按鈕 tooadd 新的儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="7b574-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="7b574-230">輸入名稱和您的 HDInsight 叢集所使用的 hello 儲存體帳戶金鑰，然後選取 hello**儲存和開啟**。</span><span class="sxs-lookup"><span data-stu-id="7b574-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="7b574-232">Hello 在清單中的 hello 介面的容器 toohello 左側，按一下 hello 與您的 HDInsight 叢集相關聯的 hello 容器名稱。</span><span class="sxs-lookup"><span data-stu-id="7b574-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="7b574-233">根據預設，這是 hello hello HDInsight 叢集名稱，但如果您輸入特定名稱建立 hello 叢集時可能會不同。</span><span class="sxs-lookup"><span data-stu-id="7b574-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="7b574-234">從 [hello] 工具列上，選取 hello 上傳的圖示。</span><span class="sxs-lookup"><span data-stu-id="7b574-234">From hello tool bar, select hello upload icon.</span></span>

    ![工具列和反白顯示的上傳圖示](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="7b574-236">指定檔案 tooupload，，然後按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="7b574-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="7b574-237">出現提示時，選取**上傳**tooupload hello 檔案 toohello 根目錄 hello 儲存體容器。</span><span class="sxs-lookup"><span data-stu-id="7b574-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="7b574-238">如果您想 tooupload hello 檔案 tooa 特定路徑，輸入 hello 路徑 hello**目的地**欄位，然後選取 **上傳**。</span><span class="sxs-lookup"><span data-stu-id="7b574-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![檔案上傳對話方塊](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="7b574-240">在 hello 檔案已上傳完成時，您可以使用它從 hello HDInsight 叢集上的作業。</span><span class="sxs-lookup"><span data-stu-id="7b574-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="7b574-241">將 Azure Blob 儲存體掛接為本機磁碟機</span><span class="sxs-lookup"><span data-stu-id="7b574-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="7b574-242">請參閱 [將 Azure Blob 儲存體掛接為本機磁碟機](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7b574-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="7b574-243">服務</span><span class="sxs-lookup"><span data-stu-id="7b574-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="7b574-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7b574-244">Azure Data Factory</span></span>
<span data-ttu-id="7b574-245">hello Azure Data Factory 服務是完全受管理的服務，以便撰寫成有效率、 可擴充且可靠的資料實際執行管線的資料儲存體、 資料處理和資料移動服務。</span><span class="sxs-lookup"><span data-stu-id="7b574-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="7b574-246">Azure Data Factory 可以使用的 toomove 資料到 Azure Blob 儲存體，或直接使用 HDInsight 功能，例如 toocreate 資料管線 Hive 和 Pig。</span><span class="sxs-lookup"><span data-stu-id="7b574-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="7b574-247">如需詳細資訊，請參閱 hello [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="7b574-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="7b574-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="7b574-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="7b574-249">Sqoop 是 Hadoop 和關聯式資料庫之間所設計的工具 tootransfer 資料。</span><span class="sxs-lookup"><span data-stu-id="7b574-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="7b574-250">您可以使用它 tooimport 資料從關聯式資料庫管理系統 (RDBMS)，例如 SQL Server、 MySQL 或 Oracle hello Hadoop 分散式檔案系統 (HDFS)，到 Hadoop MapReduce 或登錄區，使用中的 hello 資料轉換，然後匯出成的 hello 資料RDBMS。</span><span class="sxs-lookup"><span data-stu-id="7b574-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="7b574-251">如需詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="7b574-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="7b574-252">開發 SDK</span><span class="sxs-lookup"><span data-stu-id="7b574-252">Development SDKs</span></span>
<span data-ttu-id="7b574-253">Azure Blob 儲存體也可以使用下列的程式語言的 hello 從 Azure SDK 來存取：</span><span class="sxs-lookup"><span data-stu-id="7b574-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="7b574-254">.NET</span><span class="sxs-lookup"><span data-stu-id="7b574-254">.NET</span></span>
* <span data-ttu-id="7b574-255">Java</span><span class="sxs-lookup"><span data-stu-id="7b574-255">Java</span></span>
* <span data-ttu-id="7b574-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="7b574-256">Node.js</span></span>
* <span data-ttu-id="7b574-257">PHP</span><span class="sxs-lookup"><span data-stu-id="7b574-257">PHP</span></span>
* <span data-ttu-id="7b574-258">Python</span><span class="sxs-lookup"><span data-stu-id="7b574-258">Python</span></span>
* <span data-ttu-id="7b574-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="7b574-259">Ruby</span></span>

<span data-ttu-id="7b574-260">如需安裝 hello Azure Sdk 的詳細資訊，請參閱[Azure 下載](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="7b574-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7b574-261">疑難排解</span><span class="sxs-lookup"><span data-stu-id="7b574-261">Troubleshooting</span></span>
### <span data-ttu-id="7b574-262"><a id="storageexception"></a>在 Blob 上寫入時的儲存體例外狀況</span><span class="sxs-lookup"><span data-stu-id="7b574-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="7b574-263">**徵狀**： 當使用 hello`hadoop`或`hdfs dfs`toowrite 檔案的命令是 ~ 12 GB 或更大 HBase 叢集上，您可能會遇到下列錯誤 hello:</span><span class="sxs-lookup"><span data-stu-id="7b574-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

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

<span data-ttu-id="7b574-264">**可能的原因**： 撰寫 tooAzure 儲存體時，在 HDInsight HBase 叢集預設 tooa 區塊大小為 256 KB。</span><span class="sxs-lookup"><span data-stu-id="7b574-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="7b574-265">雖然這適用於 HBase 應用程式開發介面或 REST Api，它會導致發生錯誤時使用 hello`hadoop`或`hdfs dfs`命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="7b574-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="7b574-266">**解析**： 使用`fs.azure.write.request.size`toospecify 較大的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="7b574-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="7b574-267">您可以在每次使用基礎上使用 hello`-D`參數。</span><span class="sxs-lookup"><span data-stu-id="7b574-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="7b574-268">hello 的範例如下使用此參數以 hello`hadoop`命令：</span><span class="sxs-lookup"><span data-stu-id="7b574-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="7b574-269">您也可以增加 hello 值`fs.azure.write.request.size`全域利用 Ambari。</span><span class="sxs-lookup"><span data-stu-id="7b574-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="7b574-270">hello 下列步驟可以是 hello Ambari Web UI 中用於 toochange hello 值：</span><span class="sxs-lookup"><span data-stu-id="7b574-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="7b574-271">在您的瀏覽器，移 toohello Ambari Web UI，針對您的叢集。</span><span class="sxs-lookup"><span data-stu-id="7b574-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="7b574-272">這是 https://CLUSTERNAME.azurehdinsight.net，其中**CLUSTERNAME**是 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b574-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="7b574-273">出現提示時，輸入 hello 叢集 hello 管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="7b574-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="7b574-274">從 hello 囉 」 畫面的左側，選取**HDFS**，然後選取 [hello **Configs** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7b574-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="7b574-275">在 hello**篩選...**欄位中，輸入`fs.azure.write.request.size`。</span><span class="sxs-lookup"><span data-stu-id="7b574-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="7b574-276">這會顯示 hello 欄位和目前的值，在 hello hello 頁面中間。</span><span class="sxs-lookup"><span data-stu-id="7b574-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="7b574-277">變更 hello 262144 (256 KB) toohello 新值。</span><span class="sxs-lookup"><span data-stu-id="7b574-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="7b574-278">例如，4194304 (4 MB)。</span><span class="sxs-lookup"><span data-stu-id="7b574-278">For example, 4194304 (4MB).</span></span>

![變更 Ambari Web UI 的 hello 寶貴的映像](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="7b574-280">如需有關使用 Ambari 的詳細資訊，請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="7b574-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b574-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b574-281">Next steps</span></span>
<span data-ttu-id="7b574-282">既然您了解 HDInsight tooget 資料的讀取方式 hello 如何遵循文章 toolearn tooperform 分析：</span><span class="sxs-lookup"><span data-stu-id="7b574-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="7b574-283">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="7b574-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="7b574-284">[以程式設計方式提交 Hadoop 工作][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="7b574-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="7b574-285">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="7b574-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="7b574-286">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="7b574-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
