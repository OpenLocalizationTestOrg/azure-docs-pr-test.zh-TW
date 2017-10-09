---
title: "在 Azure 中設定 VM 可用性 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 受管理的可用性設定或未受管理的可用性設定虛擬機器使用 Azure PowerShell 或 hello hello Resource Manager 部署模型中的入口網站。"
keywords: "可用性設定組"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eadcdfcd28bb2fa21a4647f207b390c33e022ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="b25d1-104">建立 Azure 可用性設定組以增加 VM 可用性</span><span class="sxs-lookup"><span data-stu-id="b25d1-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="b25d1-105">可用性設定組提供備援 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b25d1-105">Availability sets provide redundancy tooyour application.</span></span> <span data-ttu-id="b25d1-106">建議您在可用性設定組中，將兩部以上的虛擬機器組成群組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="b25d1-107">此組態可確保任一個計劃或非計劃性維護事件期間，至少一部虛擬機器將會 hello 可用且符合 99.95%Azure SLA。</span><span class="sxs-lookup"><span data-stu-id="b25d1-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet hello 99.95% Azure SLA.</span></span> <span data-ttu-id="b25d1-108">如需詳細資訊，請參閱 hello[虛擬機器的 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)。</span><span class="sxs-lookup"><span data-stu-id="b25d1-108">For more information, see hello [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b25d1-109">Vm 也必須在建立 hello 相同 hello 可用性設定組的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-109">VMs must be created in hello same resource group as hello availability set.</span></span>
> 

