---
title: "建立應用程式閘道 - Azure 入口網站 | Microsoft Docs"
description: "了解如何使用入口網站來建立「應用程式閘道」"
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
ms.openlocfilehash: d3c39cfe3159cd4059a81f966fb551175188278b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-with-the-portal"></a><span data-ttu-id="1429c-103">使用入口網站建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1429c-103">Create an application gateway with the portal</span></span>

<span data-ttu-id="1429c-104">[應用程式閘道](application-gateway-introduction.md)是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。</span><span class="sxs-lookup"><span data-stu-id="1429c-104">[Application Gateway](application-gateway-introduction.md) is a dedicated virtual appliance providing application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span> <span data-ttu-id="1429c-105">本文會引導您逐步進行使用 Azure 入口網站建立應用程式閘道，以及新增現有的伺服器作為後端成員。</span><span class="sxs-lookup"><span data-stu-id="1429c-105">This article takes you through the steps to create an Application Gateway using the Azure portal and adding an existing server as a backend member.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="1429c-106">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="1429c-106">Log in to Azure</span></span>

<span data-ttu-id="1429c-107">登入 Azure 入口網站，網址是 [http://portal.azure.com](http://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1429c-107">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com)</span></span>

## <a name="create-application-gateway"></a><span data-ttu-id="1429c-108">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1429c-108">Create application gateway</span></span>

<span data-ttu-id="1429c-109">若要建立應用程式閘道，您需完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="1429c-109">To create an application gateway, complete the steps that follow.</span></span> <span data-ttu-id="1429c-110">應用程式閘道需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="1429c-110">Application gateway requires its own subnet.</span></span> <span data-ttu-id="1429c-111">建立虛擬網路時，請確定您保留足夠的位址空間，以便擁有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="1429c-111">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="1429c-112">將應用程式閘道部署到子網路之後，只有其他應用程式閘道可以新增至其中。</span><span class="sxs-lookup"><span data-stu-id="1429c-112">After the application gateway is deployed to a subnet, only other application gateways can be added to it.</span></span>

1. <span data-ttu-id="1429c-113">在入口網站的 [我的最愛] 窗格中，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="1429c-113">In the Favorites pane of the portal, click **New**</span></span>
1. <span data-ttu-id="1429c-114">在 [新增] 刀鋒視窗中，按一下 [網路]。</span><span class="sxs-lookup"><span data-stu-id="1429c-114">In the **New** blade, click **Networking**.</span></span> <span data-ttu-id="1429c-115">在 [網路] 刀鋒視窗中，按一下 [應用程式閘道]，如下圖中所示：</span><span class="sxs-lookup"><span data-stu-id="1429c-115">In the **Networking** blade, click **Application Gateway**, as shown in the following image:</span></span>

    ![建立應用程式閘道][1]

1. <span data-ttu-id="1429c-117">在顯示的 [基本] 刀鋒視窗中，輸入下列值，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="1429c-117">In the **Basics** blade that appears, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="1429c-118">**設定**</span><span class="sxs-lookup"><span data-stu-id="1429c-118">**Setting**</span></span> | <span data-ttu-id="1429c-119">**值**</span><span class="sxs-lookup"><span data-stu-id="1429c-119">**Value**</span></span> | <span data-ttu-id="1429c-120">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="1429c-120">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="1429c-121">**名稱**</span><span class="sxs-lookup"><span data-stu-id="1429c-121">**Name**</span></span>|<span data-ttu-id="1429c-122">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="1429c-122">AdatumAppGateway</span></span>|<span data-ttu-id="1429c-123">應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="1429c-123">The name of the application gateway</span></span>|
   |<span data-ttu-id="1429c-124">**層級**</span><span class="sxs-lookup"><span data-stu-id="1429c-124">**Tier**</span></span>|<span data-ttu-id="1429c-125">標準</span><span class="sxs-lookup"><span data-stu-id="1429c-125">Standard</span></span>|<span data-ttu-id="1429c-126">可用的值為「標準」或 WAF。</span><span class="sxs-lookup"><span data-stu-id="1429c-126">Available values are Standard and WAF.</span></span> <span data-ttu-id="1429c-127">若要深入了解 WAF，請瀏覽 [Web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1429c-127">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) to learn more about WAF.</span></span>|
   |<span data-ttu-id="1429c-128">**SKU 大小**</span><span class="sxs-lookup"><span data-stu-id="1429c-128">**SKU Size**</span></span>|<span data-ttu-id="1429c-129">中型</span><span class="sxs-lookup"><span data-stu-id="1429c-129">Medium</span></span>|<span data-ttu-id="1429c-130">當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="1429c-130">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="1429c-131">當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="1429c-131">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="1429c-132">**執行個體計數**</span><span class="sxs-lookup"><span data-stu-id="1429c-132">**Instance count**</span></span>|<span data-ttu-id="1429c-133">2</span><span class="sxs-lookup"><span data-stu-id="1429c-133">2</span></span>|<span data-ttu-id="1429c-134">高可用性的應用程式閘道執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="1429c-134">Number of instances of the application gateway for high availability.</span></span> <span data-ttu-id="1429c-135">執行個體計數 1 應僅用於測試目的。</span><span class="sxs-lookup"><span data-stu-id="1429c-135">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="1429c-136">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="1429c-136">**Subscription**</span></span>|<span data-ttu-id="1429c-137">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="1429c-137">[Your subscription]</span></span>|<span data-ttu-id="1429c-138">選取要在其中建立應用程式閘道的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1429c-138">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="1429c-139">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="1429c-139">**Resource group**</span></span>|<span data-ttu-id="1429c-140">**建立新項目：**AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="1429c-140">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="1429c-141">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1429c-141">Create a resource group.</span></span> <span data-ttu-id="1429c-142">資源群組名稱在您選取的訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="1429c-142">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="1429c-143">若要深入了解資源群組，請閱讀 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 概觀。</span><span class="sxs-lookup"><span data-stu-id="1429c-143">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="1429c-144">**位置**</span><span class="sxs-lookup"><span data-stu-id="1429c-144">**Location**</span></span>|<span data-ttu-id="1429c-145">美國西部</span><span class="sxs-lookup"><span data-stu-id="1429c-145">West US</span></span>||

1. <span data-ttu-id="1429c-146">在 [虛擬網路] 底下顯示的 [設定] 刀鋒視窗中，按一下 [選擇虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="1429c-146">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="1429c-147">[選擇虛擬網路] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1429c-147">The **Choose virtual network** blade opens.</span></span>  <span data-ttu-id="1429c-148">按一下 [建立新項目] 以開啟 [建立虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1429c-148">Click **Create new** to open the **Create virtual network** blade.</span></span>

   ![選擇虛擬網路][2]

1. <span data-ttu-id="1429c-150">在 [建立虛擬網路] 刀鋒視窗中輸入下列值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1429c-150">On the **Create virtual network blade** enter the following values, then click **OK**.</span></span> <span data-ttu-id="1429c-151">[建立虛擬網路] 和 [選擇虛擬網路] 刀鋒視窗會關閉。</span><span class="sxs-lookup"><span data-stu-id="1429c-151">The **Create virtual network** and **Choose virtual network** blades close.</span></span> <span data-ttu-id="1429c-152">這個步驟會使用所選的子網路，填入 [設定] 刀鋒視窗的 [子網路] 欄位。</span><span class="sxs-lookup"><span data-stu-id="1429c-152">This step populates the **Subnet** field on the **Settings** blade with the subnet chosen.</span></span>

   | <span data-ttu-id="1429c-153">**設定**</span><span class="sxs-lookup"><span data-stu-id="1429c-153">**Setting**</span></span> | <span data-ttu-id="1429c-154">**值**</span><span class="sxs-lookup"><span data-stu-id="1429c-154">**Value**</span></span> | <span data-ttu-id="1429c-155">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="1429c-155">**Details**</span></span>|
   |---|---|---|
   |<span data-ttu-id="1429c-156">**名稱**</span><span class="sxs-lookup"><span data-stu-id="1429c-156">**Name**</span></span>|<span data-ttu-id="1429c-157">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="1429c-157">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="1429c-158">應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="1429c-158">Name of the application gateway</span></span>|
   |<span data-ttu-id="1429c-159">**位址空間**</span><span class="sxs-lookup"><span data-stu-id="1429c-159">**Address Space**</span></span>|<span data-ttu-id="1429c-160">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="1429c-160">10.0.0.0/16</span></span>|<span data-ttu-id="1429c-161">這是虛擬網路的位址空間</span><span class="sxs-lookup"><span data-stu-id="1429c-161">This is the address space for the virtual network</span></span>|
   |<span data-ttu-id="1429c-162">**子網路名稱**</span><span class="sxs-lookup"><span data-stu-id="1429c-162">**Subnet name**</span></span>|<span data-ttu-id="1429c-163">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="1429c-163">AppGatewaySubnet</span></span>|<span data-ttu-id="1429c-164">應用程式閘道的子網路名稱</span><span class="sxs-lookup"><span data-stu-id="1429c-164">Name of the subnet for the application gateway</span></span>|
   |<span data-ttu-id="1429c-165">**子網路位址範圍**</span><span class="sxs-lookup"><span data-stu-id="1429c-165">**Subnet address range**</span></span>|<span data-ttu-id="1429c-166">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="1429c-166">10.0.0.0/28</span></span>|<span data-ttu-id="1429c-167">這個子網路允許在虛擬網路中有更多其他的子網路，以供後端集區成員使用</span><span class="sxs-lookup"><span data-stu-id="1429c-167">This subnet allows more additional subnets in the virtual network for backend pool members</span></span>|

1. <span data-ttu-id="1429c-168">在 [前端 IP 設定] 底下的 [設定] 刀鋒視窗中，選擇 [公用] 作為 [IP 位址類型]</span><span class="sxs-lookup"><span data-stu-id="1429c-168">On the **Settings** blade under **Frontend IP configuration**, choose **Public** as the **IP address type**</span></span>

1. <span data-ttu-id="1429c-169">在 [公用 IP 位址] 底下的 [設定] 刀鋒視窗中，按一下 [選擇公用 IP 位址]，[選擇公用 IP 位址] 刀鋒視窗隨即開啟，然後按一下 [建立新項目]。</span><span class="sxs-lookup"><span data-stu-id="1429c-169">On the **Settings** blade under **Public IP address** click **Choose a public IP address**, the **Choose public IP address** blade opens, click **Create new**.</span></span>

   ![選擇公用 IP][3]

1. <span data-ttu-id="1429c-171">在 [建立公用 IP 位址] 刀鋒視窗中，接受預設值，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="1429c-171">On the **Create public IP address** blade, accept the default value, and click **OK**.</span></span> <span data-ttu-id="1429c-172">刀鋒視窗會關閉，並且以選擇的公用 IP 位址填入 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="1429c-172">The blade closes and populates the **Public IP address** with the public IP address chosen.</span></span>

1. <span data-ttu-id="1429c-173">在 [接聽程式設定] 底下的 [設定] 刀鋒視窗中，按一下 [通訊協定] 底下的 [HTTP]。</span><span class="sxs-lookup"><span data-stu-id="1429c-173">On the **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="1429c-174">輸入要在 [連接埠] 欄位中使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="1429c-174">Enter the port to use in the **Port** field.</span></span>

2. <span data-ttu-id="1429c-175">按一下 [設定] 刀鋒視窗上的 [確定] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="1429c-175">Click **OK** on the **Settings** blade to continue.</span></span>

1. <span data-ttu-id="1429c-176">檢閱 [摘要] 刀鋒視窗上的設定，然後按一下 [確定] 以開始建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-176">Review the settings on the **Summary** blade and click **OK** to start creation of the application gateway.</span></span> <span data-ttu-id="1429c-177">建立應用程式閘道是漫長的工作，而且需要一段時間才能完成。</span><span class="sxs-lookup"><span data-stu-id="1429c-177">Creating an application gateway is a long running task and takes time to complete.</span></span>

## <a name="add-servers-to-backend-pools"></a><span data-ttu-id="1429c-178">將伺服器新增到後端集區</span><span class="sxs-lookup"><span data-stu-id="1429c-178">Add servers to backend pools</span></span>

<span data-ttu-id="1429c-179">建立應用程式閘道後，仍需將裝載要進行負載平衡之應用程式的系統新增至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-179">Once you create the application gateway, the systems that host the application to be load balanced still need to be added to the application gateway.</span></span> <span data-ttu-id="1429c-180">這些伺服器的 IP 位址、FQDN 或 NIC 會新增至後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="1429c-180">The IP addresses, FQDN, or NICs of these servers are added to the backend address pools.</span></span>

### <a name="ip-address-or-fqdn"></a><span data-ttu-id="1429c-181">IP 位址或 FQDN</span><span class="sxs-lookup"><span data-stu-id="1429c-181">IP Address or FQDN</span></span>

1. <span data-ttu-id="1429c-182">建立應用程式閘道之後，在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="1429c-182">With the application gateway created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="1429c-183">按一下 [所有資源] 刀鋒視窗中的 [AdatumAppGateway] 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-183">Click the **AdatumAppGateway** application gateway in the All resources blade.</span></span> <span data-ttu-id="1429c-184">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選] 方塊中輸入 **AdatumAppGateway**</span><span class="sxs-lookup"><span data-stu-id="1429c-184">If the subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in the **Filter by name…**</span></span> <span data-ttu-id="1429c-185">輕鬆地存取應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-185">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="1429c-186">系統會顯示您建立的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-186">The application gateway you created is displayed.</span></span> <span data-ttu-id="1429c-187">按一下 [後端集區]，然後選取目前的後端集區 [appGatewayBackendPool]，[appGatewayBackendPool] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1429c-187">Click **Backend pools**, and select the current backend pool **appGatewayBackendPool**, the **appGatewayBackendPool** blade opens.</span></span>

   ![應用程式閘道後端集區][4]

1. <span data-ttu-id="1429c-189">按一下 [新增目標] 以新增 FQDN 值的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1429c-189">Click **Add Target** to add IP addresses of FQDN values.</span></span> <span data-ttu-id="1429c-190">選擇 [IP 位址或 FQDN] 當作 [類型]，並在欄位中輸入您的 IP 位址或 FQDN。</span><span class="sxs-lookup"><span data-stu-id="1429c-190">Choose **IP address or FQDN** as the **Type** and enter your IP address or FQDN in the field.</span></span> <span data-ttu-id="1429c-191">針對其他的後端集區成員重複這個步驟。</span><span class="sxs-lookup"><span data-stu-id="1429c-191">Repeat this step for additional backend pool members.</span></span> <span data-ttu-id="1429c-192">完成時，按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1429c-192">When done click **Save**.</span></span>

### <a name="virtual-machine-and-nic"></a><span data-ttu-id="1429c-193">虛擬機器和 NIC</span><span class="sxs-lookup"><span data-stu-id="1429c-193">Virtual Machine and NIC</span></span>

<span data-ttu-id="1429c-194">您也可以將虛擬機器 NIC 新增為後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="1429c-194">You can also add Virtual Machine NICs as backend pool members.</span></span> <span data-ttu-id="1429c-195">只有與應用程式閘道相同的虛擬網路內的虛擬機器可透過下拉式清單來取得。</span><span class="sxs-lookup"><span data-stu-id="1429c-195">Only virtual machines within the same virtual network as the Application Gateway are available through the dropdown.</span></span>

1. <span data-ttu-id="1429c-196">建立應用程式閘道之後，在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="1429c-196">With the application gateway created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="1429c-197">按一下 [所有資源] 刀鋒視窗中的 [AdatumAppGateway] 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-197">Click the **AdatumAppGateway** application gateway in the All resources blade.</span></span> <span data-ttu-id="1429c-198">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選] 方塊中輸入 **AdatumAppGateway**</span><span class="sxs-lookup"><span data-stu-id="1429c-198">If the subscription you selected already has several resources in it, you can enter **AdatumAppGateway** in the **Filter by name…**</span></span> <span data-ttu-id="1429c-199">輕鬆地存取應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-199">box to easily access the application gateway.</span></span>

1. <span data-ttu-id="1429c-200">系統會顯示您建立的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1429c-200">The application gateway you created is displayed.</span></span> <span data-ttu-id="1429c-201">按一下 [後端集區]，然後選取目前的後端集區 [appGatewayBackendPool]，[appGatewayBackendPool] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1429c-201">Click **Backend pools**, and select the current backend pool **appGatewayBackendPool**, the **appGatewayBackendPool** blade opens.</span></span>

   ![應用程式閘道後端集區][5]

1. <span data-ttu-id="1429c-203">按一下 [新增目標] 以新增 FQDN 值的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1429c-203">Click **Add Target** to add IP addresses of FQDN values.</span></span> <span data-ttu-id="1429c-204">選擇 [虛擬機器] 當作 [類型]，並選取要使用的虛擬機器和 NIC。</span><span class="sxs-lookup"><span data-stu-id="1429c-204">Choose **Virtual Machine** as the **Type** and select the virtual machine and NIC to use.</span></span> <span data-ttu-id="1429c-205">完成時，按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="1429c-205">When done click **Save**</span></span>

   > [!NOTE]
   > <span data-ttu-id="1429c-206">下拉式方塊中只提供位於應用程式閘道相同虛擬網路內的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1429c-206">Only virtual machines in the same virtual network as the application gateway are available in the drop down box.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1429c-207">清除資源</span><span class="sxs-lookup"><span data-stu-id="1429c-207">Clean up resources</span></span>

<span data-ttu-id="1429c-208">若不再需要，可刪除資源群組、應用程式閘道和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="1429c-208">When no longer needed, delete the resource group, application gateway, and all related resources.</span></span> <span data-ttu-id="1429c-209">若要這樣做，請選取應用程式閘道刀鋒視窗中的資源群組，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="1429c-209">To do so, select the resource group from the application gateway blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1429c-210">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1429c-210">Next steps</span></span>

<span data-ttu-id="1429c-211">在此案例中，您部署應用程式閘道，並且將伺服器新增至後端。</span><span class="sxs-lookup"><span data-stu-id="1429c-211">In this scenario, you deployed an application gateway and added a server to the backend.</span></span> <span data-ttu-id="1429c-212">後續步驟用於設定應用程式閘道，方法是修改設定，以及調整閘道中的規則。</span><span class="sxs-lookup"><span data-stu-id="1429c-212">The next steps are to configure the application gateway by modifying settings, and adjusting rules in the gateway.</span></span> <span data-ttu-id="1429c-213">瀏覽下列文章即可找到這些步驟：</span><span class="sxs-lookup"><span data-stu-id="1429c-213">These steps can be found by visiting the following articles:</span></span>

<span data-ttu-id="1429c-214">參閱 [建立自訂健康狀態探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1429c-214">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="1429c-215">參閱 [設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1429c-215">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<span data-ttu-id="1429c-216">了解如何使用應用程式閘道的功能 - [Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)來保護您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1429c-216">Learn how to protect your applications with [Web Application Firewall](application-gateway-webapplicationfirewall-overview.md) a feature of application gateway.</span></span>

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
