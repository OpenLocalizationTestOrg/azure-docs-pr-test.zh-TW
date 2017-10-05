---
title: "使用 PowerShell 將 VHD 檔案上傳到 Azure DevTest Labs | Microsoft Docs"
description: "使用 PowerShell 將 VHD 檔案上傳到實驗室的儲存體帳戶"
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
ms.openlocfilehash: 3c43ef77b8fa10cd6dbd726968264f32f7a3dd0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-vhd-file-to-labs-storage-account-using-powershell"></a><span data-ttu-id="d8c09-103">使用 PowerShell 將 VHD 檔案上傳到實驗室的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d8c09-103">Upload VHD file to lab's storage account using PowerShell</span></span>

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

<span data-ttu-id="d8c09-104">在 Azure DevTest Labs 中，可以使用 VHD 檔案來建立自訂映像，這些映像可用來佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d8c09-104">In Azure DevTest Labs, VHD files can be used to create custom images, which are used to provision virtual machines.</span></span> <span data-ttu-id="d8c09-105">下列步驟將逐步引導您使用 PowerShell，將 VHD 檔案上傳到實驗室的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d8c09-105">The following steps walk you through using PowerShell to upload a VHD file to a lab's storage account.</span></span> <span data-ttu-id="d8c09-106">在您上傳 VHD 檔案之後，[後續步驟](#next-steps)一節會列出一些說明如何從所上傳的 VHD 檔案建立自訂映像的文章。</span><span class="sxs-lookup"><span data-stu-id="d8c09-106">Once you've uploaded your VHD file, the [Next steps section](#next-steps) lists some articles that illustrate how to create a custom image from the uploaded VHD file.</span></span> <span data-ttu-id="d8c09-107">如需有關 Azure 中磁碟和 VHD 的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../virtual-machines/linux/about-disks-and-vhds.md)</span><span class="sxs-lookup"><span data-stu-id="d8c09-107">For more information about disks and VHDs in Azure, see [About disks and VHDs for virtual machines](../virtual-machines/linux/about-disks-and-vhds.md)</span></span>

## <a name="step-by-step-instructions"></a><span data-ttu-id="d8c09-108">逐步指示</span><span class="sxs-lookup"><span data-stu-id="d8c09-108">Step-by-step instructions</span></span>

<span data-ttu-id="d8c09-109">下列步驟將逐步引導您使用 PowerShell 將 VHD 檔案上傳到 Azure DevTest Labs。</span><span class="sxs-lookup"><span data-stu-id="d8c09-109">The following steps walk you through uploading a VHD file to Azure DevTest Labs using PowerShell.</span></span> 

1. <span data-ttu-id="d8c09-110">登入 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="d8c09-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="d8c09-111">選取 [更多服務]，然後從清單中選取 [DevTest Labs]。</span><span class="sxs-lookup"><span data-stu-id="d8c09-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="d8c09-112">從實驗室清單中，選取所需的實驗室。</span><span class="sxs-lookup"><span data-stu-id="d8c09-112">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="d8c09-113">在實驗室的刀鋒視窗上，選取 [組態] 。</span><span class="sxs-lookup"><span data-stu-id="d8c09-113">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="d8c09-114">在實驗室的 [組態] 刀鋒視窗上，選取 [自訂映像 (VHD)]。</span><span class="sxs-lookup"><span data-stu-id="d8c09-114">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="d8c09-115">在 [自訂映像] 刀鋒視窗上，選取 [+新增]。</span><span class="sxs-lookup"><span data-stu-id="d8c09-115">On the **Custom images** blade, Select **+Add**.</span></span> 

1. <span data-ttu-id="d8c09-116">在 [自訂映像] 刀鋒視窗上，選取 [VHD]。</span><span class="sxs-lookup"><span data-stu-id="d8c09-116">On the **Custom image** blade, select **VHD**.</span></span>

1. <span data-ttu-id="d8c09-117">在 [VHD] 刀鋒視窗上，選取 [使用 PowerShell 上傳 VHD]。</span><span class="sxs-lookup"><span data-stu-id="d8c09-117">On the **VHD** blade, select **Upload a VHD using PowerShell**.</span></span>

    ![使用 PowerShell 上傳 VHD](./media/devtest-lab-upload-vhd-using-powershell/upload-image-using-psh.png)

1. <span data-ttu-id="d8c09-119">在 [使用 PowerShell 上傳映像] 刀鋒視窗中，將產生的 PowerShell 指令碼複製到文字編輯器。</span><span class="sxs-lookup"><span data-stu-id="d8c09-119">On the **Upload an image using PowerShell** blade, copy the generated PowerShell script to a text editor.</span></span>

1. <span data-ttu-id="d8c09-120">修改 **Add-AzureVhd** Cmdlet 的 **LocalFilePath** 參數，以指向您要上傳的 VHD 檔案位置。</span><span class="sxs-lookup"><span data-stu-id="d8c09-120">Modify the **LocalFilePath** parameter of the **Add-AzureVhd** cmdlet to point to the location of the VHD file you want to upload.</span></span>

1. <span data-ttu-id="d8c09-121">在 PowerShell 提示字元中，執行 **Add-AzureVhd** Cmdlet (使用修改後的 **LocalFilePath** 參數)。</span><span class="sxs-lookup"><span data-stu-id="d8c09-121">At a PowerShell prompt, run the **Add-AzureVhd** cmdlet (with the modified **LocalFilePath** parameter).</span></span>

> [!WARNING] 
> 
> <span data-ttu-id="d8c09-122">視 VHD 檔案大小及您的連線速度而定，上傳 VHD 檔案的程序可能會相當長。</span><span class="sxs-lookup"><span data-stu-id="d8c09-122">The process of uploading a VHD file can be lengthy depending on the size of the VHD file and your connection speed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8c09-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d8c09-123">Next steps</span></span>

- [<span data-ttu-id="d8c09-124">使用 Azure 入口網站在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="d8c09-124">Create a custom image in Azure DevTest Labs from a VHD file using the Azure portal</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="d8c09-125">使用 PowerShell 在 Azure DevTest Labs 中從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="d8c09-125">Create a custom image in Azure DevTest Labs from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
