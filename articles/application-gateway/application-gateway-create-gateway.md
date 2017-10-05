---
title: "建立、啟動或刪除應用程式閘道 | Microsoft Docs"
description: "本頁面提供建立、設定、啟動和刪除 Azure 應用程式閘道的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: c4932096229b1941e0966e7f3e97de39c6931392
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="5f8bb-103">使用 PowerShell 建立、啟動或刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f8bb-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5f8bb-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="5f8bb-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f8bb-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="5f8bb-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f8bb-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="5f8bb-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="5f8bb-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="5f8bb-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5f8bb-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="5f8bb-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="5f8bb-110">不論是在雲端或內部部署中，此閘道均提供在不同伺服器之間進行容錯移轉及效能路由傳送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="5f8bb-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健全狀態探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="5f8bb-112">若要尋找完整的支援功能清單，請瀏覽 [應用程式閘道概觀](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="5f8bb-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="5f8bb-113">本文將逐步引導您完成建立、設定、啟動及刪除應用程式閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5f8bb-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="5f8bb-114">Before you begin</span></span>

1. <span data-ttu-id="5f8bb-115">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="5f8bb-116">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="5f8bb-117">如果您有現有的虛擬網路，請選取現有的空白子網路，或在現有的虛擬網路中建立新的子網路，僅供應用程式閘道使用。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="5f8bb-118">除非使用 VNet 對等互連，否則，您無法將應用程式閘道部署到與您打算部署於應用程式閘道後方的資源不同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="5f8bb-119">如需深入了解，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5f8bb-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="5f8bb-120">請確認您的運作中虛擬網路具有有效子網路。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="5f8bb-121">請確定沒有虛擬機器或是雲端部署正在使用子網路。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="5f8bb-122">應用程式閘道必須單獨位於虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="5f8bb-123">您要設定來使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="5f8bb-124">建立應用程式閘道需要什麼？</span><span class="sxs-lookup"><span data-stu-id="5f8bb-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="5f8bb-125">當您使用 `New-AzureApplicationGateway` 命令來建立應用程式閘道時，此時不需進行任何設定，並使用 XML 或組態物件來設定新建立的資源。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="5f8bb-126">值如下：</span><span class="sxs-lookup"><span data-stu-id="5f8bb-126">The values are:</span></span>

* <span data-ttu-id="5f8bb-127">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="5f8bb-128">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="5f8bb-129">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="5f8bb-130">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="5f8bb-131">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="5f8bb-132">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="5f8bb-133">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="5f8bb-134">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="5f8bb-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-135">Create an application gateway</span></span>

<span data-ttu-id="5f8bb-136">建立應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="5f8bb-136">To create an application gateway:</span></span>

