---
title: "使用 Microsoft Azure 儲存體總管將 VHD 檔案上傳到 Azure DevTest Labs | Microsoft Docs"
description: "使用 Microsoft Azure 儲存體總管將 VHD 檔案上傳到實驗室的儲存體帳戶"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 502e2536fb0fd2e9dfc4c7b85a6fb4e18202f38f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="3a590-103">使用 Microsoft Azure 儲存體總管將 VHD 檔案上傳到實驗室的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3a590-103">Upload VHD file to lab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="3a590-104">在 Azure DevTest Labs 中，可以使用 VHD 檔案來建立自訂映像，這些映像可用來佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3a590-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="3a590-105">本文說明如何使用 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)將 VHD 檔案上傳到實驗室的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-105">This article illustrates how to use [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="3a590-106">在您上傳 VHD 檔案之後，[後續步驟](#next-steps)一節會列出一些說明如何從所上傳的 VHD 檔案建立自訂映像的文章。</span><span class="sxs-lookup"><span data-stu-id="3a590-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="3a590-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="3a590-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="3a590-108">逐步指示</span><span class="sxs-lookup"><span data-stu-id="3a590-108">Step-by-step instructions</span></span>

<span data-ttu-id="3a590-109">下列步驟將逐步引導您使用 [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)將 VHD 檔案上傳到 DevTest Labs。</span><span class="sxs-lookup"><span data-stu-id="3a590-109">The following steps walk you through uploading a VHD file to DevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="3a590-110">[下載並安裝最新版 Microsoft Azure 儲存體總管](http://www.storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="3a590-110">[Download and install the latest version of the Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="3a590-111">使用 Azure 入口網站來取得實驗室的儲存體帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="3a590-111">Get the name of the lab's storage account using the Azure portal:</span></span>

    1. <span data-ttu-id="3a590-112">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="3a590-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="3a590-113">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="3a590-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>
    
    1. <span data-ttu-id="3a590-114">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="3a590-114">From the list of labs, select the desired lab.</span></span>  
    
    1. <span data-ttu-id="3a590-115">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="3a590-115">On the lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="3a590-116">在實驗室的 [組態] 刀鋒視窗上，選取 [自訂映像 (VHD)]。</span><span class="sxs-lookup"><span data-stu-id="3a590-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="3a590-117">在 [自訂映像] 刀鋒視窗上，選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="3a590-117">On the **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="3a590-118">在 [自訂映像] 刀鋒視窗上，選取 [VHD]。</span><span class="sxs-lookup"><span data-stu-id="3a590-118">On the **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="3a590-119">在 [VHD] 刀鋒視窗上，選取 [使用 PowerShell 上傳 VHD]。</span><span class="sxs-lookup"><span data-stu-id="3a590-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![使用 PowerShell 上傳 VHD][0]
    
    1. <span data-ttu-id="3a590-121">[使用 PowerShell 上傳映像] 刀鋒視窗會顯示一個對 **Add-AzureVhd** Cmdlet 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="3a590-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="3a590-122">第一個參數 (*Destination*) 包含實驗室的儲存體帳戶，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="3a590-122">The first parameter (*Destination*) contains the storage account name for the lab in the following format:</span></span>
    
        <span data-ttu-id="3a590-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="3a590-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="3a590-124">記下儲存體帳戶名稱，因為在稍後的步驟中將會用到。</span><span class="sxs-lookup"><span data-stu-id="3a590-124">Make note of the storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="3a590-125">使用儲存體總管連線到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-125">Connect to an Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="3a590-126">儲存體總管支援數個連線選項。</span><span class="sxs-lookup"><span data-stu-id="3a590-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="3a590-127">本節說明如何連線到與您的 Azure 訂用帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-127">This section illustrates connecting to a storage account associated with your Azure subscription.</span></span> <span data-ttu-id="3a590-128">若要查看儲存體總管所支援的其他連線選項，請參閱[開始使用儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)一文。</span><span class="sxs-lookup"><span data-stu-id="3a590-128">To see the other connection options supported by Storage Explorer, refer to the article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="3a590-129">開啟儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="3a590-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="3a590-130">在儲存體總管中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="3a590-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure 帳戶設定][1]
    
    1. <span data-ttu-id="3a590-132">左窗格會顯示您已登入的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-132">The left pane displays the Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="3a590-133">若要連接到其他帳戶，請選取 [新增帳戶] ，並依照對話方塊使用與至少一個作用中 Azure 訂用帳戶相關聯的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="3a590-133">To connect to another account, select **Add an account**, and follow the dialogs to sign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![新增帳戶][2]
    
    1. <span data-ttu-id="3a590-135">成功使用 Microsoft 帳戶登入後，左窗格會填入與該帳戶相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-135">Once you successfully sign in with a Microsoft account, the left pane populates with the Azure subscriptions associated with that account.</span></span> <span data-ttu-id="3a590-136">選取您想要使用的訂用帳戶，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="3a590-136">Select the Azure subscriptions with which you want to work, and then select **Apply**.</span></span> <span data-ttu-id="3a590-137">(選取 [所有訂用帳戶] 切換方塊，可選取全部或不選取任何列出的 Azure 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="3a590-137">(Selecting **All subscriptions** toggles the selection of all or none of the listed Azure subscriptions.)</span></span>
    
        ![選取 Azure 訂用帳戶][3]
    
    1. <span data-ttu-id="3a590-139">左窗格會顯示與所選 Azure 訂用帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a590-139">The left pane displays the storage accounts associated with the selected Azure subscriptions.</span></span>
    
        ![已選取的 Azure 訂用帳戶][4]

1. <span data-ttu-id="3a590-141">找出實驗室的儲存體帳戶︰</span><span class="sxs-lookup"><span data-stu-id="3a590-141">Locate the lab's storage account:</span></span>

    1. <span data-ttu-id="3a590-142">在儲存體總管的左窗格中，找出並展開擁有實驗室之 Azure 訂用帳戶的節點。</span><span class="sxs-lookup"><span data-stu-id="3a590-142">In the Storage Explorer left pane, locate, and expand the node for the Azure subscription that owns the lab.</span></span>
    
    1. <span data-ttu-id="3a590-143">在訂用帳戶的節點下，展開 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="3a590-143">Under the subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="3a590-144">展開實驗室的儲存體帳戶節點，以顯示 [Blob 容器]、[檔案共用]、[佇列] 和 [資料表] 的節點。</span><span class="sxs-lookup"><span data-stu-id="3a590-144">Expand the lab's storage account node to reveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="3a590-145">展開 [Blob 容器] 節點。</span><span class="sxs-lookup"><span data-stu-id="3a590-145">Expand the **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="3a590-146">選取上傳 Blob 容器以在右窗格中顯示其內容。</span><span class="sxs-lookup"><span data-stu-id="3a590-146">Select the uploads blob container to display its contents in the right pane.</span></span>
        
        ![上傳目錄][5]

1. <span data-ttu-id="3a590-148">使用儲存體總管上傳 VHD 檔案︰</span><span class="sxs-lookup"><span data-stu-id="3a590-148">Upload the VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="3a590-149">在儲存體總管的右窗格中，您應該會在實驗室儲存體帳戶的 [上傳] Blob 容器中看到 Blob 清單。</span><span class="sxs-lookup"><span data-stu-id="3a590-149">In the Storage Explorer right pane, you should see a listing of the blobs in the **uploads** blob container of the lab's storage account.</span></span> <span data-ttu-id="3a590-150">在 Blob 編輯器工具列中，選取 [上傳]</span><span class="sxs-lookup"><span data-stu-id="3a590-150">On the blob editor toolbar, select **Upload**</span></span> 
        
        ![上傳按鈕][6]
    
    1. <span data-ttu-id="3a590-152">從 [上傳] 下拉式功能表中，選取 [上傳檔案...]。</span><span class="sxs-lookup"><span data-stu-id="3a590-152">From the **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="3a590-153">在 [上傳檔案] 對話方塊中，選取省略符號。</span><span class="sxs-lookup"><span data-stu-id="3a590-153">On the **Upload files** dialog, select the ellipsis.</span></span>
        
        ![選取檔案][8]  

    1. <span data-ttu-id="3a590-155">在 [選取要上傳的檔案] 對話方塊中，瀏覽至所需的 VHD 檔案、加以選取，然後選取 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="3a590-155">On the **Select files to upload** dialog, browse to the desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="3a590-156">在回到 [上傳檔案] 對話方塊時，將 [Blob 類型] 變更為 [分頁 Blob]。</span><span class="sxs-lookup"><span data-stu-id="3a590-156">When returned to the **Upload files** dialog, change **Blob type** to **Page Blob**.</span></span>
    
    1. <span data-ttu-id="3a590-157">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="3a590-157">Select **Upload**.</span></span>

        ![選取檔案][9]  
    
    1. <span data-ttu-id="3a590-159">儲存體總管的 [活動記錄] 窗格會顯示下載狀態 (以及用以取消上傳的連結)。</span><span class="sxs-lookup"><span data-stu-id="3a590-159">The Storage Explorer **Activity Log** pane shows the download status (along with links to cancel the upload).</span></span> <span data-ttu-id="3a590-160">視 VHD 檔案大小及您的連線速度而定，上傳 VHD 檔案的程序可能會相當長。</span><span class="sxs-lookup"><span data-stu-id="3a590-160">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span> 

        ![上傳檔案狀態][10]  

## <a name="next-steps"></a><span data-ttu-id="3a590-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a590-162">Next steps</span></span>

- [<span data-ttu-id="3a590-163">使用 Azure 入口網站在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="3a590-163">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="3a590-164">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="3a590-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
