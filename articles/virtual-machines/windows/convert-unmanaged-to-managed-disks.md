---
title: "Windows 虛擬機器從 unmanaged aaaConvert 磁碟 toomanaged 磁碟-Azure 受管理磁碟 |Microsoft 文件"
description: "如何 tooconvert 從 unmanaged 的磁碟 toomanaged Windows VM 磁碟在 hello Resource Manager 部署模型中使用 PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: cynthn
ms.openlocfilehash: e8ed8694b0e776d22df26261e2fc8340bfe5cafa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-windows-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a><span data-ttu-id="a4084-103">從 unmanaged 的磁碟 toomanaged 磁碟轉換 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a4084-103">Convert a Windows virtual machine from unmanaged disks toomanaged disks</span></span>

<span data-ttu-id="a4084-104">如果您有現有 Windows 虛擬機器 (Vm)，並且使用未受管理的磁碟，您可以將透過 hello hello Vm toouse 管理磁碟轉換[Azure 受管理磁碟](managed-disks-overview.md)服務。</span><span class="sxs-lookup"><span data-stu-id="a4084-104">If you have existing Windows virtual machines (VMs) that use unmanaged disks, you can convert hello VMs toouse managed disks through hello [Azure Managed Disks](managed-disks-overview.md) service.</span></span> <span data-ttu-id="a4084-105">此程序轉換 hello OS 磁碟和任何連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a4084-105">This process converts both hello OS disk and any attached data disks.</span></span>

<span data-ttu-id="a4084-106">本文章將示範如何使用 Azure PowerShell tooconvert Vm。</span><span class="sxs-lookup"><span data-stu-id="a4084-106">This article shows you how tooconvert VMs by using Azure PowerShell.</span></span> <span data-ttu-id="a4084-107">如果您需要 tooinstall，或將它升級，請參閱[安裝和設定 Azure PowerShell](/powershell/azure/install-azurerm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a4084-107">If you need tooinstall or upgrade it, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a4084-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="a4084-108">Before you begin</span></span>


* <span data-ttu-id="a4084-109">檢閱[hello 移轉計劃 tooManaged 磁碟](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)。</span><span class="sxs-lookup"><span data-stu-id="a4084-109">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span></span>

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]




## <a name="convert-single-instance-vms"></a><span data-ttu-id="a4084-110">轉換單一執行個體 VM</span><span class="sxs-lookup"><span data-stu-id="a4084-110">Convert single-instance VMs</span></span>
<span data-ttu-id="a4084-111">本章節涵蓋 tooconvert 單一執行個體中未受管理的 Azure Vm 磁碟 toomanaged 磁碟的方式。</span><span class="sxs-lookup"><span data-stu-id="a4084-111">This section covers how tooconvert single-instance Azure VMs from unmanaged disks toomanaged disks.</span></span> <span data-ttu-id="a4084-112">（如果您的 Vm 可用性設定組中，請參閱 hello 下一節）。</span><span class="sxs-lookup"><span data-stu-id="a4084-112">(If your VMs are in an availability set, see hello next section.)</span></span> 

