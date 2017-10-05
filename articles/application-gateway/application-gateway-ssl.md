---
title: "設定 SSL 卸載 - Azure 應用程式閘道 - PowerShell 傳統 | Microsoft Docs"
description: "本文提供使用 Azure 傳統部署模型建立具有 SSL 卸載之應用程式閘道的指示。"
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="a7506-103">使用傳統部署模型設定適用於 SSL 卸載的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7506-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a7506-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="a7506-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7506-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="a7506-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7506-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="a7506-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a7506-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="a7506-108">Azure 應用程式閘道可以設定為在閘道終止安全通訊端層 (SSL) 工作階段，以避免 Web 伺服陣列發生高成本的 SSL 解密工作。</span><span class="sxs-lookup"><span data-stu-id="a7506-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="a7506-109">SSL 卸載也可以簡化 Web 應用程式的前端伺服器設定和管理。</span><span class="sxs-lookup"><span data-stu-id="a7506-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a7506-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="a7506-110">Before you begin</span></span>

1. <span data-ttu-id="a7506-111">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a7506-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="a7506-112">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="a7506-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="a7506-113">請確認您的運作中虛擬網路具有有效子網路。</span><span class="sxs-lookup"><span data-stu-id="a7506-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="a7506-114">請確定沒有虛擬機器或是雲端部署正在使用子網路。</span><span class="sxs-lookup"><span data-stu-id="a7506-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="a7506-115">應用程式閘道必須單獨位於虛擬網路子網路中。</span><span class="sxs-lookup"><span data-stu-id="a7506-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="a7506-116">您要設定來使用應用程式閘道的伺服器必須存在，或是在虛擬網路中建立其端點，或是已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="a7506-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="a7506-117">若要在應用程式閘道上設定 SSL 卸載，請依列出的順序執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a7506-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="a7506-118">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="a7506-119">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="a7506-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="a7506-120">設定閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="a7506-121">設定閘道組態</span><span class="sxs-lookup"><span data-stu-id="a7506-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="a7506-122">啟動閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="a7506-123">確認閘道狀態</span><span class="sxs-lookup"><span data-stu-id="a7506-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="a7506-124">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-124">Create an application gateway</span></span>

<span data-ttu-id="a7506-125">若要建立閘道，請使用 `New-AzureApplicationGateway` Cmdlet，並以您自己的值來取代這些值。</span><span class="sxs-lookup"><span data-stu-id="a7506-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="a7506-126">此時還不會開始對閘道計費。</span><span class="sxs-lookup"><span data-stu-id="a7506-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="a7506-127">會在稍後的步驟中於成功啟動閘道之後開始計費。</span><span class="sxs-lookup"><span data-stu-id="a7506-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="a7506-128">若要驗證已建立閘道，您可以使用 `Get-AzureApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a7506-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="a7506-129">在範例中，*Description*、*InstanceCount* 及 *GatewaySize* 是選用參數。</span><span class="sxs-lookup"><span data-stu-id="a7506-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="a7506-130">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="a7506-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a7506-131">*GatewaySize* 的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="a7506-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a7506-132">Small 和 Large 也是可用的值。</span><span class="sxs-lookup"><span data-stu-id="a7506-132">Small and Large are other available values.</span></span> <span data-ttu-id="a7506-133">因為尚未啟動閘道，所以 VirtualIPs 和 DnsName 會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="a7506-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="a7506-134">閘道處於執行中狀態之後，就會建立這些值。</span><span class="sxs-lookup"><span data-stu-id="a7506-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="a7506-135">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="a7506-135">Upload SSL certificates</span></span>

<span data-ttu-id="a7506-136">使用 `Add-AzureApplicationGatewaySslCertificate`，將伺服器憑證 (*pfx* 格式) 上傳至應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7506-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="a7506-137">憑證名稱是使用者選擇的名稱，而且必須在應用程式閘道中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a7506-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="a7506-138">應用程式閘道上的所有憑證管理作業會使用此名稱參考該憑證。</span><span class="sxs-lookup"><span data-stu-id="a7506-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="a7506-139">下列範例會顯示 Cmdlet，請將範例中的值取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="a7506-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="a7506-140">接下來，驗證憑證上傳。</span><span class="sxs-lookup"><span data-stu-id="a7506-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="a7506-141">使用 `Get-AzureApplicationGatewayCertificate` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a7506-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="a7506-142">這個範例的第一行顯示 Cmdlet，後面接著輸出。</span><span class="sxs-lookup"><span data-stu-id="a7506-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="a7506-143">憑證密碼必須由 4 到 12 個字元、字母或數字所組成。</span><span class="sxs-lookup"><span data-stu-id="a7506-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="a7506-144">不接受使用特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a7506-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="a7506-145">設定閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-145">Configure the gateway</span></span>

