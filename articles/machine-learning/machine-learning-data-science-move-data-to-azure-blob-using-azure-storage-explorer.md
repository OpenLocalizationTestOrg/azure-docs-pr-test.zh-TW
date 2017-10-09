---
title: "從 Blob 儲存體與 Azure 儲存體總管 aaaMove 資料 tooand |Microsoft 文件"
description: "移動資料 tooand 從 Azure Blob 儲存體，使用 Azure 儲存體總管"
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
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a><span data-ttu-id="0fc33-103">移動資料 tooand 從 Azure Blob 儲存體，使用 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="0fc33-103">Move data tooand from Azure Blob Storage using Azure Storage Explorer</span></span>
<span data-ttu-id="0fc33-104">Azure 儲存體總管是 microsoft Windows、 macOS 和 Linux 的 Azure 儲存體資料 toowork 可讓您的免費的工具。</span><span class="sxs-lookup"><span data-stu-id="0fc33-104">Azure Storage Explorer is a free tool from Microsoft that allows you toowork with Azure Storage data on Windows, macOS, and Linux.</span></span> <span data-ttu-id="0fc33-105">本主題描述如何 toouse 它 tooupload 和下載資料從 Azure blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0fc33-105">This topic describes how toouse it tooupload and download data from Azure blob storage.</span></span> <span data-ttu-id="0fc33-106">hello 工具可以從下載[Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="0fc33-106">hello tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> <span data-ttu-id="0fc33-107">如果您要使用所提供的 hello 指令碼與設定的 VM [Azure 中的資料科學虛擬機器](machine-learning-data-science-virtual-machines.md)，然後 hello VM 上已安裝 Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="0fc33-107">If you are using VM that was set up with hello scripts provided by [Data Science Virtual machines in Azure](machine-learning-data-science-virtual-machines.md), then Azure Storage Explorer is already installed on hello VM.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="0fc33-108">完成簡介 tooAzure blob 儲存體，請參閱太[Azure Blob 的基本概念](../storage/blobs/storage-dotnet-how-to-use-blobs.md)和[Azure Blob 服務](https://msdn.microsoft.com/library/azure/dd179376.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0fc33-108">For a complete introduction tooAzure blob storage, refer too[Azure Blob Basics](../storage/blobs/storage-dotnet-how-to-use-blobs.md) and [Azure Blob Service](https://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>   
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0fc33-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="0fc33-109">Prerequisites</span></span>
<span data-ttu-id="0fc33-110">本文件假設您有 Azure 訂用帳戶、 儲存體帳戶和該帳戶 hello 對應儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fc33-110">This document assumes that you have an Azure subscription, a storage account, and hello corresponding storage key for that account.</span></span> <span data-ttu-id="0fc33-111">上傳/下載資料之前，您必須知道 Azure 儲存體帳戶名稱和帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="0fc33-111">Before uploading/downloading data, you must know your Azure storage account name and account key.</span></span> 

* <span data-ttu-id="0fc33-112">tooset 註冊 Azure 訂用帳戶，請參閱[免費試用一個月](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0fc33-112">tooset up an Azure subscription, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0fc33-113">如需建立儲存體帳戶的指示，以及取得帳戶和金鑰的資訊，請參閱 [關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="0fc33-113">For instructions on creating a storage account and for getting account and key information, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0fc33-114">請注意 hello 存取金鑰的儲存體帳戶，因為您需要此金鑰 tooconnect toohello 帳戶與 hello Azure 儲存體總管工具。</span><span class="sxs-lookup"><span data-stu-id="0fc33-114">Make a note hello access key for your storage account as you need this key tooconnect toohello account with hello Azure Storage Explorer tool.</span></span>
* <span data-ttu-id="0fc33-115">hello Azure 儲存體總管工具可以從下載[Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="0fc33-115">hello Azure Storage Explorer tool can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="0fc33-116">接受 hello 期間的預設值安裝。</span><span class="sxs-lookup"><span data-stu-id="0fc33-116">Accept hello defaults during install.</span></span>

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a><span data-ttu-id="0fc33-117">使用 Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="0fc33-117">Use Azure Storage Explorer</span></span>
<span data-ttu-id="0fc33-118">hello 遵循步驟文件如何使用 Azure 儲存體總管 tooupload/下載資料。</span><span class="sxs-lookup"><span data-stu-id="0fc33-118">hello following steps document how tooupload/download data using Azure Storage Explorer.</span></span> 

1. <span data-ttu-id="0fc33-119">啟動 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="0fc33-119">Launch Microsoft Azure Storage Explorer.</span></span>
2. <span data-ttu-id="0fc33-120">向上 hello toobring**登入 tooyour 帳戶...**精靈中，選取**Azure 帳戶設定**圖示，然後**將帳戶加入**並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="0fc33-120">toobring up hello **Sign in tooyour account...** wizard, select **Azure account settings** icon, then **Add an account** and enter you credentials.</span></span> <span data-ttu-id="0fc33-121">![新增 Azure 儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-121">![Add an Azure storage account](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)</span></span>
3. <span data-ttu-id="0fc33-122">向上 hello toobring**連接儲存體 tooAzure**精靈、 選取 hello **tooAzure 存放裝置連線**圖示。</span><span class="sxs-lookup"><span data-stu-id="0fc33-122">toobring up hello **Connect tooAzure Storage** wizard, select hello **Connect tooAzure storage** icon.</span></span> <span data-ttu-id="0fc33-123">![TooAzure 存放裝置連線](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-123">![Connect tooAzure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)</span></span>
4. <span data-ttu-id="0fc33-124">從您的 Azure 儲存體帳戶輸入 hello 存取金鑰，在 hello**連接儲存體 tooAzure**精靈，然後**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0fc33-124">Enter hello access key from your Azure storage account on hello **Connect tooAzure Storage** wizard and then **Next**.</span></span> <span data-ttu-id="0fc33-125">![TooAzure 存放裝置連線](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-125">![Connect tooAzure storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)</span></span>
5. <span data-ttu-id="0fc33-126">輸入儲存體帳戶名稱在 hello**帳戶名稱**方塊，然後選取 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="0fc33-126">Enter storage account name in hello **Account name** box and then select **Next**.</span></span> <span data-ttu-id="0fc33-127">![附加外部儲存體](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-127">![Attach external storage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)</span></span>
6. <span data-ttu-id="0fc33-128">現在應該會顯示 hello 新增儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fc33-128">hello storage account added should now be listed.</span></span> <span data-ttu-id="0fc33-129">toocreate blob 容器中的儲存體帳戶，以滑鼠右鍵按一下 hello **Blob 容器**中該帳戶，請選取節點**建立 Blob 容器**，然後輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fc33-129">toocreate a blob container in a storage account, right-click hello **Blob Containers** node in that account, select **Create Blob Container**, and enter a name.</span></span>
7. <span data-ttu-id="0fc33-130">tooupload 資料 tooa 容器、 選取 hello 目標容器，按一下 hello**上傳** 按鈕。![儲存體帳戶](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-130">tooupload data tooa container, select hello target container and click hello **Upload** button.![Storage accounts](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)</span></span>
8. <span data-ttu-id="0fc33-131">按一下 hello **...**方 hello toohello**檔案**方塊選取一個或多個檔案 tooupload hello 檔案系統中，按一下**上傳**toobegin hello 檔案上載。![上傳檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-131">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)</span></span>
9. <span data-ttu-id="0fc33-132">選取 hello 的 toodownload 資料 hello 對應容器 toodownload 中的 blob，並按一下**下載**。</span><span class="sxs-lookup"><span data-stu-id="0fc33-132">toodownload data, selecting hello blob in hello corresponding container toodownload and click **Download**.</span></span> <span data-ttu-id="0fc33-133">![下載檔案](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span><span class="sxs-lookup"><span data-stu-id="0fc33-133">![Download files](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)</span></span>

