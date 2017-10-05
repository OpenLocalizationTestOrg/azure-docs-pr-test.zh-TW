---
title: "建立網際網路對向負載平衡器 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站在 Resource Manager 中建立網際網路面向的負載平衡器"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: db7c328b2ba7008b9d34275341fa4bad9522b028
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-the-azure-portal"></a><span data-ttu-id="dace2-103">使用 Azure 入口網站建立網際網路面向的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dace2-103">Creating an Internet-facing load balancer using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dace2-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="dace2-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="dace2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dace2-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="dace2-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dace2-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="dace2-107">範本</span><span class="sxs-lookup"><span data-stu-id="dace2-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="dace2-108">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="dace2-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="dace2-109">您也可以 [了解如何使用傳統部署建立網際網路面向的負載平衡器](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="dace2-109">You can also [Learn how to create an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

<span data-ttu-id="dace2-110">這會說明必須完成才能建立負載平衡器的個別工作順序，並詳細說明若要達到此目標需要做些什麼。</span><span class="sxs-lookup"><span data-stu-id="dace2-110">This covers the sequence of individual tasks that have to be done to create a load balancer and explain in detail what is being done to accomplish the goal.</span></span>

## <a name="what-is-required-to-create-an-internet-facing-load-balancer"></a><span data-ttu-id="dace2-111">若要建立網際網路面向的負載平衡器，需要哪些項目？</span><span class="sxs-lookup"><span data-stu-id="dace2-111">What is required to create an Internet-facing load balancer?</span></span>

<span data-ttu-id="dace2-112">您需要建立和設定下列物件以部署負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="dace2-112">You need to create and configure the following objects to deploy a load balancer.</span></span>

* <span data-ttu-id="dace2-113">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="dace2-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="dace2-114">後端位址集區 - 包含虛擬機器的網路介面 (NIC)，可從負載平衡器接收網路流量。</span><span class="sxs-lookup"><span data-stu-id="dace2-114">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="dace2-115">負載平衡規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-115">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="dace2-116">輸入 NAT 規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中特定虛擬機器之連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-116">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="dace2-117">探查 - 包含用來檢查後端位址集區中虛擬機器執行個體可用性的健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="dace2-117">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="dace2-118">您可以在 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure Resource Manager 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dace2-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-a-load-balancer-in-azure-portal"></a><span data-ttu-id="dace2-119">在 Azure 入口網站設定負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dace2-119">Set up a load balancer in Azure portal</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dace2-120">此範例假設您擁有稱為 **myVNet**的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dace2-120">This example assumes you have a virtual network called **myVNet**.</span></span> <span data-ttu-id="dace2-121">請參閱 [建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 以便進行此作業。</span><span class="sxs-lookup"><span data-stu-id="dace2-121">Refer to [create virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) to do this.</span></span> <span data-ttu-id="dace2-122">此範例也假設您有一個稱為 **LB-Subnet-BE** 的子網路 (位於 **myVNet** 內) 以及兩個分別稱為 **web1** 和 **web2** 的 VM (位於 **myVNet** 中稱為 **myAvailSet** 的相同可用性設定組內)。</span><span class="sxs-lookup"><span data-stu-id="dace2-122">It also assumes there is a subnet within **myVNet** called **LB-Subnet-BE** and two VMs called **web1** and **web2** respectively within the same availability set called **myAvailSet** in **myVNet**.</span></span> <span data-ttu-id="dace2-123">請參閱 [此連結](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以建立 VM。</span><span class="sxs-lookup"><span data-stu-id="dace2-123">Refer to [this link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to create VMs.</span></span>

