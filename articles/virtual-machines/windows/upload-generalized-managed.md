---
title: "受管理的 Azure VM 從內部一般化的 VHD aaaCreate |Microsoft 文件"
description: "上傳一般化的 VHD tooAzure，並用它 toocreate hello Resource Manager 部署模型中的新 Vm。"
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="77653-103">一般化的 VHD 上傳，並用它 toocreate Azure 中的新 Vm</span><span class="sxs-lookup"><span data-stu-id="77653-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="77653-104">本主題會引導您逐步使用 PowerShell tooupload 一般化 VM tooAzure 的 VHD 從 hello VHD 建立映像，從該映像建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="77653-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="77653-105">您可以上傳從內部部署虛擬化工具或另一個雲端匯出的 VHD。</span><span class="sxs-lookup"><span data-stu-id="77653-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="77653-106">使用[管理磁碟](managed-disks-overview.md)hello 新的 VM 可簡化 hello VM 管理和 hello VM 放置於可用性集合時提供更佳的可用性。</span><span class="sxs-lookup"><span data-stu-id="77653-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="77653-107">如果您想 toouse 範例指令碼，請參閱[範例指令碼 tooupload VHD tooAzure 並建立新的 VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="77653-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77653-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="77653-108">Before you begin</span></span>

- <span data-ttu-id="77653-109">上傳任何 VHD tooAzure 之前, 您應該遵循[準備 Windows VHD 或 VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="77653-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="77653-110">檢閱[hello 移轉計劃 tooManaged 磁碟](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)太開始移轉之前[管理磁碟](managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="77653-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="77653-111">請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="77653-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="77653-112">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="77653-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="77653-113">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="77653-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="77653-114">一般化 hello Windows VM 使用 Sysprep</span><span class="sxs-lookup"><span data-stu-id="77653-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="77653-115">Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。</span><span class="sxs-lookup"><span data-stu-id="77653-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="77653-116">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77653-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="77653-117">請確定 hello hello 機器上執行的伺服器角色支援 sysprep。</span><span class="sxs-lookup"><span data-stu-id="77653-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="77653-118">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="77653-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77653-119">如果您第一次上傳您的 VHD tooAzure hello 之前執行 Sysprep，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。</span><span class="sxs-lookup"><span data-stu-id="77653-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="77653-120">登入 toohello Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77653-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="77653-121">系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="77653-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="77653-122">變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="77653-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="77653-123">在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="77653-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="77653-124">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="77653-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="77653-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77653-125">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="77653-127">Sysprep 完成時，它會關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77653-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="77653-128">無法重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="77653-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="77653-129">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="77653-129">Log in tooAzure</span></span>
<span data-ttu-id="77653-130">如果您還沒有 PowerShell 1.4 版或更新版本安裝，讀取[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="77653-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="77653-131">開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="77653-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="77653-132">快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="77653-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="77653-133">取得可用的訂閱 hello 訂用帳戶 Id。</span><span class="sxs-lookup"><span data-stu-id="77653-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="77653-134">設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77653-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="77653-135">取代 *<subscriptionID>*  hello 識別碼 hello 包含正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77653-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="77653-136">取得 hello 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="77653-136">Get hello storage account</span></span>
<span data-ttu-id="77653-137">您需要 Azure toostore hello 上傳 VM 映像的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="77653-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="77653-138">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="77653-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="77653-139">如果您將使用 hello VHD toocreate 受管理磁碟 vm，hello 儲存體帳戶位置必須是相同的 hello 位置，其中您要建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="77653-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="77653-140">tooshow hello 可用儲存體帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="77653-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="77653-141">如果您想 toouse 現有的儲存體帳戶，請繼續 toohello [hello VM 映像上載](#upload-the-vm-vhd-to-your-storage-account)> 一節。</span><span class="sxs-lookup"><span data-stu-id="77653-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="77653-142">如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="77653-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="77653-143">您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="77653-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="77653-144">toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="77653-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="77653-145">資源群組命名為的 toocreate **myResourceGroup**在 hello**美國東部**區域中，輸入：</span><span class="sxs-lookup"><span data-stu-id="77653-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="77653-146">建立名為儲存體帳戶**mystorageaccount**使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="77653-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="77653-147">-SkuName 的有效值包括：</span><span class="sxs-lookup"><span data-stu-id="77653-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="77653-148">**Standard_LRS** - 本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="77653-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="77653-149">**Standard_ZRS** - 區域備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="77653-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="77653-150">**Standard_GRS** - 異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="77653-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="77653-151">**Standard_RAGRS** - 讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="77653-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="77653-152">**Premium_LRS** - 進階本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="77653-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="77653-153">上傳 hello VHD tooyour 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="77653-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="77653-154">使用 hello[新增 AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa 容器儲存體帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="77653-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="77653-155">此範例中上傳 hello 檔案*myVHD.vhd*從*"C:\Users\Public\Documents\Virtual 硬碟\"* tooa 儲存體帳戶*mystorageaccount*在 hello *myResourceGroup*資源群組。</span><span class="sxs-lookup"><span data-stu-id="77653-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="77653-156">hello 檔案會放入名為 「 hello 容器*mycontainer* hello 新的檔案名稱將會*myUploadedVHD.vhd*。</span><span class="sxs-lookup"><span data-stu-id="77653-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="77653-157">如果成功的話，您會收到的回應，看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="77653-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="77653-158">根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete</span><span class="sxs-lookup"><span data-stu-id="77653-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="77653-159">儲存 hello**目的地 URI**路徑 toouse 稍後如果您正在 toocreate 受管理的磁碟，或使用 hello 的新 VM 上傳 VHD。</span><span class="sxs-lookup"><span data-stu-id="77653-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="77653-160">上傳 VHD 的其他選項</span><span class="sxs-lookup"><span data-stu-id="77653-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="77653-161">您也可以上傳 VHD tooyour 儲存體帳戶使用 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="77653-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="77653-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="77653-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="77653-163">Azure 儲存體複製 Blob API</span><span class="sxs-lookup"><span data-stu-id="77653-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="77653-164">Azure 儲存體總管上傳 Blob</span><span class="sxs-lookup"><span data-stu-id="77653-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="77653-165">儲存體匯入/匯出服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="77653-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="77653-166">如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="77653-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="77653-167">您可以使用[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello 時間資料的大小和傳輸的單位。</span><span class="sxs-lookup"><span data-stu-id="77653-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="77653-168">可以匯入/匯出用 toocopy tooa 標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="77653-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="77653-169">您必須從標準儲存體 toopremium 儲存體帳戶，使用 AzCopy 這類工具 toocopy。</span><span class="sxs-lookup"><span data-stu-id="77653-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="77653-170">建立受管理 hello 從映像上傳 VHD</span><span class="sxs-lookup"><span data-stu-id="77653-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="77653-171">使用一般化 OS VHD 建立受控映像。</span><span class="sxs-lookup"><span data-stu-id="77653-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="77653-172">Hello 值取代為您自己的資訊。</span><span class="sxs-lookup"><span data-stu-id="77653-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="77653-173">首先，設定 hello 一般參數：</span><span class="sxs-lookup"><span data-stu-id="77653-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="77653-174">建立 hello 使用一般化的 OS VHD 的映像。</span><span class="sxs-lookup"><span data-stu-id="77653-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="77653-175">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="77653-175">Create a virtual network</span></span>
<span data-ttu-id="77653-176">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="77653-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="77653-177">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="77653-177">Create hello subnet.</span></span> <span data-ttu-id="77653-178">這個範例會建立名為的子網路*mySubnet* hello 位址前置詞與*10.0.0.0/24*。</span><span class="sxs-lookup"><span data-stu-id="77653-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="77653-179">建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="77653-179">Create hello virtual network.</span></span> <span data-ttu-id="77653-180">這個範例會建立虛擬網路，名為*myVnet* hello 位址前置詞與*10.0.0.0/16*。</span><span class="sxs-lookup"><span data-stu-id="77653-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="77653-181">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="77653-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="77653-182">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="77653-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="77653-183">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77653-183">Create a public IP address.</span></span> <span data-ttu-id="77653-184">此範例會建立名為 *myPip* 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="77653-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="77653-185">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="77653-185">Create hello NIC.</span></span> <span data-ttu-id="77653-186">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="77653-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="77653-187">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="77653-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="77653-188">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 網路安全性規則 (NSG)，允許連接埠 3389 RDP 存取權。</span><span class="sxs-lookup"><span data-stu-id="77653-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="77653-189">此範例會建立名為 *myNsg* 的 NSG，其包含的規則 *myRdpRule* 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="77653-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="77653-190">如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="77653-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="77653-191">針對 hello 虛擬網路建立的變數</span><span class="sxs-lookup"><span data-stu-id="77653-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="77653-192">建立 hello 完成虛擬網路的變數。</span><span class="sxs-lookup"><span data-stu-id="77653-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="77653-193">取得 hello VM hello 認證</span><span class="sxs-lookup"><span data-stu-id="77653-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="77653-194">hello 下列 cmdlet 會開啟的視窗，您就會在輸入新的使用者名稱和密碼 toouse hello 的本機 administrator 帳戶從遠端存取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="77653-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="77653-195">加入 hello VM 名稱和大小 toohello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="77653-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="77653-196">集 hello VM 映像 hello 的來源映像為新的 VM</span><span class="sxs-lookup"><span data-stu-id="77653-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="77653-197">設定使用受管理的 hello VM 映像的 hello 識別碼 hello 來源映像。</span><span class="sxs-lookup"><span data-stu-id="77653-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="77653-198">設定 hello 作業系統設定以及新增 hello nic。</span><span class="sxs-lookup"><span data-stu-id="77653-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="77653-199">輸入 hello 儲存類型 （PremiumLRS 或 StandardLRS） 和 hello hello 作業系統磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="77653-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="77653-200">此範例會設定 hello 帳戶類型太*PremiumLRS*，太 hello 磁碟大小*128 GB*和磁碟快取太*ReadWrite*。</span><span class="sxs-lookup"><span data-stu-id="77653-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="77653-201">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="77653-201">Create hello VM</span></span>

<span data-ttu-id="77653-202">建立新的 VM 使用 hello 組態儲存在 hello hello **$vm**變數。</span><span class="sxs-lookup"><span data-stu-id="77653-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="77653-203">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="77653-203">Verify that hello VM was created</span></span>
<span data-ttu-id="77653-204">完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="77653-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="77653-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77653-205">Next steps</span></span>

<span data-ttu-id="77653-206">在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="77653-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="77653-207">Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="77653-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="77653-208">如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="77653-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

