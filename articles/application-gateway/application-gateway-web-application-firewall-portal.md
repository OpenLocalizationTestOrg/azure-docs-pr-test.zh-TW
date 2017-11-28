---
title: "aaaCreate 或更新 Azure 應用程式閘道與 web 應用程式防火牆 |Microsoft 文件"
description: "了解如何 toocreate 應用程式閘道使用的 web 應用程式防火牆 hello 入口網站"
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
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a><span data-ttu-id="28bb8-103">建立 web 應用程式防火牆使用 hello 入口網站應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="28bb8-103">Create an application gateway with web application firewall by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="28bb8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="28bb8-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="28bb8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="28bb8-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="28bb8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="28bb8-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="28bb8-107">了解如何 toocreate web 應用程式防火牆啟用應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="28bb8-107">Learn how toocreate a web application firewall enabled application gateway.</span></span>

<span data-ttu-id="28bb8-108">hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道會從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若保護 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="28bb8-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span> <span data-ttu-id="28bb8-109">Web 應用程式可防止許多 hello OWASP 前 10 個常見 web 弱點。</span><span class="sxs-lookup"><span data-stu-id="28bb8-109">Web application protects against many of hello OWASP top 10 common web vulnerabilities.</span></span>

## <a name="scenarios"></a><span data-ttu-id="28bb8-110">案例</span><span class="sxs-lookup"><span data-stu-id="28bb8-110">Scenarios</span></span>

<span data-ttu-id="28bb8-111">本文有兩個案例︰</span><span class="sxs-lookup"><span data-stu-id="28bb8-111">In this article there are two scenarios:</span></span>

