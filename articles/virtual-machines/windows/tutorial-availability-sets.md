---
title: "Azure 中 Windows VM 的可用性設定組教學課程 | Microsoft Docs"
description: "了解 Azure 中 Windows VM 的可用性設定組。"
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
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="aed46-103">如何使用可用性設定組</span><span class="sxs-lookup"><span data-stu-id="aed46-103">How to use availability sets</span></span>

<span data-ttu-id="aed46-104">在本教學課程中，您會學到如何使用稱為「可用性設定組」的功能，增加 Azure 虛擬機器解決方案的可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="aed46-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="aed46-105">可用性設定組可確保您在 Azure 上部署的 VM 會分散到多個各自獨立的硬體叢集中。</span><span class="sxs-lookup"><span data-stu-id="aed46-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="aed46-106">這麼做可以確保當 Azure 發生硬體或軟體故障時，受到影響的只會是一小部分的 VM，整體解決方案會維持可用且正常運作，而作為使用者的客戶卻不會發現故障情形。</span><span class="sxs-lookup"><span data-stu-id="aed46-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="aed46-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="aed46-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed46-108">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="aed46-108">Create an availability set</span></span>
> * <span data-ttu-id="aed46-109">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="aed46-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="aed46-110">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="aed46-110">Check available VM sizes</span></span>

<span data-ttu-id="aed46-111">本教學課程需要 Azure PowerShell 模組 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="aed46-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="aed46-112">執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="aed46-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="aed46-113">如果您需要升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="aed46-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="aed46-114">可用性設定組概觀</span><span class="sxs-lookup"><span data-stu-id="aed46-114">Availability set overview</span></span>

<span data-ttu-id="aed46-115">可用性設定組是一種可在 Azure 中使用的邏輯群組功能，用以確保其中所放置的 VM 資源在部署到 Azure 資料中心時會彼此隔離。</span><span class="sxs-lookup"><span data-stu-id="aed46-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="aed46-116">Azure 可確保您在可用性設定組中所放置的 VM，會橫跨多部實體伺服器、計算機架、儲存體單位和網路交換器來執行。</span><span class="sxs-lookup"><span data-stu-id="aed46-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="aed46-117">如此便能確保當硬體或 Azure 軟體發生故障時，只有一小部分的 VM 會受到影響，整個應用程式會保持運作狀態，可供客戶繼續使用。</span><span class="sxs-lookup"><span data-stu-id="aed46-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="aed46-118">如果您想要建置可靠的雲端解決方案，就一定要運用可用性設定組功能。</span><span class="sxs-lookup"><span data-stu-id="aed46-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="aed46-119">請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="aed46-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="aed46-120">在使用 Azure 時，建議您先定義兩個可用性設定組，再部署 VM︰一個可用性設定組用來放置「Web」層，另一個可用性設定組用來放置「資料庫」層。</span><span class="sxs-lookup"><span data-stu-id="aed46-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="aed46-121">當您建立新的 VM 時，您便可以將可用性設定組指定為 az vm create 命令的參數，Azure 會自動確保您在可用性設定組內所建立的 VM，會跨多個實體硬體資源來隔離。</span><span class="sxs-lookup"><span data-stu-id="aed46-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="aed46-122">這表示，如果其中一個用來執行 Web 伺服器或資料庫伺服器 VM 的實體硬體發生問題，您知道 Web 伺服器和資料庫 VM 的其他執行個體會繼續正常執行，因為它們位於不同硬體上。</span><span class="sxs-lookup"><span data-stu-id="aed46-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="aed46-123">如果您想要在 Azure 中部署可靠的 VM 架構解決方案，請務必使用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="aed46-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="aed46-124">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="aed46-124">Create an availability set</span></span>

<span data-ttu-id="aed46-125">您可以使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="aed46-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="aed46-126">在此範例中，我們將針對 *myResourceGroupAvailability* 資源群組中名為 *myAvailabilitySet* 的可用性設定組，同時將更新數目和容錯網域數目設為 *2*。</span><span class="sxs-lookup"><span data-stu-id="aed46-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="aed46-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="aed46-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="aed46-128">建立位於可用性設定組內的 VM</span><span class="sxs-lookup"><span data-stu-id="aed46-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="aed46-129">VM 需要建立於可用性設定組內，以確保其會正確地分散到硬體上。</span><span class="sxs-lookup"><span data-stu-id="aed46-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="aed46-130">您無法在建立可用性設定組之後，將現有的 VM 加入至其中。</span><span class="sxs-lookup"><span data-stu-id="aed46-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="aed46-131">位置中的硬體已分為多個更新網域和容錯網域。</span><span class="sxs-lookup"><span data-stu-id="aed46-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="aed46-132">**更新網域**是一組虛擬機器和可同時重新啟動的基礎實體硬體。</span><span class="sxs-lookup"><span data-stu-id="aed46-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="aed46-133">相同**容錯網域**中的 VM 會共用一般儲存體以及通用電源和網路交換器。</span><span class="sxs-lookup"><span data-stu-id="aed46-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="aed46-134">當您透過 [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) 使用組態建立 VM 時，會使用 `-AvailabilitySetId`參數來指定可用性設定組，以指定可用性設定組的識別碼。</span><span class="sxs-lookup"><span data-stu-id="aed46-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="aed46-135">在可用性設定組中使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立兩部 VM。</span><span class="sxs-lookup"><span data-stu-id="aed46-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

   # Here is where we specify the availability set
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

<span data-ttu-id="aed46-136">建立及設定這兩部 VM 需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="aed46-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="aed46-137">完成後，您將有 2 部分散於基礎硬體上的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="aed46-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="aed46-138">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="aed46-138">Check for available VM sizes</span></span> 

<span data-ttu-id="aed46-139">您稍後可以將更多 VM 加入至可用性設定組，但是需要知道硬體上有哪些可用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="aed46-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="aed46-140">針對可用性設定組，使用 [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) 來列出硬體叢集上所有可用的大小。</span><span class="sxs-lookup"><span data-stu-id="aed46-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="aed46-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aed46-141">Next steps</span></span>

<span data-ttu-id="aed46-142">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="aed46-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed46-143">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="aed46-143">Create an availability set</span></span>
> * <span data-ttu-id="aed46-144">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="aed46-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="aed46-145">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="aed46-145">Check available VM sizes</span></span>

<span data-ttu-id="aed46-146">請前進到下一個教學課程，以了解虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="aed46-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aed46-147">建立 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="aed46-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


