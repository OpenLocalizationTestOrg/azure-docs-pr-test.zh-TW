---
title: "aaaUpload 一般化 VHD toocreate 在 Azure 中的多個 Vm |Microsoft 文件"
description: "上傳一般化的 VHD tooan Azure 儲存體帳戶 toocreate Windows VM toouse 與 hello 資源管理員部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="42f7e-103">上傳一般化的 VHD tooAzure toocreate 新的 VM</span><span class="sxs-lookup"><span data-stu-id="42f7e-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="42f7e-104">本主題涵蓋上載一般化 unmanaged 的磁碟 tooa 儲存體帳戶，然後再建立新的 VM 使用上傳的 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="42f7e-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="42f7e-105">一般化 VHD 映像已使用 Sysprep 移除您所有的個人帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="42f7e-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="42f7e-106">如果您想 toocreate 將 VM 從儲存體帳戶中的特定 VHD，請參閱[從特定的 VHD 建立 VM](sa-create-vm-specialized.md)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="42f7e-107">本主題將說明如何使用儲存體帳戶，但我們建議客戶改用移動 toousing 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="42f7e-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="42f7e-108">如需 tooprepare 上, 傳內容，以及建立新的 VM 使用的完整逐步解說會管理磁碟，請參閱 <<c0> [ 建立新的 VM 從一般化的 VHD 上傳 tooAzure 使用受管理磁碟](upload-generalized-managed.md)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="42f7e-109">準備 VM hello</span><span class="sxs-lookup"><span data-stu-id="42f7e-109">Prepare hello VM</span></span>

