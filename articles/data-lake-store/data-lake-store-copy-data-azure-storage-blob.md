---
title: "從 Azure 資料湖存放區的儲存體 Blob aaaCopy 資料 |Microsoft 文件"
description: "使用 AdlCopy 工具 toocopy 資料從 Azure 儲存體 Blob tooData 湖存放區"
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
ms.openlocfilehash: a3d4172eaefe7395cdef2fff72691bd70f642b78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-from-azure-storage-blobs-toodata-lake-store"></a><span data-ttu-id="3e5e7-103">從 Azure 儲存體 Blob tooData 湖存放區複製資料</span><span class="sxs-lookup"><span data-stu-id="3e5e7-103">Copy data from Azure Storage Blobs tooData Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e5e7-104">使用 DistCp</span><span class="sxs-lookup"><span data-stu-id="3e5e7-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="3e5e7-105">使用 AdlCopy</span><span class="sxs-lookup"><span data-stu-id="3e5e7-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="3e5e7-106">Azure Data Lake Store 提供的命令列工具， [AdlCopy](http://aka.ms/downloadadlcopy)，從下列來源的 hello toocopy 資料：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), toocopy data from hello following sources:</span></span>

* <span data-ttu-id="3e5e7-107">從 Azure 儲存體 Blob 複製到 Data Lake Store 中。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-107">From Azure Storage Blobs into Data Lake Store.</span></span> <span data-ttu-id="3e5e7-108">您無法使用 AdlCopy toocopy Data Lake Store tooAzure 儲存體 blob 資料。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-108">You cannot use AdlCopy toocopy data from Data Lake Store tooAzure Storage blobs.</span></span>
* <span data-ttu-id="3e5e7-109">兩個 Azure Data Lake Store 帳戶之間。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-109">Between two Azure Data Lake Store accounts.</span></span>

<span data-ttu-id="3e5e7-110">此外，您可以使用 hello AdlCopy 工具在兩個不同的模式：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-110">Also, you can use hello AdlCopy tool in two different modes:</span></span>

* <span data-ttu-id="3e5e7-111">**獨立**，其中 hello 工具會使用 Data Lake Store 資源 tooperform hello 工作。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-111">**Standalone**, where hello tool uses Data Lake Store resources tooperform hello task.</span></span>
* <span data-ttu-id="3e5e7-112">**使用 Data Lake Analytics 帳戶**，其中 hello 單位 tooyour Data Lake Analytics 帳戶指派給使用的 tooperform hello 複製作業。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-112">**Using a Data Lake Analytics account**, where hello units assigned tooyour Data Lake Analytics account are used tooperform hello copy operation.</span></span> <span data-ttu-id="3e5e7-113">當您以預期的方式搜尋 tooperform hello 複製工作時您可能想指定 toouse 此選項。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-113">You might want toouse this option when you are looking tooperform hello copy tasks in a predictable manner.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e5e7-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="3e5e7-114">Prerequisites</span></span>
<span data-ttu-id="3e5e7-115">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-115">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="3e5e7-116">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-116">**An Azure subscription**.</span></span> <span data-ttu-id="3e5e7-117">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3e5e7-118">**Azure 儲存體 Blob** 容器 (其中含有一些資料)。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-118">**Azure Storage Blobs** container with some data.</span></span>
* <span data-ttu-id="3e5e7-119">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="3e5e7-120">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3e5e7-120">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="3e5e7-121">**Azure Data Lake Analytics 帳戶 （選擇性）** -請參閱[開始使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)指示如何 toocreate 資料湖存放區的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how toocreate a Data Lake Store account.</span></span>
* <span data-ttu-id="3e5e7-122">**AdlCopy 工具**。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-122">**AdlCopy tool**.</span></span> <span data-ttu-id="3e5e7-123">安裝從 hello AdlCopy 工具[http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy)。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-123">Install hello AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span></span>

## <a name="syntax-of-hello-adlcopy-tool"></a><span data-ttu-id="3e5e7-124">Hello AdlCopy 工具語法</span><span class="sxs-lookup"><span data-stu-id="3e5e7-124">Syntax of hello AdlCopy tool</span></span>
<span data-ttu-id="3e5e7-125">使用下列語法 toowork hello AdlCopy 工具與 hello</span><span class="sxs-lookup"><span data-stu-id="3e5e7-125">Use hello following syntax toowork with hello AdlCopy tool</span></span>

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern

<span data-ttu-id="3e5e7-126">hello 語法中的 hello 參數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-126">hello parameters in hello syntax are described below:</span></span>

| <span data-ttu-id="3e5e7-127">選項</span><span class="sxs-lookup"><span data-stu-id="3e5e7-127">Option</span></span> | <span data-ttu-id="3e5e7-128">說明</span><span class="sxs-lookup"><span data-stu-id="3e5e7-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3e5e7-129">來源</span><span class="sxs-lookup"><span data-stu-id="3e5e7-129">Source</span></span> |<span data-ttu-id="3e5e7-130">指定 hello Azure 儲存體 blob 中的 hello hello 來源資料的位置。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-130">Specifies hello location of hello source data in hello Azure storage blob.</span></span> <span data-ttu-id="3e5e7-131">hello 來源可以是 blob 容器、 blob 或另一個 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-131">hello source can be a blob container, a blob, or another Data Lake Store account.</span></span> |
| <span data-ttu-id="3e5e7-132">Dest</span><span class="sxs-lookup"><span data-stu-id="3e5e7-132">Dest</span></span> |<span data-ttu-id="3e5e7-133">指定要 hello Data Lake Store 目的地 toocopy。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-133">Specifies hello Data Lake Store destination toocopy to.</span></span> |
| <span data-ttu-id="3e5e7-134">SourceKey</span><span class="sxs-lookup"><span data-stu-id="3e5e7-134">SourceKey</span></span> |<span data-ttu-id="3e5e7-135">指定 hello hello Azure 儲存體 blob 來源的儲存體存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-135">Specifies hello storage access key for hello Azure storage blob source.</span></span> <span data-ttu-id="3e5e7-136">這是必要的只有 hello 來源 blob 容器或 blob。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-136">This is required only if hello source is a blob container or a blob.</span></span> |
| <span data-ttu-id="3e5e7-137">帳戶</span><span class="sxs-lookup"><span data-stu-id="3e5e7-137">Account</span></span> |<span data-ttu-id="3e5e7-138">**選用**。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-138">**Optional**.</span></span> <span data-ttu-id="3e5e7-139">如果您想 toouse Azure Data Lake Analytics 帳戶 toorun hello 複製作業，請使用此選項。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-139">Use this if you want toouse Azure Data Lake Analytics account toorun hello copy job.</span></span> <span data-ttu-id="3e5e7-140">如果您在 hello 語法中使用 hello /Account 選項但未指定 Data Lake Analytics 帳戶，AdlCopy 會使用預設帳戶 toorun hello 工作。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-140">If you use hello /Account option in hello syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account toorun hello job.</span></span> <span data-ttu-id="3e5e7-141">此外，如果您使用此選項時，您必須加入 hello 來源 (Azure 儲存體 Blob) 和目的地 （Azure 資料湖存放區） 做為資料來源資料湖分析帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-141">Also, if you use this option, you must add hello source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span></span> |
| <span data-ttu-id="3e5e7-142">Units</span><span class="sxs-lookup"><span data-stu-id="3e5e7-142">Units</span></span> |<span data-ttu-id="3e5e7-143">指定將用於 hello 複製作業的 Data Lake Analytics 單位的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-143">Specifies hello number of Data Lake Analytics units that will be used for hello copy job.</span></span> <span data-ttu-id="3e5e7-144">這個選項會強制，如果您使用 hello **/帳戶**選項 toospecify hello Data Lake Analytics 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-144">This option is mandatory if you use hello **/Account** option toospecify hello Data Lake Analytics account.</span></span> |
| <span data-ttu-id="3e5e7-145">模式</span><span class="sxs-lookup"><span data-stu-id="3e5e7-145">Pattern</span></span> |<span data-ttu-id="3e5e7-146">指定指出哪些 blob 或檔案 toocopy regex 模式。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-146">Specifies a regex pattern that indicates which blobs or files toocopy.</span></span> <span data-ttu-id="3e5e7-147">AdlCopy 使用區分大小寫的比對。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-147">AdlCopy uses case-sensitive matching.</span></span> <span data-ttu-id="3e5e7-148">所有項目 toocopy 不指定任何模式時，使用 hello 預設模式。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-148">hello default pattern used when no pattern is specified is toocopy all items.</span></span> <span data-ttu-id="3e5e7-149">不支援指定多個檔案模式。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-149">Specifying multiple file patterns is not supported.</span></span> |

## <a name="use-adlcopy-as-standalone-toocopy-data-from-an-azure-storage-blob"></a><span data-ttu-id="3e5e7-150">使用 （做為獨立） AdlCopy toocopy 資料從 Azure 儲存體 blob</span><span class="sxs-lookup"><span data-stu-id="3e5e7-150">Use AdlCopy (as standalone) toocopy data from an Azure Storage blob</span></span>
1. <span data-ttu-id="3e5e7-151">開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-151">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="3e5e7-152">從 hello 來源容器 tooa 資料湖存放區執行下列命令 toocopy hello 特定的 blob:</span><span class="sxs-lookup"><span data-stu-id="3e5e7-152">Run hello following command toocopy a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    <span data-ttu-id="3e5e7-153">例如：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-153">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] <span data-ttu-id="3e5e7-154">hello 上述語法指定 hello 檔案 toobe 複製的 tooa 資料夾 hello Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-154">hello syntax above specifies hello file toobe copied tooa folder in hello Data Lake Store account.</span></span> <span data-ttu-id="3e5e7-155">如果 hello 指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-155">AdlCopy tool creates a folder if hello specified folder name does not exist.</span></span>

    <span data-ttu-id="3e5e7-156">您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-156">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="3e5e7-157">您會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-157">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. <span data-ttu-id="3e5e7-158">您也可以複製所有 hello blob 從某個容器 toohello Data Lake Store 帳戶使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-158">You can also copy all hello blobs from one container toohello Data Lake Store account using hello following command:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        

    <span data-ttu-id="3e5e7-159">例如：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-159">For example:</span></span>

        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a><span data-ttu-id="3e5e7-160">效能考量</span><span class="sxs-lookup"><span data-stu-id="3e5e7-160">Performance considerations</span></span>

