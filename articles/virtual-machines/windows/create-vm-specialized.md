---
title: "從 Azure 中的特製化 VHD 建立 Windows VM | Microsoft Docs"
description: "在 Resource Manager 部署模型中連結特製化受控磁碟作為 OS 磁碟，以建立新的 Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: fa952286a9ceca8b3b2c7efe2cc4867a2728c477
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="df093-103">從特製化磁碟建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="df093-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="df093-104">使用 Powershell 連結特製化非受控磁碟作為 OS 磁碟，以建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="df093-104">Create a new VM by attaching a specialized managed disk as the OS disk using Powershell.</span></span> <span data-ttu-id="df093-105">特製化磁碟是現有 VM 中的虛擬硬碟 (VHD) 複本，可從原始的 VM 維護使用者帳戶、應用程式和其他狀態資料。</span><span class="sxs-lookup"><span data-stu-id="df093-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains the user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="df093-106">當您使用特製化 VHD 來建立新的 VM 時，新的 VM 會保留原始 VM 的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="df093-106">When you use a specialized VHD to create a new VM, the new VM retains the computer name of the original VM.</span></span> <span data-ttu-id="df093-107">系統也會保留其他電腦特定資訊，在某些情況下，此重複資訊可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="df093-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="df093-108">複製 VM 時，請留意您的應用程式會依賴哪些類型的電腦特定資訊。</span><span class="sxs-lookup"><span data-stu-id="df093-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="df093-109">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="df093-109">You have two options:</span></span>
* [<span data-ttu-id="df093-110">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="df093-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="df093-111">複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="df093-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="df093-112">本主題說明如何使用受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-112">This topic shows you how to use managed disks.</span></span> <span data-ttu-id="df093-113">如果您的舊版部署需要使用儲存體帳戶，請參閱[從儲存體帳戶中的特殊化 VHD 建立 VM](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="df093-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="df093-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="df093-114">Before you begin</span></span>
<span data-ttu-id="df093-115">如果您使用 PowerShell，請確定您擁有最新版的 AzureRM.Compute PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="df093-115">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="df093-116">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="df093-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="df093-117">選項 1：上傳特製化 VHD</span><span class="sxs-lookup"><span data-stu-id="df093-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="df093-118">您可以上傳從特製化的 VM，以在內部部署虛擬化工具，像是從另一個雲端匯出 HYPER-V 或在 VM 建立 VHD。</span><span class="sxs-lookup"><span data-stu-id="df093-118">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="df093-119">準備 VM</span><span class="sxs-lookup"><span data-stu-id="df093-119">Prepare the VM</span></span>
<span data-ttu-id="df093-120">如果您想要使用 VHD 現狀建立新的 VM，請確定完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="df093-120">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="df093-121">[準備要上傳至 Azure 的 Windows VHD](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="df093-121">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="df093-122">**不要**使用 Sysprep 一般化 VM。</span><span class="sxs-lookup"><span data-stu-id="df093-122">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="df093-123">移除 VM 上 (如 VMware 工具) 已安裝的任何來賓虛擬化工具和代理程式。</span><span class="sxs-lookup"><span data-stu-id="df093-123">Remove any guest virtualization tools and agents that are installed on the VM (like VMware tools).</span></span>
  * <span data-ttu-id="df093-124">確認已透過 DHCP 設定 VM 提取其 IP 位址和 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="df093-124">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="df093-125">這可確保伺服器在啟動時取得 VNet 內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df093-125">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="df093-126">取得儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="df093-126">Get the storage account</span></span>
<span data-ttu-id="df093-127">您需要一個 Azure 中的儲存體帳戶來儲存已上傳的 VHD。</span><span class="sxs-lookup"><span data-stu-id="df093-127">You need a storage account in Azure to store the uploaded VHD.</span></span> <span data-ttu-id="df093-128">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="df093-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="df093-129">若要顯示可用的儲存體帳戶，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="df093-129">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="df093-130">如果您想要使用現有的儲存體帳戶，請移至[上傳 VHD](#upload-the-vhd-to-your-storage-account) 一節。</span><span class="sxs-lookup"><span data-stu-id="df093-130">If you want to use an existing storage account, proceed to the [Upload the VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="df093-131">如果您需要建立儲存體帳戶，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="df093-131">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="df093-132">您需要在當中建立儲存體帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="df093-132">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="df093-133">若要找出您訂用帳戶中的所有資源群組，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="df093-133">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="df093-134">若要在*美國中部*區域建立名為 *myResourceGroup* 的資源群組，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="df093-134">To create a resource group named *myResourceGroup* in the *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="df093-135">使用 [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) Cmdlet，在此資源群組中建立名為 *mystorageaccount*的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="df093-135">Create a storage account named *mystorageaccount* in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="df093-136">將 VHD 上傳至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="df093-136">Upload the VHD to your storage account</span></span> 
<span data-ttu-id="df093-137">使用 [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) Cmdlet，將 VHD 上傳至儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="df093-137">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="df093-138">這個範例會將檔案 *myVHD.vhd* 從 `"C:\Users\Public\Documents\Virtual hard disks\"` 上傳至 *myResourceGroup* 資源群組中名為 *mystorageaccount* 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="df093-138">This example uploads the file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="df093-139">此檔案會儲存在名為 *mycontainer* 的容器中，而新的檔案名稱會是 *myUploadedVHD.vhd*。</span><span class="sxs-lookup"><span data-stu-id="df093-139">The file is stored in the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="df093-140">如果成功，您會得到看起來如以下的回應：</span><span class="sxs-lookup"><span data-stu-id="df093-140">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="df093-141">視您的網路連線和 VHD 檔案大小而定，此命令可能需要一些時間才能完成</span><span class="sxs-lookup"><span data-stu-id="df093-141">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

### <a name="create-a-managed-disk-from-the-vhd"></a><span data-ttu-id="df093-142">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="df093-142">Create a managed disk from the VHD</span></span>

<span data-ttu-id="df093-143">使用 [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)，從儲存體帳戶中的特製化 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-143">Create a managed disk from the specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="df093-144">這個範例使用 **myOSDisk1** 作為磁碟名稱，將磁碟放入 *StandardLRS* 儲存體，並使用 *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* 作為來源 VHD 的 URI。</span><span class="sxs-lookup"><span data-stu-id="df093-144">This example uses **myOSDisk1** for the disk name, puts the disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as the URI for the source VHD.</span></span>

<span data-ttu-id="df093-145">建立新 VM 的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="df093-145">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="df093-146">從已上傳的 VHD 建立新的 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-146">Create the new OS disk from the uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="df093-147">選項 2：複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="df093-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="df093-148">您可以製作 VM 的快照集，然後使用該，快照集來建立新的受控磁碟和新的 VM，進而建立使用受控磁碟的 VM 複本。</span><span class="sxs-lookup"><span data-stu-id="df093-148">You can create a copy of a VM that uses managed disks by taking a snapshot of the VM, then using that snapshot to create a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-the-os-disk"></a><span data-ttu-id="df093-149">製作 OS 磁碟的快照集</span><span class="sxs-lookup"><span data-stu-id="df093-149">Take a snapshot of the OS disk</span></span>

<span data-ttu-id="df093-150">您可以製作整個 VM (包括所有磁碟) 或僅只單一磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="df093-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="df093-151">下列步驟說明如何使用 [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) Cmdlet，製作僅只您 VM 之 OS 磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="df093-151">The following steps show you how to take a snapshot of just the OS disk of your VM using the [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="df093-152">設定部分參數。</span><span class="sxs-lookup"><span data-stu-id="df093-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="df093-153">取得 VM 物件。</span><span class="sxs-lookup"><span data-stu-id="df093-153">Get the VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="df093-154">取得 OS 磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="df093-154">Get the OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="df093-155">建立快照集組態。</span><span class="sxs-lookup"><span data-stu-id="df093-155">Create the snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="df093-156">建立快照集。</span><span class="sxs-lookup"><span data-stu-id="df093-156">Take the snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="df093-157">如果您計劃使用快照集來建立必須是高效能的 VM，請在 New-AzureRmSnapshot 命令中使用參數 `-AccountType Premium_LRS`。</span><span class="sxs-lookup"><span data-stu-id="df093-157">If you plan to use the snapshot to create a VM that needs to be high performing, use the parameter `-AccountType Premium_LRS` with the New-AzureRmSnapshot command.</span></span> <span data-ttu-id="df093-158">此參數建立的快照集會儲存為進階受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-158">The parameter creates the snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="df093-159">進階受控磁碟的價格高於「標準」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="df093-160">因此，使用該參數之前，請確定您真的需要「進階」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-160">So be sure you really need Premium before using the parameter.</span></span>

### <a name="create-a-new-disk-from-the-snapshot"></a><span data-ttu-id="df093-161">從快照集建立新的磁碟</span><span class="sxs-lookup"><span data-stu-id="df093-161">Create a new disk from the snapshot</span></span>

<span data-ttu-id="df093-162">使用 [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)，從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-162">Create a managed disk from the snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="df093-163">這個範例會使用 *myOSDisk* 作為磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="df093-163">This example uses *myOSDisk* for the disk name.</span></span>

<span data-ttu-id="df093-164">建立新 VM 的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="df093-164">Create a new resource group for the new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="df093-165">設定 OS 磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="df093-165">Set the OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="df093-166">建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-166">Create the managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-the-new-vm"></a><span data-ttu-id="df093-167">建立新 VM</span><span class="sxs-lookup"><span data-stu-id="df093-167">Create the new VM</span></span> 

<span data-ttu-id="df093-168">建立新 VM 所要使用的網路和其他 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="df093-168">Create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="df093-169">建立子網路和 VNet</span><span class="sxs-lookup"><span data-stu-id="df093-169">Create the subNet and vNet</span></span>

<span data-ttu-id="df093-170">建立 [虛擬網路](../../virtual-network/virtual-networks-overview.md)的 vNet 和 subNet。</span><span class="sxs-lookup"><span data-stu-id="df093-170">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="df093-171">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="df093-171">Create the subNet.</span></span> <span data-ttu-id="df093-172">此範例會在資源群組 **myDestinationResourceGroup** 中建立名為 **mySubnet** 的子網路，並將子網路位址首碼設定為 **10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="df093-172">This example creates a subnet named **mySubNet**, in the resource group **myDestinationResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="df093-173">建立 vNet。</span><span class="sxs-lookup"><span data-stu-id="df093-173">Create the vNet.</span></span> <span data-ttu-id="df093-174">此範例會將虛擬網路名稱設定為 **myVnetName**、位置設定為 **美國西部**，及虛擬網路的位址首碼設定為 **10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="df093-174">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="df093-175">建立網路安全性群組和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="df093-175">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="df093-176">若要能夠使用 RDP 登入 VM，您必須有可在連接埠 3389 上允許 RDP 存取的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="df093-176">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="df093-177">因為新 VM 的 VHD 是建立自現有的特製化 VM，您可以使用來自 RDP 來源虛擬機器的帳戶。</span><span class="sxs-lookup"><span data-stu-id="df093-177">Because the VHD for the new VM was created from an existing specialized VM, you can use an account from the source virtual machine for RDP.</span></span>

<span data-ttu-id="df093-178">此範例會將 NSG 名稱設定為 **myNsg** 以及將 RDP 規則名稱設定為 **myRdpRule**。</span><span class="sxs-lookup"><span data-stu-id="df093-178">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="df093-179">如需端點和 NSG 規則的詳細資訊，請參閱[使用 PowerShell 對 Azure 中的 VM 開啟連接埠](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="df093-179">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="df093-180">建立公用 IP 位址和 NIC</span><span class="sxs-lookup"><span data-stu-id="df093-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="df093-181">若要能夠與虛擬網路中的虛擬機器進行通訊，您需要 [公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 和網路介面。</span><span class="sxs-lookup"><span data-stu-id="df093-181">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="df093-182">建立公用 IP。</span><span class="sxs-lookup"><span data-stu-id="df093-182">Create the public IP.</span></span> <span data-ttu-id="df093-183">在此範例中，公用 IP 位址名稱會設定為 **myIP**。</span><span class="sxs-lookup"><span data-stu-id="df093-183">In this example, the public IP address name is set to **myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="df093-184">建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="df093-184">Create the NIC.</span></span> <span data-ttu-id="df093-185">在此範例中，NIC 名稱會設定為 **myNicName**。</span><span class="sxs-lookup"><span data-stu-id="df093-185">In this example, the NIC name is set to **myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="df093-186">設定 VM 名稱和大小</span><span class="sxs-lookup"><span data-stu-id="df093-186">Set the VM name and size</span></span>

<span data-ttu-id="df093-187">此範例將 VM 名稱設定為 myVM，將 VM 大小設定為 Standard_A2。</span><span class="sxs-lookup"><span data-stu-id="df093-187">This example sets the VM name to *myVM* and the VM size to *Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="df093-188">新增 NIC</span><span class="sxs-lookup"><span data-stu-id="df093-188">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-the-os-disk"></a><span data-ttu-id="df093-189">新增 OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="df093-189">Add the OS disk</span></span> 

<span data-ttu-id="df093-190">使用 [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) 將 OS 磁碟新增至組態。</span><span class="sxs-lookup"><span data-stu-id="df093-190">Add the OS disk to the configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="df093-191">這個範例將磁碟大小設定為 *128GB*，並附加受控磁碟作為 *Windows* OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="df093-191">This example sets the size of the disk to *128 GB* and attaches the managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-the-vm"></a><span data-ttu-id="df093-192">完成 VM</span><span class="sxs-lookup"><span data-stu-id="df093-192">Complete the VM</span></span> 

<span data-ttu-id="df093-193">使用 [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm) 以及我們剛才建立的組態建立 VM。</span><span class="sxs-lookup"><span data-stu-id="df093-193">Create the VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)the configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="df093-194">如果此命令成功，您會看到如下的輸出︰</span><span class="sxs-lookup"><span data-stu-id="df093-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="df093-195">確認已建立 VM</span><span class="sxs-lookup"><span data-stu-id="df093-195">Verify that the VM was created</span></span>
<span data-ttu-id="df093-196">從 [Azure 入口網站](https://portal.azure.com)的 [瀏覽] > [虛擬機器]下，或是使用下列 PowerShell 命令，應可看到新建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="df093-196">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="df093-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df093-197">Next steps</span></span>
<span data-ttu-id="df093-198">若要登入新的虛擬機器，請瀏覽至[入口網站](https://portal.azure.com)中的 VM，按一下 [連接] 並開啟遠端桌面 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="df093-198">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="df093-199">使用原始虛擬機器的帳戶認證來登入新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="df093-199">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="df093-200">如需詳細資訊，請參閱 [如何連接和登入執行 Windows 的 Azure 虛擬機器](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="df093-200">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

