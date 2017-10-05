---
title: "在 HDInsight 上將 Hadoop 工作的資料上傳 | Microsoft Docs"
description: "了解如何使用 Azure CLI、Azure 儲存體總管、Azure PowerShell、Hadoop 命令列或 Sqoop 在 HDInsight 中上傳及存取 Hadoop 工作。"
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="e09b9-104">在 HDInsight 上將 Hadoop 工作的資料上傳</span><span class="sxs-lookup"><span data-stu-id="e09b9-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="e09b9-105">Azure HDInsight 在 Azure Blob 儲存體上提供了全功能的 Hadoop 分散式檔案系統 (HDFS)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="e09b9-106">此儲存體是設計為 HDFS 的延伸，以便為使用者提供流暢的體驗。</span><span class="sxs-lookup"><span data-stu-id="e09b9-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="e09b9-107">此儲存體可讓 Hadoop 生態系統中的完整元件集直接在它管理的資料上運作。</span><span class="sxs-lookup"><span data-stu-id="e09b9-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="e09b9-108">Azure Blob 儲存體和 HDFS 是不同的檔案系統，但經過最佳化後，都非常適合儲存資料以及計算儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="e09b9-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="e09b9-109">如需關於使用 Azure Blob 儲存體有哪些優點的資訊，請參閱[搭配 HDInsight 使用 Azure Blob 儲存體][hdinsight-storage]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="e09b9-110">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="e09b9-110">**Prerequisites**</span></span>

<span data-ttu-id="e09b9-111">開始進行之前，請注意下列需求：</span><span class="sxs-lookup"><span data-stu-id="e09b9-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="e09b9-112">Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="e09b9-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="e09b9-113">如需指示，請參閱 [Azure HDInsight 使用者入門][hdinsight-get-started]或[佈建 HDInsight 叢集][hdinsight-provision]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="e09b9-114">為什麼要使用 Blob 儲存體？</span><span class="sxs-lookup"><span data-stu-id="e09b9-114">Why blob storage?</span></span>
<span data-ttu-id="e09b9-115">部署 Azure HDInsight 叢集通常是為了執行 MapReduce 工作，並在這些工作完成後卸除叢集。</span><span class="sxs-lookup"><span data-stu-id="e09b9-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="e09b9-116">將計算完成後的資料保留在 HDFS 叢集是成本較高的資料儲存方式。</span><span class="sxs-lookup"><span data-stu-id="e09b9-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="e09b9-117">對於使用 HDInsight 來處理的資料，Azure Blob 儲存體是一種高可用性、高延展性、大容量、低成本且可共用的儲存方案。</span><span class="sxs-lookup"><span data-stu-id="e09b9-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="e09b9-118">將資料儲存在 Blob 中，可安全地釋放做為計算用途的 HDInsight 叢集，而且不會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="e09b9-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="e09b9-119">目錄</span><span class="sxs-lookup"><span data-stu-id="e09b9-119">Directories</span></span>
<span data-ttu-id="e09b9-120">Azure Blob 儲存體容器會以機碼/值組來儲存資料，而且沒有目錄階層。</span><span class="sxs-lookup"><span data-stu-id="e09b9-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="e09b9-121">然而，機碼名稱中可使用 "/" 字元，使檔案變成好像儲存在目錄結構中一樣。</span><span class="sxs-lookup"><span data-stu-id="e09b9-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="e09b9-122">HDInsight 會將它們視為就像是實際的目錄一樣。</span><span class="sxs-lookup"><span data-stu-id="e09b9-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="e09b9-123">例如，Blob 的機碼可能是 *input/log1.txt*。</span><span class="sxs-lookup"><span data-stu-id="e09b9-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="e09b9-124">實際上不存在 "input" 目錄，只是因為機碼名稱中有 "/" 字元，才形成檔案路徑的外觀。</span><span class="sxs-lookup"><span data-stu-id="e09b9-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="e09b9-125">因此，當您使用 Azure Explorer 工具時，可能會注意到一些 0 位元組的檔案。</span><span class="sxs-lookup"><span data-stu-id="e09b9-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="e09b9-126">這些檔案有兩種用途：</span><span class="sxs-lookup"><span data-stu-id="e09b9-126">These files serve two purposes:</span></span>