<span data-ttu-id="3e5e7-161">如果您要從 Azure Blob 儲存體帳戶複製，您可能會節流處理 hello blob 儲存體端複製期間。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on hello blob storage side.</span></span> <span data-ttu-id="3e5e7-162">這會降低 hello 的複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-162">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="3e5e7-163">toolearn 進一步了解 hello 限制的 Azure Blob 儲存體，請參閱 < 在 Azure 儲存體限制[Azure 訂用帳戶和服務限制](../azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-163">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="use-adlcopy-as-standalone-toocopy-data-from-another-data-lake-store-account"></a><span data-ttu-id="3e5e7-164">使用從另一個 Data Lake Store 帳戶 （做為獨立） AdlCopy toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="3e5e7-164">Use AdlCopy (as standalone) toocopy data from another Data Lake Store account</span></span>
<span data-ttu-id="3e5e7-165">您也可以使用兩個 Data Lake Store 帳戶之間 AdlCopy toocopy 資料。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-165">You can also use AdlCopy toocopy data between two Data Lake Store accounts.</span></span>

1. <span data-ttu-id="3e5e7-166">開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-166">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="3e5e7-167">從一個 Data Lake Store 帳戶 tooanother 執行下列命令 toocopy hello 特定檔案。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-167">Run hello following command toocopy a specific file from one Data Lake Store account tooanother.</span></span>

        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/

    <span data-ttu-id="3e5e7-168">例如：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-168">For example:</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

   > [!NOTE]
   > <span data-ttu-id="3e5e7-169">hello 上述語法指定 hello 檔案 toobe 複製的 tooa 資料夾 hello 目的地 Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-169">hello syntax above specifies hello file toobe copied tooa folder in hello destination Data Lake Store account.</span></span> <span data-ttu-id="3e5e7-170">如果 hello 指定的資料夾名稱不存在，AdlCopy 工具會建立一個資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-170">AdlCopy tool creates a folder if hello specified folder name does not exist.</span></span>
   >
   >

    <span data-ttu-id="3e5e7-171">您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-171">You will be prompted tooenter hello credentials for hello Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="3e5e7-172">您會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-172">You will see an output similar toohello following:</span></span>

        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. <span data-ttu-id="3e5e7-173">hello 下列命令會將所有檔案從特定資料夾中的資料夾 hello 來源 Data Lake Store 帳戶 tooa hello 目的地 Data Lake Store 帳戶中。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-173">hello following command copies all files from a specific folder in hello source Data Lake Store account tooa folder in hello destination Data Lake Store account.</span></span>

        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a><span data-ttu-id="3e5e7-174">效能考量</span><span class="sxs-lookup"><span data-stu-id="3e5e7-174">Performance considerations</span></span>

