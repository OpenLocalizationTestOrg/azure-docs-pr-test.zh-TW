---
title: "aaaUpgrade Azure 虛擬機器規模集 |Microsoft 文件"
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
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a><span data-ttu-id="d6d68-103">升級虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="d6d68-103">Upgrade a virtual machine scale set</span></span>
<span data-ttu-id="d6d68-104">本文描述您可以制定 OS 更新 tooan Azure 虛擬機器擴展集完全不需要停機。</span><span class="sxs-lookup"><span data-stu-id="d6d68-104">This article describes how you can roll out an OS update tooan Azure virtual machine scale set without any downtime.</span></span> <span data-ttu-id="d6d68-105">在此情況下，作業系統更新包括變更 hello 版本或 SKU 的 hello OS 或變更 hello 的自訂映像的 URI。</span><span class="sxs-lookup"><span data-stu-id="d6d68-105">In this context, an OS update involves changing hello version or SKU of hello OS or changing hello URI of a custom image.</span></span> <span data-ttu-id="d6d68-106">在不需停機的情況下進行更新意謂著一次更新一部虛擬機器，或依群組 (例如一次一個容錯網域) 更新虛擬機器，而不是全部一起更新。</span><span class="sxs-lookup"><span data-stu-id="d6d68-106">Updating without downtime means updating virtual machines one at a time or in groups (such as one fault domain at a time) rather than all at once.</span></span> <span data-ttu-id="d6d68-107">透過這種方式，任何非升級中的虛擬機器都可繼續執行。</span><span class="sxs-lookup"><span data-stu-id="d6d68-107">By doing so, any virtual machines that are not being upgraded can keep running.</span></span>

<span data-ttu-id="d6d68-108">tooavoid 模稜兩可，讓我們來區別四種類型的作業系統更新，您可能會想 tooperform:</span><span class="sxs-lookup"><span data-stu-id="d6d68-108">tooavoid ambiguity, let’s distinguish four types of OS update you might want tooperform:</span></span>

* <span data-ttu-id="d6d68-109">變更 hello 版本或平台映像的 SKU。</span><span class="sxs-lookup"><span data-stu-id="d6d68-109">Changing hello version or SKU of a platform image.</span></span> <span data-ttu-id="d6d68-110">例如，變更 Ubuntu 14.04.201506100 14.04.2-LTS 版本 too14.04.201507060，或變更 hello Ubuntu 15.10/最新 SKU too16.04.0-LTS/latest。</span><span class="sxs-lookup"><span data-stu-id="d6d68-110">For example, changing Ubuntu 14.04.2-LTS version from 14.04.201506100 too14.04.201507060, or changing hello Ubuntu 15.10/latest SKU too16.04.0-LTS/latest.</span></span> <span data-ttu-id="d6d68-111">本文涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="d6d68-111">This scenario is covered in this article.</span></span>
* <span data-ttu-id="d6d68-112">變更 hello 指向 tooa 新版本，您所建立的自訂映像的 URI (**屬性** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **映像** > **uri**)。</span><span class="sxs-lookup"><span data-stu-id="d6d68-112">Changing hello URI that points tooa new version of a custom image you built (**properties** > **virtualMachineProfile** > **storageProfile** > **osDisk** > **image** > **uri**).</span></span> <span data-ttu-id="d6d68-113">本文涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="d6d68-113">This scenario is covered in this article.</span></span>
* <span data-ttu-id="d6d68-114">變更使用 Azure 受管理的磁碟建立規模集的 hello 影像參考。</span><span class="sxs-lookup"><span data-stu-id="d6d68-114">Changing hello image reference of a scale set that was created using Azure Managed Disks.</span></span>
* <span data-ttu-id="d6d68-115">修補程式的虛擬機器內 hello 從作業系統 （這個範例包含安裝的安全性修補程式和執行 Windows Update）。</span><span class="sxs-lookup"><span data-stu-id="d6d68-115">Patching hello OS from within a virtual machine (examples of this include installing a security patch and running Windows Update).</span></span> <span data-ttu-id="d6d68-116">支援此案例，但本文並未涵蓋此案例。</span><span class="sxs-lookup"><span data-stu-id="d6d68-116">This scenario is supported but not covered in this article.</span></span>

<span data-ttu-id="d6d68-117">這裡未涵蓋隨 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) 一起部署的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="d6d68-117">Virtual machine scale sets that are deployed as part of an [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) cluster are not covered here.</span></span> <span data-ttu-id="d6d68-118">如需修補 Service Fabric 的詳細資訊，請參閱[在 Service Fabric 叢集中修補 Windows OS](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application)。</span><span class="sxs-lookup"><span data-stu-id="d6d68-118">See [Patch Windows OS in your Service Fabric cluster](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) for more information about patching Service Fabric.</span></span>

