---
title: "在 Azure 中的多個 IP 組態上的平衡 aaaLoad |Microsoft 文件"
description: "在主要和次要 IP 組態間進行負載平衡。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a><span data-ttu-id="e395c-103">多個 IP 組態使用 hello Azure 入口網站上的負載平衡</span><span class="sxs-lookup"><span data-stu-id="e395c-103">Load balancing on multiple IP configurations using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e395c-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="e395c-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="e395c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e395c-105">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)
> * [<span data-ttu-id="e395c-106">CLI</span><span class="sxs-lookup"><span data-stu-id="e395c-106">CLI</span></span>](load-balancer-multiple-ip-cli.md)

<span data-ttu-id="e395c-107">本文說明如何 toouse Azure 負載平衡器與多個 IP 位址上的次要網路介面 (NIC)。此案例中，我們有兩個 Vm 執行 Windows，每個都有主要和次要的 nic。</span><span class="sxs-lookup"><span data-stu-id="e395c-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="e395c-108">每個次要 hello Nic 有兩個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="e395c-108">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="e395c-109">每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站會繫結的 tooone 的 hello hello 次要 NIC 上的 IP 組態</span><span class="sxs-lookup"><span data-stu-id="e395c-109">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="e395c-110">我們使用 Azure 負載平衡器 tooexpose 兩個前端 IP 位址，一個用於每個網站，toodistribute 流量 toohello 個別的 IP 組態 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="e395c-110">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="e395c-111">這種情況下使用 hello 跨前端，以及兩個後端集區 IP 位址相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="e395c-111">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a><span data-ttu-id="e395c-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="e395c-113">Prerequisites</span></span>
<span data-ttu-id="e395c-114">這個範例假設您有資源群組名稱*contosofabrikam*以 hello 下列組態：</span><span class="sxs-lookup"><span data-stu-id="e395c-114">This example assumes that you have a Resource Group named *contosofabrikam* with hello following configuration:</span></span>
 -  <span data-ttu-id="e395c-115">包含虛擬網路，名為*myVNet*，呼叫的兩個 Vm *VM1*和*VM2*分別內 hello 相同可用性設定組具名*myAvailset*.</span><span class="sxs-lookup"><span data-stu-id="e395c-115">includes a virtual network named *myVNet*, two VMs called *VM1* and *VM2* respectively within hello same availability set named *myAvailset*.</span></span> 
 - <span data-ttu-id="e395c-116">每個 VM 各有主要 NIC 和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="e395c-116">each VM has a primary NIC and a secondary NIC.</span></span> <span data-ttu-id="e395c-117">hello 主要名為 Nic *VM1NIC1*和*VM2NIC1*和 hello 次要命名 Nic *VM1NIC2*和*VM2NIC2*。</span><span class="sxs-lookup"><span data-stu-id="e395c-117">hello primary NICs are named *VM1NIC1* and *VM2NIC1* and hello secondary NICs are named *VM1NIC2* and *VM2NIC2*.</span></span> <span data-ttu-id="e395c-118">如需如何建立具有多個 NIC 之 VM 的詳細資訊，請參閱[使用 PowerShell 建立具有多個 NIC 的 VM](../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="e395c-118">For more information about creating VMs with multiple NICs, see [Create a VM with multiple NICs using PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="e395c-119">多個 IP 組態步驟 tooload 餘額</span><span class="sxs-lookup"><span data-stu-id="e395c-119">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="e395c-120">遵循下列步驟下, 面這篇文章所述的 tooachieve hello 案例：</span><span class="sxs-lookup"><span data-stu-id="e395c-120">Follow these steps below tooachieve hello scenario outlined in this article:</span></span>

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a><span data-ttu-id="e395c-121">步驟 1： 設定每個 VM hello 次要 Nic</span><span class="sxs-lookup"><span data-stu-id="e395c-121">STEP 1: Configure hello secondary NICs for each VM</span></span>

<span data-ttu-id="e395c-122">在虛擬網路中，每個 VM，請加入設定的 IP 組態 hello 次要 NIC，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e395c-122">For each VM in your virtual network, add set IP configuration for hello secondary NIC as follows:</span></span>  

1. <span data-ttu-id="e395c-123">從瀏覽器瀏覽 toohello Azure 入口網站： http://portal.azure.com 並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="e395c-123">From a browser navigate toohello Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="e395c-124">左側 hello 頂端囉 」 畫面，按一下 hello 資源群組圖示，然後再按一下 Vm 位於 hello 資源群組 hello (例如， *contosofabrikam*)。</span><span class="sxs-lookup"><span data-stu-id="e395c-124">On hello top left-hand side of hello screen, click hello Resource Group icon, and then click hello resource group hello VMs are located in (for example, *contosofabrikam*).</span></span> <span data-ttu-id="e395c-125">hello**資源群組**刀鋒視窗，其中列出所有 hello 資源以及 hello hello Vm 的網路介面現在會顯示。</span><span class="sxs-lookup"><span data-stu-id="e395c-125">hello **Resource groups** blade that lists all hello resources along with hello network interfaces for hello VMs is now displayed.</span></span>
3. <span data-ttu-id="e395c-126">toohello 次要複本的每個 VM NIC 新增 IP 設定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e395c-126">toohello secondary NIC of each VM, add an IP configuration as follows:</span></span>
    1. <span data-ttu-id="e395c-127">選取您想要 tooadd hello IP 組態的 hello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="e395c-127">Select hello network interface you want tooadd hello IP configuration to.</span></span>
    2. <span data-ttu-id="e395c-128">在 hello 刀鋒視窗中出現的 hello NIC，您選取，按一下  **IP 組態**。</span><span class="sxs-lookup"><span data-stu-id="e395c-128">In hello blade that appears for hello NIC that you selected, click **IP configurations**.</span></span> <span data-ttu-id="e395c-129">然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="e395c-129">Then click **Add** towards hello top of hello blade that shows up.</span></span>
    3. <span data-ttu-id="e395c-130">在 hello**新增的 IP 組態**刀鋒視窗中，加入第二個 IP 組態 toohello NIC，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e395c-130">In hello **Add IP configurations** blade, add a second IP configuration toohello NIC as follows:</span></span> 
        1. <span data-ttu-id="e395c-131">輸入次要的 IP 組態的名稱 (例如，針對 VM1 和 VM2 名稱 hello 做為 IP 組態*VM1NIC2 ipconfig2*和*VM2NIC2 ipconfig2*分別)。</span><span class="sxs-lookup"><span data-stu-id="e395c-131">Type a name for your secondary IP configuration (for example, for VM1 and VM2 name hello IP configurations as *VM1NIC2-ipconfig2* and *VM2NIC2-ipconfig2* respectively).</span></span>
        2. <span data-ttu-id="e395c-132">針對 [私人 IP 位址]，為 [配置] 選取 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="e395c-132">For **Private IP address**, for **Allocation**, select **Static**.</span></span>
        3. <span data-ttu-id="e395c-133">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e395c-133">Click **OK**.</span></span>
        4. <span data-ttu-id="e395c-134">Hello 第二個 IP 組態 hello 次要 NIC 完成時，它會顯示在 hello **IP 組態**hello 指定 NIC 的 設定 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="e395c-134">When hello second IP configuration for hello secondary NIC is complete, it is displayed in hello **IP configurations** settings blade for hello given NIC.</span></span>

### <a name="step-2-create-a-load-balancer"></a><span data-ttu-id="e395c-135">步驟 2：建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e395c-135">STEP 2: Create a load balancer</span></span>

<span data-ttu-id="e395c-136">如下所示建立負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="e395c-136">Create a load balancer as follows:</span></span>

1. <span data-ttu-id="e395c-137">從瀏覽器瀏覽 toohello Azure 入口網站： http://portal.azure.com 並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="e395c-137">From a browser navigate toohello Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="e395c-138">在 hello 左邊囉 」 畫面，按一下 **新增** > **網路** > **負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="e395c-138">On hello top left-hand side of hello screen, click **New** > **Networking** > **Load Balancer**.</span></span> <span data-ttu-id="e395c-139">接下來，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e395c-139">Next, click **Create**.</span></span>
3. <span data-ttu-id="e395c-140">在 hello**建立負載平衡器**刀鋒視窗中，輸入您的負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="e395c-140">In hello **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="e395c-141">在此我們將其稱為 mylb。</span><span class="sxs-lookup"><span data-stu-id="e395c-141">Here it is called *mylb*.</span></span>
4. <span data-ttu-id="e395c-142">在 [公用 IP 位址] 底下建立稱為 **PublicIP1** 的新公用 IP。</span><span class="sxs-lookup"><span data-stu-id="e395c-142">Under Public IP address, create a new public IP called **PublicIP1**.</span></span>
5. <span data-ttu-id="e395c-143">在資源群組下選取 hello Vm 的現有的資源群組 (例如， *contosofabrikam*)。</span><span class="sxs-lookup"><span data-stu-id="e395c-143">Under Resource Group, select hello existing Resource group of your VMs (for example, *contosofabrikam*).</span></span> <span data-ttu-id="e395c-144">接著選取適當位置，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="e395c-144">Then, select an appropriate location, and then click **OK**.</span></span> <span data-ttu-id="e395c-145">hello 負載平衡器會啟動 toodeploy 和 toosuccessfully 完整部署時將會需要幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="e395c-145">hello load balancer will then start toodeploy and will take a few minutes toosuccessfully complete deployment.</span></span>
6. <span data-ttu-id="e395c-146">一旦部署之後，hello 負載平衡器會顯示為資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="e395c-146">Once deployed, hello load balancer is displayed as a resource in your Resource Group.</span></span>

### <a name="step-3-configure-hello-frontend-ip-pool"></a><span data-ttu-id="e395c-147">步驟 3： 設定 hello 前端 IP 集區</span><span class="sxs-lookup"><span data-stu-id="e395c-147">STEP 3: Configure hello frontend IP pool</span></span>

<span data-ttu-id="e395c-148">為每個網站 (Contoso 和 Fabrikam) 設定前端 IP 集區，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e395c-148">Configure your frontend IP pool for each website (Contoso and Fabrikam) as follows:</span></span>

1. <span data-ttu-id="e395c-149">在 hello 入口網站中，按一下 **更多服務**> 類型**公用 IP 位址**在 hello 篩選 方塊中，然後按一下**公用 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="e395c-149">In hello portal, click **More services** > type **Public IP address** in hello filter box, and then click **Public IP addresses**.</span></span> <span data-ttu-id="e395c-150">按一下**新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="e395c-150">Click **Add** towards hello top of hello blade that shows up.</span></span>
2. <span data-ttu-id="e395c-151">為這兩個網站 (contoso 和 fabrikam) 設定兩個公用 IP 位址 (PublicIP1 和 PublicIP2)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e395c-151">Configure two Public IP addresses (*PublicIP1* and *PublicIP2*) for both websites (contoso and fabrikam) as follows:</span></span>
    1. <span data-ttu-id="e395c-152">輸入前端 IP 位址的名稱。</span><span class="sxs-lookup"><span data-stu-id="e395c-152">Type a name for your frontend IP address.</span></span>
    2. <span data-ttu-id="e395c-153">如**資源群組**，選取 hello hello Vm 的現有的資源群組 (例如， *contosofabrikam*)。</span><span class="sxs-lookup"><span data-stu-id="e395c-153">For **Resource Group**, select hello existing Resource Group of hello VMs (for example, *contosofabrikam*).</span></span>
    3. <span data-ttu-id="e395c-154">如**位置**，選取 hello 相同的位置，如 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="e395c-154">For **Location**, select hello same location as hello VMs.</span></span>
    4. <span data-ttu-id="e395c-155">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e395c-155">Click **OK**.</span></span>
    5. <span data-ttu-id="e395c-156">一旦建立 hello 兩個公用 IP 位址，它們會同時顯示在 hello**公用 IP**位址刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e395c-156">Once hello two Public IP addresses are created, they are both displayed in hello **Public IP** addresses blade.</span></span>
3. <span data-ttu-id="e395c-157">在 hello 入口網站中，按一下 **更多服務**> 類型**負載平衡器**在 hello 篩選 方塊中，然後按一下**負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="e395c-157">In hello portal, click **More services** > type **load balancer** in hello filter box, and then click **Load Balancer**.</span></span>  
4. <span data-ttu-id="e395c-158">選取 hello 負載平衡器 (*mylb*) 您想 tooadd hello 前端 IP 集區。</span><span class="sxs-lookup"><span data-stu-id="e395c-158">Select hello load balancer (*mylb*) that you want tooadd hello frontend IP pool to.</span></span>
5. <span data-ttu-id="e395c-159">在 [設定] 底下選取 [前端集區]。</span><span class="sxs-lookup"><span data-stu-id="e395c-159">Under **Settings**, select **Frontend Pools**.</span></span> <span data-ttu-id="e395c-160">然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="e395c-160">Then click **Add** towards hello top of hello blade that shows up.</span></span>
6. <span data-ttu-id="e395c-161">輸入前端 IP 位址的名稱 (farbikamfe 或 *contosofe)。</span><span class="sxs-lookup"><span data-stu-id="e395c-161">Type a name for your frontend IP address (*farbikamfe* or **contosofe*).</span></span>
7. <span data-ttu-id="e395c-162">按一下**IP 位址**在 hello**選擇公用 IP 位址**刀鋒視窗中，選取 hello 您前端的 IP 位址 (*PublicIP1*或*PublicIP2*).</span><span class="sxs-lookup"><span data-stu-id="e395c-162">Click **IP address** and on hello **Choose Public IP address** blade, select hello IP addresses for your frontend (*PublicIP1* or *PublicIP2*).</span></span>
8. <span data-ttu-id="e395c-163">重複步驟 3 too7 內這個區段 toocreate hello 第二個前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e395c-163">Repeat steps 3 too7 within this section toocreate hello second frontend IP address.</span></span>
9. <span data-ttu-id="e395c-164">這兩個前端 IP 位址 hello 前端 IP 集區組態完成時，會顯示在 hello**前端 IP 集區**刀鋒視窗，您的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e395c-164">When hello frontend IP pool configuration is complete, both frontend IP addresses are displayed in hello **Frontend IP Pool** blade of your load balancer.</span></span> 
    
### <a name="step-4-configure-hello-backend-pool"></a><span data-ttu-id="e395c-165">步驟 4： 設定 hello 後端集區</span><span class="sxs-lookup"><span data-stu-id="e395c-165">STEP 4: Configure hello backend pool</span></span>   
<span data-ttu-id="e395c-166">設定 hello 後端位址集區上您的負載平衡器，為每個網站 （Contoso 和 Fabrikam），如下所示：</span><span class="sxs-lookup"><span data-stu-id="e395c-166">Configure hello backend address pools on your load balancer for each website (Contoso and Fabrikam) as follows:</span></span>
        
1. <span data-ttu-id="e395c-167">在 hello 入口網站中，按一下 **更多服務**> 在 hello 篩選方塊中，輸入負載平衡器，然後按一下**負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="e395c-167">In hello portal, click **More services** > type load balancer in hello filter box, and then click **Load Balancer**.</span></span>  
2. <span data-ttu-id="e395c-168">選取 hello 負載平衡器 (*mylb*) 您想要 tooadd hello 後端集區。</span><span class="sxs-lookup"><span data-stu-id="e395c-168">Select hello load balancer (*mylb*) that you want tooadd hello backend pools to.</span></span>
3. <span data-ttu-id="e395c-169">在 [設定] 底下選取 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="e395c-169">Under **Settings**, select **Backend Pools**.</span></span> <span data-ttu-id="e395c-170">輸入後端集區的名稱 (例如，contosopool 或 fabrikampool)。</span><span class="sxs-lookup"><span data-stu-id="e395c-170">Type a name for your backend pool (for example, *contosopool* or *fabrikampool*).</span></span> <span data-ttu-id="e395c-171">然後按一下 hello**新增**朝 hello 顯示 hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="e395c-171">Then click hello **Add** button toward hello top of hello blade that shows up.</span></span> 
4. <span data-ttu-id="e395c-172">在 [關聯到] 中，選取 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="e395c-172">For **Associated to**, select **Availability set**.</span></span>
5. <span data-ttu-id="e395c-173">在 [可用性設定組] 中，選取 [myAvailset]。</span><span class="sxs-lookup"><span data-stu-id="e395c-173">For **Availability set**, select **myAvailset**.</span></span>
6. <span data-ttu-id="e395c-174">如下所示為這兩個 VM 新增目標網路 IP 組態 (請參閱圖 2)︰</span><span class="sxs-lookup"><span data-stu-id="e395c-174">Add Target network IP configurations, for both VMs as follows (see Figure 2):</span></span>  
    1. <span data-ttu-id="e395c-175">如**目標虛擬機器**，選取 hello 想 tooadd toohello 後端集區 （例如，VM1 或 vm2 的情況） 的 VM。</span><span class="sxs-lookup"><span data-stu-id="e395c-175">For **Target Virtual machine**, select hello VM that you want tooadd toohello backend pool (for example, VM1 or VM2).</span></span>
    2. <span data-ttu-id="e395c-176">如**網路 IP 設定**，請選取該 vm （例如，VM1NIC2 ipconfig2 或 VM2NIC2 ipconfig2） hello 次要 Nic IP 設定。</span><span class="sxs-lookup"><span data-stu-id="e395c-176">For **Network IP configuration**, select hello secondary NICs IP configuration for that VM (for example, VM1NIC2-ipconfig2 or VM2NIC2-ipconfig2).</span></span>
    <span data-ttu-id="e395c-177">![LB 案例影像](./media/load-balancer-multiple-ip/lb-backendpool.PNG)</span><span class="sxs-lookup"><span data-stu-id="e395c-177">![LB scenario image](./media/load-balancer-multiple-ip/lb-backendpool.PNG)</span></span>
            
        <span data-ttu-id="e395c-178">**圖 2**: hello 負載平衡器設定的後端集區</span><span class="sxs-lookup"><span data-stu-id="e395c-178">**Figure 2**: Configuring hello load balancer with backend pools</span></span>  
7. <span data-ttu-id="e395c-179">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e395c-179">Click **OK**.</span></span>
8. <span data-ttu-id="e395c-180">當 hello 後端集區設定已完成時，這兩個後端位址集區會顯示在 [hello**後端集區] 刀鋒視窗**您的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e395c-180">When hello backend pool configuration is complete, both backend address pools are displayed in hello **Backend pool blade** of your load balancer.</span></span>

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a><span data-ttu-id="e395c-181">步驟 5︰設定負載平衡器的健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="e395c-181">STEP 5: Configure a health probe for your load balancer</span></span>
<span data-ttu-id="e395c-182">設定負載平衡器的健康狀態探查，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e395c-182">Configure a health probe for your load balancer as follows:</span></span>
    1. <span data-ttu-id="e395c-183">在 hello 入口網站中，按一下 更多服務 > 在 hello 篩選方塊中，輸入負載平衡器，然後按一下**負載平衡器**。</span><span class="sxs-lookup"><span data-stu-id="e395c-183">In hello portal, click More services > type load balancer in hello filter box, and then click **Load Balancer**.</span></span>  
    2. <span data-ttu-id="e395c-184">選取您想要 tooadd hello 後端集區的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e395c-184">Select hello load balancer that you want tooadd hello backend pools to.</span></span>
    3. <span data-ttu-id="e395c-185">在 [設定] 下，選取 [健康狀態探查]。</span><span class="sxs-lookup"><span data-stu-id="e395c-185">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="e395c-186">然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="e395c-186">Then click **Add** towards hello top of hello blade that shows up.</span></span>
    4. <span data-ttu-id="e395c-187">輸入 hello 健全狀況探查 (例如，HTTP) 的名稱，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e395c-187">Type a name for hello health probe (for example, HTTP), and click **OK**.</span></span>

### <a name="step-6-configure-load-balancing-rules"></a><span data-ttu-id="e395c-188">步驟 6：設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="e395c-188">STEP 6: Configure load balancing rules</span></span>
<span data-ttu-id="e395c-189">為每個網站設定負載平衡規則 (HTTPc 和 HTTPf)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="e395c-189">Configure load balancing rules (*HTTPc* and *HTTPf*) for each website as follows:</span></span>
    
1. <span data-ttu-id="e395c-190">在 [設定] 下，選取 [健康狀態探查]。</span><span class="sxs-lookup"><span data-stu-id="e395c-190">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="e395c-191">然後按一下 **新增**朝向 hello 顯示 hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="e395c-191">Then click **Add** towards hello top of hello blade that shows up.</span></span>
2. <span data-ttu-id="e395c-192">如**名稱**，輸入 hello 負載平衡規則的名稱 (例如， *HTTPc* contoso 或*HTTPf* fabrikam)</span><span class="sxs-lookup"><span data-stu-id="e395c-192">For **Name**, type a name for hello load balancing rule (for example, *HTTPc* for Contoso, or *HTTPf* for Fabrikam)</span></span>
3. <span data-ttu-id="e395c-193">前端 IP 位址，選取 hello hello 前端 IP 位址 (例如*Contosofe*或*Fabrikamfe*)</span><span class="sxs-lookup"><span data-stu-id="e395c-193">For Frontend IP address, select hello hello frontend IP address (for example *Contosofe* or *Fabrikamfe*)</span></span>
4. <span data-ttu-id="e395c-194">如**連接埠**和**後端連接埠**，保留 hello 預設值**80**。</span><span class="sxs-lookup"><span data-stu-id="e395c-194">For **Port** and **Backend port**, keep hello default value **80**.</span></span>
5. <span data-ttu-id="e395c-195">在 [浮動 IP (伺服器直接回傳)] 中，按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="e395c-195">For **Floating IP (direct server return)**, click **Enabled**.</span></span>
6. <span data-ttu-id="e395c-196">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="e395c-196">Click **OK**.</span></span>
7. <span data-ttu-id="e395c-197">重複步驟 1 too6 這個區段 toocreate hello 第二個負載平衡器規則中。</span><span class="sxs-lookup"><span data-stu-id="e395c-197">Repeat steps 1 too6 within this section toocreate hello second Load Balancer rule.</span></span>
8. <span data-ttu-id="e395c-198">Hello 負載平衡規則已完成設定，這兩個規則 ((*HTTPc*和*HTTPf*) 會顯示在 hello**負載平衡規則**刀鋒視窗，您的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e395c-198">When hello load balancing rules configuration is complete, both rules ((*HTTPc* and *HTTPf*) are displayed in hello **Load balancing rules** blade of your load balancer.</span></span>

### <a name="step-7-configure-dns-records"></a><span data-ttu-id="e395c-199">步驟 7︰設定 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="e395c-199">STEP 7: Configure DNS records</span></span>
<span data-ttu-id="e395c-200">最後，您必須設定 DNS 資源記錄 toopoint toohello 各自的前端 IP 位址的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e395c-200">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello load balancer.</span></span> <span data-ttu-id="e395c-201">您可以在 Azure DNS 中裝載網域。</span><span class="sxs-lookup"><span data-stu-id="e395c-201">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="e395c-202">如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="e395c-202">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e395c-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e395c-203">Next steps</span></span>
- <span data-ttu-id="e395c-204">深入了解如何 toocombine 負載平衡服務在 Azure 中[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="e395c-204">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="e395c-205">了解如何在 Azure toomanage 中使用不同類型的記錄檔，以及疑難排解負載平衡器中的[Azure 負載平衡器的記錄分析](../load-balancer/load-balancer-monitor-log.md)。</span><span class="sxs-lookup"><span data-stu-id="e395c-205">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