<span data-ttu-id="3e5e7-175">當使用 AdlCopy 做為獨立的工具，hello 複本上執行共用，Azure 受管理資源。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-175">When using AdlCopy as a standalone tool, hello copy is run on shared, Azure managed resources.</span></span> <span data-ttu-id="3e5e7-176">在此環境中，您可能會收到 hello 效能取決於系統負載，以及可用資源。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-176">hello performance you may get in this environment depends on system load and available resources.</span></span> <span data-ttu-id="3e5e7-177">這個模式最適合臨時的少量傳輸。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-177">This mode is best used for small transfers on an ad hoc basis.</span></span> <span data-ttu-id="3e5e7-178">沒有參數需要 toobe 微調時使用 AdlCopy 當作獨立的工具。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-178">No parameters need toobe tuned when using AdlCopy as a standalone tool.</span></span>

## <a name="use-adlcopy-with-data-lake-analytics-account-toocopy-data"></a><span data-ttu-id="3e5e7-179">使用 （與資料湖分析帳戶） AdlCopy toocopy 資料</span><span class="sxs-lookup"><span data-stu-id="3e5e7-179">Use AdlCopy (with Data Lake Analytics account) toocopy data</span></span>
<span data-ttu-id="3e5e7-180">您也可以使用您的資料湖分析帳戶 toorun hello AdlCopy 作業 toocopy 資料從 Azure 儲存體 blob tooData 湖存放區。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-180">You can also use your Data Lake Analytics account toorun hello AdlCopy job toocopy data from Azure storage blobs tooData Lake Store.</span></span> <span data-ttu-id="3e5e7-181">移動 hello 資料 toobe 位於 hello 範圍 gb 和 tb，而且您想更佳且可預測的效能輸送量時，通常會使用此選項。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-181">You would typically use this option when hello data toobe moved is in hello range of gigabytes and terabytes, and you want better and predictable performance throughput.</span></span>

