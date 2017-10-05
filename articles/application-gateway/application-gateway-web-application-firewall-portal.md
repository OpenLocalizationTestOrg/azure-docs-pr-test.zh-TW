---
title: "使用 Web 應用程式防火牆建立或更新 Azure 應用程式閘道 | Microsoft Docs"
description: "了解如何使用入口網站以 Web 應用程式防火牆建立應用程式閘道"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 650f26d19615d27a94f3947aad7b7904b6c1fabc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-the-portal"></a><span data-ttu-id="f1e8b-103">使用入口網站以 Web 應用程式防火牆建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f1e8b-103">Create an application gateway with web application firewall by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1e8b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f1e8b-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="f1e8b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1e8b-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="f1e8b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f1e8b-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="f1e8b-107">了解如何建立已啟用 Web 應用程式防火牆的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-107">Learn how to create a web application firewall enabled application gateway.</span></span>

<span data-ttu-id="f1e8b-108">Azure 應用程式閘道中的 Web 應用程式防火牆 (WAF) 可保護 Web 應用程式，不致遭受常見的 Web 型攻擊，例如 SQL 插入式攻擊、跨網站指令碼攻擊和工作階段攔截。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span> <span data-ttu-id="f1e8b-109">Web 應用程式可防止許多 OWASP 前 10 大常見 Web 弱點。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-109">Web application protects against many of the OWASP top 10 common web vulnerabilities.</span></span>

## <a name="scenarios"></a><span data-ttu-id="f1e8b-110">案例</span><span class="sxs-lookup"><span data-stu-id="f1e8b-110">Scenarios</span></span>

<span data-ttu-id="f1e8b-111">本文有兩個案例︰</span><span class="sxs-lookup"><span data-stu-id="f1e8b-111">In this article there are two scenarios:</span></span>

