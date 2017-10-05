---
title: "使用 AzCopy 從 Azure Blob 儲存體來回移動資料 | Microsoft Docs"
description: "使用 AzCopy 從 Azure Blob 儲存體來回移動資料"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: a41ccdd5739a5b10cef201910abd639ae3126c02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="a9d04-103">使用 AzCopy 從 Azure Blob 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="a9d04-103">Move data to and from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="a9d04-104">AzCopy 是個命令列公用程式，專為上傳、下載，以及將資料複製到和複製出 Microsoft Azure Blob、檔案和表格儲存體所設計。</span><span class="sxs-lookup"><span data-stu-id="a9d04-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data to and from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="a9d04-105">如需安裝 AzCopy 的指示，和以 Azure 平台加以執行的其他資訊，請參閱 [開始使用 AzCopy 命令列公用程式](../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="a9d04-105">For instructions on installing AzCopy and additional information on using it with the Azure platform, see [Getting Started with the AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="a9d04-106">如果您是使用以 [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)提供的指令碼所設定的 VM，則 AzCopy 已經安裝在 VM 上。</span><span class="sxs-lookup"><span data-stu-id="a9d04-106">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="a9d04-107">如需 Azure Blob 儲存體的完整介紹，請參閱 [Azure Blob 基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和 [Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a9d04-107">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and to [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a9d04-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="a9d04-108">Prerequisites</span></span>
<span data-ttu-id="a9d04-109">本文件假設您擁有 Azure 訂用帳戶、儲存體帳戶和該帳戶的對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="a9d04-109">This document assumes that you have an Azure subscription, a storage account and the corresponding storage key for that account.</span></span> <span data-ttu-id="a9d04-110">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="a9d04-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="a9d04-111">若要設定 Azure 訂用帳戶，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a9d04-111">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a9d04-112">如需建立儲存體帳戶以及取得帳戶和金鑰資訊的指示，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="a9d04-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="a9d04-113">執行 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="a9d04-113">Run AzCopy commands</span></span>
<span data-ttu-id="a9d04-114">若要執行 AzCopy 命令，請開啟命令視窗並瀏覽至電腦上的 AzCopy 安裝目錄，也就是 AzCopy.exe 可執行檔的所在位置。</span><span class="sxs-lookup"><span data-stu-id="a9d04-114">To run AzCopy commands, open a command window and navigate to the AzCopy installation directory on your computer, where the AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="a9d04-115">AzCopy 命令的基本語法是：</span><span class="sxs-lookup"><span data-stu-id="a9d04-115">The basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="a9d04-116">您可以將 AzCopy 安裝位置新增到系統路徑，然後從任何目錄執行命令。</span><span class="sxs-lookup"><span data-stu-id="a9d04-116">You can add the AzCopy installation location to your system path and then run the commands from any directory.</span></span> <span data-ttu-id="a9d04-117">根據預設，AzCopy 會安裝到 *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* 或 *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*。</span><span class="sxs-lookup"><span data-stu-id="a9d04-117">By default, AzCopy is installed to *%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-to-an-azure-blob"></a><span data-ttu-id="a9d04-118">將檔案上傳至 Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a9d04-118">Upload files to an Azure blob</span></span>
<span data-ttu-id="a9d04-119">若要上傳檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a9d04-119">To upload a file, use the following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="a9d04-120">從 Azure Blob 下載檔案</span><span class="sxs-lookup"><span data-stu-id="a9d04-120">Download files from an Azure blob</span></span>
<span data-ttu-id="a9d04-121">若要從 Azure Blob 下載檔案，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a9d04-121">To download a file from an Azure blob, use the following command:</span></span>

    # Downloading blobs to local file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="a9d04-122">在 Azure 容器之間傳輸 Blob</span><span class="sxs-lookup"><span data-stu-id="a9d04-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="a9d04-123">若要在 Azure 容器之間傳輸 Blob，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="a9d04-123">To transfer blobs between Azure containers, use the following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: the sub directory in the container
    <your_local_directory>: directory of local file system where files to be uploaded from or the directory of local file system files to be downloaded to
    <file_pattern>: pattern of file names to be transferred. The standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="a9d04-124">使用 AzCopy 的秘訣</span><span class="sxs-lookup"><span data-stu-id="a9d04-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="a9d04-125">**上傳**檔案時，*/S* 將以遞迴方式上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="a9d04-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="a9d04-126">如果沒有這個參數，則不會上傳子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a9d04-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="a9d04-127">**下載**檔案時，*/S* 將以遞迴方式搜尋容器，直到下載了指定目錄及其子目錄中的所有檔案，或指定目錄及其子目錄中所有符合指定模式的所有檔案為止。</span><span class="sxs-lookup"><span data-stu-id="a9d04-127">When **downloading** file, */S* searches the container recursively until all files in the specified directory and its subdirectories, or all files that match the specified pattern in the given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="a9d04-128">您無法使用 /Source  參數來指定要下載的 *特定 Blob 檔案* 。</span><span class="sxs-lookup"><span data-stu-id="a9d04-128">You cannot specify a **specific blob file** to download using the */Source* parameter.</span></span> <span data-ttu-id="a9d04-129">若要下載特定檔案，請使用 /Pattern  參數指定要下載的 Blob 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="a9d04-129">To download a specific file, specify the blob file name to download using the */Pattern* parameter.</span></span> <span data-ttu-id="a9d04-130">**/S** 參數可用來讓 AzCopy 以遞迴方式尋找檔案名稱模式。</span><span class="sxs-lookup"><span data-stu-id="a9d04-130">**/S** parameter can be used to have AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="a9d04-131">若未提供模式參數，AzCopy 會下載該目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="a9d04-131">Without the pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