<span data-ttu-id="3e5e7-182">toouse 您 AdlCopy toocopy 從 Azure 儲存體 Blob hello 來源 (Azure 儲存體 Blob) 的資料湖分析帳戶必須新增為您的 Data Lake Analytics 帳戶的資料來源。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-182">toouse your Data Lake Analytics account with AdlCopy toocopy from an Azure Storage Blob, hello source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span></span> <span data-ttu-id="3e5e7-183">如需加入額外的資料來源 tooyour Data Lake Analytics 帳戶的指示，請參閱[管理 Data Lake Analytics 帳戶的資料來源](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources)。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-183">For instructions on adding additional data sources tooyour Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-data-sources).</span></span>

> [!NOTE]
> <span data-ttu-id="3e5e7-184">如果您要從 Azure Data Lake Store 帳戶複製為 hello 來源使用 Data Lake Analytics 帳戶，您不需要以 hello Data Lake Analytics 帳戶 tooassociate hello Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-184">If you are copying from an Azure Data Lake Store account as hello source using a Data Lake Analytics account, you do not need tooassociate hello Data Lake Store account with hello Data Lake Analytics account.</span></span> <span data-ttu-id="3e5e7-185">hello 需求 tooassociate hello 來源存放區以 hello Data Lake Analytics 帳戶是只當 hello 來源是 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-185">hello requirement tooassociate hello source store with hello Data Lake Analytics account is only when hello source is an Azure Storage account.</span></span>
>
>