<span data-ttu-id="f1e8b-112">在第一個案例中，您會了解如何[使用 Web 應用程式防火牆來建立應用程式閘道](#create-an-application-gateway-with-web-application-firewall)</span><span class="sxs-lookup"><span data-stu-id="f1e8b-112">In the first scenario, you learn to [create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span></span>

<span data-ttu-id="f1e8b-113">在第二個案例中，您會了解如何[對現有應用程式閘道新增 Web 應用程式防火牆](#add-web-application-firewall-to-an-existing-application-gateway)。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-113">In the second scenario, you learn to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span></span>

![案例範例][scenario]

> [!NOTE]
> <span data-ttu-id="f1e8b-115">其他應用程式閘道組態 (包括自訂健康狀況探查、後端集區位址及其他規則) 會在設定應用程式閘道設定之後才進行設定，而不會在初始部署期間設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-115">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f1e8b-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="f1e8b-116">Before you begin</span></span>

<span data-ttu-id="f1e8b-117">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-117">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="f1e8b-118">建立虛擬網路時，請確定您保留足夠的位址空間，以便擁有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-118">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="f1e8b-119">將應用程式閘道部署到子網路之後，就只能將額外的應用程式閘道新增到該子網路。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-119">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

##<span data-ttu-id="f1e8b-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> 對現有應用程式閘道新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="f1e8b-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="f1e8b-121">此範例會更新現有應用程式閘道，以便在防止模式中支援 Web 應用程式防火牆。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-121">This example updates an existing application gateway to support web application firewall in prevention mode.</span></span>

1. <span data-ttu-id="f1e8b-122">在 Azure 入口網站的 [我的最愛] 窗格中，按一下 [所有資源]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-122">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="f1e8b-123">按一下 [所有資源] 刀鋒視窗中的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-123">Click the existing Application Gateway in the **All resources** blade.</span></span> <span data-ttu-id="f1e8b-124">如果您選取的訂用帳戶已有幾個資源，您可以在 [依名稱篩選...] 方塊中輸入名稱，</span><span class="sxs-lookup"><span data-stu-id="f1e8b-124">If the subscription you selected already has several resources in it, you can enter the name in the **Filter by name…**</span></span> <span data-ttu-id="f1e8b-125">輕鬆地存取 DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-125">box to easily access the DNS zone.</span></span>

   ![建立應用程式閘道][1]

1. <span data-ttu-id="f1e8b-127">按一下 [Web 應用程式防火牆]，然後更新應用程式閘道設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-127">Click **Web application firewall** and update the application gateway settings.</span></span> <span data-ttu-id="f1e8b-128">完成時，按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="f1e8b-128">When complete click **Save**</span></span>

    <span data-ttu-id="f1e8b-129">用來更新現有應用程式閘道以支援 Web 應用程式防火牆的設定如下：</span><span class="sxs-lookup"><span data-stu-id="f1e8b-129">The settings to update an existing application gateway to support web application firewall are:</span></span>

   | <span data-ttu-id="f1e8b-130">**設定**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-130">**Setting**</span></span> | <span data-ttu-id="f1e8b-131">**值**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-131">**Value**</span></span> | <span data-ttu-id="f1e8b-132">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-132">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="f1e8b-133">**升級至 WAF 層**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-133">**Upgrade to WAF Tier**</span></span>| <span data-ttu-id="f1e8b-134">已檢查</span><span class="sxs-lookup"><span data-stu-id="f1e8b-134">Checked</span></span> | <span data-ttu-id="f1e8b-135">這會將應用程式閘道層設為 WAF 層。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-135">This sets the tier of the application gateway to the WAF tier.</span></span>|
   |<span data-ttu-id="f1e8b-136">**防火牆狀態**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-136">**Firewall status**</span></span>| <span data-ttu-id="f1e8b-137">已啟用</span><span class="sxs-lookup"><span data-stu-id="f1e8b-137">Enabled</span></span> | <span data-ttu-id="f1e8b-138">此設定會在 WAF 上啟用防火牆。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-138">This setting enables the firewall on the WAF.</span></span>|
   |<span data-ttu-id="f1e8b-139">**防火牆模式**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-139">**Firewall mode**</span></span> | <span data-ttu-id="f1e8b-140">預防</span><span class="sxs-lookup"><span data-stu-id="f1e8b-140">Prevention</span></span> | <span data-ttu-id="f1e8b-141">此設定可指定 Web 應用程式防火牆處理惡意流量的方式。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-141">This setting is how web application firewall deals with malicious traffic.</span></span> <span data-ttu-id="f1e8b-142">**偵測**模式只會記錄事件，**防止**模式則會記錄事件並停止惡意流量。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-142">**Detection** mode only logs the events, where **Prevention** mode logs the events and stops the malicious traffic.</span></span>|
   |<span data-ttu-id="f1e8b-143">**規則集**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-143">**Rule set**</span></span>|<span data-ttu-id="f1e8b-144">3.0</span><span class="sxs-lookup"><span data-stu-id="f1e8b-144">3.0</span></span>|<span data-ttu-id="f1e8b-145">此設定會決定用來保護後端集區成員的[核心規則集](application-gateway-web-application-firewall-overview.md#core-rule-sets)。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-145">This setting determines the [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used to protect the backend pool members.</span></span>|
   |<span data-ttu-id="f1e8b-146">**設定已停用的規則**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-146">**Configure disabled rules**</span></span>|<span data-ttu-id="f1e8b-147">視情況而異</span><span class="sxs-lookup"><span data-stu-id="f1e8b-147">varies</span></span>|<span data-ttu-id="f1e8b-148">若要防止可能發生誤判，此設定可讓您停用某些[規則與規則群組](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-148">To prevent possible false positives, this setting allows you to disable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span></span>|

    >[!NOTE]
    > <span data-ttu-id="f1e8b-149">將現有的應用程式閘道升級至 WAF SKU 時，SKU 大小會變更為 [中型]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-149">When upgrading an existing application gateway to the WAF SKU, the SKU size changes to **medium**.</span></span> <span data-ttu-id="f1e8b-150">這可以在設定完成之後重新設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-150">This can be reconfigured after configuration is complete.</span></span>

    ![顯示基本設定的刀鋒視窗][2-1]

    > [!NOTE]
    > <span data-ttu-id="f1e8b-152">若要檢視 Web 應用程式防火牆記錄檔，必須啟用診斷功能並選取 ApplicationGatewayFirewallLog。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-152">To view web application firewall logs, diagnostics must be enabled and ApplicationGatewayFirewallLog selected.</span></span> <span data-ttu-id="f1e8b-153">若要進行測試，可以選擇執行個體計數 1。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-153">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="f1e8b-154">請務必了解 SLA 不涵蓋任何低於兩個執行個體的執行個體計數，因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-154">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="f1e8b-155">如果使用 Web 應用程式防火牆，便無法使用小型閘道。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-155">Small gateways are not available when using web application firewall.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="f1e8b-156">使用 Web 應用程式防火牆來建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="f1e8b-156">Create an application gateway with web application firewall</span></span>

<span data-ttu-id="f1e8b-157">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="f1e8b-157">This scenario will:</span></span>

* <span data-ttu-id="f1e8b-158">建立含有兩個執行個體的中型 Web 應用程式防火牆應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-158">Create a medium web application firewall application gateway with two instances.</span></span>
* <span data-ttu-id="f1e8b-159">建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-159">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="f1e8b-160">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-160">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="f1e8b-161">為 SSL 卸載設定憑證。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-161">Configure a certificate for SSL offload.</span></span>

1. <span data-ttu-id="f1e8b-162">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-162">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f1e8b-163">如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="f1e8b-163">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>
1. <span data-ttu-id="f1e8b-164">在入口網站的 [我的最愛] 窗格中，按一下 [新增]</span><span class="sxs-lookup"><span data-stu-id="f1e8b-164">In the Favorites pane of the portal, click **New**</span></span>
1. <span data-ttu-id="f1e8b-165">在 [新增] 刀鋒視窗中，按一下 [網路]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-165">In the **New** blade, click **Networking**.</span></span> <span data-ttu-id="f1e8b-166">在 [網路] 刀鋒視窗中，按一下 [應用程式閘道]，如下圖中所示：</span><span class="sxs-lookup"><span data-stu-id="f1e8b-166">In the **Networking** blade, click **Application Gateway**, as shown in the following image:</span></span>
1. <span data-ttu-id="f1e8b-167">瀏覽至 Azure 入口網站，按一下 [新增]  >  [網路]  >  [應用程式閘道]</span><span class="sxs-lookup"><span data-stu-id="f1e8b-167">Navigate to the Azure portal, click **New** > **Networking** > **Application Gateway**</span></span>

    ![建立應用程式閘道][1]

1. <span data-ttu-id="f1e8b-169">在顯示的 [基本] 刀鋒視窗中，輸入下列值，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="f1e8b-169">In the **Basics** blade that appears, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="f1e8b-170">**設定**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-170">**Setting**</span></span> | <span data-ttu-id="f1e8b-171">**值**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-171">**Value**</span></span> | <span data-ttu-id="f1e8b-172">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-172">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="f1e8b-173">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-173">**Name**</span></span>|<span data-ttu-id="f1e8b-174">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="f1e8b-174">AdatumAppGateway</span></span>|<span data-ttu-id="f1e8b-175">應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="f1e8b-175">The name of the application gateway</span></span>|
   |<span data-ttu-id="f1e8b-176">**層級**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-176">**Tier**</span></span>|<span data-ttu-id="f1e8b-177">WAF</span><span class="sxs-lookup"><span data-stu-id="f1e8b-177">WAF</span></span>|<span data-ttu-id="f1e8b-178">可用的值為「標準」或 WAF。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-178">Available values are Standard and WAF.</span></span> <span data-ttu-id="f1e8b-179">若要深入了解 WAF，請瀏覽 [Web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-179">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) to learn more about WAF.</span></span>|
   |<span data-ttu-id="f1e8b-180">**SKU 大小**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-180">**SKU Size**</span></span>|<span data-ttu-id="f1e8b-181">中型</span><span class="sxs-lookup"><span data-stu-id="f1e8b-181">Medium</span></span>|<span data-ttu-id="f1e8b-182">當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-182">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="f1e8b-183">當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-183">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="f1e8b-184">**執行個體計數**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-184">**Instance count**</span></span>|<span data-ttu-id="f1e8b-185">2</span><span class="sxs-lookup"><span data-stu-id="f1e8b-185">2</span></span>|<span data-ttu-id="f1e8b-186">高可用性的應用程式閘道執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-186">Number of instances of the application gateway for high availability.</span></span> <span data-ttu-id="f1e8b-187">執行個體計數 1 應僅用於測試目的。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-187">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="f1e8b-188">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-188">**Subscription**</span></span>|<span data-ttu-id="f1e8b-189">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="f1e8b-189">[Your subscription]</span></span>|<span data-ttu-id="f1e8b-190">選取要在其中建立應用程式閘道的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-190">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="f1e8b-191">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-191">**Resource group**</span></span>|<span data-ttu-id="f1e8b-192">**建立新項目：**AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="f1e8b-192">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="f1e8b-193">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-193">Create a resource group.</span></span> <span data-ttu-id="f1e8b-194">資源群組名稱在您選取的訂用帳戶中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-194">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="f1e8b-195">若要深入了解資源群組，請閱讀 [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) 概觀。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-195">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="f1e8b-196">**位置**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-196">**Location**</span></span>|<span data-ttu-id="f1e8b-197">美國西部</span><span class="sxs-lookup"><span data-stu-id="f1e8b-197">West US</span></span>||

   ![顯示基本設定的刀鋒視窗][2-2]

1. <span data-ttu-id="f1e8b-199">在 [虛擬網路] 底下顯示的 [設定] 刀鋒視窗中，按一下 [選擇虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-199">In the **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="f1e8b-200">此步驟會開啟進入 [選擇虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-200">This step opens enter the **Choose virtual network** blade.</span></span>  <span data-ttu-id="f1e8b-201">按一下 [建立新項目] 以開啟 [建立虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-201">Click **Create new** to open the **Create virtual network** blade.</span></span>

   ![選擇虛擬網路][2]

1. <span data-ttu-id="f1e8b-203">在 [建立虛擬網路] 刀鋒視窗中輸入下列值，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-203">On the **Create virtual network blade** enter the following values, then click **OK**.</span></span> <span data-ttu-id="f1e8b-204">此步驟會關閉 [建立虛擬網路] 和 [選擇虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-204">This step closes the **Create virtual network** and **Choose virtual network** blades.</span></span> <span data-ttu-id="f1e8b-205">這會使用所選的子網路，填入 [設定] 刀鋒視窗的 [子網路] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-205">This populates the **Subnet** field on the **Settings** blade with the subnet chosen.</span></span>

   |<span data-ttu-id="f1e8b-206">**設定**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-206">**Setting**</span></span> | <span data-ttu-id="f1e8b-207">**值**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-207">**Value**</span></span> | <span data-ttu-id="f1e8b-208">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-208">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f1e8b-209">**名稱**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-209">**Name**</span></span>|<span data-ttu-id="f1e8b-210">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="f1e8b-210">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="f1e8b-211">應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="f1e8b-211">Name of the application gateway</span></span>|
   |<span data-ttu-id="f1e8b-212">**位址空間**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-212">**Address Space**</span></span>|<span data-ttu-id="f1e8b-213">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f1e8b-213">10.0.0.0/16</span></span>| <span data-ttu-id="f1e8b-214">此值是虛擬網路的位址空間</span><span class="sxs-lookup"><span data-stu-id="f1e8b-214">This value is the address space for the virtual network</span></span>|
   |<span data-ttu-id="f1e8b-215">**子網路名稱**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-215">**Subnet name**</span></span>|<span data-ttu-id="f1e8b-216">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="f1e8b-216">AppGatewaySubnet</span></span>|<span data-ttu-id="f1e8b-217">應用程式閘道的子網路名稱</span><span class="sxs-lookup"><span data-stu-id="f1e8b-217">Name of the subnet for the application gateway</span></span>|
   |<span data-ttu-id="f1e8b-218">**子網路位址範圍**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-218">**Subnet address range**</span></span>|<span data-ttu-id="f1e8b-219">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="f1e8b-219">10.0.0.0/28</span></span> | <span data-ttu-id="f1e8b-220">這個子網路允許在虛擬網路中有更多其他的子網路，以供後端集區成員使用</span><span class="sxs-lookup"><span data-stu-id="f1e8b-220">This subnet allows more additional subnets in the virtual network for backend pool members</span></span>|

1. <span data-ttu-id="f1e8b-221">在 [前端 IP 設定] 底下的 [設定] 刀鋒視窗中，選擇 [公用] 作為 [IP 位址類型]</span><span class="sxs-lookup"><span data-stu-id="f1e8b-221">On the **Settings** blade under **Frontend IP configuration**, choose **Public** as the **IP address type**</span></span>

1. <span data-ttu-id="f1e8b-222">在 [公用 IP 位址] 底下的 [設定] 刀鋒視窗中，按一下 [選擇公用 IP 位址]。此步驟會開啟 [選擇公用 IP 位址] 刀鋒視窗，然後按一下 [建立新項目]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-222">On the **Settings** blade under **Public IP address**, click **Choose a public IP address**, this step opens the **Choose public IP address** blade, click **Create new**.</span></span>

   ![選擇公用 IP][3]

1. <span data-ttu-id="f1e8b-224">在 [建立公用 IP 位址] 刀鋒視窗中，接受預設值，並按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-224">On the **Create public IP address** blade, accept the default value, and click **OK**.</span></span> <span data-ttu-id="f1e8b-225">此步驟會關閉 [選擇公用 IP 位址] 刀鋒視窗、[建立公用 IP 位址] 刀鋒視窗，並使用所選的公用 IP 位址填入 [公用 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-225">This step closes the **Choose public IP address** blade, the **Create public IP address** blade, and populate **Public IP address** with the public IP address chosen.</span></span>

1. <span data-ttu-id="f1e8b-226">在 [接聽程式設定] 底下的 [設定] 刀鋒視窗中，按一下 [通訊協定] 底下的 [HTTP]。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-226">On the **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="f1e8b-227">若要使用 **https**，必須提供憑證。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-227">To use **https**, a certificate is required.</span></span> <span data-ttu-id="f1e8b-228">需要有憑證的私密金鑰，因此必須提供憑證的 .pfx 匯出及檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-228">The private key of the certificate is needed so a .pfx export of the certificate needs to be provided and the password for the file.</span></span>

1. <span data-ttu-id="f1e8b-229">設定 **WAF** 特定設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-229">Configure the **WAF** specific settings.</span></span>

   |<span data-ttu-id="f1e8b-230">**設定**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-230">**Setting**</span></span> | <span data-ttu-id="f1e8b-231">**值**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-231">**Value**</span></span> | <span data-ttu-id="f1e8b-232">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-232">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="f1e8b-233">**防火牆狀態**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-233">**Firewall status**</span></span>| <span data-ttu-id="f1e8b-234">已啟用</span><span class="sxs-lookup"><span data-stu-id="f1e8b-234">Enabled</span></span>| <span data-ttu-id="f1e8b-235">此設定會開啟或關閉 WAF。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-235">This setting turns WAF on or off.</span></span>|
   |<span data-ttu-id="f1e8b-236">**防火牆模式**</span><span class="sxs-lookup"><span data-stu-id="f1e8b-236">**Firewall mode**</span></span> | <span data-ttu-id="f1e8b-237">預防</span><span class="sxs-lookup"><span data-stu-id="f1e8b-237">Prevention</span></span>| <span data-ttu-id="f1e8b-238">此設定會決定 WAF 對惡意流量採取的動作。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-238">This setting determines the actions WAF takes on malicious traffic.</span></span> <span data-ttu-id="f1e8b-239">如果選擇 **偵測** ，只會記錄流量。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-239">If **Detection** is chosen, traffic is only logged.</span></span>  <span data-ttu-id="f1e8b-240">如果選擇 [防止]，則會記錄並停止流量，且產生「403 未經授權」的回應。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-240">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span></span>|


1. <span data-ttu-id="f1e8b-241">檢閱 [摘要] 頁面，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-241">Review the Summary page and click **OK**.</span></span>  <span data-ttu-id="f1e8b-242">現在應用程式閘道已排入佇列並建立。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-242">Now the application gateway is queued up and created.</span></span>

1. <span data-ttu-id="f1e8b-243">建立應用程式閘道之後，請在入口網站中瀏覽至該閘道，以繼續設定應用程式閘道組態。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-243">Once the application gateway has been created, navigate to it in the portal to continue configuration of the application gateway.</span></span>

    ![應用程式閘道資源檢視][10]

<span data-ttu-id="f1e8b-245">這些步驟會建立一個具有接聽程式、後端集區、後端 http 設定及規則之預設設定的基本應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-245">These steps create a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="f1e8b-246">佈建成功之後，您可以依據您的部署需求修改這些設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-246">You can modify these settings to suit your deployment once the provisioning is successful</span></span>

> [!NOTE]
> <span data-ttu-id="f1e8b-247">基於保護的目的，使用基本 Web 應用程式防火牆設定建立的應用程式閘道，是使用 CRS 3.0 所設定。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-247">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1e8b-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1e8b-248">Next steps</span></span>

<span data-ttu-id="f1e8b-249">接下來，您可以了解如何使用 Azure DNS 或其他 DNS 提供者，為[公用 IP 位址](../dns/dns-custom-domain.md#public-ip-address)設定自訂網域別名。</span><span class="sxs-lookup"><span data-stu-id="f1e8b-249">Next, you can learn how to configure a custom domain alias for the [public IP address](../dns/dns-custom-domain.md#public-ip-address) using Azure DNS or another DNS provider.</span></span>

<span data-ttu-id="f1e8b-250">請參閱[應用程式閘道診斷](application-gateway-diagnostics.md)，以了解如何設定診斷記錄，以及如何記錄 Web 應用程式防火牆偵測到或防止的事件</span><span class="sxs-lookup"><span data-stu-id="f1e8b-250">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="f1e8b-251">參閱 [建立自訂健康狀態探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f1e8b-251">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="f1e8b-252">參閱 [設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f1e8b-252">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
