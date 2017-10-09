---
title: "使用大型的 Azure 虛擬機器擴展集 aaaWorking |Microsoft 文件"
description: "您的需要 tooknow toouse 大型 Azure 虛擬機器擴充集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a><span data-ttu-id="80269-103">使用大型的虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="80269-103">Working with large virtual machine scale sets</span></span>
<span data-ttu-id="80269-104">您現在可以建立 Azure[虛擬機器擴展集](/azure/virtual-machine-scale-sets/)too1，000 Vm 上的容量。</span><span class="sxs-lookup"><span data-stu-id="80269-104">You can now create Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) with a capacity of up too1,000 VMs.</span></span> <span data-ttu-id="80269-105">本文件_大型虛擬機器規模集_定義為在擴展集能夠調整 toogreater 超過 100 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="80269-105">In this document, a _large virtual machine scale set_ is defined as a scale set capable of scaling toogreater than 100 VMs.</span></span> <span data-ttu-id="80269-106">此容量是由擴展集屬性 (_singlePlacementGroup=False_) 所設定。</span><span class="sxs-lookup"><span data-stu-id="80269-106">This capability is set by a scale set property (_singlePlacementGroup=False_).</span></span> 

<span data-ttu-id="80269-107">大規模的特定部分設定，例如負載平衡和容錯網域有不同的行為 tooa 標準規模集。</span><span class="sxs-lookup"><span data-stu-id="80269-107">Certain aspects of large scale sets, such as load balancing and fault domains behave differently tooa standard scale set.</span></span> <span data-ttu-id="80269-108">本文件說明的中的大規模 hello 特性，並說明哪些需要 tooknow toosuccessfully 中使用這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="80269-108">This document explains hello characteristics of large scale sets, and describes what you need tooknow toosuccessfully use them in your applications.</span></span> 

<span data-ttu-id="80269-109">常見的方法進行部署大的規模的雲端基礎結構是 toocreate 一組_延展單位_，例如藉由建立多個 Vm 跨多個 Vnet 和儲存體帳戶中調整設定。</span><span class="sxs-lookup"><span data-stu-id="80269-109">A common approach for deploying cloud infrastructure at large scale is toocreate a set of _scale units_, for example by creating multiple VMs scale sets across multiple VNETs and storage accounts.</span></span> <span data-ttu-id="80269-110">這種方法讓您更輕鬆管理比較 toosingle Vm，而且多個擴充單元可用於許多應用程式，尤其是需要其他可堆疊的元件，例如多個虛擬網路和端點。</span><span class="sxs-lookup"><span data-stu-id="80269-110">This approach provides easier management compared toosingle VMs, and multiple scale units are useful for many applications, particularly those that require other stackable components like multiple virtual networks and endpoints.</span></span> <span data-ttu-id="80269-111">如果您的應用程式需要單一大型叢集但，它可以是單一的小數位數的設定 too1，000 Vm 更直接 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="80269-111">If your application requires a single large cluster however, it can be more straightforward toodeploy a single scale set of up too1,000 VMs.</span></span> <span data-ttu-id="80269-112">範例案例包括集中式的巨量資料部署，或是需要可簡單管理大型背景工作節點集區的計算方格。</span><span class="sxs-lookup"><span data-stu-id="80269-112">Example scenarios include centralized big data deployments, or compute grids requiring simple management of a large pool of worker nodes.</span></span> <span data-ttu-id="80269-113">與 VM 規模調整集合結合[附加資料磁碟](virtual-machine-scale-sets-attached-disks.md)，大規模集可讓您 toodeploy 可擴充的基礎結構，包含數千個核心和 pb 計的儲存體，以單一作業。</span><span class="sxs-lookup"><span data-stu-id="80269-113">Combined with VM scale set [attached data disks](virtual-machine-scale-sets-attached-disks.md), large scale sets enable you toodeploy a scalable infrastructure consisting of thousands of cores and petabytes of storage, as a single operation.</span></span>