<span data-ttu-id="3e5e7-186">執行使用 Data Lake Analytics 帳戶的 Azure 儲存體 blob tooa Data Lake Store 帳戶中的下列命令 toocopy hello:</span><span class="sxs-lookup"><span data-stu-id="3e5e7-186">Run hello following command toocopy from an Azure Storage blob tooa Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

<span data-ttu-id="3e5e7-187">例如：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-187">For example:</span></span>

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

<span data-ttu-id="3e5e7-188">同樣地，執行使用 Data Lake Analytics 帳戶的 Azure 儲存體 blob tooa Data Lake Store 帳戶中的下列命令 toocopy hello:</span><span class="sxs-lookup"><span data-stu-id="3e5e7-188">Similarly, run hello following command toocopy from an Azure Storage blob tooa Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a><span data-ttu-id="3e5e7-189">效能考量</span><span class="sxs-lookup"><span data-stu-id="3e5e7-189">Performance considerations</span></span>

<span data-ttu-id="3e5e7-190">複製資料時的 tb hello 範圍中，使用您自己的 Azure Data Lake Analytics 帳戶中使用 AdlCopy 提供更好且更可預測的效能。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-190">When copying data in hello range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span></span> <span data-ttu-id="3e5e7-191">hello Azure 資料湖分析單位 toouse hello 複製作業的數目應微調的 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-191">hello parameter that should be tuned is hello number of Azure Data Lake Analytics Units toouse for hello copy job.</span></span> <span data-ttu-id="3e5e7-192">增加 hello 單元數目會增加 hello 的複製作業的效能。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-192">Increasing hello number of units will increase hello performance of your copy job.</span></span> <span data-ttu-id="3e5e7-193">複製每個檔案 toobe 可以使用最大的一個單位。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-193">Each file toobe copied can use maximum one unit.</span></span> <span data-ttu-id="3e5e7-194">指定多個單位 hello 複製的檔案數目，將不會增加效能。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-194">Specifying more units than hello number of files being copied will not increase performance.</span></span>

## <a name="use-adlcopy-toocopy-data-using-pattern-matching"></a><span data-ttu-id="3e5e7-195">使用 AdlCopy toocopy 資料使用模式比對</span><span class="sxs-lookup"><span data-stu-id="3e5e7-195">Use AdlCopy toocopy data using pattern matching</span></span>
<span data-ttu-id="3e5e7-196">在本節中，您學會如何 toouse AdlCopy toocopy 資料來源 （在下列範例中我們使用 Azure 儲存體 Blob） 使用模式比對 tooa 目的地 Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-196">In this section, you learn how toouse AdlCopy toocopy data from a source (in our example below we use Azure Storage Blob) tooa destination Data Lake Store account using pattern matching.</span></span> <span data-ttu-id="3e5e7-197">比方說，您可以使用下列 toocopy hello 步驟是所有檔案從 hello 來源 blob toohello 目的地.csv 副檔名。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-197">For example, you can use hello steps below toocopy all files with .csv extension from hello source blob toohello destination.</span></span>

1. <span data-ttu-id="3e5e7-198">開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-198">Open a command prompt and navigate toohello directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="3e5e7-199">執行下列命令 toocopy hello 所有檔案 *.csv 副檔名 hello 來源容器 tooa 資料湖存放區中的特定 blob:</span><span class="sxs-lookup"><span data-stu-id="3e5e7-199">Run hello following command toocopy all files with *.csv extension from a specific blob from hello source container tooa Data Lake Store:</span></span>

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv

    <span data-ttu-id="3e5e7-200">例如：</span><span class="sxs-lookup"><span data-stu-id="3e5e7-200">For example:</span></span>

        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a><span data-ttu-id="3e5e7-201">計費</span><span class="sxs-lookup"><span data-stu-id="3e5e7-201">Billing</span></span>
