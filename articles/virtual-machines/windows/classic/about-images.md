---
title: "aaaAbout 映像的 Windows 虛擬機器 |Microsoft 文件"
description: "了解如何將映像與 Azure 中的 Windows 虛擬機器搭配使用。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="6990c-103">關於 Windows 虛擬機器的映像</span><span class="sxs-lookup"><span data-stu-id="6990c-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6990c-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="6990c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6990c-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="6990c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6990c-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="6990c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6990c-107">如需尋找與 hello 資源管理員模型中使用映像相關資訊，請參閱[這裡](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="6990c-107">For information about finding and using images in hello Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="6990c-108">使用映像</span><span class="sxs-lookup"><span data-stu-id="6990c-108">Working with images</span></span>

<span data-ttu-id="6990c-109">您可以使用 hello Azure PowerShell 模組和 hello Azure 入口網站 toomanage hello 映像可用 tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6990c-109">You can use hello Azure PowerShell module and hello Azure portal toomanage hello images available tooyour Azure subscription.</span></span> <span data-ttu-id="6990c-110">hello Azure PowerShell 模組可提供更多的命令選項，以便您查出到底是什麼 toosee 或執行。</span><span class="sxs-lookup"><span data-stu-id="6990c-110">hello Azure PowerShell module provides more command options, so you can pinpoint exactly what you want toosee or do.</span></span> <span data-ttu-id="6990c-111">hello Azure 入口網站提供的 GUI 許多 hello 日常系統管理工作。</span><span class="sxs-lookup"><span data-stu-id="6990c-111">hello Azure portal provides a GUI for many of hello everyday administrative tasks.</span></span>

<span data-ttu-id="6990c-112">以下是一些使用 hello Azure PowerShell 模組的範例。</span><span class="sxs-lookup"><span data-stu-id="6990c-112">Here are some examples that use hello Azure PowerShell module.</span></span>

* <span data-ttu-id="6990c-113">**取得所有映像**:`Get-AzureVMImage`傳回所有可用在您目前的訂用帳戶中的 hello 映像的清單： 您的映像和 Azure 或協力廠商所提供。</span><span class="sxs-lookup"><span data-stu-id="6990c-113">**Get all images**:`Get-AzureVMImage`returns a list of all hello images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="6990c-114">hello 產生清單可能是大。</span><span class="sxs-lookup"><span data-stu-id="6990c-114">hello resulting list could be large.</span></span> <span data-ttu-id="6990c-115">hello 下一個範例顯示如何 tooget 較短的清單。</span><span class="sxs-lookup"><span data-stu-id="6990c-115">hello next examples show how tooget a shorter list.</span></span>
* <span data-ttu-id="6990c-116">**取得映像系列**：`Get-AzureVMImage | select ImageFamily`顯示字串 **ImageFamily** 屬性以取得映像系列清單。</span><span class="sxs-lookup"><span data-stu-id="6990c-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="6990c-117">**取得特定系列中的所有映像**：`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="6990c-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="6990c-118">**尋找 VM 映像**:`Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName`這個指令程式的運作方式是篩選 hello DataDiskConfiguration 屬性只適用於 tooVM 映像。</span><span class="sxs-lookup"><span data-stu-id="6990c-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering hello DataDiskConfiguration property, which only applies tooVM Images.</span></span> <span data-ttu-id="6990c-119">此範例也會篩選 hello 輸出 tooonly hello 標籤和映像名稱。</span><span class="sxs-lookup"><span data-stu-id="6990c-119">This example also filters hello output tooonly hello label and image name.</span></span>
* <span data-ttu-id="6990c-120">**儲存一般化映像**：`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="6990c-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="6990c-121">**儲存特殊化映像**：`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="6990c-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="6990c-122">hello OSState 參數是必要的 toocreate VM 映像，其中包含 hello 作業系統磁碟，並連接資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="6990c-122">hello OSState parameter is required toocreate a VM image, which includes hello operating system disk and attached data disks.</span></span> <span data-ttu-id="6990c-123">如果您不使用 hello 參數，hello cmdlet 會建立 OS 映像。</span><span class="sxs-lookup"><span data-stu-id="6990c-123">If you don’t use hello parameter, hello cmdlet creates an OS image.</span></span> <span data-ttu-id="6990c-124">hello hello 參數值會指出 hello 映像為一般化或特殊化，根據 hello 作業系統磁碟是否已準備好要重複使用。</span><span class="sxs-lookup"><span data-stu-id="6990c-124">hello value of hello parameter indicates whether hello image is generalized or specialized, based on whether hello operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="6990c-125">**删除映像**：`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="6990c-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="6990c-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6990c-126">Next Steps</span></span>
<span data-ttu-id="6990c-127">您也可以[建立一部使用 hello Azure 入口網站的 Windows 電腦](tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="6990c-127">You can also [create a Windows machine using hello Azure portal](tutorial.md).</span></span>
