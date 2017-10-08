---
title: "aaaCreate 網際網路對向負載平衡器-Azure 入口網站 |Microsoft 文件"
description: "了解如何使用資源管理員 toocreate 網際網路對向負載平衡器 hello Azure 入口網站"
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
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a><span data-ttu-id="a2a50-103">建立使用 hello Azure 入口網站的網際網路對向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a2a50-103">Creating an Internet-facing load balancer using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a2a50-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="a2a50-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="a2a50-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2a50-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="a2a50-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a2a50-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="a2a50-107">範本</span><span class="sxs-lookup"><span data-stu-id="a2a50-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a2a50-108">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="a2a50-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="a2a50-109">您也可以[學習 toocreate 網際網路對向負載平衡器使用傳統部署的方式](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a2a50-109">You can also [Learn how toocreate an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

<span data-ttu-id="a2a50-110">這涵蓋 hello 一連串個別的工作已完成的 toobe toocreate 負載平衡器，並詳細說明什麼正在進行 tooaccomplish hello 目標。</span><span class="sxs-lookup"><span data-stu-id="a2a50-110">This covers hello sequence of individual tasks that have toobe done toocreate a load balancer and explain in detail what is being done tooaccomplish hello goal.</span></span>

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a><span data-ttu-id="a2a50-111">什麼是必要的 toocreate 網際網路對向負載平衡器？</span><span class="sxs-lookup"><span data-stu-id="a2a50-111">What is required toocreate an Internet-facing load balancer?</span></span>

<span data-ttu-id="a2a50-112">您需要 toocreate 並設定下列物件 toodeploy 負載平衡器的 hello。</span><span class="sxs-lookup"><span data-stu-id="a2a50-112">You need toocreate and configure hello following objects toodeploy a load balancer.</span></span>

* <span data-ttu-id="a2a50-113">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a2a50-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="a2a50-114">後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。</span><span class="sxs-lookup"><span data-stu-id="a2a50-114">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="a2a50-115">負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-115">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="a2a50-116">輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-116">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="a2a50-117">探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。</span><span class="sxs-lookup"><span data-stu-id="a2a50-117">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="a2a50-118">您可以在 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)中取得關於負載平衡器元件與 Azure Resource Manager 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a2a50-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-a-load-balancer-in-azure-portal"></a><span data-ttu-id="a2a50-119">在 Azure 入口網站設定負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a2a50-119">Set up a load balancer in Azure portal</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2a50-120">此範例假設您擁有稱為 **myVNet**的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a2a50-120">This example assumes you have a virtual network called **myVNet**.</span></span> <span data-ttu-id="a2a50-121">請參閱太[建立虛擬網路](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)toodo 這。</span><span class="sxs-lookup"><span data-stu-id="a2a50-121">Refer too[create virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo this.</span></span> <span data-ttu-id="a2a50-122">它也會假設沒有子網路內**myVNet**呼叫**LB 子網路是**和呼叫的兩個 Vm **web1**和**web2**分別內hello 相同可用性設定組，稱為**myAvailSet**中**myVNet**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-122">It also assumes there is a subnet within **myVNet** called **LB-Subnet-BE** and two VMs called **web1** and **web2** respectively within hello same availability set called **myAvailSet** in **myVNet**.</span></span> <span data-ttu-id="a2a50-123">請參閱太[此連結](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="a2a50-123">Refer too[this link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate VMs.</span></span>

1. <span data-ttu-id="a2a50-124">從瀏覽器瀏覽 toohello Azure 入口網站： [http://portal.azure.com](http://portal.azure.com)並使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="a2a50-124">From a browser navigate toohello Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="a2a50-125">在 hello 左邊囉 」 畫面上選取**新增** > **網路** > **負載平衡器。**</span><span class="sxs-lookup"><span data-stu-id="a2a50-125">On hello top left-hand side of hello screen select **New** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="a2a50-126">在 hello**建立負載平衡器**刀鋒視窗中，輸入您的負載平衡器的名稱。</span><span class="sxs-lookup"><span data-stu-id="a2a50-126">In hello **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="a2a50-127">在此我們將其稱為 **myLoadBalancer**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-127">Here it is called **myLoadBalancer**.</span></span>
4. <span data-ttu-id="a2a50-128">在 [類型] 底下選取 [公用]。</span><span class="sxs-lookup"><span data-stu-id="a2a50-128">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="a2a50-129">在 [公用 IP 位址] 底下建立稱為 **myPublicIP** 的新公用 IP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span></span>
6. <span data-ttu-id="a2a50-130">在 [資源群組] 底下選取 [myRG] 。</span><span class="sxs-lookup"><span data-stu-id="a2a50-130">Under Resource Group, select **myRG**.</span></span> <span data-ttu-id="a2a50-131">選取適當 位置，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="a2a50-131">Then select an appropriate **Location**, and then click **OK**.</span></span> <span data-ttu-id="a2a50-132">hello 負載平衡器會啟動 toodeploy 和 toosuccessfully 完整部署時將會需要幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="a2a50-132">hello load balancer will then start toodeploy and will take a few minutes toosuccessfully complete deployment.</span></span>

    ![更新負載平衡器的資源群組](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a><span data-ttu-id="a2a50-134">建立後端位址集區</span><span class="sxs-lookup"><span data-stu-id="a2a50-134">Create a back-end address pool</span></span>

1. <span data-ttu-id="a2a50-135">順利部署負載平衡器之後，請從資源內加以選取。</span><span class="sxs-lookup"><span data-stu-id="a2a50-135">Once your load balancer has successfully deployed, select it from within your resources.</span></span> <span data-ttu-id="a2a50-136">在 [設定] 底下選取 [後端集區]。</span><span class="sxs-lookup"><span data-stu-id="a2a50-136">Under settings, select Backend Pools.</span></span> <span data-ttu-id="a2a50-137">輸入後端集區的名稱。</span><span class="sxs-lookup"><span data-stu-id="a2a50-137">Type a name for your backend pool.</span></span> <span data-ttu-id="a2a50-138">然後按一下 hello**新增**朝 hello 顯示 hello 刀鋒視窗頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a2a50-138">Then click on hello **Add** button toward hello top of hello blade that shows up.</span></span>
2. <span data-ttu-id="a2a50-139">按一下**新增虛擬機器**在 hello**新增後端集區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2a50-139">Click on **Add a virtual machine** in hello **Add backend pool** blade.</span></span>  <span data-ttu-id="a2a50-140">選取 [可用性設定組] 底下的 [選擇可用性設定組]，然後選取 [myAvailSet]。</span><span class="sxs-lookup"><span data-stu-id="a2a50-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span></span> <span data-ttu-id="a2a50-141">接下來，選取**選擇 hello 虛擬機器**底下 hello hello 刀鋒視窗中的 虛擬機器 區段，然後按一下  **web1**和**web2**，hello 兩個 Vm 建立負載平衡。</span><span class="sxs-lookup"><span data-stu-id="a2a50-141">Next, select **Choose hello virtual machines** under hello Virtual Machines section in hello blade and click on **web1** and **web2**, hello two VMs created for load balancing.</span></span> <span data-ttu-id="a2a50-142">請確定兩者都有藍色的核取記號 toohello 左 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="a2a50-142">Ensure that both have blue check marks toohello left as shown in hello image below.</span></span> <span data-ttu-id="a2a50-143">然後按一下 **選取**hello 中後面接著確定該刀鋒視窗中**選擇虛擬機器**刀鋒視窗，然後**確定**hello 中**新增後端集區**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a2a50-143">Then, click **Select** in that blade followed by OK in hello **Choose Virtual machines** blade and then **OK** in hello **Add backend pool** blade.</span></span>

    ![<span data-ttu-id="a2a50-144">加入 toohello 後端位址集區-</span><span class="sxs-lookup"><span data-stu-id="a2a50-144">Adding toohello backend address pool -</span></span> ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="a2a50-145">檢查 toomake 確定您的通知下拉式清單中已有更新的同時 hello Vm 有關儲存 hello 負載平衡器後端集區中增加 tooupdating hello 網路介面**web1**和**web2**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-145">Check toomake sure your notifications drop down list has an update regarding saving hello load balancer backend pool in addition tooupdating hello network interface for both hello VMs **web1** and **web2**.</span></span>

## <a name="create-a-probe-lb-rule-and-nat-rules"></a><span data-ttu-id="a2a50-146">建立探查、LB 規則和 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="a2a50-146">Create a probe, LB rule, and NAT rules</span></span>

1. <span data-ttu-id="a2a50-147">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="a2a50-147">Create a health probe.</span></span>

    <span data-ttu-id="a2a50-148">在負載平衡器的 [設定] 底下選取 [探查]。</span><span class="sxs-lookup"><span data-stu-id="a2a50-148">Under Settings of your load balancer, select Probes.</span></span> <span data-ttu-id="a2a50-149">然後按一下 **新增**位於 hello hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="a2a50-149">Then click **Add** located at hello top of hello blade.</span></span>

    <span data-ttu-id="a2a50-150">有兩種方式 tooconfigure 探查： HTTP 或 TCP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-150">There are two ways tooconfigure a probe: HTTP or TCP.</span></span> <span data-ttu-id="a2a50-151">此範例示範 HTTP，但您可以透過類似方式設定 TCP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-151">This example shows HTTP, but TCP can be configured in a similar manner.</span></span>
    <span data-ttu-id="a2a50-152">更新 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="a2a50-152">Update hello necessary information.</span></span> <span data-ttu-id="a2a50-153">如前所述， **myLoadBalancer** 會對連接埠 80 上的流量進行負載平衡。</span><span class="sxs-lookup"><span data-stu-id="a2a50-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span></span> <span data-ttu-id="a2a50-154">選取的 hello 路徑為 HealthProbe.aspx、 間隔是 15 秒，而狀況不良閾值為 2。</span><span class="sxs-lookup"><span data-stu-id="a2a50-154">hello path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span></span> <span data-ttu-id="a2a50-155">完成之後，按一下**確定**toocreate hello 探查。</span><span class="sxs-lookup"><span data-stu-id="a2a50-155">Once finished, click **OK** toocreate hello probe.</span></span>

    <span data-ttu-id="a2a50-156">將指標停留 hello 'i' 圖示 toolearn 深入了解這些個別的設定，並且可變更的 toocater tooyour 需求的方式。</span><span class="sxs-lookup"><span data-stu-id="a2a50-156">Hover your pointer over hello 'i' icon toolearn more about these individual configurations and how they can be changed toocater tooyour requirements.</span></span>

    ![新增探查](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. <span data-ttu-id="a2a50-158">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-158">Create a load balancer rule.</span></span>

    <span data-ttu-id="a2a50-159">負載平衡中 hello 規則上按一下您負載平衡器的 [設定] 區段。</span><span class="sxs-lookup"><span data-stu-id="a2a50-159">Click on Load balancing rules in hello Settings section of your load balancer.</span></span> <span data-ttu-id="a2a50-160">在 hello 新刀鋒視窗中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-160">In hello new blade, click on **Add**.</span></span> <span data-ttu-id="a2a50-161">為規則命名。</span><span class="sxs-lookup"><span data-stu-id="a2a50-161">Name your rule.</span></span> <span data-ttu-id="a2a50-162">在這裡，其名稱為 HTTP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-162">Here, it is HTTP.</span></span> <span data-ttu-id="a2a50-163">選擇 hello 的前端連接埠與後端連接埠。</span><span class="sxs-lookup"><span data-stu-id="a2a50-163">Choose hello frontend port and Backend port.</span></span> <span data-ttu-id="a2a50-164">在這裡，兩者皆選擇 80。</span><span class="sxs-lookup"><span data-stu-id="a2a50-164">Here, 80 is chosen for both.</span></span> <span data-ttu-id="a2a50-165">選擇**LB 後端**做為後端集區，並且先前建立的 hello **HealthProbe**為 hello 探查。</span><span class="sxs-lookup"><span data-stu-id="a2a50-165">Choose **LB-backend** as your Backend pool and hello previously created **HealthProbe** as hello Probe.</span></span> <span data-ttu-id="a2a50-166">您可以根據 tooyour 需求設定其他組態。</span><span class="sxs-lookup"><span data-stu-id="a2a50-166">Other configurations can be set according tooyour requirements.</span></span> <span data-ttu-id="a2a50-167">然後按一下 [確定] toosave hello 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-167">Then click OK toosave hello load balancing rule.</span></span>

    ![新增負載平衡規則](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. <span data-ttu-id="a2a50-169">建立輸入 NAT 規則</span><span class="sxs-lookup"><span data-stu-id="a2a50-169">Create inbound NAT rules</span></span>

    <span data-ttu-id="a2a50-170">按一下您負載平衡器的 hello [設定] 區段下方的輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-170">Click on Inbound NAT rules under hello settings section of your load balancer.</span></span> <span data-ttu-id="a2a50-171">在 hello 新刀鋒視窗中，按一下 **新增**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-171">In hello new blade that, click **Add**.</span></span> <span data-ttu-id="a2a50-172">然後為輸入 NAT 規則命名。</span><span class="sxs-lookup"><span data-stu-id="a2a50-172">Then name your inbound NAT rule.</span></span> <span data-ttu-id="a2a50-173">在此我們將其稱為 **inboundNATrule1**。</span><span class="sxs-lookup"><span data-stu-id="a2a50-173">Here it is called **inboundNATrule1**.</span></span> <span data-ttu-id="a2a50-174">hello 目的地應該的 hello 先前建立的公用 IP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-174">hello destination should be hello Public IP previously created.</span></span> <span data-ttu-id="a2a50-175">選取服務下的 自訂，然後選取您想要 toouse hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a2a50-175">Select Custom under Service and select hello protocol you would like toouse.</span></span> <span data-ttu-id="a2a50-176">此處選取 TCP。</span><span class="sxs-lookup"><span data-stu-id="a2a50-176">Here TCP is selected.</span></span> <span data-ttu-id="a2a50-177">輸入 hello 連接埠，3441，和 hello 目標連接埠，在此情況下，3389。</span><span class="sxs-lookup"><span data-stu-id="a2a50-177">Enter hello port, 3441, and hello Target port, in this case, 3389.</span></span> <span data-ttu-id="a2a50-178">然後按一下 [確定] toosave 此規則。</span><span class="sxs-lookup"><span data-stu-id="a2a50-178">then click OK toosave this rule.</span></span>

    <span data-ttu-id="a2a50-179">Hello 第一個規則建立之後，請針對 hello 第二個輸入 NAT 規則通訊埠 3442 tooTarget 連接埠 3389 從呼叫 inboundNATrule2 重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="a2a50-179">Once hello first rule is created, repeat this step for hello second inbound NAT rule called inboundNATrule2 from port 3442 tooTarget port 3389.</span></span>

    ![新增輸入 NAT 規則](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a><span data-ttu-id="a2a50-181">移除負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a2a50-181">Remove a Load Balancer</span></span>

<span data-ttu-id="a2a50-182">toodelete 負載平衡器，您想要 tooremove 選取 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a2a50-182">toodelete a load balancer, select hello load balancer you want tooremove.</span></span> <span data-ttu-id="a2a50-183">在 hello*負載平衡器*刀鋒視窗中，按一下 **刪除**位於 hello hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="a2a50-183">In hello *Load Balancer* blade, click on **Delete** located at hello top of hello blade.</span></span> <span data-ttu-id="a2a50-184">然後在提示時選取 [是]  。</span><span class="sxs-lookup"><span data-stu-id="a2a50-184">Then select **Yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2a50-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a2a50-185">Next steps</span></span>

[<span data-ttu-id="a2a50-186">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a2a50-186">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="a2a50-187">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="a2a50-187">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a2a50-188">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="a2a50-188">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
