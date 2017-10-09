---
title: "aaaAvailability 適用於 Linux Vm 在 Azure 中設定教學課程 |Microsoft 文件"
description: "適用於 Linux Vm 在 Azure 中，以了解 hello 可用性設定組。"
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="7b857-103">如何 toouse 可用性設定組</span><span class="sxs-lookup"><span data-stu-id="7b857-103">How toouse availability sets</span></span>


<span data-ttu-id="7b857-104">在本教學課程中，您將學習如何 tooincrease hello 可用性和可靠性的虛擬機器上使用此功能的 Azure 方案的呼叫可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="7b857-105">可用性設定組，請確定您在 Azure 上部署的 Vm 會分散到多個隔離的硬體叢集該 hello。</span><span class="sxs-lookup"><span data-stu-id="7b857-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="7b857-106">如此一來，可確保如果在 Azure 中的硬體或軟體失敗，會影響您的 Vm 子組可用且正常運作，從您的客戶使用它的 hello 觀點來看，將會保留您的整體解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b857-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="7b857-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="7b857-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7b857-108">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="7b857-108">Create an availability set</span></span>
> * <span data-ttu-id="7b857-109">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="7b857-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="7b857-110">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="7b857-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7b857-111">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7b857-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7b857-112">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7b857-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7b857-113">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7b857-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="7b857-114">可用性設定組概觀</span><span class="sxs-lookup"><span data-stu-id="7b857-114">Availability set overview</span></span>

<span data-ttu-id="7b857-115">可用性設定組中您在其中放置 hello VM 資源時，都是彼此隔離的 Azure 資料中心內部署的 Azure tooensure 是一種邏輯群組功能，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="7b857-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="7b857-116">Azure 可確保該 hello 您放置多個實體伺服器上執行可用性設定組內的 Vm、 計算機架、 儲存體單位及網路交換器。</span><span class="sxs-lookup"><span data-stu-id="7b857-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="7b857-117">這樣可以確保在 hello 事件中的硬體或 Azure 軟體失敗，會影響 Vm 的子集，整體應用程式將保持為設定並繼續 toobe 可用 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="7b857-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="7b857-118">使用可用性設定組時，重要的功能 tooleverage 想 toobuild 可靠的雲端解決方案。</span><span class="sxs-lookup"><span data-stu-id="7b857-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="7b857-119">請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。</span><span class="sxs-lookup"><span data-stu-id="7b857-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="7b857-120">有了 Azure，您會想 toodefine 兩個可用性設定組才能部署您的 Vm: hello"web"層和一個可用性設定 hello 「 資料庫 」 層的一個可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="7b857-121">當您建立新的 VM，您可以接著指定 hello 可用性設定組參數 toohello az vm 建立命令，以及 Azure 會自動確保該 hello hello 可用中所建立的 Vm 組會隔離跨多個實體硬體資源。</span><span class="sxs-lookup"><span data-stu-id="7b857-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="7b857-122">這表示如果 hello 實體硬體上執行您的 Web 伺服器或資料庫伺服器 Vm 的其中一個發生問題，您知道該 hello 網頁伺服器及資料庫 Vm 的其他執行個體將會繼續執行正常因為它們是在不同硬體上。</span><span class="sxs-lookup"><span data-stu-id="7b857-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="7b857-123">當您想 toodeploy 可靠 VM 為基礎的解決方案在 Azure 中，您應該一律使用可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="7b857-124">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="7b857-124">Create an availability set</span></span>

<span data-ttu-id="7b857-125">您可以使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 來建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="7b857-126">在此範例中，我們設定兩個 hello 的更新和容錯網域數目在*2* hello 可用性名為*myAvailabilitySet*在 hello *myResourceGroupAvailability*資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b857-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="7b857-127">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="7b857-127">Create a resource group.</span></span>

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

