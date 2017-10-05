---
title: "設定 Web 應用程式防火牆 - Azure 應用程式閘道 | Microsoft Docs"
description: "本文提供如何在現有的或新的應用程式閘道上開始使用 Web 應用程式防火牆的指引。"
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
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="53223-103">在新的或現有的應用程式閘道上設定 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="53223-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53223-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="53223-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="53223-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53223-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="53223-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="53223-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="53223-107">了解如何建立已啟用 Web 應用程式防火牆的應用程式閘道，或將 Web 應用程式防火牆新增至現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="53223-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="53223-108">Azure 應用程式閘道中的 Web 應用程式防火牆 (WAF) 可保護 Web 應用程式，不致遭受常見的 Web 型攻擊，例如 SQL 插入式攻擊、跨網站指令碼攻擊和工作階段攔截。</span><span class="sxs-lookup"><span data-stu-id="53223-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="53223-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="53223-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="53223-110">不論是在雲端或內部部署中，此閘道均提供在不同伺服器之間進行容錯移轉及效能路由傳送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="53223-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="53223-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="53223-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="53223-112">若要尋找完整的支援功能清單，請瀏覽：[應用程式閘道概觀](application-gateway-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="53223-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="53223-113">下列文章說明如何[將 Web 應用程式防火牆新增至現有應用程式閘道](#add-web-application-firewall-to-an-existing-application-gateway)和[建立使用 Web 應用程式防火牆的應用程式閘道](#create-an-application-gateway-with-web-application-firewall)。</span><span class="sxs-lookup"><span data-stu-id="53223-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![案例影像][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="53223-115">WAF 組態差異</span><span class="sxs-lookup"><span data-stu-id="53223-115">WAF configuration differences</span></span>

<span data-ttu-id="53223-116">如果您已經讀過 [使用 PowerShell 建立應用程式閘道](application-gateway-create-gateway-arm.md)，您會了解建立應用程式閘道時要設定的 SKU 設定。</span><span class="sxs-lookup"><span data-stu-id="53223-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="53223-117">在應用程式閘道上設定 SKU 時，WAF 會提供其他可定義的設定。</span><span class="sxs-lookup"><span data-stu-id="53223-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="53223-118">您對應用程式閘道本身不會進行任何其他變更。</span><span class="sxs-lookup"><span data-stu-id="53223-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="53223-119">**設定**</span><span class="sxs-lookup"><span data-stu-id="53223-119">**Setting**</span></span> | <span data-ttu-id="53223-120">**詳細資料**</span><span class="sxs-lookup"><span data-stu-id="53223-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="53223-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="53223-121">**SKU**</span></span> |<span data-ttu-id="53223-122">不具有 WAF 的一般應用程式閘道支援 **Standard\_Small**、**Standard\_Medium** 和 **Standard\_Large** 大小。</span><span class="sxs-lookup"><span data-stu-id="53223-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="53223-123">WAF 推出後另外出現了兩個 SKU，分別是 **WAF\_Medium** 和 **WAF\_Large**。</span><span class="sxs-lookup"><span data-stu-id="53223-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="53223-124">小型應用程式閘道不支援 WAF。</span><span class="sxs-lookup"><span data-stu-id="53223-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="53223-125">**層級**</span><span class="sxs-lookup"><span data-stu-id="53223-125">**Tier**</span></span> | <span data-ttu-id="53223-126">可用的值為**標準**或 **WAF**。</span><span class="sxs-lookup"><span data-stu-id="53223-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="53223-127">使用 Web 應用程式防火牆時，必須選擇 **WAF** 。</span><span class="sxs-lookup"><span data-stu-id="53223-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="53223-128">**模式**</span><span class="sxs-lookup"><span data-stu-id="53223-128">**Mode**</span></span> | <span data-ttu-id="53223-129">此設定是 WAF 的模式。</span><span class="sxs-lookup"><span data-stu-id="53223-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="53223-130">允許的值為**偵測**和**防止**。</span><span class="sxs-lookup"><span data-stu-id="53223-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="53223-131">當 WAF 設定為偵測模式時，所有威脅會儲存在記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="53223-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="53223-132">在防止模式時仍會記錄事件，但攻擊者會從應用程式閘道收到 403 未經授權的回應。</span><span class="sxs-lookup"><span data-stu-id="53223-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="53223-133">對現有應用程式閘道新增 Web 應用程式防火牆</span><span class="sxs-lookup"><span data-stu-id="53223-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="53223-134">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="53223-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="53223-135">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="53223-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="53223-136">登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="53223-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="53223-137">選取要用於此案例的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53223-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="53223-138">擷取要在其中新增 Web 應用程式防火牆的閘道。</span><span class="sxs-lookup"><span data-stu-id="53223-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="53223-139">設定 Web 應用程式防火牆 SKU。</span><span class="sxs-lookup"><span data-stu-id="53223-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="53223-140">可用大小為 **WAF\_Large** 和 **WAF\_Medium**。</span><span class="sxs-lookup"><span data-stu-id="53223-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="53223-141">使用 Web 應用程式防火牆時，必須為 **WAF** 層，設定 SKU 時必須確認容量。</span><span class="sxs-lookup"><span data-stu-id="53223-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="53223-142">如下列範例所定義地設定 WAF 設定︰</span><span class="sxs-lookup"><span data-stu-id="53223-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="53223-143">在 **WafMode** 中，可用值是「防止」和「偵測」。</span><span class="sxs-lookup"><span data-stu-id="53223-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="53223-144">使用上一個步驟所定義的設定來更新應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="53223-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="53223-145">此命令會更新具有 Web 應用程式防火牆的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="53223-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="53223-146">請參閱[應用程式閘道診斷](application-gateway-diagnostics.md)，了解如何檢視應用程式閘道中的記錄。</span><span class="sxs-lookup"><span data-stu-id="53223-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="53223-147">由於 WAF 的安全性本質，您必須定期檢閱記錄檔，以了解 Web 應用程式的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="53223-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="53223-148">建立具有 Web 應用程式防火牆的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="53223-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="53223-149">下列步驟會帶您從頭到尾完成建立具有 Web 應用程式防火牆之應用程式閘道的整個程序。</span><span class="sxs-lookup"><span data-stu-id="53223-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="53223-150">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="53223-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="53223-151">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="53223-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="53223-152">執行 `Login-AzureRmAccount` 來登入 Azure，系統會提示使用您的認證進行驗證。</span><span class="sxs-lookup"><span data-stu-id="53223-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="53223-153">執行 `Get-AzureRmSubscription` 來檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53223-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="53223-154">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53223-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="53223-155">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="53223-155">Create a resource group</span></span>

<span data-ttu-id="53223-156">建立應用程式閘道的資源群組。</span><span class="sxs-lookup"><span data-stu-id="53223-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="53223-157">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="53223-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="53223-158">此位置用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="53223-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="53223-159">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="53223-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="53223-160">在上述範例中，我們建立名為 "appgw-RG" 的資源群組，且位置為美國西部 ("West US")。</span><span class="sxs-lookup"><span data-stu-id="53223-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="53223-161">如果您需要為應用程式閘道設定自訂探查，請參閱[使用 PowerShell 建立具有自訂探查的應用程式閘道](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="53223-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="53223-162">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="53223-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="53223-163">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="53223-163">Configure virtual network</span></span>

<span data-ttu-id="53223-164">應用程式閘道需要有自己的子網路。</span><span class="sxs-lookup"><span data-stu-id="53223-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="53223-165">在此步驟中，您會建立具有 10.0.0.0/16 位址空間的虛擬網路和兩個子網路，其中，一個用於應用程式閘道，另一個用於後端集區成員。</span><span class="sxs-lookup"><span data-stu-id="53223-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="53223-166">設定公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="53223-166">Configure public IP address</span></span>

<span data-ttu-id="53223-167">為了處理外部要求，應用程式閘道需要公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="53223-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="53223-168">這個公用 IP 位址不能定義 `DomainNameLabel` 給應用程式閘道使用。</span><span class="sxs-lookup"><span data-stu-id="53223-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="53223-169">設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="53223-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="53223-170">基於保護的目的，使用基本 Web 應用程式防火牆設定建立的應用程式閘道，是使用 CRS 3.0 所設定。</span><span class="sxs-lookup"><span data-stu-id="53223-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="53223-171">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="53223-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="53223-172">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="53223-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="53223-173">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="53223-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="53223-174">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="53223-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="53223-175">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="53223-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="53223-176">若要設定別名，請使用連結至應用程式閘道的 PublicIPAddress 項目，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="53223-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="53223-177">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="53223-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="53223-178">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="53223-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="53223-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53223-179">Next steps</span></span>

<span data-ttu-id="53223-180">請參閱[應用程式閘道診斷](application-gateway-diagnostics.md)，以了解如何設定診斷記錄，以及如何記錄 Web 應用程式防火牆偵測到或防止的事件</span><span class="sxs-lookup"><span data-stu-id="53223-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
