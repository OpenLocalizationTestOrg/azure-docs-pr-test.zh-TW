---
title: "Azure 中 Linux VM 的可用性設定組教學課程 | Microsoft Docs"
description: "了解 Azure 中 Linux VM 的可用性設定組。"
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="df737-103">如何使用可用性設定組</span><span class="sxs-lookup"><span data-stu-id="df737-103">How to use availability sets</span></span>


<span data-ttu-id="df737-104">在本教學課程中，您會學到如何使用稱為「可用性設定組」的功能，增加 Azure 虛擬機器解決方案的可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="df737-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="df737-105">可用性設定組可確保您在 Azure 上部署的 VM 會分散到多個各自獨立的硬體叢集中。</span><span class="sxs-lookup"><span data-stu-id="df737-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="df737-106">這麼做可以確保當 Azure 發生硬體或軟體故障時，受到影響的只會是一小部分的 VM，整體解決方案會維持可用且正常運作，而作為使用者的客戶卻不會發現故障情形。</span><span class="sxs-lookup"><span data-stu-id="df737-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="df737-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="df737-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df737-108">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="df737-108">Create an availability set</span></span>
> * <span data-ttu-id="df737-109">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="df737-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="df737-110">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="df737-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="df737-111">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="df737-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="df737-112">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="df737-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="df737-113">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="df737-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="df737-114">可用性設定組概觀</span><span class="sxs-lookup"><span data-stu-id="df737-114">Availability set overview</span></span>

<span data-ttu-id="df737-115">可用性設定組是一種可在 Azure 中使用的邏輯群組功能，用以確保其中所放置的 VM 資源在部署到 Azure 資料中心時會彼此隔離。</span><span class="sxs-lookup"><span data-stu-id="df737-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="df737-116">Azure 可確保您在可用性設定組中所放置的 VM，會橫跨多部實體伺服器、計算機架、儲存體單位和網路交換器來執行。</span><span class="sxs-lookup"><span data-stu-id="df737-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="df737-117">如此便能確保當硬體或 Azure 軟體發生故障時，只有一小部分的 VM 會受到影響，整個應用程式會保持運作狀態，可供客戶繼續使用。</span><span class="sxs-lookup"><span data-stu-id="df737-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="df737-118">如果您想要建置可靠的雲端解決方案，就一定要運用可用性設定組功能。</span><span class="sxs-lookup"><span data-stu-id="df737-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="df737-119">請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="df737-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="df737-120">在使用 Azure 時，建議您先定義兩個可用性設定組，再部署 VM︰一個可用性設定組用來放置「Web」層，另一個可用性設定組用來放置「資料庫」層。</span><span class="sxs-lookup"><span data-stu-id="df737-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="df737-121">當您建立新的 VM 時，您便可以將可用性設定組指定為 az vm create 命令的參數，Azure 會自動確保您在可用性設定組內所建立的 VM，會跨多個實體硬體資源來隔離。</span><span class="sxs-lookup"><span data-stu-id="df737-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="df737-122">這表示，如果其中一個用來執行 Web 伺服器或資料庫伺服器 VM 的實體硬體發生問題，您知道 Web 伺服器和資料庫 VM 的其他執行個體會繼續正常執行，因為它們位於不同硬體上。</span><span class="sxs-lookup"><span data-stu-id="df737-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="df737-123">如果您想要在 Azure 中部署可靠的虛擬機器架構解決方案，請務必使用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="df737-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="df737-124">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="df737-124">Create an availability set</span></span>