<span data-ttu-id="28bb8-112">在 hello 第一個案例中，您學會太[建立 web 應用程式防火牆應用程式閘道](#create-an-application-gateway-with-web-application-firewall)</span><span class="sxs-lookup"><span data-stu-id="28bb8-112">In hello first scenario, you learn too[create an application gateway with web application firewall](#create-an-application-gateway-with-web-application-firewall)</span></span>

<span data-ttu-id="28bb8-113">在 hello 第二個案例中，您學會太[加入 web 應用程式防火牆 tooan 現有應用程式閘道](#add-web-application-firewall-to-an-existing-application-gateway)。</span><span class="sxs-lookup"><span data-stu-id="28bb8-113">In hello second scenario, you learn too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway).</span></span>

![案例範例][scenario]

> [!NOTE]
> <span data-ttu-id="28bb8-115">額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。</span><span class="sxs-lookup"><span data-stu-id="28bb8-115">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28bb8-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="28bb8-116">Before you begin</span></span>

<span data-ttu-id="28bb8-117">「Azure 應用程式閘道」需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-117">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="28bb8-118">當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-118">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="28bb8-119">一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道就能 toobe 加入 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-119">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

##<span data-ttu-id="28bb8-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a>加入 web 應用程式防火牆 tooan 現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="28bb8-120"><a name="add-web-application-firewall-to-an-existing-application-gateway"></a> Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="28bb8-121">這個範例會更新現有應用程式閘道 toosupport web 應用程式的防火牆防止模式中。</span><span class="sxs-lookup"><span data-stu-id="28bb8-121">This example updates an existing application gateway toosupport web application firewall in prevention mode.</span></span>

1. <span data-ttu-id="28bb8-122">在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-122">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="28bb8-123">按一下 hello hello 中的現有應用程式閘道**所有資源**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28bb8-123">Click hello existing Application Gateway in hello **All resources** blade.</span></span> <span data-ttu-id="28bb8-124">如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 名稱 hello**依名稱篩選...**</span><span class="sxs-lookup"><span data-stu-id="28bb8-124">If hello subscription you selected already has several resources in it, you can enter hello name in hello **Filter by name…**</span></span> <span data-ttu-id="28bb8-125">方塊 tooeasily 存取 hello DNS 區域。</span><span class="sxs-lookup"><span data-stu-id="28bb8-125">box tooeasily access hello DNS zone.</span></span>

   ![建立應用程式閘道][1]

1. <span data-ttu-id="28bb8-127">按一下**Web 應用程式防火牆**並更新 hello 應用程式閘道設定。</span><span class="sxs-lookup"><span data-stu-id="28bb8-127">Click **Web application firewall** and update hello application gateway settings.</span></span> <span data-ttu-id="28bb8-128">完成時，按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="28bb8-128">When complete click **Save**</span></span>

    <span data-ttu-id="28bb8-129">hello 設定 tooupdate 現有應用程式閘道 toosupport web 應用程式的防火牆是：</span><span class="sxs-lookup"><span data-stu-id="28bb8-129">hello settings tooupdate an existing application gateway toosupport web application firewall are:</span></span>

   | <span data-ttu-id="28bb8-130">**設定**</span><span class="sxs-lookup"><span data-stu-id="28bb8-130">**Setting**</span></span> | <span data-ttu-id="28bb8-131">**值**</span><span class="sxs-lookup"><span data-stu-id="28bb8-131">**Value**</span></span> | <span data-ttu-id="28bb8-132">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="28bb8-132">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="28bb8-133">**升級 tooWAF 層**</span><span class="sxs-lookup"><span data-stu-id="28bb8-133">**Upgrade tooWAF Tier**</span></span>| <span data-ttu-id="28bb8-134">已檢查</span><span class="sxs-lookup"><span data-stu-id="28bb8-134">Checked</span></span> | <span data-ttu-id="28bb8-135">這會設定 hello 應用程式閘道 toohello WAF 層 hello 層。</span><span class="sxs-lookup"><span data-stu-id="28bb8-135">This sets hello tier of hello application gateway toohello WAF tier.</span></span>|
   |<span data-ttu-id="28bb8-136">**防火牆狀態**</span><span class="sxs-lookup"><span data-stu-id="28bb8-136">**Firewall status**</span></span>| <span data-ttu-id="28bb8-137">已啟用</span><span class="sxs-lookup"><span data-stu-id="28bb8-137">Enabled</span></span> | <span data-ttu-id="28bb8-138">此設定可讓 hello WAF hello 防火牆。</span><span class="sxs-lookup"><span data-stu-id="28bb8-138">This setting enables hello firewall on hello WAF.</span></span>|
   |<span data-ttu-id="28bb8-139">**防火牆模式**</span><span class="sxs-lookup"><span data-stu-id="28bb8-139">**Firewall mode**</span></span> | <span data-ttu-id="28bb8-140">預防</span><span class="sxs-lookup"><span data-stu-id="28bb8-140">Prevention</span></span> | <span data-ttu-id="28bb8-141">此設定可指定 Web 應用程式防火牆處理惡意流量的方式。</span><span class="sxs-lookup"><span data-stu-id="28bb8-141">This setting is how web application firewall deals with malicious traffic.</span></span> <span data-ttu-id="28bb8-142">**偵測**模式只會記錄 hello 事件，其中**防止**模式 hello 事件記錄和停駐點 hello 惡意流量。</span><span class="sxs-lookup"><span data-stu-id="28bb8-142">**Detection** mode only logs hello events, where **Prevention** mode logs hello events and stops hello malicious traffic.</span></span>|
   |<span data-ttu-id="28bb8-143">**規則集**</span><span class="sxs-lookup"><span data-stu-id="28bb8-143">**Rule set**</span></span>|<span data-ttu-id="28bb8-144">3.0</span><span class="sxs-lookup"><span data-stu-id="28bb8-144">3.0</span></span>|<span data-ttu-id="28bb8-145">此設定會決定 hello[核心規則集](application-gateway-web-application-firewall-overview.md#core-rule-sets)也就是使用的 tooprotect hello 後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="28bb8-145">This setting determines hello [core rule set](application-gateway-web-application-firewall-overview.md#core-rule-sets) that is used tooprotect hello backend pool members.</span></span>|
   |<span data-ttu-id="28bb8-146">**設定已停用的規則**</span><span class="sxs-lookup"><span data-stu-id="28bb8-146">**Configure disabled rules**</span></span>|<span data-ttu-id="28bb8-147">視情況而異</span><span class="sxs-lookup"><span data-stu-id="28bb8-147">varies</span></span>|<span data-ttu-id="28bb8-148">tooprevent 可能誤判，此設定可讓您 toodisable 特定[規則與規則群組](application-gateway-crs-rulegroups-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="28bb8-148">tooprevent possible false positives, this setting allows you toodisable certain [rules and rule groups](application-gateway-crs-rulegroups-rules.md).</span></span>|

    >[!NOTE]
    > <span data-ttu-id="28bb8-149">Hello SKU 升級現有的應用程式閘道 toohello WAF SKU，太調整大小變更**媒體**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-149">When upgrading an existing application gateway toohello WAF SKU, hello SKU size changes too**medium**.</span></span> <span data-ttu-id="28bb8-150">這可以在設定完成之後重新設定。</span><span class="sxs-lookup"><span data-stu-id="28bb8-150">This can be reconfigured after configuration is complete.</span></span>

    ![顯示基本設定的刀鋒視窗][2-1]

    > [!NOTE]
    > <span data-ttu-id="28bb8-152">必須啟用 tooview web 應用程式防火牆記錄檔，診斷和 ApplicationGatewayFirewallLog 選取。</span><span class="sxs-lookup"><span data-stu-id="28bb8-152">tooview web application firewall logs, diagnostics must be enabled and ApplicationGatewayFirewallLog selected.</span></span> <span data-ttu-id="28bb8-153">若要進行測試，可以選擇執行個體計數 1。</span><span class="sxs-lookup"><span data-stu-id="28bb8-153">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="28bb8-154">請務必 tooknow 任何執行個體計數在兩個執行個體未涵蓋 hello SLA，並因此不建議使用。</span><span class="sxs-lookup"><span data-stu-id="28bb8-154">It is important tooknow that any instance count under two instances is not covered by hello SLA and are therefore not recommended.</span></span> <span data-ttu-id="28bb8-155">如果使用 Web 應用程式防火牆，便無法使用小型閘道。</span><span class="sxs-lookup"><span data-stu-id="28bb8-155">Small gateways are not available when using web application firewall.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="28bb8-156">使用 Web 應用程式防火牆來建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="28bb8-156">Create an application gateway with web application firewall</span></span>

<span data-ttu-id="28bb8-157">此案例將會：</span><span class="sxs-lookup"><span data-stu-id="28bb8-157">This scenario will:</span></span>

* <span data-ttu-id="28bb8-158">建立含有兩個執行個體的中型 Web 應用程式防火牆應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="28bb8-158">Create a medium web application firewall application gateway with two instances.</span></span>
* <span data-ttu-id="28bb8-159">建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-159">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="28bb8-160">建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-160">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="28bb8-161">為 SSL 卸載設定憑證。</span><span class="sxs-lookup"><span data-stu-id="28bb8-161">Configure a certificate for SSL offload.</span></span>

1. <span data-ttu-id="28bb8-162">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="28bb8-162">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="28bb8-163">如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="28bb8-163">If you don't already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free)</span></span>
1. <span data-ttu-id="28bb8-164">在 hello hello 入口網站的 我的最愛 窗格，按一下 **新增**</span><span class="sxs-lookup"><span data-stu-id="28bb8-164">In hello Favorites pane of hello portal, click **New**</span></span>
1. <span data-ttu-id="28bb8-165">在 hello**新增**刀鋒視窗中，按一下 **網路**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-165">In hello **New** blade, click **Networking**.</span></span> <span data-ttu-id="28bb8-166">在 hello**網路**刀鋒視窗中，按一下**應用程式閘道**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="28bb8-166">In hello **Networking** blade, click **Application Gateway**, as shown in hello following image:</span></span>
1. <span data-ttu-id="28bb8-167">瀏覽 toohello Azure 入口網站中，按一下**新增** > **網路** > **應用程式閘道**</span><span class="sxs-lookup"><span data-stu-id="28bb8-167">Navigate toohello Azure portal, click **New** > **Networking** > **Application Gateway**</span></span>

    ![建立應用程式閘道][1]

1. <span data-ttu-id="28bb8-169">在 hello**基本概念**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="28bb8-169">In hello **Basics** blade that appears, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="28bb8-170">**設定**</span><span class="sxs-lookup"><span data-stu-id="28bb8-170">**Setting**</span></span> | <span data-ttu-id="28bb8-171">**值**</span><span class="sxs-lookup"><span data-stu-id="28bb8-171">**Value**</span></span> | <span data-ttu-id="28bb8-172">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="28bb8-172">**Details**</span></span>
   |---|---|---|
   |<span data-ttu-id="28bb8-173">**名稱**</span><span class="sxs-lookup"><span data-stu-id="28bb8-173">**Name**</span></span>|<span data-ttu-id="28bb8-174">AdatumAppGateway</span><span class="sxs-lookup"><span data-stu-id="28bb8-174">AdatumAppGateway</span></span>|<span data-ttu-id="28bb8-175">hello hello 應用程式閘道名稱</span><span class="sxs-lookup"><span data-stu-id="28bb8-175">hello name of hello application gateway</span></span>|
   |<span data-ttu-id="28bb8-176">**層級**</span><span class="sxs-lookup"><span data-stu-id="28bb8-176">**Tier**</span></span>|<span data-ttu-id="28bb8-177">WAF</span><span class="sxs-lookup"><span data-stu-id="28bb8-177">WAF</span></span>|<span data-ttu-id="28bb8-178">可用的值為「標準」或 WAF。</span><span class="sxs-lookup"><span data-stu-id="28bb8-178">Available values are Standard and WAF.</span></span> <span data-ttu-id="28bb8-179">請瀏覽[web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)toolearn 更多關於 WAF。</span><span class="sxs-lookup"><span data-stu-id="28bb8-179">Visit [web application firewall](application-gateway-web-application-firewall-overview.md) toolearn more about WAF.</span></span>|
   |<span data-ttu-id="28bb8-180">**SKU 大小**</span><span class="sxs-lookup"><span data-stu-id="28bb8-180">**SKU Size**</span></span>|<span data-ttu-id="28bb8-181">中型</span><span class="sxs-lookup"><span data-stu-id="28bb8-181">Medium</span></span>|<span data-ttu-id="28bb8-182">當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="28bb8-182">Choices when choosing Standard tier are Small, Medium, and Large.</span></span> <span data-ttu-id="28bb8-183">當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。</span><span class="sxs-lookup"><span data-stu-id="28bb8-183">When choosing WAF tier, options are Medium and Large only.</span></span>|
   |<span data-ttu-id="28bb8-184">**執行個體計數**</span><span class="sxs-lookup"><span data-stu-id="28bb8-184">**Instance count**</span></span>|<span data-ttu-id="28bb8-185">2</span><span class="sxs-lookup"><span data-stu-id="28bb8-185">2</span></span>|<span data-ttu-id="28bb8-186">高可用性的 hello 應用程式閘道的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="28bb8-186">Number of instances of hello application gateway for high availability.</span></span> <span data-ttu-id="28bb8-187">執行個體計數 1 應僅用於測試目的。</span><span class="sxs-lookup"><span data-stu-id="28bb8-187">Instance counts of 1 should only be used for testing purposes.</span></span>|
   |<span data-ttu-id="28bb8-188">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="28bb8-188">**Subscription**</span></span>|<span data-ttu-id="28bb8-189">[您的訂用帳戶]</span><span class="sxs-lookup"><span data-stu-id="28bb8-189">[Your subscription]</span></span>|<span data-ttu-id="28bb8-190">選取的訂用帳戶 toocreate hello 應用程式閘道中。</span><span class="sxs-lookup"><span data-stu-id="28bb8-190">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="28bb8-191">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="28bb8-191">**Resource group**</span></span>|<span data-ttu-id="28bb8-192">**建立新項目：**AdatumAppGatewayRG</span><span class="sxs-lookup"><span data-stu-id="28bb8-192">**Create new:** AdatumAppGatewayRG</span></span>|<span data-ttu-id="28bb8-193">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="28bb8-193">Create a resource group.</span></span> <span data-ttu-id="28bb8-194">hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="28bb8-194">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="28bb8-195">深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups)概觀文件。</span><span class="sxs-lookup"><span data-stu-id="28bb8-195">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="28bb8-196">**位置**</span><span class="sxs-lookup"><span data-stu-id="28bb8-196">**Location**</span></span>|<span data-ttu-id="28bb8-197">美國西部</span><span class="sxs-lookup"><span data-stu-id="28bb8-197">West US</span></span>||

   ![顯示基本設定的刀鋒視窗][2-2]

1. <span data-ttu-id="28bb8-199">在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-199">In hello **Settings** blade that appears under **Virtual network**, click **Choose a virtual network**.</span></span> <span data-ttu-id="28bb8-200">此步驟會開啟輸入 hello**選擇虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28bb8-200">This step opens enter hello **Choose virtual network** blade.</span></span>  <span data-ttu-id="28bb8-201">按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28bb8-201">Click **Create new** tooopen hello **Create virtual network** blade.</span></span>

   ![選擇虛擬網路][2]

1. <span data-ttu-id="28bb8-203">在 hello**刀鋒視窗中建立虛擬網路**輸入 hello 下列值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-203">On hello **Create virtual network blade** enter hello following values, then click **OK**.</span></span> <span data-ttu-id="28bb8-204">此步驟會關閉 hello**建立虛擬網路**和**選擇虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="28bb8-204">This step closes hello **Create virtual network** and **Choose virtual network** blades.</span></span> <span data-ttu-id="28bb8-205">如此即會填入 hello**子網路**欄位 hello**設定**刀鋒視窗的 選擇的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="28bb8-205">This populates hello **Subnet** field on hello **Settings** blade with hello subnet chosen.</span></span>

   |<span data-ttu-id="28bb8-206">**設定**</span><span class="sxs-lookup"><span data-stu-id="28bb8-206">**Setting**</span></span> | <span data-ttu-id="28bb8-207">**值**</span><span class="sxs-lookup"><span data-stu-id="28bb8-207">**Value**</span></span> | <span data-ttu-id="28bb8-208">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="28bb8-208">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="28bb8-209">**名稱**</span><span class="sxs-lookup"><span data-stu-id="28bb8-209">**Name**</span></span>|<span data-ttu-id="28bb8-210">AdatumAppGatewayVNET</span><span class="sxs-lookup"><span data-stu-id="28bb8-210">AdatumAppGatewayVNET</span></span>|<span data-ttu-id="28bb8-211">Hello 應用程式閘道的名稱</span><span class="sxs-lookup"><span data-stu-id="28bb8-211">Name of hello application gateway</span></span>|
   |<span data-ttu-id="28bb8-212">**位址空間**</span><span class="sxs-lookup"><span data-stu-id="28bb8-212">**Address Space**</span></span>|<span data-ttu-id="28bb8-213">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="28bb8-213">10.0.0.0/16</span></span>| <span data-ttu-id="28bb8-214">此值為 hello hello 虛擬網路的位址空間</span><span class="sxs-lookup"><span data-stu-id="28bb8-214">This value is hello address space for hello virtual network</span></span>|
   |<span data-ttu-id="28bb8-215">**子網路名稱**</span><span class="sxs-lookup"><span data-stu-id="28bb8-215">**Subnet name**</span></span>|<span data-ttu-id="28bb8-216">AppGatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="28bb8-216">AppGatewaySubnet</span></span>|<span data-ttu-id="28bb8-217">Hello 應用程式閘道 hello 子網路名稱</span><span class="sxs-lookup"><span data-stu-id="28bb8-217">Name of hello subnet for hello application gateway</span></span>|
   |<span data-ttu-id="28bb8-218">**子網路位址範圍**</span><span class="sxs-lookup"><span data-stu-id="28bb8-218">**Subnet address range**</span></span>|<span data-ttu-id="28bb8-219">10.0.0.0/28</span><span class="sxs-lookup"><span data-stu-id="28bb8-219">10.0.0.0/28</span></span> | <span data-ttu-id="28bb8-220">此子網路的後端集區成員 hello 虛擬網路中允許更多的其他子網路</span><span class="sxs-lookup"><span data-stu-id="28bb8-220">This subnet allows more additional subnets in hello virtual network for backend pool members</span></span>|

1. <span data-ttu-id="28bb8-221">在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇**公用**為 hello **IP 位址類型**</span><span class="sxs-lookup"><span data-stu-id="28bb8-221">On hello **Settings** blade under **Frontend IP configuration**, choose **Public** as hello **IP address type**</span></span>

1. <span data-ttu-id="28bb8-222">在 hello**設定**刀鋒視窗底下**公用 IP 位址**，按一下 **選擇公用 IP 位址**，此步驟會開啟 hello**選擇公用 IP 位址**刀鋒視窗中，按一下 **建立新**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-222">On hello **Settings** blade under **Public IP address**, click **Choose a public IP address**, this step opens hello **Choose public IP address** blade, click **Create new**.</span></span>

   ![選擇公用 IP][3]

1. <span data-ttu-id="28bb8-224">在 hello**建立公用 IP 位址**刀鋒視窗中，接受 hello 預設值，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-224">On hello **Create public IP address** blade, accept hello default value, and click **OK**.</span></span> <span data-ttu-id="28bb8-225">此步驟會關閉 hello**選擇公用 IP 位址**刀鋒視窗，hello**建立公用 IP 位址**刀鋒視窗中，並填入**公用 IP 位址**hello 選擇公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="28bb8-225">This step closes hello **Choose public IP address** blade, hello **Create public IP address** blade, and populate **Public IP address** with hello public IP address chosen.</span></span>

1. <span data-ttu-id="28bb8-226">在 hello**設定**刀鋒視窗底下**接聽程式組態**，按一下  **HTTP**下**通訊協定**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-226">On hello **Settings** blade under **Listener configuration**, click **HTTP** under **Protocol**.</span></span> <span data-ttu-id="28bb8-227">toouse **https**，都需要的憑證。</span><span class="sxs-lookup"><span data-stu-id="28bb8-227">toouse **https**, a certificate is required.</span></span> <span data-ttu-id="28bb8-228">被需要 hello hello 憑證私密金鑰，因此必須提供 toobe hello 憑證的.pfx 匯出，而且 hello hello 檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="28bb8-228">hello private key of hello certificate is needed so a .pfx export of hello certificate needs toobe provided and hello password for hello file.</span></span>

1. <span data-ttu-id="28bb8-229">設定 hello **WAF**特定設定。</span><span class="sxs-lookup"><span data-stu-id="28bb8-229">Configure hello **WAF** specific settings.</span></span>

   |<span data-ttu-id="28bb8-230">**設定**</span><span class="sxs-lookup"><span data-stu-id="28bb8-230">**Setting**</span></span> | <span data-ttu-id="28bb8-231">**值**</span><span class="sxs-lookup"><span data-stu-id="28bb8-231">**Value**</span></span> | <span data-ttu-id="28bb8-232">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="28bb8-232">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="28bb8-233">**防火牆狀態**</span><span class="sxs-lookup"><span data-stu-id="28bb8-233">**Firewall status**</span></span>| <span data-ttu-id="28bb8-234">已啟用</span><span class="sxs-lookup"><span data-stu-id="28bb8-234">Enabled</span></span>| <span data-ttu-id="28bb8-235">此設定會開啟或關閉 WAF。</span><span class="sxs-lookup"><span data-stu-id="28bb8-235">This setting turns WAF on or off.</span></span>|
   |<span data-ttu-id="28bb8-236">**防火牆模式**</span><span class="sxs-lookup"><span data-stu-id="28bb8-236">**Firewall mode**</span></span> | <span data-ttu-id="28bb8-237">預防</span><span class="sxs-lookup"><span data-stu-id="28bb8-237">Prevention</span></span>| <span data-ttu-id="28bb8-238">此設定會決定 hello 動作 WAF 接替惡意流量。</span><span class="sxs-lookup"><span data-stu-id="28bb8-238">This setting determines hello actions WAF takes on malicious traffic.</span></span> <span data-ttu-id="28bb8-239">如果選擇 **偵測** ，只會記錄流量。</span><span class="sxs-lookup"><span data-stu-id="28bb8-239">If **Detection** is chosen, traffic is only logged.</span></span>  <span data-ttu-id="28bb8-240">如果選擇 [防止]，則會記錄並停止流量，且產生「403 未經授權」的回應。</span><span class="sxs-lookup"><span data-stu-id="28bb8-240">If **Prevention** is chosen, traffic is logged and stopped with a 403 Unauthorized response.</span></span>|


1. <span data-ttu-id="28bb8-241">檢閱 hello 摘要] 頁面上，按一下 [**確定**。</span><span class="sxs-lookup"><span data-stu-id="28bb8-241">Review hello Summary page and click **OK**.</span></span>  <span data-ttu-id="28bb8-242">現在 hello 應用程式閘道會排入佇列，並建立。</span><span class="sxs-lookup"><span data-stu-id="28bb8-242">Now hello application gateway is queued up and created.</span></span>

1. <span data-ttu-id="28bb8-243">一旦建立 hello 應用程式閘道之後，瀏覽 tooit hello 應用程式閘道 hello toocontinue 入口網站組態中。</span><span class="sxs-lookup"><span data-stu-id="28bb8-243">Once hello application gateway has been created, navigate tooit in hello portal toocontinue configuration of hello application gateway.</span></span>

    ![應用程式閘道資源檢視][10]

<span data-ttu-id="28bb8-245">下列步驟建立基本應用程式閘道與 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。</span><span class="sxs-lookup"><span data-stu-id="28bb8-245">These steps create a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="28bb8-246">您可以修改這些設定 toosuit 部署成功 hello 佈建之後</span><span class="sxs-lookup"><span data-stu-id="28bb8-246">You can modify these settings toosuit your deployment once hello provisioning is successful</span></span>

> [!NOTE]
> <span data-ttu-id="28bb8-247">建立與 hello 基本 web 應用程式的防火牆設定的應用程式閘道設定成使用 CR 3.0 保護。</span><span class="sxs-lookup"><span data-stu-id="28bb8-247">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28bb8-248">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28bb8-248">Next steps</span></span>

<span data-ttu-id="28bb8-249">接下來，您可以了解如何 tooconfigure hello 的自訂網域別名[公用 IP 位址](../dns/dns-custom-domain.md#public-ip-address)使用 Azure DNS 或其他的 DNS 提供者。</span><span class="sxs-lookup"><span data-stu-id="28bb8-249">Next, you can learn how tooconfigure a custom domain alias for hello [public IP address](../dns/dns-custom-domain.md#public-ip-address) using Azure DNS or another DNS provider.</span></span>

<span data-ttu-id="28bb8-250">深入了解如何 tooconfigure 診斷記錄，toolog hello 或之事件的偵測到使用 web 應用程式防火牆阻止造訪[應用程式閘道診斷](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="28bb8-250">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="28bb8-251">了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="28bb8-251">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="28bb8-252">了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="28bb8-252">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
