---
title: "aaaExpand 資料磁碟附加 tooa 在 Azure 中的 Windows VM |Microsoft 文件"
description: "展開 hello 附加的 tooa 使用 PowerShell 的 Windows 虛擬機器的資料磁碟大小。"
services: virtual-machines-windows
documentationcenter: na
author: cynthn
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.openlocfilehash: b16ad0da9cff9dfffc9dc9ec7dd72891e7ddd745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="increase-hello-size-of-a-data-disk-attached-tooa-windows-vm"></a><span data-ttu-id="930bd-103">增加 hello 大小的資料磁碟附加 tooa Windows VM</span><span class="sxs-lookup"><span data-stu-id="930bd-103">Increase hello size of a data disk attached tooa Windows VM</span></span>

<span data-ttu-id="930bd-104">如果您需要 tooincrease hello hello 資料磁碟附加 tooyour 虛擬機器大小，您可以增加 hello 大小使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="930bd-104">If you need tooincrease hello size of hello data disk attached tooyour virtual machine, you can increase hello size using PowerShell.</span></span> <span data-ttu-id="930bd-105">增加 hello hello Azure VM 設定中的 hello 資料磁碟大小之後，您也需要 tooallocate hello 新的磁碟空間 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="930bd-105">After you increase hello size of hello data disk in hello Azure VM settings, you also need tooallocate hello new disk space within hello VM.</span></span>


## <a name="use-powershell-tooincrease-hello-size-of-a-managed-data-disk"></a><span data-ttu-id="930bd-106">使用 Powershell tooincrease hello 大小的受管理的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="930bd-106">Use Powershell tooincrease hello size of a managed data disk</span></span>

