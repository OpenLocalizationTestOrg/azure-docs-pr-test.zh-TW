---
title: "使用 Azure 應用程式閘道搭配內部負載平衡器 | Microsoft Docs"
description: "本頁面提供的指示可讓您使用內部負載平衡端點來設定 Azure 應用程式閘道"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="59dd6-103">搭配內部負載平衡器 (ILB) 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="59dd6-104">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="59dd6-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="59dd6-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="59dd6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="59dd6-106">可以使用面對網際網路的虛擬 IP 或不會對網際網路公開的內部端點 (也稱為內部負載平衡器 (ILB) 端點) 來設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="59dd6-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="59dd6-107">使用 ILB 設定閘道適合不會對網際網路公開的內部企業營運應用程式。</span><span class="sxs-lookup"><span data-stu-id="59dd6-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="59dd6-108">對於位在不會對網際網路公開的安全性界限中的多層式應用程式內的服務/階層也很有用的，但仍需要循環配置資源負載散發、工作階段綁定或 SSL 終止。</span><span class="sxs-lookup"><span data-stu-id="59dd6-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="59dd6-109">本文會逐步引導您完成使用 ILB 設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="59dd6-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="59dd6-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="59dd6-110">Before you begin</span></span>

1. <span data-ttu-id="59dd6-111">使用 Web Platform Installer 安裝最新版的 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="59dd6-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="59dd6-112">您可以從 **下載頁面** 的 [Windows PowerShell](https://azure.microsoft.com/downloads/)區段下載並安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="59dd6-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="59dd6-113">請確認您有運作中的虛擬網路，且其子網路有效。</span><span class="sxs-lookup"><span data-stu-id="59dd6-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="59dd6-114">請確認您的後端伺服器位於虛擬網路中，或已指派公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="59dd6-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="59dd6-115">若要建立應用程式閘道，請依列出的順序執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="59dd6-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="59dd6-116">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="59dd6-117">設定閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="59dd6-118">設定閘道組態</span><span class="sxs-lookup"><span data-stu-id="59dd6-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="59dd6-119">啟動閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="59dd6-120">確認閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="59dd6-121">建立應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="59dd6-121">Create an application gateway:</span></span>

<span data-ttu-id="59dd6-122">**若要建立閘道**，請使用 `New-AzureApplicationGateway` Cmdlet，並以您自己的值來取代這些值。</span><span class="sxs-lookup"><span data-stu-id="59dd6-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="59dd6-123">請注意，此時不會開始為閘道計費。</span><span class="sxs-lookup"><span data-stu-id="59dd6-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="59dd6-124">會在稍後的步驟中於成功啟動閘道之後開始計費。</span><span class="sxs-lookup"><span data-stu-id="59dd6-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="59dd6-125">**若要驗證**已建立閘道，您可以使用 `Get-AzureApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="59dd6-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="59dd6-126">在範例中，*Description*、*InstanceCount* 及 *GatewaySize* 是選用參數。</span><span class="sxs-lookup"><span data-stu-id="59dd6-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="59dd6-127">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="59dd6-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="59dd6-128">*GatewaySize* 的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="59dd6-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="59dd6-129">Small 和 Large 也是可用的值。</span><span class="sxs-lookup"><span data-stu-id="59dd6-129">Small and Large are other available values.</span></span> <span data-ttu-id="59dd6-130">因為尚未啟動閘道，所以 *Vip* 和 *DnsName* 會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="59dd6-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="59dd6-131">閘道處於執行中狀態之後，就會建立這些項目。</span><span class="sxs-lookup"><span data-stu-id="59dd6-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="59dd6-132">設定閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-132">Configure the gateway</span></span>
<span data-ttu-id="59dd6-133">應用程式閘道組態是由多個值所組成。</span><span class="sxs-lookup"><span data-stu-id="59dd6-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="59dd6-134">可以將值繫結在一起，以建構組態。</span><span class="sxs-lookup"><span data-stu-id="59dd6-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="59dd6-135">值如下：</span><span class="sxs-lookup"><span data-stu-id="59dd6-135">The values are:</span></span>

