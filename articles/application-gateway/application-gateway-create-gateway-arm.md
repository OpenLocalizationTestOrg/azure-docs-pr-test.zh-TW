---
title: "建立和管理 Azure 應用程式閘道 - PowerShell | Microsoft Docs"
description: "本頁面提供使用 Azure 資源管理員建立、設定、啟動和刪除 Azure 應用程式閘道的指示。"
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
ms.openlocfilehash: 5f1713365406764998de505ff62309bab9fa2567
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="dfde2-103">使用 Azure 資源管理員建立、啟動或刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dfde2-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="dfde2-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dfde2-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="dfde2-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfde2-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="dfde2-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfde2-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="dfde2-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="dfde2-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="dfde2-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dfde2-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="dfde2-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="dfde2-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="dfde2-110">不論是在雲端或內部部署環境中，此閘道均提供在不同伺服器之間進行容錯移轉及效能路由傳送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="dfde2-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="dfde2-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健全狀態探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="dfde2-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="dfde2-112">若要尋找完整的支援功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="dfde2-113">本文將逐步引導您完成建立、設定、啟動及刪除應用程式閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="dfde2-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfde2-114">使用 Azure 資源之前，請務必了解 Azure 目前有「資源管理員」和「傳統」兩種部署模型。</span><span class="sxs-lookup"><span data-stu-id="dfde2-114">Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="dfde2-115">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-classic-rm.md) 。</span><span class="sxs-lookup"><span data-stu-id="dfde2-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="dfde2-116">您可以按一下本文頂端的索引標籤，檢視不同工具的文件。</span><span class="sxs-lookup"><span data-stu-id="dfde2-116">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="dfde2-117">本文件會討論如何使用 Azure Resource Manager 建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dfde2-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="dfde2-118">若要使用傳統的版本，請移至 [使用 PowerShell 建立應用程式閘道傳統部署](application-gateway-create-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-118">To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dfde2-119">開始之前</span><span class="sxs-lookup"><span data-stu-id="dfde2-119">Before you begin</span></span>

1. <span data-ttu-id="dfde2-120">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dfde2-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="dfde2-121">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="dfde2-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="dfde2-122">如果您有現有的虛擬網路，請選取現有的空白子網路，或在現有的虛擬網路中建立子網路，僅供應用程式閘道使用。</span><span class="sxs-lookup"><span data-stu-id="dfde2-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="dfde2-123">您無法將應用程式閘道部署到與您打算部署於應用程式閘道後方的資源不同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="dfde2-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="dfde2-124">您要設定來使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="dfde2-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="dfde2-125">建立應用程式閘道需要什麼？</span><span class="sxs-lookup"><span data-stu-id="dfde2-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="dfde2-126">**後端伺服器集區：**後端伺服器的 IP 位址清單、FQDN 或 NIC。</span><span class="sxs-lookup"><span data-stu-id="dfde2-126">**Backend server pool:** The list of IP addresses, FQDNs, or NICs of the backend servers.</span></span> <span data-ttu-id="dfde2-127">如果使用 IP 位址，它們應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="dfde2-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="dfde2-128">**後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="dfde2-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="dfde2-129">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfde2-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="dfde2-130">**前端連接埠：**此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="dfde2-130">**frontend port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="dfde2-131">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfde2-131">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="dfde2-132">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-132">**Listener:** The listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="dfde2-133">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="dfde2-133">**Rule:** The rule binds the listener, the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="dfde2-134">建立資源管理員的資源群組</span><span class="sxs-lookup"><span data-stu-id="dfde2-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="dfde2-135">確定您使用最新版本的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="dfde2-135">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="dfde2-136">如需詳細資訊，可在 [搭配使用 Windows PowerShell 與資源管理員](../powershell-azure-resource-manager.md)取得。</span><span class="sxs-lookup"><span data-stu-id="dfde2-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="dfde2-137">登入 Azure 並輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="dfde2-137">Log in to Azure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="dfde2-138">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfde2-138">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="dfde2-139">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfde2-139">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="dfde2-140">建立資源群組 (若使用現有的資源群組，請略過此步驟)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="dfde2-141">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="dfde2-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="dfde2-142">此位置用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="dfde2-142">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="dfde2-143">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="dfde2-143">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="dfde2-144">在上述範例中，我們建立了名為 **ContosoRG** 且位於 [美國東部] 的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dfde2-144">In the example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="dfde2-145">如果您需要為應用程式閘道設定自訂探查，請造訪：[使用 PowerShell 建立具有自訂探查的應用程式閘道](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-145">If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="dfde2-146">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="dfde2-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="dfde2-147">建立應用程式閘道組態物件</span><span class="sxs-lookup"><span data-stu-id="dfde2-147">Create the application gateway configuration objects</span></span>

<span data-ttu-id="dfde2-148">建立應用程式閘道之前，必須先設定所有組態項目。</span><span class="sxs-lookup"><span data-stu-id="dfde2-148">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="dfde2-149">下列步驟會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="dfde2-149">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign the address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with the address space of 10.0.0.0/16 and add the subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used to connect to the application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. The gateway picks up an IP addressfrom the configured subnet and routes network traffic to the IP addresses in the backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with the addresses of your web servers. These backend pool members are all validated to be healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed to them when requests come into the application gateway. Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings to determine the protocol and port that is used when sending traffic to the backend servers. Cookie-based sessions are also determined by the backend HTTP settings.  If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used to connect to the application gateway through the public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure the frontend IP configuration with the public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure the listener.  The listener is a combination of the front end IP configuration, protocol, and port and is used to receive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used to route traffic to the backend servers. The backend pool settings, listener, and backend pool created in the previous steps make up the rule. Based on the criteria defined traffic is routed to the appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU for the application gateway, this determines the size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create the application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="dfde2-150">完成時，從附加至應用程式閘道的公用 IP 資源，擷取應用程式閘道的 DNS 和 VIP 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dfde2-150">When complete, retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="dfde2-151">刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="dfde2-151">Delete the application gateway</span></span>

<span data-ttu-id="dfde2-152">下列範例會刪除應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dfde2-152">The following example deletes the application gateway.</span></span>

```powershell
# Retrieve the application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops the application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="dfde2-153">**-force** 參數可用來隱藏移除確認訊息。</span><span class="sxs-lookup"><span data-stu-id="dfde2-153">The **-force** switch can be used to suppress the remove confirmation message.</span></span>

<span data-ttu-id="dfde2-154">若要確認已移除服務，您可以使用 `Get-AzureRmApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dfde2-154">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="dfde2-155">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="dfde2-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="dfde2-156">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="dfde2-156">Get application gateway DNS name</span></span>

<span data-ttu-id="dfde2-157">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="dfde2-157">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="dfde2-158">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="dfde2-159">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="dfde2-159">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="dfde2-160">做法是使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="dfde2-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="dfde2-161">這可透過 Azure DNS 或其他 DNS 提供者完成，方法是建立一筆指向[公用 IP 位址](../dns/dns-custom-domain.md#public-ip-address)的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="dfde2-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points to the [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="dfde2-162">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="dfde2-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dfde2-163">在服務啟動時，系統會將 IP 位址指派至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="dfde2-163">An IP address is assigned to the application gateway when the service starts.</span></span>

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

## <a name="delete-all-resources"></a><span data-ttu-id="dfde2-164">刪除所有資源</span><span class="sxs-lookup"><span data-stu-id="dfde2-164">Delete all resources</span></span>

<span data-ttu-id="dfde2-165">若要刪除這篇文章中建立的所有資源，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="dfde2-165">To delete all resources created in this article, complete the following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="dfde2-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfde2-166">Next steps</span></span>

<span data-ttu-id="dfde2-167">如果您想要設定 SSL 卸載，請造訪：[設定應用程式閘道以進行 SSL 卸載](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-167">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="dfde2-168">如果您想要將應用程式閘道設為與內部負載平衡器搭配使用，請造訪：[建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="dfde2-168">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="dfde2-169">如果您想進一步了解一般負載平衡選項，請造訪：</span><span class="sxs-lookup"><span data-stu-id="dfde2-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="dfde2-170">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="dfde2-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="dfde2-171">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="dfde2-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