<span data-ttu-id="a7506-146">應用程式閘道組態是由多個值所組成。</span><span class="sxs-lookup"><span data-stu-id="a7506-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="a7506-147">可以將值繫結在一起，以建構組態。</span><span class="sxs-lookup"><span data-stu-id="a7506-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="a7506-148">值如下：</span><span class="sxs-lookup"><span data-stu-id="a7506-148">The values are:</span></span>

* <span data-ttu-id="a7506-149">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="a7506-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="a7506-150">列出的 IP 位址應屬於虛擬網路子網路或是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="a7506-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="a7506-151">**後端伺服器集區設定：** 每個集區都包括一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="a7506-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="a7506-152">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="a7506-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="a7506-153">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="a7506-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="a7506-154">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="a7506-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="a7506-155">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些值都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="a7506-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="a7506-156">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="a7506-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="a7506-157">目前只支援 *基本* 規則。</span><span class="sxs-lookup"><span data-stu-id="a7506-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="a7506-158">*基本* 規則是循環配置資源的負載分配。</span><span class="sxs-lookup"><span data-stu-id="a7506-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="a7506-159">**其他組態注意事項**</span><span class="sxs-lookup"><span data-stu-id="a7506-159">**Additional configuration notes**</span></span>

<span data-ttu-id="a7506-160">針對 SSL 憑證組態，**HttpListener** 中的通訊協定應該變更為 *Https* (區分大小寫)。</span><span class="sxs-lookup"><span data-stu-id="a7506-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="a7506-161">**SslCert** 元素會新增到 **HttpListener** 中，其值會設定為與上傳先前的 SSL 憑證一節中所使用的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="a7506-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="a7506-162">前端連接埠應該更新為 443。</span><span class="sxs-lookup"><span data-stu-id="a7506-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="a7506-163">**啟用以 Cookie 為基礎的同質性**：您可以設定應用程式閘道，以確保來自用戶端工作階段的要求一律會導向至 Web 伺服陣列中的相同 VM。</span><span class="sxs-lookup"><span data-stu-id="a7506-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="a7506-164">此案例透過插入允許閘道適當導向流量的工作階段 Cookie 來完成。</span><span class="sxs-lookup"><span data-stu-id="a7506-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="a7506-165">若要啟用以 Cookie 為基礎的同質性，請在 **BackendHttpSettings** 元素中將 **CookieBasedAffinity** 設定為 *Enabled*。</span><span class="sxs-lookup"><span data-stu-id="a7506-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="a7506-166">建立組態物件或使用組態 XML 檔案，即可建構組態。</span><span class="sxs-lookup"><span data-stu-id="a7506-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="a7506-167">若要使用組態 XML 檔案以建構組態，請使用下列範例：</span><span class="sxs-lookup"><span data-stu-id="a7506-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="a7506-168">**組態 XML 範例**</span><span class="sxs-lookup"><span data-stu-id="a7506-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="a7506-169">設定閘道組態</span><span class="sxs-lookup"><span data-stu-id="a7506-169">Set the gateway configuration</span></span>

<span data-ttu-id="a7506-170">接下來，您需要設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="a7506-170">Next, you set the application gateway.</span></span> <span data-ttu-id="a7506-171">您可以搭配組態物件或組態 XML 檔案來使用 `Set-AzureApplicationGatewayConfig` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a7506-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="a7506-172">啟動閘道</span><span class="sxs-lookup"><span data-stu-id="a7506-172">Start the gateway</span></span>

<span data-ttu-id="a7506-173">設定閘道之後，請使用 `Start-AzureApplicationGateway` Cmdlet 來啟動閘道。</span><span class="sxs-lookup"><span data-stu-id="a7506-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="a7506-174">成功啟動閘道之後，會開始應用程式閘道計費。</span><span class="sxs-lookup"><span data-stu-id="a7506-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="a7506-175">`Start-AzureApplicationGateway` Cmdlet 最多可能需要 15 到 20 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="a7506-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="a7506-176">確認閘道狀態</span><span class="sxs-lookup"><span data-stu-id="a7506-176">Verify the gateway status</span></span>

<span data-ttu-id="a7506-177">使用 `Get-AzureApplicationGateway` Cmdlet 檢查閘道狀態。</span><span class="sxs-lookup"><span data-stu-id="a7506-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="a7506-178">如果上一個步驟中的 `Start-AzureApplicationGateway` 成功，則 *State* 應該是 Running，而且 *VirtualIPs* 和 *DnsName* 應該具備有效的輸入。</span><span class="sxs-lookup"><span data-stu-id="a7506-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="a7506-179">這個範例所示範的應用程式閘道已啟動、執行中並準備好要接受流量。</span><span class="sxs-lookup"><span data-stu-id="a7506-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7506-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7506-180">Next steps</span></span>

<span data-ttu-id="a7506-181">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a7506-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="a7506-182">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="a7506-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="a7506-183">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="a7506-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