<span data-ttu-id="930bd-107">受管理的資料磁碟時，使用下列 PowerShell 指令程式的 hello tooincrease hello 大小：</span><span class="sxs-lookup"><span data-stu-id="930bd-107">tooincrease hello size of a managed data disk, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="930bd-108">Get-AzureRMReseourceGroup</span><span class="sxs-lookup"><span data-stu-id="930bd-108">Get-AzureRMReseourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | [<span data-ttu-id="930bd-109">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="930bd-109">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="930bd-110">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="930bd-110">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                        | [<span data-ttu-id="930bd-111">Update-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="930bd-111">Update-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Update-AzureRmDisk) |
 | [<span data-ttu-id="930bd-112">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="930bd-112">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |
<br>

<span data-ttu-id="930bd-113">hello 下列指令碼將逐步引導您取得 hello VM 資訊、 選取 hello 資料磁碟，並指定 hello 新大小。</span><span class="sxs-lookup"><span data-stu-id="930bd-113">hello following script will walk you through getting hello VM information, selecting hello data disk and specifying hello new size.</span></span>

```powershell
# Select resource group

    $rg = Get-AzureRMResourceGroup | Out-GridView `
        -Title "Select hello resource group" `
        -PassThru

    $rgName = $rg.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM -ResourceGroupName $rgName `
        | Out-GridView `
            -Title "Select a VM" `
             -PassThru

# Select data disk

    $disk = $vm.StorageProfile.DataDisks | Out-GridView `
        -Title "Select a data disk" `
        -PassThru

# Specify a larger size for hello data disk

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    $diskUpdateConfig = New-AzureRmDiskUpdateConfig -DiskSizeGB $size

# Update hello configuration in Azure

    $managedDisk = Get-AzureRmResource -ResourceId $disk.ManagedDisk.Id
    Update-AzureRmDisk -DiskName $managedDisk.ResourceName -ResourceGroupName $managedDisk.ResourceGroupName -DiskUpdate $diskUpdateConfig

# Start hello VM

    Start-AzureRmVM -ResourceGroupName $rgName -VMName $vm.name
```

## <a name="use-powershell-tooincrease-hello-size-of-an-unmanaged-data-disk"></a><span data-ttu-id="930bd-114">使用 PowerShell tooincrease hello 大小不受管理的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="930bd-114">Use PowerShell tooincrease hello size of an unmanaged data disk</span></span>

<span data-ttu-id="930bd-115">未受管理的資料磁碟儲存體帳戶中，使用下列 PowerShell 指令程式的 hello tooincrease hello 大小：</span><span class="sxs-lookup"><span data-stu-id="930bd-115">tooincrease hello size of unmanaged data disks in a storage account, use hello following PowerShell cmdlets:</span></span>

|                                                                    |                                                            |
|--------------------------------------------------------------------|------------------------------------------------------------|
| [<span data-ttu-id="930bd-116">Get-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="930bd-116">Get-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccount) | [<span data-ttu-id="930bd-117">Get-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="930bd-117">Get-AzureRMVM</span></span>](/powershell/module/azurerm.compute/get-azurermvm)                 |
| [<span data-ttu-id="930bd-118">Stop-AzureRMVM</span><span class="sxs-lookup"><span data-stu-id="930bd-118">Stop-AzureRMVM</span></span>](/powershell/module/azurerm.compute/stop-azurermvm)                       | [<span data-ttu-id="930bd-119">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="930bd-119">Set-AzureRmVMDataDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmdatadisk) |
| [<span data-ttu-id="930bd-120">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="930bd-120">Update-AzureRmVM</span></span>](/powershell/module/azurerm.compute/update-azurermvm)                   | [<span data-ttu-id="930bd-121">Start-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="930bd-121">Start-AzureRmVM</span></span>](/powershell/module/azurerm.compute/start-azurermvm)             |

<br>

<span data-ttu-id="930bd-122">hello 下列指令碼將逐步引導您取得 hello VM 和儲存體帳戶資訊、 選取 hello 資料磁碟，並指定 hello 新大小。</span><span class="sxs-lookup"><span data-stu-id="930bd-122">hello following script will walk you through getting hello VM and storage account information, selecting hello data disk and specifying hello new size.</span></span>

```powershell

# Select Azure Storage Account

    $storageAccount =
        Get-AzureRMStorageAccount | Out-GridView `
            -Title "Select Azure Storage Account" `
            -PassThru

    $rgName = $storageAccount.ResourceGroupName

# Select hello VM

    $vm = Get-AzureRMVM `
    -ResourceGroupName $rgName | Out-GridView `
            -Title "Select a VM …" `
            -PassThru

# Select Data Disk tooresize

    $disk =
        $vm.DataDiskNames | Out-GridView `
            -Title "Select a data disk tooresize" `
            -PassThru


# Specify a larger data disk size

    $size =  Read-Host `
        -Prompt "New size in GB"

# Stop and Deallocate VM prior tooresizing data disk

    $vm | Stop-AzureRMVM -Force

# Set hello new disk size

    Set-AzureRmVMDataDisk -VM $vm -Name "$disk" `
        -DiskSizeInGB $size

# Update hello configuration in Azure

    Update-AzureRmVM -VM $vm -ResourceGroupName $rgName

# Start hello VM
    Start-AzureRmVM -ResourceGroupName $rgName `
    -VMName $vm.name

```

## <a name="allocate-hello-unallocated-disk-space"></a><span data-ttu-id="930bd-123">配置 hello 未配置磁碟空間</span><span class="sxs-lookup"><span data-stu-id="930bd-123">Allocate hello unallocated disk space</span></span>

<span data-ttu-id="930bd-124">一旦您擁有 hello 磁碟機更大，您需要 tooallocate hello 新未配置的空間從 hello VM 內。</span><span class="sxs-lookup"><span data-stu-id="930bd-124">Once you have made hello drive larger, you need tooallocate hello new unallocated space from within hello VM.</span></span> <span data-ttu-id="930bd-125">tooallocate hello 空間，您可以連接 toohello VM 使用磁碟管理 (diskmgmt.msc)。</span><span class="sxs-lookup"><span data-stu-id="930bd-125">tooallocate hello space, you can connect toohello VM use Disk Management (diskmgmt.msc).</span></span> <span data-ttu-id="930bd-126">或者，如果您在建立時啟用 WinRM 和 hello VM 上的憑證，您可以使用遠端 PowerShell tooinitialize hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="930bd-126">Or, if you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="930bd-127">您也可以使用自訂指令碼擴充：</span><span class="sxs-lookup"><span data-stu-id="930bd-127">You can also use a custom script extension:</span></span>

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```

<span data-ttu-id="930bd-128">hello 指令碼檔案可以包含此程式碼 tooincrease hello 磁碟機配置 toohello 最大大小 hello 磁碟像這樣：</span><span class="sxs-lookup"><span data-stu-id="930bd-128">hello script file can contain something like this code tooincrease hello drive allocation toohello maximum size hello disks:</span></span>

```powershell
$driveLetter= "F"

$MaxSize = (Get-PartitionSupportedSize -DriveLetter $driveLetter).sizeMax

Resize-Partition -DriveLetter $driveLetter -Size $MaxSize
```

## <a name="next-steps"></a><span data-ttu-id="930bd-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="930bd-129">Next Steps</span></span>
- [<span data-ttu-id="930bd-130">深入了解磁碟和 VHD</span><span class="sxs-lookup"><span data-stu-id="930bd-130">Learn more about disks and VHDs</span></span>](../../storage/storage-about-disks-and-vhds-windows.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
