---
title: "aaaCreate 自訂 VM 映像以 hello Azure PowerShell |Microsoft 文件"
description: "教學課程-建立自訂 VM 映像使用 hello Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a><span data-ttu-id="bbf8e-103">使用 PowerShell 建立 Azure VM 的自訂映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-103">Create a custom image of an Azure VM using PowerShell</span></span>

<span data-ttu-id="bbf8e-104">自訂映像類似 Marketplace 映像，但您要自行建立它們。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-104">Custom images are like marketplace images, but you create them yourself.</span></span> <span data-ttu-id="bbf8e-105">自訂映像可以使用的 toobootstrap 組態，例如預先載入應用程式、 應用程式設定和其他作業系統設定。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-105">Custom images can be used toobootstrap configurations such as preloading applications, application configurations, and other OS configurations.</span></span> <span data-ttu-id="bbf8e-106">在本教學課程中，您將建立自己的 Azure 虛擬機器自訂映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-106">In this tutorial, you create your own custom image of an Azure virtual machine.</span></span> <span data-ttu-id="bbf8e-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="bbf8e-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbf8e-108">執行 sysprep 及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-108">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="bbf8e-109">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-109">Create a custom image</span></span>
> * <span data-ttu-id="bbf8e-110">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-110">Create a VM from a custom image</span></span>
> * <span data-ttu-id="bbf8e-111">列出您的訂用帳戶中的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-111">List all hello images in your subscription</span></span>
> * <span data-ttu-id="bbf8e-112">删除映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-112">Delete an image</span></span>

<span data-ttu-id="bbf8e-113">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bbf8e-114">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bbf8e-115">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bbf8e-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="bbf8e-116">Before you begin</span></span>

<span data-ttu-id="bbf8e-117">下列的 hello 步驟詳細說明 tootake 現有的 VM 並開啟它的可重複使用的自訂映像，您可以使用 toocreate 新 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-117">hello steps below detail how tootake an existing VM and turn it into a re-usable custom image that you can use toocreate new VM instances.</span></span>

<span data-ttu-id="bbf8e-118">在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-118">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="bbf8e-119">如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-119">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="bbf8e-120">當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-120">When working through hello tutorial, replace hello resource group and VM names where needed.</span></span>

## <a name="prepare-vm"></a><span data-ttu-id="bbf8e-121">準備 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-121">Prepare VM</span></span>

<span data-ttu-id="bbf8e-122">toocreate 虛擬機器的映像，您需要 tooprepare hello 一般化 hello VM 解除配置，，然後將標示 hello 來源為一般化 Azure 中 VM 的 VM。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-122">toocreate an image of a virtual machine, you need tooprepare hello VM by generalizing hello VM, deallocating, and then marking hello source VM as generalized in Azure.</span></span>

### <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="bbf8e-123">一般化 hello Windows VM 使用 Sysprep</span><span class="sxs-lookup"><span data-stu-id="bbf8e-123">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="bbf8e-124">Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-124">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="bbf8e-125">如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-125">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>


1. <span data-ttu-id="bbf8e-126">Toohello 虛擬機器連線。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-126">Connect toohello virtual machine.</span></span>
2. <span data-ttu-id="bbf8e-127">系統管理員身分開啟 hello 命令提示字元視窗。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-127">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="bbf8e-128">變更 hello 目錄太*%windir%\system32\sysprep*，然後執行*sysprep.exe*。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-128">Change hello directory too*%windir%\system32\sysprep*, and then run *sysprep.exe*.</span></span>
3. <span data-ttu-id="bbf8e-129">在 hello**系統準備工具**對話方塊中，選取*進入系統的全新體驗 (OOBE)*，並確定該 hello*一般化*選取核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-129">In hello **System Preparation Tool** dialog box, select *Enter System Out-of-Box Experience (OOBE)*, and make sure that hello *Generalize* check box is selected.</span></span>
4. <span data-ttu-id="bbf8e-130">在 關機選項 中選取 關機，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-130">In **Shutdown Options**, select *Shutdown* and then click **OK**.</span></span>
5. <span data-ttu-id="bbf8e-131">Sysprep 完成時，它會關閉 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-131">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="bbf8e-132">**請勿重新啟動 hello VM**。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-132">**Do not restart hello VM**.</span></span>

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a><span data-ttu-id="bbf8e-133">解除配置，並將標示為一般化 VM hello</span><span class="sxs-lookup"><span data-stu-id="bbf8e-133">Deallocate and mark hello VM as generalized</span></span>

<span data-ttu-id="bbf8e-134">toocreate 映像，hello VM 需要 toobe 解除配置，而且標示為已在 Azure 中的一般化。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-134">toocreate an image, hello VM needs toobe deallocated and marked as generalized in Azure.</span></span>

