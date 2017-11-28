---
title: "從 Azure Windows VM 掛接 Azure 檔案儲存體 | Microsoft Docs"
description: "使用 Azure 檔案儲存體在雲端中儲存檔案，並從 Azure 虛擬機器 (VM) 掛接雲端檔案共用。"
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="ec004-103">搭配 Windows VM 使用 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="ec004-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="ec004-104">您可以使用 Azure 檔案共用，用以從 VM 儲存及存取檔案。</span><span class="sxs-lookup"><span data-stu-id="ec004-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="ec004-105">例如，您可以儲存您想要所有 VM 共用的指令碼或應用程式組態檔。</span><span class="sxs-lookup"><span data-stu-id="ec004-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="ec004-106">本主題會示範如何建立和掛接 Azure 檔案共用，以及如何上傳和下載檔案。</span><span class="sxs-lookup"><span data-stu-id="ec004-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="ec004-107">從 VM 連線至檔案共用</span><span class="sxs-lookup"><span data-stu-id="ec004-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="ec004-108">本節假設您已有想要連線的檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="ec004-109">如果需要建立檔案共用，請參閱本主題稍後的[建立檔案共用](#create-a-file-share)。</span><span class="sxs-lookup"><span data-stu-id="ec004-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="ec004-110">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec004-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec004-111">按一下左側功能表的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ec004-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="ec004-112">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ec004-112">Choose your storage account.</span></span>
4. <span data-ttu-id="ec004-113">在 [概觀] 頁面的 [服務] 底下，選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="ec004-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="ec004-114">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-114">Select a file share.</span></span>
6. <span data-ttu-id="ec004-115">按一下 [連線] 開啟網頁，該網頁會顯示從 Windows 或 Linux 掛接檔案共用的命令列語法。</span><span class="sxs-lookup"><span data-stu-id="ec004-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="ec004-116">反白顯示命令語法，並將它貼到記事本或其他可以輕鬆存取的位置。</span><span class="sxs-lookup"><span data-stu-id="ec004-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="ec004-117">編輯語法以移除前置的 **> ** 並以您想要掛接檔案共用的磁碟機代號 (例如 **Y:**) 取代 [磁碟機代號]。</span><span class="sxs-lookup"><span data-stu-id="ec004-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="ec004-118">連線至 VM，並開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="ec004-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="ec004-119">貼上已編輯的連線語法，然後點擊 [Enter]。</span><span class="sxs-lookup"><span data-stu-id="ec004-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="ec004-120">建立連線之後，會收到訊息**命令已順利完成。**</span><span class="sxs-lookup"><span data-stu-id="ec004-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="ec004-121">請檢查連線，輸入磁碟機代號以切換至該磁碟機，然後輸入 **dir** 查看檔案共用的內容。</span><span class="sxs-lookup"><span data-stu-id="ec004-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="ec004-122">建立檔案共用</span><span class="sxs-lookup"><span data-stu-id="ec004-122">Create a file share</span></span> 
1. <span data-ttu-id="ec004-123">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec004-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec004-124">按一下左側功能表的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ec004-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="ec004-125">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ec004-125">Choose your storage account.</span></span>
4. <span data-ttu-id="ec004-126">在 [概觀] 頁面的 [服務] 底下，選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="ec004-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="ec004-127">在 [檔案服務] 頁面中，按一下 [+ 檔案共用] 建立您的第一個檔案共用。\\</span><span class="sxs-lookup"><span data-stu-id="ec004-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="ec004-128">填入檔案共用名稱。</span><span class="sxs-lookup"><span data-stu-id="ec004-128">Fill in the file share name.</span></span> <span data-ttu-id="ec004-129">檔案共用名稱可以使用小寫字母、數字和單一連字號。</span><span class="sxs-lookup"><span data-stu-id="ec004-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="ec004-130">名稱不能以連字號開頭，且不能連續使用多個連字號。</span><span class="sxs-lookup"><span data-stu-id="ec004-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="ec004-131">填入檔案大小上限，最多 5120 GB。</span><span class="sxs-lookup"><span data-stu-id="ec004-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="ec004-132">按一下 [確定] 部署檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="ec004-133">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="ec004-133">Upload files</span></span>
1. <span data-ttu-id="ec004-134">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec004-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec004-135">按一下左側功能表的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ec004-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="ec004-136">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ec004-136">Choose your storage account.</span></span>
4. <span data-ttu-id="ec004-137">在 [概觀] 頁面的 [服務] 底下，選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="ec004-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="ec004-138">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-138">Select a file share.</span></span>
6. <span data-ttu-id="ec004-139">按一下 [上傳] 開啟 [上傳檔案] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ec004-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="ec004-140">按一下資料夾圖示，瀏覽本機檔案系統，找出要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="ec004-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="ec004-141">按一下 [上傳] 將檔案上傳至檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="ec004-142">下載檔案</span><span class="sxs-lookup"><span data-stu-id="ec004-142">Download files</span></span>
1. <span data-ttu-id="ec004-143">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ec004-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ec004-144">按一下左側功能表的 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="ec004-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="ec004-145">選擇儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="ec004-145">Choose your storage account.</span></span>
4. <span data-ttu-id="ec004-146">在 [概觀] 頁面的 [服務] 底下，選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="ec004-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="ec004-147">選取檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-147">Select a file share.</span></span>
6. <span data-ttu-id="ec004-148">在檔案上按一下滑鼠右鍵，選擇 [下載]，將檔案下載到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="ec004-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="ec004-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec004-149">Next steps</span></span>

<span data-ttu-id="ec004-150">您也可以使用 PowerShell 建立和管理檔案共用。</span><span class="sxs-lookup"><span data-stu-id="ec004-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="ec004-151">如需詳細資訊，請參閱[開始使用 Windows 上的 Azure 檔案儲存體](../../storage/files/storage-dotnet-how-to-use-files.md)。</span><span class="sxs-lookup"><span data-stu-id="ec004-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
