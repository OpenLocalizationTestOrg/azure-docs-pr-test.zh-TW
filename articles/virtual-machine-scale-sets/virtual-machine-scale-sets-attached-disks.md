---
title: "Azure 虛擬機器擴展集連結資料磁碟 | Microsoft Docs"
description: "了解如何搭配使用連線資料磁碟與虛擬機器擴展集"
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
ms.date: 4/25/2017
ms.author: guybo
ms.openlocfilehash: 22c7e589efa9a9f401549ec9b95c58c4eaf07b94
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-vm-scale-sets-and-attached-data-disks"></a><span data-ttu-id="8e271-103">Azure VM 擴展集與連線資料磁碟</span><span class="sxs-lookup"><span data-stu-id="8e271-103">Azure VM scale sets and attached data disks</span></span>
<span data-ttu-id="8e271-104">Azure [虛擬機器擴展集](/azure/virtual-machine-scale-sets/)現在支援具有連線資料磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8e271-104">Azure [virtual machine scale sets](/azure/virtual-machine-scale-sets/) now support virtual machines with attached data disks.</span></span> <span data-ttu-id="8e271-105">您可以在使用 Azure 受控磁碟建立的擴展集儲存體設定檔中定義資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-105">Data disks can be defined in the storage profile for scale sets that have been created with Azure Managed Disks.</span></span> <span data-ttu-id="8e271-106">先前擴展集中 VM 唯一可用的直接連結儲存體選項是作業系統磁碟機和暫存磁碟機。</span><span class="sxs-lookup"><span data-stu-id="8e271-106">Previously the only directly attached storage options available with VMs in scale sets were the OS drive and temp drives.</span></span>

> [!NOTE]
>  <span data-ttu-id="8e271-107">當您建立已定義連結資料磁碟的擴展集時，仍需掛接和格式化 VM 內的磁碟才能加以使用 (就如同獨立 Azure VM)。</span><span class="sxs-lookup"><span data-stu-id="8e271-107">When you create a scale set with attached data disks defined, you still need to mount and format the disks from within a VM to use them (just like for standalone Azure VMs).</span></span> <span data-ttu-id="8e271-108">方便的作法是使用自訂指令碼擴充功能，該擴充功能可呼叫標準指令碼來分割及格式化 VM 上的所有資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-108">A convenient way to do this is to use a custom script extension which calls a standard script to partition and format all the data disks on a VM.</span></span>

