---
title: "aaaCreate，啟動或刪除應用程式閘道 |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定、 啟動和刪除 Azure 應用程式閘道"
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
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="865a1-103">使用 PowerShell 建立、啟動或刪除應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="865a1-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="865a1-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="865a1-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="865a1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="865a1-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="865a1-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="865a1-107">Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="865a1-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="865a1-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="865a1-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="865a1-109">Azure 應用程式閘道是第 7 層負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="865a1-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="865a1-110">無論是在 hello 雲端或內部部署上，它會提供容錯移轉時，效能路由不同的伺服器之間的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="865a1-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="865a1-111">應用程式閘道提供許多應用程式傳遞控制器 (ADC) 功能，包括 HTTP 負載平衡、以 Cookie 為基礎的工作階段同質性、安全通訊端層 (SSL) 卸載、自訂健全狀態探查、多網站支援，以及許多其他功能。</span><span class="sxs-lookup"><span data-stu-id="865a1-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="865a1-112">toofind 完整支援的功能清單，請瀏覽[應用程式閘道概觀](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="865a1-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="865a1-113">本文將引導您完成 hello 步驟 toocreate、 設定、 啟動及刪除應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="865a1-114">開始之前</span><span class="sxs-lookup"><span data-stu-id="865a1-114">Before you begin</span></span>

1. <span data-ttu-id="865a1-115">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="865a1-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="865a1-116">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="865a1-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="865a1-117">如果您有現有的虛擬網路，選取現有的空白子網路，或僅用於在現有的虛擬網路中建立新的子網路，hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="865a1-118">您無法將部署 hello 應用程式閘道 tooa 不同虛擬網路 hello 資源比您想 hello 應用程式閘道後方 toodeploy 除非使用了對等互連的 vnet。</span><span class="sxs-lookup"><span data-stu-id="865a1-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="865a1-119">toolearn 更造訪[對等互連的 Vnet](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="865a1-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="865a1-120">請確認您的運作中虛擬網路具有有效子網路。</span><span class="sxs-lookup"><span data-stu-id="865a1-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="865a1-121">請確定沒有虛擬機器或雲端部署使用 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="865a1-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="865a1-122">hello 應用程式閘道必須單獨在虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="865a1-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="865a1-123">您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。</span><span class="sxs-lookup"><span data-stu-id="865a1-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="865a1-124">什麼是必要的 toocreate 應用程式閘道？</span><span class="sxs-lookup"><span data-stu-id="865a1-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="865a1-125">當您使用 hello`New-AzureApplicationGateway`命令 toocreate hello 應用程式閘道，此時設定任何設定，以及設定 hello 新建立的資源使用 XML 或設定物件。</span><span class="sxs-lookup"><span data-stu-id="865a1-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="865a1-126">hello 的值如下：</span><span class="sxs-lookup"><span data-stu-id="865a1-126">hello values are:</span></span>

* <span data-ttu-id="865a1-127">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="865a1-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="865a1-128">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="865a1-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="865a1-129">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="865a1-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="865a1-130">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="865a1-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="865a1-131">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="865a1-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="865a1-132">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="865a1-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="865a1-133">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="865a1-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="865a1-134">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="865a1-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="865a1-135">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-135">Create an application gateway</span></span>

<span data-ttu-id="865a1-136">toocreate 應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="865a1-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="865a1-137">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="865a1-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="865a1-138">建立設定 XML 檔案或設定物件。</span><span class="sxs-lookup"><span data-stu-id="865a1-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="865a1-139">認可新建立的應用程式閘道資源 hello 組態 toohello。</span><span class="sxs-lookup"><span data-stu-id="865a1-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="865a1-140">如果您需要 tooconfigure 自訂探查您應用程式閘道，請參閱[使用 PowerShell 建立應用程式閘道與自訂探查](application-gateway-create-probe-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="865a1-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="865a1-141">請參閱 [自訂探查和健全狀況監視](application-gateway-probe-overview.md) 以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="865a1-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![案例範例][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="865a1-143">建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="865a1-143">Create an application gateway resource</span></span>

<span data-ttu-id="865a1-144">toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="865a1-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="865a1-145">此時無法啟動的 hello 閘道計費。</span><span class="sxs-lookup"><span data-stu-id="865a1-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="865a1-146">計費開始在稍後步驟中，當 hello 閘道已順利啟動。</span><span class="sxs-lookup"><span data-stu-id="865a1-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="865a1-147">hello 下列範例會建立應用程式閘道使用名為"testvnet1"，稱為 「 子網路-1"的子網路的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="865a1-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="865a1-148">Description、InstanceCount 和 GatewaySize 為選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="865a1-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="865a1-149">hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="865a1-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

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
> <span data-ttu-id="865a1-150">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="865a1-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="865a1-151">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="865a1-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="865a1-152">您可以選擇 Small、Medium 和 Large。</span><span class="sxs-lookup"><span data-stu-id="865a1-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="865a1-153">*如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="865a1-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="865a1-154">這些被建立一旦 hello 閘道處於執行中狀態的 hello。</span><span class="sxs-lookup"><span data-stu-id="865a1-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="865a1-155">設定 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-155">Configure hello application gateway</span></span>

<span data-ttu-id="865a1-156">您可以使用 XML 或設定物件，以設定 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="865a1-157">使用 XML 設定 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="865a1-158">在下列範例的 hello，您可以使用 XML 檔案 tooconfigure 所有應用程式閘道設定，並認可 toohello 應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="865a1-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="865a1-159">步驟 1</span><span class="sxs-lookup"><span data-stu-id="865a1-159">Step 1</span></span>

<span data-ttu-id="865a1-160">複製下列文字 tooNotepad hello。</span><span class="sxs-lookup"><span data-stu-id="865a1-160">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="865a1-161">編輯 hello hello 設定項目的 hello 括號之間的值。</span><span class="sxs-lookup"><span data-stu-id="865a1-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="865a1-162">儲存副檔名的.xml hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="865a1-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="865a1-163">Http 或 Https 的 hello 通訊協定項目會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="865a1-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="865a1-164">hello 下列範例顯示如何 toouse 組態檔案 tooset hello 應用程式閘道設定。</span><span class="sxs-lookup"><span data-stu-id="865a1-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="865a1-165">hello 範例負載平衡公用連接埠 80 上的 HTTP 流量，並將網路流量傳送兩個 IP 位址之間的 tooback 結束連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="865a1-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

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

#### <a name="step-2"></a><span data-ttu-id="865a1-166">步驟 2</span><span class="sxs-lookup"><span data-stu-id="865a1-166">Step 2</span></span>

<span data-ttu-id="865a1-167">接下來，設定 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-167">Next, set hello application gateway.</span></span> <span data-ttu-id="865a1-168">使用 hello `Set-AzureApplicationGatewayConfig` cmdlet 搭配組態 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="865a1-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="865a1-169">使用組態物件設定 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="865a1-170">hello 下列範例顯示如何 tooconfigure hello 使用組態物件的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="865a1-171">所有設定項目必須個別設定，並接著加入 tooan 應用程式閘道組態物件。</span><span class="sxs-lookup"><span data-stu-id="865a1-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="865a1-172">建立 hello 組態物件後，您可以使用 hello`Set-AzureApplicationGateway`命令 toocommit hello 組態 toohello 先前建立的應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="865a1-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="865a1-173">之前指派值 tooeach 組態物件，您必須 toodeclare 何種物件 PowerShell 會使用儲存體。</span><span class="sxs-lookup"><span data-stu-id="865a1-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="865a1-174">hello 第一列 toocreate hello 個別項目定義項目的`Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)`可用。</span><span class="sxs-lookup"><span data-stu-id="865a1-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="865a1-175">步驟 1</span><span class="sxs-lookup"><span data-stu-id="865a1-175">Step 1</span></span>

<span data-ttu-id="865a1-176">建立所有的個別設定項目。</span><span class="sxs-lookup"><span data-stu-id="865a1-176">Create all individual configuration items.</span></span>

<span data-ttu-id="865a1-177">建立 hello 前端 IP，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="865a1-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="865a1-178">建立 hello 前端連接埠，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="865a1-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="865a1-179">建立 hello 後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="865a1-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="865a1-180">定義會加入 toohello 後端伺服器集區中 hello 下一個範例所示的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="865a1-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="865a1-181">使用 hello $server tooadd hello 值 toohello 後端集區物件 ($pool)。</span><span class="sxs-lookup"><span data-stu-id="865a1-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="865a1-182">建立 hello 後端伺服器集區設定。</span><span class="sxs-lookup"><span data-stu-id="865a1-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="865a1-183">建立 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="865a1-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="865a1-184">建立 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="865a1-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="865a1-185">步驟 2</span><span class="sxs-lookup"><span data-stu-id="865a1-185">Step 2</span></span>

<span data-ttu-id="865a1-186">所有個別設定項目 tooan 應用程式閘道組態將物件指派 ($appgwconfig)。</span><span class="sxs-lookup"><span data-stu-id="865a1-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="865a1-187">加入 hello 前端 IP toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="865a1-188">加入 hello 前端連接埠 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="865a1-189">加入 hello 後端伺服器集區 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="865a1-190">加入 hello 後端集區設定 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="865a1-191">加入 hello 接聽程式 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="865a1-192">加入 hello 規則 toohello 組態。</span><span class="sxs-lookup"><span data-stu-id="865a1-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="865a1-193">步驟 3</span><span class="sxs-lookup"><span data-stu-id="865a1-193">Step 3</span></span>
<span data-ttu-id="865a1-194">認可 hello 組態物件 toohello 應用程式閘道資源使用`Set-AzureApplicationGatewayConfig`。</span><span class="sxs-lookup"><span data-stu-id="865a1-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="865a1-195">啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-195">Start hello gateway</span></span>

<span data-ttu-id="865a1-196">一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="865a1-197">在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="865a1-198">hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toofinish too15 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="865a1-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="865a1-199">驗證 hello 閘道器狀態</span><span class="sxs-lookup"><span data-stu-id="865a1-199">Verify hello gateway status</span></span>

<span data-ttu-id="865a1-200">使用 hello `Get-AzureApplicationGateway` hello 閘道 cmdlet toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="865a1-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="865a1-201">如果`Start-AzureApplicationGateway`hello 先前步驟中，在成功*狀態*應執行和*Vip*和*DnsName*應該具有有效的項目。</span><span class="sxs-lookup"><span data-stu-id="865a1-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="865a1-202">hello 下列範例將示範會啟動、 執行的應用程式閘道，並準備好 tootake 流量目的地為`http://<generated-dns-name>.cloudapp.net`。</span><span class="sxs-lookup"><span data-stu-id="865a1-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="865a1-203">刪除 hello 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="865a1-203">Delete hello application gateway</span></span>

<span data-ttu-id="865a1-204">toodelete hello 應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="865a1-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="865a1-205">使用 hello `Stop-AzureApplicationGateway` cmdlet toostop hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="865a1-206">使用 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="865a1-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="865a1-207">確認已移除該 hello 閘道使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="865a1-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="865a1-208">hello 下列範例顯示 hello `Stop-AzureApplicationGateway` cmdlet hello 第一行，後面接著 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="865a1-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

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

<span data-ttu-id="865a1-209">處於停止狀態 hello 應用程式閘道之後，請使用 hello `Remove-AzureApplicationGateway` cmdlet tooremove hello 服務。</span><span class="sxs-lookup"><span data-stu-id="865a1-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

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

<span data-ttu-id="865a1-210">已移除 hello 服務的 tooverify，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="865a1-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="865a1-211">這不是必要步驟。</span><span class="sxs-lookup"><span data-stu-id="865a1-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="865a1-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="865a1-212">Next steps</span></span>

<span data-ttu-id="865a1-213">如果您想的 tooconfigure SSL 卸載，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="865a1-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="865a1-214">如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="865a1-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="865a1-215">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="865a1-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="865a1-216">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="865a1-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="865a1-217">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="865a1-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