1. <span data-ttu-id="5f8bb-137">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="5f8bb-138">建立設定 XML 檔案或設定物件。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="5f8bb-139">認可新建立應用程式閘道資源的設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5f8bb-140">如果您需要設定應用程式閘道的自訂探查，請參閱 [使用 PowerShell 建立具有自訂探查的應用程式閘道](application-gateway-create-probe-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-140">If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="5f8bb-141">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![案例範例][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="5f8bb-143">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="5f8bb-143">Create an application gateway resource</span></span>

<span data-ttu-id="5f8bb-144">若要建立閘道，請使用 `New-AzureApplicationGateway` Cmdlet，並以您自己的值來取代這些值。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="5f8bb-145">此時還不會開始對閘道計費。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="5f8bb-146">會在稍後的步驟中於成功啟動閘道之後開始計費。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="5f8bb-147">下列範例會使用名為 "testvnet1" 的虛擬網路和名為 "subnet-1" 的子網路來建立應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="5f8bb-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="5f8bb-148">Description、InstanceCount 和 GatewaySize 為選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="5f8bb-149">若要驗證已建立閘道，您可以使用 `Get-AzureApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="5f8bb-150">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-150">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="5f8bb-151">GatewaySize  的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-151">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="5f8bb-152">您可以選擇 Small、Medium 和 Large。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="5f8bb-153">因為尚未啟動閘道，所以 VirtualIPs 和 DnsName 會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="5f8bb-154">閘道處於執行中狀態之後，就會建立這些項目。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="5f8bb-155">設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-155">Configure the application gateway</span></span>

<span data-ttu-id="5f8bb-156">您可以使用 XML 或設定物件來設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="5f8bb-157">使用 XML 設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="5f8bb-158">在下列範例中，您將使用 XML 檔案來設定所有應用程式閘道設定，並將它們認可到應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="5f8bb-159">步驟 1</span><span class="sxs-lookup"><span data-stu-id="5f8bb-159">Step 1</span></span>

<span data-ttu-id="5f8bb-160">將下列文字複製到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="5f8bb-161">編輯設定項目括號間的值。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="5f8bb-162">以 .xml 副檔名儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f8bb-163">通訊協定項目 Http 或 Https 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-163">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="5f8bb-164">下列範例示範如何使用組態檔來設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="5f8bb-165">此範例會平衡公用連接埠 80 上的 HTTP 流量負載，並將網路流量傳送至兩個 IP 位址之間的後端連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="5f8bb-166">步驟 2</span><span class="sxs-lookup"><span data-stu-id="5f8bb-166">Step 2</span></span>

<span data-ttu-id="5f8bb-167">接下來，設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-167">Next, set the application gateway.</span></span> <span data-ttu-id="5f8bb-168">使用 `Set-AzureApplicationGatewayConfig` Cmdlet 搭配組態 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="5f8bb-169">使用設定物件設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="5f8bb-170">下列範例示範如何使用設定物件來設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="5f8bb-171">必須個別設定所有組態項目，然後再將其新增至應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="5f8bb-172">建立組態物件之後，您會使用 `Set-AzureApplicationGateway` 命令，將組態認可到先前建立的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="5f8bb-173">在將值指派到各個設定物件之前，您必須宣告 PowerShell 要用來儲存的物件種類。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-173">Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="5f8bb-174">建立個別項目的第一行會定義要使用哪些 `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)`。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-174">The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="5f8bb-175">步驟 1</span><span class="sxs-lookup"><span data-stu-id="5f8bb-175">Step 1</span></span>

<span data-ttu-id="5f8bb-176">建立所有的個別設定項目。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-176">Create all individual configuration items.</span></span>

<span data-ttu-id="5f8bb-177">建立前端 IP，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="5f8bb-178">建立前端連接埠，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="5f8bb-179">建立後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-179">Create the back-end server pool.</span></span>

<span data-ttu-id="5f8bb-180">定義加入至後端伺服器集區的 IP 位址，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="5f8bb-181">使用 $server 物件，將值加入至後端集區物件 ($pool)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="5f8bb-182">建立後端伺服器集區設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="5f8bb-183">建立接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="5f8bb-184">建立規則。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="5f8bb-185">步驟 2</span><span class="sxs-lookup"><span data-stu-id="5f8bb-185">Step 2</span></span>

<span data-ttu-id="5f8bb-186">將所有的個別設定項目指派給應用程式閘道設定物件 ($appgwconfig)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="5f8bb-187">將前端 IP 加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="5f8bb-188">將前端連接埠加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="5f8bb-189">將後端伺服器集區加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="5f8bb-190">將後端集區設定加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="5f8bb-191">將接聽程式加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="5f8bb-192">將規則加入設定。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="5f8bb-193">步驟 3</span><span class="sxs-lookup"><span data-stu-id="5f8bb-193">Step 3</span></span>
<span data-ttu-id="5f8bb-194">使用 `Set-AzureApplicationGatewayConfig`，將組態物件認可到應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="5f8bb-195">啟動閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-195">Start the gateway</span></span>

<span data-ttu-id="5f8bb-196">設定閘道之後，請使用 `Start-AzureApplicationGateway` Cmdlet 來啟動閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="5f8bb-197">成功啟動閘道之後，會開始應用程式閘道計費。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="5f8bb-198">`Start-AzureApplicationGateway` Cmdlet 最多可能需要 15 到 20 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-198">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="5f8bb-199">確認閘道狀態</span><span class="sxs-lookup"><span data-stu-id="5f8bb-199">Verify the gateway status</span></span>

<span data-ttu-id="5f8bb-200">使用 `Get-AzureApplicationGateway` Cmdlet 檢查閘道狀態。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="5f8bb-201">如果上一個步驟中的 `Start-AzureApplicationGateway` 成功，則 *State* 應該是 Running，而且 *Vip* 和 *DnsName* 應該具備有效的輸入。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="5f8bb-202">下列範例示範已啟動、正在執行且準備好將流量傳送到 `http://<generated-dns-name>.cloudapp.net`的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="5f8bb-203">刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="5f8bb-203">Delete the application gateway</span></span>

<span data-ttu-id="5f8bb-204">若要刪除應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="5f8bb-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="5f8bb-205">使用 `Stop-AzureApplicationGateway` Cmdlet 停止閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="5f8bb-206">使用 `Remove-AzureApplicationGateway` Cmdlet 移除閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="5f8bb-207">使用 `Get-AzureApplicationGateway` Cmdlet 確認已移除閘道。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="5f8bb-208">下列範例會在第一行顯示 `Stop-AzureApplicationGateway` Cmdlet，後面接著輸出。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="5f8bb-209">當應用程式閘道處於已停止狀態之後，使用 `Remove-AzureApplicationGateway` Cmdlet 來移除服務。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="5f8bb-210">若要確認已移除服務，您可以使用 `Get-AzureApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="5f8bb-211">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="5f8bb-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5f8bb-212">Next steps</span></span>

<span data-ttu-id="5f8bb-213">如果您想要設定 SSL 卸載，請參閱 [設定應用程式閘道以進行 SSL 卸載](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="5f8bb-214">如果您想要將應用程式閘道設為與內部負載平衡器搭配使用，請參閱 [建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="5f8bb-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="5f8bb-215">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="5f8bb-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="5f8bb-216">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5f8bb-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="5f8bb-217">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="5f8bb-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