## <a name="placement-groups"></a><span data-ttu-id="80269-114">放置群組</span><span class="sxs-lookup"><span data-stu-id="80269-114">Placement groups</span></span> 
<span data-ttu-id="80269-115">構成_大型_設定特殊的小數位數不 hello 的 Vm，但如果 hello 數目_放置群組_其中的內容。</span><span class="sxs-lookup"><span data-stu-id="80269-115">What makes a _large_ scale set special is not hello number of VMs, but hello number of _placement groups_ it contains.</span></span> <span data-ttu-id="80269-116">放置群組是建構類似 tooan Azure 可用性設定組，與它自己的容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="80269-116">A placement group is a construct similar tooan Azure availability set, with its own fault domains and upgrade domains.</span></span> <span data-ttu-id="80269-117">根據預設，擴展集包含一個大小上限為 100 個 VM 的位置群組。</span><span class="sxs-lookup"><span data-stu-id="80269-117">By default, a scale set consists of a single placement group with a maximum size of 100 VMs.</span></span> <span data-ttu-id="80269-118">如果小數位數設定的屬性稱為_singlePlacementGroup_設定 too_false_，hello 規模集可能會組成多個位置群組，而有 0-1000 的範圍 Vm。</span><span class="sxs-lookup"><span data-stu-id="80269-118">If a scale set property called _singlePlacementGroup_ is set too_false_, hello scale set can be composed of multiple placement groups and has a range of 0-1,000 VMs.</span></span> <span data-ttu-id="80269-119">當設定 toohello 預設值是_true_，小數位數是由單一的位置 群組中，以及範圍為 0-100 Vm。</span><span class="sxs-lookup"><span data-stu-id="80269-119">When set toohello default value of _true_, a scale set is composed of a single placement group, and has a range of 0-100 VMs.</span></span>

## <a name="checklist-for-using-large-scale-sets"></a><span data-ttu-id="80269-120">使用大型擴展集的檢查清單</span><span class="sxs-lookup"><span data-stu-id="80269-120">Checklist for using large scale sets</span></span>
<span data-ttu-id="80269-121">toodecide 是否可大規模集合的有效地使用您的應用程式。 請考慮下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="80269-121">toodecide whether your application can make effective use of large scale sets, consider hello following requirements:</span></span>

