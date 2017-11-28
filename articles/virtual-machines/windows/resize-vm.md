---
title: "aaaUse PowerShell tooresize Azure 中的 Windows VM |Microsoft 文件"
description: "調整在 hello Resource Manager 部署模型，使用 Azure Powershell 中建立 Windows 虛擬機器的大小。"
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 057ff274-6dad-415e-891c-58f8eea9ed78
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: a4a80f3bc99911e4f1a095f0ce63aca00fa50694
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm"></a><span data-ttu-id="2dcf9-103">調整 Windows VM 大小</span><span class="sxs-lookup"><span data-stu-id="2dcf9-103">Resize a Windows VM</span></span>
<span data-ttu-id="2dcf9-104">本文章將示範如何 tooresize Windows VM，在建立使用 Azure Powershell hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-104">This article shows you how tooresize a Windows VM, created in hello Resource Manager deployment model using Azure Powershell.</span></span>

<span data-ttu-id="2dcf9-105">建立虛擬機器 (VM) 之後，您可以調整 hello VM 向上或向下藉由變更 hello VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-105">After you create a virtual machine (VM), you can scale hello VM up or down by changing hello VM size.</span></span> <span data-ttu-id="2dcf9-106">在某些情況下，您必須先取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="2dcf9-107">這種情況 hello 新大小不是在 hello 硬體叢集目前裝載 hello VM 上使用。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-107">This can happen if hello new size is not available on hello hardware cluster that is currently hosting hello VM.</span></span>

## <a name="resize-a-windows-vm-not-in-an-availability-set"></a><span data-ttu-id="2dcf9-108">調整不在可用性設定組中 Windows VM 的大小</span><span class="sxs-lookup"><span data-stu-id="2dcf9-108">Resize a Windows VM not in an availability set</span></span>
1. <span data-ttu-id="2dcf9-109">列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-109">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span> 
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName> 
    ```
2. <span data-ttu-id="2dcf9-110">如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-110">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="2dcf9-111">視 hello 大小未列出，請繼續 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-111">If hello desired size is not listed, go on toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVMsize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="2dcf9-112">視 hello 大小未列出，執行下列命令 toodeallocate hello VM、 調整其大小，並重新啟動 hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-112">If hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and restart hello VM.</span></span>
   
    ```powershell
    $rgname = "<resourceGroupName>"
    $vmname = "<vmName>"
    Stop-AzureRmVM -ResourceGroupName $rgname -VMName $vmname -Force
    $vm = Get-AzureRmVM -ResourceGroupName $rgname -VMName $vmname
    $vm.HardwareProfile.VmSize = "<newVMSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName $rgname
    Start-AzureRmVM -ResourceGroupName $rgname -Name $vmname
    ```

> [!WARNING]
> <span data-ttu-id="2dcf9-113">解除配置 hello VM 釋放任何動態指派 toohello VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-113">Deallocating hello VM releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="2dcf9-114">不會影響 hello OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-114">hello OS and data disks are not affected.</span></span> 
> 
> 

## <a name="resize-a-windows-vm-in-an-availability-set"></a><span data-ttu-id="2dcf9-115">調整在可用性設定組中 Windows VM 的大小</span><span class="sxs-lookup"><span data-stu-id="2dcf9-115">Resize a Windows VM in an availability set</span></span>
<span data-ttu-id="2dcf9-116">如果 hello 新的可用性設定組中的 VM 大小並不適用於 hello 硬體叢集目前裝載的 hello VM，然後在 hello 可用性設定組中的所有 Vm 需要 toobe tooresize hello VM 解除配置。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-116">If hello new size for a VM in an availability set is not available on hello hardware cluster currently hosting hello VM, then all VMs in hello availability set will need toobe deallocated tooresize hello VM.</span></span> <span data-ttu-id="2dcf9-117">您也可能需要 tooupdate hello hello 可用性設定組後一個 VM 已調整大小的其他 Vm 大小。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-117">You also might need tooupdate hello size of other VMs in hello availability set after one VM has been resized.</span></span> <span data-ttu-id="2dcf9-118">tooresize 可用性設定組中的 VM 會執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-118">tooresize a VM in an availability set, perform hello following steps.</span></span>

1. <span data-ttu-id="2dcf9-119">列出 hello hello hello VM 所在的硬體叢集可用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-119">List hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```powershell
    Get-AzureRmVMSize -ResourceGroupName <resourceGroupName> -VMName <vmName>
    ```
2. <span data-ttu-id="2dcf9-120">如果 hello 需要列出大小，請執行下列命令 tooresize hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-120">If hello desired size is listed, run hello following commands tooresize hello VM.</span></span> <span data-ttu-id="2dcf9-121">如果未列出，請移 toostep 3。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-121">If it is not listed, go toostep 3.</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroupName> -VMName <vmName>
    $vm.HardwareProfile.VmSize = "<newVmSize>"
    Update-AzureRmVM -VM $vm -ResourceGroupName <resourceGroupName>
    ```
3. <span data-ttu-id="2dcf9-122">如果 hello 需要未列出的大小，請繼續進行下列步驟 toodeallocate hello hello 可用性設定組中的所有 Vm、 調整大小的 Vm，並重新啟動它們。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-122">If hello desired size is not listed, continue with hello following steps toodeallocate all VMs in hello availability set, resize VMs, and restart them.</span></span>
4. <span data-ttu-id="2dcf9-123">停止 hello 可用性設定組中的所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-123">Stop all VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     Stop-AzureRmVM -ResourceGroupName $rg -Name $vmName -Force
   } 
   ```
5. <span data-ttu-id="2dcf9-124">調整大小，並重新啟動 hello 可用性設定組中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-124">Resize and restart hello VMs in hello availability set.</span></span>
   
   ```powershell
   $rg = "<resourceGroupName>"
   $newSize = "<newVmSize>"
   $as = Get-AzureRmAvailabilitySet -ResourceGroupName $rg
   $vmIds = $as.VirtualMachinesReferences
   foreach ($vmId in $vmIDs){
     $string = $vmID.Id.Split("/")
     $vmName = $string[8]
     $vm = Get-AzureRmVM -ResourceGroupName $rg -Name $vmName
     $vm.HardwareProfile.VmSize = $newSize
     Update-AzureRmVM -ResourceGroupName $rg -VM $vm
     Start-AzureRmVM -ResourceGroupName $rg -Name $vmName
   }
   ```

## <a name="next-steps"></a><span data-ttu-id="2dcf9-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2dcf9-125">Next steps</span></span>
* <span data-ttu-id="2dcf9-126">如需提高延展性，可執行多個 VM 執行個體並相應放大。如需詳細資訊，請參閱[在虛擬機器擴展集中自動調整機器](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md)。</span><span class="sxs-lookup"><span data-stu-id="2dcf9-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Windows machines in a Virtual Machine Scale Set](../../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span></span>

