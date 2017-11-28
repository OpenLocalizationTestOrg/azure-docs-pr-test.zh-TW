---
title: "aaaUsing Azure 應用程式閘道與內部負載平衡器 |Microsoft 文件"
description: "本頁面提供的指示 tooconfigure Azure 應用程式閘道與內部負載平衡的端點"
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
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="d9438-103">搭配內部負載平衡器 (ILB) 的應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d9438-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9438-104">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9438-104">Azure Classic PowerShell</span></span>](application-gateway-ilb.md)
> * [<span data-ttu-id="d9438-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9438-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ilb-arm.md)

<span data-ttu-id="d9438-106">可設定應用程式閘道，與網際網路對向虛擬 IP，或使用不會公開內部端點 toohello 網際網路，也稱為內部負載平衡 (ILB) 端點。</span><span class="sxs-lookup"><span data-stu-id="d9438-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed toohello internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="d9438-107">適用於內部特定業務應用程式不會公開 toointernet 設定 hello 閘道搭配 ILB 一起運作。</span><span class="sxs-lookup"><span data-stu-id="d9438-107">Configuring hello gateway with an ILB is useful for internal line-of-business applications not exposed toointernet.</span></span> <span data-ttu-id="d9438-108">它也可用於服務/層內的多層式應用程式，這位於安全性界限不會公開 toointernet，但仍然需要循環配置資源負載分佈、 神奇工作階段的結果或 SSL 終止。</span><span class="sxs-lookup"><span data-stu-id="d9438-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed toointernet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="d9438-109">這篇文章會引導您 hello 步驟 tooconfigure 應用程式閘道搭配 ILB 一起運作。</span><span class="sxs-lookup"><span data-stu-id="d9438-109">This article walks you through hello steps tooconfigure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d9438-110">開始之前</span><span class="sxs-lookup"><span data-stu-id="d9438-110">Before you begin</span></span>

1. <span data-ttu-id="d9438-111">安裝最新版的 hello Azure PowerShell cmdlet 使用 hello Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="d9438-111">Install latest version of hello Azure PowerShell cmdlets using hello Web Platform Installer.</span></span> <span data-ttu-id="d9438-112">您可以從下載並安裝最新版本的 hello hello **Windows PowerShell**區段 hello[下載頁面](https://azure.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="d9438-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d9438-113">請確認您有運作中的虛擬網路，且其子網路有效。</span><span class="sxs-lookup"><span data-stu-id="d9438-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="d9438-114">請確認您有後端伺服器，在 hello 虛擬網路中，或與公用 IP/VIP 指派。</span><span class="sxs-lookup"><span data-stu-id="d9438-114">Verify that you have backend servers either in hello virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="d9438-115">toocreate 應用程式閘道，執行 hello hello 列出順序的步驟。</span><span class="sxs-lookup"><span data-stu-id="d9438-115">toocreate an application gateway, perform hello following steps in hello order listed.</span></span> 

1. [<span data-ttu-id="d9438-116">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="d9438-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="d9438-117">Hello 閘道設定</span><span class="sxs-lookup"><span data-stu-id="d9438-117">Configure hello gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="d9438-118">設定 hello 閘道組態</span><span class="sxs-lookup"><span data-stu-id="d9438-118">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="d9438-119">啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="d9438-119">Start hello gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="d9438-120">確認 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="d9438-120">Verify hello gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="d9438-121">建立應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="d9438-121">Create an application gateway:</span></span>

<span data-ttu-id="d9438-122">**toocreate hello 閘道**，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="d9438-122">**toocreate hello gateway**, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="d9438-123">請注意計費 hello 閘道不會在此時啟動。</span><span class="sxs-lookup"><span data-stu-id="d9438-123">Note that billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="d9438-124">計費開始在稍後步驟中，當 hello 閘道已順利啟動。</span><span class="sxs-lookup"><span data-stu-id="d9438-124">Billing begins in a later step, when hello gateway is successfully started.</span></span>

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

<span data-ttu-id="d9438-125">**toovalidate**建立 hello 閘道，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="d9438-125">**toovalidate** that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="d9438-126">在 hello 範例中，*描述*， *InstanceCount*，和*GatewaySize*是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="d9438-126">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="d9438-127">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="d9438-127">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d9438-128">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="d9438-128">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d9438-129">Small 和 Large 也是可用的值。</span><span class="sxs-lookup"><span data-stu-id="d9438-129">Small and Large are other available values.</span></span> <span data-ttu-id="d9438-130">*Vip*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="d9438-130">*Vip* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="d9438-131">這些被建立一旦 hello 閘道處於執行中狀態的 hello。</span><span class="sxs-lookup"><span data-stu-id="d9438-131">These are created once hello gateway is in hello running state.</span></span> 

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

## <a name="configure-hello-gateway"></a><span data-ttu-id="d9438-132">Hello 閘道設定</span><span class="sxs-lookup"><span data-stu-id="d9438-132">Configure hello gateway</span></span>
<span data-ttu-id="d9438-133">應用程式閘道組態是由多個值所組成。</span><span class="sxs-lookup"><span data-stu-id="d9438-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="d9438-134">hello 值可以繫結在一起的 tooconstruct hello 組態。</span><span class="sxs-lookup"><span data-stu-id="d9438-134">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="d9438-135">hello 的值如下：</span><span class="sxs-lookup"><span data-stu-id="d9438-135">hello values are:</span></span>

* <span data-ttu-id="d9438-136">**後端伺服器集區：** hello hello 後端伺服器的 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="d9438-136">**Backend server pool:** hello list of IP addresses of hello backend servers.</span></span> <span data-ttu-id="d9438-137">列出 hello IP 位址應該是屬於 toohello VNet 子網路，或應該是公用 IP/VIP。</span><span class="sxs-lookup"><span data-stu-id="d9438-137">hello IP addresses listed should either belong toohello VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="d9438-138">**後端伺服器集區設定：** 每個集區都有一些設定，例如連接埠、通訊協定和以 Cookie 為基礎的同質性。</span><span class="sxs-lookup"><span data-stu-id="d9438-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d9438-139">這些設定會繫結的 tooa 集區，並套用的 tooall hello 集區內的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9438-139">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="d9438-140">**前端連接埠：**則 hello 公用連接埠 hello 應用程式閘道上開啟此連接埠。</span><span class="sxs-lookup"><span data-stu-id="d9438-140">**Frontend Port:** This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="d9438-141">叫用這個連接埠，並接著會取得 hello 後端伺服器的重新導向的 tooone。</span><span class="sxs-lookup"><span data-stu-id="d9438-141">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="d9438-142">**接聽程式：** hello 接聽程式有前端連接埠的通訊協定 （Http 或 Https，這些是區分大小寫），與 hello 的 SSL 憑證名稱 （如果有設定 SSL 卸載）。</span><span class="sxs-lookup"><span data-stu-id="d9438-142">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="d9438-143">**規則：** hello 規則繫結 hello 接聽程式和 hello 後端伺服器集區，並定義哪一個後端伺服器集區 hello 流量應導向的 toowhen 配接器特定接聽程式。</span><span class="sxs-lookup"><span data-stu-id="d9438-143">**Rule:** hello rule binds hello listener and hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="d9438-144">目前，只有 hello*基本*規則支援。</span><span class="sxs-lookup"><span data-stu-id="d9438-144">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="d9438-145">hello*基本*規則是循環配置資源負載分佈。</span><span class="sxs-lookup"><span data-stu-id="d9438-145">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="d9438-146">建立組態物件或使用組態 XML 檔案，即可建構組態。</span><span class="sxs-lookup"><span data-stu-id="d9438-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="d9438-147">tooconstruct 您使用的組態 XML 檔案、 使用 hello 組態的範例如下。</span><span class="sxs-lookup"><span data-stu-id="d9438-147">tooconstruct your configuration by using a configuration XML file, use hello sample below.</span></span>

<span data-ttu-id="d9438-148">請注意 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d9438-148">Note hello following:</span></span>

* <span data-ttu-id="d9438-149">hello *FrontendIPConfigurations*元素描述相關的設定搭配 ILB 一起運作的應用程式閘道的 hello ILB 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d9438-149">hello *FrontendIPConfigurations* element describes hello ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="d9438-150">hello 前端 IP*類型*應該設定 too'Private'</span><span class="sxs-lookup"><span data-stu-id="d9438-150">hello Frontend IP *Type* should be set too'Private'</span></span>
* <span data-ttu-id="d9438-151">hello *StaticIPAddress*應該設定 toohello 預期的內部 IP 的 hello 閘道接收流量。</span><span class="sxs-lookup"><span data-stu-id="d9438-151">hello *StaticIPAddress* should be set toohello desired internal IP on which hello gateway receives traffic.</span></span> <span data-ttu-id="d9438-152">請注意該 hello *StaticIPAddress*是選擇性項目。</span><span class="sxs-lookup"><span data-stu-id="d9438-152">Note that hello *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="d9438-153">如果不是集合，會選擇可用的內部 IP，從部署的 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="d9438-153">If not set, an available internal IP from hello deployed subnet is chosen.</span></span> 
* <span data-ttu-id="d9438-154">hello 值 hello*名稱*中指定的項目*FrontendIPConfiguration*應該用於 hello HTTPListener 的*FrontendIP*元素 toorefer toohelloFrontendIPConfiguration。</span><span class="sxs-lookup"><span data-stu-id="d9438-154">hello value of hello *Name* element specified in *FrontendIPConfiguration* should be used in hello HTTPListener's *FrontendIP* element toorefer toohello FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="d9438-155">**組態 XML 範例**</span><span class="sxs-lookup"><span data-stu-id="d9438-155">**Configuration XML sample**</span></span>
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


## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="d9438-156">設定 hello 閘道組態</span><span class="sxs-lookup"><span data-stu-id="d9438-156">Set hello gateway configuration</span></span>
<span data-ttu-id="d9438-157">接下來，您將設定 hello 應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d9438-157">Next, you'll set hello application gateway.</span></span> <span data-ttu-id="d9438-158">您可以使用 hello`Set-AzureApplicationGatewayConfig`指令程式與組態物件，或設定 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d9438-158">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

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

## <a name="start-hello-gateway"></a><span data-ttu-id="d9438-159">啟動 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="d9438-159">Start hello gateway</span></span>

<span data-ttu-id="d9438-160">一旦已設定 hello 閘道，使用 hello `Start-AzureApplicationGateway` cmdlet toostart hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="d9438-160">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="d9438-161">在 hello 閘道已順利啟動後，就會開始計費，應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="d9438-161">Billing for an application gateway begins after hello gateway has been successfully started.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9438-162">hello `Start-AzureApplicationGateway` cmdlet 可能會佔用 toocomplete too15 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="d9438-162">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toocomplete.</span></span> 
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

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="d9438-163">驗證 hello 閘道器狀態</span><span class="sxs-lookup"><span data-stu-id="d9438-163">Verify hello gateway status</span></span>

<span data-ttu-id="d9438-164">使用 hello `Get-AzureApplicationGateway` cmdlet toocheck hello 狀態的閘道。</span><span class="sxs-lookup"><span data-stu-id="d9438-164">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of gateway.</span></span> <span data-ttu-id="d9438-165">如果`Start-AzureApplicationGateway`成功 hello 上一個步驟中，hello 狀態應該是*執行*，hello Vip 和 DnsName 應該具有有效的項目。</span><span class="sxs-lookup"><span data-stu-id="d9438-165">If `Start-AzureApplicationGateway` succeeded in hello previous step, hello State should be *Running*, and hello Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="d9438-166">這個範例會顯示 hello cmdlet hello 第一行，後面接著 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="d9438-166">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span> <span data-ttu-id="d9438-167">在此範例中，hello 閘道正在執行，而且已準備好 tootake 流量。</span><span class="sxs-lookup"><span data-stu-id="d9438-167">In this sample, hello gateway is running, and is ready tootake traffic.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9438-168">hello 應用程式閘道設定為在 hello tooaccept 流量設定 10.0.0.10 ILB 端點在此範例中。</span><span class="sxs-lookup"><span data-stu-id="d9438-168">hello application gateway is configured tooaccept traffic at hello configured ILB endpoint of 10.0.0.10 in this example.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d9438-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9438-169">Next steps</span></span>
<span data-ttu-id="d9438-170">如果您想進一步了解一般負載平衡選項，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d9438-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="d9438-171">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="d9438-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="d9438-172">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="d9438-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

