---
title: "aaaUpload VHD 檔案使用 AzCopy tooAzure DevTest Labs |Microsoft 文件"
description: "上傳 VHD 檔案 toolab 的儲存體帳戶，使用 AzCopy"
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
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a><span data-ttu-id="52191-103">上傳 VHD 檔案 toolab 的儲存體帳戶，使用 AzCopy</span><span class="sxs-lookup"><span data-stu-id="52191-103">Upload VHD file toolab's storage account using AzCopy</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="52191-104">在 Azure 的 DevTest Labs、 VHD 檔案可以是使用的 toocreate 自訂映像，也就是使用的 tooprovision 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="52191-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="52191-105">hello 步驟引導您完成使用 hello AzCopy 命令列公用程式 tooupload 的 VHD 檔案 tooa 實驗室儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="52191-105">hello following steps walk you through using hello AzCopy command-line utility tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="52191-106">一旦您已上傳 VHD 檔案，hello[後續步驟 > 一節](#next-steps)列出說明如何 toocreate hello 從自訂映像上傳 VHD 檔案的某些文件。</span><span class="sxs-lookup"><span data-stu-id="52191-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="52191-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="52191-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

> [!NOTE] 
>  
> <span data-ttu-id="52191-108">AzCopy 是一個僅適用於 Windows 的命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="52191-108">AzCopy is a Windows-only command-line utility.</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="52191-109">逐步指示</span><span class="sxs-lookup"><span data-stu-id="52191-109">Step-by-step instructions</span></span>

<span data-ttu-id="52191-110">下列步驟查核行程您上傳 VHD 檔案使用 tooAzure DevTest Labs hello [AzCopy](http://aka.ms/downloadazcopy)。</span><span class="sxs-lookup"><span data-stu-id="52191-110">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using [AzCopy](http://aka.ms/downloadazcopy).</span></span> 

1. <span data-ttu-id="52191-111">收到 hello 使用 hello Azure 入口網站的 hello 實驗室儲存體帳戶名稱：</span><span class="sxs-lookup"><span data-stu-id="52191-111">Get hello name of hello lab's storage account using hello Azure portal:</span></span>

1. <span data-ttu-id="52191-112">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="52191-112">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="52191-113">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="52191-113">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="52191-114">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="52191-114">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="52191-115">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="52191-115">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="52191-116">在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。</span><span class="sxs-lookup"><span data-stu-id="52191-116">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="52191-117">在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="52191-117">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="52191-118">在 hello**自訂映像**刀鋒視窗中，選取**VHD**。</span><span class="sxs-lookup"><span data-stu-id="52191-118">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="52191-119">在 hello **VHD**刀鋒視窗中，選取**使用 PowerShell 將 VHD 上傳**。</span><span class="sxs-lookup"><span data-stu-id="52191-119">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![使用 PowerShell 上傳 VHD](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. <span data-ttu-id="52191-121">hello**上傳映像使用 PowerShell**刀鋒視窗會顯示呼叫 toohello **Add-azurevhd** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="52191-121">hello **Upload an image using PowerShell** blade displays a call toohello **Add-AzureVhd** cmdlet.</span></span> <span data-ttu-id="52191-122">hello 第一個參數 (*目的地*) 包含 hello URI blob 容器 (*上載*) 在 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="52191-122">hello first parameter (*Destination*) contains hello URI for a blob container (*uploads*) in hello following format:</span></span>

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. <span data-ttu-id="52191-123">請記下 hello 完整 URI，因為它用於接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="52191-123">Make note of hello full URI as it is used in later steps.</span></span>

1. <span data-ttu-id="52191-124">使用 AzCopy 的 hello VHD 檔案上傳：</span><span class="sxs-lookup"><span data-stu-id="52191-124">Upload hello VHD file using AzCopy:</span></span>
 
1. <span data-ttu-id="52191-125">[下載並安裝新版 AzCopy hello](http://aka.ms/downloadazcopy)。</span><span class="sxs-lookup"><span data-stu-id="52191-125">[Download and install hello latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

1. <span data-ttu-id="52191-126">開啟命令視窗，並瀏覽 toohello AzCopy 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="52191-126">Open a command window and navigate toohello AzCopy installation directory.</span></span> <span data-ttu-id="52191-127">（選擇性） 您可以加入 hello AzCopy 安裝位置 tooyour 系統路徑。</span><span class="sxs-lookup"><span data-stu-id="52191-127">Optionally, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="52191-128">根據預設，AzCopy 會是已安裝的 toohello 下列目錄：</span><span class="sxs-lookup"><span data-stu-id="52191-128">By default, AzCopy is installed toohello following directory:</span></span>

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. <span data-ttu-id="52191-129">使用 hello 儲存體帳戶金鑰和 blob 容器的 URI，執行下列命令在 hello 命令提示字元的 hello。</span><span class="sxs-lookup"><span data-stu-id="52191-129">Using hello storage account key and blob container URI, run hello following command at hello command prompt.</span></span> <span data-ttu-id="52191-130">hello *vhdFileName*值必須以引號括住 toobe。</span><span class="sxs-lookup"><span data-stu-id="52191-130">hello *vhdFileName* value needs toobe in quotes.</span></span> <span data-ttu-id="52191-131">上傳 VHD 檔案 hello 程序可能很費時視 hello hello VHD 檔案大小和您的連線速度而定。</span><span class="sxs-lookup"><span data-stu-id="52191-131">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a><span data-ttu-id="52191-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="52191-132">Next steps</span></span>

- [<span data-ttu-id="52191-133">在 Azure DevTest Labs 從 VHD 檔案使用 hello Azure 入口網站中建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="52191-133">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="52191-134">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="52191-134">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)