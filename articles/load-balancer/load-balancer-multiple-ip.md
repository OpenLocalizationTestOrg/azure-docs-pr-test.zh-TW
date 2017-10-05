---
title: "在 Azure 中的多個 IP 組態上進行負載平衡 | Microsoft Docs"
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
ms.openlocfilehash: cf1e68c7b37b2506de007bdf24eea63a27187a33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-the-azure-portal"></a><span data-ttu-id="4d28d-103">使用 Azure 入口網站在多個 IP 組態上進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="4d28d-103">Load balancing on multiple IP configurations using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d28d-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="4d28d-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="4d28d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d28d-105">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)
> * [<span data-ttu-id="4d28d-106">CLI</span><span class="sxs-lookup"><span data-stu-id="4d28d-106">CLI</span></span>](load-balancer-multiple-ip-cli.md)

<span data-ttu-id="4d28d-107">本文說明如何對次要網路介面 (NIC) 上的多個 IP 位址使用 Azure Load Balancer。在此案例中，我們有兩部執行 Windows 的 VM，每部各有一個主要和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="4d28d-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="4d28d-108">每個次要 Nic 有兩個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4d28d-108">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="4d28d-109">每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。</span><span class="sxs-lookup"><span data-stu-id="4d28d-109">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="4d28d-110">每個網站繫結到次要 NIC 上的其中一個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4d28d-110">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="4d28d-111">我們使用 Azure Load Balancer 來公開兩個前端 IP 位址，每個網站各使用其中一個，以將流量分散給網站的個別 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4d28d-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="4d28d-112">此案例會在兩個前端以及兩個後端集區 IP 位址使用相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="4d28d-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a><span data-ttu-id="4d28d-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="4d28d-114">Prerequisites</span></span>
<span data-ttu-id="4d28d-115">此範例假設您有一個名為 contosofabrikam 的資源群組，其具有下列組態︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-115">This example assumes that you have a Resource Group named *contosofabrikam* with the following configuration:</span></span>
 -  <span data-ttu-id="4d28d-116">在名為 myAvailset 的同一個可用性設定組內，包含一個名為 myVNet 的虛擬網路，和兩個名稱分別為 VM1 和 VM2 的 VM。</span><span class="sxs-lookup"><span data-stu-id="4d28d-116">includes a virtual network named *myVNet*, two VMs called *VM1* and *VM2* respectively within the same availability set named *myAvailset*.</span></span> 
 - <span data-ttu-id="4d28d-117">每個 VM 各有主要 NIC 和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="4d28d-117">each VM has a primary NIC and a secondary NIC.</span></span> <span data-ttu-id="4d28d-118">主要 NIC 名為 VM1NIC1 和 VM2NIC1，次要 NIC 名為 VM1NIC2 和 VM2NIC2。</span><span class="sxs-lookup"><span data-stu-id="4d28d-118">The primary NICs are named *VM1NIC1* and *VM2NIC1* and the secondary NICs are named *VM1NIC2* and *VM2NIC2*.</span></span> <span data-ttu-id="4d28d-119">如需如何建立具有多個 NIC 之 VM 的詳細資訊，請參閱[使用 PowerShell 建立具有多個 NIC 的 VM](../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-119">For more information about creating VMs with multiple NICs, see [Create a VM with multiple NICs using PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="4d28d-120">在多個 IP 組態上進行負載平衡的步驟</span><span class="sxs-lookup"><span data-stu-id="4d28d-120">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="4d28d-121">請遵循下列步驟來達成本文所述案例︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-121">Follow these steps below to achieve the scenario outlined in this article:</span></span>

### <a name="step-1-configure-the-secondary-nics-for-each-vm"></a><span data-ttu-id="4d28d-122">步驟 1︰設定每個 VM 的次要 NIC</span><span class="sxs-lookup"><span data-stu-id="4d28d-122">STEP 1: Configure the secondary NICs for each VM</span></span>

<span data-ttu-id="4d28d-123">為虛擬網路中的每個 VM，新增次要 NIC 的 IP 組態，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-123">For each VM in your virtual network, add set IP configuration for the secondary NIC as follows:</span></span>  

1. <span data-ttu-id="4d28d-124">透過瀏覽器瀏覽至 Azure 入口網站 http://portal.azure.com，並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="4d28d-124">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="4d28d-125">在畫面左側按一下 [資源群組] 圖示，然後按一下 VM 所位在的資源群組 (例如，contosofabrikam)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-125">On the top left-hand side of the screen, click the Resource Group icon, and then click the resource group the VMs are located in (for example, *contosofabrikam*).</span></span> <span data-ttu-id="4d28d-126">此時會顯示 [資源群組] 刀鋒視窗，裡面列出了所有資源以及 VM 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="4d28d-126">The **Resource groups** blade that lists all the resources along with the network interfaces for the VMs is now displayed.</span></span>
3. <span data-ttu-id="4d28d-127">對每個 VM 的次要 NIC 新增 IP 組態，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-127">To the secondary NIC of each VM, add an IP configuration as follows:</span></span>
    1. <span data-ttu-id="4d28d-128">選取要將 IP 組態新增至的網路介面。</span><span class="sxs-lookup"><span data-stu-id="4d28d-128">Select the network interface you want to add the IP configuration to.</span></span>
    2. <span data-ttu-id="4d28d-129">在針對所選 NIC 出現的刀鋒視窗中，按一下 [IP 組態]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-129">In the blade that appears for the NIC that you selected, click **IP configurations**.</span></span> <span data-ttu-id="4d28d-130">然後按一下出現的刀鋒視窗中靠近上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-130">Then click **Add** towards the top of the blade that shows up.</span></span>
    3. <span data-ttu-id="4d28d-131">在 [新增 IP 組態] 刀鋒視窗中，對 NIC 新增第二個 IP 組態，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-131">In the **Add IP configurations** blade, add a second IP configuration to the NIC as follows:</span></span> 
        1. <span data-ttu-id="4d28d-132">輸入次要 IP 組態的名稱 (例如，將 VM1 和 VM2 的 IP 組態分別命名為 VM1NIC2-ipconfig2 和 VM2NIC2-ipconfig2)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-132">Type a name for your secondary IP configuration (for example, for VM1 and VM2 name the IP configurations as *VM1NIC2-ipconfig2* and *VM2NIC2-ipconfig2* respectively).</span></span>
        2. <span data-ttu-id="4d28d-133">針對 [私人 IP 位址]，為 [配置] 選取 [靜態]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-133">For **Private IP address**, for **Allocation**, select **Static**.</span></span>
        3. <span data-ttu-id="4d28d-134">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4d28d-134">Click **OK**.</span></span>
        4. <span data-ttu-id="4d28d-135">次要 NIC 的第二個 IP 組態在設定完成時，會顯示在給定 NIC 的 [IP 組態] 設定刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4d28d-135">When the second IP configuration for the secondary NIC is complete, it is displayed in the **IP configurations** settings blade for the given NIC.</span></span>

### <a name="step-2-create-a-load-balancer"></a><span data-ttu-id="4d28d-136">步驟 2：建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4d28d-136">STEP 2: Create a load balancer</span></span>

<span data-ttu-id="4d28d-137">如下所示建立負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-137">Create a load balancer as follows:</span></span>

1. <span data-ttu-id="4d28d-138">透過瀏覽器瀏覽至 Azure 入口網站 http://portal.azure.com，並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="4d28d-138">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="4d28d-139">在畫面左側按一下 [新增] > [網路] > [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-139">On the top left-hand side of the screen, click **New** > **Networking** > **Load Balancer**.</span></span> <span data-ttu-id="4d28d-140">接下來，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-140">Next, click **Create**.</span></span>
3. <span data-ttu-id="4d28d-141">在 [建立負載平衡器] 刀鋒視窗中，輸入負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="4d28d-141">In the **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="4d28d-142">在此我們將其稱為 mylb。</span><span class="sxs-lookup"><span data-stu-id="4d28d-142">Here it is called *mylb*.</span></span>
4. <span data-ttu-id="4d28d-143">在 [公用 IP 位址] 底下建立稱為 **PublicIP1** 的新公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4d28d-143">Under Public IP address, create a new public IP called **PublicIP1**.</span></span>
5. <span data-ttu-id="4d28d-144">在 [資源群組] 底下，選取 VM 的現有資源群組 (例如，contosofabrikam)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-144">Under Resource Group, select the existing Resource group of your VMs (for example, *contosofabrikam*).</span></span> <span data-ttu-id="4d28d-145">接著選取適當位置，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-145">Then, select an appropriate location, and then click **OK**.</span></span> <span data-ttu-id="4d28d-146">負載平衡器接著會開始部署，並且需要幾分鐘的時間才能順利完成部署。</span><span class="sxs-lookup"><span data-stu-id="4d28d-146">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span></span>
6. <span data-ttu-id="4d28d-147">負載平衡器在部署後會顯示為資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="4d28d-147">Once deployed, the load balancer is displayed as a resource in your Resource Group.</span></span>

### <a name="step-3-configure-the-frontend-ip-pool"></a><span data-ttu-id="4d28d-148">步驟 3︰設定前端 IP 集區</span><span class="sxs-lookup"><span data-stu-id="4d28d-148">STEP 3: Configure the frontend IP pool</span></span>

<span data-ttu-id="4d28d-149">為每個網站 (Contoso 和 Fabrikam) 設定前端 IP 集區，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-149">Configure your frontend IP pool for each website (Contoso and Fabrikam) as follows:</span></span>

1. <span data-ttu-id="4d28d-150">在入口網站中，按一下 [更多服務]，在篩選方塊中輸入**公用 IP 位址**，然後按一下 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-150">In the portal, click **More services** > type **Public IP address** in the filter box, and then click **Public IP addresses**.</span></span> <span data-ttu-id="4d28d-151">按一下出現的刀鋒視窗中靠近上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-151">Click **Add** towards the top of the blade that shows up.</span></span>
2. <span data-ttu-id="4d28d-152">為這兩個網站 (contoso 和 fabrikam) 設定兩個公用 IP 位址 (PublicIP1 和 PublicIP2)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-152">Configure two Public IP addresses (*PublicIP1* and *PublicIP2*) for both websites (contoso and fabrikam) as follows:</span></span>
    1. <span data-ttu-id="4d28d-153">輸入前端 IP 位址的名稱。</span><span class="sxs-lookup"><span data-stu-id="4d28d-153">Type a name for your frontend IP address.</span></span>
    2. <span data-ttu-id="4d28d-154">在 [資源群組] 中選取 VM 的現有資源群組 (例如，contosofabrikam)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-154">For **Resource Group**, select the existing Resource Group of the VMs (for example, *contosofabrikam*).</span></span>
    3. <span data-ttu-id="4d28d-155">在 [位置] 中選取和 VM 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="4d28d-155">For **Location**, select the same location as the VMs.</span></span>
    4. <span data-ttu-id="4d28d-156">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4d28d-156">Click **OK**.</span></span>
    5. <span data-ttu-id="4d28d-157">兩個公用 IP 位址都建立好之後，便會同時顯示在 [公用 IP 位址] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4d28d-157">Once the two Public IP addresses are created, they are both displayed in the **Public IP** addresses blade.</span></span>
3. <span data-ttu-id="4d28d-158">在入口網站中，按一下 [更多服務]，在篩選方塊中輸入**負載平衡器**，然後按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-158">In the portal, click **More services** > type **load balancer** in the filter box, and then click **Load Balancer**.</span></span>  
4. <span data-ttu-id="4d28d-159">選取要將前端 IP 集區新增到的負載平衡器 (mylb)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-159">Select the load balancer (*mylb*) that you want to add the frontend IP pool to.</span></span>
5. <span data-ttu-id="4d28d-160">在 [設定] 底下選取 [前端集區]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-160">Under **Settings**, select **Frontend Pools**.</span></span> <span data-ttu-id="4d28d-161">然後按一下出現的刀鋒視窗中靠近上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-161">Then click **Add** towards the top of the blade that shows up.</span></span>
6. <span data-ttu-id="4d28d-162">輸入前端 IP 位址的名稱 (farbikamfe 或 *contosofe)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-162">Type a name for your frontend IP address (*farbikamfe* or **contosofe*).</span></span>
7. <span data-ttu-id="4d28d-163">按一下 [IP 位址]，然後在 [選擇公用 IP 位址] 刀鋒視窗上，選取前端的 IP 位址 (PublicIP1 或 PublicIP2)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-163">Click **IP address** and on the **Choose Public IP address** blade, select the IP addresses for your frontend (*PublicIP1* or *PublicIP2*).</span></span>
8. <span data-ttu-id="4d28d-164">重複本節中的步驟 3 到 7，以建立第二個前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d28d-164">Repeat steps 3 to 7 within this section to create the second frontend IP address.</span></span>
9. <span data-ttu-id="4d28d-165">當前端 IP 集區組態設定完成時，這兩個前端 IP 位址會顯示在負載平衡器的 [前端 IP 集區] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4d28d-165">When the frontend IP pool configuration is complete, both frontend IP addresses are displayed in the **Frontend IP Pool** blade of your load balancer.</span></span> 
    
### <a name="step-4-configure-the-backend-pool"></a><span data-ttu-id="4d28d-166">步驟 4︰設定後端集區</span><span class="sxs-lookup"><span data-stu-id="4d28d-166">STEP 4: Configure the backend pool</span></span>   
<span data-ttu-id="4d28d-167">為每個網站 (Contoso 和 Fabrikam) 設定負載平衡器上的後端位址集區，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-167">Configure the backend address pools on your load balancer for each website (Contoso and Fabrikam) as follows:</span></span>
        
1. <span data-ttu-id="4d28d-168">在入口網站中，按一下 [更多服務]，在篩選方塊中輸入負載平衡器，然後按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-168">In the portal, click **More services** > type load balancer in the filter box, and then click **Load Balancer**.</span></span>  
2. <span data-ttu-id="4d28d-169">選取要將後端集區新增到的負載平衡器 (mylb)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-169">Select the load balancer (*mylb*) that you want to add the backend pools to.</span></span>
3. <span data-ttu-id="4d28d-170">在 [設定] 底下選取 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-170">Under **Settings**, select **Backend Pools**.</span></span> <span data-ttu-id="4d28d-171">輸入後端集區的名稱 (例如，contosopool 或 fabrikampool)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-171">Type a name for your backend pool (for example, *contosopool* or *fabrikampool*).</span></span> <span data-ttu-id="4d28d-172">然後按一下出現的刀鋒視窗中靠近上方的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d28d-172">Then click the **Add** button toward the top of the blade that shows up.</span></span> 
4. <span data-ttu-id="4d28d-173">在 [關聯到] 中，選取 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-173">For **Associated to**, select **Availability set**.</span></span>
5. <span data-ttu-id="4d28d-174">在 [可用性設定組] 中，選取 [myAvailset]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-174">For **Availability set**, select **myAvailset**.</span></span>
6. <span data-ttu-id="4d28d-175">如下所示為這兩個 VM 新增目標網路 IP 組態 (請參閱圖 2)︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-175">Add Target network IP configurations, for both VMs as follows (see Figure 2):</span></span>  
    1. <span data-ttu-id="4d28d-176">在 [目標虛擬機器] 中，選取要新增到後端集區的 VM (例如，VM1 或 VM2)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-176">For **Target Virtual machine**, select the VM that you want to add to the backend pool (for example, VM1 or VM2).</span></span>
    2. <span data-ttu-id="4d28d-177">在 [網路 IP 組態] 中，選取該 VM 的次要 NIC IP 組態 (例如，VM1NIC2-ipconfig2 或 VM2NIC2-ipconfig2)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-177">For **Network IP configuration**, select the secondary NICs IP configuration for that VM (for example, VM1NIC2-ipconfig2 or VM2NIC2-ipconfig2).</span></span>
    <span data-ttu-id="4d28d-178">![LB 案例影像](./media/load-balancer-multiple-ip/lb-backendpool.PNG)</span><span class="sxs-lookup"><span data-stu-id="4d28d-178">![LB scenario image](./media/load-balancer-multiple-ip/lb-backendpool.PNG)</span></span>
            
        <span data-ttu-id="4d28d-179">**圖 2**︰設定具有後端集區的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="4d28d-179">**Figure 2**: Configuring the load balancer with backend pools</span></span>  
7. <span data-ttu-id="4d28d-180">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4d28d-180">Click **OK**.</span></span>
8. <span data-ttu-id="4d28d-181">當後端集區組態設定完成時，這兩個後端位址集區會顯示在負載平衡器的 [後端集區] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4d28d-181">When the backend pool configuration is complete, both backend address pools are displayed in the **Backend pool blade** of your load balancer.</span></span>

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a><span data-ttu-id="4d28d-182">步驟 5︰設定負載平衡器的健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="4d28d-182">STEP 5: Configure a health probe for your load balancer</span></span>
<span data-ttu-id="4d28d-183">設定負載平衡器的健康狀態探查，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-183">Configure a health probe for your load balancer as follows:</span></span>
    1. <span data-ttu-id="4d28d-184">在入口網站中，按一下 [更多服務]，在篩選方塊中輸入負載平衡器，然後按一下 [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-184">In the portal, click More services > type load balancer in the filter box, and then click **Load Balancer**.</span></span>  
    2. <span data-ttu-id="4d28d-185">選取要將後端集區新增到的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="4d28d-185">Select the load balancer that you want to add the backend pools to.</span></span>
    3. <span data-ttu-id="4d28d-186">在 [設定] 下，選取 [健康狀態探查]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-186">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="4d28d-187">然後按一下出現的刀鋒視窗中靠近上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-187">Then click **Add** towards the top of the blade that shows up.</span></span>
    4. <span data-ttu-id="4d28d-188">輸入健康狀態探查的名稱 (例如，HTTP)，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-188">Type a name for the health probe (for example, HTTP), and click **OK**.</span></span>

### <a name="step-6-configure-load-balancing-rules"></a><span data-ttu-id="4d28d-189">步驟 6：設定負載平衡規則</span><span class="sxs-lookup"><span data-stu-id="4d28d-189">STEP 6: Configure load balancing rules</span></span>
<span data-ttu-id="4d28d-190">為每個網站設定負載平衡規則 (HTTPc 和 HTTPf)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="4d28d-190">Configure load balancing rules (*HTTPc* and *HTTPf*) for each website as follows:</span></span>
    
1. <span data-ttu-id="4d28d-191">在 [設定] 下，選取 [健康狀態探查]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-191">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="4d28d-192">然後按一下出現的刀鋒視窗中靠近上方的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-192">Then click **Add** towards the top of the blade that shows up.</span></span>
2. <span data-ttu-id="4d28d-193">在 [名稱] 中，輸入負載平衡規則的名稱 (例如，對 Contoso 輸入 HTTPc，對 Fabrikam 則輸入 HTTPf)</span><span class="sxs-lookup"><span data-stu-id="4d28d-193">For **Name**, type a name for the load balancing rule (for example, *HTTPc* for Contoso, or *HTTPf* for Fabrikam)</span></span>
3. <span data-ttu-id="4d28d-194">在 [前端 IP 位址] 中選取前端 IP 位址 (例如，Contosofe 或 Fabrikamfe)</span><span class="sxs-lookup"><span data-stu-id="4d28d-194">For Frontend IP address, select the the frontend IP address (for example *Contosofe* or *Fabrikamfe*)</span></span>
4. <span data-ttu-id="4d28d-195">在 [連接埠] 和 [後端連接埠] 中，保留預設值 **80**。</span><span class="sxs-lookup"><span data-stu-id="4d28d-195">For **Port** and **Backend port**, keep the default value **80**.</span></span>
5. <span data-ttu-id="4d28d-196">在 [浮動 IP (伺服器直接回傳)] 中，按一下 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="4d28d-196">For **Floating IP (direct server return)**, click **Enabled**.</span></span>
6. <span data-ttu-id="4d28d-197">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="4d28d-197">Click **OK**.</span></span>
7. <span data-ttu-id="4d28d-198">重複本節中的步驟 1 到 6，以建立第二個負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="4d28d-198">Repeat steps 1 to 6 within this section to create the second Load Balancer rule.</span></span>
8. <span data-ttu-id="4d28d-199">當負載平衡規則組態設定完成時，這兩個規則 (HTTPc 和 HTTPf) 會顯示在負載平衡器的 [負載平衡規則] 刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="4d28d-199">When the load balancing rules configuration is complete, both rules ((*HTTPc* and *HTTPf*) are displayed in the **Load balancing rules** blade of your load balancer.</span></span>

### <a name="step-7-configure-dns-records"></a><span data-ttu-id="4d28d-200">步驟 7︰設定 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="4d28d-200">STEP 7: Configure DNS records</span></span>
<span data-ttu-id="4d28d-201">最後，您必須將 DNS 資源記錄設定為指向負載平衡器的個別前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4d28d-201">Finally, you must configure DNS resource records to point to the respective frontend IP address of the load balancer.</span></span> <span data-ttu-id="4d28d-202">您可以在 Azure DNS 中裝載網域。</span><span class="sxs-lookup"><span data-stu-id="4d28d-202">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="4d28d-203">如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-203">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d28d-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d28d-204">Next steps</span></span>
- <span data-ttu-id="4d28d-205">若要深入了解如何在 Azure 中合併負載平衡服務，請參閱[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-205">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="4d28d-206">若要深入了解如何在 Azure 中使用不同類型的 記錄檔來管理負載平衡器和針對其問題進行疑難排解，請參閱 [Azure Load Balancer 的 Log Analytics](../load-balancer/load-balancer-monitor-log.md)。</span><span class="sxs-lookup"><span data-stu-id="4d28d-206">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
