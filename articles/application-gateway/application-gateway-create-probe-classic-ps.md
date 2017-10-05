---
title: "建立自訂探查 - Azure 應用程式閘道 - PowerShell 傳統 | Microsoft Docs"
description: "了解如何在傳統部署模型中使用 PowerShell 建立應用程式閘道的自訂探查"
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
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="4c1f4-103">使用 PowerShell 建立 Azure 應用程式閘道 (傳統) 的自訂探查</span><span class="sxs-lookup"><span data-stu-id="4c1f4-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c1f4-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4c1f4-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="4c1f4-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c1f4-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="4c1f4-106">Azure 傳統 PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c1f4-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="4c1f4-107">在本文中，您會使用 PowerShell 將自訂探查新增到現有的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="4c1f4-108">對於具有特定健康狀態檢查頁面的應用程式，或是在預設 Web 應用程式上不提供成功回應的應用程式，自訂探查非常實用。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c1f4-109">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c1f4-110">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4c1f4-111">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4c1f4-112">了解如何[使用 Resource Manager 模型執行這些步驟](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="4c1f4-113">建立應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4c1f4-113">Create an application gateway</span></span>

<span data-ttu-id="4c1f4-114">建立應用程式閘道：</span><span class="sxs-lookup"><span data-stu-id="4c1f4-114">To create an application gateway:</span></span>

1. <span data-ttu-id="4c1f4-115">建立應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="4c1f4-116">建立設定 XML 檔案或設定物件。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="4c1f4-117">認可新建立應用程式閘道資源的設定。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="4c1f4-118">使用自訂探查建立應用程式閘道資源</span><span class="sxs-lookup"><span data-stu-id="4c1f4-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="4c1f4-119">若要建立閘道，請使用 `New-AzureApplicationGateway` Cmdlet，並以您自己的值來取代這些值。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="4c1f4-120">此時還不會開始對閘道計費。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="4c1f4-121">會在稍後的步驟中於成功啟動閘道之後開始計費。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="4c1f4-122">下列範例會使用名為 "testvnet1" 的虛擬網路和名為 "subnet-1" 的子網路來建立應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="4c1f4-123">若要驗證已建立閘道，您可以使用 `Get-AzureApplicationGateway` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="4c1f4-124">*InstanceCount* 的預設值是 2，且最大值是 10。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="4c1f4-125">GatewaySize  的預設值是 Medium。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="4c1f4-126">您可以選擇 Small、Medium 和 Large。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="4c1f4-127">因為尚未啟動閘道，所以 VirtualIPs 和 DnsName 會顯示為空白。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="4c1f4-128">閘道處於執行中狀態之後，就會建立這些值。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="4c1f4-129">使用 XML 設定應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4c1f4-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="4c1f4-130">在下列範例中，您將使用 XML 檔案來設定所有應用程式閘道設定，並將它們認可到應用程式閘道資源。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="4c1f4-131">將下列文字複製到 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="4c1f4-132">編輯設定項目括號間的值。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="4c1f4-133">以 .xml 副檔名儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="4c1f4-134">下列範例示範如何使用設定檔來設定應用程式閘道，使公用連接埠 80 上的 HTTP 流量達到負載平衡，並使用自訂探查將網路流量傳送到兩個 IP 位址之間的後端連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c1f4-135">通訊協定項目 Http 或 Https 會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="4c1f4-136">已新增用來設定自訂探查的新組態項目 \<Probe\>。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="4c1f4-137">組態參數如下：</span><span class="sxs-lookup"><span data-stu-id="4c1f4-137">The configuration parameters are:</span></span>

|<span data-ttu-id="4c1f4-138">參數</span><span class="sxs-lookup"><span data-stu-id="4c1f4-138">Parameter</span></span>|<span data-ttu-id="4c1f4-139">說明</span><span class="sxs-lookup"><span data-stu-id="4c1f4-139">Description</span></span>|
|---|---|
|<span data-ttu-id="4c1f4-140">**名稱**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-140">**Name**</span></span> |<span data-ttu-id="4c1f4-141">自訂探查的參考名稱。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="4c1f4-142">* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-142">* **Protocol**</span></span> | <span data-ttu-id="4c1f4-143">使用的通訊協定 (可能的值是 HTTP 或 HTTPS)。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="4c1f4-144">**Host** 和 **Path**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-144">**Host** and **Path**</span></span> | <span data-ttu-id="4c1f4-145">應用程式閘道所叫用的完整 URL 路徑，可藉以判斷執行個體健康狀態。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="4c1f4-146">例如，若您擁有網站 http://contoso.com/，則可以為 "http://contoso.com/path/custompath.htm" 設定自訂探查，以便讓探查檢查有成功的 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="4c1f4-147">**間隔**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-147">**Interval**</span></span> | <span data-ttu-id="4c1f4-148">以秒為單位設定探查間隔檢查。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="4c1f4-149">**逾時**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-149">**Timeout**</span></span> | <span data-ttu-id="4c1f4-150">定義 HTTP 回應檢查的探查逾時。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="4c1f4-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="4c1f4-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="4c1f4-152">要將後端執行個體標記為「狀況不良」所需的失敗 HTTP 回應次數。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="4c1f4-153">\<BackendHttpSettings\> 組態中會參考探查名稱，以指派哪個後端集區會使用自訂探查設定。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="4c1f4-154">將自訂探查新增至現有應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="4c1f4-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="4c1f4-155">變更目前的應用程式閘道組態需要三個步驟：取得目前的 XML 組態檔、進行修改使其具有自訂探查，並以新的 XML 設定來設定應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="4c1f4-156">使用 `Get-AzureApplicationGatewayConfig` 取得 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="4c1f4-157">此 cmdlet 會匯出要修改的組態 XML 以新增探查設定。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="4c1f4-158">在文字編輯器中開啟 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="4c1f4-159">在 `<frontendport>` 之後新增 `<probe>` 區段。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="4c1f4-160">在 XML 的 backendHttpSettings 區段中，如下列範例所示，新增探查名稱：</span><span class="sxs-lookup"><span data-stu-id="4c1f4-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="4c1f4-161">儲存 XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-161">Save the XML file.</span></span>

1. <span data-ttu-id="4c1f4-162">使用 `Set-AzureApplicationGatewayConfig` 以新的 XML 檔案更新應用程式閘道組態。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="4c1f4-163">此 cmdlet 會以新組態更新您的應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="4c1f4-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c1f4-164">Next steps</span></span>

<span data-ttu-id="4c1f4-165">如果您想要設定「安全通訊端層」(SSL) 卸載，請參閱 [設定適用於 SSL 卸載的應用程式閘道](application-gateway-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="4c1f4-166">如果您想要設定要與內部負載平衡器搭配使用的應用程式閘道，請參閱 [建立具有內部負載平衡器 (ILB) 的應用程式閘道](application-gateway-ilb.md)。</span><span class="sxs-lookup"><span data-stu-id="4c1f4-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

