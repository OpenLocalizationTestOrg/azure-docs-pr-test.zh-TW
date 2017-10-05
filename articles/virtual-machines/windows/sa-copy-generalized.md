---
title: "在 Azure 中建立一般化 VM 未受管理的映像 | Microsoft Docs"
description: "建立一般化的 Windows VM 未受管理的映像，在 Azure 中用以建立多個 VM 複本。"
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
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="e557b-103">如何從 Azure VM 建立未受管理的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="e557b-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="e557b-104">本文章涵蓋使用儲存體帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="e557b-104">This article covers using storage accounts.</span></span> <span data-ttu-id="e557b-105">建議您使用受控磁碟和受管理的映像，不要使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e557b-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="e557b-106">如需詳細資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](capture-image-resource.md)。</span><span class="sxs-lookup"><span data-stu-id="e557b-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="e557b-107">本文示範如何使用 Azure PowerShell 建立使用儲存體帳戶的一般化 Azure VM 的映像。</span><span class="sxs-lookup"><span data-stu-id="e557b-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="e557b-108">然後可以使用映像來建立另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="e557b-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="e557b-109">此映像包含作業系統磁碟與連結到虛擬機器的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="e557b-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="e557b-110">映像不包含虛擬網路資源，因此您需要在建立新的 VM 時設定這些資源。</span><span class="sxs-lookup"><span data-stu-id="e557b-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e557b-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="e557b-111">Prerequisites</span></span>
<span data-ttu-id="e557b-112">您需要安裝 Azure PowerShell 1.0.x 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="e557b-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="e557b-113">如果您尚未安裝 PowerShell，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 以了解安裝步驟。</span><span class="sxs-lookup"><span data-stu-id="e557b-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="e557b-114">一般化 VM</span><span class="sxs-lookup"><span data-stu-id="e557b-114">Generalize the VM</span></span> 
<span data-ttu-id="e557b-115">本節說明如何將 Windows 虛擬機器一般化以做為映像。</span><span class="sxs-lookup"><span data-stu-id="e557b-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="e557b-116">將 VM 一般化會移除您的所有個人帳戶資訊，以及其他項目，並準備電腦作為映像。</span><span class="sxs-lookup"><span data-stu-id="e557b-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="e557b-117">如需 Sysprep 的詳細資訊，請參閱 [如何使用 Sysprep：簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e557b-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="e557b-118">請確定 Sysprep 支援電腦上執行的伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="e557b-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="e557b-119">如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="e557b-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e557b-120">如果您是第一次將 VHD 上傳至 Azure，請確定您已[準備好 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 再執行 Sysprep。</span><span class="sxs-lookup"><span data-stu-id="e557b-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="e557b-121">您也可以使用 `sudo waagent -deprovision+user` 將 Linux VM 一般化，然後使用 PowerShell 來擷取該 VM.</span><span class="sxs-lookup"><span data-stu-id="e557b-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="e557b-122">如需有關使用 CLI 來擷取 VM 的資訊，請參閱[如何使用 Azure CLI 來一般化和擷取 Linux 虛擬機器](../linux/capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="e557b-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="e557b-123">登入 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e557b-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="e557b-124">以系統管理員身分開啟 [命令提示字元] 視窗。</span><span class="sxs-lookup"><span data-stu-id="e557b-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="e557b-125">切換至 **%windir%\system32\sysprep** 目錄，然後執行 `sysprep.exe`。</span><span class="sxs-lookup"><span data-stu-id="e557b-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="e557b-126">在 [系統準備工具] 對話方塊中，選取 [進入系統全新體驗 (OOBE)]，並確認已勾選 [一般化] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="e557b-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="e557b-127">在 [關機選項] 中選取 [關機]。</span><span class="sxs-lookup"><span data-stu-id="e557b-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="e557b-128">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e557b-128">Click **OK**.</span></span>
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="e557b-130">Sysprep 完成時，會關閉虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e557b-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e557b-131">在您完成將 VHD 上傳到 Azure 或從 VM 建立映像之前，請勿重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="e557b-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="e557b-132">如果 VM 意外重新啟動，請執行 Sysprep 來重新將它一般化。</span><span class="sxs-lookup"><span data-stu-id="e557b-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="e557b-133">登入 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e557b-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="e557b-134">開啟 Azure PowerShell，並登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e557b-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="e557b-135">這會開啟一個可供您輸入 Azure 帳戶認證的快顯視窗。</span><span class="sxs-lookup"><span data-stu-id="e557b-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="e557b-136">取得您可用訂用帳戶的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="e557b-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="e557b-137">使用訂用帳戶識別碼來設定正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e557b-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="e557b-138">解除配置 VM 並將狀態設定為一般化</span><span class="sxs-lookup"><span data-stu-id="e557b-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="e557b-139">解除配置 VM 資源。</span><span class="sxs-lookup"><span data-stu-id="e557b-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="e557b-140">Azure 入口網站中 VM 的 [狀態] 會從 [已停止] 變更為 [已停止 (已解除配置)]。</span><span class="sxs-lookup"><span data-stu-id="e557b-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="e557b-141">將虛擬機器的狀態設定為 [一般化] 。</span><span class="sxs-lookup"><span data-stu-id="e557b-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="e557b-142">檢查 VM 的狀態。</span><span class="sxs-lookup"><span data-stu-id="e557b-142">Check the status of the VM.</span></span> <span data-ttu-id="e557b-143">VM 的 [OSState/一般化] 區段中的 [DisplayStatus] 應設定為 [VM 一般化]。</span><span class="sxs-lookup"><span data-stu-id="e557b-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="e557b-144">建立映像</span><span class="sxs-lookup"><span data-stu-id="e557b-144">Create the image</span></span>

<span data-ttu-id="e557b-145">使用這個命令，在目的地儲存體容器中建立未受管理的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="e557b-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="e557b-146">此映像會建立在與原始虛擬機器相同的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e557b-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="e557b-147">`-Path` 參數會將來源 VM 的 JSON 範本複本儲存到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="e557b-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="e557b-148">`-DestinationContainerName` 參數是要用以保存映像的容器名稱。</span><span class="sxs-lookup"><span data-stu-id="e557b-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="e557b-149">如果此容器不存在，則會為您建立。</span><span class="sxs-lookup"><span data-stu-id="e557b-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="e557b-150">您可以從 JSON 檔案範本取得映像的 URL。</span><span class="sxs-lookup"><span data-stu-id="e557b-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="e557b-151">請依序前往 [資源]  >  [storageProfile]  >  [osDisk]  >  [映像]  >  [uri] 區段，取得您映像的完整路徑。</span><span class="sxs-lookup"><span data-stu-id="e557b-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="e557b-152">映像的 URL 如下所示： `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`</span><span class="sxs-lookup"><span data-stu-id="e557b-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="e557b-153">您也可以在入口網站中驗證 URI。</span><span class="sxs-lookup"><span data-stu-id="e557b-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="e557b-154">系統會將映像複製到儲存體帳戶中名為 **system** 的容器中。</span><span class="sxs-lookup"><span data-stu-id="e557b-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="e557b-155">從映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="e557b-155">Create a VM from the image</span></span>

<span data-ttu-id="e557b-156">現在您可以從未受管理的映像建立一或多部 VM。</span><span class="sxs-lookup"><span data-stu-id="e557b-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="e557b-157">設定 VHD 的 URI</span><span class="sxs-lookup"><span data-stu-id="e557b-157">Set the URI of the VHD</span></span>

<span data-ttu-id="e557b-158">要使用之 VHD 的 URI 格式如下：https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd。</span><span class="sxs-lookup"><span data-stu-id="e557b-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="e557b-159">在此範例中，名為 **myVHD** 的 VHD 位於容器 **mycontainer** 中的儲存體帳戶 **mystorageaccount**。</span><span class="sxs-lookup"><span data-stu-id="e557b-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="e557b-160">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e557b-160">Create a virtual network</span></span>
<span data-ttu-id="e557b-161">建立[虛擬網路](../../virtual-network/virtual-networks-overview.md)的 vNet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="e557b-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="e557b-162">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="e557b-162">Create the subnet.</span></span> <span data-ttu-id="e557b-163">下列範例會在資源群組 **myResourceGroup** 中建立名為 **mySubnet** 的子網路，而其位址首碼為 **10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="e557b-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="e557b-164">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e557b-164">Create the virtual network.</span></span> <span data-ttu-id="e557b-165">下列範例會在**美國西部**位置中建立名為 **myVnet** 的虛擬網路，其位址首碼為 **10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="e557b-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="e557b-166">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="e557b-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="e557b-167">若要能夠與虛擬網路中的虛擬機器進行通訊，您需要 [公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 和網路介面。</span><span class="sxs-lookup"><span data-stu-id="e557b-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="e557b-168">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e557b-168">Create a public IP address.</span></span> <span data-ttu-id="e557b-169">此範例會建立名為 **myPip** 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e557b-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="e557b-170">建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="e557b-170">Create the NIC.</span></span> <span data-ttu-id="e557b-171">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="e557b-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="e557b-172">建立網路安全性群組和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="e557b-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="e557b-173">若要能夠使用 RDP 登入 VM，您必須有可在連接埠 3389 上允許 RDP 存取的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="e557b-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="e557b-174">此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="e557b-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="e557b-175">如需 NSG 的詳細資訊，請參閱[使用 PowerShell 對 Azure 中的 VM 開啟連接埠](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e557b-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="e557b-176">建立虛擬網路的變數</span><span class="sxs-lookup"><span data-stu-id="e557b-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="e557b-177">為已完成的虛擬網路建立變數。</span><span class="sxs-lookup"><span data-stu-id="e557b-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="e557b-178">建立 VM</span><span class="sxs-lookup"><span data-stu-id="e557b-178">Create the VM</span></span>
<span data-ttu-id="e557b-179">下列 PowerShell 會完成虛擬機器設定，並使用未受管理的映像當做新安裝的來源。</span><span class="sxs-lookup"><span data-stu-id="e557b-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="e557b-180">確認已建立 VM</span><span class="sxs-lookup"><span data-stu-id="e557b-180">Verify that the VM was created</span></span>
<span data-ttu-id="e557b-181">完成時，在 [Azure 入口網站](https://portal.azure.com)的 [瀏覽] > [虛擬機器] 底下，或是使用下列 PowerShell 命令，應該就可以看到新建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="e557b-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="e557b-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e557b-182">Next steps</span></span>
<span data-ttu-id="e557b-183">若要使用 Azure PowerShell 管理新的虛擬機器，請參閱 [使用 Azure Resource Manager 與 PowerShell 管理虛擬機器](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e557b-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


