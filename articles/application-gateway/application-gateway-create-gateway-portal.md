---
title: "aaaCreate 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello 入口網站"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a><span data-ttu-id="64acf-103">建立與 hello 入口網站應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="64acf-103">Create an application gateway with hello portal</span></span>

<span data-ttu-id="64acf-104">[應用程式閘道](application-gateway-introduction.md)是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="64acf-104">[Application Gateway](application-gateway-introduction.md) is a dedicated virtual appliance providing application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span> <span data-ttu-id="64acf-105">這篇文章帶領您完成 hello 步驟 toocreate 利用 hello Azure 入口網站，做為後端成員加入現有的伺服器應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-105">This article takes you through hello steps toocreate an Application Gateway using hello Azure portal and adding an existing server as a backend member.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="64acf-106">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="64acf-106">Log in tooAzure</span></span>

<span data-ttu-id="64acf-107">登入 toohello 在 Azure 入口網站[http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="64acf-107">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-application-gateway"></a><span data-ttu-id="64acf-108">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="64acf-108">Create application gateway</span></span>

<span data-ttu-id="64acf-109">toocreate 應用程式閘道，完成 hello 遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="64acf-109">toocreate an application gateway, complete hello steps that follow.</span></span> <span data-ttu-id="64acf-110">應用程式閘道需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="64acf-110">Application gateway requires its own subnet.</span></span> <span data-ttu-id="64acf-111">當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。</span><span class="sxs-lookup"><span data-stu-id="64acf-111">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="64acf-112">Hello 應用程式閘道部署的 tooa 子網路之後，只是其他應用程式閘道可以加入 tooit。</span><span class="sxs-lookup"><span data-stu-id="64acf-112">After hello application gateway is deployed tooa subnet, only other application gateways can be added tooit.</span></span>

1. <span data-ttu-id="64acf-113">在 hello hello 入口網站的 我的最愛 窗格，按一下 **新增**</span><span class="sxs-lookup"><span data-stu-id="64acf-113">In hello Favorites pane of hello portal, click **New**</span></span>
1. <span data-ttu-id="64acf-114">在 hello**新增**刀鋒視窗中，按一下 **網路**。</span><span class="sxs-lookup"><span data-stu-id="64acf-114">In hello **New** blade, click **Networking**.</span></span> <span data-ttu-id="64acf-115">在 hello**網路**刀鋒視窗中，按一下**應用程式閘道**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="64acf-115">In hello **Networking** blade, click **Application Gateway**, as shown in hello following image:</span></span>

    ![建立應用程式閘道][1]

1. <span data-ttu-id="64acf-117">在 hello**基本概念**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="64acf-117">In hello **Basics** blade that appears, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="64acf-118">**設定**</span><span class="sxs-lookup"><span data-stu-id="64acf-118">**Setting**</span></span> | <span data-ttu-id="64acf-119">**值**</span><span class="sxs-lookup"><span data-stu-id="64acf-119">**Value**</span></span> | <span data-ttu-id="64acf-120">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="64acf-120">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="64acf-121">**名稱**</span><span class="sxs-lookup"><span data-stu-id="64acf-121">**Name**</span></span>|<span data-ttu-id="64acf-122">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="64acf-122">AdatumAppGateway</span></span>|<span data-ttu-id="64acf-123">hello hello 應用程式閘道名稱</span><span class="sxs-lookup"><span data-stu-id="64acf-123">hello name of hello application gateway</span></span>|
   |<span data-ttu-id="64acf-124">**層級**</span><span class="sxs-lookup"><span data-stu-id="64acf-124">**Tier**</span></span>|<span data-ttu-id="64acf-125">標準</span><span class="sxs-lookup"><span data-stu-id="64acf-125">Standard</span></span>|<span data-ttu-id="64acf-126">可用的值為「標準」或 WAF。</span><span class="sxs-lookup"><span data-stu-id="64acf-126">Available values are Standard and WAF.</span></span> <span data-ttu-id="64acf-127">請瀏覽[web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)toolearn 更多關於 WAF。</span><span class="sxs-lookup"><span data-stu-id="64acf-127">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn more about WAF.</span></span>|
   |<span data-ttu-id="64acf-128">**SKU 大小**</span><span class="sxs-lookup"><span data-stu-id="64acf-128">**SKU Size**</span></span>|<span data-ttu-id="64acf-129">中型</span><span class="sxs-lookup"><span data-stu-id="64acf-129">Medium</span></span>|<span data-ttu-id="64acf-130">當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="64acf-130">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="64acf-131">當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="64acf-131">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="64acf-132">**執行個體計數**</span><span class="sxs-lookup"><span data-stu-id="64acf-132">**Instance count**</span></span>|<span data-ttu-id="64acf-133">2</span><span class="sxs-lookup"><span data-stu-id="64acf-133">2</span></span>|<span data-ttu-id="64acf-134">高可用性的 hello 應用程式閘道的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="64acf-134">Number of instances of hello application gateway for high availability.</span></span> <span data-ttu-id="64acf-135">執行個體計數 1 應僅用於測試目的。</span><span class="sxs-lookup"><span data-stu-id="64acf-135">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="64acf-136">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="64acf-136">**Subscription**</span></span>|<span data-ttu-id="64acf-137">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="64acf-137">[Your subscription]</span></span>|<span data-ttu-id="64acf-138">選取的訂用帳戶 toocreate hello 應用程式閘道中。</span><span class="sxs-lookup"><span data-stu-id="64acf-138">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="64acf-139">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="64acf-139">**Resource group**</span></span>|<span data-ttu-id="64acf-140">**建立新項目：**AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="64acf-140">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="64acf-141">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="64acf-141">Create a resource group.</span></span> <span data-ttu-id="64acf-142">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="64acf-142">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="64acf-143">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="64acf-143">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="64acf-144">**位置**</span><span class="sxs-lookup"><span data-stu-id="64acf-144">**Location**</span></span>|<span data-ttu-id="64acf-145">美國西部</span><span class="sxs-lookup"><span data-stu-id="64acf-145">West US</span></span>||

1. <span data-ttu-id="64acf-146">在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="64acf-146">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="64acf-147">hello**選擇虛擬網路**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="64acf-147">hello **Choose virtual network** blade opens.</span></span>  <span data-ttu-id="64acf-148">按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64acf-148">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

   ![選擇虛擬網路][2]

1. <span data-ttu-id="64acf-150">在 hello**刀鋒視窗中建立虛擬網路**輸入 hello 下列值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="64acf-150">On hello **Create virtual network blade** enter hello following values, then click **OK**.</span></span> <span data-ttu-id="64acf-151">hello**建立虛擬網路**和**選擇虛擬網路**關閉刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64acf-151">hello **Create virtual network** and **Choose virtual network** blades close.</span></span> <span data-ttu-id="64acf-152">此步驟中會填入 hello**子網路**欄位 hello**設定**刀鋒視窗的 選擇的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="64acf-152">This step populates hello **Subnet** field on hello **Settings** blade with hello subnet chosen.</span></span>

   | <span data-ttu-id="64acf-153">**設定**</span><span class="sxs-lookup"><span data-stu-id="64acf-153">**Setting**</span></span> | <span data-ttu-id="64acf-154">**值**</span><span class="sxs-lookup"><span data-stu-id="64acf-154">**Value**</span></span> | <span data-ttu-id="64acf-155">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="64acf-155">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="64acf-156">**名稱**</span><span class="sxs-lookup"><span data-stu-id="64acf-156">**Name**</span></span>|<span data-ttu-id="64acf-157">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="64acf-157">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="64acf-158">Hello 應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="64acf-158">Name of hello application gateway</span></span>|
   |<span data-ttu-id="64acf-159">**位址空間**</span><span class="sxs-lookup"><span data-stu-id="64acf-159">**Address Space**</span></span>|<span data-ttu-id="64acf-160">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="64acf-160">10.0.0.0/16</span></span>|<span data-ttu-id="64acf-161">這是 hello hello 虛擬網路的位址空間</span><span class="sxs-lookup"><span data-stu-id="64acf-161">This is hello address space for hello virtual network</span></span>|
   |<span data-ttu-id="64acf-162">**子網路名稱**</span><span class="sxs-lookup"><span data-stu-id="64acf-162">**Subnet name**</span></span>|<span data-ttu-id="64acf-163">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="64acf-163">AppGatewaySubnet</span></span>|<span data-ttu-id="64acf-164">Hello 應用程式閘道 hello 子網路名稱</span><span class="sxs-lookup"><span data-stu-id="64acf-164">Name of hello subnet for hello application gateway</span></span>|
   |<span data-ttu-id="64acf-165">**子網路位址範圍**</span><span class="sxs-lookup"><span data-stu-id="64acf-165">**Subnet address range**</span></span>|<span data-ttu-id="64acf-166">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="64acf-166">10.0.0.0/28</span></span>|<span data-ttu-id="64acf-167">此子網路的後端集區成員 hello 虛擬網路中允許更多的其他子網路</span><span class="sxs-lookup"><span data-stu-id="64acf-167">This subnet allows more additional subnets in hello virtual network for backend pool members</span></span>|

1. <span data-ttu-id="64acf-168">在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇**公用**為 hello **IP 位址類型**</span><span class="sxs-lookup"><span data-stu-id="64acf-168">On hello **Settings** blade under **Frontend IP configuration**, choose **Public** as hello **IP address type**</span></span>

1. <span data-ttu-id="64acf-169">在 hello**設定**刀鋒視窗底下**公用 IP 位址**按一下**選擇公用 IP 位址**，hello**選擇公用 IP 位址**刀鋒視窗中開啟按一下 **建立新**。</span><span class="sxs-lookup"><span data-stu-id="64acf-169">On hello **Settings** blade under **Public IP address** click **Choose a public IP address**, hello **Choose public IP address** blade opens, click **Create new**.</span></span>

   ![選擇公用 IP][3]

1. <span data-ttu-id="64acf-171">在 hello**建立公用 IP 位址**刀鋒視窗中，接受 hello 預設值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="64acf-171">On hello **Create public IP address** blade, accept hello default value, and click **OK**.</span></span> <span data-ttu-id="64acf-172">hello 刀鋒視窗會關閉，並於其中填入 hello**公用 IP 位址**hello 選擇公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64acf-172">hello blade closes and populates hello **Public IP address** with hello public IP address chosen.</span></span>

1. <span data-ttu-id="64acf-173">在 hello**設定**刀鋒視窗底下**接聽程式組態**，按一下  **HTTP**下**通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="64acf-173">On hello **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="64acf-174">輸入 hello hello 連接埠 toouse**連接埠**欄位。</span><span class="sxs-lookup"><span data-stu-id="64acf-174">Enter hello port toouse in hello **Port** field.</span></span>

2. <span data-ttu-id="64acf-175">按一下**確定**上 hello**設定**toocontinue 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64acf-175">Click **OK** on hello **Settings** blade toocontinue.</span></span>

1. <span data-ttu-id="64acf-176">檢閱上 hello 的 hello 設定**摘要**刀鋒視窗，然後按一下**確定**toostart 建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-176">Review hello settings on hello **Summary** blade and click **OK** toostart creation of hello application gateway.</span></span> <span data-ttu-id="64acf-177">建立應用程式閘道是長時間執行的工作，並採用時間 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="64acf-177">Creating an application gateway is a long running task and takes time toocomplete.</span></span>

## <a name="add-servers-toobackend-pools"></a><span data-ttu-id="64acf-178">新增伺服器 toobackend 集區</span><span class="sxs-lookup"><span data-stu-id="64acf-178">Add servers toobackend pools</span></span>

<span data-ttu-id="64acf-179">一旦您建立 hello 應用程式閘道時，裝載 hello 應用程式 toobe 負載平衡的 hello 系統仍然需要 toobe 加入的 toohello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-179">Once you create hello application gateway, hello systems that host hello application toobe load balanced still need toobe added toohello application gateway.</span></span> <span data-ttu-id="64acf-180">hello IP 位址、 FQDN 或 Nic 的這些伺服器會加入 toohello 後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="64acf-180">hello IP addresses, FQDN, or NICs of these servers are added toohello backend address pools.</span></span>

### <a name="ip-address-or-fqdn"></a><span data-ttu-id="64acf-181">IP 位址或 FQDN</span><span class="sxs-lookup"><span data-stu-id="64acf-181">IP Address or FQDN</span></span>

1. <span data-ttu-id="64acf-182">Hello，hello Azure 入口網站中建立的應用程式閘道與**我的最愛**] 窗格中，按一下 [**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="64acf-182">With hello application gateway created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="64acf-183">按一下 hello **AdatumAppGateway**中的應用程式閘道 hello 所有資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64acf-183">Click hello **AdatumAppGateway** application gateway in hello All resources blade.</span></span> <span data-ttu-id="64acf-184">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**AdatumAppGateway**在 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="64acf-184">If hello subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in hello **Filter by name…**</span></span> <span data-ttu-id="64acf-185">方塊 tooeasily 存取 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-185">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="64acf-186">會顯示您所建立的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-186">hello application gateway you created is displayed.</span></span> <span data-ttu-id="64acf-187">按一下**後端集區**，並選取目前後端集區 hello **appGatewayBackendPool**，hello **appGatewayBackendPool**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="64acf-187">Click **Backend pools**, and select hello current backend pool **appGatewayBackendPool**, hello **appGatewayBackendPool** blade opens.</span></span>

   ![應用程式閘道後端集區][4]

1. <span data-ttu-id="64acf-189">按一下**加入目標**tooadd IP 位址的 FQDN 值。</span><span class="sxs-lookup"><span data-stu-id="64acf-189">Click **Add Target** tooadd IP addresses of FQDN values.</span></span> <span data-ttu-id="64acf-190">選擇**IP 位址或 FQDN**為 hello**類型**hello 欄位中輸入您的 IP 位址或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="64acf-190">Choose **IP address or FQDN** as hello **Type** and enter your IP address or FQDN in hello field.</span></span> <span data-ttu-id="64acf-191">針對其他的後端集區成員重複這個步驟。</span><span class="sxs-lookup"><span data-stu-id="64acf-191">Repeat this step for additional backend pool members.</span></span> <span data-ttu-id="64acf-192">完成時，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="64acf-192">When done click **Save**.</span></span>

### <a name="virtual-machine-and-nic"></a><span data-ttu-id="64acf-193">虛擬機器和 NIC</span><span class="sxs-lookup"><span data-stu-id="64acf-193">Virtual Machine and NIC</span></span>

<span data-ttu-id="64acf-194">您也可以將虛擬機器 NIC 新增為後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="64acf-194">You can also add Virtual Machine NICs as backend pool members.</span></span> <span data-ttu-id="64acf-195">唯一的虛擬機器內 hello 與 hello 應用程式閘道相同虛擬網路都是透過 hello 下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="64acf-195">Only virtual machines within hello same virtual network as hello Application Gateway are available through hello dropdown.</span></span>

1. <span data-ttu-id="64acf-196">Hello，hello Azure 入口網站中建立的應用程式閘道與**我的最愛**] 窗格中，按一下 [**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="64acf-196">With hello application gateway created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="64acf-197">按一下 hello **AdatumAppGateway**中的應用程式閘道 hello 所有資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="64acf-197">Click hello **AdatumAppGateway** application gateway in hello All resources blade.</span></span> <span data-ttu-id="64acf-198">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**AdatumAppGateway**在 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="64acf-198">If hello subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in hello **Filter by name…**</span></span> <span data-ttu-id="64acf-199">方塊 tooeasily 存取 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-199">box tooeasily access hello application gateway.</span></span>

1. <span data-ttu-id="64acf-200">會顯示您所建立的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-200">hello application gateway you created is displayed.</span></span> <span data-ttu-id="64acf-201">按一下**後端集區**，並選取目前後端集區 hello **appGatewayBackendPool**，hello **appGatewayBackendPool**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="64acf-201">Click **Backend pools**, and select hello current backend pool **appGatewayBackendPool**, hello **appGatewayBackendPool** blade opens.</span></span>

   ![應用程式閘道後端集區][5]

1. <span data-ttu-id="64acf-203">按一下**加入目標**tooadd IP 位址的 FQDN 值。</span><span class="sxs-lookup"><span data-stu-id="64acf-203">Click **Add Target** tooadd IP addresses of FQDN values.</span></span> <span data-ttu-id="64acf-204">選擇**虛擬機器**為 hello**類型**選取 hello 虛擬機器和 NIC toouse。</span><span class="sxs-lookup"><span data-stu-id="64acf-204">Choose **Virtual Machine** as hello **Type** and select hello virtual machine and NIC toouse.</span></span> <span data-ttu-id="64acf-205">完成時，按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="64acf-205">When done click **Save**</span></span>

   > [!NOTE]
   > <span data-ttu-id="64acf-206">唯一的虛擬機器中 hello 相同虛擬網路，如 hello 下拉式方塊中的 hello 應用程式閘道可用。</span><span class="sxs-lookup"><span data-stu-id="64acf-206">Only virtual machines in hello same virtual network as hello application gateway are available in hello drop down box.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="64acf-207">清除資源</span><span class="sxs-lookup"><span data-stu-id="64acf-207">Clean up resources</span></span>

<span data-ttu-id="64acf-208">當不再需要請刪除 hello 資源群組、 應用程式閘道和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="64acf-208">When no longer needed, delete hello resource group, application gateway, and all related resources.</span></span> <span data-ttu-id="64acf-209">因此，從 hello 應用程式閘道刀鋒視窗，然後按一下 選取 hello 資源群組的 toodo**刪除**。</span><span class="sxs-lookup"><span data-stu-id="64acf-209">toodo so, select hello resource group from hello application gateway blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64acf-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64acf-210">Next steps</span></span>

<span data-ttu-id="64acf-211">在此案例中，您可以部署應用程式閘道，並加入伺服器 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="64acf-211">In this scenario, you deployed an application gateway and added a server toohello backend.</span></span> <span data-ttu-id="64acf-212">hello 下一個步驟是修改設定，並在 hello 閘道的調整規則的 tooconfigure hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="64acf-212">hello next steps are tooconfigure hello application gateway by modifying settings, and adjusting rules in hello gateway.</span></span> <span data-ttu-id="64acf-213">瀏覽下列發行項的 hello，您可以找到下列步驟：</span><span class="sxs-lookup"><span data-stu-id="64acf-213">These steps can be found by visiting hello following articles:</span></span>

<span data-ttu-id="64acf-214">了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="64acf-214">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="64acf-215">了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="64acf-215">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<span data-ttu-id="64acf-216">深入了解如何 tooprotect 應用程式與[Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)應用程式閘道的功能。</span><span class="sxs-lookup"><span data-stu-id="64acf-216">Learn how tooprotect your applications with [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) a feature of application gateway.</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