<span data-ttu-id="42f7e-110">一般化 VHD - 已使用 Sysprep 移除您所有的個人帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="42f7e-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="42f7e-111">如果您想 toouse hello 做為映像 toocreate VHD 中的新 Vm，您應該：</span><span class="sxs-lookup"><span data-stu-id="42f7e-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="42f7e-112">[準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="42f7e-113">一般化 hello 使用 Sysprep 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="42f7e-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="42f7e-114">使用 Sysprep 將 Windows 虛擬機器一般化</span><span class="sxs-lookup"><span data-stu-id="42f7e-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="42f7e-115">這個區段會顯示如何 toogeneralize 用作映像的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="42f7e-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="42f7e-116">Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。</span><span class="sxs-lookup"><span data-stu-id="42f7e-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="42f7e-117">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="42f7e-118">請確定 hello hello 機器上執行的伺服器角色支援 sysprep。</span><span class="sxs-lookup"><span data-stu-id="42f7e-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="42f7e-119">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="42f7e-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42f7e-120">如果您第一次上傳您的 VHD tooAzure hello 之前執行 Sysprep，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。</span><span class="sxs-lookup"><span data-stu-id="42f7e-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="42f7e-121">登入 toohello Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="42f7e-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="42f7e-122">系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="42f7e-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="42f7e-123">變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="42f7e-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="42f7e-124">在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="42f7e-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="42f7e-125">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="42f7e-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="42f7e-126">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="42f7e-126">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="42f7e-128">Sysprep 完成時，它會關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="42f7e-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="42f7e-129">不要重新啟動 hello VM，直到您完成上傳的 hello VHD tooAzure 或從 hello VM 建立映像。</span><span class="sxs-lookup"><span data-stu-id="42f7e-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="42f7e-130">如果 hello VM 不小心取得重新啟動，執行 Sysprep toogeneralize 再試一次。</span><span class="sxs-lookup"><span data-stu-id="42f7e-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="42f7e-131">上傳 VHD hello</span><span class="sxs-lookup"><span data-stu-id="42f7e-131">Upload hello VHD</span></span>

<span data-ttu-id="42f7e-132">上傳 hello VHD tooan Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42f7e-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="42f7e-133">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="42f7e-133">Log in tooAzure</span></span>
<span data-ttu-id="42f7e-134">如果您還沒有 PowerShell 1.4 版或更新版本安裝，讀取[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="42f7e-135">開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="42f7e-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="42f7e-136">快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="42f7e-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="42f7e-137">取得可用的訂閱 hello 訂用帳戶 Id。</span><span class="sxs-lookup"><span data-stu-id="42f7e-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="42f7e-138">設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="42f7e-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="42f7e-139">取代`<subscriptionID>`hello 識別碼 hello 包含正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="42f7e-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="42f7e-140">取得 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="42f7e-140">Get hello storage account</span></span>
<span data-ttu-id="42f7e-141">您需要 Azure toostore hello 上傳 VM 映像的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="42f7e-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="42f7e-142">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="42f7e-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="42f7e-143">tooshow hello 可用儲存體帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="42f7e-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="42f7e-144">如果您想 toouse 現有的儲存體帳戶，請繼續 toohello [hello VM 映像上載](#upload-the-vm-vhd-to-your-storage-account)> 一節。</span><span class="sxs-lookup"><span data-stu-id="42f7e-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="42f7e-145">如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="42f7e-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="42f7e-146">您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="42f7e-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="42f7e-147">toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="42f7e-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="42f7e-148">資源群組命名為的 toocreate **myResourceGroup**在 hello**美國西部**區域中，輸入：</span><span class="sxs-lookup"><span data-stu-id="42f7e-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="42f7e-149">建立名為儲存體帳戶**mystorageaccount**使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="42f7e-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="42f7e-150">開始 hello 上傳</span><span class="sxs-lookup"><span data-stu-id="42f7e-150">Start hello upload</span></span> 

<span data-ttu-id="42f7e-151">使用 hello[新增 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello 影像 tooa 容器儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="42f7e-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="42f7e-152">此範例中上傳 hello 檔案**myVHD.vhd**從`"C:\Users\Public\Documents\Virtual hard disks\"`tooa 儲存體帳戶**mystorageaccount**在 hello **myResourceGroup**資源群組。</span><span class="sxs-lookup"><span data-stu-id="42f7e-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="42f7e-153">hello 檔案會放入名為 「 hello 容器**mycontainer** hello 新的檔案名稱將會**myUploadedVHD.vhd**。</span><span class="sxs-lookup"><span data-stu-id="42f7e-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="42f7e-154">如果成功的話，您會收到的回應，看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="42f7e-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="42f7e-155">根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="42f7e-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="42f7e-156">建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="42f7e-156">Create a new VM</span></span> 

<span data-ttu-id="42f7e-157">您可以現在使用 hello 上傳 VHD toocreate 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="42f7e-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="42f7e-158">設定 hello hello VHD URI</span><span class="sxs-lookup"><span data-stu-id="42f7e-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="42f7e-159">如 hello VHD toouse hello URI 的格式 hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd。</span><span class="sxs-lookup"><span data-stu-id="42f7e-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="42f7e-160">在此範例中的 hello VHD 名為**myVHD** hello 儲存體帳戶中是**mystorageaccount** hello 容器中**mycontainer**。</span><span class="sxs-lookup"><span data-stu-id="42f7e-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="42f7e-161">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="42f7e-161">Create a virtual network</span></span>
<span data-ttu-id="42f7e-162">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="42f7e-163">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="42f7e-163">Create hello subnet.</span></span> <span data-ttu-id="42f7e-164">hello 下列範例會建立名為的子網路**mySubnet** hello 資源群組中**myResourceGroup** hello 位址前置詞與**10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="42f7e-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="42f7e-165">建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="42f7e-165">Create hello virtual network.</span></span> <span data-ttu-id="42f7e-166">hello 下列範例會建立虛擬網路，名為**myVnet**在 hello**美國西部**hello 位址前置詞的位置**10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="42f7e-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="42f7e-167">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="42f7e-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="42f7e-168">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="42f7e-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="42f7e-169">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="42f7e-169">Create a public IP address.</span></span> <span data-ttu-id="42f7e-170">此範例會建立名為 **myPip** 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="42f7e-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="42f7e-171">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="42f7e-171">Create hello NIC.</span></span> <span data-ttu-id="42f7e-172">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="42f7e-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="42f7e-173">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="42f7e-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="42f7e-174">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 允許連接埠 3389 RDP 存取權的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="42f7e-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="42f7e-175">此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="42f7e-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="42f7e-176">如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="42f7e-177">針對 hello 虛擬網路建立的變數</span><span class="sxs-lookup"><span data-stu-id="42f7e-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="42f7e-178">建立 hello 完成虛擬網路的變數。</span><span class="sxs-lookup"><span data-stu-id="42f7e-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="42f7e-179">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="42f7e-179">Create hello VM</span></span>
<span data-ttu-id="42f7e-180">hello 下列 PowerShell 指令碼會示範如何 hello 虛擬機器設定和使用 hello tooset 上傳 VM 映像為 hello hello 新安裝的來源。</span><span class="sxs-lookup"><span data-stu-id="42f7e-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="42f7e-181">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="42f7e-181">Verify that hello VM was created</span></span>
<span data-ttu-id="42f7e-182">完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="42f7e-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="42f7e-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42f7e-183">Next steps</span></span>
<span data-ttu-id="42f7e-184">toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[使用 Azure 資源管理員和 PowerShell 管理虛擬機器](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="42f7e-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


