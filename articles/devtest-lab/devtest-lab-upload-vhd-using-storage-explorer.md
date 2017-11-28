---
title: "aaaUpload VHD 檔案使用 Microsoft Azure 儲存體總管 tooAzure DevTest Labs |Microsoft 文件"
description: "上傳 VHD 檔案 toolab 的儲存體帳戶使用 Microsoft Azure 儲存體總管"
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
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a><span data-ttu-id="fd243-103">上傳 VHD 檔案 toolab 的儲存體帳戶使用 Microsoft Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="fd243-103">Upload VHD file toolab's storage account using Microsoft Azure Storage Explorer</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="fd243-104">在 Azure 的 DevTest Labs、 VHD 檔案可以是使用的 toocreate 自訂映像，也就是使用的 tooprovision 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd243-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="fd243-105">本文將說明如何 toouse [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)tooupload VHD 檔案 tooa 實驗室儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-105">This article illustrates how toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="fd243-106">一旦您已上傳 VHD 檔案，hello[後續步驟 > 一節](#next-steps)列出說明如何 toocreate hello 從自訂映像上傳 VHD 檔案的某些文件。</span><span class="sxs-lookup"><span data-stu-id="fd243-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="fd243-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="fd243-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="fd243-108">逐步指示</span><span class="sxs-lookup"><span data-stu-id="fd243-108">Step-by-step instructions</span></span>

