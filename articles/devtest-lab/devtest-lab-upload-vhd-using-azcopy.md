---
title: "使用 AzCopy 將 VHD 檔案上傳到 Azure DevTest Labs | Microsoft Docs"
description: "使用 AzCopy 將 VHD 檔案上傳到實驗室的儲存體帳戶"
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
ms.openlocfilehash: a4f43354740d9f17570932b0b9c753f46d67dc33
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-azcopy"></a><span data-ttu-id="2417c-103">使用 AzCopy 將 VHD 檔案上傳到實驗室的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="2417c-103">Upload VHD file to lab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="2417c-104">在 Azure DevTest Labs 中，可以使用 VHD 檔案來建立自訂映像，這些映像可用來佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2417c-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="2417c-105">下列步驟將逐步引導您使用 AzCopy 命令列公用程式，將 VHD 檔案上傳到實驗室的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2417c-105">The following steps walk you through using the AzCopy command-line utility to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="2417c-106">在您上傳 VHD 檔案之後，[後續步驟](#next-steps)一節會列出一些說明如何從所上傳的 VHD 檔案建立自訂映像的文章。</span><span class="sxs-lookup"><span data-stu-id="2417c-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="2417c-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="2417c-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="2417c-108">AzCopy 是一個僅適用於 Windows 的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="2417c-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="2417c-109">逐步指示</span><span class="sxs-lookup"><span data-stu-id="2417c-109">Step-by-step instructions</span></span>

<span data-ttu-id="2417c-110">下列步驟將逐步引導您使用 [AzCopy](http://aka.ms/downloadazcopy) 將 VHD 檔案上傳到 Azure DevTest Labs。</span><span class="sxs-lookup"><span data-stu-id="2417c-110">The following steps walk you through uploading a VHD file to Azure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="2417c-111">使用 Azure 入口網站來取得實驗室的儲存體帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="2417c-111">Get the name of the lab's storage account using the Azure portal:</span></span>

1. <span data-ttu-id="2417c-112">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="2417c-112">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2417c-113">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="2417c-113">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="2417c-114">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="2417c-114">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="2417c-115">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="2417c-115">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="2417c-116">在實驗室的 [組態] 刀鋒視窗上，選取 [自訂映像 (VHD)]。</span><span class="sxs-lookup"><span data-stu-id="2417c-116">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="2417c-117">在 [自訂映像] 刀鋒視窗上，選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="2417c-117">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="2417c-118">在 [自訂映像] 刀鋒視窗上，選取 [VHD]。</span><span class="sxs-lookup"><span data-stu-id="2417c-118">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="2417c-119">在 [VHD] 刀鋒視窗上，選取 [使用 PowerShell 上傳 VHD]。</span><span class="sxs-lookup"><span data-stu-id="2417c-119">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![使用 PowerShell 上傳 VHD](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="2417c-121">[使用 PowerShell 上傳映像] 刀鋒視窗會顯示一個對 **Add-AzureVhd** Cmdlet 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="2417c-121">The **Upload an image using PowerShell** blade displays a call to the **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="2417c-122">第一個參數 (*Destination*) 包含 Blob 容器 (*uploads*) 的 URI，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="2417c-122">The first parameter (*Destination*) contains the URI for a blob container (*uploads*) in the following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="2417c-123">記下完整的 URI，因為在稍後的步驟中將會用到。</span><span class="sxs-lookup"><span data-stu-id="2417c-123">Make note of the full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="2417c-124">使用 AzCopy 來上傳 VHD 檔案：</span><span class="sxs-lookup"><span data-stu-id="2417c-124">Upload the VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="2417c-125">[下載並安裝最新版的 AzCopy](http://aka.ms/downloadazcopy)。</span><span class="sxs-lookup"><span data-stu-id="2417c-125">[Download and install the latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="2417c-126">開啟命令視窗，然後瀏覽至 AzCopy 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="2417c-126">Open a command window and navigate to the AzCopy installation directory.</span></span> <span data-ttu-id="2417c-127">您可以視需要將 AzCopy 安裝位置新增到您的系統路徑。</span><span class="sxs-lookup"><span data-stu-id="2417c-127">Optionally, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="2417c-128">AzCopy 預設會安裝到下列目錄：</span><span class="sxs-lookup"><span data-stu-id="2417c-128">By default, AzCopy is installed to the following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="2417c-129">使用儲存體帳戶金鑰和 Blob 容器 URI，在命令提示字元中執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="2417c-129">Using the storage account key and blob container URI, run the following command at the command prompt.</span></span> <span data-ttu-id="2417c-130">*vhdFileName* 值必須包含在引號中。</span><span class="sxs-lookup"><span data-stu-id="2417c-130">The *vhdFileName* value needs to be in quotes.</span></span> <span data-ttu-id="2417c-131">視 VHD 檔案大小及您的連線速度而定，上傳 VHD 檔案的程序可能會相當長。</span><span class="sxs-lookup"><span data-stu-id="2417c-131">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="2417c-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2417c-132">Next steps</span></span>

- [<span data-ttu-id="2417c-133">使用 Azure 入口網站在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="2417c-133">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="2417c-134">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="2417c-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)