<span data-ttu-id="df737-125">您可以使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 來建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="df737-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="df737-126">在此範例中，我們將針對 *myResourceGroupAvailability* 資源群組中名為 *myAvailabilitySet* 的可用性設定組，同時將更新數目和容錯網域數目設為 *2*。</span><span class="sxs-lookup"><span data-stu-id="df737-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="df737-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="df737-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="df737-128">可用性設定組可讓您跨「容錯網域」和「更新網域」來隔離資源。</span><span class="sxs-lookup"><span data-stu-id="df737-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="df737-129">**容錯網域**代表以隔離方式集合在一起的伺服器、網路和儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="df737-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="df737-130">在前面的範例中，我們表示我們想在部署 VM 時，讓可用性設定組分散到至少兩個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="df737-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="df737-131">我們也表示我們想要讓可用性設定組分散到兩個**更新網域**。</span><span class="sxs-lookup"><span data-stu-id="df737-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="df737-132">兩個更新網域可確保當 Azure 執行軟體更新時，我們的 VM 資源是隔離的，以免 VM 中執行的所有軟體同時更新。</span><span class="sxs-lookup"><span data-stu-id="df737-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="df737-133">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="df737-133">Configure virtual network</span></span>
<span data-ttu-id="df737-134">請先建立支援的虛擬網路資源，才可部署一些 VM 及測試您的平衡器。</span><span class="sxs-lookup"><span data-stu-id="df737-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="df737-135">如需虛擬網路的詳細資訊，請參閱[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="df737-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="df737-136">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="df737-136">Create network resources</span></span>
<span data-ttu-id="df737-137">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="df737-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="df737-138">下列範例會建立名為 myVnet 的虛擬網路和名為 mySubnet 的子網路：</span><span class="sxs-lookup"><span data-stu-id="df737-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="df737-139">使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="df737-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="df737-140">下列範例會建立三個虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="df737-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="df737-141">(您在下列步驟中針對應用程式建立的每部 VM 都有一個虛擬 NIC)。</span><span class="sxs-lookup"><span data-stu-id="df737-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="df737-142">您可以隨時建立其他虛擬 NIC 和 VM，並將它們新增至負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="df737-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="df737-143">建立位於可用性設定組內的 VM</span><span class="sxs-lookup"><span data-stu-id="df737-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="df737-144">您必須將 VM 建立於可用性設定組內，才能確保 VM 會在硬體中正確地分散。</span><span class="sxs-lookup"><span data-stu-id="df737-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="df737-145">您無法在建立可用性設定組之後，將現有的 VM 加入至其中。</span><span class="sxs-lookup"><span data-stu-id="df737-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="df737-146">當您使用 [az vm create](/cli/azure/vm#create) 建立 VM 時，會使用 `--availability-set` 參數來指定可用性設定組，以指定可用性設定組的名稱。</span><span class="sxs-lookup"><span data-stu-id="df737-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="df737-147">現在，我們新建立的可用性設定組內有兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="df737-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="df737-148">由於它們位於相同的可用性設定組內，Azure 會確保 VM 和其所有資源 (包括資料磁碟) 會分散到隔離開來的實體硬體中。</span><span class="sxs-lookup"><span data-stu-id="df737-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="df737-149">這樣的分佈方式有助於確保 VM 解決方案整體有更高的可用性。</span><span class="sxs-lookup"><span data-stu-id="df737-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="df737-150">當您新增 VM 時，您可能會遇到特定 VM 大小已不再適用於可用性設定組的情況。</span><span class="sxs-lookup"><span data-stu-id="df737-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="df737-151">此問題的發生原因是，其容量已經不足，無法既新增 VM，又保持可用性設定組所強制實施的隔離規則。</span><span class="sxs-lookup"><span data-stu-id="df737-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="df737-152">您可以使用 `--availability-set list-sizes` 參數，檢查看看有哪些 VM 大小可在現有的可用性設定組內使用。</span><span class="sxs-lookup"><span data-stu-id="df737-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="df737-153">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="df737-153">Check for available VM sizes</span></span> 

<span data-ttu-id="df737-154">您稍後可以將更多 VM 加入至可用性設定組，但是需要知道硬體上有哪些可用的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="df737-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="df737-155">針對可用性設定組，使用 [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) 來列出硬體叢集上所有可用的大小。</span><span class="sxs-lookup"><span data-stu-id="df737-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="df737-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df737-156">Next steps</span></span>

<span data-ttu-id="df737-157">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="df737-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df737-158">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="df737-158">Create an availability set</span></span>
> * <span data-ttu-id="df737-159">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="df737-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="df737-160">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="df737-160">Check available VM sizes</span></span>

<span data-ttu-id="df737-161">請前進到下一個教學課程，以了解虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="df737-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df737-162">建立 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="df737-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

