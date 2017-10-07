---
title: "aaaCreate 和 PowerShell 管理 Azure 應用程式閘道-|Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定、 啟動及使用 Azure Resource Manager 刪除 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="835d8-103">使用 Azure 資源管理員建立、啟動或刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="835d8-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="835d8-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="835d8-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="835d8-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="835d8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="835d8-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="835d8-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="835d8-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="835d8-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="835d8-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="835d8-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="835d8-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="835d8-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="835d8-110">它提供容錯移轉和效能路由不同的伺服器之間的 HTTP 要求是否位於 hello 雲端或內部部署。</span><span class="sxs-lookup"><span data-stu-id="835d8-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="835d8-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健康情況探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="835d8-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="835d8-112">toofind 完整支援的功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="835d8-113">本文將引導您完成 hello 步驟 toocreate、 設定、 啟動及刪除應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="835d8-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="835d8-114">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand： 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="835d8-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="835d8-115">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="835d8-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="835d8-116">您可以按一下上方的這篇文章 hello hello 索引標籤檢視 hello 文件不同的工具。</span><span class="sxs-lookup"><span data-stu-id="835d8-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="835d8-117">本文件會討論如何使用 Azure Resource Manager 建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="835d8-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="835d8-118">toouse hello 傳統版本，請移太[使用 PowerShell 建立應用程式閘道傳統部署](application-gateway-create-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="835d8-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="835d8-119">Before you begin</span></span>

1. <span data-ttu-id="835d8-120">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="835d8-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="835d8-121">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="835d8-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="835d8-122">如果您有現有的虛擬網路，選取現有的空白子網路，或僅用於在現有的虛擬網路中建立 hello 應用程式閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="835d8-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="835d8-123">您無法將部署 hello 應用程式閘道 tooa 不同虛擬網路 hello 資源比您想 toodeploy hello 應用程式閘道後方。</span><span class="sxs-lookup"><span data-stu-id="835d8-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="835d8-124">您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。</span><span class="sxs-lookup"><span data-stu-id="835d8-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="835d8-125">什麼是必要的 toocreate 應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="835d8-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="835d8-126">**後端伺服器集區：** hello IP 位址、 Fqdn 或 Nic hello 後端伺服器的清單。</span><span class="sxs-lookup"><span data-stu-id="835d8-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="835d8-127">如果使用 IP 位址，它們應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="835d8-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="835d8-128">**後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="835d8-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="835d8-129">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="835d8-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="835d8-130">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="835d8-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="835d8-131">叫用這個連接埠，並接著會取得 hello 後端伺服器的重新導向的 tooone。</span><span class="sxs-lookup"><span data-stu-id="835d8-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="835d8-132">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="835d8-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="835d8-133">**規則：** hello 規則繫結 hello 接聽程式，hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="835d8-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="835d8-134">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="835d8-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="835d8-135">請確定您使用 Azure PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="835d8-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="835d8-136">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="835d8-137">登入 tooAzure，並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="835d8-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="835d8-138">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="835d8-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="835d8-139">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="835d8-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="835d8-140">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="835d8-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="835d8-141">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="835d8-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="835d8-142">此位置用於 hello 預設位置為該資源群組。</span><span class="sxs-lookup"><span data-stu-id="835d8-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="835d8-143">請確定應用程式閘道使用的所有命令 toocreate 都 hello 相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="835d8-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="835d8-144">在 hello 上述範例中，我們建立一個稱為資源群組**ContosoRG**和位置**美國東部**。</span><span class="sxs-lookup"><span data-stu-id="835d8-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="835d8-145">如果您需要 tooconfigure 自訂探查您應用程式閘道，請瀏覽：[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="835d8-146">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="835d8-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="835d8-147">建立 hello 應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="835d8-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="835d8-148">所有設定項目必須都設定才能建立 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="835d8-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="835d8-149">hello 下列步驟建立 hello 組態項目所需的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="835d8-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="835d8-150">完成時，擷取 hello 公用 IP 資源附加的 toohello 應用程式閘道 DNS 和 VIP 的 hello 應用程式閘道的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="835d8-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="835d8-151">刪除 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="835d8-151">Delete hello application gateway</span></span>

<span data-ttu-id="835d8-152">hello 下列範例會刪除 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="835d8-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="835d8-153">hello **-強制**參數可以是使用的 toosuppress hello 移除確認訊息。</span><span class="sxs-lookup"><span data-stu-id="835d8-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="835d8-154">已移除 hello 服務的 tooverify，您可以使用 hello `Get-AzureRmApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="835d8-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="835d8-155">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="835d8-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="835d8-156">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="835d8-156">Get application gateway DNS name</span></span>

<span data-ttu-id="835d8-157">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="835d8-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="835d8-158">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="835d8-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="835d8-159">tooensure 終端使用者可以叫用 hello 應用程式閘道，CNAME 記錄可使用的 toopoint toohello 公用端點的 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="835d8-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="835d8-160">toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="835d8-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="835d8-161">這可以使用 Azure DNS 或其他的 DNS 提供者，藉由建立一筆 CNAME 記錄指向 toohello[公用 IP 位址](../dns/dns-custom-domain.md#public-ip-address)。</span><span class="sxs-lookup"><span data-stu-id="835d8-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="835d8-162">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="835d8-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="835d8-163">Hello 服務啟動時，會指派 toohello 應用程式閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="835d8-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="835d8-164">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="835d8-164">Delete all resources</span></span>

<span data-ttu-id="835d8-165">在本文中完成下列步驟的 hello 建立 toodelete 所有資源：</span><span class="sxs-lookup"><span data-stu-id="835d8-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="835d8-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="835d8-166">Next steps</span></span>

<span data-ttu-id="835d8-167">如果您想的 tooconfigure SSL 卸載，請造訪：[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="835d8-168">如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請造訪：[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="835d8-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="835d8-169">如果您想進一步了解一般負載平衡選項，請造訪：</span><span class="sxs-lookup"><span data-stu-id="835d8-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="835d8-170">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="835d8-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="835d8-171">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="835d8-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
