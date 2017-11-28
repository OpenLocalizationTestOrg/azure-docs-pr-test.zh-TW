---
title: "aaaConfigure SSL 卸載 Azure 應用程式閘道-PowerShell 傳統 |Microsoft 文件"
description: "本文章提供應用程式閘道以 SSL 卸載使用 toocreate hello Azure 傳統部署模型的指示。"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="9b7ce-103">設定 SSL 卸載的應用程式閘道使用 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="9b7ce-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b7ce-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9b7ce-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="9b7ce-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7ce-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="9b7ce-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b7ce-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="9b7ce-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9b7ce-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="9b7ce-108">Azure 應用程式閘道可以在 hello 閘道 tooavoid 昂貴 SSL 解密工作 toohappen hello web 伺服陣列設定的 tooterminate hello Secure Sockets Layer (SSL) 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="9b7ce-109">Hello 前端伺服器安裝並管理 hello web 應用程式，也可以簡化 SSL 卸載。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9b7ce-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="9b7ce-110">Before you begin</span></span>

1. <span data-ttu-id="9b7ce-111">使用 hello Web Platform Installer 安裝 hello hello Azure PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="9b7ce-112">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9b7ce-113">請確認您的運作中虛擬網路具有有效子網路。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="9b7ce-114">請確定沒有虛擬機器或雲端部署使用 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="9b7ce-115">hello 應用程式閘道必須單獨在虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="9b7ce-116">您設定 toouse hello 應用程式閘道的 hello 伺服器必須存在，或指派建立 hello 虛擬網路中，或是具有公用 IP/VIP 端點。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="9b7ce-117">tooconfigure SSL 卸載應用程式閘道上，執行 hello hello 依列出的順序執行步驟：</span><span class="sxs-lookup"><span data-stu-id="9b7ce-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="9b7ce-118">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9b7ce-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="9b7ce-119">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="9b7ce-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="9b7ce-120">Hello 閘道設定</span><span class="sxs-lookup"><span data-stu-id="9b7ce-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="9b7ce-121">設定 hello 閘道組態</span><span class="sxs-lookup"><span data-stu-id="9b7ce-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="9b7ce-122">啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="9b7ce-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="9b7ce-123">驗證 hello 閘道器狀態</span><span class="sxs-lookup"><span data-stu-id="9b7ce-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="9b7ce-124">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="9b7ce-124">Create an application gateway</span></span>

<span data-ttu-id="9b7ce-125">toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="9b7ce-126">此時無法啟動的 hello 閘道計費。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="9b7ce-127">計費開始在稍後步驟中，當 hello 閘道已順利啟動。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="9b7ce-128">hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="9b7ce-129">在 hello 範例中，*描述*， *InstanceCount*，和*GatewaySize*是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="9b7ce-130">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="9b7ce-131">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="9b7ce-132">Small 和 Large 也是可用的值。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-132">Small and Large are other available values.</span></span> <span data-ttu-id="9b7ce-133">*如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="9b7ce-134">執行中狀態的 hello hello 閘道之後，會建立這些值。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="9b7ce-135">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="9b7ce-135">Upload SSL certificates</span></span>

<span data-ttu-id="9b7ce-136">使用`Add-AzureApplicationGatewaySslCertificate`tooupload hello 伺服器憑證中的*pfx*格式 toohello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="9b7ce-137">hello 憑證名稱是使用者所選名稱，而且必須是唯一在 hello 應用程式閘道中。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="9b7ce-138">此憑證是參照的 tooby hello 應用程式閘道上的所有憑證管理作業的這個名稱。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="9b7ce-139">此下列範例顯示 hello cmdlet，在 hello 範例中的 hello 值取代為您自己。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="9b7ce-140">接下來，驗證 hello 憑證上傳。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="9b7ce-141">使用 hello `Get-AzureApplicationGatewayCertificate` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="9b7ce-142">這個範例會顯示 hello cmdlet hello 第一行，後面接著 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="9b7ce-143">hello 憑證密碼有 toobe 之間 4 too12 字元、 字母或數字。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="9b7ce-144">不接受使用特殊字元。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="9b7ce-145">Hello 閘道設定</span><span class="sxs-lookup"><span data-stu-id="9b7ce-145">Configure hello gateway</span></span>

