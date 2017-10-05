---
title: "在 Azure 應用程式閘道上設定 SSL 原則 - PowerShell | Microsoft Docs"
description: "本分頁提供在 Azure 應用程式閘道上設定 SSL 原則的指示"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: ece2549a607ffa06602c26cf77db93f67112d029
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="8cdec-103">在應用程式閘道上設定 SSL 原則版本和加密套件</span><span class="sxs-lookup"><span data-stu-id="8cdec-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="8cdec-104">了解如何在應用程式閘道上設定 SSL 原則版本和加密套件。</span><span class="sxs-lookup"><span data-stu-id="8cdec-104">Learn how to configure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="8cdec-105">您可以從[預先定義的原則清單](#predefined-ssl-policies)中選取，清單包含 SSL 原則版本和已啟用加密套件的不同設定。</span><span class="sxs-lookup"><span data-stu-id="8cdec-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="8cdec-106">您也可以根據您的需求定義[自訂 SSL 原則](#configure-a-custom-ssl-policy)。</span><span class="sxs-lookup"><span data-stu-id="8cdec-106">You also have the ability to define a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="8cdec-107">取得可用的 SSL 選項</span><span class="sxs-lookup"><span data-stu-id="8cdec-107">Get available SSL options</span></span>

<span data-ttu-id="8cdec-108">`Get-AzureRMApplicationGatewayAvailableSslOptions` Cmdlet 提供可用預先定義原則、可用加密套件，以及可以設定之通訊協定版本的清單。</span><span class="sxs-lookup"><span data-stu-id="8cdec-108">The `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="8cdec-109">下列範例顯示執行 Cmdlet 後的範例輸出。</span><span class="sxs-lookup"><span data-stu-id="8cdec-109">The following example shows an example output from running the cmdlet.</span></span>

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="8cdec-110">列出預先定義的 SSL 原則</span><span class="sxs-lookup"><span data-stu-id="8cdec-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="8cdec-111">應用程式閘道隨附 3 個可用的預先定義原則。</span><span class="sxs-lookup"><span data-stu-id="8cdec-111">Application gateway comes with 3 pre-defined policies that can be used.</span></span> <span data-ttu-id="8cdec-112">`Get-AzureRmApplicationGatewaySslPredefinedPolicy` Cmdlet 會擷取這些原則。</span><span class="sxs-lookup"><span data-stu-id="8cdec-112">The `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="8cdec-113">每個原則都有不同的通訊協定版本與已啟用的加密套件。</span><span class="sxs-lookup"><span data-stu-id="8cdec-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="8cdec-114">這些預先定義的原則可以用來快速地在應用程式閘道上設定 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="8cdec-114">These pre-defined policies can be used to quickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="8cdec-115">根據預設，如果未定義特定 SSL 原則，則會選取 **AppGwSslPolicy20170401**。</span><span class="sxs-lookup"><span data-stu-id="8cdec-115">By default **AppGwSslPolicy20170401** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="8cdec-116">以下是執行 `Get-AzureRmApplicationGatewaySslPredefinedPolicy` 的範例。</span><span class="sxs-lookup"><span data-stu-id="8cdec-116">The following is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="8cdec-117">設定自訂 SSL 原則</span><span class="sxs-lookup"><span data-stu-id="8cdec-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="8cdec-118">下列範例會在應用程式閘道上設定自訂 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="8cdec-118">The following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="8cdec-119">它會設定 `TLSv1_1` 的最小通訊協定版本，並且啟用下列加密套件：</span><span class="sxs-lookup"><span data-stu-id="8cdec-119">It sets the minimum protocol version to `TLSv1_1` and enables the following cipher suites:</span></span>

* <span data-ttu-id="8cdec-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="8cdec-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="8cdec-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cdec-122">設定自訂 SSL 原則時，必須從下列清單選取至少一個加密套件。</span><span class="sxs-lookup"><span data-stu-id="8cdec-122">At least one cipher suite from the following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="8cdec-123">應用程式閘道使用 RSA SHA256 加密套件進行後端管理。</span><span class="sxs-lookup"><span data-stu-id="8cdec-123">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="8cdec-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="8cdec-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="8cdec-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="8cdec-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="8cdec-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="8cdec-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="8cdec-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set the SSL policy on the application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="8cdec-130">使用預先定義的 SSL 原則建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="8cdec-130">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="8cdec-131">下列範例會使用預先定義的 SSL 原則建立新的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8cdec-131">The following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for the application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve the subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define the backend http settings to be used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for the public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with the certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define the size of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure the SSL policy to use a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create the application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a><span data-ttu-id="8cdec-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8cdec-132">Next steps</span></span>

<span data-ttu-id="8cdec-133">請參閱[應用程式閘道重新導向概觀](application-gateway-redirect-overview.md)以了解如何將 HTTP 流量重新導向至 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="8cdec-133">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn how to redirect HTTP traffic to a HTTPS endpoint.</span></span>