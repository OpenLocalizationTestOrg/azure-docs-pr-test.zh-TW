---
title: "使用 Python 從 Azure Blob 儲存體來回移動資料 | Microsoft Docs"
description: "使用 Python 從 Azure Blob 儲存體來回移動資料"
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
ms.openlocfilehash: 0eea1ff8e4f4c1d108445e1a1250b6fa8ff48910
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-python"></a><span data-ttu-id="ed8bd-103">使用 Python 從 Azure Blob 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="ed8bd-103">Move data to and from Azure Blob Storage using Python</span></span>
<span data-ttu-id="ed8bd-104">本主題說明如何使用 Python API 列出、上傳及下載 Blob。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-104">This topic describes how to list, upload, and download blobs using the Python API.</span></span> <span data-ttu-id="ed8bd-105">使用 Azure SDK 中提供的 Python API，您可以</span><span class="sxs-lookup"><span data-stu-id="ed8bd-105">With the Python API provided in Azure SDK, you can:</span></span>

* <span data-ttu-id="ed8bd-106">建立容器</span><span class="sxs-lookup"><span data-stu-id="ed8bd-106">Create a container</span></span>
* <span data-ttu-id="ed8bd-107">將 Blob 上傳至容器</span><span class="sxs-lookup"><span data-stu-id="ed8bd-107">Upload a blob into a container</span></span>
* <span data-ttu-id="ed8bd-108">下載 Blob</span><span class="sxs-lookup"><span data-stu-id="ed8bd-108">Download blobs</span></span>
* <span data-ttu-id="ed8bd-109">列出容器中的 Blob</span><span class="sxs-lookup"><span data-stu-id="ed8bd-109">List the blobs in a container</span></span>
* <span data-ttu-id="ed8bd-110">刪除 Blob</span><span class="sxs-lookup"><span data-stu-id="ed8bd-110">Delete a blob</span></span>

