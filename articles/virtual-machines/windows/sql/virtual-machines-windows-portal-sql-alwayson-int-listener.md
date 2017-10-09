---
title: "Azure 虛擬機器中 SQL Server 可用性群組接聽程式 aaaCreate |Microsoft 文件"
description: "在 Azure 虛擬機器中建立 SQL Server 的 AlwaysOn 可用性群組接聽程式的逐步指示"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a><span data-ttu-id="9cf76-103">在 Azure 中設定 Always On 可用性群組的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9cf76-103">Configure a load balancer for an Always On availability group in Azure</span></span>
<span data-ttu-id="9cf76-104">這篇文章說明如何 toocreate 負載平衡器，為 SQL Server Always On 可用性群組在 Azure 虛擬機器正在使用 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="9cf76-104">This article explains how toocreate a load balancer for a SQL Server Always On availability group in Azure virtual machines that are running with Azure Resource Manager.</span></span> <span data-ttu-id="9cf76-105">Hello SQL Server 執行個體位於 Azure 虛擬機器時，可用性群組需要負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-105">An availability group requires a load balancer when hello SQL Server instances are on Azure virtual machines.</span></span> <span data-ttu-id="9cf76-106">hello 負載平衡器會儲存 hello hello 可用性群組接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-106">hello load balancer stores hello IP address for hello availability group listener.</span></span> <span data-ttu-id="9cf76-107">如果可用性群組跨越多個區域，則每個區域都需要負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-107">If an availability group spans multiple regions, each region needs a load balancer.</span></span>

<span data-ttu-id="9cf76-108">toocomplete 這個工作中，您需要的 toohave 正在使用資源管理員的 Azure 虛擬機器部署 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-108">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines that are running with Resource Manager.</span></span> <span data-ttu-id="9cf76-109">這兩個 SQL Server 虛擬機器必須屬於 toohello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-109">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="9cf76-110">您可以使用 hello [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)tooautomatically 建立 hello 可用性群組資源管理員 中。</span><span class="sxs-lookup"><span data-stu-id="9cf76-110">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Resource Manager.</span></span> <span data-ttu-id="9cf76-111">此範本會自動為您建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-111">This template automatically creates an internal load balancer for you.</span></span> 

