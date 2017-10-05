---
title: "變更 VM 可用性設定組 | Microsoft Docs"
description: "了解如何使用 Azure PowerShell 和 Resource Manager 部署模型來變更虛擬機器的可用性設定組。"
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
ms.openlocfilehash: d1daa01191480eaeb81727416b2134b00c698dc3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="change-the-availability-set-for-a-windows-vm"></a><span data-ttu-id="5cc11-103">變更 Windows VM 的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="5cc11-103">Change the availability set for a Windows VM</span></span>
<span data-ttu-id="5cc11-104">下列步驟說明如何使用 Azure PowerShell 來變更 VM 的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5cc11-104">The following steps describe how to change the availability set of a VM using Azure PowerShell.</span></span> <span data-ttu-id="5cc11-105">只有在建立 VM 時，才能將 VM 新增到可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="5cc11-105">A VM can only be added to an availability set when it is created.</span></span> <span data-ttu-id="5cc11-106">若要變更可用性設定組，您必須將虛擬機器刪除後再重新建立。</span><span class="sxs-lookup"><span data-stu-id="5cc11-106">In order to change the availability set, you need to delete and recreate the virtual machine.</span></span> 

## <a name="change-the-availability-set-using-powershell"></a><span data-ttu-id="5cc11-107">使用 PowerShell 來變更可用性設定組</span><span class="sxs-lookup"><span data-stu-id="5cc11-107">Change the availability set using PowerShell</span></span>
1. <span data-ttu-id="5cc11-108">從要修改的 VM 中擷取下列主要詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5cc11-108">Capture the following key details from the VM to be modified.</span></span>
   
    <span data-ttu-id="5cc11-109">VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="5cc11-109">Name of the VM</span></span>
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <Name-of-resource-group> -Name <name-of-VM>
    $vm.Name
    ```
   
    <span data-ttu-id="5cc11-110">VM 大小</span><span class="sxs-lookup"><span data-stu-id="5cc11-110">VM Size</span></span>
   
    ```powershell
    $vm.HardwareProfile.VmSize
    ```
   
    <span data-ttu-id="5cc11-111">網路主要網路介面和選擇性網路介面 (如果它們存在於 VM 上)</span><span class="sxs-lookup"><span data-stu-id="5cc11-111">Network primary network interface and optional network interfaces if they exist on the VM</span></span>
   
    ```powershell
    $vm.NetworkProfile.NetworkInterfaces[0].Id
    ```
   
    <span data-ttu-id="5cc11-112">OS 磁碟設定檔</span><span class="sxs-lookup"><span data-stu-id="5cc11-112">OS Disk Profile</span></span>
   
    ```powershell
    $vm.StorageProfile.OsDisk.OsType
    $vm.StorageProfile.OsDisk.Name
    $vm.StorageProfile.OsDisk.Vhd.Uri
    ```
   
    <span data-ttu-id="5cc11-113">每個資料磁碟的磁碟設定檔</span><span class="sxs-lookup"><span data-stu-id="5cc11-113">Disk profiles for each data disk</span></span> 
   
    ```powershell
    $vm.StorageProfile.DataDisks[<index>].Lun
    $vm.StorageProfile.DataDisks[<index>].Vhd.Uri
    ```
   
    <span data-ttu-id="5cc11-114">已安裝的 VM 延伸模組</span><span class="sxs-lookup"><span data-stu-id="5cc11-114">VM extensions installed</span></span> 
   
    ```powershell
    $vm.Extensions
    ```
2. <span data-ttu-id="5cc11-115">刪除 VM 而不刪除任何磁碟或網路介面。</span><span class="sxs-lookup"><span data-stu-id="5cc11-115">Delete the VM without deleting any of the disks or the network interfaces.</span></span>
   
    ```powershell
    Remove-AzureRmVM -ResourceGroupName <resourceGroupName> -Name <vmName> 
    ```
3. <span data-ttu-id="5cc11-116">建立可用性設定組 (如果可用性設定組尚未存在)</span><span class="sxs-lookup"><span data-stu-id="5cc11-116">Create the availability set if it does not already exist</span></span>
   
    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName <resourceGroupName> -Name <availabilitySetName> -Location "<location>" 
    ```
4. <span data-ttu-id="5cc11-117">使用新的可用性設定組來重新建立 VM</span><span class="sxs-lookup"><span data-stu-id="5cc11-117">Recreate the VM using the new availability set</span></span>
   
    ```powershell
    $vm2 = New-AzureRmVMConfig -VMName <VM-name> -VMSize <vm-size> -AvailabilitySetId <availability-set-id>
   
    Set-AzureRmVMOSDisk -CreateOption "Attach" -VM <vmConfig> -VhdUri <osDiskURI> -Name <osDiskName> [-Windows | -Linux]
   
    Add-AzureRmVMNetworkInterface -VM <vmConfig> -Id  <nicId> 
   
    New-AzureRmVM -ResourceGroupName <resourceGroupName> -Location <location> -VM <vmConfig>
    ``` 
5. <span data-ttu-id="5cc11-118">新增資料磁碟和延伸模組。</span><span class="sxs-lookup"><span data-stu-id="5cc11-118">Add data disks and extensions.</span></span> <span data-ttu-id="5cc11-119">如需詳細資訊，請參閱[將資料磁碟連結到 VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 和 [Resource Manager 範本中的延伸模組](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions)。</span><span class="sxs-lookup"><span data-stu-id="5cc11-119">For more information, see [Attach Data Disk to VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Extensions in Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span> <span data-ttu-id="5cc11-120">您可以使用 PowerShell 或 Azure CLI 將資料磁碟和延伸模組新增到 VM 中。</span><span class="sxs-lookup"><span data-stu-id="5cc11-120">Data disks and extensions can be added to the VM using PowerShell or Azure CLI.</span></span>

## <a name="example-script"></a><span data-ttu-id="5cc11-121">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5cc11-121">Example Script</span></span>
<span data-ttu-id="5cc11-122">下列指令碼提供一個範例，此範例會收集必要資訊、刪除原始 VM，然後在新的可用性設定組中重新建立 VM。</span><span class="sxs-lookup"><span data-stu-id="5cc11-122">The following script provides an example of gathering the required information, deleting the original VM and then recreating it in a new availability set.</span></span>

```powershell
    #set variables
    $rg = "demo-resource-group"
    $vmName = "demo-vm"
    $newAvailSetName = "demo-as"
    $outFile = "C:\temp\outfile.txt"

    #Get VM Details
    $OriginalVM = get-azurermvm -ResourceGroupName $rg -Name $vmName

    #Output VM details to file
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

    #Remove the original VM
    Remove-AzureRmVM -ResourceGroupName $rg -Name $vmName

    #Create new availability set if it does not exist
    $availSet = Get-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -ErrorAction Ignore
    if (-Not $availSet) {
    $availset = New-AzureRmAvailabilitySet -ResourceGroupName $rg -Name $newAvailSetName -Location $OriginalVM.Location
    }

    #Create the basic configuration for the replacement VM
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

    #Create the VM
    New-AzureRmVM -ResourceGroupName $rg -Location $OriginalVM.Location -VM $NewVM -DisableBginfoExtension
```

## <a name="next-steps"></a><span data-ttu-id="5cc11-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5cc11-123">Next steps</span></span>
<span data-ttu-id="5cc11-124">透過新增額外 [資料磁碟](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，將額外的存放裝置新增到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="5cc11-124">Add additional storage to your VM by adding an additional [data disk](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

