---
title: "在 Azure 中的特定 VHD 從 Windows VM aaaCreate |Microsoft 文件"
description: "建立新的 Windows VM，藉由將特定的受管理的磁碟附加為 hello hello 資源管理員部署模型中使用的作業系統磁碟。"
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
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="3e4a7-103">從特製化磁碟建立 Windows VM</span><span class="sxs-lookup"><span data-stu-id="3e4a7-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="3e4a7-104">藉由將特定的受管理的磁碟附加為 hello OS 磁碟使用 Powershell 建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="3e4a7-105">專用的磁碟是從現有的 VM 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM 的虛擬硬碟 (VHD) 的複本。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="3e4a7-106">當您使用特殊的 VHD toocreate 新的 VM 時，新的 VM 會保留 hello 電腦名稱的 hello hello 原始 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="3e4a7-107">系統也會保留其他電腦特定資訊，在某些情況下，此重複資訊可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="3e4a7-108">複製 VM 時，請留意您的應用程式會依賴哪些類型的電腦特定資訊。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="3e4a7-109">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-109">You have two options:</span></span>
* [<span data-ttu-id="3e4a7-110">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="3e4a7-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="3e4a7-111">複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="3e4a7-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="3e4a7-112">本主題說明如何 toouse 管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="3e4a7-113">如果您的舊版部署需要使用儲存體帳戶，請參閱[從儲存體帳戶中的特殊化 VHD 建立 VM](sa-create-vm-specialized.md)</span><span class="sxs-lookup"><span data-stu-id="3e4a7-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3e4a7-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="3e4a7-114">Before you begin</span></span>
<span data-ttu-id="3e4a7-115">如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="3e4a7-116">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="3e4a7-117">選項 1：上傳特製化 VHD</span><span class="sxs-lookup"><span data-stu-id="3e4a7-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="3e4a7-118">您可以上傳的 hello 與內部部署虛擬化工具，像是從另一個雲端匯出 HYPER-V 或在 VM 建立從特製化的 VM 的 VHD。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="3e4a7-119">準備 VM hello</span><span class="sxs-lookup"><span data-stu-id="3e4a7-119">Prepare hello VM</span></span>
<span data-ttu-id="3e4a7-120">如果您想 toouse hello VHD 當做-是 toocreate 新的 VM，請完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="3e4a7-121">[準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="3e4a7-122">**不這麼做**一般化 hello VM 使用 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="3e4a7-123">移除任何客體的虛擬化工具和 hello VM （例如 VMware 工具） 所安裝的代理程式。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="3e4a7-124">請確定 hello VM 是已設定的 toopull 其 IP 位址和 DNS 設定，透過 DHCP。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="3e4a7-125">這可確保該 hello 伺服器會在啟動時，取得 hello VNet 內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="3e4a7-126">取得 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3e4a7-126">Get hello storage account</span></span>
<span data-ttu-id="3e4a7-127">您需要儲存體帳戶中 Azure toostore hello 上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="3e4a7-128">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="3e4a7-129">tooshow hello 可用儲存體帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="3e4a7-130">如果您想 toouse 現有的儲存體帳戶，請繼續 toohello[上載 hello VHD](#upload-the-vhd-to-your-storage-account) > 一節。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="3e4a7-131">如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="3e4a7-132">您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="3e4a7-133">toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="3e4a7-134">資源群組命名為的 toocreate *myResourceGroup*在 hello*美國西部*區域中，輸入：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="3e4a7-135">建立名為儲存體帳戶*mystorageaccount*使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3e4a7-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="3e4a7-136">上傳 hello VHD tooyour 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3e4a7-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="3e4a7-137">使用 hello[新增 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa 容器儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="3e4a7-138">此範例中上傳 hello 檔案*myVHD.vhd*從`"C:\Users\Public\Documents\Virtual hard disks\"`tooa 儲存體帳戶*mystorageaccount*在 hello *myResourceGroup*資源群組。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="3e4a7-139">hello 檔案會儲存在名為 「 hello 容器*mycontainer* hello 新的檔案名稱將會*myUploadedVHD.vhd*。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="3e4a7-140">如果成功的話，您會收到的回應，看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="3e4a7-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="3e4a7-141">根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete</span><span class="sxs-lookup"><span data-stu-id="3e4a7-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="3e4a7-142">從 hello VHD 建立受管理的磁碟</span><span class="sxs-lookup"><span data-stu-id="3e4a7-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="3e4a7-143">從 hello 建立受管理的磁碟在儲存體帳戶中使用特製化 VHD[新增 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="3e4a7-144">這個範例會使用**myOSDisk1** hello 磁碟名稱 中，將 hello 磁碟*StandardLRS*存放裝置，並使用*https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd*為 hello hello 來源 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="3e4a7-145">建立新的資源群組 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="3e4a7-146">建立從 hello hello 新作業系統磁碟上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="3e4a7-147">選項 2：複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="3e4a7-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="3e4a7-148">您可以建立一份使用受磁碟 hello VM 的快照，然後使用該快照集 toocreate 新受管理的磁碟和新的 VM 的 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="3e4a7-149">取得 hello 作業系統磁碟的快照</span><span class="sxs-lookup"><span data-stu-id="3e4a7-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="3e4a7-150">您可以製作整個 VM (包括所有磁碟) 或僅只單一磁碟的快照集。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="3e4a7-151">hello 下列步驟說明如何 tootake 只 hello OS 磁碟 VM 使用的快照集 hello[新增 AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="3e4a7-152">設定部分參數。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="3e4a7-153">收到 hello VM 物件。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="3e4a7-154">收到 hello 作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="3e4a7-155">建立 hello 快照集設定。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="3e4a7-156">取得 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="3e4a7-157">如果您計劃 toouse hello 快照 toocreate 需要 toobe 高執行 VM 時，使用 hello 參數`-AccountType Premium_LRS`hello 新增 AzureRmSnapshot 命令。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="3e4a7-158">hello 參數建立 hello 快照集，使它儲存為 Premium 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="3e4a7-159">進階受控磁碟的價格高於「標準」受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="3e4a7-160">因此務必真的需要付費才能使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="3e4a7-161">從 hello 快照集建立新的磁碟</span><span class="sxs-lookup"><span data-stu-id="3e4a7-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="3e4a7-162">建立受管理的磁碟，從快照集使用的 hello[新增 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="3e4a7-163">這個範例會使用*myOSDisk* hello 磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="3e4a7-164">建立新的資源群組 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="3e4a7-165">設定 hello 作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="3e4a7-166">建立 hello 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="3e4a7-167">建立 hello 新的 VM</span><span class="sxs-lookup"><span data-stu-id="3e4a7-167">Create hello new VM</span></span> 

<span data-ttu-id="3e4a7-168">網路功能與 hello 所使用的其他 VM 資源 toobe 建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="3e4a7-169">建立 hello 子網路和 vNet</span><span class="sxs-lookup"><span data-stu-id="3e4a7-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="3e4a7-170">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="3e4a7-171">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-171">Create hello subNet.</span></span> <span data-ttu-id="3e4a7-172">這個範例會建立名為的子網路**mySubNet**，hello 資源群組中**myDestinationResourceGroup**，並設定太 hello 子網路位址首碼**10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="3e4a7-173">建立 hello vNet。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-173">Create hello vNet.</span></span> <span data-ttu-id="3e4a7-174">此範例中設定 hello 虛擬網路名稱 toobe **myVnetName**，太 hello 位置**美國西部**，太 hello hello 虛擬網路的位址前置詞和**10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3e4a7-175">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="3e4a7-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="3e4a7-176">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 允許連接埠 3389 RDP 存取權的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="3e4a7-177">因為 hello 的 hello 從現有特製化的 VM 建立新的 VM 的 VHD，您可以使用帳戶 hello 來源虛擬機器從 rdp。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="3e4a7-178">此範例中設定 hello NSG 名稱太**myNsg**和 hello RDP 規則名稱太**myRdpRule**。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="3e4a7-179">如需有關端點和 NSG 規則的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="3e4a7-180">建立公用 IP 位址和 NIC</span><span class="sxs-lookup"><span data-stu-id="3e4a7-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="3e4a7-181">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="3e4a7-182">建立 hello 公用 IP。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-182">Create hello public IP.</span></span> <span data-ttu-id="3e4a7-183">在此範例中，hello 公用 IP 位址名稱設定太**myIP**。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="3e4a7-184">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-184">Create hello NIC.</span></span> <span data-ttu-id="3e4a7-185">在此範例中，hello NIC 設定名稱太**myNicName**。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="3e4a7-186">設定 hello VM 名稱和大小</span><span class="sxs-lookup"><span data-stu-id="3e4a7-186">Set hello VM name and size</span></span>

<span data-ttu-id="3e4a7-187">此範例中設定 hello VM 名稱太*myVM*和 hello VM 大小太*Standard_A2*。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="3e4a7-188">新增 hello NIC</span><span class="sxs-lookup"><span data-stu-id="3e4a7-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="3e4a7-189">新增 hello OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="3e4a7-189">Add hello OS disk</span></span> 

<span data-ttu-id="3e4a7-190">Hello OS 磁碟 toohello 設定使用新增[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="3e4a7-191">此範例會設定 hello hello 磁碟大小太*128 GB*附加 hello 受管理的磁碟和*Windows*作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="3e4a7-192">完成 hello VM</span><span class="sxs-lookup"><span data-stu-id="3e4a7-192">Complete hello VM</span></span> 

<span data-ttu-id="3e4a7-193">建立 hello VM 使用[新增 AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello 剛才所建立的組態。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="3e4a7-194">如果此命令成功，您會看到如下的輸出︰</span><span class="sxs-lookup"><span data-stu-id="3e4a7-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="3e4a7-195">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="3e4a7-195">Verify that hello VM was created</span></span>
<span data-ttu-id="3e4a7-196">您應該會看到 hello 新建立的 VM 在 hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用下列 PowerShell hello命令：</span><span class="sxs-lookup"><span data-stu-id="3e4a7-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3e4a7-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e4a7-197">Next steps</span></span>
<span data-ttu-id="3e4a7-198">在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="3e4a7-199">Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="3e4a7-200">如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="3e4a7-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