<span data-ttu-id="b25d1-110">如果您想可用性設定組您 VM toobe 部分，您需要 toocreate hello 可用性設定第一次，或您正在建立您的第一個 VM hello 集合中。</span><span class="sxs-lookup"><span data-stu-id="b25d1-110">If you want your VM toobe part of an availability set, you need toocreate hello availability set first or while you are creating your first VM in hello set.</span></span> <span data-ttu-id="b25d1-111">如果您的 VM 將會使用受管理的磁碟，必須為受管理的可用性設定組建立 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-111">If your VM will be using Managed Disks, hello availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="b25d1-112">如需有關建立及使用可用性設定組的詳細資訊，請參閱[管理虛擬機器可用性 hello](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b25d1-112">For more information about creating and using availability sets, see [Manage hello availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-hello-portal-toocreate-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="b25d1-113">使用 hello 入口 toocreate 可用性設定組在建立 Vm 之前</span><span class="sxs-lookup"><span data-stu-id="b25d1-113">Use hello portal toocreate an availability set before creating your VMs</span></span>
1. <span data-ttu-id="b25d1-114">在 hello 中樞功能表中，按一下 **瀏覽**選取**可用性設定組**。</span><span class="sxs-lookup"><span data-stu-id="b25d1-114">In hello hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="b25d1-115">在 hello**可用性設定組 刀鋒視窗**，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="b25d1-115">On hello **Availability sets blade**, click **Add**.</span></span>
   
    ![螢幕擷取畫面顯示 hello 新增按鈕來建立新的可用性設定組。](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="b25d1-117">在 hello**建立可用性設定組**刀鋒視窗，完成 hello 資訊集合。</span><span class="sxs-lookup"><span data-stu-id="b25d1-117">On hello **Create availability set** blade, complete hello information for your set.</span></span>
   
    ![螢幕擷取畫面顯示 hello 需要 tooenter toocreate hello 可用性的資訊設定。](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="b25d1-119">**名稱**-hello 名稱應該是 1-80 個字元的數字、 字母、 句號、 底線和連字號組成。</span><span class="sxs-lookup"><span data-stu-id="b25d1-119">**Name** - hello name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="b25d1-120">hello 第一個字元必須是字母或數字。</span><span class="sxs-lookup"><span data-stu-id="b25d1-120">hello first character must be a letter or number.</span></span> <span data-ttu-id="b25d1-121">hello 最後一個字元必須是字母、 數字或底線。</span><span class="sxs-lookup"><span data-stu-id="b25d1-121">hello last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="b25d1-122">**故障網域**-錯誤網域定義 hello 群組共用通用的電力來源和網路交換器的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b25d1-122">**Fault domains** - fault domains define hello group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="b25d1-123">根據預設，hello Vm 之間設定 toothree 容錯網域隔開，而且可以是已變更的 toobetween 1 和 3。</span><span class="sxs-lookup"><span data-stu-id="b25d1-123">By default, hello VMs  are separated across up toothree fault domains and can be changed toobetween 1 and 3.</span></span>
   * <span data-ttu-id="b25d1-124">**更新網域**-五個更新網域已依預設指派，而且這可以設定 toobetween 1 到 20。</span><span class="sxs-lookup"><span data-stu-id="b25d1-124">**Update domains** -  five update domains are assigned by default and this can be set toobetween 1 and 20.</span></span> <span data-ttu-id="b25d1-125">更新網域會指出群組的虛擬機器，可以在 hello 重新開機的基礎實體硬體相同的時間。</span><span class="sxs-lookup"><span data-stu-id="b25d1-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="b25d1-126">相同，例如 hello 如果我們在此指定五個更新網域設定為單一可用性設定組內，第六個虛擬機器 hello 五個以上的虛擬機器時，將會放置到 hello 與 hello 第一部虛擬機器的相同更新網域 hello 第七個中第二個虛擬機器 hello，等等的 UD。</span><span class="sxs-lookup"><span data-stu-id="b25d1-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, hello sixth virtual machine will be placed into hello same update domain as hello first virtual machine, hello seventh in hello same UD as hello second virtual machine, and so on.</span></span> <span data-ttu-id="b25d1-127">hello 的 hello 重新開機的順序可能不是循序的但只能有一個更新網域將會重新啟動一次。</span><span class="sxs-lookup"><span data-stu-id="b25d1-127">hello order of hello reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="b25d1-128">**訂用帳戶**-選取 hello toouse 訂用帳戶，如果您有一個以上。</span><span class="sxs-lookup"><span data-stu-id="b25d1-128">**Subscription** - select hello subscription toouse if you have more than one.</span></span>
   * <span data-ttu-id="b25d1-129">**資源群組**-選取現有的資源群組按一下 hello 箭號，選取資源群組 hello 從下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="b25d1-129">**Resource group** - select an existing resource group by clicking hello arrow and selecting a resource group from hello drop down.</span></span> <span data-ttu-id="b25d1-130">您也可以輸入名稱，來建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="b25d1-131">hello 名稱可以包含任何下列字元的 hello： 字母、 數字、 句號、 連字號、 底線和左或右括號。</span><span class="sxs-lookup"><span data-stu-id="b25d1-131">hello name can contain any of hello following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="b25d1-132">hello 名稱不能以句號結尾。</span><span class="sxs-lookup"><span data-stu-id="b25d1-132">hello name cannot end in a period.</span></span> <span data-ttu-id="b25d1-133">所有 hello 可用性群組中的 hello Vm 需要 toobe hello 中建立與 hello 可用性設定組的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-133">All of hello VMs in hello availability group need toobe created in hello same resource group as hello availability set.</span></span>
   * <span data-ttu-id="b25d1-134">**位置**-hello 下拉式清單中選取的位置。</span><span class="sxs-lookup"><span data-stu-id="b25d1-134">**Location** - select a location from hello drop-down.</span></span>
   * <span data-ttu-id="b25d1-135">**Managed** -選取*是*toocreate 受管理的可用性設定 toouse 與受管理的磁碟用於儲存體的 Vm。</span><span class="sxs-lookup"><span data-stu-id="b25d1-135">**Managed** - select *Yes* toocreate a managed availability set toouse with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="b25d1-136">選取**否**如果 hello Vm hello 集將會使用未受管理的磁碟的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="b25d1-136">Select **No** if hello VMs that will be in hello set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="b25d1-137">當您輸入 hello 資訊後時，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="b25d1-137">When you are done entering hello information, click **Create**.</span></span> 

## <a name="use-hello-portal-toocreate-a-virtual-machine-and-an-availability-set-at-hello-same-time"></a><span data-ttu-id="b25d1-138">使用虛擬機器可用性同時設定與 hello 相同的 hello 入口 toocreate 時間</span><span class="sxs-lookup"><span data-stu-id="b25d1-138">Use hello portal toocreate a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="b25d1-139">如果您要建立新的 VM 使用 hello 入口網站，您也可以建立新的可用性設定組 hello VM 時建立 hello hello 集合中的第一個 VM。</span><span class="sxs-lookup"><span data-stu-id="b25d1-139">If you are creating a new VM using hello portal, you can also create a new availability set for hello VM while you create hello first VM in hello set.</span></span> <span data-ttu-id="b25d1-140">如果您選擇 toouse 管理磁碟 vm，就會建立受管理的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-140">If you choose toouse Managed Disks for your VM, a managed availability set will be created.</span></span>

![如果螢幕擷取畫面顯示 hello 程序建立新的可用性，您建立 hello VM 時設定。](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-tooan-existing-availability-set-in-hello-portal"></a><span data-ttu-id="b25d1-142">加入新 VM tooan 現有可用性設定組中 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="b25d1-142">Add a new VM tooan existing availability set in hello portal</span></span>
<span data-ttu-id="b25d1-143">每個其他您建立針對 vm 應該屬於 hello 組，請確定您建立在 hello 相同**資源群組**，然後選取 hello 現有的可用性設定組中步驟 3。</span><span class="sxs-lookup"><span data-stu-id="b25d1-143">For each additional VM that you create that should belong in hello set, make sure that you create it in hello same **resource group** and then select hello existing availability set in Step 3.</span></span> 

![螢幕擷取畫面顯示如何 tooselect 的現有可用性設定 toouse vm。](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-toocreate-an-availability-set"></a><span data-ttu-id="b25d1-145">使用 PowerShell toocreate 可用性集</span><span class="sxs-lookup"><span data-stu-id="b25d1-145">Use PowerShell toocreate an availability set</span></span>
<span data-ttu-id="b25d1-146">這個範例會建立可用性設定組具名**myAvailabilitySet**在 hello **myResourceGroup** hello 中的資源群組**美國西部**位置。</span><span class="sxs-lookup"><span data-stu-id="b25d1-146">This example creates an availability set named **myAvailabilitySet** in hello **myResourceGroup** resource group in hello **West US** location.</span></span> <span data-ttu-id="b25d1-147">這必須完成才能建立 hello toobe hello 集將會第一個 VM。</span><span class="sxs-lookup"><span data-stu-id="b25d1-147">This needs toobe done before you create hello first VM that will be in hello set.</span></span>

<span data-ttu-id="b25d1-148">在開始之前，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="b25d1-148">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b25d1-149">執行 hello 下列命令 tooinstall 它。</span><span class="sxs-lookup"><span data-stu-id="b25d1-149">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="b25d1-150">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b25d1-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="b25d1-151">如果您將受控磁碟使用於您的 VM，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="b25d1-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="b25d1-152">如果您將自己的儲存體帳戶使用於您的 VM，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="b25d1-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="b25d1-153">如需詳細資訊，請參閱 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset)。</span><span class="sxs-lookup"><span data-stu-id="b25d1-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b25d1-154">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b25d1-154">Troubleshooting</span></span>
* <span data-ttu-id="b25d1-155">當您建立的 VM，如果您想要的 hello 可用性設定組不在 hello 入口網站中的 hello 下拉式清單中您可能建立它的不同資源群組中。</span><span class="sxs-lookup"><span data-stu-id="b25d1-155">When you create a VM, if hello availability set you want isn't in hello drop-down list in hello portal you may have created it in a different resource group.</span></span> <span data-ttu-id="b25d1-156">如果您不知道您的可用性的 hello 資源群組設定 toohello 中樞功能表中，請按一下 瀏覽 > 可用性設定組 toosee 清單，您的可用性集合，且它們隸屬於哪一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="b25d1-156">If you don't know hello resource group for your availability set, go toohello hub menu and click Browse > Availability sets toosee a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b25d1-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b25d1-157">Next steps</span></span>
<span data-ttu-id="b25d1-158">新增額外新增額外的儲存體 tooyour VM[資料磁碟](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b25d1-158">Add additional storage tooyour VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

