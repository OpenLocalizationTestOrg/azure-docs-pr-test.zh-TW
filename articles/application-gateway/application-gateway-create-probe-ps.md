---
title: "aaaCreate 自訂探查-Azure 應用程式閘道-PowerShell |Microsoft 文件"
description: "了解如何 toocreate 自訂探查應用程式閘道資源管理員 中使用 PowerShell"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="1e84f-103">使用 Azure 資源管理員的 PowerShell 建立 Azure 應用程式閘道的自訂探查</span><span class="sxs-lookup"><span data-stu-id="1e84f-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e84f-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1e84f-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="1e84f-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e84f-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="1e84f-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e84f-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="1e84f-107">在本文中，您可以加入自訂探查 tooan 現有應用程式閘道使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="1e84f-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="1e84f-108">自訂探查適合應用程式的健全狀況檢查 頁面，或未提供成功的回應 hello 預設 web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e84f-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="1e84f-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1e84f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1e84f-110">本文將說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello[傳統部署模型](application-gateway-create-probe-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="1e84f-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="1e84f-111">建立含有自訂探查的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1e84f-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="1e84f-112">登入並建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1e84f-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="1e84f-113">使用`Login-AzureRmAccount`tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="1e84f-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="1e84f-114">收到 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e84f-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="1e84f-115">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="1e84f-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="1e84f-116">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e84f-116">Create a resource group.</span></span> <span data-ttu-id="1e84f-117">如果您有現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="1e84f-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="1e84f-118">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="1e84f-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1e84f-119">此位置用於 hello 預設位置為該資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e84f-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="1e84f-120">請確定所有命令 toocreate 應用程式閘道使用 hello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1e84f-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="1e84f-121">在上述範例中的 hello，我們建立一個稱為資源群組**appgw RG**位置**美國西部**。</span><span class="sxs-lookup"><span data-stu-id="1e84f-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="1e84f-122">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="1e84f-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="1e84f-123">hello 下列範例會建立虛擬網路和 hello 應用程式閘道的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e84f-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="1e84f-124">「應用程式閘道」需要使用其專屬的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e84f-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="1e84f-125">基於這個理由，應該小於 hello 位址空間中建立及使用其他子網路 toobe 的 hello VNET tooallow hello 建立 hello 應用程式閘道的子網路。</span><span class="sxs-lookup"><span data-stu-id="1e84f-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="1e84f-126">建立 hello 前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="1e84f-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="1e84f-127">建立公用 IP 資源**publicIP01**資源群組中**appgw rg** hello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="1e84f-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="1e84f-128">此範例會使用 hello 前端 IP 位址的 hello 應用程式閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1e84f-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="1e84f-129">應用程式閘道需要 hello 公用 IP 位址 toohave 動態建立的 DNS 名稱因此 hello`-DomainNameLabel`不 hello hello 公用 IP 位址建立期間指定。</span><span class="sxs-lookup"><span data-stu-id="1e84f-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="1e84f-130">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1e84f-130">Create an application gateway</span></span>

<span data-ttu-id="1e84f-131">您之前建立 hello 應用程式閘道設定所有設定項目。</span><span class="sxs-lookup"><span data-stu-id="1e84f-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="1e84f-132">hello 下列範例會建立 hello 所需的應用程式閘道資源的設定項目。</span><span class="sxs-lookup"><span data-stu-id="1e84f-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="1e84f-133">**元件**</span><span class="sxs-lookup"><span data-stu-id="1e84f-133">**Component**</span></span> | <span data-ttu-id="1e84f-134">**說明**</span><span class="sxs-lookup"><span data-stu-id="1e84f-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="1e84f-135">**閘道 IP 設定**</span><span class="sxs-lookup"><span data-stu-id="1e84f-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="1e84f-136">應用程式閘道的 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="1e84f-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="1e84f-137">**後端集區**</span><span class="sxs-lookup"><span data-stu-id="1e84f-137">**Backend pool**</span></span> | <span data-ttu-id="1e84f-138">IP 位址、 FQDN 或 Nic 的 toohello 應用程式伺服器主控 hello web 應用程式集區</span><span class="sxs-lookup"><span data-stu-id="1e84f-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="1e84f-139">**健康狀態探查**</span><span class="sxs-lookup"><span data-stu-id="1e84f-139">**Health probe**</span></span> | <span data-ttu-id="1e84f-140">自訂探查使用 hello 後端集區成員 toomonitor hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="1e84f-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="1e84f-141">**HTTP 設定**</span><span class="sxs-lookup"><span data-stu-id="1e84f-141">**HTTP settings**</span></span> | <span data-ttu-id="1e84f-142">包括連接埠、通訊協定、以 Cookie 為依據的親和性、探查和逾時等設定的集合。</span><span class="sxs-lookup"><span data-stu-id="1e84f-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="1e84f-143">這些設定會決定流量的路由的 toohello 後端集區成員的方式</span><span class="sxs-lookup"><span data-stu-id="1e84f-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="1e84f-144">**前端連接埠**</span><span class="sxs-lookup"><span data-stu-id="1e84f-144">**Frontend port**</span></span> | <span data-ttu-id="1e84f-145">hello hello 應用程式閘道的連接埠上接聽流量</span><span class="sxs-lookup"><span data-stu-id="1e84f-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="1e84f-146">**接聽程式**</span><span class="sxs-lookup"><span data-stu-id="1e84f-146">**Listener**</span></span> | <span data-ttu-id="1e84f-147">通訊協定、前端 IP 設定以及前端連接埠的組合。</span><span class="sxs-lookup"><span data-stu-id="1e84f-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="1e84f-148">這是用於接聽傳入要求的項目。</span><span class="sxs-lookup"><span data-stu-id="1e84f-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="1e84f-149">**規則**</span><span class="sxs-lookup"><span data-stu-id="1e84f-149">**Rule**</span></span>| <span data-ttu-id="1e84f-150">路由 hello 流量 toohello 適當的後端 HTTP 設定所決定。</span><span class="sxs-lookup"><span data-stu-id="1e84f-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="1e84f-151">新增探查 tooan 現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1e84f-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="1e84f-152">hello 下列程式碼片段加入探查 tooan 現有應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1e84f-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="1e84f-153">從現有應用程式閘道中移除探查</span><span class="sxs-lookup"><span data-stu-id="1e84f-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="1e84f-154">下列程式碼片段的 hello 移除現有的應用程式閘道的探查。</span><span class="sxs-lookup"><span data-stu-id="1e84f-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="1e84f-155">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="1e84f-155">Get application gateway DNS name</span></span>

<span data-ttu-id="1e84f-156">一旦建立 hello 閘道，hello 下一個步驟是 tooconfigure hello 前端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="1e84f-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="1e84f-157">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="1e84f-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="1e84f-158">tooensure 終端使用者可以叫用可以用一筆 CNAME 記錄的 hello 應用程式閘道的 hello 應用程式閘道 toopoint toohello 公用端點。</span><span class="sxs-lookup"><span data-stu-id="1e84f-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="1e84f-159">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1e84f-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="1e84f-160">toodo hello 應用程式閘道及其相關聯的 IP/DNS 名稱，使用 hello PublicIPAddress 項目附加的 toohello 應用程式閘道的這個，擷取詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1e84f-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="1e84f-161">hello 應用程式閘道的 DNS 名稱應該使用的 toocreate CNAME 記錄，哪個點 hello 兩個 web 應用程式 toothis DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1e84f-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="1e84f-162">不建議 hello 使用 A 記錄，因為可能會在重新啟動應用程式閘道變更 hello VIP。</span><span class="sxs-lookup"><span data-stu-id="1e84f-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1e84f-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e84f-163">Next steps</span></span>

<span data-ttu-id="1e84f-164">了解 tooconfigure SSL 卸載造訪：[設定 SSL 卸載](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="1e84f-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

