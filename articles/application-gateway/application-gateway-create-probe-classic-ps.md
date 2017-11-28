---
title: "自訂探查-Azure 應用程式閘道-PowerShell 傳統 aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 自訂探查應用程式閘道在 hello 傳統部署模型中使用 PowerShell"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="a61ab-103">使用 PowerShell 建立 Azure 應用程式閘道 (傳統) 的自訂探查</span><span class="sxs-lookup"><span data-stu-id="a61ab-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a61ab-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a61ab-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="a61ab-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="a61ab-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="a61ab-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="a61ab-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="a61ab-107">在本文中，您可以加入自訂探查 tooan 現有應用程式閘道使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="a61ab-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="a61ab-108">自訂探查適合應用程式的健全狀況檢查 頁面，或未提供成功的回應 hello 預設 web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a61ab-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a61ab-109">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="a61ab-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a61ab-110">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a61ab-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a61ab-111">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="a61ab-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a61ab-112">了解如何太[使用 hello 資源管理員的模型執行這些步驟](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="a61ab-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="a61ab-113">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a61ab-113">Create an application gateway</span></span>

<span data-ttu-id="a61ab-114">toocreate 應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="a61ab-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="a61ab-115">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="a61ab-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="a61ab-116">建立設定 XML 檔案或設定物件。</span><span class="sxs-lookup"><span data-stu-id="a61ab-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="a61ab-117">認可新建立的應用程式閘道資源 hello 組態 toohello。</span><span class="sxs-lookup"><span data-stu-id="a61ab-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="a61ab-118">使用自訂探查建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="a61ab-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="a61ab-119">toocreate hello 閘道，使用 hello `New-AzureApplicationGateway` cmdlet，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="a61ab-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="a61ab-120">此時無法啟動的 hello 閘道計費。</span><span class="sxs-lookup"><span data-stu-id="a61ab-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="a61ab-121">計費開始在稍後步驟中，當 hello 閘道已順利啟動。</span><span class="sxs-lookup"><span data-stu-id="a61ab-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="a61ab-122">hello 下列範例會建立應用程式閘道使用名為"testvnet1"，稱為 「 子網路-1"的子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a61ab-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="a61ab-123">hello 閘道的 toovalidate 所建立，您可以使用 hello `Get-AzureApplicationGateway` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="a61ab-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="a61ab-124">預設值的 hello *InstanceCount*為 2，最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="a61ab-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="a61ab-125">預設值的 hello *GatewaySize*都是 Medium。</span><span class="sxs-lookup"><span data-stu-id="a61ab-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="a61ab-126">您可以選擇 Small、Medium 和 Large。</span><span class="sxs-lookup"><span data-stu-id="a61ab-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="a61ab-127">*如*和*DnsName*會顯示為空白，因為 hello 閘道尚未啟動。</span><span class="sxs-lookup"><span data-stu-id="a61ab-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="a61ab-128">執行中狀態的 hello hello 閘道之後，會建立這些值。</span><span class="sxs-lookup"><span data-stu-id="a61ab-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="a61ab-129">使用 XML 設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a61ab-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="a61ab-130">在下列範例的 hello，您可以使用 XML 檔案 tooconfigure 所有應用程式閘道設定，並認可 toohello 應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="a61ab-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="a61ab-131">複製下列文字 tooNotepad hello。</span><span class="sxs-lookup"><span data-stu-id="a61ab-131">Copy hello following text tooNotepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="a61ab-132">編輯 hello hello 設定項目的 hello 括號之間的值。</span><span class="sxs-lookup"><span data-stu-id="a61ab-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="a61ab-133">儲存副檔名的.xml hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="a61ab-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="a61ab-134">hello 下列範例顯示如何 toouse 向上 hello 應用程式閘道 tooload 組態檔案 tooset 平衡公用連接埠 80 上的 HTTP 流量和使用自訂探查的兩個 IP 位址之間的 tooback 結束連接埠 80 傳送網路流量。</span><span class="sxs-lookup"><span data-stu-id="a61ab-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a61ab-135">Http 或 Https 的 hello 通訊協定項目會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="a61ab-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="a61ab-136">新的設定項目\<探查\>加入 tooconfigure 自訂探查。</span><span class="sxs-lookup"><span data-stu-id="a61ab-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="a61ab-137">hello 設定參數如下：</span><span class="sxs-lookup"><span data-stu-id="a61ab-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="a61ab-138">參數</span><span class="sxs-lookup"><span data-stu-id="a61ab-138">Parameter</span></span>|<span data-ttu-id="a61ab-139">說明</span><span class="sxs-lookup"><span data-stu-id="a61ab-139">Description</span></span>|
|---|---|
|<span data-ttu-id="a61ab-140">**名稱**</span><span class="sxs-lookup"><span data-stu-id="a61ab-140">**Name**</span></span> |<span data-ttu-id="a61ab-141">自訂探查的參考名稱。</span><span class="sxs-lookup"><span data-stu-id="a61ab-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="a61ab-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="a61ab-142">* **Protocol**</span></span> | <span data-ttu-id="a61ab-143">使用的通訊協定 (可能的值是 HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="a61ab-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="a61ab-144">**Host** 和 **Path**</span><span class="sxs-lookup"><span data-stu-id="a61ab-144">**Host** and **Path**</span></span> | <span data-ttu-id="a61ab-145">叫用由 hello 應用程式閘道 toodetermine hello 健康嗨執行個體的完整 URL 路徑。</span><span class="sxs-lookup"><span data-stu-id="a61ab-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="a61ab-146">比方說，如果您有網站 http://contoso.com/，請 hello 自訂探查可設定為"http://contoso.com/path/custompath.htm"探查檢查 toohave 成功的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="a61ab-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="a61ab-147">**間隔**</span><span class="sxs-lookup"><span data-stu-id="a61ab-147">**Interval**</span></span> | <span data-ttu-id="a61ab-148">設定 hello 探查間隔檢查，以秒為單位。</span><span class="sxs-lookup"><span data-stu-id="a61ab-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="a61ab-149">**逾時**</span><span class="sxs-lookup"><span data-stu-id="a61ab-149">**Timeout**</span></span> | <span data-ttu-id="a61ab-150">定義 HTTP 回應檢查 hello 探查逾時。</span><span class="sxs-lookup"><span data-stu-id="a61ab-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="a61ab-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="a61ab-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="a61ab-152">hello 需要 tooflag hello 後端執行個體標示為失敗的 HTTP 回應數*不良*。</span><span class="sxs-lookup"><span data-stu-id="a61ab-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="a61ab-153">hello 探查名稱會參考 hello \<BackendHttpSettings\>組態 tooassign 哪一個後端集區會使用自訂探查設定。</span><span class="sxs-lookup"><span data-stu-id="a61ab-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="a61ab-154">新增自訂探查 tooan 現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="a61ab-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="a61ab-155">變更 hello 目前組態的應用程式閘道需要三個步驟： 取得 hello 目前的 XML 組態檔、 修改 toohave 自訂探查，和 hello 應用程式閘道設定為使用 hello 新的 XML 設定。</span><span class="sxs-lookup"><span data-stu-id="a61ab-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="a61ab-156">取得 hello XML 檔案使用`Get-AzureApplicationGatewayConfig`。</span><span class="sxs-lookup"><span data-stu-id="a61ab-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="a61ab-157">此指令程式匯出 hello 組態 XML toobe 修改 tooadd 探查設定。</span><span class="sxs-lookup"><span data-stu-id="a61ab-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="a61ab-158">在文字編輯器中開啟 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="a61ab-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="a61ab-159">在 `<frontendport>` 之後新增 `<probe>` 區段。</span><span class="sxs-lookup"><span data-stu-id="a61ab-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="a61ab-160">中的 hello XML hello backendHttpSettings 區段中，加入 hello 探查名稱 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a61ab-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="a61ab-161">儲存 hello XML 檔。</span><span class="sxs-lookup"><span data-stu-id="a61ab-161">Save hello XML file.</span></span>

1. <span data-ttu-id="a61ab-162">更新 hello 應用程式與 hello 新的 XML 檔案使用的閘道設定`Set-AzureApplicationGatewayConfig`。</span><span class="sxs-lookup"><span data-stu-id="a61ab-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="a61ab-163">此 cmdlet 會更新您的應用程式閘道 hello 新組態。</span><span class="sxs-lookup"><span data-stu-id="a61ab-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="a61ab-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a61ab-164">Next steps</span></span>

<span data-ttu-id="a61ab-165">如果您想的 tooconfigure Secure Sockets Layer (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="a61ab-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="a61ab-166">如果您想 tooconfigure 內部負載平衡器的應用程式閘道 toouse，請參閱[內部負載平衡器 (ILB) 建立應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="a61ab-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

