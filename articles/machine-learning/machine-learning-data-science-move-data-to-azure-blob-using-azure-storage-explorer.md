---
title: "使用 Azure 儲存體總管從 Blob 儲存體移入或移出資料 | Microsoft Docs"
description: "使用 Azure 儲存體總管從 Azure Blob 儲存體來回移動資料"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 0943bfcf51a1196e3e4ae7b2145708aa26d52190
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-and-from-azure-blob-storage-using-azure-storage-explorer"></a><span data-ttu-id="bd7a7-103">使用 Azure 儲存體總管從 Azure Blob 儲存體來回移動資料</span><span class="sxs-lookup"><span data-stu-id="bd7a7-103">Move data to and from Azure Blob Storage using Azure Storage Explorer</span></span>
<span data-ttu-id="bd7a7-104">Azure 儲存體總管是 Microsoft 所提供的免費工具，可讓您在 Windows、MacOS 和 Linux 上使用 Azure 儲存體資料。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-104">Azure Storage Explorer is a free tool from Microsoft that allows you to work with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="bd7a7-105">本主題說明如何使用它來於 Azure Blob 儲存體中上傳及下載資料。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-105">This topic describes how to use it to upload and download data from Azure blob storage.</span></span> <span data-ttu-id="bd7a7-106">您可以從 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)下載此工具。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-106">The tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="bd7a7-107">如果您是使用以 [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)提供的指令碼所設定的 VM，則 Azure 儲存體總管已經安裝在 VM 上。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-107">If you are using VM that was set up with the scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then Azure Storage Explorer is already installed on the VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="bd7a7-108">如需 Azure Blob 儲存體的完整介紹，請參閱 [Azure Blob 基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和 [Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-108">For a complete introduction to Azure blob storage, refer to [Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>   
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bd7a7-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="bd7a7-109">Prerequisites</span></span>
<span data-ttu-id="bd7a7-110">本文件假設您擁有 Azure 訂用帳戶、儲存體帳戶和該帳戶的對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-110">This document assumes that you have an Azure subscription, a storage account, and the corresponding storage key for that account.</span></span> <span data-ttu-id="bd7a7-111">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span> 

* <span data-ttu-id="bd7a7-112">若要設定 Azure 訂用帳戶，請參閱 [免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-112">To set up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="bd7a7-113">如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="bd7a7-114">記下儲存體帳戶的存取金鑰，因為您需要此金鑰，才能連接到具有 Azure 儲存體總管工具的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-114">Make a note the access key for your storage account as you need this key to connect to the account with the Azure Storage Explorer tool.</span></span>
* <span data-ttu-id="bd7a7-115">您可以從 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)下載 Azure 儲存體總管工具。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-115">The Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="bd7a7-116">安裝期間請接受預設值。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-116">Accept the defaults during install.</span></span>

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a><span data-ttu-id="bd7a7-117">使用 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="bd7a7-117">Use Azure Storage Explorer</span></span>
<span data-ttu-id="bd7a7-118">下列步驟說明如何使用 Azure 儲存體總管上傳/下載資料。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-118">The following steps document how to upload/download data using Azure Storage Explorer.</span></span> 

1. <span data-ttu-id="bd7a7-119">啟動 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-119">Launch Microsoft Azure Storage Explorer.</span></span>
2. <span data-ttu-id="bd7a7-120">若要啟動 [登入您的帳戶...] 精靈，請選取 [Azure 帳戶設定] 圖示，然後選取 [新增帳戶] 並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-120">To bring up the **Sign in to your account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span></span> <span data-ttu-id="bd7a7-121">![新增 Azure 儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-121">![Add an Azure storage account](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span></span>
3. <span data-ttu-id="bd7a7-122">若要啟動 [連接到 Azure 儲存體] 精靈，請選取 [連接到 Azure 儲存體] 圖示。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-122">To bring up the **Connect to Azure Storage** wizard, select the **Connect to Azure storage** icon.</span></span> <span data-ttu-id="bd7a7-123">![連接到 Azure 儲存體](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-123">![Connect to Azure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span></span>
4. <span data-ttu-id="bd7a7-124">在 [連接到 Azure 儲存體] 精靈中輸入 Azure 儲存體帳戶的存取金鑰，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-124">Enter the access key from your Azure storage account on the **Connect to Azure Storage** wizard and then **Next**.</span></span> <span data-ttu-id="bd7a7-125">![連接到 Azure 儲存體](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-125">![Connect to Azure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span></span>
5. <span data-ttu-id="bd7a7-126">在 [帳戶名稱] 方塊中輸入儲存體帳戶名稱，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-126">Enter storage account name in the **Account name** box and then select **Next**.</span></span> <span data-ttu-id="bd7a7-127">![附加外部儲存體](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-127">![Attach external storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span></span>
6. <span data-ttu-id="bd7a7-128">現在應該會列出新增的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-128">The storage account added should now be listed.</span></span> <span data-ttu-id="bd7a7-129">若要在儲存體帳戶中建立 Blob 容器，請以滑鼠右鍵按一下該帳戶中的 [Blob 容器] 節點、選取 [建立 Blob 容器]，然後輸入名稱。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-129">To create a blob container in a storage account, right-click the **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span></span>
7. <span data-ttu-id="bd7a7-130">若要將資料上傳至容器，請選取目標容器，然後按一下 [上傳] 按鈕。![儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-130">To upload data to a container, select the target container and click the **Upload** button.![Storage accounts](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span></span>
8. <span data-ttu-id="bd7a7-131">按一下 [檔案] 方塊右邊的 [...]，從檔案系統中選取一或多個要上傳的檔案，然後按一下 [上傳]，開始上傳檔案。![上傳檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-131">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span></span>
9. <span data-ttu-id="bd7a7-132">若要下載資料，選取對應容器中要下載的 Blob，然後按一下 [下載] 。</span><span class="sxs-lookup"><span data-stu-id="bd7a7-132">To download data, selecting the blob in the corresponding container to download and click **Download**.</span></span> <span data-ttu-id="bd7a7-133">![下載檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span><span class="sxs-lookup"><span data-stu-id="bd7a7-133">![Download files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span></span>

