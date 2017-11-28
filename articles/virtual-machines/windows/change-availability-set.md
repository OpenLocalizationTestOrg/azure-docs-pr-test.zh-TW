---
title: "aaaChange Vm 的可用性設定組 |Microsoft 文件"
description: "了解 toochange hello 可用性設定虛擬機器使用 Azure PowerShell 及 hello Resource Manager 部署模型的方式。"
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 44c90f90-bc9a-4260-a36f-5465e2a1ef94
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: drewm
ms.openlocfilehash: 3b1cc010a6d4c4883f2e34da9cfca4372aec92cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-availability-set-for-a-windows-vm"></a><span data-ttu-id="e6a09-103">變更 hello 可用性集合，針對 Windows VM</span><span class="sxs-lookup"><span data-stu-id="e6a09-103">Change hello availability set for a Windows VM</span></span>
<span data-ttu-id="e6a09-104">hello 下列步驟說明如何 toochange hello 可用性設定組的 VM，使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e6a09-104">hello following steps describe how toochange hello availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="e6a09-105">VM 只能加入 tooan 可用性設定組在建立時。</span><span class="sxs-lookup"><span data-stu-id="e6a09-105">A VM can only be added tooan availability set when it is created.</span></span> <span data-ttu-id="e6a09-106">在訂單 toochange hello 可用性設定組，您需要 toodelete，並重新建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e6a09-106">In order toochange hello availability set, you need toodelete and recreate hello virtual machine.</span></span> 

## <a name="change-hello-availability-set-using-powershell"></a><span data-ttu-id="e6a09-107">變更 hello 可用性集合，使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6a09-107">Change hello availability set using PowerShell</span></span>
1. <span data-ttu-id="e6a09-108">擷取 hello hello VM toobe 修改中的下列索引鍵的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e6a09-108">Capture hello following key details from hello VM toobe modified.</span></span>
   
    <span data-ttu-id="e6a09-109">Hello VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="e6a09-109">Name of hello VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="e6a09-110">VM 大小</span><span class="sxs-lookup"><span data-stu-id="e6a09-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="e6a09-111">如果它們存在於網路主要網路介面和選用網路介面 hello VM</span><span class="sxs-lookup"><span data-stu-id="e6a09-111">Network primary network interface and optional network interfaces if they exist on hello VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="e6a09-112">OS 磁碟設定檔</span><span class="sxs-lookup"><span data-stu-id="e6a09-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="e6a09-113">每個資料磁碟的磁碟設定檔</span><span class="sxs-lookup"><span data-stu-id="e6a09-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="e6a09-114">已安裝的 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="e6a09-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="e6a09-115">刪除 hello VM，但不刪除任何 hello 磁碟或 hello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="e6a09-115">Delete hello VM without deleting any of hello disks or hello network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="e6a09-116">建立 hello 可用性設定組，如果不存在</span><span class="sxs-lookup"><span data-stu-id="e6a09-116">Create hello availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="e6a09-117">重新建立 hello VM 使用 hello 新的可用性集合</span><span class="sxs-lookup"><span data-stu-id="e6a09-117">Recreate hello VM using hello new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="e6a09-118">新增資料磁碟和延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e6a09-118">Add data disks and extensions.</span></span> <span data-ttu-id="e6a09-119">如需詳細資訊，請參閱[附加資料磁碟 tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[資源管理員範本中的延伸模組](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)。</span><span class="sxs-lookup"><span data-stu-id="e6a09-119">For more information, see [Attach Data Disk tooVM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="e6a09-120">資料磁碟和擴充功能可以加入 toohello VM 使用 PowerShell 或 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="e6a09-120">Data disks and extensions can be added toohello VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="e6a09-121">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e6a09-121">Example Script</span></span>
<span data-ttu-id="e6a09-122">hello 下列指令碼提供一個範例的收集設定資訊所需的 hello，刪除 hello 原始 VM，然後重新建立新的可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="e6a09-122">hello following script provides an example of gathering hello required information, deleting hello original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details toofile
    "VM Name: " | Out-File -FilePath $outFile 
    $OriginalVM.Name | Out-File -FilePath $outFile -Append

    "Extensions: " | Out-File -FilePath $outFile -Append
    $OriginalVM.Extensions | Out-File -FilePath $outFile -Append

    "VMSize: " | Out-File -FilePath $outFile -Append
    $OriginalVM.HardwareProfile.VmSize | Out-File -FilePath $outFile -Append

    "NIC: " | Out-File -FilePath $outFile -Append
    $OriginalVM.NetworkProfile.NetworkInterfaces[0].Id | Out-File -FilePath $outFile -Append

    "OSType: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.OsType | Out-File -FilePath $outFile -Append

    "OS Disk: " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.OsDisk.Vhd.Uri | Out-File -FilePath $outFile -Append

    if ($OriginalVM.StorageProfile.DataDisks) {
    "Data Disk(s): " | Out-File -FilePath $outFile -Append
    $OriginalVM.StorageProfile.DataDisks | Out-File -FilePath $outFile -Append
    }

    #Remove hello original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create hello basic configuration for hello replacement VM
    $newVM = New-AzureRmVMConfig -VMName $OriginalVM.Name -VMSize $OriginalVM.HardwareProfile.VmSize -AvailabilitySetId $availSet.Id
    Set-AzureRmVMOSDisk -VM $NewVM -VhdUri $OriginalVM.StorageProfile.OsDisk.Vhd.Uri  -Name $OriginalVM.Name -CreateOption Attach -Windows

    #Add Data Disks
    foreach ($disk in $OriginalVM.StorageProfile.DataDisks ) { 
    Add-AzureRmVMDataDisk -VM $newVM -Name $disk.Name -VhdUri $disk.Vhd.Uri -Caching $disk.Caching -Lun $disk.Lun -CreateOption Attach -DiskSizeInGB $disk.DiskSizeGB
    }

    #Add NIC(s)
    foreach ($nic in $OriginalVM.NetworkInterfaceIDs) {
        Add-AzureRmVMNetworkInterface -VM $NewVM -Id $nic
    }

    #Create hello VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="e6a09-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6a09-123">Next steps</span></span>
<span data-ttu-id="e6a09-124">新增額外新增額外的儲存體 tooyour VM[資料磁碟](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e6a09-124">Add additional storage tooyour VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

