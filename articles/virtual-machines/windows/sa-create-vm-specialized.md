---
title: "從專用的磁碟在 Azure 中的 VM aaaCreate |Microsoft 文件"
description: "藉由附加專用的 unmanaged 的磁碟，hello Resource Manager 部署模型中建立新的 VM。"
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="fd95e-103">從儲存體帳戶中的特製化 VHD 建立 VM</span><span class="sxs-lookup"><span data-stu-id="fd95e-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="fd95e-104">藉由將專用的 unmanaged 的磁碟附加為 hello OS 磁碟使用 Powershell 建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="fd95e-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="fd95e-105">專用的磁碟是從現有的 VM 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM VHD 的複本。</span><span class="sxs-lookup"><span data-stu-id="fd95e-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="fd95e-106">您有兩個選擇：</span><span class="sxs-lookup"><span data-stu-id="fd95e-106">You have two options:</span></span>
* [<span data-ttu-id="fd95e-107">上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="fd95e-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="fd95e-108">複製現有的 Azure VM 的 VHD hello</span><span class="sxs-lookup"><span data-stu-id="fd95e-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="fd95e-109">開始之前</span><span class="sxs-lookup"><span data-stu-id="fd95e-109">Before you begin</span></span>
<span data-ttu-id="fd95e-110">如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="fd95e-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="fd95e-111">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="fd95e-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="fd95e-112">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="fd95e-113">選項 1：上傳特製化 VHD</span><span class="sxs-lookup"><span data-stu-id="fd95e-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="fd95e-114">您可以上傳的 hello 與內部部署虛擬化工具，像是從另一個雲端匯出 HYPER-V 或在 VM 建立從特製化的 VM 的 VHD。</span><span class="sxs-lookup"><span data-stu-id="fd95e-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="fd95e-115">準備 VM hello</span><span class="sxs-lookup"><span data-stu-id="fd95e-115">Prepare hello VM</span></span>
<span data-ttu-id="fd95e-116">您可以上傳使用內部部署 VM 建立的特製化 VHD，或上傳從另一個雲端匯出的 VHD。</span><span class="sxs-lookup"><span data-stu-id="fd95e-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="fd95e-117">特製化的 VHD 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM。</span><span class="sxs-lookup"><span data-stu-id="fd95e-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="fd95e-118">如果您想 toouse hello VHD 當做-是 toocreate 新的 VM，請完成下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="fd95e-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="fd95e-119">[準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="fd95e-120">**不這麼做**一般化 hello VM 使用 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="fd95e-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="fd95e-121">移除任何客體的虛擬化工具和 hello VM （也就是 VMware 工具） 所安裝的代理程式。</span><span class="sxs-lookup"><span data-stu-id="fd95e-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="fd95e-122">請確定 hello VM 是已設定的 toopull 其 IP 位址和 DNS 設定，透過 DHCP。</span><span class="sxs-lookup"><span data-stu-id="fd95e-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="fd95e-123">這可確保該 hello 伺服器會在啟動時，取得 hello VNet 內的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fd95e-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="fd95e-124">取得 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fd95e-124">Get hello storage account</span></span>
<span data-ttu-id="fd95e-125">您需要 Azure toostore hello 上傳 VM 映像的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd95e-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="fd95e-126">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd95e-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="fd95e-127">tooshow hello 可用儲存體帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="fd95e-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="fd95e-128">如果您想 toouse 現有的儲存體帳戶，請繼續 toohello [hello VM 映像上載](#upload-the-vm-vhd-to-your-storage-account)> 一節。</span><span class="sxs-lookup"><span data-stu-id="fd95e-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="fd95e-129">如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="fd95e-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="fd95e-130">您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="fd95e-131">toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="fd95e-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="fd95e-132">資源群組命名為的 toocreate **myResourceGroup**在 hello**美國西部**區域中，輸入：</span><span class="sxs-lookup"><span data-stu-id="fd95e-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="fd95e-133">建立名為儲存體帳戶**mystorageaccount**使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fd95e-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="fd95e-134">上傳 hello VHD tooyour 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="fd95e-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="fd95e-135">使用 hello[新增 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello 影像 tooa 容器儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="fd95e-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="fd95e-136">此範例中上傳 hello 檔案**myVHD.vhd**從`"C:\Users\Public\Documents\Virtual hard disks\"`tooa 儲存體帳戶**mystorageaccount**在 hello **myResourceGroup**資源群組。</span><span class="sxs-lookup"><span data-stu-id="fd95e-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="fd95e-137">hello 檔案會放入名為 「 hello 容器**mycontainer** hello 新的檔案名稱將會**myUploadedVHD.vhd**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="fd95e-138">如果成功的話，您會收到的回應，看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="fd95e-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="fd95e-139">根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="fd95e-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="fd95e-140">選項 2: Hello VHD 複製現有的 Azure VM</span><span class="sxs-lookup"><span data-stu-id="fd95e-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="fd95e-141">建立新的、 重複的 VM 時，您可以複製 VHD tooanother 儲存體帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="fd95e-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="fd95e-142">開始之前</span><span class="sxs-lookup"><span data-stu-id="fd95e-142">Before you begin</span></span>
<span data-ttu-id="fd95e-143">請確定您︰</span><span class="sxs-lookup"><span data-stu-id="fd95e-143">Make sure that you:</span></span>

* <span data-ttu-id="fd95e-144">會有資訊 hello**來源和目的地儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="fd95e-145">Hello 來源 VM，您需要 toohave hello 儲存體帳戶和容器名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="fd95e-146">通常，是 hello 容器名稱**vhd**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="fd95e-147">您也需要 toohave 目的地儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd95e-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="fd95e-148">如果您還沒有其中一個，您可以建立一個使用任一個 hello 入口網站 (**更服務**> 儲存體帳戶 > 加入) 或使用 hello[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="fd95e-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="fd95e-149">已下載並安裝 hello [AzCopy 工具](../../storage/common/storage-use-azcopy.md)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="fd95e-150">Hello VM 解除配置</span><span class="sxs-lookup"><span data-stu-id="fd95e-150">Deallocate hello VM</span></span>
<span data-ttu-id="fd95e-151">解除配置 VM，這可釋 hello VHD toobe 複製 hello。</span><span class="sxs-lookup"><span data-stu-id="fd95e-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="fd95e-152">**入口網站**︰ 按一下 [虛擬機器]  >  [myVM] > [停止]</span><span class="sxs-lookup"><span data-stu-id="fd95e-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="fd95e-153">**Powershell**： 使用[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop （解除配置） hello 名為 VM **myVM**資源群組中**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="fd95e-154">hello**狀態**hello VM 在 hello Azure 入口網站變更從**已停止**太**已停止 （取消配置）**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="fd95e-155">取得 hello 儲存體帳戶 Url</span><span class="sxs-lookup"><span data-stu-id="fd95e-155">Get hello storage account URLs</span></span>
<span data-ttu-id="fd95e-156">您需要 hello hello 來源和目的地儲存體帳戶的 Url。</span><span class="sxs-lookup"><span data-stu-id="fd95e-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="fd95e-157">hello Url 如下： `https://<storageaccount>.blob.core.windows.net/<containerName>/`。</span><span class="sxs-lookup"><span data-stu-id="fd95e-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="fd95e-158">如果您已經知道 hello 儲存體帳戶和容器名稱，您可以只取代之間 hello 方括號 toocreate hello 資訊 URL。</span><span class="sxs-lookup"><span data-stu-id="fd95e-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="fd95e-159">您可以使用 hello Azure 入口網站或 Azure Powershell tooget hello URL:</span><span class="sxs-lookup"><span data-stu-id="fd95e-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="fd95e-160">**入口網站**： 按一下 hello  **>** 如**更多服務** > **儲存體帳戶** >  *儲存體帳戶* > **Blob**和原始程式 VHD 檔可能是 hello **vhd**容器。</span><span class="sxs-lookup"><span data-stu-id="fd95e-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="fd95e-161">按一下**屬性**hello 容器和複製 hello 文字標示為**URL**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="fd95e-162">您將需要這兩個 hello 來源和目的地容器的 hello Url。</span><span class="sxs-lookup"><span data-stu-id="fd95e-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="fd95e-163">**Powershell**： 使用[Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)名為 VM 的 tooget hello 資訊**myVM** hello 資源群組中**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="fd95e-164">在 hello 結果，請查看 hello**儲存體設定檔**hello 區段**Vhd Uri**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="fd95e-165">hello 的 hello Uri 的第一個部分是 hello URL toohello 容器和 hello 最後一個部分是 hello hello VM 的 OS VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="fd95e-166">取得 hello 儲存體存取金鑰</span><span class="sxs-lookup"><span data-stu-id="fd95e-166">Get hello storage access keys</span></span>
<span data-ttu-id="fd95e-167">尋找 hello hello 便捷鍵的來源和目的地儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd95e-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="fd95e-168">如需存取金鑰的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](../../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="fd95e-169">**入口網站**︰按一下 [更多服務]  > [儲存體帳戶]  > [儲存體帳戶] > [存取金鑰]。</span><span class="sxs-lookup"><span data-stu-id="fd95e-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="fd95e-170">複製 hello 機碼標示為**key1**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="fd95e-171">**Powershell**： 使用[Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello hello 儲存體帳戶的儲存體金鑰**mystorageaccount** hello 資源群組中**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="fd95e-172">複製 hello 機碼標示為**key1**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="fd95e-173">複製 hello VHD</span><span class="sxs-lookup"><span data-stu-id="fd95e-173">Copy hello VHD</span></span>
<span data-ttu-id="fd95e-174">您可以使用 AzCopy 在儲存體帳戶之間複製檔案。</span><span class="sxs-lookup"><span data-stu-id="fd95e-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="fd95e-175">Hello 目的地容器，如果 hello 指定的容器不存在，它就會為您建立。</span><span class="sxs-lookup"><span data-stu-id="fd95e-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="fd95e-176">toouse AzCopy，開啟命令提示字元在本機電腦上，並瀏覽 toohello AzCopy 安裝所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fd95e-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="fd95e-177">它將會類似太*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*。</span><span class="sxs-lookup"><span data-stu-id="fd95e-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="fd95e-178">toocopy hello 的所有檔案的容器內，使用 hello **/S**切換。</span><span class="sxs-lookup"><span data-stu-id="fd95e-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="fd95e-179">這可以是使用的 toocopy hello 作業系統 VHD 和所有 hello 資料磁碟，如果它們是在 hello 相同的容器。</span><span class="sxs-lookup"><span data-stu-id="fd95e-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="fd95e-180">這個範例會示範如何 toocopy hello 的所有檔案在 hello 容器**mysourcecontainer**儲存體帳戶中**mysourcestorageaccount** toohello 容器**mydestinationcontainer**在 hello **mydestinationstorageaccount**儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fd95e-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="fd95e-181">以您自己取代 hello hello 儲存體帳戶和容器的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="fd95e-182">使用您自己的金鑰取代 `<sourceStorageAccountKey1>` 和 `<destinationStorageAccountKey1>`。</span><span class="sxs-lookup"><span data-stu-id="fd95e-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="fd95e-183">如果您只想 toocopy 容器中的特定 VHD 與多個檔案，您也可以指定使用 hello /Pattern 交換器 hello 檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="fd95e-184">在此範例中，只有 hello 檔名為**myFileName.vhd**會被複製。</span><span class="sxs-lookup"><span data-stu-id="fd95e-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="fd95e-185">完成時，您將收到如下的訊息：</span><span class="sxs-lookup"><span data-stu-id="fd95e-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="fd95e-186">疑難排解</span><span class="sxs-lookup"><span data-stu-id="fd95e-186">Troubleshooting</span></span>
* <span data-ttu-id="fd95e-187">當您使用 AZCopy，如果您看到 hello 錯誤 「 伺服器無法 tooauthenticate hello 要求 」 時，請確定 hello hello 授權標頭值格式正確並包含 hello 簽章。</span><span class="sxs-lookup"><span data-stu-id="fd95e-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="fd95e-188">如果您使用索引鍵 2 或 hello 次要儲存體金鑰，請嘗試使用 hello 主要或第 1 個儲存體金鑰。</span><span class="sxs-lookup"><span data-stu-id="fd95e-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="fd95e-189">建立 hello 新的 VM</span><span class="sxs-lookup"><span data-stu-id="fd95e-189">Create hello new VM</span></span> 

<span data-ttu-id="fd95e-190">您需要 toocreate 網路功能與其他 VM 資源 toobe hello 使用新的 VM。</span><span class="sxs-lookup"><span data-stu-id="fd95e-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="fd95e-191">建立 hello 子網路和 vNet</span><span class="sxs-lookup"><span data-stu-id="fd95e-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="fd95e-192">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="fd95e-193">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="fd95e-193">Create hello subNet.</span></span> <span data-ttu-id="fd95e-194">這個範例會建立名為的子網路**mySubNet**，hello 資源群組中**myResourceGroup**，並設定太 hello 子網路位址首碼**10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="fd95e-195">建立 hello vNet。</span><span class="sxs-lookup"><span data-stu-id="fd95e-195">Create hello vNet.</span></span> <span data-ttu-id="fd95e-196">此範例中設定 hello 虛擬網路名稱 toobe **myVnetName**，太 hello 位置**美國西部**，太 hello hello 虛擬網路的位址前置詞和**10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="fd95e-197">建立公用 IP 位址和 NIC</span><span class="sxs-lookup"><span data-stu-id="fd95e-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="fd95e-198">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="fd95e-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="fd95e-199">建立 hello 公用 IP。</span><span class="sxs-lookup"><span data-stu-id="fd95e-199">Create hello public IP.</span></span> <span data-ttu-id="fd95e-200">在此範例中，hello 公用 IP 位址名稱設定太**myIP**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="fd95e-201">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="fd95e-201">Create hello NIC.</span></span> <span data-ttu-id="fd95e-202">在此範例中，hello NIC 設定名稱太**myNicName**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="fd95e-203">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="fd95e-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="fd95e-204">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 安全性規則，允許連接埠 3389 RDP 存取權。</span><span class="sxs-lookup"><span data-stu-id="fd95e-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="fd95e-205">Hello VHD 已建立新的 VM，從現有的 hello 特製化，因為 VM hello VM 建立您之後可以使用現有的帳戶從有權限 toolog 上使用 RDP 的 hello 來源虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd95e-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="fd95e-206">此範例中設定 hello NSG 名稱太**myNsg**和 hello RDP 規則名稱太**myRdpRule**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="fd95e-207">如需有關端點和 NSG 規則的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="fd95e-208">設定 hello VM 名稱和大小</span><span class="sxs-lookup"><span data-stu-id="fd95e-208">Set hello VM name and size</span></span>

<span data-ttu-id="fd95e-209">此範例中設定 hello VM 名稱太"myVM 」 和 hello VM 大小太"Standard_A2"。</span><span class="sxs-lookup"><span data-stu-id="fd95e-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="fd95e-210">新增 hello NIC</span><span class="sxs-lookup"><span data-stu-id="fd95e-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="fd95e-211">設定 hello OS 磁碟</span><span class="sxs-lookup"><span data-stu-id="fd95e-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="fd95e-212">設定您上傳或複製的 VHD hello URI。</span><span class="sxs-lookup"><span data-stu-id="fd95e-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="fd95e-213">在此範例中，hello VHD 檔案命名為**myOsDisk.vhd**保留在儲存體帳戶中**myStorageAccount**中名為的容器**myContainer**。</span><span class="sxs-lookup"><span data-stu-id="fd95e-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="fd95e-214">新增 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="fd95e-214">Add hello OS disk.</span></span> <span data-ttu-id="fd95e-215">在此範例中，建立 hello 作業系統磁碟時，hello 詞彙"osDisk"會是 appened toohello VM 名稱 toocreate hello 作業系統磁碟名稱。</span><span class="sxs-lookup"><span data-stu-id="fd95e-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="fd95e-216">此範例也會指定此 windows VHD 應該附加的 toohello 為 hello OS 磁碟的 VM。</span><span class="sxs-lookup"><span data-stu-id="fd95e-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="fd95e-217">選擇性： 如果您有資料磁碟的需要 toobe 附加 toohello VM、 使用的資料 Vhd hello Url 新增 hello 資料磁碟和 hello 適當的邏輯單元編號 (Lun)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="fd95e-218">使用時的儲存體帳戶，hello 資料及作業系統磁碟 Url 看起來像這樣： `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`。</span><span class="sxs-lookup"><span data-stu-id="fd95e-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="fd95e-219">您可以在 hello 入口網站上找到此來瀏覽 toohello 目標儲存體容器，按一下 hello 作業系統或資料已複製的 VHD，然後複製 hello URL hello 內容。</span><span class="sxs-lookup"><span data-stu-id="fd95e-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="fd95e-220">完成 hello VM</span><span class="sxs-lookup"><span data-stu-id="fd95e-220">Complete hello VM</span></span> 

<span data-ttu-id="fd95e-221">建立 hello 使用我們剛才建立的 hello 組態的 VM。</span><span class="sxs-lookup"><span data-stu-id="fd95e-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="fd95e-222">如果此命令成功，您會看到如下的輸出︰</span><span class="sxs-lookup"><span data-stu-id="fd95e-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="fd95e-223">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="fd95e-223">Verify that hello VM was created</span></span>
<span data-ttu-id="fd95e-224">您應該會看到 hello 新建立的 VM 在 hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用下列 PowerShell hello命令：</span><span class="sxs-lookup"><span data-stu-id="fd95e-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="fd95e-225">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd95e-225">Next steps</span></span>
<span data-ttu-id="fd95e-226">在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="fd95e-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="fd95e-227">Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="fd95e-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="fd95e-228">如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md)。</span><span class="sxs-lookup"><span data-stu-id="fd95e-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