<span data-ttu-id="9b7ce-146">應用程式閘道組態是由多個值所組成。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="9b7ce-147">hello 值可以繫結在一起的 tooconstruct hello 組態。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="9b7ce-148">hello 的值如下：</span><span class="sxs-lookup"><span data-stu-id="9b7ce-148">hello values are:</span></span>

* <span data-ttu-id="9b7ce-149">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="9b7ce-150">列出 hello IP 位址應該是屬於 toohello 虛擬網路子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="9b7ce-151">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="9b7ce-152">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="9b7ce-153">**前端連接埠：**此連接埠是開啟 hello 應用程式閘道上的 hello 公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="9b7ce-154">流量叫用這個連接埠，然後再取得重新導向 tooone 的 hello 後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="9b7ce-155">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些值會區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="9b7ce-156">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="9b7ce-157">目前，只有 hello*基本*規則支援。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="9b7ce-158">hello*基本*規則是循環配置資源負載分佈。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="9b7ce-159">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="9b7ce-159">**Additional configuration notes**</span></span>

<span data-ttu-id="9b7ce-160">SSL 憑證設定，如 hello 中的通訊協定**HttpListener**也應該變更*Https* （區分大小寫）。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="9b7ce-161">hello **SslCert**太新增項目**HttpListener** hello 與值設定的 toohello hello 上傳之前 SSL 憑證 > 一節中所使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="9b7ce-162">hello 前端連接埠應為更新的 too443。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="9b7ce-163">**tooenable cookie 為基礎的同質**： 應用程式閘道可以是來自用戶端工作階段的要求會導向的 toohello 設定的 tooensure hello web 伺服陣列中相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="9b7ce-164">此案例中是由資料隱碼的工作階段 cookie，可讓 hello 閘道 toodirect 流量時，適當地完成。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="9b7ce-165">tooenable cookie 架構親和性，設定**CookieBasedAffinity**太*啟用*在 hello **BackendHttpSettings**項目。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="9b7ce-166">建立組態物件或使用組態 XML 檔案，即可建構組態。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="9b7ce-167">tooconstruct 您使用組態 XML 檔案的組態，請使用下列範例 hello:</span><span class="sxs-lookup"><span data-stu-id="9b7ce-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="9b7ce-168">**組態 XML 範例**</span><span class="sxs-lookup"><span data-stu-id="9b7ce-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="9b7ce-169">設定 hello 閘道組態</span><span class="sxs-lookup"><span data-stu-id="9b7ce-169">Set hello gateway configuration</span></span>

<span data-ttu-id="9b7ce-170">接下來，您可以設定 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="9b7ce-171">您可以使用 hello`Set-AzureApplicationGatewayConfig`指令程式與組態的物件或設定 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="9b7ce-172">啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="9b7ce-172">Start hello gateway</span></span>

<span data-ttu-id="9b7ce-173">一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="9b7ce-174">在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="9b7ce-175">hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toofinish too15 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="9b7ce-176">驗證 hello 閘道器狀態</span><span class="sxs-lookup"><span data-stu-id="9b7ce-176">Verify hello gateway status</span></span>

<span data-ttu-id="9b7ce-177">使用 hello `Get-AzureApplicationGateway` hello 閘道 cmdlet toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="9b7ce-178">如果`Start-AzureApplicationGateway`hello 先前步驟中，在成功*狀態*應執行和*如*和*DnsName*應該具有有效的項目。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="9b7ce-179">這個範例會顯示應用程式閘道的執行中，已啟動，且準備好 tootake 流量。</span><span class="sxs-lookup"><span data-stu-id="9b7ce-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="9b7ce-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b7ce-180">Next steps</span></span>

<span data-ttu-id="9b7ce-181">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="9b7ce-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="9b7ce-182">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9b7ce-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="9b7ce-183">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="9b7ce-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