<span data-ttu-id="d6d68-119">hello 基本順序變更 hello OS 版本/平台映像的 SKU 或 hello URI 自訂影像看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="d6d68-119">hello basic sequence for changing hello OS version/SKU of a platform image or hello URI of a custom image looks as follows:</span></span>

1. <span data-ttu-id="d6d68-120">收到 hello 虛擬機器擴充集模型。</span><span class="sxs-lookup"><span data-stu-id="d6d68-120">Get hello virtual machine scale set model.</span></span>
2. <span data-ttu-id="d6d68-121">變更 hello 版本、 SKU、 映像參考或 hello 模型中的 URI 值。</span><span class="sxs-lookup"><span data-stu-id="d6d68-121">Change hello version, SKU, image reference, or URI value in hello model.</span></span>
3. <span data-ttu-id="d6d68-122">更新 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="d6d68-122">Update hello model.</span></span>
4. <span data-ttu-id="d6d68-123">請勿*manualUpgrade*呼叫 hello hello 規模集中的虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="d6d68-123">Do a *manualUpgrade* call on hello virtual machines in hello scale set.</span></span> <span data-ttu-id="d6d68-124">此步驟中，才會相關如果*upgradePolicy*設定得**手動**集中您的標尺。</span><span class="sxs-lookup"><span data-stu-id="d6d68-124">This step is only relevant if *upgradePolicy* is set too**Manual** in your scale set.</span></span> <span data-ttu-id="d6d68-125">如果設定太**自動**，hello 的所有虛擬機器都升級，因此會造成停機時間。</span><span class="sxs-lookup"><span data-stu-id="d6d68-125">If it is set too**Automatic**, all hello virtual machines are upgraded at once, thus causing downtime.</span></span>

<span data-ttu-id="d6d68-126">請注意這項資訊，我們來看看您無法更新在擴展集在 PowerShell 中，而藉由使用 REST API hello hello 版本的方式。</span><span class="sxs-lookup"><span data-stu-id="d6d68-126">With this information in mind, let’s see how you could update hello version of a scale set in PowerShell, and by using hello REST API.</span></span> <span data-ttu-id="d6d68-127">這些範例中涵蓋的平台映像的 hello 大小寫，但本文章提供足夠的資訊讓您 tooadapt 此程序 tooa 自訂映像。</span><span class="sxs-lookup"><span data-stu-id="d6d68-127">These examples cover hello case of a platform image, but this article provides enough information for you tooadapt this process tooa custom image.</span></span>

