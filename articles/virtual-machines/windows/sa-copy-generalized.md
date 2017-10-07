---
title: "未受管理的 Azure 中的一般化 VM 映像 aaaCreate |Microsoft 文件"
description: "在 Azure 中建立通用的 Windows VM toouse toocreate unmanaged 映的像 VM 的多個複本。"
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="f06c1-103">Toocreate 未受管理的 VM 從 Azure VM 的映像</span><span class="sxs-lookup"><span data-stu-id="f06c1-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="f06c1-104">本文章涵蓋使用儲存體帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="f06c1-104">This article covers using storage accounts.</span></span> <span data-ttu-id="f06c1-105">建議您使用受控磁碟和受管理的映像，不要使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f06c1-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="f06c1-106">如需詳細資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](capture-image-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="f06c1-107">本文章將示範如何 toouse Azure PowerShell toocreate 使用儲存體帳戶的一般化 Azure VM 的映像。</span><span class="sxs-lookup"><span data-stu-id="f06c1-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="f06c1-108">另一個 VM 時，可以使用 hello 映像 toocreate。</span><span class="sxs-lookup"><span data-stu-id="f06c1-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="f06c1-109">hello 映像包括 hello OS 磁碟和 hello 附加的 toohello 虛擬機器之資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f06c1-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="f06c1-110">hello 映像不含 hello 虛擬網路資源，因此當您建立時，需要這些資源 tooset hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="f06c1-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f06c1-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="f06c1-111">Prerequisites</span></span>
<span data-ttu-id="f06c1-112">您需要 toohave Azure PowerShell 版本 1.0.x 或較新的安裝。</span><span class="sxs-lookup"><span data-stu-id="f06c1-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="f06c1-113">如果您尚未安裝 PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="f06c1-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="f06c1-114">一般化 VM hello</span><span class="sxs-lookup"><span data-stu-id="f06c1-114">Generalize hello VM</span></span> 
<span data-ttu-id="f06c1-115">這個區段會顯示如何 toogeneralize 用作映像的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f06c1-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="f06c1-116">將 VM 一般化移除所有您個人的帳戶資訊，以及其他項目，並準備 hello 機器 toobe 做為映像。</span><span class="sxs-lookup"><span data-stu-id="f06c1-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="f06c1-117">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="f06c1-118">請確定 hello hello 機器上執行的伺服器角色支援 sysprep。</span><span class="sxs-lookup"><span data-stu-id="f06c1-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="f06c1-119">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="f06c1-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f06c1-120">如果您要上傳您的 VHD tooAzure hello 第一次，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。</span><span class="sxs-lookup"><span data-stu-id="f06c1-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="f06c1-121">您也可以普及使用 Linux VM `sudo waagent -deprovision+user` ，然後使用 PowerShell toocapture hello VM。</span><span class="sxs-lookup"><span data-stu-id="f06c1-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="f06c1-122">如需使用 hello CLI toocapture VM 的資訊，請參閱[toogeneralize 和 Linux 虛擬機器使用的擷取 hello Azure CLI ](../linux/capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="f06c1-123">登入 toohello Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f06c1-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="f06c1-124">系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="f06c1-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="f06c1-125">變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="f06c1-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="f06c1-126">在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="f06c1-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="f06c1-127">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="f06c1-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="f06c1-128">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f06c1-128">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="f06c1-130">Sysprep 完成時，它會關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f06c1-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f06c1-131">不要重新啟動 hello VM，直到您完成上傳的 hello VHD tooAzure 或從 hello VM 建立映像。</span><span class="sxs-lookup"><span data-stu-id="f06c1-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="f06c1-132">如果 hello VM 不小心取得重新啟動，執行 Sysprep toogeneralize 再試一次。</span><span class="sxs-lookup"><span data-stu-id="f06c1-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="f06c1-133">登入 tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06c1-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="f06c1-134">開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f06c1-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="f06c1-135">快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="f06c1-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="f06c1-136">取得可用的訂閱 hello 訂用帳戶 Id。</span><span class="sxs-lookup"><span data-stu-id="f06c1-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="f06c1-137">設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f06c1-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="f06c1-138">解除配置 hello VM 並設定 hello 狀態 toogeneralized</span><span class="sxs-lookup"><span data-stu-id="f06c1-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="f06c1-139">解除配置 hello VM 資源。</span><span class="sxs-lookup"><span data-stu-id="f06c1-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="f06c1-140">hello*狀態*hello VM 在 hello Azure 入口網站變更從**已停止**太**已停止 （取消配置）**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="f06c1-141">設定得 hello hello 虛擬機器狀態**一般**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="f06c1-142">檢查 hello hello VM 狀態。</span><span class="sxs-lookup"><span data-stu-id="f06c1-142">Check hello status of hello VM.</span></span> <span data-ttu-id="f06c1-143">hello **OSState/一般化**區段中針對 hello VM 應有 hello **DisplayStatus**設定得**一般化 VM**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="f06c1-144">建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="f06c1-144">Create hello image</span></span>

<span data-ttu-id="f06c1-145">使用這個命令的 hello 目的地儲存體容器中建立未受管理的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="f06c1-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="f06c1-146">hello 映像中建立 hello 相同 hello 原始虛擬機器的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f06c1-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="f06c1-147">hello`-Path`參數將儲存 hello 來源 VM tooyour 本機電腦的 hello JSON 範本的複本。</span><span class="sxs-lookup"><span data-stu-id="f06c1-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="f06c1-148">hello`-DestinationContainerName`參數就是您希望 toohold 影像 hello 容器 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="f06c1-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="f06c1-149">如果 hello 容器不存在，它會為您建立。</span><span class="sxs-lookup"><span data-stu-id="f06c1-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="f06c1-150">您可以取得映像的 hello URL 從 hello JSON 檔案的範本。</span><span class="sxs-lookup"><span data-stu-id="f06c1-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="f06c1-151">移 toohello**資源** > **storageProfile** > **osDisk** > **映像** > **uri**映像的區段 hello 完整路徑。</span><span class="sxs-lookup"><span data-stu-id="f06c1-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="f06c1-152">hello hello 影像 URL 看起來像： `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`。</span><span class="sxs-lookup"><span data-stu-id="f06c1-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="f06c1-153">您也可以驗證在 hello 入口網站中的 hello URI。</span><span class="sxs-lookup"><span data-stu-id="f06c1-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="f06c1-154">hello 映像會複製的 tooa 容器名稱**系統**儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="f06c1-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="f06c1-155">從 hello 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="f06c1-155">Create a VM from hello image</span></span>

<span data-ttu-id="f06c1-156">現在您可以建立一個或多個 Vm 從 hello unmanaged 映像。</span><span class="sxs-lookup"><span data-stu-id="f06c1-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="f06c1-157">設定 hello hello VHD URI</span><span class="sxs-lookup"><span data-stu-id="f06c1-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="f06c1-158">如 hello VHD toouse hello URI 的格式 hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd。</span><span class="sxs-lookup"><span data-stu-id="f06c1-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="f06c1-159">在此範例中的 hello VHD 名為**myVHD** hello 儲存體帳戶中是**mystorageaccount** hello 容器中**mycontainer**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="f06c1-160">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f06c1-160">Create a virtual network</span></span>
<span data-ttu-id="f06c1-161">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="f06c1-162">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="f06c1-162">Create hello subnet.</span></span> <span data-ttu-id="f06c1-163">hello 下列範例會建立名為的子網路**mySubnet** hello 資源群組中**myResourceGroup** hello 位址前置詞與**10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="f06c1-164">建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f06c1-164">Create hello virtual network.</span></span> <span data-ttu-id="f06c1-165">hello 下列範例會建立虛擬網路，名為**myVnet**在 hello**美國西部**hello 位址前置詞的位置**10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="f06c1-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="f06c1-166">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="f06c1-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="f06c1-167">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="f06c1-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="f06c1-168">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f06c1-168">Create a public IP address.</span></span> <span data-ttu-id="f06c1-169">此範例會建立名為 **myPip** 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f06c1-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="f06c1-170">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="f06c1-170">Create hello NIC.</span></span> <span data-ttu-id="f06c1-171">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="f06c1-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="f06c1-172">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="f06c1-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="f06c1-173">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 允許連接埠 3389 RDP 存取權的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="f06c1-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="f06c1-174">此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="f06c1-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="f06c1-175">如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="f06c1-176">針對 hello 虛擬網路建立的變數</span><span class="sxs-lookup"><span data-stu-id="f06c1-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="f06c1-177">建立 hello 完成虛擬網路的變數。</span><span class="sxs-lookup"><span data-stu-id="f06c1-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="f06c1-178">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="f06c1-178">Create hello VM</span></span>
<span data-ttu-id="f06c1-179">hello 下列 PowerShell 完成 hello 虛擬機器組態，並使用未受管理的映像為 hello 來源 hello 全新安裝。</span><span class="sxs-lookup"><span data-stu-id="f06c1-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

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

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="f06c1-180">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="f06c1-180">Verify that hello VM was created</span></span>
<span data-ttu-id="f06c1-181">完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="f06c1-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="f06c1-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f06c1-182">Next steps</span></span>
<span data-ttu-id="f06c1-183">toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[使用 Azure 資源管理員和 PowerShell 管理虛擬機器](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f06c1-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