1. <span data-ttu-id="dace2-124">透過瀏覽器瀏覽至 Azure 入口網站 [http://portal.azure.com](http://portal.azure.com) ，並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="dace2-124">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="dace2-125">在畫面左側選取 [新增] > [網路] > [負載平衡器]。</span><span class="sxs-lookup"><span data-stu-id="dace2-125">On the top left-hand side of the screen select **New** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="dace2-126">在 [建立負載平衡器] 刀鋒視窗中，輸入負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="dace2-126">In the **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="dace2-127">在此我們將其稱為 **myLoadBalancer**。</span><span class="sxs-lookup"><span data-stu-id="dace2-127">Here it is called **myLoadBalancer**.</span></span>
4. <span data-ttu-id="dace2-128">在 [類型] 底下選取 [公用]。</span><span class="sxs-lookup"><span data-stu-id="dace2-128">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="dace2-129">在 [公用 IP 位址] 底下建立稱為 **myPublicIP** 的新公用 IP。</span><span class="sxs-lookup"><span data-stu-id="dace2-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span></span>
6. <span data-ttu-id="dace2-130">在 [資源群組] 底下選取 [myRG] 。</span><span class="sxs-lookup"><span data-stu-id="dace2-130">Under Resource Group, select **myRG**.</span></span> <span data-ttu-id="dace2-131">選取適當 [位置]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="dace2-131">Then select an appropriate **Location**, and then click **OK**.</span></span> <span data-ttu-id="dace2-132">負載平衡器接著會開始部署，並且需要幾分鐘的時間才能順利完成部署。</span><span class="sxs-lookup"><span data-stu-id="dace2-132">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span></span>

    ![更新負載平衡器的資源群組](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a><span data-ttu-id="dace2-134">建立後端位址集區</span><span class="sxs-lookup"><span data-stu-id="dace2-134">Create a back-end address pool</span></span>

1. <span data-ttu-id="dace2-135">順利部署負載平衡器之後，請從資源內加以選取。</span><span class="sxs-lookup"><span data-stu-id="dace2-135">Once your load balancer has successfully deployed, select it from within your resources.</span></span> <span data-ttu-id="dace2-136">在 [設定] 底下選取 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="dace2-136">Under settings, select Backend Pools.</span></span> <span data-ttu-id="dace2-137">輸入後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="dace2-137">Type a name for your backend pool.</span></span> <span data-ttu-id="dace2-138">然後按一下出現的刀鋒視窗中靠近上方的 [新增]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dace2-138">Then click on the **Add** button toward the top of the blade that shows up.</span></span>
2. <span data-ttu-id="dace2-139">按一下 [新增後端集區] 刀鋒視窗中的 [新增虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="dace2-139">Click on **Add a virtual machine** in the **Add backend pool** blade.</span></span>  <span data-ttu-id="dace2-140">選取 [可用性設定組] 底下的 [選擇可用性設定組]，然後選取 [myAvailSet]。</span><span class="sxs-lookup"><span data-stu-id="dace2-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span></span> <span data-ttu-id="dace2-141">接下來，選取刀鋒視窗的 [虛擬機器] 區段底下的 [選擇虛擬機器]，然後按一下 [web1] 和 [web2]，隨即會建立兩個用於負載平衡的 VM。</span><span class="sxs-lookup"><span data-stu-id="dace2-141">Next, select **Choose the virtual machines** under the Virtual Machines section in the blade and click on **web1** and **web2**, the two VMs created for load balancing.</span></span> <span data-ttu-id="dace2-142">請確定這兩個 VM 左邊都有藍色核取記號，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="dace2-142">Ensure that both have blue check marks to the left as shown in the image below.</span></span> <span data-ttu-id="dace2-143">然後，依序按一下該刀鋒視窗中的 [選取]、[選擇虛擬機器] 刀鋒視窗中的 [確定]，以及 [新增後端集區] 刀鋒視窗中的 [確定]。</span><span class="sxs-lookup"><span data-stu-id="dace2-143">Then, click **Select** in that blade followed by OK in the **Choose Virtual machines** blade and then **OK** in the **Add backend pool** blade.</span></span>

    ![<span data-ttu-id="dace2-144">新增至後端位址集區</span><span class="sxs-lookup"><span data-stu-id="dace2-144">Adding to the backend address pool -</span></span> ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="dace2-145">檢查確定您的通知下拉式清單中有關於儲存負載平衡器後端集區的更新，以及會更新 **web1** 和 **web2** 這兩部 VM 的網路介面。</span><span class="sxs-lookup"><span data-stu-id="dace2-145">Check to make sure your notifications drop down list has an update regarding saving the load balancer backend pool in addition to updating the network interface for both the VMs **web1** and **web2**.</span></span>

## <a name="create-a-probe-lb-rule-and-nat-rules"></a><span data-ttu-id="dace2-146">建立探查、LB 規則和 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="dace2-146">Create a probe, LB rule, and NAT rules</span></span>

1. <span data-ttu-id="dace2-147">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="dace2-147">Create a health probe.</span></span>

    <span data-ttu-id="dace2-148">在負載平衡器的 [設定] 底下選取 [探查]。</span><span class="sxs-lookup"><span data-stu-id="dace2-148">Under Settings of your load balancer, select Probes.</span></span> <span data-ttu-id="dace2-149">然後按一下位於刀鋒視窗頂端的 [新增]  。</span><span class="sxs-lookup"><span data-stu-id="dace2-149">Then click **Add** located at the top of the blade.</span></span>

    <span data-ttu-id="dace2-150">有兩種方式可以設定探查：HTTP 或 TCP。</span><span class="sxs-lookup"><span data-stu-id="dace2-150">There are two ways to configure a probe: HTTP or TCP.</span></span> <span data-ttu-id="dace2-151">此範例示範 HTTP，但您可以透過類似方式設定 TCP。</span><span class="sxs-lookup"><span data-stu-id="dace2-151">This example shows HTTP, but TCP can be configured in a similar manner.</span></span>
    <span data-ttu-id="dace2-152">更新所需資訊。</span><span class="sxs-lookup"><span data-stu-id="dace2-152">Update the necessary information.</span></span> <span data-ttu-id="dace2-153">如前所述， **myLoadBalancer** 會對連接埠 80 上的流量進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="dace2-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span></span> <span data-ttu-id="dace2-154">選取的路徑為 HealthProbe.aspx、間隔為 15 秒，而狀況不良臨界值為 2。</span><span class="sxs-lookup"><span data-stu-id="dace2-154">The path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span></span> <span data-ttu-id="dace2-155">完成後，按一下 [確定]  以建立探查。</span><span class="sxs-lookup"><span data-stu-id="dace2-155">Once finished, click **OK** to create the probe.</span></span>

    <span data-ttu-id="dace2-156">將指標停留在 'i' 圖示上可深入了解這些個別組態，以及如何變更它們以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="dace2-156">Hover your pointer over the 'i' icon to learn more about these individual configurations and how they can be changed to cater to your requirements.</span></span>

    ![新增探查](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. <span data-ttu-id="dace2-158">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-158">Create a load balancer rule.</span></span>

    <span data-ttu-id="dace2-159">按一下負載平衡器的 [設定] 區段中的負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-159">Click on Load balancing rules in the Settings section of your load balancer.</span></span> <span data-ttu-id="dace2-160">在新的刀鋒視窗中按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="dace2-160">In the new blade, click on **Add**.</span></span> <span data-ttu-id="dace2-161">為規則命名。</span><span class="sxs-lookup"><span data-stu-id="dace2-161">Name your rule.</span></span> <span data-ttu-id="dace2-162">在這裡，其名稱為 HTTP。</span><span class="sxs-lookup"><span data-stu-id="dace2-162">Here, it is HTTP.</span></span> <span data-ttu-id="dace2-163">選擇前端連接埠和後端連接埠。</span><span class="sxs-lookup"><span data-stu-id="dace2-163">Choose the frontend port and Backend port.</span></span> <span data-ttu-id="dace2-164">在這裡，兩者皆選擇 80。</span><span class="sxs-lookup"><span data-stu-id="dace2-164">Here, 80 is chosen for both.</span></span> <span data-ttu-id="dace2-165">選擇 [LB-backend] 做為 [後端集區]，並以先前建立的 [HealthProbe] 做為 [探查]。</span><span class="sxs-lookup"><span data-stu-id="dace2-165">Choose **LB-backend** as your Backend pool and the previously created **HealthProbe** as the Probe.</span></span> <span data-ttu-id="dace2-166">您可以根據需求設定其他組態。</span><span class="sxs-lookup"><span data-stu-id="dace2-166">Other configurations can be set according to your requirements.</span></span> <span data-ttu-id="dace2-167">然後按一下 [確定] 以儲存負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-167">Then click OK to save the load balancing rule.</span></span>

    ![新增負載平衡規則](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. <span data-ttu-id="dace2-169">建立輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="dace2-169">Create inbound NAT rules</span></span>

    <span data-ttu-id="dace2-170">按一下負載平衡器的 [設定] 區段底下的 [輸入 NAT 規則]。</span><span class="sxs-lookup"><span data-stu-id="dace2-170">Click on Inbound NAT rules under the settings section of your load balancer.</span></span> <span data-ttu-id="dace2-171">在新的刀鋒視窗中按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="dace2-171">In the new blade that, click **Add**.</span></span> <span data-ttu-id="dace2-172">然後為輸入 NAT 規則命名。</span><span class="sxs-lookup"><span data-stu-id="dace2-172">Then name your inbound NAT rule.</span></span> <span data-ttu-id="dace2-173">在此我們將其稱為 **inboundNATrule1**。</span><span class="sxs-lookup"><span data-stu-id="dace2-173">Here it is called **inboundNATrule1**.</span></span> <span data-ttu-id="dace2-174">目的地應為先前建立的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="dace2-174">The destination should be the Public IP previously created.</span></span> <span data-ttu-id="dace2-175">選取 [服務] 底下的 [自訂]，然後選取您要使用的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="dace2-175">Select Custom under Service and select the protocol you would like to use.</span></span> <span data-ttu-id="dace2-176">此處選取 TCP。</span><span class="sxs-lookup"><span data-stu-id="dace2-176">Here TCP is selected.</span></span> <span data-ttu-id="dace2-177">輸入連接埠 3441 和目標連接埠，在此案例中 3389。</span><span class="sxs-lookup"><span data-stu-id="dace2-177">Enter the port, 3441, and the Target port, in this case, 3389.</span></span> <span data-ttu-id="dace2-178">然後按一下 [確定] 以儲存這個規則。</span><span class="sxs-lookup"><span data-stu-id="dace2-178">then click OK to save this rule.</span></span>

    <span data-ttu-id="dace2-179">在建立了第一個規則之後，從連接埠 3442 到目標連接埠 3389 針對稱為 inboundNATrule2 的第二個輸入 NAT 規則重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="dace2-179">Once the first rule is created, repeat this step for the second inbound NAT rule called inboundNATrule2 from port 3442 to Target port 3389.</span></span>

    ![新增輸入 NAT 規則](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a><span data-ttu-id="dace2-181">移除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dace2-181">Remove a Load Balancer</span></span>

<span data-ttu-id="dace2-182">若要刪除負載平衡器，請選取您要移除的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="dace2-182">To delete a load balancer, select the load balancer you want to remove.</span></span> <span data-ttu-id="dace2-183">在 [負載平衡器] 刀鋒視窗中，按一下位於刀鋒視窗頂端的 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="dace2-183">In the *Load Balancer* blade, click on **Delete** located at the top of the blade.</span></span> <span data-ttu-id="dace2-184">然後在提示時選取 [是]  。</span><span class="sxs-lookup"><span data-stu-id="dace2-184">Then select **Yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dace2-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dace2-185">Next steps</span></span>

[<span data-ttu-id="dace2-186">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dace2-186">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="dace2-187">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="dace2-187">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="dace2-188">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="dace2-188">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
