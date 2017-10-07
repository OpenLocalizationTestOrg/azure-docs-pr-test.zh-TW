---
title: "aaaConfigure web 應用程式防火牆 Azure 應用程式閘道 |Microsoft 文件"
description: "本文提供指引 toostart 使用 web 應用程式在現有或新的應用程式閘道上的防火牆。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="a7e90-103">在新的或現有的應用程式閘道上設定 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="a7e90-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7e90-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a7e90-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="a7e90-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7e90-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="a7e90-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a7e90-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="a7e90-107">了解如何 toocreate web 應用程式防火牆啟用應用程式閘道，或將 web 應用程式防火牆 tooan 現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e90-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="a7e90-108">hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道會從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若保護 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e90-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="a7e90-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="a7e90-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a7e90-110">無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="a7e90-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="a7e90-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="a7e90-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a7e90-112">toofind 完整支援的功能清單，請造訪：[應用程式閘道概觀](application-gateway-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="a7e90-113">hello 下列文章將示範如何太[加入現有的應用程式閘道的 web 應用程式防火牆 tooan](#add-web-application-firewall-to-an-existing-application-gateway)和[建立應用程式閘道使用 web 應用程式防火牆](#create-an-application-gateway-with-web-application-firewall)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![案例影像][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="a7e90-115">WAF 組態差異</span><span class="sxs-lookup"><span data-stu-id="a7e90-115">WAF configuration differences</span></span>

<span data-ttu-id="a7e90-116">如果您已閱讀[使用 PowerShell 建立應用程式閘道](application-gateway-create-gateway-arm.md)，當您了解 hello SKU 設定 tooconfigure 建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e90-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="a7e90-117">WAF 提供額外的設定 toodefine 時應用程式閘道上設定 hello SKU。</span><span class="sxs-lookup"><span data-stu-id="a7e90-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="a7e90-118">沒有您在 hello 應用程式閘道本身進行任何其他變更。</span><span class="sxs-lookup"><span data-stu-id="a7e90-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="a7e90-119">**設定**</span><span class="sxs-lookup"><span data-stu-id="a7e90-119">**Setting**</span></span> | <span data-ttu-id="a7e90-120">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="a7e90-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="a7e90-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="a7e90-121">**SKU**</span></span> |<span data-ttu-id="a7e90-122">不具有 WAF 的一般應用程式閘道支援 **Standard\_Small**、**Standard\_Medium** 和 **Standard\_Large** 大小。</span><span class="sxs-lookup"><span data-stu-id="a7e90-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="a7e90-123">使用 WAF hello 介紹，有兩個額外的 Sku， **WAF\_媒體**和**WAF\_大**。</span><span class="sxs-lookup"><span data-stu-id="a7e90-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="a7e90-124">小型應用程式閘道不支援 WAF。</span><span class="sxs-lookup"><span data-stu-id="a7e90-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="a7e90-125">**層級**</span><span class="sxs-lookup"><span data-stu-id="a7e90-125">**Tier**</span></span> | <span data-ttu-id="a7e90-126">hello 可用的值為**標準**或**WAF**。</span><span class="sxs-lookup"><span data-stu-id="a7e90-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="a7e90-127">使用 Web 應用程式防火牆時，必須選擇 **WAF** 。</span><span class="sxs-lookup"><span data-stu-id="a7e90-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="a7e90-128">**模式**</span><span class="sxs-lookup"><span data-stu-id="a7e90-128">**Mode**</span></span> | <span data-ttu-id="a7e90-129">這項設定是 WAF hello 模式。</span><span class="sxs-lookup"><span data-stu-id="a7e90-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="a7e90-130">允許的值為**偵測**和**防止**。</span><span class="sxs-lookup"><span data-stu-id="a7e90-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="a7e90-131">當 WAF 設定為偵測模式時，所有威脅會儲存在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="a7e90-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="a7e90-132">在防止模式中，還是會記錄事件，但 hello 攻擊者收到 hello 應用程式閘道 403 未經授權的回應。</span><span class="sxs-lookup"><span data-stu-id="a7e90-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="a7e90-133">加入 web 應用程式防火牆 tooan 現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a7e90-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="a7e90-134">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="a7e90-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="a7e90-135">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="a7e90-136">登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7e90-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="a7e90-137">選取此案例中的 hello 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="a7e90-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="a7e90-138">擷取您要加入至 web 應用程式防火牆的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e90-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="a7e90-139">設定 hello web 應用程式防火牆 sku。</span><span class="sxs-lookup"><span data-stu-id="a7e90-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="a7e90-140">hello 可用大小是**WAF\_大**和**WAF\_媒體**。</span><span class="sxs-lookup"><span data-stu-id="a7e90-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="a7e90-141">使用 web 應用程式的防火牆時 hello 階層必須**WAF**，設定 hello sku 時，必須確認 hello 容量。</span><span class="sxs-lookup"><span data-stu-id="a7e90-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="a7e90-142">設定 hello WAF hello 下列範例中所定義：</span><span class="sxs-lookup"><span data-stu-id="a7e90-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="a7e90-143">如**FirewallMode**，hello 可用的值為預防和偵測。</span><span class="sxs-lookup"><span data-stu-id="a7e90-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="a7e90-144">更新應用程式閘道 hello hello hello 前面步驟中所定義的設定。</span><span class="sxs-lookup"><span data-stu-id="a7e90-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="a7e90-145">此命令會更新 web 應用程式防火牆 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e90-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="a7e90-146">請瀏覽[應用程式閘道診斷](application-gateway-diagnostics.md)toounderstand tooview 記錄您的應用程式閘道的方式。</span><span class="sxs-lookup"><span data-stu-id="a7e90-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="a7e90-147">WAF toohello 安全性本質，因為記錄檔需要 toobe 定期檢閱 toounderstand hello 安全性狀態的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7e90-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="a7e90-148">建立具有 Web 應用程式防火牆的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a7e90-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="a7e90-149">hello 下列步驟引導您進行整個 hello 開頭 tooend 使用 web 應用程式防火牆中建立應用程式閘道的程序。</span><span class="sxs-lookup"><span data-stu-id="a7e90-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="a7e90-150">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="a7e90-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="a7e90-151">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="a7e90-152">執行登入 tooAzure `Login-AzureRmAccount`，您會使用您的認證的提示的 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="a7e90-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="a7e90-153">執行檢查 hello 訂閱 hello 帳戶`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="a7e90-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="a7e90-154">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="a7e90-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="a7e90-155">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="a7e90-155">Create a resource group</span></span>