<span data-ttu-id="bbf8e-135">已取消配置的 hello VM 使用[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-135">Deallocated hello VM using [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

<span data-ttu-id="bbf8e-136">設定得 hello hello 虛擬機器狀態`-Generalized`使用[組 AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-136">Set hello status of hello virtual machine too`-Generalized` using [Set-AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm).</span></span> 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a><span data-ttu-id="bbf8e-137">建立 hello 映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-137">Create hello image</span></span>

<span data-ttu-id="bbf8e-138">現在您可以使用，以建立 hello VM 的映像[新增 AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig)和[新增 AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage)。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-138">Now you can create an image of hello VM by using [New-AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig) and [New-AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage).</span></span> <span data-ttu-id="bbf8e-139">hello 下列範例會建立名為映像*myImage*從名為 VM *myVM*。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-139">hello following example creates an image named *myImage* from a VM named *myVM*.</span></span>

<span data-ttu-id="bbf8e-140">取得 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-140">Get hello virtual machine.</span></span> 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

<span data-ttu-id="bbf8e-141">建立 hello 映像設定。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-141">Create hello image configuration.</span></span>

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

<span data-ttu-id="bbf8e-142">建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-142">Create hello image.</span></span>

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a><span data-ttu-id="bbf8e-143">從 hello 映像建立 Vm</span><span class="sxs-lookup"><span data-stu-id="bbf8e-143">Create VMs from hello image</span></span>

<span data-ttu-id="bbf8e-144">既然您具有映像，您可以建立一或多個新的 Vm 從 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-144">Now that you have an image, you can create one or more new VMs from hello image.</span></span> <span data-ttu-id="bbf8e-145">從自訂映像建立 VM 是非常類似 toocreating 使用 Marketplace 映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-145">Creating a VM from a custom image is very similar toocreating a VM using a Marketplace image.</span></span> <span data-ttu-id="bbf8e-146">當您使用 Marketplace 映像時，您會有 tooinformation 有關 hello 映像、 映像提供者、 方案、 SKU 和版本。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-146">When you use a Marketplace image, you have tooinformation about hello image, image provider, offer, SKU and version.</span></span> <span data-ttu-id="bbf8e-147">使用自訂映像，您只需要 tooprovide hello hello 自訂映像資源 ID。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-147">With a custom image, you just need tooprovide hello ID of hello custom image resource.</span></span> 

<span data-ttu-id="bbf8e-148">在下列指令碼的 hello，我們會建立一個變數*$image* toostore 資訊 hello 自訂映像使用[Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) ，然後使用[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)，並指定使用 hello hello ID *$image*變數剛才所建立。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-148">In hello following script, we create a variable *$image* toostore information about hello custom image using [Get-AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) and then we use [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) and specify hello ID using hello *$image* variable we just created.</span></span> 

<span data-ttu-id="bbf8e-149">hello 指令碼會建立名為的 VM *myVMfromImage*我們新的資源群組中的自訂映像從名為*myResourceGroupFromImage*在 hello*美國西部*位置。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-149">hello script creates a VM named *myVMfromImage* from our custom image in a new resource group named *myResourceGroupFromImage* in hello *West US* location.</span></span>


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a><span data-ttu-id="bbf8e-150">映像管理</span><span class="sxs-lookup"><span data-stu-id="bbf8e-150">Image management</span></span> 

<span data-ttu-id="bbf8e-151">以下是一些常見的管理映像工作的範例以及 toocomplete 它們使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-151">Here are some examples of common management image tasks and how toocomplete them using PowerShell.</span></span>

<span data-ttu-id="bbf8e-152">依名稱列出所有映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-152">List all images by name.</span></span>

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

<span data-ttu-id="bbf8e-153">删除映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-153">Delete an image.</span></span> <span data-ttu-id="bbf8e-154">此範例中刪除 hello 名為映像*myOldImage*從 hello *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-154">This example deletes hello image named *myOldImage* from hello *myResourceGroup*.</span></span>

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bbf8e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bbf8e-155">Next steps</span></span>

<span data-ttu-id="bbf8e-156">您在本教學課程中建立了自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-156">In this tutorial, you created a custom VM image.</span></span> <span data-ttu-id="bbf8e-157">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="bbf8e-157">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbf8e-158">執行 sysprep 及一般化 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-158">Sysprep and generalize VMs</span></span>
> * <span data-ttu-id="bbf8e-159">建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-159">Create a custom image</span></span>
> * <span data-ttu-id="bbf8e-160">從自訂映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-160">Create a VM from a custom image</span></span>
> * <span data-ttu-id="bbf8e-161">列出您的訂用帳戶中的所有 hello 映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-161">List all hello images in your subscription</span></span>
> * <span data-ttu-id="bbf8e-162">删除映像</span><span class="sxs-lookup"><span data-stu-id="bbf8e-162">Delete an image</span></span>

<span data-ttu-id="bbf8e-163">前進 toohello 下一個教學課程的 toolearn 關於如何高可用性虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bbf8e-163">Advance toohello next tutorial toolearn about how highly available virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbf8e-164">建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="bbf8e-164">Create highly available VMs</span></span>](tutorial-availability-sets.md)