* <span data-ttu-id="e09b9-127">如果是空資料夾，這些檔案會標示資料夾的存在。</span><span class="sxs-lookup"><span data-stu-id="e09b9-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="e09b9-128">Azure Blob 儲存體很聰明，它知道如果有一個名為 foo/bar 的 Blob ，就有一個名為 **foo**的資料夾。</span><span class="sxs-lookup"><span data-stu-id="e09b9-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="e09b9-129">但如果要表達有一個名為 **foo** 的空資料夾，唯一的辦法就是放入這個特殊的 0 位元組檔案。</span><span class="sxs-lookup"><span data-stu-id="e09b9-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="e09b9-130">這些檔案中保存 Hadoop 檔案系統所需的特殊中繼資料，尤其是資料夾的權限和擁有者。</span><span class="sxs-lookup"><span data-stu-id="e09b9-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="e09b9-131">命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="e09b9-131">Command-line utilities</span></span>
<span data-ttu-id="e09b9-132">Microsoft 提供下列公用程式來使用 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="e09b9-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="e09b9-133">工具</span><span class="sxs-lookup"><span data-stu-id="e09b9-133">Tool</span></span> | <span data-ttu-id="e09b9-134">Linux</span><span class="sxs-lookup"><span data-stu-id="e09b9-134">Linux</span></span> | <span data-ttu-id="e09b9-135">OS X</span><span class="sxs-lookup"><span data-stu-id="e09b9-135">OS X</span></span> | <span data-ttu-id="e09b9-136">Windows</span><span class="sxs-lookup"><span data-stu-id="e09b9-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="e09b9-137">[Azure 命令列介面][azurecli]</span><span class="sxs-lookup"><span data-stu-id="e09b9-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="e09b9-138">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-138">✔</span></span> |<span data-ttu-id="e09b9-139">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-139">✔</span></span> |<span data-ttu-id="e09b9-140">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-140">✔</span></span> |
| <span data-ttu-id="e09b9-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="e09b9-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="e09b9-142">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-142">✔</span></span> |
| <span data-ttu-id="e09b9-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="e09b9-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="e09b9-144">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-144">✔</span></span> |
| [<span data-ttu-id="e09b9-145">Hadoop 命令</span><span class="sxs-lookup"><span data-stu-id="e09b9-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="e09b9-146">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-146">✔</span></span> |<span data-ttu-id="e09b9-147">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-147">✔</span></span> |<span data-ttu-id="e09b9-148">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="e09b9-149">雖然 Azure CLI、Azure PowerShell 與 AzCopy 都可從外部 Azure 使用，但是 Hadoop 命令只能在 HDInsight 叢集上使用，而且只允許將資料從本機檔案系統載入到 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e09b9-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="e09b9-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e09b9-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="e09b9-151">Azure CLI 是可讓您管理 Azure 服務的跨平台工具。</span><span class="sxs-lookup"><span data-stu-id="e09b9-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="e09b9-152">使用以下步驟將資料上傳至 Azure Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="e09b9-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="e09b9-153">[安裝和設定適用於 Mac、Linux 和 Windows 的 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="e09b9-154">開啟命令提示字元、Bash 或其他殼層，然後使用以下命令驗證您的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e09b9-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="e09b9-155">出現提示時，輸入訂用帳戶的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e09b9-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="e09b9-156">輸入以下命令可列出訂用帳戶的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="e09b9-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="e09b9-157">選取含有您想要使用之 Blob 的儲存體帳戶，然後使用以下命令擷取此帳戶的金鑰：</span><span class="sxs-lookup"><span data-stu-id="e09b9-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="e09b9-158">此時應該會傳回**主要**和**次要**金鑰。</span><span class="sxs-lookup"><span data-stu-id="e09b9-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="e09b9-159">複製 **主要** 金鑰值，因為接下來的步驟中會使用此值。</span><span class="sxs-lookup"><span data-stu-id="e09b9-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="e09b9-160">使用以下命令擷取儲存體帳戶內的 Blob 儲存體清單：</span><span class="sxs-lookup"><span data-stu-id="e09b9-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="e09b9-161">使用以下命令將檔案上傳及下載至 Blob：</span><span class="sxs-lookup"><span data-stu-id="e09b9-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="e09b9-162">上傳檔案：</span><span class="sxs-lookup"><span data-stu-id="e09b9-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="e09b9-163">下載檔案：</span><span class="sxs-lookup"><span data-stu-id="e09b9-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="e09b9-164">如果您會持續使用同一個儲存體帳戶，可以設定以下環境變數，而不是為每個命令指定帳戶和金鑰：</span><span class="sxs-lookup"><span data-stu-id="e09b9-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="e09b9-165">**AZURE\_STORAGE\_ACCOUNT**：儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="e09b9-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="e09b9-166">**AZURE\_STORAGE\_ACCESS\_KEY**：儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="e09b9-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="e09b9-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e09b9-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="e09b9-168">Azure PowerShell 是一種指令碼環境，可讓您在 Azure 中用來控制和自動化工作負載的部署及管理。</span><span class="sxs-lookup"><span data-stu-id="e09b9-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="e09b9-169">如需關於設定工作站以執行 Azure PowerShell 的資訊，請參閱 [安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="e09b9-170">**將本機檔案上傳至 Azure Blob 儲存體**</span><span class="sxs-lookup"><span data-stu-id="e09b9-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="e09b9-171">依照 [安裝和設定 Azure PowerShell](/powershell/azure/overview)的指示，開啟 Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="e09b9-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="e09b9-172">在下列指令碼中設定前五個變數的值：</span><span class="sxs-lookup"><span data-stu-id="e09b9-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="e09b9-173">將指令碼貼到 Azure PowerShell 主控台，並執行該指令碼來複製檔案。</span><span class="sxs-lookup"><span data-stu-id="e09b9-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="e09b9-174">如需建立來使用 HDInsight 的 PowerShell 指令碼範例，請參閱 [HDInsight 工具](https://github.com/blackmist/hdinsight-tools)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="e09b9-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="e09b9-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="e09b9-176">AzCopy 是一套命令列工具，此工具設計目的在於簡化將資料移入及移出 Azure 儲存體帳戶的傳輸工作。</span><span class="sxs-lookup"><span data-stu-id="e09b9-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="e09b9-177">您可以將它當做獨立工具來使用，也可以將此工具納入現有的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e09b9-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="e09b9-178">[下載 AzCopy][azure-azcopy-download]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="e09b9-179">AzCopy 語法如下：</span><span class="sxs-lookup"><span data-stu-id="e09b9-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="e09b9-180">如需詳細資訊，請參閱 [AzCopy - 上傳/下載 Azure Blob 的檔案][azure-azcopy]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="e09b9-181"><a id="commandline"></a>Hadoop 命令列</span><span class="sxs-lookup"><span data-stu-id="e09b9-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="e09b9-182">Hadoop 命令列僅適用於當資料已存在於叢集前端節點時，將資料儲存到 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e09b9-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="e09b9-183">若要使用 Hadoop 命令，您必須先使用下列其中一個方法連線到前端節點：</span><span class="sxs-lookup"><span data-stu-id="e09b9-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="e09b9-184">**Windows 架構的 HDInsight**： [使用遠端桌面連線](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="e09b9-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="e09b9-185">**Linux 架構的 HDInsight**：使用 SSH ([SSH 命令](hdinsight-hadoop-linux-use-ssh-unix.md) 或 [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md)) 來連線</span><span class="sxs-lookup"><span data-stu-id="e09b9-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="e09b9-186">連線之後，您就可以使用下列語法來將檔案上傳到儲存體。</span><span class="sxs-lookup"><span data-stu-id="e09b9-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="e09b9-187">例如， `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="e09b9-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="e09b9-188">因為 HDInsight 的預設檔案系統是位於 Azure Blob 儲存體中，所以 /example/data.txt 實際上是在 Azure Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="e09b9-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="e09b9-189">您也可以用下列語法來參考此檔案：</span><span class="sxs-lookup"><span data-stu-id="e09b9-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="e09b9-190">或</span><span class="sxs-lookup"><span data-stu-id="e09b9-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="e09b9-191">如需其他可用來處理檔案的 Hadoop 命令清單，請參閱 [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="e09b9-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="e09b9-192">在 HBase 叢集上，寫入資料時所使用的預設區塊大小是 256 KB。</span><span class="sxs-lookup"><span data-stu-id="e09b9-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="e09b9-193">雖然在使用 HBase API 或 REST API 時此大小可正常運作，但使用 `hadoop` 或 `hdfs dfs` 命令寫入大於 ~12 GB 的資料會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="e09b9-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="e09b9-194">如需詳細資訊，請參閱下面的[在 Blob 上寫入時的儲存體例外狀況](#storageexception)一節。</span><span class="sxs-lookup"><span data-stu-id="e09b9-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="e09b9-195">圖形化用戶端</span><span class="sxs-lookup"><span data-stu-id="e09b9-195">Graphical clients</span></span>
<span data-ttu-id="e09b9-196">其他還有數個應用程式也會提供可搭配 Azure 儲存體使用的圖形化介面。</span><span class="sxs-lookup"><span data-stu-id="e09b9-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="e09b9-197">以下提供數個這類應用程式的清單：</span><span class="sxs-lookup"><span data-stu-id="e09b9-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="e09b9-198">用戶端</span><span class="sxs-lookup"><span data-stu-id="e09b9-198">Client</span></span> | <span data-ttu-id="e09b9-199">Linux</span><span class="sxs-lookup"><span data-stu-id="e09b9-199">Linux</span></span> | <span data-ttu-id="e09b9-200">OS X</span><span class="sxs-lookup"><span data-stu-id="e09b9-200">OS X</span></span> | <span data-ttu-id="e09b9-201">Windows</span><span class="sxs-lookup"><span data-stu-id="e09b9-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="e09b9-202">Microsoft Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="e09b9-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="e09b9-203">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-203">✔</span></span> |<span data-ttu-id="e09b9-204">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-204">✔</span></span> |<span data-ttu-id="e09b9-205">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-205">✔</span></span> |
| [<span data-ttu-id="e09b9-206">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="e09b9-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="e09b9-207">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-207">✔</span></span> |<span data-ttu-id="e09b9-208">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-208">✔</span></span> |<span data-ttu-id="e09b9-209">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-209">✔</span></span> |
| [<span data-ttu-id="e09b9-210">Cloud Storage Studio 2</span><span class="sxs-lookup"><span data-stu-id="e09b9-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="e09b9-211">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-211">✔</span></span> |
| [<span data-ttu-id="e09b9-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="e09b9-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="e09b9-213">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-213">✔</span></span> |
| [<span data-ttu-id="e09b9-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="e09b9-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="e09b9-215">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-215">✔</span></span> |
| [<span data-ttu-id="e09b9-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="e09b9-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="e09b9-217">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-217">✔</span></span> |<span data-ttu-id="e09b9-218">✔</span><span class="sxs-lookup"><span data-stu-id="e09b9-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="e09b9-219">Visual Studio Tools for HDInsight</span><span class="sxs-lookup"><span data-stu-id="e09b9-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="e09b9-220">如需詳細資訊，請參閱 [瀏覽連結的資源](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="e09b9-221"><a id="storageexplorer"></a>Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="e09b9-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="e09b9-222">*Azure 儲存體總管* 是一種可在 Blob 中檢查和變更資料的實用工具。</span><span class="sxs-lookup"><span data-stu-id="e09b9-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="e09b9-223">它是免費開放原始碼工具，可從 [http://storageexplorer.com/](http://storageexplorer.com/)下載。</span><span class="sxs-lookup"><span data-stu-id="e09b9-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="e09b9-224">原始碼亦可從此連結取得。</span><span class="sxs-lookup"><span data-stu-id="e09b9-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="e09b9-225">使用此工具之前，必須先知道您的 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="e09b9-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="e09b9-226">如需關於取得此資訊的指示，請參閱[建立、管理或刪除儲存體帳戶][azure-create-storage-account]的＜如何：檢視、複製及重新產生儲存體存取金鑰＞一節。</span><span class="sxs-lookup"><span data-stu-id="e09b9-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="e09b9-227">執行 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="e09b9-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="e09b9-228">如果這是您第一次執行 [儲存體總管]，系統將會提示您輸入 [儲存體帳戶名稱] 和 [儲存體帳戶金鑰]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="e09b9-229">如果您之前曾執行過，請使用 [新增] 按鈕加入新的儲存體帳戶名稱和金鑰。</span><span class="sxs-lookup"><span data-stu-id="e09b9-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="e09b9-230">輸入 HDInsight 叢集所使用儲存體帳戶的名稱和金鑰，然後選取 [儲存並開啟]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI.AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="e09b9-232">在此介面左邊的 [容器] 清單中，按一下與 HDInsight 叢集相關聯的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="e09b9-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="e09b9-233">根據預設，這是 HDInsight 叢集的名稱，但如果您在建立叢集時輸入了特定名稱，則有可能不同。</span><span class="sxs-lookup"><span data-stu-id="e09b9-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="e09b9-234">從工具列選取上傳圖示。</span><span class="sxs-lookup"><span data-stu-id="e09b9-234">From the tool bar, select the upload icon.</span></span>

    ![工具列和反白顯示的上傳圖示](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="e09b9-236">指定要上傳的檔案，然後按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="e09b9-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="e09b9-237">出現提示時，請選取 [上傳]  將檔案上傳至儲存體容器的根目錄。</span><span class="sxs-lookup"><span data-stu-id="e09b9-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="e09b9-238">如果您想要將檔案上傳到特定路徑，請在 [目的地] 欄位中輸入路徑，然後選取 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![檔案上傳對話方塊](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="e09b9-240">完成上傳檔案之後，您可以從 HDInsight 叢集上的作業加以使用。</span><span class="sxs-lookup"><span data-stu-id="e09b9-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="e09b9-241">將 Azure Blob 儲存體掛接為本機磁碟機</span><span class="sxs-lookup"><span data-stu-id="e09b9-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="e09b9-242">請參閱 [將 Azure Blob 儲存體掛接為本機磁碟機](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="e09b9-243">服務</span><span class="sxs-lookup"><span data-stu-id="e09b9-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="e09b9-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e09b9-244">Azure Data Factory</span></span>
<span data-ttu-id="e09b9-245">Azure Data Factory 服務是完全受管理的服務，可將資料儲存、資料處理及資料移動服務組合成有效率、可調整且可靠的資料生產管線。</span><span class="sxs-lookup"><span data-stu-id="e09b9-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="e09b9-246">Azure Data Factory 可用來將資料移至 Azure Blob 儲存體，或建立資料管線直接使用 HDInsight 功能，例如 Hive 和 Pig。</span><span class="sxs-lookup"><span data-stu-id="e09b9-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="e09b9-247">如需詳細資訊，請參閱 [Azure Data Factory 文件](https://azure.microsoft.com/documentation/services/data-factory/)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="e09b9-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="e09b9-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="e09b9-249">Sqoop 是一種專門在 Hadoop 和關聯式資料庫之間傳送資料的工具。</span><span class="sxs-lookup"><span data-stu-id="e09b9-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="e09b9-250">此工具可讓您從 SQL Server、MySQL 或 Oracle 等關聯式資料庫管理系統 (RDBMS)，將資料匯入 Hadoop 分散式檔案系統 (HDFS)，使用 MapReduce 或 Hive 轉換 Hadoop 中的資料，然後將資料匯回 RDBMS。</span><span class="sxs-lookup"><span data-stu-id="e09b9-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="e09b9-251">如需詳細資訊，請參閱[搭配 HDInsight 使用 Sqoop][hdinsight-use-sqoop]。</span><span class="sxs-lookup"><span data-stu-id="e09b9-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="e09b9-252">開發 SDK</span><span class="sxs-lookup"><span data-stu-id="e09b9-252">Development SDKs</span></span>
<span data-ttu-id="e09b9-253">Azure Blob 儲存體也可以使用 Azure SDK，透過下列程式設計語言來存取：</span><span class="sxs-lookup"><span data-stu-id="e09b9-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="e09b9-254">.NET</span><span class="sxs-lookup"><span data-stu-id="e09b9-254">.NET</span></span>
* <span data-ttu-id="e09b9-255">Java</span><span class="sxs-lookup"><span data-stu-id="e09b9-255">Java</span></span>
* <span data-ttu-id="e09b9-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="e09b9-256">Node.js</span></span>
* <span data-ttu-id="e09b9-257">PHP</span><span class="sxs-lookup"><span data-stu-id="e09b9-257">PHP</span></span>
* <span data-ttu-id="e09b9-258">Python</span><span class="sxs-lookup"><span data-stu-id="e09b9-258">Python</span></span>
* <span data-ttu-id="e09b9-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="e09b9-259">Ruby</span></span>

<span data-ttu-id="e09b9-260">如需安裝 Azure SDK 的詳細資訊，請參閱 [Azure 下載](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="e09b9-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e09b9-261">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e09b9-261">Troubleshooting</span></span>
### <span data-ttu-id="e09b9-262"><a id="storageexception"></a>在 Blob 上寫入時的儲存體例外狀況</span><span class="sxs-lookup"><span data-stu-id="e09b9-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="e09b9-263">**徵兆**︰使用 `hadoop` 或 `hdfs dfs` 命令在 HBase 叢集上寫入 ~12 GB 或更大的檔案時，您可能會遇到下列錯誤︰</span><span class="sxs-lookup"><span data-stu-id="e09b9-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="e09b9-264">**原因**：在寫入 Azure 儲存體時，HDInsight 叢集上的 HBase 會將區塊大小預設為 256 KB。</span><span class="sxs-lookup"><span data-stu-id="e09b9-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="e09b9-265">雖然這適用於 HBase API 或 REST API，但會導致在使用 `hadoop` 或 `hdfs dfs` 命令列公用程式時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="e09b9-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="e09b9-266">**解決方案**︰使用 `fs.azure.write.request.size` 指定較大的區塊大小。</span><span class="sxs-lookup"><span data-stu-id="e09b9-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="e09b9-267">您可以使用 `-D` 參數針對每一次使用進行指定。</span><span class="sxs-lookup"><span data-stu-id="e09b9-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="e09b9-268">以下是搭配使用此參數與 `hadoop` 命令的範例︰</span><span class="sxs-lookup"><span data-stu-id="e09b9-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="e09b9-269">您也可以使用 Ambari，全域增加 `fs.azure.write.request.size` 的值。</span><span class="sxs-lookup"><span data-stu-id="e09b9-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="e09b9-270">使用下列步驟即可變更 Ambari Web UI 中的值︰</span><span class="sxs-lookup"><span data-stu-id="e09b9-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="e09b9-271">在瀏覽器中，移至叢集的 Ambari Web UI。</span><span class="sxs-lookup"><span data-stu-id="e09b9-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="e09b9-272">這是 https://CLUSTERNAME.azurehdinsight.net，其中 **CLUSTERNAME** 是叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="e09b9-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="e09b9-273">出現提示時，請輸入該叢集的管理員名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="e09b9-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="e09b9-274">在畫面左側選取 [HDFS]，然後選取 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e09b9-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="e09b9-275">在 [篩選...] 欄位中，輸入 `fs.azure.write.request.size`。</span><span class="sxs-lookup"><span data-stu-id="e09b9-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="e09b9-276">這會在頁面中間顯示欄位和目前的值。</span><span class="sxs-lookup"><span data-stu-id="e09b9-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="e09b9-277">將值從 262144 (256 KB) 變更為新值。</span><span class="sxs-lookup"><span data-stu-id="e09b9-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="e09b9-278">例如，4194304 (4 MB)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-278">For example, 4194304 (4MB).</span></span>

![透過 Ambari Web UI 變更值的影像](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="e09b9-280">如需使用 Ambari 的詳細資訊，請參閱[使用 Ambari Web UI 管理 HDInsight 叢集](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="e09b9-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e09b9-281">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e09b9-281">Next steps</span></span>
<span data-ttu-id="e09b9-282">您現在已了解如何將資料匯入 HDInsight，請接著閱讀下列文章以了解如何執行分析：</span><span class="sxs-lookup"><span data-stu-id="e09b9-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="e09b9-283">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e09b9-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="e09b9-284">[以程式設計方式提交 Hadoop 工作][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="e09b9-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="e09b9-285">[搭配 HDInsight 使用 Hivet][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e09b9-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="e09b9-286">[搭配 HDInsight 使用 Pig][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e09b9-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