## <a name="create-a-scale-set-with-attached-data-disks"></a><span data-ttu-id="8e271-109">建立具有連結資料磁碟的擴展集</span><span class="sxs-lookup"><span data-stu-id="8e271-109">Create a scale set with attached data disks</span></span>
<span data-ttu-id="8e271-110">使用 [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ 命令是建立具有連結磁碟之擴展集的簡便方法。</span><span class="sxs-lookup"><span data-stu-id="8e271-110">A simple way to create a scale set with attached disks is to use the [Azure CLI](https://github.com/Azure/azure-cli) _vmss create_ command.</span></span> <span data-ttu-id="8e271-111">下列範例會建立 Azure 資源群組，以及由 10 部 Ubuntu VM 組成的 VM 擴展集，而每部 VM 各有 2 個連結資料磁碟 (分別為 50 GB 和 100 GB)。</span><span class="sxs-lookup"><span data-stu-id="8e271-111">The following example creates an Azure resource group, and a VM scale set of 10 Ubuntu VMs, each with 2 attached data disks, of 50 GB and 100 GB respectively.</span></span>
```bash
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```
<span data-ttu-id="8e271-112">請注意，_vmss create_ 命令會預設某些組態值 (如果您未指定它們)。</span><span class="sxs-lookup"><span data-stu-id="8e271-112">Note that the _vmss create_ command defaults certain configuration values if you do not specify them.</span></span> <span data-ttu-id="8e271-113">若要查看您可覆寫的可用選項，請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="8e271-113">To see the available options that you can override try:</span></span>
```bash
az vmss create --help
```
<span data-ttu-id="8e271-114">另一種建立具有連結資料磁碟之擴展集的方法是在 Azure Resource Manager 範本中定義擴展集、在 _storageProfile_ 中包含 _dataDisks_ 區段，以及部署範本。</span><span class="sxs-lookup"><span data-stu-id="8e271-114">Another way to create a scale set with attached data disks is to define a scale set in an Azure Resource Manager template, include a _dataDisks_ section in the _storageProfile_, and deploy the template.</span></span> <span data-ttu-id="8e271-115">上述 50 GB 和 100 GB 磁碟範例會在範本中定義如下︰</span><span class="sxs-lookup"><span data-stu-id="8e271-115">The 50 GB and 100 GB disk example above would be defined like this in the template:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    }
]
```
<span data-ttu-id="8e271-116">您可以在此看到完整、可立即部署並已定義連結磁碟的擴展集範例︰[https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data)。</span><span class="sxs-lookup"><span data-stu-id="8e271-116">You can see a complete, ready to deploy example of a scale set template with an attached disk defined here: [https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data](https://github.com/chagarw/MDPP/tree/master/101-vmss-os-data).</span></span>

## <a name="adding-a-data-disk-to-an-existing-scale-set"></a><span data-ttu-id="8e271-117">將資料磁碟新增至現有的擴展集</span><span class="sxs-lookup"><span data-stu-id="8e271-117">Adding a data disk to an existing scale set</span></span>
> [!NOTE]
>  <span data-ttu-id="8e271-118">您只能將資料磁碟連結至使用 [Azure 受控磁碟](./virtual-machine-scale-sets-managed-disks.md)建立的擴展集。</span><span class="sxs-lookup"><span data-stu-id="8e271-118">You can only attach data disks to a scale set which has been created with [Azure Managed Disks](./virtual-machine-scale-sets-managed-disks.md).</span></span>

<span data-ttu-id="8e271-119">您可以使用 Azure CLI _az vmss disk attach_ 命令，將資料磁碟新增至 VM 擴展集。</span><span class="sxs-lookup"><span data-stu-id="8e271-119">You can add a data disk to a VM scale set using Azure CLI _az vmss disk attach_ command.</span></span> <span data-ttu-id="8e271-120">務必指定尚未使用的 lun。</span><span class="sxs-lookup"><span data-stu-id="8e271-120">Make sure you specify a lun which is not already in use.</span></span> <span data-ttu-id="8e271-121">下列 CLI 範例將 50 GB 磁碟機新增至 lun 3︰</span><span class="sxs-lookup"><span data-stu-id="8e271-121">The following CLI example adds a 50 GB drive to lun 3:</span></span>
```bash
az vmss disk attach -g dsktest -n dskvmss --size-gb 50 --lun 3
```

<span data-ttu-id="8e271-122">下列 PowerShell 範例將 50 GB 磁碟機新增至 lun 3︰</span><span class="sxs-lookup"><span data-stu-id="8e271-122">The following PowerShell example adds a 50 GB drive to lun 3:</span></span>
```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName myvmssrg -VMScaleSetName myvmss
$vmss = Add-AzureRmVmssDataDisk -VirtualMachineScaleSet $vmss -Lun 3 -Caching 'ReadWrite' -CreateOption Empty -DiskSizeGB 50 -StorageAccountType StandardLRS
Update-AzureRmVmss -ResourceGroupName myvmssrg -Name myvmss -VirtualMachineScaleSet $vmss
```

> [!NOTE]
> <span data-ttu-id="8e271-123">不同的 VM 大小對其支援的連結磁碟機數目會有不同的限制。</span><span class="sxs-lookup"><span data-stu-id="8e271-123">Different VM sizes have different limits on the numbers of attached drives they support.</span></span> <span data-ttu-id="8e271-124">新增磁碟前，請檢查[虛擬機器大小特性](../virtual-machines/windows/sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="8e271-124">Check the [virtual machine size characteristics](../virtual-machines/windows/sizes.md) before adding a new disk.</span></span>

<span data-ttu-id="8e271-125">將項目新增至擴展集定義的 _storageProfile_ 中的 _dataDisks_ 屬性並套用變更，也可以新增磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-125">You can also add a disk by adding a new entry to the _dataDisks_ property in the _storageProfile_ of a scale set definition and applying the change.</span></span> <span data-ttu-id="8e271-126">若要進行測試，在 [Azure 資源總管](https://resources.azure.com/)中尋找現有的擴展集定義。</span><span class="sxs-lookup"><span data-stu-id="8e271-126">To test this, find an existing scale set definition in the [Azure Resource Explorer](https://resources.azure.com/).</span></span> <span data-ttu-id="8e271-127">選取 [編輯] 並將新磁碟新增至資料磁碟清單。</span><span class="sxs-lookup"><span data-stu-id="8e271-127">Select _Edit_ and add a new disk to the list of data disks.</span></span> <span data-ttu-id="8e271-128">例如</span><span class="sxs-lookup"><span data-stu-id="8e271-128">E.g.</span></span> <span data-ttu-id="8e271-129">使用上述範例︰</span><span class="sxs-lookup"><span data-stu-id="8e271-129">using the example above:</span></span>
```json
"dataDisks": [
    {
    "lun": 1,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 50
    },
    {
    "lun": 2,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 100
    },
    {
    "lun": 3,
    "createOption": "Empty",
    "caching": "ReadOnly",
    "diskSizeGB": 20
    }          
]
```

<span data-ttu-id="8e271-130">然後選取 _PUT_ 將變更套用到您的擴展集。</span><span class="sxs-lookup"><span data-stu-id="8e271-130">Then select _PUT_ to apply the changes to your scale set.</span></span> <span data-ttu-id="8e271-131">只要您使用的 VM 大小可支援兩個以上的連結資料磁碟，此範例就可行。</span><span class="sxs-lookup"><span data-stu-id="8e271-131">This example would work as long as you are using a VM size which supports more than two attached data disks.</span></span>

> [!NOTE]
> <span data-ttu-id="8e271-132">當您變更擴展集定義時 (例如新增或移除資料磁碟)，它會套用到所有新建立的 VM，但如果 _upgradePolicy_ 屬性設定為 [自動]，則只會套用至現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="8e271-132">When you make a change to a scale set definition such as adding or removing a data disk, it applies to all newly created VMs, but only applies to existing VMs if the _upgradePolicy_ property is set to "Automatic".</span></span> <span data-ttu-id="8e271-133">如果該屬性設定為 [手動]，您必須以手動方式將新的模型套用至現有的 VM。</span><span class="sxs-lookup"><span data-stu-id="8e271-133">If it is set to "Manual", you need to manually apply the new model to existing VMs.</span></span> <span data-ttu-id="8e271-134">您可以在入口網站中，使用 _Update-AzureRmVmssInstance_ PowerShell 命令，或使用 _az vmss update-instances_ CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="8e271-134">You can do this in the portal, using the _Update-AzureRmVmssInstance_ PowerShell command, or using the _az vmss update-instances_ CLI command.</span></span>

## <a name="adding-pre-populated-data-disks-to-an-existent-scale-set"></a><span data-ttu-id="8e271-135">將預先填入的資料磁碟新增至現存的擴展集</span><span class="sxs-lookup"><span data-stu-id="8e271-135">Adding pre-populated data disks to an existent scale set</span></span> 
> <span data-ttu-id="8e271-136">當您將磁碟新增至現存的擴展集模型時，依照設計，一律會建立空白的磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-136">When you add disks to an existent scale set model, by design, the disk will always be created empty.</span></span> <span data-ttu-id="8e271-137">此案例也會包含擴展集所建立的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="8e271-137">This scenario also includes new instances created by the scale set.</span></span> <span data-ttu-id="8e271-138">這是因為擴展集定義具有空的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-138">This behaviour is because the scaleset definition has an empty data disk.</span></span> <span data-ttu-id="8e271-139">若要針對現存的擴展集模型建立預先填入的資料磁碟機，您可以選擇下列其中一個選項：</span><span class="sxs-lookup"><span data-stu-id="8e271-139">In order to create pre-populated data drives for an existent scale set model, you can choose either of next two options:</span></span>

* <span data-ttu-id="8e271-140">藉由執行自訂指令碼，將資料從執行個體 0 VM 複製到其他 VM 中的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-140">Copy data from the instance 0 VM to the data disk(s) in the other VMs by running a custom script.</span></span>
* <span data-ttu-id="8e271-141">建立具有 OS 磁碟再加上資料磁碟 (包含所需資料) 的受控映像，並使用此映像建立新的擴展集。</span><span class="sxs-lookup"><span data-stu-id="8e271-141">Create a managed image with the OS disk plus data disk (with the required data) and create a new scaleset with the image.</span></span> <span data-ttu-id="8e271-142">如此一來，每個新 VM 都會有擴展集定義中提供的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-142">This way every new VM created will have a data disk that that is provided in the definition of the scaleset.</span></span> <span data-ttu-id="8e271-143">因為此定義參考的映像具有已自訂資料的資料磁碟，所以擴展集上的每部虛擬機器都會自動出現這些變更。</span><span class="sxs-lookup"><span data-stu-id="8e271-143">Since this definition will refer to an image with a data disk that has customized data, every virtual machine on the scaleset will automatically come up with these changes.</span></span>

> <span data-ttu-id="8e271-144">在此可找到建立自訂映像的方式：[在 Azure 中建立一般化 VM 的受控映像](/azure/virtual-machines/windows/capture-image-resource/)</span><span class="sxs-lookup"><span data-stu-id="8e271-144">The way to create a custom image can be found here: [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource/)</span></span> 

> <span data-ttu-id="8e271-145">使用者必須擷取具有所需資料的執行個體 0 VM，然後使用映像定義的該 vhd。</span><span class="sxs-lookup"><span data-stu-id="8e271-145">The user needs to capture the instance 0 VM which has the required data, and then use that vhd for the image definition.</span></span>

## <a name="removing-a-data-disk-from-a-scale-set"></a><span data-ttu-id="8e271-146">從擴展集中移除資料磁碟</span><span class="sxs-lookup"><span data-stu-id="8e271-146">Removing a data disk from a scale set</span></span>
<span data-ttu-id="8e271-147">您可以使用 Azure CLI _az vmss disk detach_ 命令，從 VM 擴展集中移除資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-147">You can remove a data disk from a VM scale set using Azure CLI _az vmss disk detach_ command.</span></span> <span data-ttu-id="8e271-148">例如下列命令會移除在 lun 2 定義的磁碟︰</span><span class="sxs-lookup"><span data-stu-id="8e271-148">For example the following command removes the disk defined at lun 2:</span></span>
```bash
az vmss disk detach -g dsktest -n dskvmss --lun 2
```  
<span data-ttu-id="8e271-149">同樣第，從 _storageProfile_ 中的 _dataDisks_ 屬性中移除項目並套用變更，也可以從擴展集中移除磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-149">Similarly you can also remove a disk from a scale set by removing an entry from the _dataDisks_ property in the _storageProfile_ and applying the change.</span></span> 

## <a name="additional-notes"></a><span data-ttu-id="8e271-150">其他注意事項</span><span class="sxs-lookup"><span data-stu-id="8e271-150">Additional notes</span></span>
<span data-ttu-id="8e271-151">API 版本 [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) 或更新版本的 Microsoft.Compute API 中提供 Azure 受控磁碟和擴展集連結資料磁碟的支援。</span><span class="sxs-lookup"><span data-stu-id="8e271-151">Support for Azure Managed disks and scale set attached data disks is available in API version [_2016-04-30-preview_](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-compute/2016-04-30-preview/swagger/compute.json) or later of the Microsoft.Compute API.</span></span>

<span data-ttu-id="8e271-152">在擴展集連結磁碟支援的初始實作中，您無法對擴展集中的個別 VM 附加或卸離資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-152">In the initial implementation of attached disk support for scale sets, you cannot attach or detach data disks to/from individual VMs in a scale set.</span></span>

<span data-ttu-id="8e271-153">Azure 入口網站對於擴展集中連結資料磁碟的支援一開始就有限制。</span><span class="sxs-lookup"><span data-stu-id="8e271-153">Azure portal support for attached data disks in scale sets is initially limited.</span></span> <span data-ttu-id="8e271-154">視您的需求而定，您可以使用 Azure 範本、CLI、PowerShell、SDK 和 REST API 來管理連結磁碟。</span><span class="sxs-lookup"><span data-stu-id="8e271-154">Depending on your requirements you can use Azure templates, CLI, PowerShell, SDKs, and REST API to manage attached disks.</span></span>


