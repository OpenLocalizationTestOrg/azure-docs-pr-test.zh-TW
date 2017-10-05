---
title: "從通用內部部署 VHD 建立受管理的 Azure VM | Microsoft Docs"
description: "在 Resource Manager 部署模型中，將一般化 VHD 上傳至 Azure 並使用它來建立新 VM。"
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
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="14c1b-103">將一般化 VHD 上傳，並使用它在 Azure 中建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="14c1b-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="14c1b-104">本主題會逐步引導您使用 PowerShell 將一般化 VM 的 VHD 上傳至 Azure，從 VHD 建立映像和從該映像建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="14c1b-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="14c1b-105">您可以上傳從內部部署虛擬化工具或另一個雲端匯出的 VHD。</span><span class="sxs-lookup"><span data-stu-id="14c1b-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="14c1b-106">針對新的 VM 使用[受控磁碟](managed-disks-overview.md)可簡化 VM 管理，當 VM 中包含可用性設定組時，還可提供更高的可用性。</span><span class="sxs-lookup"><span data-stu-id="14c1b-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="14c1b-107">如果您想要使用範例指令碼，請參閱[用來將 VHD 上傳至 Azure 並建立新 VM 的範例指令碼](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="14c1b-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="14c1b-108">開始之前</span><span class="sxs-lookup"><span data-stu-id="14c1b-108">Before you begin</span></span>

- <span data-ttu-id="14c1b-109">將任何 VHD 上傳至 Azure 之前，您應該遵循[準備 Windows VHD 或 VHDX 以上傳至 Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="14c1b-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="14c1b-110">請先檢閱[規劃移轉至受控磁碟](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)，再開始移轉至[受控磁碟](managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="14c1b-111">請確定您擁有最新版的 AzureRM.Compute PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="14c1b-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="14c1b-112">執行下列命令來安裝它。</span><span class="sxs-lookup"><span data-stu-id="14c1b-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="14c1b-113">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="14c1b-114">使用 Sysprep 將 Windows VM 一般化</span><span class="sxs-lookup"><span data-stu-id="14c1b-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="14c1b-115">Sysprep 會移除您的所有個人帳戶資訊以及其他項目，並準備電腦以做為映像。</span><span class="sxs-lookup"><span data-stu-id="14c1b-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="14c1b-116">如需 Sysprep 的詳細資訊，請參閱 [如何使用 Sysprep：簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="14c1b-117">請確定 Sysprep 支援電腦上執行的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="14c1b-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="14c1b-118">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="14c1b-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14c1b-119">如果您是第一次在將 VHD 上傳至 Azure 之前執行 Sysprep，請確定您已[準備好 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 再執行 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="14c1b-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="14c1b-120">登入 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="14c1b-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="14c1b-121">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="14c1b-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="14c1b-122">切換至 **%windir%\system32\sysprep** 目錄，然後執行 `sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="14c1b-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="14c1b-123">在 [系統準備工具] 對話方塊中，選取 [進入系統全新體驗 (OOBE)]，並確認已勾選 [一般化] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="14c1b-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="14c1b-124">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="14c1b-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="14c1b-125">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="14c1b-125">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="14c1b-127">Sysprep 完成時，會關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="14c1b-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="14c1b-128">不要重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="14c1b-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="14c1b-129">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="14c1b-129">Log in to Azure</span></span>
<span data-ttu-id="14c1b-130">如果尚未安裝 Azure PowerShell 1.4 版或更高版本，請參閱 [How to install and configure Azure PowerShell (如何安裝和設定 Azure PowerShell)](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="14c1b-131">開啟 Azure PowerShell，並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="14c1b-132">這會開啟一個可供您輸入 Azure 帳戶認證的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="14c1b-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="14c1b-133">取得您可用訂用帳戶的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="14c1b-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="14c1b-134">使用訂用帳戶識別碼來設定正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="14c1b-135">使用正確訂用帳戶的識別碼取代 *<subscriptionID>*。</span><span class="sxs-lookup"><span data-stu-id="14c1b-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="14c1b-136">取得儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="14c1b-136">Get the storage account</span></span>
<span data-ttu-id="14c1b-137">您需要一個 Azure 中的儲存體帳戶來裝載上傳的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="14c1b-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="14c1b-138">您可以使用現有的儲存體帳戶或建立新帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="14c1b-139">如果您要使用 VHD 為 VM 建立受控磁碟，儲存體帳戶位置與您將建立 VM 的位置必須相同。</span><span class="sxs-lookup"><span data-stu-id="14c1b-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="14c1b-140">若要顯示可用的儲存體帳戶，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="14c1b-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="14c1b-141">如果您想要使用現有的儲存體帳戶，請移至[上傳 VM 映像](#upload-the-vm-vhd-to-your-storage-account)一節。</span><span class="sxs-lookup"><span data-stu-id="14c1b-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="14c1b-142">如果您需要建立儲存體帳戶，請依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="14c1b-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="14c1b-143">您需要在當中建立儲存體帳戶的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="14c1b-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="14c1b-144">若要找出您訂用帳戶中的所有資源群組，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="14c1b-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="14c1b-145">若要在**美國東部**區域建立名為 **myResourceGroup** 的資源群組，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="14c1b-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="14c1b-146">使用 [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) Cmdlet，在此資源群組中建立名為 **mystorageaccount**的儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="14c1b-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="14c1b-147">-SkuName 的有效值包括：</span><span class="sxs-lookup"><span data-stu-id="14c1b-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="14c1b-148">**Standard_LRS** - 本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="14c1b-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="14c1b-149">**Standard_ZRS** - 區域備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="14c1b-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="14c1b-150">**Standard_GRS** - 異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="14c1b-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="14c1b-151">**Standard_RAGRS** - 讀取權限異地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="14c1b-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="14c1b-152">**Premium_LRS** - 進階本地備援儲存體。</span><span class="sxs-lookup"><span data-stu-id="14c1b-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="14c1b-153">將 VHD 上傳至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="14c1b-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="14c1b-154">使用 [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) Cmdlet，將 VHD 上傳至儲存體帳戶中的容器。</span><span class="sxs-lookup"><span data-stu-id="14c1b-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="14c1b-155">這個範例會將 myVHD.vhd 檔案從 "C:\Users\Public\Documents\Virtual hard disks\" 上傳至 myResourceGroup 資源群組中名為 mystorageaccount 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="14c1b-156">檔案會放入名為 *mycontainer* 的容器，新的檔案名稱會是 *myUploadedVHD.vhd*。</span><span class="sxs-lookup"><span data-stu-id="14c1b-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="14c1b-157">如果成功，您會得到看起來如以下的回應：</span><span class="sxs-lookup"><span data-stu-id="14c1b-157">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="14c1b-158">視您的網路連線和 VHD 檔案大小而定，此命令可能需要一些時間才能完成</span><span class="sxs-lookup"><span data-stu-id="14c1b-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="14c1b-159">儲存 [目的地 URI] 路徑，以便日後想要使用上傳的 VHD 建立受控磁碟或新的 VM 時使用。</span><span class="sxs-lookup"><span data-stu-id="14c1b-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="14c1b-160">上傳 VHD 的其他選項</span><span class="sxs-lookup"><span data-stu-id="14c1b-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="14c1b-161">您也可以使用下列其中一種方法將 VHD 上傳至儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="14c1b-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="14c1b-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="14c1b-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="14c1b-163">Azure 儲存體複製 Blob API</span><span class="sxs-lookup"><span data-stu-id="14c1b-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="14c1b-164">Azure 儲存體總管上傳 Blob</span><span class="sxs-lookup"><span data-stu-id="14c1b-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="14c1b-165">儲存體匯入/匯出服務 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="14c1b-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="14c1b-166">如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。</span><span class="sxs-lookup"><span data-stu-id="14c1b-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="14c1b-167">您可以使用 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 從資料大小和傳輸單位來評估時間。</span><span class="sxs-lookup"><span data-stu-id="14c1b-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="14c1b-168">匯入/匯出可用來複製到標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="14c1b-169">您必須使用 AzCopy 之類的工具，從 Standard 儲存體帳戶複製到進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="14c1b-170">從上傳的 VHD 建立受控映像</span><span class="sxs-lookup"><span data-stu-id="14c1b-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="14c1b-171">使用一般化 OS VHD 建立受控映像。</span><span class="sxs-lookup"><span data-stu-id="14c1b-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="14c1b-172">使用您自己的資訊取代這些值。</span><span class="sxs-lookup"><span data-stu-id="14c1b-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="14c1b-173">首先，設定一般參數：</span><span class="sxs-lookup"><span data-stu-id="14c1b-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="14c1b-174">使用一般化 OS VHD 建立映像。</span><span class="sxs-lookup"><span data-stu-id="14c1b-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="14c1b-175">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="14c1b-175">Create a virtual network</span></span>
<span data-ttu-id="14c1b-176">建立[虛擬網路](../../virtual-network/virtual-networks-overview.md)的 vNet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="14c1b-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="14c1b-177">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="14c1b-177">Create the subnet.</span></span> <span data-ttu-id="14c1b-178">這個範例會建立名為 *mySubnet* 且具有位址首碼 *10.0.0.0/24* 的子網路。</span><span class="sxs-lookup"><span data-stu-id="14c1b-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="14c1b-179">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="14c1b-179">Create the virtual network.</span></span> <span data-ttu-id="14c1b-180">這個範例會建立名為 *myVnet* 且具有位址首碼 *10.0.0.0/16* 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="14c1b-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="14c1b-181">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="14c1b-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="14c1b-182">若要能夠與虛擬網路中的虛擬機器進行通訊，您需要 [公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 和網路介面。</span><span class="sxs-lookup"><span data-stu-id="14c1b-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="14c1b-183">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="14c1b-183">Create a public IP address.</span></span> <span data-ttu-id="14c1b-184">此範例會建立名為 *myPip* 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="14c1b-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="14c1b-185">建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="14c1b-185">Create the NIC.</span></span> <span data-ttu-id="14c1b-186">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="14c1b-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="14c1b-187">建立網路安全性群組和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="14c1b-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="14c1b-188">若要能夠使用 RDP 登入 VM，您必須有可在連接埠 3389 上允許 RDP 存取的網路安全性規則 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="14c1b-189">此範例會建立名為 *myNsg* 的 NSG，其包含的規則 *myRdpRule* 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="14c1b-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="14c1b-190">如需 NSG 的詳細資訊，請參閱[使用 PowerShell 對 Azure 中的 VM 開啟連接埠](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="14c1b-191">建立虛擬網路的變數</span><span class="sxs-lookup"><span data-stu-id="14c1b-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="14c1b-192">為已完成的虛擬網路建立變數。</span><span class="sxs-lookup"><span data-stu-id="14c1b-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="14c1b-193">取得 VM 的認證</span><span class="sxs-lookup"><span data-stu-id="14c1b-193">Get the credentials for the VM</span></span>

<span data-ttu-id="14c1b-194">下列 Cmdlet 會開啟視窗，讓您輸入新的使用者名稱和密碼，作為從遠端存取 VM 時使用的本機管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="14c1b-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="14c1b-195">將 VM 名稱和大小新增至 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="14c1b-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="14c1b-196">將 VM 映像設定為新 VM 的來源映像</span><span class="sxs-lookup"><span data-stu-id="14c1b-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="14c1b-197">使用受控 VM 映像的識別碼設定來源影像。</span><span class="sxs-lookup"><span data-stu-id="14c1b-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="14c1b-198">設定 OS 組態並新增 NIC。</span><span class="sxs-lookup"><span data-stu-id="14c1b-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="14c1b-199">輸入儲存體類型 (PremiumLRS 或 StandardLRS) 和 OS 磁碟的大小。</span><span class="sxs-lookup"><span data-stu-id="14c1b-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="14c1b-200">這個範例將帳戶類型設定為 *PremiumLRS*、將磁碟大小設定為 *128GB*，並將磁碟快取設定為 *ReadWrite*。</span><span class="sxs-lookup"><span data-stu-id="14c1b-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="14c1b-201">建立 VM</span><span class="sxs-lookup"><span data-stu-id="14c1b-201">Create the VM</span></span>

<span data-ttu-id="14c1b-202">使用 **$vm** 變數中儲存的組態來建立新 VM。</span><span class="sxs-lookup"><span data-stu-id="14c1b-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="14c1b-203">確認已建立 VM</span><span class="sxs-lookup"><span data-stu-id="14c1b-203">Verify that the VM was created</span></span>
<span data-ttu-id="14c1b-204">完成時，在 [Azure 入口網站](https://portal.azure.com)的 [瀏覽] > [虛擬機器] 底下，或是使用下列 PowerShell 命令，應該就可以看到新建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="14c1b-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="14c1b-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14c1b-205">Next steps</span></span>

<span data-ttu-id="14c1b-206">若要登入新的虛擬機器，請瀏覽至[入口網站](https://portal.azure.com)中的 VM，按一下 [連接] 並開啟遠端桌面 RDP 檔案。</span><span class="sxs-lookup"><span data-stu-id="14c1b-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="14c1b-207">使用原始虛擬機器的帳戶認證來登入新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="14c1b-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="14c1b-208">如需詳細資訊，請參閱 [如何連接和登入執行 Windows 的 Azure 虛擬機器](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="14c1b-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