<span data-ttu-id="a7e90-156">建立 hello 應用程式閘道的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a7e90-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="a7e90-157">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="a7e90-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a7e90-158">此位置用於 hello 預設位置為該資源群組。</span><span class="sxs-lookup"><span data-stu-id="a7e90-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="a7e90-159">請確定所有命令使用的應用程式閘道 toocreate 都 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a7e90-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="a7e90-160">在上述範例中的 hello，我們會建立名為"appgw RG 」 和 「 位置 」 美國西部。 」 的資源群組</span><span class="sxs-lookup"><span data-stu-id="a7e90-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="a7e90-161">如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="a7e90-162">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a7e90-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="a7e90-163">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a7e90-163">Configure virtual network</span></span>

<span data-ttu-id="a7e90-164">應用程式閘道需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="a7e90-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="a7e90-165">在此步驟中，您可以建立具有 10.0.0.0/16 和兩個子網路的位址空間，一個用於 hello 應用程式閘道，一個用於後端集區成員的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a7e90-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="a7e90-166">設定公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="a7e90-166">Configure public IP address</span></span>

<span data-ttu-id="a7e90-167">在訂單 toohandle 外部要求中，應用程式閘道需要公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a7e90-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="a7e90-168">這個公用 IP 位址不能有`DomainNameLabel`定義 toobe hello 應用程式閘道所使用。</span><span class="sxs-lookup"><span data-stu-id="a7e90-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="a7e90-169">設定應用程式閘道 hello</span><span class="sxs-lookup"><span data-stu-id="a7e90-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="a7e90-170">建立與 hello 基本 web 應用程式的防火牆設定的應用程式閘道設定成使用 CR 3.0 保護。</span><span class="sxs-lookup"><span data-stu-id="a7e90-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a7e90-171">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="a7e90-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="a7e90-172">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a7e90-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="a7e90-173">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a7e90-174">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7e90-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="a7e90-175">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a7e90-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a7e90-176">tooconfigure 別名，擷取 hello 應用程式閘道和其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 附加項目 toohello 應用程式閘道的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a7e90-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="a7e90-177">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="a7e90-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="a7e90-178">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="a7e90-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="a7e90-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7e90-179">Next steps</span></span>

<span data-ttu-id="a7e90-180">深入了解如何 tooconfigure 診斷記錄，toolog hello 或之事件的偵測到使用 web 應用程式防火牆阻止造訪[應用程式閘道診斷](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="a7e90-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
