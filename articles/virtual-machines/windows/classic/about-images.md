---
title: "關於 Windows 虛擬機器的映像 | Microsoft Docs"
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
ms.openlocfilehash: d421cee0becabdf81d865036d0c98b12b077152b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="about-images-for-windows-virtual-machines"></a><span data-ttu-id="7cd09-103">關於 Windows 虛擬機器的映像</span><span class="sxs-lookup"><span data-stu-id="7cd09-103">About images for Windows virtual machines</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7cd09-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="7cd09-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7cd09-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="7cd09-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7cd09-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="7cd09-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7cd09-107">如需在 Resource Manager 模型中尋找和使用映像的詳細資訊，請參閱[這裡](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7cd09-107">For information about finding and using images in the Resource Manager model, see [here](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a><span data-ttu-id="7cd09-108">使用映像</span><span class="sxs-lookup"><span data-stu-id="7cd09-108">Working with images</span></span>

<span data-ttu-id="7cd09-109">您可以使用 Azure PowerShell 模組和 Azure 入口網站，來管理 Azure 訂用帳戶可使用的映像。</span><span class="sxs-lookup"><span data-stu-id="7cd09-109">You can use the Azure PowerShell module and the Azure portal to manage the images available to your Azure subscription.</span></span> <span data-ttu-id="7cd09-110">Azure PowerShell 模組提供更多命令選項，讓您可以準確地指出想要查看或執行的項目。</span><span class="sxs-lookup"><span data-stu-id="7cd09-110">The Azure PowerShell module provides more command options, so you can pinpoint exactly what you want to see or do.</span></span> <span data-ttu-id="7cd09-111">Azure 入口網站提供一個 GUI，供許多日常系統管理工作使用。</span><span class="sxs-lookup"><span data-stu-id="7cd09-111">The Azure portal provides a GUI for many of the everyday administrative tasks.</span></span>

<span data-ttu-id="7cd09-112">以下是一些使用 Azure PowerShell 模組的範例。</span><span class="sxs-lookup"><span data-stu-id="7cd09-112">Here are some examples that use the Azure PowerShell module.</span></span>

* <span data-ttu-id="7cd09-113">**取得所有映像**：`Get-AzureVMImage` 會傳回您目前訂用帳戶中可用的所有映像清單︰您的映像和 Azure 或協力廠商所提供的映像。</span><span class="sxs-lookup"><span data-stu-id="7cd09-113">**Get all images**:`Get-AzureVMImage`returns a list of all the images available in your current subscription: your images and those provided by Azure or partners.</span></span> <span data-ttu-id="7cd09-114">產生的清單可能很長。</span><span class="sxs-lookup"><span data-stu-id="7cd09-114">The resulting list could be large.</span></span> <span data-ttu-id="7cd09-115">下面的範例示範如何取得較短的清單。</span><span class="sxs-lookup"><span data-stu-id="7cd09-115">The next examples show how to get a shorter list.</span></span>
* <span data-ttu-id="7cd09-116">**取得映像系列**：`Get-AzureVMImage | select ImageFamily`顯示字串 **ImageFamily** 屬性以取得映像系列清單。</span><span class="sxs-lookup"><span data-stu-id="7cd09-116">**Get image families**:`Get-AzureVMImage | select ImageFamily` gets a list of image families by showing strings **ImageFamily** property.</span></span>
* <span data-ttu-id="7cd09-117">**取得特定系列中的所有映像**：`Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span><span class="sxs-lookup"><span data-stu-id="7cd09-117">**Get all images in a specific family**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`</span></span>
* <span data-ttu-id="7cd09-118">**尋找 VM 映像**：`Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` 這個 Cmdlet 運作的方式是篩選 DataDiskConfiguration 屬性，僅適用於 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="7cd09-118">**Find VM Images**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` This cmdlet works by filtering the DataDiskConfiguration property, which only applies to VM Images.</span></span> <span data-ttu-id="7cd09-119">此範例也會篩選輸出並僅列出標籤和映像名稱。</span><span class="sxs-lookup"><span data-stu-id="7cd09-119">This example also filters the output to only the label and image name.</span></span>
* <span data-ttu-id="7cd09-120">**儲存一般化映像**：`Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span><span class="sxs-lookup"><span data-stu-id="7cd09-120">**Save a generalized image**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`</span></span>
* <span data-ttu-id="7cd09-121">**儲存特殊化映像**：`Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span><span class="sxs-lookup"><span data-stu-id="7cd09-121">**Save a specialized image**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`</span></span>

  > [!TIP]
  > <span data-ttu-id="7cd09-122">需要使用 OSState 參數，才能建立 VM 映像，其中包含作業系統磁碟和連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7cd09-122">The OSState parameter is required to create a VM image, which includes the operating system disk and attached data disks.</span></span> <span data-ttu-id="7cd09-123">如果您不使用參數，Cmdlet 就會建立 OS 映像。</span><span class="sxs-lookup"><span data-stu-id="7cd09-123">If you don’t use the parameter, the cmdlet creates an OS image.</span></span> <span data-ttu-id="7cd09-124">根據作業系統磁碟是否準備為重複使用，參數的值會表示是否要將映像一般化或特殊化。</span><span class="sxs-lookup"><span data-stu-id="7cd09-124">The value of the parameter indicates whether the image is generalized or specialized, based on whether the operating system disk has been prepared for reuse.</span></span>

* <span data-ttu-id="7cd09-125">**删除映像**：`Remove-AzureVMImage –ImageName "MyOldVmImage"`</span><span class="sxs-lookup"><span data-stu-id="7cd09-125">**Delete an image**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cd09-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7cd09-126">Next Steps</span></span>
<span data-ttu-id="7cd09-127">您也可以[使用 Azure 入口網站來建立 Windows 機器](tutorial.md)。</span><span class="sxs-lookup"><span data-stu-id="7cd09-127">You can also [create a Windows machine using the Azure portal](tutorial.md).</span></span>
