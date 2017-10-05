---
title: "建立自訂探查 - Azure 應用程式閘道 - PowerShell | Microsoft Docs"
description: "了解如何在資源管理員中使用 PowerShell 建立應用程式閘道的自訂探查"
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
ms.openlocfilehash: b54fe5267d87a41eb9e81d5d1dc9b1b16c5c5e88
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="1c073-103">使用 Azure 資源管理員的 PowerShell 建立 Azure 應用程式閘道的自訂探查</span><span class="sxs-lookup"><span data-stu-id="1c073-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c073-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1c073-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="1c073-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c073-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="1c073-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c073-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="1c073-107">在本文中，您會使用 PowerShell 將自訂探查新增到現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1c073-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="1c073-108">對於具有特定健康狀態檢查頁面的應用程式，或是在預設 Web 應用程式上不提供成功回應的應用程式，自訂探查非常實用。</span><span class="sxs-lookup"><span data-stu-id="1c073-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="1c073-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1c073-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="1c073-110">本文涵蓋之內容包括使用 Resource Manager 部署模型，Microsoft 建議大部分的新部署使用此模型，而不是[傳統部署模型](application-gateway-create-probe-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="1c073-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="1c073-111">建立含有自訂探查的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1c073-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="1c073-112">登入並建立資源群組</span><span class="sxs-lookup"><span data-stu-id="1c073-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="1c073-113">使用 `Login-AzureRmAccount`來驗證。</span><span class="sxs-lookup"><span data-stu-id="1c073-113">Use `Login-AzureRmAccount` to authenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="1c073-114">取得帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c073-114">Get the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="1c073-115">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1c073-115">Choose which of your Azure subscriptions to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="1c073-116">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1c073-116">Create a resource group.</span></span> <span data-ttu-id="1c073-117">如果您有現有的資源群組，則可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="1c073-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="1c073-118">Azure Resource Manager 需要所有的資源群組指定一個位置。</span><span class="sxs-lookup"><span data-stu-id="1c073-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="1c073-119">此位置用來作為該資源群組中資源的預設位置。</span><span class="sxs-lookup"><span data-stu-id="1c073-119">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="1c073-120">請確定所有用來建立應用程式閘道的命令都使用同一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="1c073-120">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="1c073-121">在上述範例中，我們建立名為 **appgw-RG** 的資源群組，位置為**美國西部**。</span><span class="sxs-lookup"><span data-stu-id="1c073-121">In the preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="1c073-122">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="1c073-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="1c073-123">下列範例會建立應用程式閘道的虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="1c073-123">The following example creates a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="1c073-124">「應用程式閘道」需要使用其專屬的子網路。</span><span class="sxs-lookup"><span data-stu-id="1c073-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="1c073-125">基於這個理由，針對應用程式閘道建立的子網路應該小於 VNET 位址空間，以便能建立和使用其他的子網路。</span><span class="sxs-lookup"><span data-stu-id="1c073-125">For this reason, the subnet created for the application gateway should be smaller than the address space of the VNET to allow for other subnets to be created and used.</span></span>

