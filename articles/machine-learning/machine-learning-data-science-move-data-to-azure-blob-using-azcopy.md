---
title: "從 Azure Blob 儲存體，使用 AzCopy aaaMove 資料 tooand |Microsoft 文件"
description: "從 Azure Blob 儲存體，使用 AzCopy 移動資料 tooand"
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
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a><span data-ttu-id="26b52-103">從 Azure Blob 儲存體，使用 AzCopy 移動資料 tooand</span><span class="sxs-lookup"><span data-stu-id="26b52-103">Move data tooand from Azure Blob Storage using AzCopy</span></span>
<span data-ttu-id="26b52-104">AzCopy 是上傳、 下載和複製資料 tooand 從 Microsoft Azure blob、 檔案和資料表儲存體設計的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="26b52-104">AzCopy is a command-line utility designed for uploading, downloading, and copying data tooand from Microsoft Azure blob, file, and table storage.</span></span>

<span data-ttu-id="26b52-105">如需使用以 hello Azure 平台上安裝 AzCopy 和其他資訊的指示，請參閱[開始使用 AzCopy 命令列公用程式的 hello](../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="26b52-105">For instructions on installing AzCopy and additional information on using it with hello Azure platform, see [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="26b52-106">如果您要使用所提供的 hello 指令碼與設定的 VM [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)，然後 AzCopy hello VM 上已安裝。</span><span class="sxs-lookup"><span data-stu-id="26b52-106">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then AzCopy is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="26b52-107">完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和太[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="26b52-107">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and too[Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="26b52-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="26b52-108">Prerequisites</span></span>
<span data-ttu-id="26b52-109">本文件假設您有 Azure 訂閱，儲存體帳戶和 hello 對應的儲存體金鑰，該帳戶。</span><span class="sxs-lookup"><span data-stu-id="26b52-109">This document assumes that you have an Azure subscription, a storage account and hello corresponding storage key for that account.</span></span> <span data-ttu-id="26b52-110">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="26b52-110">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span>

* <span data-ttu-id="26b52-111">tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="26b52-111">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="26b52-112">如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="26b52-112">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

## <a name="run-azcopy-commands"></a><span data-ttu-id="26b52-113">執行 AzCopy 命令</span><span class="sxs-lookup"><span data-stu-id="26b52-113">Run AzCopy commands</span></span>
<span data-ttu-id="26b52-114">toorun 的 AzCopy 命令開啟命令視窗，並瀏覽您 hello AzCopy.exe 可執行檔所在的電腦上的 toohello AzCopy 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="26b52-114">toorun AzCopy commands, open a command window and navigate toohello AzCopy installation directory on your computer, where hello AzCopy.exe executable is located.</span></span> 

<span data-ttu-id="26b52-115">hello 的 AzCopy 命令的基本語法如下：</span><span class="sxs-lookup"><span data-stu-id="26b52-115">hello basic syntax for AzCopy commands is:</span></span>

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> <span data-ttu-id="26b52-116">您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑，並從任何目錄執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="26b52-116">You can add hello AzCopy installation location tooyour system path and then run hello commands from any directory.</span></span> <span data-ttu-id="26b52-117">根據預設，AzCopy 會太安裝*%programfiles (x86) %\Microsoft SDKs\Azure\AzCopy*或*%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*。</span><span class="sxs-lookup"><span data-stu-id="26b52-117">By default, AzCopy is installed too*%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy* or *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.</span></span>
> 
> 

## <a name="upload-files-tooan-azure-blob"></a><span data-ttu-id="26b52-118">上傳檔案 tooan Azure blob</span><span class="sxs-lookup"><span data-stu-id="26b52-118">Upload files tooan Azure blob</span></span>
<span data-ttu-id="26b52-119">tooupload 檔案，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="26b52-119">tooupload a file, use hello following command:</span></span>

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a><span data-ttu-id="26b52-120">從 Azure Blob 下載檔案</span><span class="sxs-lookup"><span data-stu-id="26b52-120">Download files from an Azure blob</span></span>
<span data-ttu-id="26b52-121">toodownload 檔案，以從 Azure blob，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="26b52-121">toodownload a file from an Azure blob, use hello following command:</span></span>

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a><span data-ttu-id="26b52-122">在 Azure 容器之間傳輸 Blob</span><span class="sxs-lookup"><span data-stu-id="26b52-122">Transfer blobs between Azure containers</span></span>
<span data-ttu-id="26b52-123">Azure 的容器之間的 tootransfer blob 使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="26b52-123">tootransfer blobs between Azure containers, use hello following command:</span></span>

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a><span data-ttu-id="26b52-124">使用 AzCopy 的秘訣</span><span class="sxs-lookup"><span data-stu-id="26b52-124">Tips for using AzCopy</span></span>
> [!TIP]
> 1. <span data-ttu-id="26b52-125">**上傳**檔案時，*/S* 將以遞迴方式上傳檔案。</span><span class="sxs-lookup"><span data-stu-id="26b52-125">When **uploading** files, */S* uploads files recursively.</span></span> <span data-ttu-id="26b52-126">如果沒有這個參數，則不會上傳子目錄中的檔案。</span><span class="sxs-lookup"><span data-stu-id="26b52-126">Without this parameter, files in subdirectories are not uploaded.</span></span>  
> 2. <span data-ttu-id="26b52-127">當**下載**檔案， */S*搜尋才 hello 指定的目錄和其子目錄中的所有檔案 hello 容器以遞迴方式或相符的所有檔案都 hello 都 hello 指定中指定的模式目錄和其子目錄中，會下載。</span><span class="sxs-lookup"><span data-stu-id="26b52-127">When **downloading** file, */S* searches hello container recursively until all files in hello specified directory and its subdirectories, or all files that match hello specified pattern in hello given directory and its subdirectories, are downloaded.</span></span>  
> 3. <span data-ttu-id="26b52-128">您無法指定**特定 blob 檔案**toodownload 使用 hello */來源*參數。</span><span class="sxs-lookup"><span data-stu-id="26b52-128">You cannot specify a **specific blob file** toodownload using hello */Source* parameter.</span></span> <span data-ttu-id="26b52-129">toodownload 特定檔案，指定使用 hello hello blob 檔案名稱 toodownload */模式*參數。</span><span class="sxs-lookup"><span data-stu-id="26b52-129">toodownload a specific file, specify hello blob file name toodownload using hello */Pattern* parameter.</span></span> <span data-ttu-id="26b52-130">**/S**參數可以是檔案名稱模式以遞迴方式使用的 toohave AzCopy 尋找。</span><span class="sxs-lookup"><span data-stu-id="26b52-130">**/S** parameter can be used toohave AzCopy look for a file name pattern recursively.</span></span> <span data-ttu-id="26b52-131">如果沒有 hello 模式參數，AzCopy 會下載該目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="26b52-131">Without hello pattern parameter, AzCopy downloads all files in that directory.</span></span>
> 
> 

