---
title: "升級 Azure 虛擬機器擴展集 | Microsoft Docs"
description: "升級 Azure 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: c7093e221ff8fe69ded1cfbce4f3ddeb1a195666
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="8a862-103">升級虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="8a862-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="8a862-104">本文說明如何在不需停機的情況下，對 Azure 虛擬機器擴展集推出 OS 更新。</span><span class="sxs-lookup"><span data-stu-id="8a862-104">This article describes how you can roll out an OS update to an Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="8a862-105">在此背景環境下，OS 更新包括變更 OS 的版本或 SKU，或是變更自訂映像的 URI。</span><span class="sxs-lookup"><span data-stu-id="8a862-105">In this context, an OS update involves changing the version or SKU of the OS or changing the URI of a custom image.</span></span> <span data-ttu-id="8a862-106">在不需停機的情況下進行更新意謂著一次更新一部虛擬機器，或依群組 (例如一次一個容錯網域) 更新虛擬機器，而不是全部一起更新。</span><span class="sxs-lookup"><span data-stu-id="8a862-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="8a862-107">透過這種方式，任何非升級中的虛擬機器都可繼續執行。</span><span class="sxs-lookup"><span data-stu-id="8a862-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="8a862-108">為了避免混淆不清，讓我們區分您可能會想要執行的四種 OS 更新：</span><span class="sxs-lookup"><span data-stu-id="8a862-108">To avoid ambiguity, let’s distinguish four types of OS update you might want to perform:</span></span>

