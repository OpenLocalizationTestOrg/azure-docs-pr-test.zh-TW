---
title: "將資料從 Azure 儲存體 Blob 複製到 Data Lake Store | Microsoft Docs"
description: "使用 AdlCopy 工具將資料從 Azure 儲存體 Blob 複製到 Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68f44991432a76c2ef1c79ec6dffdea4c62bcb17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-from-azure-storage-blobs-to-data-lake-store"></a><span data-ttu-id="cf59d-103">將資料從 Azure 儲存體 Blob 複製到 Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cf59d-103">Copy data from Azure Storage Blobs to Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf59d-104">使用 DistCp</span><span class="sxs-lookup"><span data-stu-id="cf59d-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="cf59d-105">使用 AdlCopy</span><span class="sxs-lookup"><span data-stu-id="cf59d-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="cf59d-106">Azure Data Lake Store 提供命令列工具 [AdlCopy](http://aka.ms/downloadadlcopy)以從下列來源複製資料：</span><span class="sxs-lookup"><span data-stu-id="cf59d-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), to copy data from the following sources:</span></span>

* <span data-ttu-id="cf59d-107">從 Azure 儲存體 Blob 複製到 Data Lake Store 中。</span><span class="sxs-lookup"><span data-stu-id="cf59d-107">From Azure Storage Blobs into Data Lake Store.</span></span> <span data-ttu-id="cf59d-108">您無法使用 AdlCopy 將資料從 Data Lake Store 複製到 Azure 儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="cf59d-108">You cannot use AdlCopy to copy data from Data Lake Store to Azure Storage blobs.</span></span>
* <span data-ttu-id="cf59d-109">兩個 Azure Data Lake Store 帳戶之間。</span><span class="sxs-lookup"><span data-stu-id="cf59d-109">Between two Azure Data Lake Store accounts.</span></span>

<span data-ttu-id="cf59d-110">此外，您可以兩個不同的模式使用 AdlCopy 工具：</span><span class="sxs-lookup"><span data-stu-id="cf59d-110">Also, you can use the AdlCopy tool in two different modes:</span></span>

* <span data-ttu-id="cf59d-111">**單獨使用**，此工具會使用 Data Lake Store 資源來執行工作。</span><span class="sxs-lookup"><span data-stu-id="cf59d-111">**Standalone**, where the tool uses Data Lake Store resources to perform the task.</span></span>
* <span data-ttu-id="cf59d-112">**使用 Data Lake Analytics 帳戶**，指派給 Data Lake Analytics 帳戶的單位可用來執行複製作業。</span><span class="sxs-lookup"><span data-stu-id="cf59d-112">**Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation.</span></span> <span data-ttu-id="cf59d-113">當您想要以可預測的方式執行複製工作時，可能會想使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cf59d-113">You might want to use this option when you are looking to perform the copy tasks in a predictable manner.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf59d-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="cf59d-114">Prerequisites</span></span>
<span data-ttu-id="cf59d-115">開始閱讀本文之前，您必須符合下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="cf59d-115">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="cf59d-116">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cf59d-116">**An Azure subscription**.</span></span> <span data-ttu-id="cf59d-117">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cf59d-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cf59d-118">**Azure 儲存體 Blob** 容器 (其中含有一些資料)。</span><span class="sxs-lookup"><span data-stu-id="cf59d-118">**Azure Storage Blobs** container with some data.</span></span>
* <span data-ttu-id="cf59d-119">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="cf59d-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="cf59d-120">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cf59d-120">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="cf59d-121">**Azure Data Lake Analytics 帳戶 (選用)** - 如需如何建立 Data Lake Store 帳戶的指示，請參閱 [開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="cf59d-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how to create a Data Lake Store account.</span></span>
* <span data-ttu-id="cf59d-122">**AdlCopy 工具**。</span><span class="sxs-lookup"><span data-stu-id="cf59d-122">**AdlCopy tool**.</span></span> <span data-ttu-id="cf59d-123">從 [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)安裝 AdlCopy 工具。</span><span class="sxs-lookup"><span data-stu-id="cf59d-123">Install the AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span></span>

## <a name="syntax-of-the-adlcopy-tool"></a><span data-ttu-id="cf59d-124">AdlCopy 工具的語法</span><span class="sxs-lookup"><span data-stu-id="cf59d-124">Syntax of the AdlCopy tool</span></span>
<span data-ttu-id="cf59d-125">利用下列語法來使用 AdlCopy 工具</span><span class="sxs-lookup"><span data-stu-id="cf59d-125">Use the following syntax to work with the AdlCopy tool</span></span>

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

<span data-ttu-id="cf59d-126">以下將說明語法中的參數：</span><span class="sxs-lookup"><span data-stu-id="cf59d-126">The parameters in the syntax are described below:</span></span>

| <span data-ttu-id="cf59d-127">選項</span><span class="sxs-lookup"><span data-stu-id="cf59d-127">Option</span></span> | <span data-ttu-id="cf59d-128">說明</span><span class="sxs-lookup"><span data-stu-id="cf59d-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf59d-129">來源</span><span class="sxs-lookup"><span data-stu-id="cf59d-129">Source</span></span> |<span data-ttu-id="cf59d-130">指定來源資料在 Azure 儲存體 Blob 中的位置。</span><span class="sxs-lookup"><span data-stu-id="cf59d-130">Specifies the location of the source data in the Azure storage blob.</span></span> <span data-ttu-id="cf59d-131">來源可以是 Blob 容器、Blob 或其他 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf59d-131">The source can be a blob container, a blob, or another Data Lake Store account.</span></span> |
| <span data-ttu-id="cf59d-132">Dest</span><span class="sxs-lookup"><span data-stu-id="cf59d-132">Dest</span></span> |<span data-ttu-id="cf59d-133">指定要複製的 Data Lake Store 目的地。</span><span class="sxs-lookup"><span data-stu-id="cf59d-133">Specifies the Data Lake Store destination to copy to.</span></span> |
| <span data-ttu-id="cf59d-134">SourceKey</span><span class="sxs-lookup"><span data-stu-id="cf59d-134">SourceKey</span></span> |<span data-ttu-id="cf59d-135">指定 Azure 儲存體 Blob 來源的儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="cf59d-135">Specifies the storage access key for the Azure storage blob source.</span></span> <span data-ttu-id="cf59d-136">這只有在來源是 Blob 容器或 Blob 時才是必要的。</span><span class="sxs-lookup"><span data-stu-id="cf59d-136">This is required only if the source is a blob container or a blob.</span></span> |
| <span data-ttu-id="cf59d-137">帳戶</span><span class="sxs-lookup"><span data-stu-id="cf59d-137">Account</span></span> |<span data-ttu-id="cf59d-138">**選用**。</span><span class="sxs-lookup"><span data-stu-id="cf59d-138">**Optional**.</span></span> <span data-ttu-id="cf59d-139">如果您想要使用 Azure Data Lake Analytics 帳戶來執行複製工作，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cf59d-139">Use this if you want to use Azure Data Lake Analytics account to run the copy job.</span></span> <span data-ttu-id="cf59d-140">如果您在語法中使用 /Account 選項，但未指定 Data Lake Analytics 帳戶，AdlCopy 就會使用預設帳戶來執行工作。</span><span class="sxs-lookup"><span data-stu-id="cf59d-140">If you use the /Account option in the syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account to run the job.</span></span> <span data-ttu-id="cf59d-141">此外，如果您使用此選項，就必須加入來源 (Azure 儲存體 Blob) 和目的地 (Azure Data Lake Store) 做為 Data Lake Analytics 帳戶的資料來源。</span><span class="sxs-lookup"><span data-stu-id="cf59d-141">Also, if you use this option, you must add the source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span></span> |
| <span data-ttu-id="cf59d-142">Units</span><span class="sxs-lookup"><span data-stu-id="cf59d-142">Units</span></span> |<span data-ttu-id="cf59d-143">指定將針對複製工作使用的 Data Lake Analytics 單位數目。</span><span class="sxs-lookup"><span data-stu-id="cf59d-143">Specifies the number of Data Lake Analytics units that will be used for the copy job.</span></span> <span data-ttu-id="cf59d-144">如果您使用 **/Account** 選項來指定 Data Lake Analytics 帳戶，則此為必要選項。</span><span class="sxs-lookup"><span data-stu-id="cf59d-144">This option is mandatory if you use the **/Account** option to specify the Data Lake Analytics account.</span></span> |
| <span data-ttu-id="cf59d-145">模式</span><span class="sxs-lookup"><span data-stu-id="cf59d-145">Pattern</span></span> |<span data-ttu-id="cf59d-146">指定用來指示要複製哪些 Blob 或檔案的 regex 模式。</span><span class="sxs-lookup"><span data-stu-id="cf59d-146">Specifies a regex pattern that indicates which blobs or files to copy.</span></span> <span data-ttu-id="cf59d-147">AdlCopy 使用區分大小寫的比對。</span><span class="sxs-lookup"><span data-stu-id="cf59d-147">AdlCopy uses case-sensitive matching.</span></span> <span data-ttu-id="cf59d-148">不指定任何模式時所使用的預設模式是複製所有項目。</span><span class="sxs-lookup"><span data-stu-id="cf59d-148">The default pattern used when no pattern is specified is to copy all items.</span></span> <span data-ttu-id="cf59d-149">不支援指定多個檔案模式。</span><span class="sxs-lookup"><span data-stu-id="cf59d-149">Specifying multiple file patterns is not supported.</span></span> |

## <a name="use-adlcopy-as-standalone-to-copy-data-from-an-azure-storage-blob"></a><span data-ttu-id="cf59d-150">使用 AdlCopy (獨立) 從 Azure 儲存體 Blob 複製資料</span><span class="sxs-lookup"><span data-stu-id="cf59d-150">Use AdlCopy (as standalone) to copy data from an Azure Storage blob</span></span>
1. <span data-ttu-id="cf59d-151">開啟命令提示字元，並瀏覽至安裝 AdlCopy 的目錄，通常是 `%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="cf59d-151">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="cf59d-152">執行下列命令，將特定的 Blob 從來源容器複製到 Data Lake Store：</span><span class="sxs-lookup"><span data-stu-id="cf59d-152">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="cf59d-153">例如：</span><span class="sxs-lookup"><span data-stu-id="cf59d-153">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] <span data-ttu-id="cf59d-154">上述語法指定要複製到 Data Lake Store 帳戶內資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="cf59d-154">The syntax above specifies the file to be copied to a folder in the Data Lake Store account.</span></span> <span data-ttu-id="cf59d-155">如果指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="cf59d-155">AdlCopy tool creates a folder if the specified folder name does not exist.</span></span>

    <span data-ttu-id="cf59d-156">系統會提示您輸入您 Data Lake Store 帳戶所在 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="cf59d-156">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="cf59d-157">您將看到類似以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="cf59d-157">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. <span data-ttu-id="cf59d-158">您也可以使用下列命令，將所有的 Blob 從某一個容器複製到 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="cf59d-158">You can also copy all the blobs from one container to the Data Lake Store account using the following command:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    <span data-ttu-id="cf59d-159">例如：</span><span class="sxs-lookup"><span data-stu-id="cf59d-159">For example:</span></span>

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a><span data-ttu-id="cf59d-160">效能考量</span><span class="sxs-lookup"><span data-stu-id="cf59d-160">Performance considerations</span></span>

<span data-ttu-id="cf59d-161">如果您從 Azure Blob 儲存體帳戶複製，Blob 儲存體端在複製期間可能會進行節流。</span><span class="sxs-lookup"><span data-stu-id="cf59d-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on the blob storage side.</span></span> <span data-ttu-id="cf59d-162">這會降低複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="cf59d-162">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="cf59d-163">若要深入了解 Azure Blob 儲存體的限制，請參閱 [Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)中的 Azure 儲存體限制。</span><span class="sxs-lookup"><span data-stu-id="cf59d-163">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="use-adlcopy-as-standalone-to-copy-data-from-another-data-lake-store-account"></a><span data-ttu-id="cf59d-164">使用 AdlCopy (獨立) 從另一個 Data Lake Store 帳戶複製資料</span><span class="sxs-lookup"><span data-stu-id="cf59d-164">Use AdlCopy (as standalone) to copy data from another Data Lake Store account</span></span>
<span data-ttu-id="cf59d-165">您也可以使用 AdlCopy 在兩個 Data Lake Store 帳戶之間複製資料。</span><span class="sxs-lookup"><span data-stu-id="cf59d-165">You can also use AdlCopy to copy data between two Data Lake Store accounts.</span></span>

1. <span data-ttu-id="cf59d-166">開啟命令提示字元，並瀏覽至安裝 AdlCopy 的目錄，通常是 `%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="cf59d-166">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="cf59d-167">執行下列命令，從 Data Lake Store 帳戶將特定檔案複製到另一個 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf59d-167">Run the following command to copy a specific file from one Data Lake Store account to another.</span></span>

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    <span data-ttu-id="cf59d-168">例如：</span><span class="sxs-lookup"><span data-stu-id="cf59d-168">For example:</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > <span data-ttu-id="cf59d-169">上述語法會指定要複製到目的地 Data Lake Store 帳戶內資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="cf59d-169">The syntax above specifies the file to be copied to a folder in the destination Data Lake Store account.</span></span> <span data-ttu-id="cf59d-170">如果指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="cf59d-170">AdlCopy tool creates a folder if the specified folder name does not exist.</span></span>
   >
   >

    <span data-ttu-id="cf59d-171">系統會提示您輸入您 Data Lake Store 帳戶所在 Azure 訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="cf59d-171">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="cf59d-172">您將看到類似以下的輸出：</span><span class="sxs-lookup"><span data-stu-id="cf59d-172">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. <span data-ttu-id="cf59d-173">下列命令會將來源 Data Lake Store 帳戶特定資料夾中的所有檔案，複製到目的地 Data Lake Store 帳戶中的資料夾。</span><span class="sxs-lookup"><span data-stu-id="cf59d-173">The following command copies all files from a specific folder in the source Data Lake Store account to a folder in the destination Data Lake Store account.</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a><span data-ttu-id="cf59d-174">效能考量</span><span class="sxs-lookup"><span data-stu-id="cf59d-174">Performance considerations</span></span>

<span data-ttu-id="cf59d-175">使用 AdlCopy 作為獨立工具時，複製是在共用的 Azure 受管理資源上執行。</span><span class="sxs-lookup"><span data-stu-id="cf59d-175">When using AdlCopy as a standalone tool, the copy is run on shared, Azure managed resources.</span></span> <span data-ttu-id="cf59d-176">您在此環境中的可達到的效能取決於系統負載和可用的資源。</span><span class="sxs-lookup"><span data-stu-id="cf59d-176">The performance you may get in this environment depends on system load and available resources.</span></span> <span data-ttu-id="cf59d-177">這個模式最適合臨時的少量傳輸。</span><span class="sxs-lookup"><span data-stu-id="cf59d-177">This mode is best used for small transfers on an ad hoc basis.</span></span> <span data-ttu-id="cf59d-178">使用 AdlCopy 作為獨立工具時不需要調整參數。</span><span class="sxs-lookup"><span data-stu-id="cf59d-178">No parameters need to be tuned when using AdlCopy as a standalone tool.</span></span>

## <a name="use-adlcopy-with-data-lake-analytics-account-to-copy-data"></a><span data-ttu-id="cf59d-179">使用 AdlCopy (利用 Data Lake Analytics 帳戶) 複製資料</span><span class="sxs-lookup"><span data-stu-id="cf59d-179">Use AdlCopy (with Data Lake Analytics account) to copy data</span></span>
<span data-ttu-id="cf59d-180">您也可以使用 Data Lake Analytics 帳戶來執行 AdlCopy 工作，將資料從 Azure 儲存體 Blob 複製到 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="cf59d-180">You can also use your Data Lake Analytics account to run the AdlCopy job to copy data from Azure storage blobs to Data Lake Store.</span></span> <span data-ttu-id="cf59d-181">若要移動的資料大小範圍在 GB 或 TB 內，而且您想要獲得更好且可預期的效能輸送量，您通常會使用此選項。</span><span class="sxs-lookup"><span data-stu-id="cf59d-181">You would typically use this option when the data to be moved is in the range of gigabytes and terabytes, and you want better and predictable performance throughput.</span></span>

<span data-ttu-id="cf59d-182">若要使用您的 Data Lake Analytics 帳戶與 AdlCopy 從 Azure 儲存體 Blob 複製，必須將來源 (Azure 儲存體 Blob) 新增為您 Data Lake Analytics 帳戶的資料來源。</span><span class="sxs-lookup"><span data-stu-id="cf59d-182">To use your Data Lake Analytics account with AdlCopy to copy from an Azure Storage Blob, the source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span></span> <span data-ttu-id="cf59d-183">如需將其他資料來源加入至 Data Lake Analytics 帳戶的指示，請參閱[管理 Data Lake Analytics 帳戶資料來源](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)。</span><span class="sxs-lookup"><span data-stu-id="cf59d-183">For instructions on adding additional data sources to your Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).</span></span>

> [!NOTE]
> <span data-ttu-id="cf59d-184">如果您是使用 Data Lake Analytics 帳戶從做為來源的 Azure Data Lake Store 帳戶複製，則您不需將 Data Lake Store 帳戶與 Data Lake Analytics 帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cf59d-184">If you are copying from an Azure Data Lake Store account as the source using a Data Lake Analytics account, you do not need to associate the Data Lake Store account with the Data Lake Analytics account.</span></span> <span data-ttu-id="cf59d-185">當來源為 Azure 儲存體帳戶時，才需要將來源儲存體與 Data Lake Analytics 帳戶產生關聯。</span><span class="sxs-lookup"><span data-stu-id="cf59d-185">The requirement to associate the source store with the Data Lake Analytics account is only when the source is an Azure Storage account.</span></span>
>
>

<span data-ttu-id="cf59d-186">執行下列命令，使用 Data Lake Analytics 帳戶從 Azure 儲存體 Blob 複製到 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="cf59d-186">Run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

<span data-ttu-id="cf59d-187">例如：</span><span class="sxs-lookup"><span data-stu-id="cf59d-187">For example:</span></span>

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

<span data-ttu-id="cf59d-188">同樣地，執行下列命令，使用 Data Lake Analytics 帳戶從 Azure 儲存體 Blob 複製到 Data Lake Store 帳戶：</span><span class="sxs-lookup"><span data-stu-id="cf59d-188">Similarly, run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a><span data-ttu-id="cf59d-189">效能考量</span><span class="sxs-lookup"><span data-stu-id="cf59d-189">Performance considerations</span></span>

<span data-ttu-id="cf59d-190">複製 TB 規模的資料時，使用 AdlCopy 搭配您自己的 Azure Data Lake Analytics 帳戶可達到更好和更可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="cf59d-190">When copying data in the range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span></span> <span data-ttu-id="cf59d-191">應該調整的參數為用於複製作業的 Azure Data Lake Analytics 單位數目。</span><span class="sxs-lookup"><span data-stu-id="cf59d-191">The parameter that should be tuned is the number of Azure Data Lake Analytics Units to use for the copy job.</span></span> <span data-ttu-id="cf59d-192">增加單位數目可提高複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="cf59d-192">Increasing the number of units will increase the performance of your copy job.</span></span> <span data-ttu-id="cf59d-193">每個要複製的檔案最多可使用一個單位。</span><span class="sxs-lookup"><span data-stu-id="cf59d-193">Each file to be copied can use maximum one unit.</span></span> <span data-ttu-id="cf59d-194">指定的單位數目超過要複製的檔案數目時，將不會提高效能。</span><span class="sxs-lookup"><span data-stu-id="cf59d-194">Specifying more units than the number of files being copied will not increase performance.</span></span>

## <a name="use-adlcopy-to-copy-data-using-pattern-matching"></a><span data-ttu-id="cf59d-195">使用 AdlCopy 複製使用模式比對的資料</span><span class="sxs-lookup"><span data-stu-id="cf59d-195">Use AdlCopy to copy data using pattern matching</span></span>
<span data-ttu-id="cf59d-196">在本節中，您會了解如何使用 AdlCopy 將來源 (在我們使用 Azure 儲存體 Blob 的下列範例中) 的資料複製到使用模式比對的目的地 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf59d-196">In this section, you learn how to use AdlCopy to copy data from a source (in our example below we use Azure Storage Blob) to a destination Data Lake Store account using pattern matching.</span></span> <span data-ttu-id="cf59d-197">例如，您可以使用下列步驟將所有副檔名為 .csv 的檔案從來源 Blob 複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="cf59d-197">For example, you can use the steps below to copy all files with .csv extension from the source blob to the destination.</span></span>

1. <span data-ttu-id="cf59d-198">開啟命令提示字元，並瀏覽至安裝 AdlCopy 的目錄，通常是 `%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="cf59d-198">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="cf59d-199">執行下列命令，將所有副檔名為 .csv 的檔案從來源容器的特定 Blob 複製到 Data Lake Store：</span><span class="sxs-lookup"><span data-stu-id="cf59d-199">Run the following command to copy all files with *.csv extension from a specific blob from the source container to a Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    <span data-ttu-id="cf59d-200">例如：</span><span class="sxs-lookup"><span data-stu-id="cf59d-200">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a><span data-ttu-id="cf59d-201">計費</span><span class="sxs-lookup"><span data-stu-id="cf59d-201">Billing</span></span>
* <span data-ttu-id="cf59d-202">如果您獨立使用 AdlCopy 工具，而且如果來源 Azure 儲存體帳戶與 Data Lake Store 位於不同區域，則您將需支付移動資料的輸出成本。</span><span class="sxs-lookup"><span data-stu-id="cf59d-202">If you use the AdlCopy tool as standalone you will be billed for egress costs for moving data, if the source Azure Storage account is not in the same region as the Data Lake Store.</span></span>
* <span data-ttu-id="cf59d-203">如果您將 AdlCopy 工具與 Data Lake Analytics 帳戶搭配使用，即會套用標準的 [Data Lake Analytics 計費費率](https://azure.microsoft.com/pricing/details/data-lake-analytics/) 。</span><span class="sxs-lookup"><span data-stu-id="cf59d-203">If you use the AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span></span>

## <a name="considerations-for-using-adlcopy"></a><span data-ttu-id="cf59d-204">使用 AdlCopy 的考量</span><span class="sxs-lookup"><span data-stu-id="cf59d-204">Considerations for using AdlCopy</span></span>
* <span data-ttu-id="cf59d-205">AdlCopy (適用於 1.0.5 版) 支援從共同擁有超過數千個檔案和資料夾的來源複製資料。</span><span class="sxs-lookup"><span data-stu-id="cf59d-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span></span> <span data-ttu-id="cf59d-206">但是，如果您在複製大型資料集時發生問題，可將檔案/資料夾分散到不同的子資料夾，並改用這些子資料夾的路徑做為來源。</span><span class="sxs-lookup"><span data-stu-id="cf59d-206">However, if you encounter issues copying a large dataset, you can distribute the files/folders into different sub-folders and use the path to those sub-folders as the source instead.</span></span>

## <a name="performance-considerations-for-using-adlcopy"></a><span data-ttu-id="cf59d-207">使用 AdlCopy 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="cf59d-207">Performance considerations for using AdlCopy</span></span>

<span data-ttu-id="cf59d-208">AdlCopy 支援複製包含數千個檔案和資料夾的資料。</span><span class="sxs-lookup"><span data-stu-id="cf59d-208">AdlCopy supports copying data containing thousands of files and folders.</span></span> <span data-ttu-id="cf59d-209">不過，如果您在複製大型資料集時遇到問題，您可以將檔案/資料夾分散至較小的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="cf59d-209">However, if you encounter issues copying a large dataset, you can distribute the files/folders into smaller sub-folders.</span></span> <span data-ttu-id="cf59d-210">AdlCopy 適用於臨時複製。</span><span class="sxs-lookup"><span data-stu-id="cf59d-210">AdlCopy was built for ad hoc copies.</span></span> <span data-ttu-id="cf59d-211">如果您嘗試反覆地複製資料，請考慮使用 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)，它能夠完整地管理複製作業。</span><span class="sxs-lookup"><span data-stu-id="cf59d-211">If you are trying to copy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around the copy operations.</span></span>

## <a name="release-notes"></a><span data-ttu-id="cf59d-212">版本資訊</span><span class="sxs-lookup"><span data-stu-id="cf59d-212">Release notes</span></span>
* <span data-ttu-id="cf59d-213">1.0.13 - 如果您在多個 adlcopy 命令中將資料複製到相同的 Azure Data Lake Store 帳戶，則您每次執行時已不需要重新輸入認證。</span><span class="sxs-lookup"><span data-stu-id="cf59d-213">1.0.13 - If you are copying data to the same Azure Data Lake Store account across multiple adlcopy commands, you do not need to reenter your credentials for each run anymore.</span></span> <span data-ttu-id="cf59d-214">Adlcopy 現在會在多次執行之間快取該資訊。</span><span class="sxs-lookup"><span data-stu-id="cf59d-214">Adlcopy will now cache that information across multiple runs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf59d-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf59d-215">Next steps</span></span>
* [<span data-ttu-id="cf59d-216">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="cf59d-216">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="cf59d-217">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="cf59d-217">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="cf59d-218">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf59d-218">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
