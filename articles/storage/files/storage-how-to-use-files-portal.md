---
title: "如何管理 Azure 入口網站的 Azure 檔案儲存體 | Microsoft Docs"
description: "了解使用 Azure 入口網站來管理 Azure 檔案儲存體。"
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: d5ffa7cff0a31e36f5a96aaa4b2d477fa39333fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-file-storage-from-the-azure-portal"></a><span data-ttu-id="121a8-103">如何使用 Azure 入口網站的 Azure 檔案儲存體</span><span class="sxs-lookup"><span data-stu-id="121a8-103">How to use Azure File storage from the Azure Portal</span></span>
<span data-ttu-id="121a8-104">[Azure 入口網站](https://portal.azure.com)提供可管理 Azure 檔案儲存體的使用者介面。</span><span class="sxs-lookup"><span data-stu-id="121a8-104">The [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="121a8-105">您可以從網路瀏覽器執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="121a8-105">You can perform the following actions from your web browser:</span></span>

* <span data-ttu-id="121a8-106">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="121a8-106">Create a File Share</span></span>
* <span data-ttu-id="121a8-107">上傳檔案至檔案共用以及從檔案共用下載檔案。</span><span class="sxs-lookup"><span data-stu-id="121a8-107">Upload and download files to and from your file share.</span></span>
* <span data-ttu-id="121a8-108">監視每個檔案共用的實際使用狀況。</span><span class="sxs-lookup"><span data-stu-id="121a8-108">Monitor the actual usage of each file share.</span></span>
* <span data-ttu-id="121a8-109">調整檔案室共用大小配額。</span><span class="sxs-lookup"><span data-stu-id="121a8-109">Adjust the file share size quota.</span></span>
* <span data-ttu-id="121a8-110">複製並使用掛接命令以從 Windows 或 Linux 用戶端掛接檔案共用。</span><span class="sxs-lookup"><span data-stu-id="121a8-110">Copy the mount commands to use to mount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="121a8-111">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="121a8-111">Create file share</span></span>
1. <span data-ttu-id="121a8-112">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="121a8-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="121a8-113">在導覽功能表中，按一下 [儲存體帳戶] 或 [儲存體帳戶 (傳統)]。</span><span class="sxs-lookup"><span data-stu-id="121a8-113">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![示範如何在入口網站中建立檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="121a8-115">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="121a8-115">Choose your storage account.</span></span>

    ![示範如何在入口網站中建立檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="121a8-117">選擇「檔案」服務。</span><span class="sxs-lookup"><span data-stu-id="121a8-117">Choose "Files" service.</span></span>

    ![示範如何在入口網站中建立檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="121a8-119">按一下 [檔案共用] 並依連結建立您的第一個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="121a8-119">Click "File shares" and follow the link to create your first file share.</span></span>

    ![示範如何在入口網站中建立檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="121a8-121">填寫檔案共用名稱和檔案共用大小 (最多 5120 GB)，以建立第一個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="121a8-121">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="121a8-122">建立檔案共用之後，您可以從任何支援 SMB 2.1 或 SMB 3.0 的檔案系統掛接此共用。</span><span class="sxs-lookup"><span data-stu-id="121a8-122">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="121a8-123">您可以按一下檔案共用上的 [配額]  以變更檔案大小 (最多 5120 GB)。</span><span class="sxs-lookup"><span data-stu-id="121a8-123">You could click on **Quota** on the file share to change the size of the file up to 5120 GB.</span></span> <span data-ttu-id="121a8-124">請參閱 [Azure 價格計算機](https://azure.microsoft.com/pricing/calculator/)來估計使用 Azure 檔案儲存體的儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="121a8-124">Please refer to [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) to estimate the storage cost of using Azure File storage.</span></span>

    ![示範如何在入口網站中建立檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="121a8-126">上傳及下載檔案</span><span class="sxs-lookup"><span data-stu-id="121a8-126">Upload and download files</span></span>
1. <span data-ttu-id="121a8-127">選擇一個您已建立的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="121a8-127">Choose one file share your have already created.</span></span>

    ![示範如何從入口網站上傳和下載檔案](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="121a8-129">按一下 [上傳]  以開啟使用者介面以進行檔案上傳。</span><span class="sxs-lookup"><span data-stu-id="121a8-129">Click **Upload** to open the user interface for files uploading.</span></span>

    ![示範如何從入口網站上傳檔案](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-to-file-share"></a><span data-ttu-id="121a8-131">連線至檔案共用</span><span class="sxs-lookup"><span data-stu-id="121a8-131">Connect to file share</span></span>
-  <span data-ttu-id="121a8-132">按一下 [連線] 以取得從 Windows 和 Linux 掛接檔案共用的命令列。</span><span class="sxs-lookup"><span data-stu-id="121a8-132">Click **Connect** to get the command line for mounting the file share from Windows and Linux.</span></span> <span data-ttu-id="121a8-133">針對 Linux 使用者，您也可以參閱[如何搭配使用 Azure 檔案儲存體與 Linux](../storage-how-to-use-files-linux.md)取得更多 Linux 散發套件的掛接指示。</span><span class="sxs-lookup"><span data-stu-id="121a8-133">For Linux users, you can also refer to [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![示範如何掛接檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="121a8-135">您可以在 Windows 或 Linux 上複製掛接檔案共用的命令，並從您的 Azure VM 或內部部署機器執行。</span><span class="sxs-lookup"><span data-stu-id="121a8-135">You can copy the commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![顯示適用於 Windows 和 Linux 掛接命令的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="121a8-137">**秘訣：**</span><span class="sxs-lookup"><span data-stu-id="121a8-137">**Tip:**</span></span>  
<span data-ttu-id="121a8-138">要尋找掛接的儲存體帳戶存取金鑰，按一下連線頁面底部的 [檢視此儲存體帳戶的存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="121a8-138">To find the storage account access key for mounting, click on **View access keys for this storage account** at the bottom of the connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="121a8-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="121a8-139">See also</span></span>
<span data-ttu-id="121a8-140">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="121a8-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="121a8-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="121a8-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="121a8-142">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="121a8-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="121a8-143">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="121a8-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    