- <span data-ttu-id="80269-122">大型擴展集需要 Azure 受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="80269-122">Large scale sets require Azure Managed Disks.</span></span> <span data-ttu-id="80269-123">所建立的擴展集若非使用受控磁碟，則需要多個儲存體帳戶 (每 20 個 VM 一個)。</span><span class="sxs-lookup"><span data-stu-id="80269-123">Scale sets that are not created with Managed Disks require multiple storage accounts (one for every 20 VMs).</span></span> <span data-ttu-id="80269-124">設計的 toowork 獨佔方式使用受管理磁碟 tooreduce 儲存體管理額外負荷，以及 tooavoid hello 的風險執行訂用帳戶限制的儲存體帳戶中的大規模集合。</span><span class="sxs-lookup"><span data-stu-id="80269-124">Large scale sets are designed toowork exclusively with Managed Disks tooreduce your storage management overhead, and tooavoid hello risk of running into subscription limits for storage accounts.</span></span> <span data-ttu-id="80269-125">如果您未使用受管理的磁碟，小數位數組是有限的 too100 Vm。</span><span class="sxs-lookup"><span data-stu-id="80269-125">If you do not use Managed Disks, your scale set is limited too100 VMs.</span></span>
- <span data-ttu-id="80269-126">從 Azure Marketplace 映像建立的規模集就能相應 too1，000 Vm。</span><span class="sxs-lookup"><span data-stu-id="80269-126">Scale sets created from Azure Marketplace images can scale up too1,000 VMs.</span></span>
- <span data-ttu-id="80269-127">擴展集所建立的自訂映像 （VM 映像您建立及上傳您自己） 目前可以 too100 Vm 向上延展。</span><span class="sxs-lookup"><span data-stu-id="80269-127">Scale sets created from custom images (VM images you create and upload yourself) can currently scale up too100 VMs.</span></span>
- <span data-ttu-id="80269-128">第 4 層負載平衡及 hello Azure 負載平衡器尚未支援多個位置群組所組成的小數位數組。</span><span class="sxs-lookup"><span data-stu-id="80269-128">Layer-4 load balancing with hello Azure Load Balancer is not yet supported for scale sets composed of multiple placement groups.</span></span> <span data-ttu-id="80269-129">如果您需要 toouse hello Azure 負載平衡器進行確定 hello 擴展集是設定的 toouse 單一位置群組，也就是 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="80269-129">If you need toouse hello Azure Load Balancer make sure hello scale set is configured toouse a single placement group, which is hello default setting.</span></span>
- <span data-ttu-id="80269-130">支援所有的小數位數組 7 層負載平衡及 hello Azure 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="80269-130">Layer-7 load balancing with hello Azure Application Gateway is supported for all scale sets.</span></span>
- <span data-ttu-id="80269-131">擴展集以單一子網路定義-請確定您的子網路具有位址空間夠大，您需要的所有 hello vm。</span><span class="sxs-lookup"><span data-stu-id="80269-131">A scale set is defined with a single subnet - make sure your subnet has an address space large enough for all hello VMs you need.</span></span> <span data-ttu-id="80269-132">根據預設小數位數設定 overprovisions （建立額外的 Vm，在部署時，或向外延展，則不需收費的） tooimprove 部署可靠性和效能。</span><span class="sxs-lookup"><span data-stu-id="80269-132">By default a scale set overprovisions (creates extra VMs at deployment time or when scaling out, which you are not charged for) tooimprove deployment reliability and performance.</span></span> <span data-ttu-id="80269-133">允許的位址空間 20%大於 hello 您計劃要 tooscale 中 Vm 的數目。</span><span class="sxs-lookup"><span data-stu-id="80269-133">Allow for an address space 20% greater than hello number of VMs you plan tooscale to.</span></span>
- <span data-ttu-id="80269-134">如果您計劃 toodeploy 許多 Vm，您的運算核心配額限制可能需要增加 toobe。</span><span class="sxs-lookup"><span data-stu-id="80269-134">If you are planning toodeploy many VMs, your Compute core quota limits may need toobe increased.</span></span>
- <span data-ttu-id="80269-135">容錯網域和升級網域只會在放置群組內保持一致。</span><span class="sxs-lookup"><span data-stu-id="80269-135">Fault domains and upgrade domains are only consistent within a placement group.</span></span> <span data-ttu-id="80269-136">這個架構不會變更 hello 整體標尺的可用性設定，因為 Vm 平均分散於不同的實體硬體，但也不會表示，如果您需要的 tooguarantee 兩個 Vm 位於不同的硬體，請確定這些主機位於不同的錯誤中的網域 hello 相同位置 群組。</span><span class="sxs-lookup"><span data-stu-id="80269-136">This architecture does not change hello overall availability of a scale set, as VMs are evenly distributed across distinct physical hardware, but it does means that if you need tooguarantee two VMs are on different hardware, make sure they are in different fault domains in hello same placement group.</span></span> <span data-ttu-id="80269-137">容錯網域和放置群組的識別碼會顯示在 hello_執行個體檢視_的小數位數設定的 VM。</span><span class="sxs-lookup"><span data-stu-id="80269-137">Fault domain and placement group ID are shown in hello _instance view_ of a scale set VM.</span></span> <span data-ttu-id="80269-138">您可以檢視 hello 擴展集 VM 執行個體檢視中 hello [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="80269-138">You can view hello instance view of a scale set VM in hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>


## <a name="creating-a-large-scale-set"></a><span data-ttu-id="80269-139">建立大型擴展集</span><span class="sxs-lookup"><span data-stu-id="80269-139">Creating a large scale set</span></span>
<span data-ttu-id="80269-140">當您建立 hello Azure 入口網站中設定的標尺時，您可以允許它 tooscale toomultiple 放置群組設定 hello_限制 tooa 單一位置群組_在 hello 選項 too_False__基本概念_刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="80269-140">When you create a scale set in hello Azure portal, you can allow it tooscale toomultiple placement groups by setting hello _Limit tooa single placement group_ option too_False_ in hello _Basics_ blade.</span></span> <span data-ttu-id="80269-141">使用此選項設定 too_False_，您可以指定_執行個體計數_too1，000 的值。</span><span class="sxs-lookup"><span data-stu-id="80269-141">With this option set too_False_, you can specify an _Instance count_ value of up too1,000.</span></span>

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

<span data-ttu-id="80269-142">您可以建立使用 hello 設定大型 VM 規模調整[Azure CLI](https://github.com/Azure/azure-cli) _az vmss 建立_命令。</span><span class="sxs-lookup"><span data-stu-id="80269-142">You can create a large VM scale set using hello [Azure CLI](https://github.com/Azure/azure-cli) _az vmss create_ command.</span></span> <span data-ttu-id="80269-143">此命令會設定智慧型預設值，例如子網路大小根據 hello_執行個體計數_引數：</span><span class="sxs-lookup"><span data-stu-id="80269-143">This command sets intelligent defaults such as subnet size based on hello _instance-count_ argument:</span></span>

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
<span data-ttu-id="80269-144">請注意該 hello _vmss 建立_命令預設某些設定值，如果您未指定。</span><span class="sxs-lookup"><span data-stu-id="80269-144">Note that hello _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="80269-145">toosee hello 可用的選項，您可以覆寫，請再試一次：</span><span class="sxs-lookup"><span data-stu-id="80269-145">toosee hello available options that you can override, try:</span></span>
```bash
az vmss create --help
```

<span data-ttu-id="80269-146">如果您要建立大規模撰寫 Azure Resource Manager 範本設定，請確定 hello 範本建立 Azure 受管理磁碟為基礎的小數位數集。</span><span class="sxs-lookup"><span data-stu-id="80269-146">If you are creating a large scale set by composing an Azure Resource Manager template, make sure hello template creates a scale set based on Azure Managed Disks.</span></span> <span data-ttu-id="80269-147">您可以設定 hello _singlePlacementGroup_在 hello 屬性 too_false__屬性_區段 hello _Microsoft.Compute/virtualMAchineScaleSets_資源。</span><span class="sxs-lookup"><span data-stu-id="80269-147">You can set hello _singlePlacementGroup_ property too_false_ in hello _properties_ section of hello _Microsoft.Compute/virtualMAchineScaleSets_ resource.</span></span> <span data-ttu-id="80269-148">hello 下列 JSON 片段顯示的小數位數組範本，包括 hello 1000 的 VM 容量和 hello 的 hello 開頭_"singlePlacementGroup": false_設定：</span><span class="sxs-lookup"><span data-stu-id="80269-148">hello following JSON fragment shows hello beginning of a scale set template, including hello 1,000 VM capacity and hello _"singlePlacementGroup" : false_ setting:</span></span>
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
<span data-ttu-id="80269-149">如需完整的範例，若要大規模的設定範本，請參閱太[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json)。</span><span class="sxs-lookup"><span data-stu-id="80269-149">For a complete example of a large scale set template, refer too[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).</span></span>

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a><span data-ttu-id="80269-150">轉換現有的小數位數設定多個位置群組 toospan</span><span class="sxs-lookup"><span data-stu-id="80269-150">Converting an existing scale set toospan multiple placement groups</span></span>
<span data-ttu-id="80269-151">toomake 現有的 VM 規模調整集合能夠調整 toomore 超過 100 的 Vm，您需要 toochange hello _singplePlacementGroup_屬性 too_false_ hello 規模設定的模型。</span><span class="sxs-lookup"><span data-stu-id="80269-151">toomake an existing VM scale set capable of scaling toomore than 100 VMs, you need toochange hello _singplePlacementGroup_ property too_false_ in hello scale set model.</span></span> <span data-ttu-id="80269-152">您可以測試變更這個屬性與 hello [Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="80269-152">You can test changing this property with hello [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="80269-153">尋找現有的小數位數集合，選取_編輯_並變更 hello _singlePlacementGroup_屬性。</span><span class="sxs-lookup"><span data-stu-id="80269-153">Find an existing scale set, select _Edit_ and change hello _singlePlacementGroup_ property.</span></span> <span data-ttu-id="80269-154">如果看不到此屬性，您可能會檢視 hello 與較舊版本的 hello Microsoft.Compute 應用程式開發介面所設定的小數位數。</span><span class="sxs-lookup"><span data-stu-id="80269-154">If you do not see this property, you may be viewing hello scale set with an older version of hello Microsoft.Compute API.</span></span>

>[!NOTE] 
<span data-ttu-id="80269-155">您可以變更設定從支援唯一 （hello 預設行為） tooa 支援多個位置群組，單一放置群組的比例，但您無法將轉換 hello 反過來。</span><span class="sxs-lookup"><span data-stu-id="80269-155">You can change a scale set from supporting a single placement group only (hello default behavior) tooa supporting multiple placement groups, but you cannot convert hello other way around.</span></span> <span data-ttu-id="80269-156">因此請確定您了解的大型集合，然後再將轉換的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="80269-156">Therefore make sure you understand hello properties of large scale sets before converting.</span></span> <span data-ttu-id="80269-157">特別是，請確定您不需要第 4 層負載平衡及 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="80269-157">In particular, make sure you do not need layer-4 load balancing with hello Azure Load Balancer.</span></span>


