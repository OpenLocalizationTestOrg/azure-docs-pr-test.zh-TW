---
title: "aaaSelect Windows VM 映像在 Azure 中 |Microsoft 文件"
description: "了解如何 toouse Azure PowerSHell toodetermine hello 發行者、 方案、 SKU 和 Marketplace 的 VM 映像的版本。"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="151f1-103">Toofind Windows VM hello Azure powershell 的 Azure Marketplace 中的映像</span><span class="sxs-lookup"><span data-stu-id="151f1-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="151f1-104">本主題描述 toouse Azure PowerShell toofind VM hello Azure Marketplace 中的映像。</span><span class="sxs-lookup"><span data-stu-id="151f1-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="151f1-105">當您建立 Windows VM 時，請使用此資訊 toospecify Marketplace 映像。</span><span class="sxs-lookup"><span data-stu-id="151f1-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="151f1-106">請確定您已安裝，並最新設定 hello [Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="151f1-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="151f1-107">常用 Windows 映像表</span><span class="sxs-lookup"><span data-stu-id="151f1-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="151f1-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="151f1-108">PublisherName</span></span> | <span data-ttu-id="151f1-109">提供項目</span><span class="sxs-lookup"><span data-stu-id="151f1-109">Offer</span></span> | <span data-ttu-id="151f1-110">SKU</span><span class="sxs-lookup"><span data-stu-id="151f1-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="151f1-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-112">WindowsServer</span></span> |<span data-ttu-id="151f1-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="151f1-113">2016-Datacenter</span></span> |
| <span data-ttu-id="151f1-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-115">WindowsServer</span></span> |<span data-ttu-id="151f1-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="151f1-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="151f1-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-118">WindowsServer</span></span> |<span data-ttu-id="151f1-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="151f1-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="151f1-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-121">WindowsServer</span></span> |<span data-ttu-id="151f1-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="151f1-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="151f1-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-124">WindowsServer</span></span> |<span data-ttu-id="151f1-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="151f1-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="151f1-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="151f1-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="151f1-127">WindowsServer</span></span> |<span data-ttu-id="151f1-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="151f1-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="151f1-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="151f1-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="151f1-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="151f1-130">DynamicsNAV</span></span> |<span data-ttu-id="151f1-131">2017</span><span class="sxs-lookup"><span data-stu-id="151f1-131">2017</span></span> |
| <span data-ttu-id="151f1-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="151f1-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="151f1-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="151f1-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="151f1-134">2016</span><span class="sxs-lookup"><span data-stu-id="151f1-134">2016</span></span> |
| <span data-ttu-id="151f1-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="151f1-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="151f1-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="151f1-136">SQL2016-WS2016</span></span> |<span data-ttu-id="151f1-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="151f1-137">Enterprise</span></span> |
| <span data-ttu-id="151f1-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="151f1-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="151f1-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="151f1-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="151f1-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="151f1-140">Enterprise</span></span> |
| <span data-ttu-id="151f1-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="151f1-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="151f1-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="151f1-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="151f1-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="151f1-143">2012R2</span></span> |
| <span data-ttu-id="151f1-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="151f1-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="151f1-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="151f1-145">WindowsServerEssentials</span></span> |<span data-ttu-id="151f1-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="151f1-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="151f1-147">尋找特定映像</span><span class="sxs-lookup"><span data-stu-id="151f1-147">Find specific images</span></span>


<span data-ttu-id="151f1-148">在建立新的虛擬機器與 Azure 資源管理員時，在某些情況下您需要 toospecify 映像具有下列映像屬性的 hello hello 組合：</span><span class="sxs-lookup"><span data-stu-id="151f1-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="151f1-149">發佈者</span><span class="sxs-lookup"><span data-stu-id="151f1-149">Publisher</span></span>
* <span data-ttu-id="151f1-150">提供項目</span><span class="sxs-lookup"><span data-stu-id="151f1-150">Offer</span></span>
* <span data-ttu-id="151f1-151">SKU</span><span class="sxs-lookup"><span data-stu-id="151f1-151">SKU</span></span>

<span data-ttu-id="151f1-152">例如，使用這些值以 hello[組 AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet 或使用資源群組範本中，您必須指定建立的 VM toobe hello 型別。</span><span class="sxs-lookup"><span data-stu-id="151f1-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="151f1-153">如果您需要 toodetermine 這些值，您可以執行 hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher)， [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer)，和[Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlettoonavigate hello 映像。</span><span class="sxs-lookup"><span data-stu-id="151f1-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="151f1-154">您要判斷這些值：</span><span class="sxs-lookup"><span data-stu-id="151f1-154">You determine these values:</span></span>

1. <span data-ttu-id="151f1-155">清單 hello 映像的發行者。</span><span class="sxs-lookup"><span data-stu-id="151f1-155">List hello image publishers.</span></span>
2. <span data-ttu-id="151f1-156">針對指定的發行者，列出其提供項目。</span><span class="sxs-lookup"><span data-stu-id="151f1-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="151f1-157">針對指定的提供項目，列出其 SKU。</span><span class="sxs-lookup"><span data-stu-id="151f1-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="151f1-158">首先，列出 hello 發行者以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="151f1-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="151f1-159">填入您所選的發行者的名稱，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="151f1-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="151f1-160">填入您所選的提供項目名稱，然後執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="151f1-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="151f1-161">從 hello hello 輸出`Get-AzureRMVMImageSku`命令時，您會有新的虛擬機器所需 toospecify hello 映像的所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="151f1-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="151f1-162">hello 下列範例示範完整的範例：</span><span class="sxs-lookup"><span data-stu-id="151f1-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="151f1-163">輸出：</span><span class="sxs-lookup"><span data-stu-id="151f1-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="151f1-164">Hello"MicrosoftWindowsServer"發行者：</span><span class="sxs-lookup"><span data-stu-id="151f1-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="151f1-165">輸出：</span><span class="sxs-lookup"><span data-stu-id="151f1-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="151f1-166">Hello"WindowsServer 」 提供：</span><span class="sxs-lookup"><span data-stu-id="151f1-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="151f1-167">輸出：</span><span class="sxs-lookup"><span data-stu-id="151f1-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="151f1-168">從這個清單中，複製 hello 選擇 SKU 名稱，而且您擁有 hello 所有 hello 資訊`Set-AzureRMVMSourceImage`PowerShell cmdlet 或資源群組範本。</span><span class="sxs-lookup"><span data-stu-id="151f1-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="151f1-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="151f1-169">Next steps</span></span>
<span data-ttu-id="151f1-170">現在您可以選擇明確地說 hello 映像您會想 toouse。</span><span class="sxs-lookup"><span data-stu-id="151f1-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="151f1-171">toocreate 虛擬機器，快速利用剛找到的 hello 映像資訊，請參閱[使用 PowerShell 建立 Windows 虛擬機器](quick-create-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="151f1-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
