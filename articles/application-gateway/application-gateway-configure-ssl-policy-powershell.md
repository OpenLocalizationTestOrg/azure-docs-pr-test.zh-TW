---
title: "在 Azure 應用程式閘道 PowerShell aaaConfigure SSL 原則 |Microsoft 文件"
description: "本頁面提供 Azure 應用程式閘道上的指示 tooconfigure SSL 原則"
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
ms.openlocfilehash: 7802ad3d3191a2fe9d88dddcb7c65bc4a70a419c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="e6ca9-103">在應用程式閘道上設定 SSL 原則版本和加密套件</span><span class="sxs-lookup"><span data-stu-id="e6ca9-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="e6ca9-104">深入了解如何 tooconfigure SSL 的原則版本和加密應用程式閘道上的套件。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-104">Learn how tooconfigure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="e6ca9-105">您可以從[預先定義的原則清單](#predefined-ssl-policies)中選取，清單包含 SSL 原則版本和已啟用加密套件的不同設定。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="e6ca9-106">您也可以 hello 能力 toodefine[自訂 SSL 原則](#configure-a-custom-ssl-policy)根據您的需求。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-106">You also have hello ability toodefine a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="e6ca9-107">取得可用的 SSL 選項</span><span class="sxs-lookup"><span data-stu-id="e6ca9-107">Get available SSL options</span></span>

<span data-ttu-id="e6ca9-108">hello `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet 提供的清單，可用的預先定義的原則，可用的加密套件，以及您可以設定的通訊協定版本。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-108">hello `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="e6ca9-109">hello 下列範例示範執行 hello cmdlet 的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-109">hello following example shows an example output from running hello cmdlet.</span></span>

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

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="e6ca9-110">列出預先定義的 SSL 原則</span><span class="sxs-lookup"><span data-stu-id="e6ca9-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="e6ca9-111">應用程式閘道隨附 3 個可用的預先定義原則。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-111">Application gateway comes with 3 pre-defined policies that can be used.</span></span> <span data-ttu-id="e6ca9-112">hello`Get-AzureRmApplicationGatewaySslPredefinedPolicy`指令程式會擷取這些原則。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-112">hello `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="e6ca9-113">每個原則都有不同的通訊協定版本與已啟用的加密套件。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="e6ca9-114">這些預先定義的原則可以用 tooquickly 應用程式閘道上設定 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-114">These pre-defined policies can be used tooquickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="e6ca9-115">根據預設，如果未定義特定 SSL 原則，則會選取 **AppGwSslPolicy20170401**。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-115">By default **AppGwSslPolicy20170401** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="e6ca9-116">hello 下列是範例執行`Get-AzureRmApplicationGatewaySslPredefinedPolicy`。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-116">hello following is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

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

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="e6ca9-117">設定自訂 SSL 原則</span><span class="sxs-lookup"><span data-stu-id="e6ca9-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="e6ca9-118">下列範例中的 hello 應用程式閘道上設定自訂的 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-118">hello following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="e6ca9-119">它會設定 hello 最小的通訊協定版本太`TLSv1_1`並啟用 hello 遵循加密套件：</span><span class="sxs-lookup"><span data-stu-id="e6ca9-119">It sets hello minimum protocol version too`TLSv1_1` and enables hello following cipher suites:</span></span>

* <span data-ttu-id="e6ca9-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="e6ca9-120">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="e6ca9-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-121">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6ca9-122">設定自訂的 SSL 原則時，必須選取一個以上的加密套件，從下列清單中的 hello。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-122">At least one cipher suite from hello following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="e6ca9-123">應用程式閘道使用 RSA SHA256 加密套件進行後端管理。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-123">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="e6ca9-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-124">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="e6ca9-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-125">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="e6ca9-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-126">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="e6ca9-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-127">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="e6ca9-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-128">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="e6ca9-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="e6ca9-129">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set hello SSL policy on hello application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="e6ca9-130">使用預先定義的 SSL 原則建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="e6ca9-130">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="e6ca9-131">hello 下列範例會建立新的應用程式閘道與預先定義的 SSL 原則。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-131">hello following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"
# Create a subnet for hello application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
# Retrieve hello subnet object for later use
$subnet = $vnet.Subnets[0]
# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic
# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
# Define hello backend http settings toobe used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
# Upload an existing pfx certificate for SSL offload
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password "P@ssw0rd"
# Create a frontend IP configuration for hello public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
# Create a new listener with hello certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
# Define hello size of hello application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
# Configure hello SSL policy toouse a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
# Create hello application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="next-steps"></a><span data-ttu-id="e6ca9-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6ca9-132">Next steps</span></span>

<span data-ttu-id="e6ca9-133">請瀏覽[應用程式閘道重新導向概觀](application-gateway-redirect-overview.md)toolearn tooredirect HTTP 流量 tooa HTTPS 端點的方式。</span><span class="sxs-lookup"><span data-stu-id="e6ca9-133">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn how tooredirect HTTP traffic tooa HTTPS endpoint.</span></span>