* <span data-ttu-id="8a862-109">變更平台映像的版本或 SKU。</span><span class="sxs-lookup"><span data-stu-id="8a862-109">Changing the version or SKU of a platform image.</span></span> <span data-ttu-id="8a862-110">例如，將 Ubuntu 14.04.2-LTS 版本從 14.04.201506100 變更為 14.04.201507060，或將 Ubuntu 15.10/最新 SKU 變更為 16.04.0-LTS/最新 SKU。</span><span class="sxs-lookup"><span data-stu-id="8a862-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 to 14.04.201507060, or changing the Ubuntu 15.10/latest SKU to 16.04.0-LTS/latest.</span></span> <span data-ttu-id="8a862-111">本文涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="8a862-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="8a862-112">變更指向您所建立的新版本自訂映像的 URI (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**)。</span><span class="sxs-lookup"><span data-stu-id="8a862-112">Changing the URI that points to a new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="8a862-113">本文涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="8a862-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="8a862-114">變更使用 Azure 受控磁碟所建立之擴展集的映像參考。</span><span class="sxs-lookup"><span data-stu-id="8a862-114">Changing the image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="8a862-115">從虛擬機器內修補 OS (範例包括安裝安全性修補程式並執行 Windows Update)。</span><span class="sxs-lookup"><span data-stu-id="8a862-115">Patching the OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="8a862-116">支援此案例，但本文並未涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="8a862-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="8a862-117">這裡未涵蓋隨 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) 一起部署的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="8a862-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="8a862-118">如需修補 Service Fabric 的詳細資訊，請參閱[在 Service Fabric 叢集中修補 Windows OS](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)。</span><span class="sxs-lookup"><span data-stu-id="8a862-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="8a862-119">變更平台映像 OS 版本/SKU 或自訂映像 URI 的基本順序看起來如下：</span><span class="sxs-lookup"><span data-stu-id="8a862-119">The basic sequence for changing the OS version/SKU of a platform image or the URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="8a862-120">取得虛擬機器擴展集模型。</span><span class="sxs-lookup"><span data-stu-id="8a862-120">Get the virtual machine scale set model.</span></span>
2. <span data-ttu-id="8a862-121">變更模型中的版本、SKU、映像參考或 URI 值。</span><span class="sxs-lookup"><span data-stu-id="8a862-121">Change the version, SKU, image reference, or URI value in the model.</span></span>
3. <span data-ttu-id="8a862-122">更新模型。</span><span class="sxs-lookup"><span data-stu-id="8a862-122">Update the model.</span></span>
4. <span data-ttu-id="8a862-123">對擴展集中的虛擬機器進行 *manualUpgrade* 呼叫。</span><span class="sxs-lookup"><span data-stu-id="8a862-123">Do a *manualUpgrade* call on the virtual machines in the scale set.</span></span> <span data-ttu-id="8a862-124">只有當您擴展集中的 *upgradePolicy* 設定為 [手動] 時，此步驟才相關。</span><span class="sxs-lookup"><span data-stu-id="8a862-124">This step is only relevant if *upgradePolicy* is set to **Manual** in your scale set.</span></span> <span data-ttu-id="8a862-125">如果它是設定為 [自動] ，則會同時升級所有虛擬機器，因而造成停機。</span><span class="sxs-lookup"><span data-stu-id="8a862-125">If it is set to **Automatic**, all the virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="8a862-126">將這項資訊謹記在心，讓我們看看如何在 PowerShell 中使用 REST API 來更新擴展集的版本。</span><span class="sxs-lookup"><span data-stu-id="8a862-126">With this information in mind, let’s see how you could update the version of a scale set in PowerShell, and by using the REST API.</span></span> <span data-ttu-id="8a862-127">這些範例涵蓋平台映像的案例，但本文所提供的資訊已足以讓您將此程序應用在自訂映像上。</span><span class="sxs-lookup"><span data-stu-id="8a862-127">These examples cover the case of a platform image, but this article provides enough information for you to adapt this process to a custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="8a862-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a862-128">PowerShell</span></span>
<span data-ttu-id="8a862-129">此範例會將 Windows 虛擬機器擴展集更新 (建立) 成新版本 4.0.20160229。</span><span class="sxs-lookup"><span data-stu-id="8a862-129">This example updates a Windows virtual machine scale set (creating to the new version 4.0.20160229.</span></span> <span data-ttu-id="8a862-130">更新完模型之後，它會一次更新一個虛擬機器執行個體。</span><span class="sxs-lookup"><span data-stu-id="8a862-130">After updating the model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get the VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update the virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="8a862-131">如果您更新的是自訂映像的 URI，而不是變更平台映像版本，請以更新來源映像 URI 的命令取代 “set the new version” 行。</span><span class="sxs-lookup"><span data-stu-id="8a862-131">If you are updating the URI for a custom image instead of changing a platform image version, replace the “set the new version” line with a command that will update the source image URI.</span></span> <span data-ttu-id="8a862-132">例如，如果擴展集不是使用 Azure 受控磁碟所建立，更新會如下所示：</span><span class="sxs-lookup"><span data-stu-id="8a862-132">For example, if the scale set was created without using Azure Managed Disks, the update would look like this:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="8a862-133">如果使用 Azure 受控磁碟建立了以自訂映像為基礎的擴展集，則會更新映像參考。</span><span class="sxs-lookup"><span data-stu-id="8a862-133">If a custom image based scale set was created using Azure Managed Disks, then the image reference would be updated.</span></span> <span data-ttu-id="8a862-134">例如：</span><span class="sxs-lookup"><span data-stu-id="8a862-134">For example:</span></span>

```powershell
# set the new version in the model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="the-rest-api"></a><span data-ttu-id="8a862-135">REST API</span><span class="sxs-lookup"><span data-stu-id="8a862-135">The REST API</span></span>
<span data-ttu-id="8a862-136">以下是幾個使用 Azure REST API 來推出 OS 版本更新的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="8a862-136">Here are a couple of Python examples that use the Azure REST API to roll out an OS version update.</span></span> <span data-ttu-id="8a862-137">兩者都使用 Azure REST API 包裝函式的輕量型 [azurerm](https://pypi.python.org/pypi/azurerm) 程式庫對擴展集模型執行 GET，然後搭配更新的模型執行 PUT。</span><span class="sxs-lookup"><span data-stu-id="8a862-137">Both use the lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions to do a GET on the scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="8a862-138">它們也會查看虛擬機器執行個體檢視，以依據更新網域識別虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8a862-138">They also look at virtual machine instances views to identify the virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="8a862-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="8a862-139">Vmssupgrade</span></span>
 <span data-ttu-id="8a862-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) 是一個 Python 指令碼，能夠用來一次以一個更新網域為範圍，對執行中的虛擬機器擴展集推出 OS 升級。</span><span class="sxs-lookup"><span data-stu-id="8a862-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used to roll out an OS upgrade to a running virtual machine scale set one update domain at a time.</span></span>

![選擇虛擬機器或更新網域的 vmssupgrade 指令碼](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="8a862-142">此指令碼能讓您選擇要更新的特定虛擬機器，或是指定更新網域。</span><span class="sxs-lookup"><span data-stu-id="8a862-142">This script lets you choose specific virtual machines to update or specify an update domain.</span></span> <span data-ttu-id="8a862-143">它支援變更平台映像版本，或變更自訂映像的 URI。</span><span class="sxs-lookup"><span data-stu-id="8a862-143">It supports changing a platform image version or changing the URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="8a862-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="8a862-144">Vmsseditor</span></span>
<span data-ttu-id="8a862-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 是虛擬機器擴展集的一般用途編輯器，能夠以熱力圖的形式顯示虛擬機器狀態，其中一個資料列代表一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="8a862-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="8a862-146">除此之外，您還可以使用新的版本、SKU 或自訂映像 URI 來更新擴展集的模型，然後選擇要升級的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="8a862-146">Among other things, you can update the model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains to upgrade.</span></span> <span data-ttu-id="8a862-147">當您這麼做時，該更新網域中的所有虛擬機器都會升級成新模型。</span><span class="sxs-lookup"><span data-stu-id="8a862-147">When you do so, all the virtual machines in that update domain are upgraded to the new model.</span></span> <span data-ttu-id="8a862-148">或者，您也可以根據所選的批次大小執行輪流升級。</span><span class="sxs-lookup"><span data-stu-id="8a862-148">Alternatively, you can do a rolling upgrade based on the batch size of your choice.</span></span>  

<span data-ttu-id="8a862-149">下列螢幕擷取畫面顯示 Ubuntu 14.04-2LTS 版本 14.04.201507060 的擴展集模型。</span><span class="sxs-lookup"><span data-stu-id="8a862-149">The following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="8a862-150">自從拍攝此螢幕擷取畫面之後，有許多其他選項已經新增到此工具中。</span><span class="sxs-lookup"><span data-stu-id="8a862-150">Many more options have been added to this tool since this screenshot was taken.</span></span>

![Ubuntu 14.04-2LTS 的擴展集 vmsseditor 模型](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="8a862-152">當您依序按一下 [升級] 和 [取得詳細資料] 之後，UD 0 中的虛擬機器將會開始更新。</span><span class="sxs-lookup"><span data-stu-id="8a862-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start to update.</span></span>

![顯示更新進行中的 vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

