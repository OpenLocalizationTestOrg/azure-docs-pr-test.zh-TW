---
title: "在 Azure 中對 managed 影像 aaaCreate |Microsoft 文件"
description: "在 Azure 中建立一般化 VM 或 VHD 的受控映像。 映像可以是使用的 toocreate 使用受管理的磁碟的多個 Vm。"
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="a52e2-104">在 Azure 中建立一般化 VM 的受控映像</span><span class="sxs-lookup"><span data-stu-id="a52e2-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="a52e2-105">您可以從在儲存體帳戶中儲存為受控磁碟或非受控磁碟的一般化 VM，建立受控映像資源。</span><span class="sxs-lookup"><span data-stu-id="a52e2-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="a52e2-106">hello 映像可以，則是使用的 toocreate 多個 Vm。</span><span class="sxs-lookup"><span data-stu-id="a52e2-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="a52e2-107">一般化 hello Windows VM 使用 Sysprep</span><span class="sxs-lookup"><span data-stu-id="a52e2-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="a52e2-108">Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。</span><span class="sxs-lookup"><span data-stu-id="a52e2-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a52e2-109">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a52e2-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a52e2-110">請確定 hello hello 機器上執行的伺服器角色支援 sysprep。</span><span class="sxs-lookup"><span data-stu-id="a52e2-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="a52e2-111">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="a52e2-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a52e2-112">如果您第一次上傳您的 VHD tooAzure hello 之前執行 Sysprep，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。</span><span class="sxs-lookup"><span data-stu-id="a52e2-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="a52e2-113">登入 toohello Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a52e2-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="a52e2-114">系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="a52e2-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a52e2-115">變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="a52e2-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a52e2-116">在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a52e2-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a52e2-117">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="a52e2-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a52e2-118">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a52e2-118">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a52e2-120">Sysprep 完成時，它會關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a52e2-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="a52e2-121">無法重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a52e2-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="a52e2-122">Hello 入口網站中建立的受管理的映像</span><span class="sxs-lookup"><span data-stu-id="a52e2-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="a52e2-123">開啟 hello[入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a52e2-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a52e2-124">按一下 hello 加號 toocreate 新的資源。</span><span class="sxs-lookup"><span data-stu-id="a52e2-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="a52e2-125">在 hello 篩選搜尋中，輸入**映像**。</span><span class="sxs-lookup"><span data-stu-id="a52e2-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="a52e2-126">選取**映像**hello 結果中。</span><span class="sxs-lookup"><span data-stu-id="a52e2-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="a52e2-127">在 hello**映像**刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="a52e2-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="a52e2-128">在**名稱**，輸入 hello 映像的名稱。</span><span class="sxs-lookup"><span data-stu-id="a52e2-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="a52e2-129">如果您有多個訂閱，選取 hello 之一從 hello**訂用帳戶**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="a52e2-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="a52e2-130">在**資源群組**選取**建立新**和輸入的名稱，或選取**從現有**從 hello 下拉式清單中選取資源群組 toouse。</span><span class="sxs-lookup"><span data-stu-id="a52e2-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="a52e2-131">在**位置**，選擇您的資源群組的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="a52e2-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="a52e2-132">在**OS 類型**選取的作業系統，Windows 或 Linux 的 hello 類型。</span><span class="sxs-lookup"><span data-stu-id="a52e2-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="a52e2-133">在**儲存體 blob**，按一下 **瀏覽**toolook 您 Azure 儲存體中的 hello VHD。</span><span class="sxs-lookup"><span data-stu-id="a52e2-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="a52e2-134">在 [帳戶類型] 中選擇 Standard_LRS 或 Premium_LRS。</span><span class="sxs-lookup"><span data-stu-id="a52e2-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="a52e2-135">標準使用硬碟機，而進階使用固態磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a52e2-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="a52e2-136">兩者都使用本機備援的儲存體。</span><span class="sxs-lookup"><span data-stu-id="a52e2-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="a52e2-137">在**磁碟快取**選取 hello 適當的磁碟快取選項。</span><span class="sxs-lookup"><span data-stu-id="a52e2-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="a52e2-138">hello 選項**無**，**唯讀**和**可讀取 \ 寫入**。</span><span class="sxs-lookup"><span data-stu-id="a52e2-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="a52e2-139">選用： 您也可以加入現有的資料磁碟 toohello 映像即可**+ 新增資料磁碟**。</span><span class="sxs-lookup"><span data-stu-id="a52e2-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="a52e2-140">完成選取之後，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a52e2-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="a52e2-141">建立 hello 映像之後，您會看到它做為**映像**hello hello 資源群組中選擇清單中的資源。</span><span class="sxs-lookup"><span data-stu-id="a52e2-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="a52e2-142">使用 Powershell 建立 VM 的受控映像</span><span class="sxs-lookup"><span data-stu-id="a52e2-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="a52e2-143">建立映像，直接從 hello VM 可確保該 hello 映像包括所有的 hello 與 hello VM，包括 hello OS 磁碟和任何資料磁碟相關聯的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a52e2-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="a52e2-144">在開始之前，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="a52e2-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a52e2-145">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="a52e2-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="a52e2-146">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a52e2-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="a52e2-147">建立一些變數。</span><span class="sxs-lookup"><span data-stu-id="a52e2-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="a52e2-148">請確定已解除配置 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="a52e2-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="a52e2-149">設定得 hello hello 虛擬機器狀態**一般**。</span><span class="sxs-lookup"><span data-stu-id="a52e2-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="a52e2-150">取得 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a52e2-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="a52e2-151">建立 hello 映像設定。</span><span class="sxs-lookup"><span data-stu-id="a52e2-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="a52e2-152">建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="a52e2-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="a52e2-153">在 PowerShell 中建立 VHD 的受控映像</span><span class="sxs-lookup"><span data-stu-id="a52e2-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="a52e2-154">使用一般化 OS VHD 建立受控映像。</span><span class="sxs-lookup"><span data-stu-id="a52e2-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="a52e2-155">首先，設定 hello 一般參數：</span><span class="sxs-lookup"><span data-stu-id="a52e2-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="a52e2-156">Step\deallocate hello VM。</span><span class="sxs-lookup"><span data-stu-id="a52e2-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="a52e2-157">將標示為一般化 VM hello。</span><span class="sxs-lookup"><span data-stu-id="a52e2-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="a52e2-158">建立 hello 使用一般化的 OS VHD 的映像。</span><span class="sxs-lookup"><span data-stu-id="a52e2-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="a52e2-159">使用 Powershell 從快照集建立受控映像</span><span class="sxs-lookup"><span data-stu-id="a52e2-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="a52e2-160">您也可以從 hello VHD 從一般化 VM 的快照集建立的受管理的映像。</span><span class="sxs-lookup"><span data-stu-id="a52e2-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="a52e2-161">建立一些變數。</span><span class="sxs-lookup"><span data-stu-id="a52e2-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="a52e2-162">收到 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="a52e2-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="a52e2-163">建立 hello 映像設定。</span><span class="sxs-lookup"><span data-stu-id="a52e2-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="a52e2-164">建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="a52e2-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="a52e2-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a52e2-165">Next steps</span></span>
- <span data-ttu-id="a52e2-166">現在您可以[從 hello 一般化受管理的映像建立 VM](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a52e2-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