<span data-ttu-id="9cf76-112">如果您想要的話，也可以 [手動設定可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-112">If you prefer, you can [manually configure an availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="9cf76-113">本文會要求您已經設定可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-113">This article requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="9cf76-114">相關主題包括：</span><span class="sxs-lookup"><span data-stu-id="9cf76-114">Related topics include:</span></span>

* [<span data-ttu-id="9cf76-115">在 Azure VM (GUI) 中設定 Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="9cf76-115">Configure Always On availability groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="9cf76-116">使用 Azure Resource Manager 和 PowerShell 來設定 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="9cf76-116">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

<span data-ttu-id="9cf76-117">藉由查核透過這份文件，來建立，並在 hello Azure 入口網站中設定負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-117">By walking through this article, you create and configure a load balancer in hello Azure portal.</span></span> <span data-ttu-id="9cf76-118">Hello 程序完成之後，您會設定 hello 叢集 toouse hello IP 位址從 hello hello 可用性群組接聽程式的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-118">After hello process is complete, you configure hello cluster toouse hello IP address from hello load balancer for hello availability group listener.</span></span>

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="9cf76-119">建立及設定 hello Azure 入口網站中的 hello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9cf76-119">Create and configure hello load balancer in hello Azure portal</span></span>
<span data-ttu-id="9cf76-120">在這個部分 hello 工作中，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9cf76-120">In this portion of hello task, do hello following:</span></span>

1. <span data-ttu-id="9cf76-121">在 hello Azure 入口網站，建立 hello 負載平衡器並設定 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-121">In hello Azure portal, create hello load balancer and configure hello IP address.</span></span>
2. <span data-ttu-id="9cf76-122">設定 hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-122">Configure hello back-end pool.</span></span>
3. <span data-ttu-id="9cf76-123">建立 hello 探查。</span><span class="sxs-lookup"><span data-stu-id="9cf76-123">Create hello probe.</span></span> 
4. <span data-ttu-id="9cf76-124">設定 hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-124">Set hello load balancing rules.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf76-125">如果在多個資源群組和地區 hello SQL Server 執行個體，執行每個步驟兩次，一次每個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="9cf76-125">If hello SQL Server instances are in multiple resource groups and regions, perform each step twice, once in each resource group.</span></span>
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a><span data-ttu-id="9cf76-126">步驟 1： 建立 hello 負載平衡器並設定 hello IP 位址</span><span class="sxs-lookup"><span data-stu-id="9cf76-126">Step 1: Create hello load balancer and configure hello IP address</span></span>
<span data-ttu-id="9cf76-127">首先，建立 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-127">First, create hello load balancer.</span></span> 

1. <span data-ttu-id="9cf76-128">在 hello Azure 入口網站，開啟 hello 資源群組含有 hello SQL Server 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-128">In hello Azure portal, open hello resource group that contains hello SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="9cf76-129">在 hello 資源群組中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-129">In hello resource group, click **Add**.</span></span>

3. <span data-ttu-id="9cf76-130">搜尋**負載平衡器**，然後在 hello 搜尋結果中，選取**負載平衡器**，這由發佈**Microsoft**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-130">Search for **load balancer** and then, in hello search results, select **Load Balancer**, which is published by **Microsoft**.</span></span>

4. <span data-ttu-id="9cf76-131">在 hello**負載平衡器**刀鋒視窗中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-131">On hello **Load Balancer** blade, click **Create**.</span></span>

5. <span data-ttu-id="9cf76-132">在 hello**建立負載平衡器**對話方塊方塊中，hello 負載平衡器設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9cf76-132">In hello **Create load balancer** dialog box, configure hello load balancer as follows:</span></span>

   | <span data-ttu-id="9cf76-133">設定</span><span class="sxs-lookup"><span data-stu-id="9cf76-133">Setting</span></span> | <span data-ttu-id="9cf76-134">值</span><span class="sxs-lookup"><span data-stu-id="9cf76-134">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="9cf76-135">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9cf76-135">**Name**</span></span> |<span data-ttu-id="9cf76-136">文字名稱，代表 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-136">A text name representing hello load balancer.</span></span> <span data-ttu-id="9cf76-137">例如 **sqlLB**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-137">For example, **sqlLB**.</span></span> |
   | <span data-ttu-id="9cf76-138">**類型**</span><span class="sxs-lookup"><span data-stu-id="9cf76-138">**Type**</span></span> |<span data-ttu-id="9cf76-139">**內部**： 大部分的實作會使用內部負載平衡器，可讓應用程式內 hello 相同虛擬網路 tooconnect toohello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-139">**Internal**: Most implementations use an internal load balancer, which allows applications within hello same virtual network tooconnect toohello availability group.</span></span>  </br> <span data-ttu-id="9cf76-140">**外部**： 允許應用程式 tooconnect toohello 透過公用網際網路連線的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-140">**External**: Allows applications tooconnect toohello availability group through a public Internet connection.</span></span> |
   | <span data-ttu-id="9cf76-141">**虛擬網路**</span><span class="sxs-lookup"><span data-stu-id="9cf76-141">**Virtual network**</span></span> |<span data-ttu-id="9cf76-142">選取 hello hello SQL Server 則會在中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9cf76-142">Select hello virtual network that hello SQL Server intances are in.</span></span> |
   | <span data-ttu-id="9cf76-143">**子網路**</span><span class="sxs-lookup"><span data-stu-id="9cf76-143">**Subnet**</span></span> |<span data-ttu-id="9cf76-144">選取 hello SQL Server 執行個體位在的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="9cf76-144">Select hello subnet that hello SQL Server instances are in.</span></span> |
   | <span data-ttu-id="9cf76-145">**IP 位址指派**</span><span class="sxs-lookup"><span data-stu-id="9cf76-145">**IP address assignment**</span></span> |<span data-ttu-id="9cf76-146">**靜態**</span><span class="sxs-lookup"><span data-stu-id="9cf76-146">**Static**</span></span> |
   | <span data-ttu-id="9cf76-147">**私人 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="9cf76-147">**Private IP address**</span></span> |<span data-ttu-id="9cf76-148">指定可用的 IP 位址從 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="9cf76-148">Specify an available IP address from hello subnet.</span></span> <span data-ttu-id="9cf76-149">當您建立 hello 叢集上的接聽程式時，請使用此 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-149">Use this IP address when you create a listener on hello cluster.</span></span> <span data-ttu-id="9cf76-150">在 PowerShell 指令碼，在本文中稍後使用這個位址 hello`$ILBIP`變數。</span><span class="sxs-lookup"><span data-stu-id="9cf76-150">In a PowerShell script, later in this article, use this address for hello `$ILBIP` variable.</span></span> |
   | <span data-ttu-id="9cf76-151">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="9cf76-151">**Subscription**</span></span> |<span data-ttu-id="9cf76-152">如果您有多個訂用帳戶，此欄位才會出現。</span><span class="sxs-lookup"><span data-stu-id="9cf76-152">If you have multiple subscriptions, this field might appear.</span></span> <span data-ttu-id="9cf76-153">選取您想要與此資源 tooassociate hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9cf76-153">Select hello subscription that you want tooassociate with this resource.</span></span> <span data-ttu-id="9cf76-154">它通常是 hello 相同訂用帳戶的 hello 可用性群組的所有都 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="9cf76-154">It is normally hello same subscription as all hello resources for hello availability group.</span></span> |
   | <span data-ttu-id="9cf76-155">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="9cf76-155">**Resource group**</span></span> |<span data-ttu-id="9cf76-156">選取 hello 資源群組中的 hello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cf76-156">Select hello resource group that hello SQL Server instances are in.</span></span> |
   | <span data-ttu-id="9cf76-157">**位置**</span><span class="sxs-lookup"><span data-stu-id="9cf76-157">**Location**</span></span> |<span data-ttu-id="9cf76-158">選取 hello Azure hello SQL Server 執行個體位在的位置。</span><span class="sxs-lookup"><span data-stu-id="9cf76-158">Select hello Azure location that hello SQL Server instances are in.</span></span> |

6. <span data-ttu-id="9cf76-159">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9cf76-159">Click **Create**.</span></span> 

<span data-ttu-id="9cf76-160">Azure 會建立 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-160">Azure creates hello load balancer.</span></span> <span data-ttu-id="9cf76-161">hello 負載平衡器所屬 tooa 特定網路、 子網路、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="9cf76-161">hello load balancer belongs tooa specific network, subnet, resource group, and location.</span></span> <span data-ttu-id="9cf76-162">Azure 完成 hello 工作之後，請確認在 Azure 中的 hello 負載平衡器設定。</span><span class="sxs-lookup"><span data-stu-id="9cf76-162">After Azure completes hello task, verify hello load balancer settings in Azure.</span></span> 

### <a name="step-2-configure-hello-back-end-pool"></a><span data-ttu-id="9cf76-163">步驟 2： 設定 hello 後端集區</span><span class="sxs-lookup"><span data-stu-id="9cf76-163">Step 2: Configure hello back-end pool</span></span>
<span data-ttu-id="9cf76-164">Azure 會呼叫 hello 後端位址集區*後端集區*。</span><span class="sxs-lookup"><span data-stu-id="9cf76-164">Azure calls hello back-end address pool *backend pool*.</span></span> <span data-ttu-id="9cf76-165">在此情況下，hello 後端集區是 hello 兩個 SQL Server 執行個體可用性群組中的 hello 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-165">In this case, hello back-end pool is hello addresses of hello two SQL Server instances in your availability group.</span></span> 

1. <span data-ttu-id="9cf76-166">在資源群組中，按一下您所建立的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-166">In your resource group, click hello load balancer that you created.</span></span> 

2. <span data-ttu-id="9cf76-167">在 [設定] 上，按一下 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="9cf76-167">On **Settings**, click **Backend pools**.</span></span>

3. <span data-ttu-id="9cf76-168">在**後端集區**，按一下 **新增**toocreate 的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-168">On **Backend pools**, click **Add** toocreate a back-end address pool.</span></span> 

4. <span data-ttu-id="9cf76-169">在**新增後端集區**下**名稱**，輸入 hello 後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf76-169">On **Add backend pool**, under **Name**, type a name for hello back-end pool.</span></span>

5. <span data-ttu-id="9cf76-170">在 [虛擬機器] 之下，按一下 [新增虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="9cf76-170">Under **Virtual machines**, click **Add a virtual machine**.</span></span> 

6. <span data-ttu-id="9cf76-171">在下**選擇虛擬機器**，按一下 **選擇可用性設定組**，然後指定 hello 可用性設定組 hello SQL Server 虛擬機器屬於。</span><span class="sxs-lookup"><span data-stu-id="9cf76-171">Under **Choose virtual machines**, click **Choose an availability set**, and then specify hello availability set that hello SQL Server virtual machines belong to.</span></span>

7. <span data-ttu-id="9cf76-172">您已選擇 hello 可用性設定組之後，請按一下**選擇 hello 虛擬機器**，選取 hello 兩部虛擬機器的主控件 hello hello 可用性群組中的 SQL Server 執行個體，然後按一下**選取**.</span><span class="sxs-lookup"><span data-stu-id="9cf76-172">After you have chosen hello availability set, click **Choose hello virtual machines**, select hello two virtual machines that host hello SQL Server instances in hello availability group, and then click **Select**.</span></span> 

8. <span data-ttu-id="9cf76-173">按一下**確定**tooclose hello 刀鋒視窗的**選擇虛擬機器**，和**新增後端集區**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-173">Click **OK** tooclose hello blades for **Choose virtual machines**, and **Add backend pool**.</span></span> 

<span data-ttu-id="9cf76-174">Azure 會更新 hello hello 後端位址集區設定。</span><span class="sxs-lookup"><span data-stu-id="9cf76-174">Azure updates hello settings for hello back-end address pool.</span></span> <span data-ttu-id="9cf76-175">您的可用性設定組現在有包含兩個 SQL Server 執行個體的集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-175">Now your availability set has a pool of two SQL Server instances.</span></span>

### <a name="step-3-create-a-probe"></a><span data-ttu-id="9cf76-176">步驟 3：建立探查</span><span class="sxs-lookup"><span data-stu-id="9cf76-176">Step 3: Create a probe</span></span>
<span data-ttu-id="9cf76-177">hello 探查定義 Azure 如何驗證哪些 hello SQL Server 執行個體目前擁有 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-177">hello probe defines how Azure verifies which of hello SQL Server instances currently owns hello availability group listener.</span></span> <span data-ttu-id="9cf76-178">Azure 探查 hello 服務根據 hello 建立 hello 探查時，您所定義的連接埠上的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-178">Azure probes hello service based on hello IP address on a port that you define when you create hello probe.</span></span>

1. <span data-ttu-id="9cf76-179">在 hello 負載平衡器**設定**刀鋒視窗中，按一下 **健全狀況探查**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-179">On hello load balancer **Settings** blade, click **Health probes**.</span></span> 

2. <span data-ttu-id="9cf76-180">在 hello**健全狀況探查**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-180">On hello **Health probes** blade, click **Add**.</span></span>

3. <span data-ttu-id="9cf76-181">Hello 上設定 hello 探查**新增探查**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9cf76-181">Configure hello probe on hello **Add probe** blade.</span></span> <span data-ttu-id="9cf76-182">使用下列值 tooconfigure hello 探查的 hello:</span><span class="sxs-lookup"><span data-stu-id="9cf76-182">Use hello following values tooconfigure hello probe:</span></span>

   | <span data-ttu-id="9cf76-183">設定</span><span class="sxs-lookup"><span data-stu-id="9cf76-183">Setting</span></span> | <span data-ttu-id="9cf76-184">值</span><span class="sxs-lookup"><span data-stu-id="9cf76-184">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="9cf76-185">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9cf76-185">**Name**</span></span> |<span data-ttu-id="9cf76-186">代表 hello 探查文字名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf76-186">A text name representing hello probe.</span></span> <span data-ttu-id="9cf76-187">例如 **SQLAlwaysOnEndPointProbe**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-187">For example, **SQLAlwaysOnEndPointProbe**.</span></span> |
   | <span data-ttu-id="9cf76-188">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="9cf76-188">**Protocol**</span></span> |<span data-ttu-id="9cf76-189">**TCP**</span><span class="sxs-lookup"><span data-stu-id="9cf76-189">**TCP**</span></span> |
   | <span data-ttu-id="9cf76-190">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-190">**Port**</span></span> |<span data-ttu-id="9cf76-191">您可以使用任何可用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="9cf76-191">You can use any available port.</span></span> <span data-ttu-id="9cf76-192">例如 *59999*。</span><span class="sxs-lookup"><span data-stu-id="9cf76-192">For example, *59999*.</span></span> |
   | <span data-ttu-id="9cf76-193">**間隔**</span><span class="sxs-lookup"><span data-stu-id="9cf76-193">**Interval**</span></span> |<span data-ttu-id="9cf76-194">*5*</span><span class="sxs-lookup"><span data-stu-id="9cf76-194">*5*</span></span> |
   | <span data-ttu-id="9cf76-195">**狀況不良臨界值**</span><span class="sxs-lookup"><span data-stu-id="9cf76-195">**Unhealthy threshold**</span></span> |<span data-ttu-id="9cf76-196">*2*</span><span class="sxs-lookup"><span data-stu-id="9cf76-196">*2*</span></span> |

4.  <span data-ttu-id="9cf76-197">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9cf76-197">Click **OK**.</span></span> 

> [!NOTE]
> <span data-ttu-id="9cf76-198">請確定您指定的 hello 通訊埠的兩個 SQL Server 執行個體的 hello 防火牆上開啟。</span><span class="sxs-lookup"><span data-stu-id="9cf76-198">Make sure that hello port you specify is open on hello firewall of both SQL Server instances.</span></span> <span data-ttu-id="9cf76-199">兩個執行個體需要 hello 您使用的 TCP 連接埠的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-199">Both instances require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="9cf76-200">如需詳細資訊，請參閱[新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-200">For more information, see [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx).</span></span> 
> 
> 

<span data-ttu-id="9cf76-201">Azure 會建立 hello 探查，然後再使用它 tootest 哪一個 SQL Server 執行個體具有 hello hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-201">Azure creates hello probe and then uses it tootest which SQL Server instance has hello listener for hello availability group.</span></span>

### <a name="step-4-set-hello-load-balancing-rules"></a><span data-ttu-id="9cf76-202">步驟 4： 設定 hello 負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="9cf76-202">Step 4: Set hello load balancing rules</span></span>
<span data-ttu-id="9cf76-203">hello 負載平衡規則設定 hello 負載平衡器將流量 toohello SQL Server 執行個體的路由。</span><span class="sxs-lookup"><span data-stu-id="9cf76-203">hello load balancing rules configure how hello load balancer routes traffic toohello SQL Server instances.</span></span> <span data-ttu-id="9cf76-204">此負載平衡器，您會啟用伺服器直接回傳，因為只有其中一個 hello 兩個 SQL Server 執行個體擁有 hello 可用性群組接聽程式資源一次。</span><span class="sxs-lookup"><span data-stu-id="9cf76-204">For this load balancer, you enable direct server return because only one of hello two SQL Server instances owns hello availability group listener resource at a time.</span></span>

1. <span data-ttu-id="9cf76-205">在 hello 負載平衡器**設定**刀鋒視窗中，按一下 **負載平衡規則**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-205">On hello load balancer **Settings** blade, click **Load balancing rules**.</span></span> 

2. <span data-ttu-id="9cf76-206">在 hello**負載平衡規則**刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-206">On hello **Load balancing rules** blade, click **Add**.</span></span>

3. <span data-ttu-id="9cf76-207">在 hello**新增負載平衡規則**刀鋒視窗中，設定 hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-207">On hello **Add load balancing rules** blade, configure hello load balancing rule.</span></span> <span data-ttu-id="9cf76-208">使用下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="9cf76-208">Use hello following settings:</span></span> 

   | <span data-ttu-id="9cf76-209">設定</span><span class="sxs-lookup"><span data-stu-id="9cf76-209">Setting</span></span> | <span data-ttu-id="9cf76-210">值</span><span class="sxs-lookup"><span data-stu-id="9cf76-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="9cf76-211">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9cf76-211">**Name**</span></span> |<span data-ttu-id="9cf76-212">文字名稱，代表 hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-212">A text name representing hello load balancing rules.</span></span> <span data-ttu-id="9cf76-213">例如 **SQLAlwaysOnEndPointListener**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-213">For example, **SQLAlwaysOnEndPointListener**.</span></span> |
   | <span data-ttu-id="9cf76-214">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="9cf76-214">**Protocol**</span></span> |<span data-ttu-id="9cf76-215">**TCP**</span><span class="sxs-lookup"><span data-stu-id="9cf76-215">**TCP**</span></span> |
   | <span data-ttu-id="9cf76-216">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-216">**Port**</span></span> |<span data-ttu-id="9cf76-217">*1433*</span><span class="sxs-lookup"><span data-stu-id="9cf76-217">*1433*</span></span> |
   | <span data-ttu-id="9cf76-218">**後端連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-218">**Backend Port**</span></span> |<span data-ttu-id="9cf76-219">*1433*.系統會忽略此值，因為此規則使用 [浮動 IP (伺服器直接回傳)]。</span><span class="sxs-lookup"><span data-stu-id="9cf76-219">*1433*. This value is ignored because this rule uses **Floating IP (direct server return)**.</span></span> |
   | <span data-ttu-id="9cf76-220">**探查**</span><span class="sxs-lookup"><span data-stu-id="9cf76-220">**Probe**</span></span> |<span data-ttu-id="9cf76-221">此負載平衡器使用您所建立的 hello 探查 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf76-221">Use hello name of hello probe that you created for this load balancer.</span></span> |
   | <span data-ttu-id="9cf76-222">**工作階段持續性**</span><span class="sxs-lookup"><span data-stu-id="9cf76-222">**Session persistence**</span></span> |<span data-ttu-id="9cf76-223">**None**</span><span class="sxs-lookup"><span data-stu-id="9cf76-223">**None**</span></span> |
   | <span data-ttu-id="9cf76-224">**閒置逾時 (分鐘)**</span><span class="sxs-lookup"><span data-stu-id="9cf76-224">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="9cf76-225">*4*</span><span class="sxs-lookup"><span data-stu-id="9cf76-225">*4*</span></span> |
   | <span data-ttu-id="9cf76-226">**浮動 IP (伺服器直接回傳)**</span><span class="sxs-lookup"><span data-stu-id="9cf76-226">**Floating IP (direct server return)**</span></span> |<span data-ttu-id="9cf76-227">**已啟用**</span><span class="sxs-lookup"><span data-stu-id="9cf76-227">**Enabled**</span></span> |

   > [!NOTE]
   > <span data-ttu-id="9cf76-228">您可能必須關閉 hello 刀鋒視窗 tooview tooscroll hello 的所有設定。</span><span class="sxs-lookup"><span data-stu-id="9cf76-228">You might have tooscroll down hello blade tooview all hello settings.</span></span>
   > 

4. <span data-ttu-id="9cf76-229">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9cf76-229">Click **OK**.</span></span> 
5. <span data-ttu-id="9cf76-230">Azure 會設定 hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-230">Azure configures hello load balancing rule.</span></span> <span data-ttu-id="9cf76-231">現在 hello 負載平衡器設定的 tooroute 流量 toohello SQL Server 執行個體裝載 hello hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-231">Now hello load balancer is configured tooroute traffic toohello SQL Server instance that hosts hello listener for hello availability group.</span></span> 

<span data-ttu-id="9cf76-232">此時，hello 資源群組已連接 tooboth SQL Server 電腦的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-232">At this point, hello resource group has a load balancer that connects tooboth SQL Server machines.</span></span> <span data-ttu-id="9cf76-233">hello 負載平衡器也包含 hello SQL Server Always On 可用性群組接聽程式，IP 位址，讓電腦可以回應 toorequests hello 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-233">hello load balancer also contains an IP address for hello SQL Server Always On availability group listener, so that either machine can respond toorequests for hello availability groups.</span></span>

> [!NOTE]
> <span data-ttu-id="9cf76-234">如果您的 SQL Server 執行個體中兩個不同的區域，請重複 hello hello 步驟其他區域。</span><span class="sxs-lookup"><span data-stu-id="9cf76-234">If your SQL Server instances are in two separate regions, repeat hello steps in hello other region.</span></span> <span data-ttu-id="9cf76-235">每個區域都需要負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-235">Each region requires a load balancer.</span></span> 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a><span data-ttu-id="9cf76-236">設定 hello 叢集 toouse hello 負載平衡器 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9cf76-236">Configure hello cluster toouse hello load balancer IP address</span></span>
<span data-ttu-id="9cf76-237">hello 下一個步驟是在 hello 叢集 tooconfigure hello 接聽程式，並讓 hello 接聽程式連線。</span><span class="sxs-lookup"><span data-stu-id="9cf76-237">hello next step is tooconfigure hello listener on hello cluster, and bring hello listener online.</span></span> <span data-ttu-id="9cf76-238">請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9cf76-238">Do hello following:</span></span> 

1. <span data-ttu-id="9cf76-239">Hello 容錯移轉叢集上建立 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-239">Create hello availability group listener on hello failover cluster.</span></span> 

2. <span data-ttu-id="9cf76-240">顯示 hello 接聽程式連線。</span><span class="sxs-lookup"><span data-stu-id="9cf76-240">Bring hello listener online.</span></span>

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a><span data-ttu-id="9cf76-241">步驟 5: Hello 容錯移轉叢集上建立 hello 可用性群組接聽程式</span><span class="sxs-lookup"><span data-stu-id="9cf76-241">Step 5: Create hello availability group listener on hello failover cluster</span></span>
<span data-ttu-id="9cf76-242">在此步驟中，您可以手動建立容錯移轉叢集管理員和 SQL Server Management Studio 中的 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-242">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a><span data-ttu-id="9cf76-243">確認 hello hello 接聽程式組態</span><span class="sxs-lookup"><span data-stu-id="9cf76-243">Verify hello configuration of hello listener</span></span>

<span data-ttu-id="9cf76-244">如果正確設定 hello 叢集資源和相依性，您應該在 SQL Server Management Studio 無法 tooview hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-244">If hello cluster resources and dependencies are correctly configured, you should be able tooview hello listener in SQL Server Management Studio.</span></span> <span data-ttu-id="9cf76-245">tooset hello 接聽程式通訊埠，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="9cf76-245">tooset hello listener port, do hello following:</span></span>

1. <span data-ttu-id="9cf76-246">啟動 SQL Server Management Studio，然後連接 toohello 主要複本。</span><span class="sxs-lookup"><span data-stu-id="9cf76-246">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

2. <span data-ttu-id="9cf76-247">跳過**AlwaysOn 高可用性** > **可用性群組** > **可用性群組接聽程式**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-247">Go too**AlwaysOn High Availability** > **Availability Groups** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="9cf76-248">您現在應該會看到您在建立容錯移轉叢集管理員 中的 hello 接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf76-248">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> 

3. <span data-ttu-id="9cf76-249">Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-249">Right-click hello listener name, and then click **Properties**.</span></span>

4. <span data-ttu-id="9cf76-250">在 hello**連接埠**方塊中，使用 hello $EndpointPort 您稍早所指定 hello hello 可用性群組接聽程式的連接埠號碼 （1433年是 hello 預設值），然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-250">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), and then click **OK**.</span></span>

<span data-ttu-id="9cf76-251">現在，您在以 Resource Manager 模式執行的 Azure 虛擬機器中，已有一個可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9cf76-251">You now have an availability group in Azure virtual machines running in Resource Manager mode.</span></span> 

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="9cf76-252">測試 hello 連接 toohello 接聽程式</span><span class="sxs-lookup"><span data-stu-id="9cf76-252">Test hello connection toohello listener</span></span>
<span data-ttu-id="9cf76-253">藉由 hello 下列測試 hello 連接：</span><span class="sxs-lookup"><span data-stu-id="9cf76-253">Test hello connection by doing hello following:</span></span>

1. <span data-ttu-id="9cf76-254">RDP tooa SQL Server 執行個體處於 hello 相同虛擬網路，但不會無法自己 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="9cf76-254">RDP tooa SQL Server instance that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="9cf76-255">此伺服器可以 hello hello 叢集中的其他 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cf76-255">This server can be hello other SQL Server instance in hello cluster.</span></span>

2. <span data-ttu-id="9cf76-256">使用**sqlcmd**公用程式 tootest hello 連線。</span><span class="sxs-lookup"><span data-stu-id="9cf76-256">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="9cf76-257">例如，下列指令碼的 hello 建立**sqlcmd**透過 hello 接聽程式使用 Windows 驗證連接 toohello 主要複本：</span><span class="sxs-lookup"><span data-stu-id="9cf76-257">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
        sqlcmd -S <listenerName> -E

<span data-ttu-id="9cf76-258">hello SQLCMD 連線自動連接到裝載主要複本的 hello toohello SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9cf76-258">hello SQLCMD connection automatically connects toohello SQL Server instance that hosts hello primary replica.</span></span> 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a><span data-ttu-id="9cf76-259">建立其他可用性群組的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9cf76-259">Create an IP address for an additional availability group</span></span>

<span data-ttu-id="9cf76-260">每個可用性群組都會使用個別的接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-260">Each availability group uses a separate listener.</span></span> <span data-ttu-id="9cf76-261">每個接聽程式有其自己的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-261">Each listener has its own IP address.</span></span> <span data-ttu-id="9cf76-262">使用 hello 相同額外的接聽程式的負載平衡器 toohold hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-262">Use hello same load balancer toohold hello IP address for additional listeners.</span></span> <span data-ttu-id="9cf76-263">建立可用性群組之後，新增 hello IP 位址 toohello 負載平衡器，然後再設定 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-263">After you create an availability group, add hello IP address toohello load balancer, and then configure hello listener.</span></span>

<span data-ttu-id="9cf76-264">tooadd IP 位址 tooa 負載平衡器以 hello Azure 入口網站，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9cf76-264">tooadd an IP address tooa load balancer with hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="9cf76-265">在 hello Azure 入口網站，開啟包含 hello 負載平衡器的 hello 資源群組，然後按一下 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9cf76-265">In hello Azure portal, open hello resource group that contains hello load balancer, and then click hello load balancer.</span></span> 

2. <span data-ttu-id="9cf76-266">在 設定 下按一下 前端 IP 集區，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="9cf76-266">Under **SETTINGS**, click **Frontend IP pool**, and then click **Add**.</span></span> 

3. <span data-ttu-id="9cf76-267">在下**新增前端 IP 位址**，指派 hello 前端的名稱。</span><span class="sxs-lookup"><span data-stu-id="9cf76-267">Under **Add frontend IP address**, assign a name for hello front end.</span></span> 

4. <span data-ttu-id="9cf76-268">請確認該 hello**虛擬網路**和 hello**子網路**hello 與 hello SQL Server 執行個體相同。</span><span class="sxs-lookup"><span data-stu-id="9cf76-268">Verify that hello **Virtual network** and hello **Subnet** are hello same as hello SQL Server instances.</span></span>

5. <span data-ttu-id="9cf76-269">Hello hello 接聽程式的 IP 位址設定。</span><span class="sxs-lookup"><span data-stu-id="9cf76-269">Set hello IP address for hello listener.</span></span> 
   
   >[!TIP]
   ><span data-ttu-id="9cf76-270">您可以設定 hello IP 位址 toostatic，然後輸入 hello 子網路中的目前未使用的位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-270">You can set hello IP address toostatic and type an address that is not currently used in hello subnet.</span></span> <span data-ttu-id="9cf76-271">或者，您可以設定 hello IP 位址 toodynamic，並儲存 hello 前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-271">Alternatively, you can set hello IP address toodynamic and save hello new front-end IP pool.</span></span> <span data-ttu-id="9cf76-272">當您這樣做時，hello Azure 入口網站會自動指派的可用 IP 位址 toohello 集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-272">When you do so, hello Azure portal automatically assigns an available IP address toohello pool.</span></span> <span data-ttu-id="9cf76-273">然後，您可以重新開啟 hello 前端 IP 集區，並變更 hello 分派 toostatic。</span><span class="sxs-lookup"><span data-stu-id="9cf76-273">You can then reopen hello front-end IP pool and change hello assignment toostatic.</span></span> 

6. <span data-ttu-id="9cf76-274">儲存 hello hello 接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-274">Save hello IP address for hello listener.</span></span> 

7. <span data-ttu-id="9cf76-275">使用下列設定的 hello 新增健全狀況探查：</span><span class="sxs-lookup"><span data-stu-id="9cf76-275">Add a health probe by using hello following settings:</span></span>

   |<span data-ttu-id="9cf76-276">設定</span><span class="sxs-lookup"><span data-stu-id="9cf76-276">Setting</span></span> |<span data-ttu-id="9cf76-277">值</span><span class="sxs-lookup"><span data-stu-id="9cf76-277">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="9cf76-278">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9cf76-278">**Name**</span></span> |<span data-ttu-id="9cf76-279">名稱 tooidentify hello 探查。</span><span class="sxs-lookup"><span data-stu-id="9cf76-279">A name tooidentify hello probe.</span></span>
   |<span data-ttu-id="9cf76-280">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="9cf76-280">**Protocol**</span></span> |<span data-ttu-id="9cf76-281">TCP</span><span class="sxs-lookup"><span data-stu-id="9cf76-281">TCP</span></span>
   |<span data-ttu-id="9cf76-282">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-282">**Port**</span></span> |<span data-ttu-id="9cf76-283">未使用的 TCP 通訊埠，其必須可在所有虛擬機器上使用。</span><span class="sxs-lookup"><span data-stu-id="9cf76-283">An unused TCP port, which must be available on all virtual machines.</span></span> <span data-ttu-id="9cf76-284">不能用於其他用途。</span><span class="sxs-lookup"><span data-stu-id="9cf76-284">It cannot be used for any other purpose.</span></span> <span data-ttu-id="9cf76-285">沒有兩個接聽程式可以使用 hello 相同探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="9cf76-285">No two listeners can use hello same probe port.</span></span> 
   |<span data-ttu-id="9cf76-286">**間隔**</span><span class="sxs-lookup"><span data-stu-id="9cf76-286">**Interval**</span></span> |<span data-ttu-id="9cf76-287">嘗試 hello 探查之間的時間量。</span><span class="sxs-lookup"><span data-stu-id="9cf76-287">hello amount of time between probe attempts.</span></span> <span data-ttu-id="9cf76-288">使用 hello 預設 (5)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-288">Use hello default (5).</span></span>
   |<span data-ttu-id="9cf76-289">**狀況不良臨界值**</span><span class="sxs-lookup"><span data-stu-id="9cf76-289">**Unhealthy threshold**</span></span> |<span data-ttu-id="9cf76-290">hello 應該會失敗，虛擬機器會被視為狀況不良之前的連續臨界值數目。</span><span class="sxs-lookup"><span data-stu-id="9cf76-290">hello number of consecutive thresholds that should fail before a virtual machine is considered unhealthy.</span></span>

8. <span data-ttu-id="9cf76-291">按一下**確定**toosave hello 探查。</span><span class="sxs-lookup"><span data-stu-id="9cf76-291">Click **OK** toosave hello probe.</span></span> 

9. <span data-ttu-id="9cf76-292">建立負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-292">Create a load balancing rule.</span></span> <span data-ttu-id="9cf76-293">按一下 負載平衡規則，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="9cf76-293">Click **Load balancing rules**, and then click **Add**.</span></span>

10. <span data-ttu-id="9cf76-294">設定 hello 新負載平衡規則使用 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="9cf76-294">Configure hello new load balancing rule by using hello following settings:</span></span>

   |<span data-ttu-id="9cf76-295">設定</span><span class="sxs-lookup"><span data-stu-id="9cf76-295">Setting</span></span> |<span data-ttu-id="9cf76-296">值</span><span class="sxs-lookup"><span data-stu-id="9cf76-296">Value</span></span>
   |:-----|:----
   |<span data-ttu-id="9cf76-297">**名稱**</span><span class="sxs-lookup"><span data-stu-id="9cf76-297">**Name**</span></span> |<span data-ttu-id="9cf76-298">名稱 tooidentify hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="9cf76-298">A name tooidentify hello load balancing rule.</span></span> 
   |<span data-ttu-id="9cf76-299">**前端 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="9cf76-299">**Frontend IP address**</span></span> |<span data-ttu-id="9cf76-300">選取您建立 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-300">Select hello IP address you created.</span></span> 
   |<span data-ttu-id="9cf76-301">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="9cf76-301">**Protocol**</span></span> |<span data-ttu-id="9cf76-302">TCP</span><span class="sxs-lookup"><span data-stu-id="9cf76-302">TCP</span></span>
   |<span data-ttu-id="9cf76-303">**連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-303">**Port**</span></span> |<span data-ttu-id="9cf76-304">使用 hello hello SQL Server 執行個體正在使用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="9cf76-304">Use hello port that hello SQL Server instances are using.</span></span> <span data-ttu-id="9cf76-305">預設的執行個體會使用連接埠 1433，除非您有進行變更。</span><span class="sxs-lookup"><span data-stu-id="9cf76-305">A default instance uses port 1433, unless you changed it.</span></span> 
   |<span data-ttu-id="9cf76-306">**後端連接埠**</span><span class="sxs-lookup"><span data-stu-id="9cf76-306">**Backend port**</span></span> |<span data-ttu-id="9cf76-307">相同的值做為使用 hello**連接埠**。</span><span class="sxs-lookup"><span data-stu-id="9cf76-307">Use hello same value as **Port**.</span></span>
   |<span data-ttu-id="9cf76-308">**後端集區**</span><span class="sxs-lookup"><span data-stu-id="9cf76-308">**Backend pool**</span></span> |<span data-ttu-id="9cf76-309">hello 包含 hello hello SQL Server 執行個體的虛擬機器的集區。</span><span class="sxs-lookup"><span data-stu-id="9cf76-309">hello pool that contains hello virtual machines with hello SQL Server instances.</span></span> 
   |<span data-ttu-id="9cf76-310">**健康狀態探查**</span><span class="sxs-lookup"><span data-stu-id="9cf76-310">**Health probe**</span></span> |<span data-ttu-id="9cf76-311">選擇您所建立的 hello 探查。</span><span class="sxs-lookup"><span data-stu-id="9cf76-311">Choose hello probe you created.</span></span>
   |<span data-ttu-id="9cf76-312">**工作階段持續性**</span><span class="sxs-lookup"><span data-stu-id="9cf76-312">**Session persistence**</span></span> |<span data-ttu-id="9cf76-313">None</span><span class="sxs-lookup"><span data-stu-id="9cf76-313">None</span></span>
   |<span data-ttu-id="9cf76-314">**閒置逾時 (分鐘)**</span><span class="sxs-lookup"><span data-stu-id="9cf76-314">**Idle timeout (minutes)**</span></span> |<span data-ttu-id="9cf76-315">預設值 (4)</span><span class="sxs-lookup"><span data-stu-id="9cf76-315">Default (4)</span></span>
   |<span data-ttu-id="9cf76-316">**浮動 IP (伺服器直接回傳)**</span><span class="sxs-lookup"><span data-stu-id="9cf76-316">**Floating IP (direct server return)**</span></span> | <span data-ttu-id="9cf76-317">已啟用</span><span class="sxs-lookup"><span data-stu-id="9cf76-317">Enabled</span></span>

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a><span data-ttu-id="9cf76-318">設定 hello 可用性群組 toouse hello 新 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9cf76-318">Configure hello availability group toouse hello new IP address</span></span>

<span data-ttu-id="9cf76-319">toofinish 設定 hello 叢集中，遵循您所做的 hello 第一個可用性群組的重複 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="9cf76-319">toofinish configuring hello cluster, repeat hello steps that you followed when you made hello first availability group.</span></span> <span data-ttu-id="9cf76-320">也就是設定 hello[叢集 toouse hello 新 IP 位址](#configure-the-cluster-to-use-the-load-balancer-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-320">That is, configure hello [cluster toouse hello new IP address](#configure-the-cluster-to-use-the-load-balancer-ip-address).</span></span> 

<span data-ttu-id="9cf76-321">加入 hello 接聽程式的 IP 位址之後，請透過 hello 下列方式設定 hello 其他可用性群組：</span><span class="sxs-lookup"><span data-stu-id="9cf76-321">After you have added an IP address for hello listener, configure hello additional availability group by doing hello following:</span></span> 

1. <span data-ttu-id="9cf76-322">請確認為 hello 新 IP 位址的 hello 探查連接埠已開啟兩部 SQL Server 虛擬機器上。</span><span class="sxs-lookup"><span data-stu-id="9cf76-322">Verify that hello probe port for hello new IP address is open on both SQL Server virtual machines.</span></span> 

2. <span data-ttu-id="9cf76-323">[在 [叢集管理員] 中，加入 hello 用戶端存取點](#addcap)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-323">[In Cluster Manager, add hello client access point](#addcap).</span></span>

3. <span data-ttu-id="9cf76-324">[設定 hello 可用性群組的 hello IP 資源](#congroup)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-324">[Configure hello IP resource for hello availability group](#congroup).</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="9cf76-325">當您建立 hello IP 位址時，使用您加入 toohello 負載平衡器的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9cf76-325">When you create hello IP address, use hello IP address that you added toohello load balancer.</span></span>  

4. <span data-ttu-id="9cf76-326">[讓 hello SQL Server 可用性群組資源相依於 hello 用戶端存取點](#dependencyGroup)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-326">[Make hello SQL Server availability group resource dependent on hello client access point](#dependencyGroup).</span></span>

5. <span data-ttu-id="9cf76-327">[使 hello 用戶端存取點依存於 hello IP 位址資源](#listname)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-327">[Make hello client access point resource dependent on hello IP address](#listname).</span></span>
 
6. <span data-ttu-id="9cf76-328">[在 PowerShell 中設定 hello 叢集參數](#setparam)。</span><span class="sxs-lookup"><span data-stu-id="9cf76-328">[Set hello cluster parameters in PowerShell](#setparam).</span></span>

<span data-ttu-id="9cf76-329">設定 hello 可用性群組 toouse hello 新的 IP 位址之後，設定 hello 連接 toohello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9cf76-329">After you configure hello availability group toouse hello new IP address, configure hello connection toohello listener.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9cf76-330">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9cf76-330">Next steps</span></span>

- [<span data-ttu-id="9cf76-331">在不同區域中的 Azure 虛擬機器上設定 SQL Server Always On 可用性群組</span><span class="sxs-lookup"><span data-stu-id="9cf76-331">Configure a SQL Server Always On availability group on Azure virtual machines in different regions</span></span>](virtual-machines-windows-portal-sql-availability-group-dr.md)