<span data-ttu-id="ed8bd-111">如需使用 Python API 的詳細資訊，請參閱 [如何從 Python 使用 Blob 儲存體服務](../storage/blobs/storage-python-how-to-use-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-111">For more information about using the Python API, see [How to Use the Blob Storage Service from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="ed8bd-112">如果您是使用以 [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)提供的指令碼所設定的 VM，則 AzCopy 已經安裝在 VM 上。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-112">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ed8bd-113">如需 Azure Blob 儲存體的完整介紹，請參閱 [Azure Blob 基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和 [Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-113">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ed8bd-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="ed8bd-114">Prerequisites</span></span>
<span data-ttu-id="ed8bd-115">本文件假設您擁有 Azure 訂用帳戶、儲存體帳戶和該帳戶的對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-115">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="ed8bd-116">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-116">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="ed8bd-117">若要設定 Azure 訂用帳戶，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-117">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ed8bd-118">如需建立儲存體帳戶以及取得帳戶和金鑰資訊的指示，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-118">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="upload-data-to-blob"></a><span data-ttu-id="ed8bd-119">將資料上傳至 Blob</span><span class="sxs-lookup"><span data-stu-id="ed8bd-119">Upload Data to Blob</span></span>
<span data-ttu-id="ed8bd-120">將下列程式碼片段新增至您希望以程式設計方式存取 Azure 儲存體的任何 Python 程式碼頂端附近：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-120">Add the following snippet near the top of any Python code in which you wish to programmatically access Azure Storage:</span></span>

    from azure.storage.blob import BlobService

<span data-ttu-id="ed8bd-121">**BlobService** 物件讓您能使用容器及 blob。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-121">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ed8bd-122">下列程式碼會使用儲存體帳戶名稱和帳戶金鑰來建立 BlobService 物件。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-122">The following code creates a BlobService object using the storage account name and account key.</span></span> <span data-ttu-id="ed8bd-123">使用您真正的帳戶和金鑰來取代帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-123">Replace account name and account key with your real account and key.</span></span>

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

<span data-ttu-id="ed8bd-124">使用下列方法，將資料上傳至 Blob：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-124">Use the following methods to upload data to a blob:</span></span>

1. <span data-ttu-id="ed8bd-125">put\_block\_blob\_from\_path (從指定路徑上傳檔案的內容)</span><span class="sxs-lookup"><span data-stu-id="ed8bd-125">put\_block\_blob\_from\_path (uploads the contents of a file from the specified path)</span></span>
2. <span data-ttu-id="ed8bd-126">put\_block_blob\_from\_file (從任何已經開啟的檔案/資料流上傳內容)</span><span class="sxs-lookup"><span data-stu-id="ed8bd-126">put\_block_blob\_from\_file (uploads the contents from an already opened file/stream)</span></span>
3. <span data-ttu-id="ed8bd-127">put\_block\_blob\_from\_bytes (上傳位元組陣列)</span><span class="sxs-lookup"><span data-stu-id="ed8bd-127">put\_block\_blob\_from\_bytes (uploads an array of bytes)</span></span>
4. <span data-ttu-id="ed8bd-128">put\_block\_blob\_from\_text (使用指定的編碼方式上傳指定的文字值)</span><span class="sxs-lookup"><span data-stu-id="ed8bd-128">put\_block\_blob\_from\_text (uploads the specified text value using the specified encoding)</span></span>

<span data-ttu-id="ed8bd-129">下列程式碼範例會將本機檔案上傳至容器：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-129">The following sample code uploads a local file to a container:</span></span>

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ed8bd-130">下列程式碼範例會將本機目錄中的所有檔案 (不含目錄) 上傳至 Blob 儲存體：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-130">The following sample code uploads all the files (excluding directories) in a local directory to blob storage:</span></span>

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in the LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading the data %s"%blob_name


## <a name="download-data-from-blob"></a><span data-ttu-id="ed8bd-131">從 Blob 下載資料</span><span class="sxs-lookup"><span data-stu-id="ed8bd-131">Download Data from Blob</span></span>
<span data-ttu-id="ed8bd-132">使用下列方法，從 Blob 下載資料：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-132">Use the following methods to download data from a blob:</span></span>

1. <span data-ttu-id="ed8bd-133">get\_blob\_to\_path</span><span class="sxs-lookup"><span data-stu-id="ed8bd-133">get\_blob\_to\_path</span></span>
2. <span data-ttu-id="ed8bd-134">get\_blob\_to\_file</span><span class="sxs-lookup"><span data-stu-id="ed8bd-134">get\_blob\_to\_file</span></span>
3. <span data-ttu-id="ed8bd-135">get\_blob\_to\_bytes</span><span class="sxs-lookup"><span data-stu-id="ed8bd-135">get\_blob\_to\_bytes</span></span>
4. <span data-ttu-id="ed8bd-136">get\_blob\_to\_text</span><span class="sxs-lookup"><span data-stu-id="ed8bd-136">get\_blob\_to\_text</span></span>

<span data-ttu-id="ed8bd-137">這些方法可以在資料大小超過 64 MB 時執行必要的區塊化動作。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-137">These methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="ed8bd-138">下列程式碼範例會將容器中 Blob 的內容下載至本機檔案：</span><span class="sxs-lookup"><span data-stu-id="ed8bd-138">The following sample code downloads the contents of a blob in a container to a local file:</span></span>

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

<span data-ttu-id="ed8bd-139">下列程式碼範例會從容器下載所有 Blob。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-139">The following sample code downloads all blobs from a container.</span></span> <span data-ttu-id="ed8bd-140">它會使用 list\_blobs 來取得容器中可用的 Blob 清單，並將它們下載至本機目錄。</span><span class="sxs-lookup"><span data-stu-id="ed8bd-140">It uses list\_blobs to get the list of available blobs in the container and downloads them to a local directory.</span></span>

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
            print "something wrong happened when downloading the data %s"%blob.name
