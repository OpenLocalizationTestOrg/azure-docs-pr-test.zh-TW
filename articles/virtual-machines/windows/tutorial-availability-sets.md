---
title: "aaaAvailability 適用於 Windows Vm 在 Azure 中設定教學課程 |Microsoft 文件"
description: "深入了解 hello 可用性集的 Windows Azure 中的 Vm。"
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="2a327-103">如何 toouse 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2a327-103">How toouse availability sets</span></span>

<span data-ttu-id="2a327-104">在本教學課程中，您將學習如何 tooincrease hello 可用性和可靠性的虛擬機器上使用此功能的 Azure 方案的呼叫可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="2a327-105">可用性設定組，請確定您在 Azure 上部署的 Vm 會分散到多個隔離的硬體叢集該 hello。</span><span class="sxs-lookup"><span data-stu-id="2a327-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="2a327-106">如此一來，可確保如果在 Azure 中的硬體或軟體失敗，會影響您的 Vm 子組可用且正常運作，從您的客戶使用它的 hello 觀點來看，將會保留您的整體解決方案。</span><span class="sxs-lookup"><span data-stu-id="2a327-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="2a327-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="2a327-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a327-108">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2a327-108">Create an availability set</span></span>
> * <span data-ttu-id="2a327-109">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="2a327-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="2a327-110">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="2a327-110">Check available VM sizes</span></span>

<span data-ttu-id="2a327-111">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2a327-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="2a327-112">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="2a327-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="2a327-113">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="2a327-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="2a327-114">可用性設定組概觀</span><span class="sxs-lookup"><span data-stu-id="2a327-114">Availability set overview</span></span>

<span data-ttu-id="2a327-115">可用性設定組中您在其中放置 hello VM 資源時，都是彼此隔離的 Azure 資料中心內部署的 Azure tooensure 是一種邏輯群組功能，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="2a327-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="2a327-116">Azure 可確保該 hello 您放置多個實體伺服器上執行可用性設定組內的 Vm、 計算機架、 儲存體單位及網路交換器。</span><span class="sxs-lookup"><span data-stu-id="2a327-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="2a327-117">這樣可以確保在 hello 事件中的硬體或 Azure 軟體失敗，會影響 Vm 的子集，整體應用程式將保持為設定並繼續 toobe 可用 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="2a327-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="2a327-118">使用可用性設定組時，重要的功能 tooleverage 想 toobuild 可靠的雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="2a327-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="2a327-119">請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="2a327-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="2a327-120">有了 Azure，您會想 toodefine 兩個可用性設定組才能部署您的 Vm: hello"web"層和一個可用性設定 hello 「 資料庫 」 層的一個可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="2a327-121">當您建立新的 VM，您可以接著指定 hello 可用性設定組參數 toohello az vm 建立命令，以及 Azure 會自動確保該 hello hello 可用中所建立的 Vm 組會隔離跨多個實體硬體資源。</span><span class="sxs-lookup"><span data-stu-id="2a327-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="2a327-122">這表示如果 hello 實體硬體上執行您的 Web 伺服器或資料庫伺服器 Vm 的其中一個發生問題，您知道該 hello 網頁伺服器及資料庫 Vm 的其他執行個體將會繼續執行正常因為它們是在不同硬體上。</span><span class="sxs-lookup"><span data-stu-id="2a327-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="2a327-123">當您想在 Azure 中的 toodeploy 可靠 VM 基礎解決方案時，您應該一律使用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="2a327-124">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2a327-124">Create an availability set</span></span>

<span data-ttu-id="2a327-125">您可以使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="2a327-126">在此範例中，我們設定兩個 hello 的更新和容錯網域數目在*2* hello 可用性名為*myAvailabilitySet*在 hello *myResourceGroupAvailability*資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a327-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="2a327-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="2a327-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="2a327-128">建立位於可用性設定組內的 VM</span><span class="sxs-lookup"><span data-stu-id="2a327-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="2a327-129">Vm 需要 toobe hello 可用性集 toomake 確定正確分散 hello 硬體內建立。</span><span class="sxs-lookup"><span data-stu-id="2a327-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="2a327-130">您無法加入現有 VM tooan 可用性設定組建立之後。</span><span class="sxs-lookup"><span data-stu-id="2a327-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="2a327-131">分割的位置中的 hello 硬體 toomultiple 更新網域和故障網域。</span><span class="sxs-lookup"><span data-stu-id="2a327-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="2a327-132">**更新網域**是一組的 Vm 和可以重新啟動在 hello 的基礎實體硬體相同的時間。</span><span class="sxs-lookup"><span data-stu-id="2a327-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="2a327-133">中的 Vm hello 相同**容錯網域**共用通用的儲存體，以及通用電源來源和網路交換器。</span><span class="sxs-lookup"><span data-stu-id="2a327-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="2a327-134">當您使用建立 VM 組態使用[新增 AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)指定 hello 可用性設定組使用 hello`-AvailabilitySetId`參數 toospecify hello 識別碼 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="2a327-135">建立具有 2 個 Vm[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) hello 可用性設定。</span><span class="sxs-lookup"><span data-stu-id="2a327-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="2a327-136">它會採用幾分鐘的時間 toocreate 並設定這兩個 Vm。</span><span class="sxs-lookup"><span data-stu-id="2a327-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="2a327-137">完成時，您必須 2 的虛擬機器分散於 hello 基礎硬體。</span><span class="sxs-lookup"><span data-stu-id="2a327-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="2a327-138">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="2a327-138">Check for available VM sizes</span></span> 

<span data-ttu-id="2a327-139">您可以加入更多的 Vm toohello 可用性設定組更新版本中，但您需要一個 tooknow hello 硬體上可用哪些 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2a327-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="2a327-140">使用[Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist hello 硬體上的 hello 可用大小叢集以 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="2a327-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="2a327-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a327-141">Next steps</span></span>

<span data-ttu-id="2a327-142">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="2a327-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2a327-143">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="2a327-143">Create an availability set</span></span>
> * <span data-ttu-id="2a327-144">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="2a327-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="2a327-145">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="2a327-145">Check available VM sizes</span></span>

<span data-ttu-id="2a327-146">前進 toohello 下一個教學課程的 toolearn 有關虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="2a327-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a327-147">建立 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="2a327-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


