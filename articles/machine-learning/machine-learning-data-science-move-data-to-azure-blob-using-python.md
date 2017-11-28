---
title: "從 Azure Blob 儲存體使用 Python aaaMove 資料 tooand |Microsoft 文件"
description: "移動資料 tooand 從 Azure Blob 儲存體使用 Python"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a><span data-ttu-id="fc05a-103">移動資料 tooand 從 Azure Blob 儲存體使用 Python</span><span class="sxs-lookup"><span data-stu-id="fc05a-103">Move data tooand from Azure Blob Storage using Python</span></span>
<span data-ttu-id="fc05a-104">本主題描述如何 toolist 上, 傳及下載 blob 使用 hello Python 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="fc05a-104">This topic describes how toolist, upload, and download blobs using hello Python API.</span></span> <span data-ttu-id="fc05a-105">以 hello Azure SDK 中提供的 Python API，您可以：</span><span class="sxs-lookup"><span data-stu-id="fc05a-105">With hello Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="fc05a-106">建立容器</span><span class="sxs-lookup"><span data-stu-id="fc05a-106">Create a container</span></span>
* <span data-ttu-id="fc05a-107">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="fc05a-107">Upload a blob into a container</span></span>
* <span data-ttu-id="fc05a-108">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="fc05a-108">Download blobs</span></span>
* <span data-ttu-id="fc05a-109">列出容器中的 hello blob</span><span class="sxs-lookup"><span data-stu-id="fc05a-109">List hello blobs in a container</span></span>
* <span data-ttu-id="fc05a-110">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="fc05a-110">Delete a blob</span></span>

<span data-ttu-id="fc05a-111">如需使用 hello Python 應用程式開發介面的詳細資訊，請參閱[tooUse hello 來自 Python 的 Blob 儲存體服務的方式](../storage/blobs/storage-python-how-to-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="fc05a-111">For more information about using hello Python API, see [How tooUse hello Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="fc05a-112">如果您要使用所提供的 hello 指令碼與設定的 VM [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)，然後 AzCopy hello VM 上已安裝。</span><span class="sxs-lookup"><span data-stu-id="fc05a-112">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="fc05a-113">完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="fc05a-113">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fc05a-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="fc05a-114">Prerequisites</span></span>
<span data-ttu-id="fc05a-115">本文件假設您有 Azure 訂用帳戶、 儲存體帳戶和該帳戶 hello 對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc05a-115">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="fc05a-116">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc05a-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="fc05a-117">tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="fc05a-117">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fc05a-118">如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="fc05a-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-tooblob"></a><span data-ttu-id="fc05a-119">上傳資料 tooBlob</span><span class="sxs-lookup"><span data-stu-id="fc05a-119">Upload Data tooBlob</span></span>
<span data-ttu-id="fc05a-120">加入下列程式碼片段，任何您想在其中 tooprogrammatically 存取 Azure 儲存體的 Python 程式碼的 hello 頂端附近的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc05a-120">Add hello following snippet near hello top of any Python code in which you wish tooprogrammatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="fc05a-121">hello **BlobService**物件可讓您使用容器和 blob。</span><span class="sxs-lookup"><span data-stu-id="fc05a-121">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="fc05a-122">下列程式碼的 hello 建立 BlobService 物件使用 hello 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc05a-122">hello following code creates a BlobService object using hello storage account name and account key.</span></span> <span data-ttu-id="fc05a-123">使用您真正的帳戶和金鑰來取代帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc05a-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="fc05a-124">使用下列方法 tooupload 資料 tooa blob hello:</span><span class="sxs-lookup"><span data-stu-id="fc05a-124">Use hello following methods tooupload data tooa blob:</span></span>

1. <span data-ttu-id="fc05a-125">put\_區塊\_blob\_從\_（上傳 hello 從 hello 指定路徑的檔案內容） 的路徑</span><span class="sxs-lookup"><span data-stu-id="fc05a-125">put\_block\_blob\_from\_path (uploads hello contents of a file from hello specified path)</span></span>
2. <span data-ttu-id="fc05a-126">put\_block_blob\_從\_（上傳已開啟的檔案/資料流中的 hello 內容） 的檔案</span><span class="sxs-lookup"><span data-stu-id="fc05a-126">put\_block_blob\_from\_file (uploads hello contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="fc05a-127">put\_block\_blob\_from\_bytes (上傳位元組陣列)</span><span class="sxs-lookup"><span data-stu-id="fc05a-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="fc05a-128">put\_區塊\_blob\_從\_文字 (上傳指定的 hello 使用 hello 文字值會指定編碼方式)</span><span class="sxs-lookup"><span data-stu-id="fc05a-128">put\_block\_blob\_from\_text (uploads hello specified text value using hello specified encoding)</span></span>

<span data-ttu-id="fc05a-129">下列範例程式碼的 hello 上傳本機檔案 tooa 容器：</span><span class="sxs-lookup"><span data-stu-id="fc05a-129">hello following sample code uploads a local file tooa container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="fc05a-130">hello 下列範例程式碼上傳所有 hello 檔 （不含目錄） 中的本機目錄 tooblob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="fc05a-130">hello following sample code uploads all hello files (excluding directories) in a local directory tooblob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="fc05a-131">從 Blob 下載資料</span><span class="sxs-lookup"><span data-stu-id="fc05a-131">Download Data from Blob</span></span>
<span data-ttu-id="fc05a-132">使用下列方法 toodownload 資料 blob 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc05a-132">Use hello following methods toodownload data from a blob:</span></span>

1. <span data-ttu-id="fc05a-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="fc05a-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="fc05a-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="fc05a-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="fc05a-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="fc05a-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="fc05a-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="fc05a-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="fc05a-137">執行 hello 所需區塊處理 hello hello 資料大小超過 64 MB 時，這些方法。</span><span class="sxs-lookup"><span data-stu-id="fc05a-137">These methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="fc05a-138">hello 下列範例程式碼下載 blob 容器 tooa 本機檔案中的 hello 的內容：</span><span class="sxs-lookup"><span data-stu-id="fc05a-138">hello following sample code downloads hello contents of a blob in a container tooa local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="fc05a-139">hello 下列範例程式碼會下載的所有 blob 的容器。</span><span class="sxs-lookup"><span data-stu-id="fc05a-139">hello following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="fc05a-140">它會使用清單\_tooget hello 份可用 hello 容器中 blob 的 blob，並將其下載 tooa 本機目錄。</span><span class="sxs-lookup"><span data-stu-id="fc05a-140">It uses list\_blobs tooget hello list of available blobs in hello container and downloads them tooa local directory.</span></span>

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
