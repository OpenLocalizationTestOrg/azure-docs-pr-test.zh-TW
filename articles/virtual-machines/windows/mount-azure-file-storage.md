---
title: "從 Windows Azure VM 的 Azure 檔案儲存體 aaaMount |Microsoft 文件"
description: "將檔案儲存在 hello 雲端，使用 Azure 檔案儲存體，並從 Azure 虛擬機器 (VM) 掛接您雲端的檔案共用。"
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="f10f0-103">搭配 Windows VM 使用 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="f10f0-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="f10f0-104">您可以使用 Azure 檔案共用方式 toostore 及存取檔案，從您的 VM。</span><span class="sxs-lookup"><span data-stu-id="f10f0-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="f10f0-105">例如，您可以儲存指令碼或您想要您所有的 Vm tooshare 應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="f10f0-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="f10f0-106">在本主題中，我們會示範如何 toocreate 及掛接 Azure 檔案共用，以及如何 tooupload 和下載檔案。</span><span class="sxs-lookup"><span data-stu-id="f10f0-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="f10f0-107">從 VM 連接 tooa 檔案共用</span><span class="sxs-lookup"><span data-stu-id="f10f0-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="f10f0-108">本節假設您已經有個檔案共用您想要 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="f10f0-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="f10f0-109">如果您需要一個 toocreate，請參閱[建立檔案共用](#create-a-file-share)本主題稍後。</span><span class="sxs-lookup"><span data-stu-id="f10f0-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="f10f0-110">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f10f0-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f10f0-111">在 hello 左窗格中，按一下 **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f10f0-112">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f10f0-112">Choose your storage account.</span></span>
4. <span data-ttu-id="f10f0-113">在 hello**概觀**頁面的 **服務**，選取**檔案**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f10f0-114">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-114">Select a file share.</span></span>
6. <span data-ttu-id="f10f0-115">按一下**連接**tooopen 頁面，其中顯示 hello 命令列語法，從 Windows 或 Linux 掛接 hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="f10f0-116">反白顯示 hello hello 命令語法，並將它貼到 [記事本] 或其他位置，您可以輕鬆地存取。</span><span class="sxs-lookup"><span data-stu-id="f10f0-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="f10f0-117">編輯 hello 語法 tooremove hello 前置 * * > * * 並取代*[磁碟機代號]* hello 磁碟機代號 (例如， **y:**) toomount hello 檔案共用的位置。</span><span class="sxs-lookup"><span data-stu-id="f10f0-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="f10f0-118">連接 tooyour VM，然後開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f10f0-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="f10f0-119">貼上的 hello 編輯連接語法，叫用**Enter**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="f10f0-120">Hello 連線建立後，您會收到 hello 訊息**hello 命令已順利完成。**</span><span class="sxs-lookup"><span data-stu-id="f10f0-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="f10f0-121">請檢查輸入 hello 磁碟機代號 tooswitch toothat 磁碟機中的 hello 連線，然後輸入**dir** toosee hello hello 檔案共用內容。</span><span class="sxs-lookup"><span data-stu-id="f10f0-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="f10f0-122">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="f10f0-122">Create a file share</span></span> 
1. <span data-ttu-id="f10f0-123">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f10f0-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f10f0-124">在 hello 左窗格中，按一下 **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f10f0-125">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f10f0-125">Choose your storage account.</span></span>
4. <span data-ttu-id="f10f0-126">在 hello**概觀**頁面的 **服務**，選取**檔案**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f10f0-127">在 hello 檔案服務 頁面上，按一下  **+ 檔案共用**toocreate 第一個檔案共用。 \\</span><span class="sxs-lookup"><span data-stu-id="f10f0-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="f10f0-128">填寫 hello 檔案共用名稱。</span><span class="sxs-lookup"><span data-stu-id="f10f0-128">Fill in hello file share name.</span></span> <span data-ttu-id="f10f0-129">檔案共用名稱可以使用小寫字母、數字和單一連字號。</span><span class="sxs-lookup"><span data-stu-id="f10f0-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="f10f0-130">hello 名稱不能以連字號開頭，而且您無法使用多個連續連字號。</span><span class="sxs-lookup"><span data-stu-id="f10f0-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="f10f0-131">最長 too5120 GB，可能會填滿多少 hello 檔案上的限制。</span><span class="sxs-lookup"><span data-stu-id="f10f0-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="f10f0-132">按一下**確定**toodeploy hello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="f10f0-133">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="f10f0-133">Upload files</span></span>
1. <span data-ttu-id="f10f0-134">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f10f0-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f10f0-135">在 hello 左窗格中，按一下 **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f10f0-136">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f10f0-136">Choose your storage account.</span></span>
4. <span data-ttu-id="f10f0-137">在 hello**概觀**頁面的 **服務**，選取**檔案**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f10f0-138">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-138">Select a file share.</span></span>
6. <span data-ttu-id="f10f0-139">按一下**上傳**tooopen hello**將檔案上傳**頁面。</span><span class="sxs-lookup"><span data-stu-id="f10f0-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="f10f0-140">按一下 hello 資料夾圖示 toobrowse 本機檔案系統，對檔案 tooupload。</span><span class="sxs-lookup"><span data-stu-id="f10f0-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="f10f0-141">按一下**上傳**tooupload hello 檔案 toohello 檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="f10f0-142">下載檔案</span><span class="sxs-lookup"><span data-stu-id="f10f0-142">Download files</span></span>
1. <span data-ttu-id="f10f0-143">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f10f0-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f10f0-144">在 hello 左窗格中，按一下 **儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="f10f0-145">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="f10f0-145">Choose your storage account.</span></span>
4. <span data-ttu-id="f10f0-146">在 hello**概觀**頁面的 **服務**，選取**檔案**。</span><span class="sxs-lookup"><span data-stu-id="f10f0-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="f10f0-147">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-147">Select a file share.</span></span>
6. <span data-ttu-id="f10f0-148">Hello 檔案上按一下滑鼠右鍵，然後選擇 **下載**toodownload 它 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="f10f0-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="f10f0-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f10f0-149">Next steps</span></span>

<span data-ttu-id="f10f0-150">您也可以使用 PowerShell 建立和管理檔案共用。</span><span class="sxs-lookup"><span data-stu-id="f10f0-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="f10f0-151">如需詳細資訊，請參閱[開始使用 Windows 上的 Azure 檔案儲存體](../../storage/files/storage-dotnet-how-to-use-files.md)。</span><span class="sxs-lookup"><span data-stu-id="f10f0-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