1. <span data-ttu-id="a4084-113">Deallocate hello VM 使用 hello[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a4084-113">Deallocate hello VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet.</span></span> <span data-ttu-id="a4084-114">hello 下列範例會取消配置 hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="a4084-114">hello following example deallocates hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span> 

  ```powershell
  $rgName = "myResourceGroup"
  $vmName = "myVM"
  Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
  ```

2. <span data-ttu-id="a4084-115">使用 hello 轉換 hello VM toomanaged 磁碟[ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a4084-115">Convert hello VM toomanaged disks by using hello [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk) cmdlet.</span></span> <span data-ttu-id="a4084-116">下列程序會將轉換的 hello hello 先前的 VM，包括 hello OS 磁碟和任何資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="a4084-116">hello following process converts hello previous VM, including hello OS disk and any data disks:</span></span>

  ```powershell
  ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vmName
  ```

3. <span data-ttu-id="a4084-117">使用 hello 轉換 toomanaged 磁碟後啟動 hello VM[開始 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="a4084-117">Start hello VM after hello conversion toomanaged disks by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm).</span></span> <span data-ttu-id="a4084-118">下列範例會重新啟動的 hello hello 先前的 VM:</span><span class="sxs-lookup"><span data-stu-id="a4084-118">hello following example restarts hello previous VM:</span></span>

  ```powershell
  Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  ```


## <a name="convert-vms-in-an-availability-set"></a><span data-ttu-id="a4084-119">轉換可用性設定組中的 VM</span><span class="sxs-lookup"><span data-stu-id="a4084-119">Convert VMs in an availability set</span></span>

<span data-ttu-id="a4084-120">如果您想要 tooconvert toomanaged 磁碟都在可用性設定組中的 hello Vm，您必須先管理 tooconvert hello 可用性集 tooa 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="a4084-120">If hello VMs that you want tooconvert toomanaged disks are in an availability set, you first need tooconvert hello availability set tooa managed availability set.</span></span>

1. <span data-ttu-id="a4084-121">轉換 hello 可用性設定組使用 hello[更新 AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a4084-121">Convert hello availability set by using hello [Update-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/update-azurermavailabilityset) cmdlet.</span></span> <span data-ttu-id="a4084-122">下列範例更新 hello 可用性設定組具名的 hello `myAvailabilitySet` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="a4084-122">hello following example updates hello availability set named `myAvailabilitySet` in hello resource group named `myResourceGroup`:</span></span>

  ```powershell
  $rgName = 'myResourceGroup'
  $avSetName = 'myAvailabilitySet'

  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned 
  ```

  <span data-ttu-id="a4084-123">如果您的可用性設定組所在的 hello 區域只有 2 的受管理的容錯網域，但 hello 未受管理的容錯網域數目是 3，此命令會顯示錯誤類似太 「 hello 指定容錯網域計數 3 必須落在 hello 範圍 1 too2。 」</span><span class="sxs-lookup"><span data-stu-id="a4084-123">If hello region where your availability set is located has only 2 managed fault domains but hello number of unmanaged fault domains is 3, this command shows an error similar too"hello specified fault domain count 3 must fall in hello range 1 too2."</span></span> <span data-ttu-id="a4084-124">tooresolve hello 錯誤、 更新 hello 容錯網域 too2 和 update`Sku`太`Aligned`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a4084-124">tooresolve hello error, update hello fault domain too2 and update `Sku` too`Aligned` as follows:</span></span>

  ```powershell
  $avSet.PlatformFaultDomainCount = 2
  Update-AzureRmAvailabilitySet -AvailabilitySet $avSet -Sku Aligned
  ```

2. <span data-ttu-id="a4084-125">解除配置，並轉換 hello 可用性設定組中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a4084-125">Deallocate and convert hello VMs in hello availability set.</span></span> <span data-ttu-id="a4084-126">hello 下列指令碼解除配置每個 VM 使用 hello[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet，將它轉換使用[ConvertTo AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk)，並重新啟動使用[開始 AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="a4084-126">hello following script deallocates each VM by using hello [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) cmdlet, converts it by using [ConvertTo-AzureRmVMManagedDisk](/powershell/module/azurerm.compute/convertto-azurermvmmanageddisk), and restarts it by using [Start-AzureRmVM](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

  ```powershell
  $avSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rgName -Name $avSetName

  foreach($vmInfo in $avSet.VirtualMachinesReferences)
  {
     $vm = Get-AzureRmVM -ResourceGroupName $rgName | Where-Object {$_.Id -eq $vmInfo.id}
     Stop-AzureRmVM -ResourceGroupName $rgName -Name $vm.Name -Force
     ConvertTo-AzureRmVMManagedDisk -ResourceGroupName $rgName -VMName $vm.Name
     Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
  }
  ```


## <a name="troubleshooting"></a><span data-ttu-id="a4084-127">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a4084-127">Troubleshooting</span></span>

<span data-ttu-id="a4084-128">如果在轉換期間，發生錯誤，或如果 VM 是處於失敗狀態，因為先前的轉換中的問題，執行 hello `ConvertTo-AzureRmVMManagedDisk` cmdlet 一次。</span><span class="sxs-lookup"><span data-stu-id="a4084-128">If there is an error during conversion, or if a VM is in a failed state because of issues in a previous conversion, run hello `ConvertTo-AzureRmVMManagedDisk` cmdlet again.</span></span> <span data-ttu-id="a4084-129">簡單的重試通常會解除封鎖 hello 的情況。</span><span class="sxs-lookup"><span data-stu-id="a4084-129">A simple retry usually unblocks hello situation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4084-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4084-130">Next steps</span></span>

[<span data-ttu-id="a4084-131">轉換受管理的標準磁碟 toopremium</span><span class="sxs-lookup"><span data-stu-id="a4084-131">Convert standard managed disks toopremium</span></span>](convert-disk-storage.md)

<span data-ttu-id="a4084-132">使用[快照](snapshot-copy-managed-disk.md)來取得 VM 的唯讀複本。</span><span class="sxs-lookup"><span data-stu-id="a4084-132">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

