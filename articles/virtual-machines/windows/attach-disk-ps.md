---
title: "使用 PowerShell 在 Azure 中的 Windows VM 資料磁碟 tooa aaaAttach |Microsoft 文件"
description: "Tooattach 新的或現有的資料磁碟 tooa Windows VM 如何使用 PowerShell 和 hello Resource Manager 部署模型。"
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
ms.date: 02/07/2017
ms.author: cynthn
ms.openlocfilehash: 12ffdd4ced791ba0948047d3af24ad73e36c7ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-vm-using-powershell"></a><span data-ttu-id="93524-103">附加資料磁碟 tooa Windows VM 使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="93524-103">Attach a data disk tooa Windows VM using PowerShell</span></span>

<span data-ttu-id="93524-104">本文章將示範如何 tooattach 新的和現有磁碟 tooa 使用 PowerShell 的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="93524-104">This article shows you how tooattach both new and existing disks tooa Windows virtual machine using PowerShell.</span></span> <span data-ttu-id="93524-105">如果您的 VM 使用受控磁碟，您可以附加其他受控資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="93524-105">If your VM uses managed disks, you can attach additional managed data disks.</span></span> <span data-ttu-id="93524-106">您也可以附加 unmanaged 的資料磁碟 tooa 使用未受管理的磁碟儲存體帳戶中的 VM。</span><span class="sxs-lookup"><span data-stu-id="93524-106">You can also attach unmanaged data disks tooa VM that uses unmanaged disks in a storage account.</span></span>

<span data-ttu-id="93524-107">這麼做之前，請先檢閱下列提示：</span><span class="sxs-lookup"><span data-stu-id="93524-107">Before you do this, review these tips:</span></span>
* <span data-ttu-id="93524-108">hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。</span><span class="sxs-lookup"><span data-stu-id="93524-108">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="93524-109">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="93524-109">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="93524-110">toouse 高階儲存體，您將需要進階儲存體啟用像 hello DS 系列或 GS 系列虛擬機器的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="93524-110">toouse Premium storage, you'll need a Premium Storage enabled VM size like hello DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="93524-111">您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="93524-111">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="93524-112">僅特定地區可用進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="93524-112">Premium storage is available in certain regions.</span></span> <span data-ttu-id="93524-113">如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="93524-113">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="93524-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="93524-114">Before you begin</span></span>
<span data-ttu-id="93524-115">如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="93524-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="93524-116">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="93524-116">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="93524-117">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="93524-117">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="add-an-empty-data-disk-tooa-virtual-machine"></a><span data-ttu-id="93524-118">加入空的資料磁碟 tooa 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="93524-118">Add an empty data disk tooa virtual machine</span></span>

<span data-ttu-id="93524-119">這個範例會示範如何 tooadd 空的資料磁碟 tooan 現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="93524-119">This example shows how tooadd an empty data disk tooan existing virtual machine.</span></span>

### <a name="using-managed-disks"></a><span data-ttu-id="93524-120">使用受控磁碟</span><span class="sxs-lookup"><span data-stu-id="93524-120">Using managed disks</span></span>

```powershell
$rgName = 'myResourceGroup'
$vmName = 'myVM'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk1'

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Empty -DiskSizeGB 128

$dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

### <a name="using-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="93524-121">使用儲存體帳戶中的非受控磁碟</span><span class="sxs-lookup"><span data-stu-id="93524-121">Using unmanaged disks in a storage account</span></span>

```powershell
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    Add-AzureRmVMDataDisk -VM $vm -Name "disk-name" -VhdUri "https://mystore1.blob.core.windows.net/vhds/datadisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
```


### <a name="initialize-hello-disk"></a><span data-ttu-id="93524-122">初始化 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="93524-122">Initialize hello disk</span></span>

<span data-ttu-id="93524-123">加入空的磁碟之後，您需要 tooinitialize 它。</span><span class="sxs-lookup"><span data-stu-id="93524-123">After you add an empty disk, you need tooinitialize it.</span></span> <span data-ttu-id="93524-124">tooinitialize hello 磁碟，您可以登入 tooa VM 並使用磁碟管理。</span><span class="sxs-lookup"><span data-stu-id="93524-124">tooinitialize hello disk, you can log in tooa VM and use disk management.</span></span> <span data-ttu-id="93524-125">如果您在建立時啟用 WinRM 和 hello VM 上的憑證，您可以使用遠端 PowerShell tooinitialize hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="93524-125">If you enabled WinRM and a certificate on hello VM when you created it, you can use remote PowerShell tooinitialize hello disk.</span></span> <span data-ttu-id="93524-126">您也可以使用自訂指令碼擴充：</span><span class="sxs-lookup"><span data-stu-id="93524-126">You can also use a custom script extension:</span></span> 

```powershell
    $location = "location-name"
    $scriptName = "script-name"
    $fileName = "script-file-name"
    Set-AzureRmVMCustomScriptExtension -ResourceGroupName $rgName -Location $locName -VMName $vmName -Name $scriptName -TypeHandlerVersion "1.4" -StorageAccountName "mystore1" -StorageAccountKey "primary-key" -FileName $fileName -ContainerName "scripts"
```
        
<span data-ttu-id="93524-127">hello 指令碼檔案可以包含此程式碼 tooinitialize hello 磁碟像這樣：</span><span class="sxs-lookup"><span data-stu-id="93524-127">hello script file can contain something like this code tooinitialize hello disks:</span></span>

```powershell
    $disks = Get-Disk | Where partitionstyle -eq 'raw' | sort number

    $letters = 70..89 | ForEach-Object { [char]$_ }
    $count = 0
    $labels = "data1","data2"

    foreach ($disk in $disks) {
        $driveLetter = $letters[$count].ToString()
        $disk | 
        Initialize-Disk -PartitionStyle MBR -PassThru |
        New-Partition -UseMaximumSize -DriveLetter $driveLetter |
        Format-Volume -FileSystem NTFS -NewFileSystemLabel $labels[$count] -Confirm:$false -Force
    $count++
    }
```


## <a name="attach-an-existing-data-disk-tooa-vm"></a><span data-ttu-id="93524-128">附加現有的資料磁碟 tooa VM</span><span class="sxs-lookup"><span data-stu-id="93524-128">Attach an existing data disk tooa VM</span></span>

<span data-ttu-id="93524-129">您也可以將現有的 VHD 附加為受管理的資料磁碟 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="93524-129">You can also attach an existing VHD as a managed data disk tooa virtual machine.</span></span> 

### <a name="using-managed-disks"></a><span data-ttu-id="93524-130">使用受控磁碟</span><span class="sxs-lookup"><span data-stu-id="93524-130">Using managed disks</span></span>

```powershell
$rgName = 'myRG'
$vmName = 'ContosoMdPir3'
$location = 'West Central US' 
$storageType = 'PremiumLRS'
$dataDiskName = $vmName + '_datadisk2'
$dataVhdUri = 'https://mystorageaccount.blob.core.windows.net/vhds/managed_data_disk.vhd' 

$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Import -SourceUri $dataVhdUri -DiskSizeGB 128

$dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $diskConfig -ResourceGroupName $rgName

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk2.Id -Lun 2

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="next-steps"></a><span data-ttu-id="93524-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93524-131">Next steps</span></span>

<span data-ttu-id="93524-132">建立[快照集](snapshot-copy-managed-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="93524-132">Create a [snapshot](snapshot-copy-managed-disk.md).</span></span>