* <span data-ttu-id="3e5e7-202">如果輸出成本來移動使用 hello AdlCopy 工具以在將予計費的獨立伺服器資料，如果 hello 來源 Azure 儲存體帳戶不在 hello 相同的區域，因為 hello 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-202">If you use hello AdlCopy tool as standalone you will be billed for egress costs for moving data, if hello source Azure Storage account is not in hello same region as hello Data Lake Store.</span></span>
* <span data-ttu-id="3e5e7-203">如果您使用 hello AdlCopy 工具與您的 Data Lake Analytics 帳戶，標準[Data Lake Analytics 計費費率](https://azure.microsoft.com/pricing/details/data-lake-analytics/)會套用。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-203">If you use hello AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span></span>

## <a name="considerations-for-using-adlcopy"></a><span data-ttu-id="3e5e7-204">使用 AdlCopy 的考量</span><span class="sxs-lookup"><span data-stu-id="3e5e7-204">Considerations for using AdlCopy</span></span>
* <span data-ttu-id="3e5e7-205">AdlCopy (適用於 1.0.5 版) 支援從共同擁有超過數千個檔案和資料夾的來源複製資料。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span></span> <span data-ttu-id="3e5e7-206">不過，如果您遇到複製大型資料集的問題，您可以在於 hello 檔案/資料夾分散到不同的子資料夾，並為 hello 來源改用 hello 路徑 toothose 子資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-206">However, if you encounter issues copying a large dataset, you can distribute hello files/folders into different sub-folders and use hello path toothose sub-folders as hello source instead.</span></span>

## <a name="performance-considerations-for-using-adlcopy"></a><span data-ttu-id="3e5e7-207">使用 AdlCopy 時的效能考量</span><span class="sxs-lookup"><span data-stu-id="3e5e7-207">Performance considerations for using AdlCopy</span></span>

<span data-ttu-id="3e5e7-208">AdlCopy 支援複製包含數千個檔案和資料夾的資料。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-208">AdlCopy supports copying data containing thousands of files and folders.</span></span> <span data-ttu-id="3e5e7-209">不過，如果您遇到複製大型資料集的問題，您可以將 hello 檔案/資料夾發佈成較小的子資料夾。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-209">However, if you encounter issues copying a large dataset, you can distribute hello files/folders into smaller sub-folders.</span></span> <span data-ttu-id="3e5e7-210">AdlCopy 適用於臨時複製。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-210">AdlCopy was built for ad hoc copies.</span></span> <span data-ttu-id="3e5e7-211">如果您嘗試以週期性 toocopy 資料，您應該考慮使用[Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)提供周圍 hello 複製作業的完整管理。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-211">If you are trying toocopy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around hello copy operations.</span></span>

## <a name="release-notes"></a><span data-ttu-id="3e5e7-212">版本資訊</span><span class="sxs-lookup"><span data-stu-id="3e5e7-212">Release notes</span></span>
* <span data-ttu-id="3e5e7-213">1.0.13-如果您要複製資料 toohello 相同的 Azure Data Lake Store 帳戶跨多個 adlcopy 命令，您不需要再執行您的認證，針對每個 tooreenter。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-213">1.0.13 - If you are copying data toohello same Azure Data Lake Store account across multiple adlcopy commands, you do not need tooreenter your credentials for each run anymore.</span></span> <span data-ttu-id="3e5e7-214">Adlcopy 現在會在多次執行之間快取該資訊。</span><span class="sxs-lookup"><span data-stu-id="3e5e7-214">Adlcopy will now cache that information across multiple runs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e5e7-215">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e5e7-215">Next steps</span></span>
* [<span data-ttu-id="3e5e7-216">保護 Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="3e5e7-216">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="3e5e7-217">搭配 Data Lake Store 使用 Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3e5e7-217">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3e5e7-218">搭配 Data Lake Store 使用 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e5e7-218">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