<span data-ttu-id="fd243-109">下列步驟查核行程您上傳 VHD 檔案使用 tooDevTest 實驗室 hello [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="fd243-109">hello following steps walk you through uploading a VHD file tooDevTest Labs using [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>

1. <span data-ttu-id="fd243-110">[下載並安裝 hello 最新版 Microsoft Azure 儲存體總管 hello](http://www.storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="fd243-110">[Download and install hello latest version of hello Microsoft Azure Storage Explorer](http://www.storageexplorer.com).</span></span>

1. <span data-ttu-id="fd243-111">收到 hello 使用 hello Azure 入口網站的 hello 實驗室儲存體帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="fd243-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

    1. <span data-ttu-id="fd243-112">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="fd243-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
    
    1. <span data-ttu-id="fd243-113">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="fd243-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>
    
    1. <span data-ttu-id="fd243-114">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="fd243-114">From hello list of labs, select hello desired lab.</span></span>  
    
    1. <span data-ttu-id="fd243-115">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="fd243-115">On hello lab's blade, select **Configuration**.</span></span> 
    
    1. <span data-ttu-id="fd243-116">在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。</span><span class="sxs-lookup"><span data-stu-id="fd243-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>
    
    1. <span data-ttu-id="fd243-117">在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="fd243-117">On hello **Custom images** blade, Select **+Add**.</span></span> 
    
    1. <span data-ttu-id="fd243-118">在 hello**自訂映像**刀鋒視窗中，選取**VHD**。</span><span class="sxs-lookup"><span data-stu-id="fd243-118">On hello **Custom image** blade, select **VHD**.</span></span>
    
    1. <span data-ttu-id="fd243-119">在 hello **VHD**刀鋒視窗中，選取**使用 PowerShell 將 VHD 上傳**。</span><span class="sxs-lookup"><span data-stu-id="fd243-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>
    
        ![使用 PowerShell 上傳 VHD][0]
    
    1. <span data-ttu-id="fd243-121">hello**上傳映像使用 PowerShell**刀鋒視窗會顯示呼叫 toohello **Add-azurevhd** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fd243-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="fd243-122">hello 第一個參數 (*目的地*) 包含下列格式的 hello 中的 hello 實驗室 hello 儲存體帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="fd243-122">hello first parameter (*Destination*) contains hello storage account name for hello lab in hello following format:</span></span>
    
        <span data-ttu-id="fd243-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span><span class="sxs-lookup"><span data-stu-id="fd243-123">https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...</span></span> 

    1. <span data-ttu-id="fd243-124">請記 hello 儲存體帳戶名稱，因為它在稍後步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="fd243-124">Make note of hello storage account name as it is used in later steps.</span></span>
    
1. <span data-ttu-id="fd243-125">連接 tooan 使用存放裝置總管的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-125">Connect tooan Azure subscription account using Storage Explorer.</span></span>

    > [!TIP] 
    > 
    > <span data-ttu-id="fd243-126">儲存體總管支援數個連線選項。</span><span class="sxs-lookup"><span data-stu-id="fd243-126">Storage Explorer supports several connection options.</span></span> <span data-ttu-id="fd243-127">本節說明您的 Azure 訂用帳戶相關聯的連接 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-127">This section illustrates connecting tooa storage account associated with your Azure subscription.</span></span> <span data-ttu-id="fd243-128">toosee hello 儲存體總管支援其他連接選項，請參閱 toohello 文章[開始使用儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)。</span><span class="sxs-lookup"><span data-stu-id="fd243-128">toosee hello other connection options supported by Storage Explorer, refer toohello article, [Getting started with Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>
 
    1. <span data-ttu-id="fd243-129">開啟儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="fd243-129">Open Storage Explorer.</span></span>
    
    1. <span data-ttu-id="fd243-130">在儲存體總管中，選取 [Azure 帳戶設定]。</span><span class="sxs-lookup"><span data-stu-id="fd243-130">In Storage Explorer, select **Azure Account settings**.</span></span> 
    
        ![Azure 帳戶設定][1]
    
    1. <span data-ttu-id="fd243-132">hello 左的窗格會顯示您已登入的 hello Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-132">hello left pane displays hello Microsoft accounts you've logged in to.</span></span> <span data-ttu-id="fd243-133">tooconnect tooanother 帳戶，請選取**將帳戶加入**，並遵循 hello 對話方塊 toosign 使用至少一個有效的 Azure 訂閱相關聯的 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-133">tooconnect tooanother account, select **Add an account**, and follow hello dialogs toosign in with a Microsoft account that is associated with at least one active Azure subscription.</span></span>
    
        ![新增帳戶][2]
    
    1. <span data-ttu-id="fd243-135">一旦您已成功登入 Microsoft 帳戶，hello 左的窗格中填入 hello 與該帳戶相關聯的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-135">Once you successfully sign in with a Microsoft account, hello left pane populates with hello Azure subscriptions associated with that account.</span></span> <span data-ttu-id="fd243-136">選取 hello Azure 訂用帳戶與您想 toowork，，然後選取**套用**。</span><span class="sxs-lookup"><span data-stu-id="fd243-136">Select hello Azure subscriptions with which you want toowork, and then select **Apply**.</span></span> <span data-ttu-id="fd243-137">(選取**所有訂用帳戶**切換 hello 所有的選取範圍或列出任何 hello Azure 訂用帳戶。)</span><span class="sxs-lookup"><span data-stu-id="fd243-137">(Selecting **All subscriptions** toggles hello selection of all or none of hello listed Azure subscriptions.)</span></span>
    
        ![選取 Azure 訂用帳戶][3]
    
    1. <span data-ttu-id="fd243-139">hello 左的窗格會顯示 hello 與 hello 選取 Azure 訂用帳戶相關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd243-139">hello left pane displays hello storage accounts associated with hello selected Azure subscriptions.</span></span>
    
        ![已選取的 Azure 訂用帳戶][4]

1. <span data-ttu-id="fd243-141">找出 hello 實驗室儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="fd243-141">Locate hello lab's storage account:</span></span>

    1. <span data-ttu-id="fd243-142">Hello 存放裝置總管左窗格中，找出並展開 hello hello 擁有 hello 實驗室的 Azure 訂用帳戶節點。</span><span class="sxs-lookup"><span data-stu-id="fd243-142">In hello Storage Explorer left pane, locate, and expand hello node for hello Azure subscription that owns hello lab.</span></span>
    
    1. <span data-ttu-id="fd243-143">Hello 訂用帳戶的節點下，依序展開**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fd243-143">Under hello subscription's node, expand **Storage Accounts**.</span></span>

    1. <span data-ttu-id="fd243-144">展開 hello 實驗室儲存體帳戶節點 tooreveal 節點**Blob 容器**，**檔案共用**，**佇列**，和**資料表**。</span><span class="sxs-lookup"><span data-stu-id="fd243-144">Expand hello lab's storage account node tooreveal nodes for **Blob Containers**, **File Shares**, **Queues**, and **Tables**.</span></span>
    
    1. <span data-ttu-id="fd243-145">展開 hello **Blob 容器**節點。</span><span class="sxs-lookup"><span data-stu-id="fd243-145">Expand hello **Blob Containers** node.</span></span>
    
    1. <span data-ttu-id="fd243-146">Hello 右窗格中選取 hello 上傳 blob 容器 toodisplay 其內容。</span><span class="sxs-lookup"><span data-stu-id="fd243-146">Select hello uploads blob container toodisplay its contents in hello right pane.</span></span>
        
        ![上傳目錄][5]

1. <span data-ttu-id="fd243-148">使用儲存體總管的 hello VHD 檔案上傳：</span><span class="sxs-lookup"><span data-stu-id="fd243-148">Upload hello VHD file using Storage Explorer:</span></span>

    1. <span data-ttu-id="fd243-149">Hello 存放裝置總管右窗格中，您應該會看到 hello 中的 hello blob 清單**上載**hello 實驗室儲存體帳戶的 blob 容器。</span><span class="sxs-lookup"><span data-stu-id="fd243-149">In hello Storage Explorer right pane, you should see a listing of hello blobs in hello **uploads** blob container of hello lab's storage account.</span></span> <span data-ttu-id="fd243-150">在 hello blob 編輯器工具列上，選取 **上傳**</span><span class="sxs-lookup"><span data-stu-id="fd243-150">On hello blob editor toolbar, select **Upload**</span></span> 
        
        ![上傳按鈕][6]
    
    1. <span data-ttu-id="fd243-152">從 hello**上傳**下拉式選單中，選取**上傳檔案...**.</span><span class="sxs-lookup"><span data-stu-id="fd243-152">From hello **Upload** drop-down menu, select **Upload files...**.</span></span>
    
    1. <span data-ttu-id="fd243-153">在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號。</span><span class="sxs-lookup"><span data-stu-id="fd243-153">On hello **Upload files** dialog, select hello ellipsis.</span></span>
        
        ![選取檔案][8]  

    1. <span data-ttu-id="fd243-155">在 hello**選取檔案 tooupload**  對話方塊中，瀏覽 toohello 預期 VHD 檔案，選取它，並選取**開啟**。</span><span class="sxs-lookup"><span data-stu-id="fd243-155">On hello **Select files tooupload** dialog, browse toohello desired VHD file, select it, and then select **Open**.</span></span>
    
    1. <span data-ttu-id="fd243-156">當傳回 toohello**將檔案上傳** 對話方塊中，變更**Blob 類型**太**分頁 Blob**。</span><span class="sxs-lookup"><span data-stu-id="fd243-156">When returned toohello **Upload files** dialog, change **Blob type** too**Page Blob**.</span></span>
    
    1. <span data-ttu-id="fd243-157">選取 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="fd243-157">Select **Upload**.</span></span>

        ![選取檔案][9]  
    
    1. <span data-ttu-id="fd243-159">儲存體總管 hello**活動記錄檔** 窗格會顯示 hello 下載狀態 （與連結 toocancel hello 上傳）。</span><span class="sxs-lookup"><span data-stu-id="fd243-159">hello Storage Explorer **Activity Log** pane shows hello download status (along with links toocancel hello upload).</span></span> <span data-ttu-id="fd243-160">上傳 VHD 檔案 hello 程序可能很費時視 hello hello VHD 檔案大小和您的連線速度而定。</span><span class="sxs-lookup"><span data-stu-id="fd243-160">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span> 

        ![上傳檔案狀態][10]  

## <a name="next-steps"></a><span data-ttu-id="fd243-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd243-162">Next steps</span></span>

- [<span data-ttu-id="fd243-163">在 Azure DevTest Labs 從 VHD 檔案使用 hello Azure 入口網站中建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="fd243-163">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="fd243-164">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="fd243-164">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

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