* <span data-ttu-id="59dd6-136">**後端伺服器集區：** 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="59dd6-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="59dd6-137">列出的 IP 位址應該屬於 VNet 子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="59dd6-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="59dd6-138">**後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="59dd6-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="59dd6-139">這些設定會繫結至集區，並套用至集區內所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="59dd6-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="59dd6-140">**前端連接埠：** 此連接埠是在應用程式閘道上開啟的公用連接埠。</span><span class="sxs-lookup"><span data-stu-id="59dd6-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="59dd6-141">流量會到達此連接埠，然後重新導向至其中一個後端伺服器。</span><span class="sxs-lookup"><span data-stu-id="59dd6-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="59dd6-142">**接聽程式：** 接聽程式具有前端連接埠、通訊協定 (Http 或 Https，這些都區分大小寫) 和 SSL 憑證名稱 (如果已設定 SSL 卸載)。</span><span class="sxs-lookup"><span data-stu-id="59dd6-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="59dd6-143">**規則：** 規則會繫結接聽程式和後端伺服器集區，並定義當流量到達特定接聽程式時，應該導向到哪個後端伺服器集區。</span><span class="sxs-lookup"><span data-stu-id="59dd6-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="59dd6-144">目前，只支援 *基本* 規則。</span><span class="sxs-lookup"><span data-stu-id="59dd6-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="59dd6-145">「基本」  規則是循環配置資源的負載分散。</span><span class="sxs-lookup"><span data-stu-id="59dd6-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="59dd6-146">建立組態物件或使用組態 XML 檔案，即可建構組態。</span><span class="sxs-lookup"><span data-stu-id="59dd6-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="59dd6-147">若要使用組態 XML 檔案以建構組態，請使用下面的範例。</span><span class="sxs-lookup"><span data-stu-id="59dd6-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="59dd6-148">請注意：</span><span class="sxs-lookup"><span data-stu-id="59dd6-148">Note the following:</span></span>

* <span data-ttu-id="59dd6-149">*FrontendIPConfigurations* 元素描述設定搭配 ILB 之應用程式閘道器的相關 ILB 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="59dd6-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="59dd6-150">前端 IP *類型* 應該設定為「私人」</span><span class="sxs-lookup"><span data-stu-id="59dd6-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="59dd6-151">StaticIPAddress 應該設定為需要的內部 IP，閘道會在該處接收流量。</span><span class="sxs-lookup"><span data-stu-id="59dd6-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="59dd6-152">請注意，StaticIPAddress 元素為選擇性。</span><span class="sxs-lookup"><span data-stu-id="59dd6-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="59dd6-153">如果未設定，會選擇來自已部署子網路的可用內部 IP。</span><span class="sxs-lookup"><span data-stu-id="59dd6-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="59dd6-154">在 FrontendIPConfiguration 中指定的 Name 元素的值應該用於 HTTPListener 的 FrontendIP 元素，以指向 FrontendIPConfiguration。</span><span class="sxs-lookup"><span data-stu-id="59dd6-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="59dd6-155">**組態 XML 範例**</span><span class="sxs-lookup"><span data-stu-id="59dd6-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="59dd6-156">設定閘道組態</span><span class="sxs-lookup"><span data-stu-id="59dd6-156">Set the gateway configuration</span></span>
<span data-ttu-id="59dd6-157">接下來，您將設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="59dd6-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="59dd6-158">您可以搭配使用 `Set-AzureApplicationGatewayConfig` Cmdlet 與組態物件或組態 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="59dd6-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="59dd6-159">啟動閘道</span><span class="sxs-lookup"><span data-stu-id="59dd6-159">Start the gateway</span></span>

<span data-ttu-id="59dd6-160">設定閘道之後，請使用 `Start-AzureApplicationGateway` Cmdlet 來啟動閘道。</span><span class="sxs-lookup"><span data-stu-id="59dd6-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="59dd6-161">成功啟動閘道之後，會開始應用程式閘道計費。</span><span class="sxs-lookup"><span data-stu-id="59dd6-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="59dd6-162">「基本」 `Start-AzureApplicationGateway` Cmdlet 最多可能需要 15 到 20 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="59dd6-162">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete.</span></span> 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="59dd6-163">確認閘道狀態</span><span class="sxs-lookup"><span data-stu-id="59dd6-163">Verify the gateway status</span></span>

<span data-ttu-id="59dd6-164">使用 `Get-AzureApplicationGateway` Cmdlet 來檢查閘道狀態。</span><span class="sxs-lookup"><span data-stu-id="59dd6-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="59dd6-165">如果上一個步驟中的 `Start-AzureApplicationGateway` 成功，則 State 應該是 Running，而且 Vip 和 DnsName 應該具備有效的輸入。</span><span class="sxs-lookup"><span data-stu-id="59dd6-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="59dd6-166">這個範例的第一行顯示 Cmdlet，後面接著輸出。</span><span class="sxs-lookup"><span data-stu-id="59dd6-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="59dd6-167">在此範例中，閘道正在執行，且準備好要接受流量。</span><span class="sxs-lookup"><span data-stu-id="59dd6-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="59dd6-168">此範例中是將應用程式閘道器設定為在所設定的 ILB 端點 10.0.0.10 接受流量。</span><span class="sxs-lookup"><span data-stu-id="59dd6-168">The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="59dd6-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59dd6-169">Next steps</span></span>
<span data-ttu-id="59dd6-170">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="59dd6-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="59dd6-171">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="59dd6-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="59dd6-172">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="59dd6-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

