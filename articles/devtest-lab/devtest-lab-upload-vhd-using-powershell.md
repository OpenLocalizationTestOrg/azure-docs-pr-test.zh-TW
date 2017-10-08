---
title: "aaaUpload VHD 檔案使用 PowerShell tooAzure DevTest Labs |Microsoft 文件"
description: "上傳 VHD 檔案 toolab 的儲存體帳戶使用 PowerShell"
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
ms.openlocfilehash: 9c3ee96e212457b0ef8203714b419350cb97f895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-powershell"></a><span data-ttu-id="89248-103">上傳 VHD 檔案 toolab 的儲存體帳戶使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="89248-103">Upload VHD file toolab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="89248-104">在 Azure 的 DevTest Labs、 VHD 檔案可以是使用的 toocreate 自訂映像，也就是使用的 tooprovision 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="89248-104">In Azure DevTest Labs, VHD files can be used toocreate custom images, which are used tooprovision virtual machines.</span></span> <span data-ttu-id="89248-105">hello 下列步驟逐步引導您逐步使用 PowerShell tooupload 的 VHD 檔案 tooa 實驗室儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="89248-105">hello following steps walk you through using PowerShell tooupload a VHD file tooa lab's storage account.</span></span> <span data-ttu-id="89248-106">一旦您已上傳 VHD 檔案，hello[後續步驟 > 一節](#next-steps)列出說明如何 toocreate hello 從自訂映像上傳 VHD 檔案的某些文件。</span><span class="sxs-lookup"><span data-stu-id="89248-106">Once you've uploaded your VHD file, hello [Next steps section](#next-steps) lists some articles that illustrate how toocreate a custom image from hello uploaded VHD file.</span></span> <span data-ttu-id="89248-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="89248-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="89248-108">逐步指示</span><span class="sxs-lookup"><span data-stu-id="89248-108">Step-by-step instructions</span></span>

<span data-ttu-id="89248-109">hello 下列會引導您透過上傳 VHD 檔案使用 PowerShell tooAzure DevTest Labs 查核行程。</span><span class="sxs-lookup"><span data-stu-id="89248-109">hello following steps walk you through uploading a VHD file tooAzure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="89248-110">登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="89248-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="89248-111">選取**更多服務**，然後選取**DevTest Labs**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="89248-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="89248-112">從 hello 清單的實驗室中，選取 hello 所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="89248-112">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="89248-113">在 hello 實驗室刀鋒視窗中，選取 **組態**。</span><span class="sxs-lookup"><span data-stu-id="89248-113">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="89248-114">在 hello 實驗室**組態**刀鋒視窗中，選取**自訂映像 (Vhd)**。</span><span class="sxs-lookup"><span data-stu-id="89248-114">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="89248-115">在 hello**自訂映像**刀鋒視窗中，選取**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="89248-115">On hello **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="89248-116">在 hello**自訂映像**刀鋒視窗中，選取**VHD**。</span><span class="sxs-lookup"><span data-stu-id="89248-116">On hello **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="89248-117">在 hello **VHD**刀鋒視窗中，選取**使用 PowerShell 將 VHD 上傳**。</span><span class="sxs-lookup"><span data-stu-id="89248-117">On hello **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![使用 PowerShell 上傳 VHD](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="89248-119">在 hello**上傳映像使用 PowerShell**刀鋒視窗，複製 hello 產生 PowerShell 指令碼 tooa 文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="89248-119">On hello **Upload an image using PowerShell** blade, copy hello generated PowerShell script tooa text editor.</span></span>

1. <span data-ttu-id="89248-120">修改 hello **LocalFilePath** hello 參數**Add-azurevhd** hello 想 tooupload 的 VHD 檔案的 cmdlet toopoint toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="89248-120">Modify hello **LocalFilePath** parameter of hello **Add-AzureVhd** cmdlet toopoint toohello location of hello VHD file you want tooupload.</span></span>

1. <span data-ttu-id="89248-121">在 PowerShell 提示字元執行 hello **Add-azurevhd** cmdlet (以修改 hello **LocalFilePath**參數)。</span><span class="sxs-lookup"><span data-stu-id="89248-121">At a PowerShell prompt, run hello **Add-AzureVhd** cmdlet (with hello modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="89248-122">上傳 VHD 檔案 hello 程序可能很費時視 hello hello VHD 檔案大小和您的連線速度而定。</span><span class="sxs-lookup"><span data-stu-id="89248-122">hello process of uploading a VHD file can be lengthy depending on hello size of hello VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89248-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89248-123">Next steps</span></span>

- [<span data-ttu-id="89248-124">在 Azure DevTest Labs 從 VHD 檔案使用 hello Azure 入口網站中建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="89248-124">Create a custom image in Azure DevTest Labs from a VHD file using hello Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="89248-125">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="89248-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