```powershell
# Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for the next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="1c073-126">建立前端組態的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="1c073-126">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="1c073-127">在美國西部區域的 **appgw-rg** 資源群組中建立公用 IP 資源 **publicIP01**。</span><span class="sxs-lookup"><span data-stu-id="1c073-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="1c073-128">此範例使用公用 IP 位址做為應用程式閘道的前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1c073-128">This example uses a public IP address for the front-end IP address of the application gateway.</span></span>  <span data-ttu-id="1c073-129">應用程式閘道需要公用 IP 位址才能具有動態建立的 DNS 名稱，因此在公用 IP 位址建立期間無法指定 `-DomainNameLabel`。</span><span class="sxs-lookup"><span data-stu-id="1c073-129">Application gateway requires the public IP address to have a dynamically created DNS name therefore the `-DomainNameLabel` cannot be specified during the creation of the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="1c073-130">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1c073-130">Create an application gateway</span></span>

<span data-ttu-id="1c073-131">您先設定所有組態項目，再建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1c073-131">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="1c073-132">下列範例會建立應用程式閘道資源所需的組態項目。</span><span class="sxs-lookup"><span data-stu-id="1c073-132">The following example creates the configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="1c073-133">**元件**</span><span class="sxs-lookup"><span data-stu-id="1c073-133">**Component**</span></span> | <span data-ttu-id="1c073-134">**說明**</span><span class="sxs-lookup"><span data-stu-id="1c073-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="1c073-135">**閘道 IP 設定**</span><span class="sxs-lookup"><span data-stu-id="1c073-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="1c073-136">應用程式閘道的 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="1c073-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="1c073-137">**後端集區**</span><span class="sxs-lookup"><span data-stu-id="1c073-137">**Backend pool**</span></span> | <span data-ttu-id="1c073-138">這是應用程式伺服器的 IP 位址、FQDN 或 NIC 的集區，此應用程式伺服器負責裝載 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1c073-138">A pool of IP addresses, FQDN's, or NICs that are to the application servers that host the web application</span></span>|
| <span data-ttu-id="1c073-139">**健康狀態探查**</span><span class="sxs-lookup"><span data-stu-id="1c073-139">**Health probe**</span></span> | <span data-ttu-id="1c073-140">用於監視後端集區成員健康狀態的自訂探查</span><span class="sxs-lookup"><span data-stu-id="1c073-140">A custom probe used to monitor the health of the backend pool members</span></span>|
| <span data-ttu-id="1c073-141">**HTTP 設定**</span><span class="sxs-lookup"><span data-stu-id="1c073-141">**HTTP settings**</span></span> | <span data-ttu-id="1c073-142">包括連接埠、通訊協定、以 Cookie 為依據的親和性、探查和逾時等設定的集合。</span><span class="sxs-lookup"><span data-stu-id="1c073-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="1c073-143">這些設定會決定流量路由傳送到後端集區成員的方式</span><span class="sxs-lookup"><span data-stu-id="1c073-143">These settings determine how traffic is routed to the backend pool members</span></span>|
| <span data-ttu-id="1c073-144">**前端連接埠**</span><span class="sxs-lookup"><span data-stu-id="1c073-144">**Frontend port**</span></span> | <span data-ttu-id="1c073-145">應用程式閘道接聽流量的連接埠</span><span class="sxs-lookup"><span data-stu-id="1c073-145">The port that the application gateway listens for traffic on</span></span>|
| <span data-ttu-id="1c073-146">**接聽程式**</span><span class="sxs-lookup"><span data-stu-id="1c073-146">**Listener**</span></span> | <span data-ttu-id="1c073-147">通訊協定、前端 IP 設定以及前端連接埠的組合。</span><span class="sxs-lookup"><span data-stu-id="1c073-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="1c073-148">這是用於接聽傳入要求的項目。</span><span class="sxs-lookup"><span data-stu-id="1c073-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="1c073-149">**規則**</span><span class="sxs-lookup"><span data-stu-id="1c073-149">**Rule**</span></span>| <span data-ttu-id="1c073-150">根據 HTTP 設定，將流量路由傳送至適當的後端。</span><span class="sxs-lookup"><span data-stu-id="1c073-150">Routes the traffic to the appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates the backend http settings to be used. This component references the $probe created in the previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for the application gateway to listen on port 80 that will be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates the $publicip variable defined previously with the front-end IP that will be used by the listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates the listener. The listener is a combination of protocol and the frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates the rule that routes traffic to the backend pools.  In this example we create a basic rule that uses the previous defined http settings and backend address pool.  It also associates the listener to the rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets the SKU of the application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# The final step creates the application gateway with all the previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="1c073-151">將探查新增至現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="1c073-151">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="1c073-152">下列的程式碼片段會將探查新增至現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="1c073-152">The following code snippet adds a probe to an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create the probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set the backend HTTP settings to use the new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="1c073-153">從現有應用程式閘道中移除探查</span><span class="sxs-lookup"><span data-stu-id="1c073-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="1c073-154">下列的程式碼片段會從現有的應用程式閘道移除探查。</span><span class="sxs-lookup"><span data-stu-id="1c073-154">The following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load the application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove the probe from the application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set the backend HTTP settings to remove the reference to the probe. The backend http settings now use the default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save the application gateway with the configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="1c073-155">取得應用程式閘道 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="1c073-155">Get application gateway DNS name</span></span>

<span data-ttu-id="1c073-156">建立閘道之後，下一步是設定通訊的前端。</span><span class="sxs-lookup"><span data-stu-id="1c073-156">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="1c073-157">當使用公用 IP 時，應用程式閘道需要動態指派的 DNS 名稱 (不易記住)。</span><span class="sxs-lookup"><span data-stu-id="1c073-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="1c073-158">為了確保使用者可以叫用應用程式閘道，可使用 CNAME 記錄來指向應用程式閘道的公用端點。</span><span class="sxs-lookup"><span data-stu-id="1c073-158">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="1c073-159">[在 Azure 中設定自訂網域名稱](../cloud-services/cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1c073-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="1c073-160">做法是使用連接至應用程式閘道的 PublicIPAddress 元素，擷取應用程式閘道的詳細資料及其關聯的 IP/DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="1c073-160">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="1c073-161">應用程式閘道的 DNS 名稱應該用來建立將兩個 Web 應用程式指向此 DNS 名稱的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="1c073-161">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="1c073-162">不建議使用 A-records，因為重新啟動應用程式閘道時，VIP 可能會變更。</span><span class="sxs-lookup"><span data-stu-id="1c073-162">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1c073-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c073-163">Next steps</span></span>

<span data-ttu-id="1c073-164">請瀏覽：[設定 SSL 卸載](application-gateway-ssl-arm.md)了解如何設定 SSL 卸載</span><span class="sxs-lookup"><span data-stu-id="1c073-164">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