<span data-ttu-id="7b857-128">可用性設定組可讓您 tooisolate 資源跨 「 故障網域 」 和 「 更新網域 」。</span><span class="sxs-lookup"><span data-stu-id="7b857-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="7b857-129">**容錯網域**代表以隔離方式集合在一起的伺服器、網路和儲存體資源。</span><span class="sxs-lookup"><span data-stu-id="7b857-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="7b857-130">在上述範例中的 hello，我們表示我們想要我們可用性設定組 toobe 我們 Vm 部署時，分散在至少兩個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="7b857-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="7b857-131">我們也表示我們想要讓可用性設定組分散到兩個**更新網域**。</span><span class="sxs-lookup"><span data-stu-id="7b857-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="7b857-132">兩個更新網域確保 Azure 會執行軟體更新 VM 資源都會隔離，導致無法更新在 hello 我們 VM 執行的所有 hello 軟體相同的時間。</span><span class="sxs-lookup"><span data-stu-id="7b857-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="7b857-133">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b857-133">Configure virtual network</span></span>
<span data-ttu-id="7b857-134">您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="7b857-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="7b857-135">如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7b857-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="7b857-136">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="7b857-136">Create network resources</span></span>
<span data-ttu-id="7b857-137">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7b857-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="7b857-138">hello 下列範例會建立虛擬網路，名為*myVnet*與子網路，名為*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="7b857-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="7b857-139">使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="7b857-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="7b857-140">hello 下列範例會建立三個虛擬 Nic。</span><span class="sxs-lookup"><span data-stu-id="7b857-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="7b857-141">（每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。</span><span class="sxs-lookup"><span data-stu-id="7b857-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="7b857-142">您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="7b857-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="7b857-143">建立位於可用性設定組內的 VM</span><span class="sxs-lookup"><span data-stu-id="7b857-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="7b857-144">Vm 必須確定正確分散 hello 硬體的 hello 可用性集 toomake 內建立。</span><span class="sxs-lookup"><span data-stu-id="7b857-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="7b857-145">您無法加入現有 VM tooan 可用性設定組建立之後。</span><span class="sxs-lookup"><span data-stu-id="7b857-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="7b857-146">當您建立 VM 使用[az vm 建立](/cli/azure/vm#create)指定 hello 可用性設定組使用 hello`--availability-set`參數 toospecify hello 名稱 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="7b857-147">現在，我們新建立的可用性設定組內有兩部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7b857-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="7b857-148">因為它們是在 hello 相同可用性設定組，Azure 可確保該 hello Vm 及其所有資源 （包括資料磁碟） 會分散到隔離的實體硬體。</span><span class="sxs-lookup"><span data-stu-id="7b857-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="7b857-149">這樣的分佈方式有助於確保 VM 解決方案整體有更高的可用性。</span><span class="sxs-lookup"><span data-stu-id="7b857-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="7b857-150">當您新增 Vm 可能會遇到的一件事是特定的 VM 大小已不再可用 toouse 可用性集內。</span><span class="sxs-lookup"><span data-stu-id="7b857-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="7b857-151">如果不再有足夠的容量 tooadd 它同時保留 hello 隔離規則 hello 可用性設定組會強制執行，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="7b857-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="7b857-152">您可以檢查 toosee 哪些 VM 大小是使用中的現有的可用性設定組使用 hello toouse`--availability-set list-sizes`參數。</span><span class="sxs-lookup"><span data-stu-id="7b857-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="7b857-153">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="7b857-153">Check for available VM sizes</span></span> 

<span data-ttu-id="7b857-154">您可以加入更多的 Vm toohello 可用性設定組更新版本中，但您需要一個 tooknow hello 硬體上可用哪些 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="7b857-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="7b857-155">使用[az vm 可用性設定組清單大小](/cli/azure/availability-set#list-sizes)toolist hello 硬體上的 hello 可用大小叢集以 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7b857-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="7b857-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b857-156">Next steps</span></span>

<span data-ttu-id="7b857-157">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="7b857-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7b857-158">建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="7b857-158">Create an availability set</span></span>
> * <span data-ttu-id="7b857-159">在可用性設定組中建立 VM</span><span class="sxs-lookup"><span data-stu-id="7b857-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="7b857-160">檢查可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="7b857-160">Check available VM sizes</span></span>

<span data-ttu-id="7b857-161">前進 toohello 下一個教學課程的 toolearn 有關虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="7b857-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7b857-162">建立 VM 擴展集</span><span class="sxs-lookup"><span data-stu-id="7b857-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