## <a name="powershell"></a><span data-ttu-id="d6d68-128">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6d68-128">PowerShell</span></span>
<span data-ttu-id="d6d68-129">這個範例會更新 Windows 虛擬機器規模集 （建立 toohello 新版 4.0.20160229。</span><span class="sxs-lookup"><span data-stu-id="d6d68-129">This example updates a Windows virtual machine scale set (creating toohello new version 4.0.20160229.</span></span> <span data-ttu-id="d6d68-130">在更新之後 hello 模型，則它會更新一個虛擬機器執行個體一次。</span><span class="sxs-lookup"><span data-stu-id="d6d68-130">After updating hello model, it does an update one virtual machine instance at a time.</span></span>

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

<span data-ttu-id="d6d68-131">如果您要更新 hello URI，而不是變更平台映像版本的自訂映像，取代 hello 「 組 hello 新的版本 」 將更新的命令列 hello 來源影像 URI。</span><span class="sxs-lookup"><span data-stu-id="d6d68-131">If you are updating hello URI for a custom image instead of changing a platform image version, replace hello “set hello new version” line with a command that will update hello source image URI.</span></span> <span data-ttu-id="d6d68-132">例如，如果 hello 規模集不使用 Azure 受管理的磁碟建立的 hello 更新看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="d6d68-132">For example, if hello scale set was created without using Azure Managed Disks, hello update would look like this:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

<span data-ttu-id="d6d68-133">如果自訂映像基礎規模調整集合會建立使用 Azure 受管理的磁碟，則會更新 hello 影像參考。</span><span class="sxs-lookup"><span data-stu-id="d6d68-133">If a custom image based scale set was created using Azure Managed Disks, then hello image reference would be updated.</span></span> <span data-ttu-id="d6d68-134">例如：</span><span class="sxs-lookup"><span data-stu-id="d6d68-134">For example:</span></span>

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a><span data-ttu-id="d6d68-135">hello REST API</span><span class="sxs-lookup"><span data-stu-id="d6d68-135">hello REST API</span></span>
<span data-ttu-id="d6d68-136">以下是幾個使用 hello Azure REST API tooroll OS 版本更新的 Python 範例。</span><span class="sxs-lookup"><span data-stu-id="d6d68-136">Here are a couple of Python examples that use hello Azure REST API tooroll out an OS version update.</span></span> <span data-ttu-id="d6d68-137">同時使用 hello 輕量型[azurerm](https://pypi.python.org/pypi/azurerm) Azure REST API 的包裝函式的函式 toodo hello 標尺上 GET 的程式庫設定模型的 PUT 與更新的模型。</span><span class="sxs-lookup"><span data-stu-id="d6d68-137">Both use hello lightweight [azurerm](https://pypi.python.org/pypi/azurerm) library of Azure REST API wrapper functions toodo a GET on hello scale set model, followed by a PUT with an updated model.</span></span> <span data-ttu-id="d6d68-138">它們也查看虛擬機器執行個體檢視 tooidentify hello 虛擬機器的更新網域。</span><span class="sxs-lookup"><span data-stu-id="d6d68-138">They also look at virtual machine instances views tooidentify hello virtual machines by update domain.</span></span>

### <a name="vmssupgrade"></a><span data-ttu-id="d6d68-139">Vmssupgrade</span><span class="sxs-lookup"><span data-stu-id="d6d68-139">Vmssupgrade</span></span>
 <span data-ttu-id="d6d68-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools)是否 Python 指令碼使用 tooroll 出 OS 升級 tooa 執行虛擬機器擴展集一次一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="d6d68-140">[Vmssupgrade](https://github.com/gbowerman/vmsstools) is a Python script that's used tooroll out an OS upgrade tooa running virtual machine scale set one update domain at a time.</span></span>

![選擇虛擬機器或更新網域的 vmssupgrade 指令碼](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

<span data-ttu-id="d6d68-142">此指令碼可讓您選擇特定虛擬機器 tooupdate 或指定的更新網域。</span><span class="sxs-lookup"><span data-stu-id="d6d68-142">This script lets you choose specific virtual machines tooupdate or specify an update domain.</span></span> <span data-ttu-id="d6d68-143">它支援變更平台映像版本，或變更 hello 的自訂映像的 URI。</span><span class="sxs-lookup"><span data-stu-id="d6d68-143">It supports changing a platform image version or changing hello URI of a custom image.</span></span>

### <a name="vmsseditor"></a><span data-ttu-id="d6d68-144">Vmsseditor</span><span class="sxs-lookup"><span data-stu-id="d6d68-144">Vmsseditor</span></span>
<span data-ttu-id="d6d68-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) 是虛擬機器擴展集的一般用途編輯器，能夠以熱力圖的形式顯示虛擬機器狀態，其中一個資料列代表一個更新網域。</span><span class="sxs-lookup"><span data-stu-id="d6d68-145">[Vmsseditor](https://github.com/gbowerman/vmssdashboard) is a general-purpose editor for virtual machine scale sets that shows virtual machine status as a heatmap where one row represents one update domain.</span></span> <span data-ttu-id="d6d68-146">在其他方面，您可以擴展集 hello 模型使用新的版本、 SKU 或更新自訂映像的 URI，，，然後挑選容錯網域 tooupgrade。</span><span class="sxs-lookup"><span data-stu-id="d6d68-146">Among other things, you can update hello model for a scale set with a new version, SKU, or custom image URI, and then pick fault domains tooupgrade.</span></span> <span data-ttu-id="d6d68-147">當您這樣做時，所有更新網域中的 hello 虛擬機器將都會升級的 toohello 新模型。</span><span class="sxs-lookup"><span data-stu-id="d6d68-147">When you do so, all hello virtual machines in that update domain are upgraded toohello new model.</span></span> <span data-ttu-id="d6d68-148">或者，您可以根據您選擇的 hello 批次大小的輪流升級。</span><span class="sxs-lookup"><span data-stu-id="d6d68-148">Alternatively, you can do a rolling upgrade based on hello batch size of your choice.</span></span>  

<span data-ttu-id="d6d68-149">hello 下列螢幕擷取畫面顯示 Ubuntu 14.04 2LTS 14.04.201507060 版本設定標尺的模型。</span><span class="sxs-lookup"><span data-stu-id="d6d68-149">hello following screenshot shows a model of a scale set for Ubuntu 14.04-2LTS version 14.04.201507060.</span></span> <span data-ttu-id="d6d68-150">更多選擇已加入 toothis 工具執行這個螢幕擷取畫面之後。</span><span class="sxs-lookup"><span data-stu-id="d6d68-150">Many more options have been added toothis tool since this screenshot was taken.</span></span>

![Ubuntu 14.04-2LTS 的擴展集 vmsseditor 模型](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

<span data-ttu-id="d6d68-152">按一下 之後**升級**然後**取得詳細資料**，UD 0 中的虛擬機器啟動 tooupdate。</span><span class="sxs-lookup"><span data-stu-id="d6d68-152">After you click **Upgrade** and then **Get Details**, virtual machines in UD 0 start tooupdate.</span></span>

![顯示更新進行中的 vmsseditor](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

