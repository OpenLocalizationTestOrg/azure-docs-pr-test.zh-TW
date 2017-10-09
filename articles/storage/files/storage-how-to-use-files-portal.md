---
title: "aaaHow toomanage 從 hello Azure 入口網站的 Azure 檔案儲存體 |Microsoft 文件"
description: "了解 toouse hello Azure 入口網站 toomanage Azure 檔案儲存體。"
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="b074e-103">如何從 toouse Azure 檔案儲存體 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b074e-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="b074e-104">hello [Azure 入口網站](https://portal.azure.com)管理 Azure 檔案儲存體提供使用者介面。</span><span class="sxs-lookup"><span data-stu-id="b074e-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="b074e-105">您可以執行下列動作，從您網頁瀏覽器的 hello:</span><span class="sxs-lookup"><span data-stu-id="b074e-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="b074e-106">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="b074e-106">Create a File Share</span></span>
* <span data-ttu-id="b074e-107">上傳和下載檔案 tooand 從檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b074e-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="b074e-108">監視 hello 實際使用量的每個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b074e-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="b074e-109">調整 hello 檔案共用大小配額。</span><span class="sxs-lookup"><span data-stu-id="b074e-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="b074e-110">複製 Windows 或 Linux 的用戶端 hello 掛接命令 toouse toomount 您的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b074e-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="b074e-111">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="b074e-111">Create file share</span></span>
1. <span data-ttu-id="b074e-112">登入 toohello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b074e-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="b074e-113">Hello 導覽功能表上，按一下**儲存體帳戶**或**儲存體帳戶 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="b074e-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="b074e-115">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="b074e-115">Choose your storage account.</span></span>

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="b074e-117">選擇「檔案」服務。</span><span class="sxs-lookup"><span data-stu-id="b074e-117">Choose "Files" service.</span></span>

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="b074e-119">按一下 [檔案共用]，並遵循 hello 連結 toocreate 第一個檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b074e-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="b074e-121">填入您的第一個檔案共用 hello 檔案共用名稱與 hello 檔案共用 （向上 too5120 GB) toocreate hello 大小。</span><span class="sxs-lookup"><span data-stu-id="b074e-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="b074e-122">一旦建立 hello 檔案共用之後，您可以從任何支援 SMB 2.1 或 SMB 3.0 的檔案系統掛接它。</span><span class="sxs-lookup"><span data-stu-id="b074e-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="b074e-123">您可以按一下**配額**hello 檔案共用 toochange hello 大小 hello 向上 too5120 GB 的檔案。</span><span class="sxs-lookup"><span data-stu-id="b074e-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="b074e-124">請參閱太[Azure 定價計算機](https://azure.microsoft.com/pricing/calculator/)使用 Azure 檔案儲存體的 tooestimate hello 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="b074e-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![示範如何 toocreate 檔案共用 hello 入口網站中的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="b074e-126">上傳及下載檔案</span><span class="sxs-lookup"><span data-stu-id="b074e-126">Upload and download files</span></span>
1. <span data-ttu-id="b074e-127">選擇一個您已建立的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="b074e-127">Choose one file share your have already created.</span></span>

    ![示範如何從 tooupload 和下載檔案 hello 入口網站的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="b074e-129">按一下**上傳**開啟檔案上傳的 hello 使用者介面。</span><span class="sxs-lookup"><span data-stu-id="b074e-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![示範如何 tooupload 檔案從 hello 入口網站的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="b074e-131">連接 toofile 共用</span><span class="sxs-lookup"><span data-stu-id="b074e-131">Connect toofile share</span></span>
-  <span data-ttu-id="b074e-132">按一下**連接**取得掛接 hello 檔案共用中的 hello 命令列，從 Windows 和 Linux。</span><span class="sxs-lookup"><span data-stu-id="b074e-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="b074e-133">針對 Linux 使用者，您也可以使用參照太[如何 toouse Linux 的 Azure 檔案儲存體](../storage-how-to-use-files-linux.md)針對其他 Linux 散發套件的其他掛接指示。</span><span class="sxs-lookup"><span data-stu-id="b074e-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![示範如何 toomount hello 檔案共用的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="b074e-135">您可以複製的 hello 掛接檔案的命令在 Windows 或 Linux 上共用，並且執行您的 Azure VM 中或在內部部署機器。</span><span class="sxs-lookup"><span data-stu-id="b074e-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![適用於 Windows 和 Linux 顯示 hello 掛接命令的螢幕擷取畫面](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="b074e-137">**秘訣：**</span><span class="sxs-lookup"><span data-stu-id="b074e-137">**Tip:**</span></span>  
<span data-ttu-id="b074e-138">按一下 toofind hello 儲存體帳戶存取金鑰裝載、**檢視存取這個儲存體帳戶金鑰**底部 hello hello 連接頁面。</span><span class="sxs-lookup"><span data-stu-id="b074e-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="b074e-139">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b074e-139">See also</span></span>
<span data-ttu-id="b074e-140">請參閱這些連結以取得 Azure 檔案儲存體的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b074e-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="b074e-141">常見問題集</span><span class="sxs-lookup"><span data-stu-id="b074e-141">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="b074e-142">在 Windows 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b074e-142">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="b074e-143">在 Linux 上進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b074e-143">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    