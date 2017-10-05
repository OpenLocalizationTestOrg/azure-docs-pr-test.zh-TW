---
title: "疑難排解 Azure 應用程式閘道閘道不正確 (502) 的錯誤 | Microsoft Docs"
description: "了解如何對應用程式閘道 502 錯誤進行疑難排解"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: cbf9c552c4818b3925f449081539f1db6d61918e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="a1ff1-103">疑難排解應用程式閘道中閘道不正確的錯誤</span><span class="sxs-lookup"><span data-stu-id="a1ff1-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="a1ff1-104">了解使用應用程式閘道時如何針對收到的閘道不正確 (502) 錯誤進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-104">Learn how to troubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="a1ff1-105">概觀</span><span class="sxs-lookup"><span data-stu-id="a1ff1-105">Overview</span></span>

<span data-ttu-id="a1ff1-106">設定應用程式閘道之後，使用者可能遇到的其中一個錯誤是「伺服器錯誤︰502 - 網頁伺服器作為閘道器或 Proxy 伺服器時收到無效的回應」。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-106">After configuring an application gateway, one of the errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="a1ff1-107">此錯誤可能是由於下列主要原因所導致：</span><span class="sxs-lookup"><span data-stu-id="a1ff1-107">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="a1ff1-108">Azure 應用程式閘道的[後端集區未設定或空白](#empty-backendaddresspool)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="a1ff1-109">VM 擴展集中[沒有狀況良好的 VM 或執行個體](#unhealthy-instances-in-backendaddresspool)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-109">None of the VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="a1ff1-110">VM 擴展集的後端 VM 或執行個體都[沒有回應預設的健康情況探查](#problems-with-default-health-probe.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-110">Back-end VMs or instances of VM Scale Set are [not responding to the default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="a1ff1-111">無效或不適當的[自訂健康情況探查設定](#problems-with-custom-health-probe.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="a1ff1-112">使用者要求的[要求逾期或連線問題](#request-time-out)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="a1ff1-113">空白的 BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="a1ff1-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="a1ff1-114">原因</span><span class="sxs-lookup"><span data-stu-id="a1ff1-114">Cause</span></span>

<span data-ttu-id="a1ff1-115">如果應用程式閘道未在後端位址集區中設定 VM 或 VM 擴展集，就無法路由傳送任何客戶要求，並會擲回閘道不正確的錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-115">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ff1-116">方案</span><span class="sxs-lookup"><span data-stu-id="a1ff1-116">Solution</span></span>

<span data-ttu-id="a1ff1-117">確定後端位址集區不是空白的。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-117">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="a1ff1-118">這可透過 PowerShell、CLI 或入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="a1ff1-119">前述 Cmdlet 的輸出應包含非空白的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-119">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="a1ff1-120">下列範例會傳回兩個針對後端 VM 使用 FQDN 或 IP 位址設定的集區。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="a1ff1-121">BackendAddressPool 的佈建狀態必須是 'Succeeded'。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-121">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="a1ff1-122">BackendAddressPoolsText：</span><span class="sxs-lookup"><span data-stu-id="a1ff1-122">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="a1ff1-123">BackendAddressPool 中狀況不良的執行個體</span><span class="sxs-lookup"><span data-stu-id="a1ff1-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="a1ff1-124">原因</span><span class="sxs-lookup"><span data-stu-id="a1ff1-124">Cause</span></span>

<span data-ttu-id="a1ff1-125">如果 BackendAddressPool 的所有執行個體都狀況不良，則應用程式閘道不會包含任何要將使用者要求路由傳送到其中的後端。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-125">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="a1ff1-126">當後端執行個體的狀況良好，但尚未部署必要的應用程式時，也可能發生此情況。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-126">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ff1-127">方案</span><span class="sxs-lookup"><span data-stu-id="a1ff1-127">Solution</span></span>

<span data-ttu-id="a1ff1-128">確定執行個體的狀況良好且已正確設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-128">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="a1ff1-129">檢查後端執行個體是否能夠從同一個 VNet 中的其他 VM 回應 Ping。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-129">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="a1ff1-130">如果是使用公用端點所設定，請確定對 Web 應用程式的瀏覽器要求能夠提供服務。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-130">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="a1ff1-131">預設健全狀況探查的問題</span><span class="sxs-lookup"><span data-stu-id="a1ff1-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="a1ff1-132">原因</span><span class="sxs-lookup"><span data-stu-id="a1ff1-132">Cause</span></span>

<span data-ttu-id="a1ff1-133">502 錯誤也可以是預設健全狀態探查無法連線到後端 VM 的常用指標。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-133">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="a1ff1-134">佈建應用程式閘道執行個體時，它會使用 BackendHttpSetting 的屬性，自動將預設的健全狀況探查設定到每個 BackendAddressPool 。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="a1ff1-135">設定此探查時不需任何使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-135">No user input is required to set this probe.</span></span> <span data-ttu-id="a1ff1-136">具體而言，設定負載平衡規則時，會在 BackendHttpSetting 和 BackendAddressPool 之間建立關聯。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="a1ff1-137">預設探查是針對這其中的每一個關聯所設定，而應用程式閘道會在 BackendHttpSetting 項目中指定的連接埠上，將定期的健全狀況檢查連線初始到 BackendAddressPool 中的每一個執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="a1ff1-138">下表列出與預設健全狀況探查相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-138">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="a1ff1-139">探查屬性</span><span class="sxs-lookup"><span data-stu-id="a1ff1-139">Probe property</span></span> | <span data-ttu-id="a1ff1-140">值</span><span class="sxs-lookup"><span data-stu-id="a1ff1-140">Value</span></span> | <span data-ttu-id="a1ff1-141">說明</span><span class="sxs-lookup"><span data-stu-id="a1ff1-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a1ff1-142">探查 URL</span><span class="sxs-lookup"><span data-stu-id="a1ff1-142">Probe URL</span></span> |<span data-ttu-id="a1ff1-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="a1ff1-143">http://127.0.0.1/</span></span> |<span data-ttu-id="a1ff1-144">URL 路徑</span><span class="sxs-lookup"><span data-stu-id="a1ff1-144">URL path</span></span> |
| <span data-ttu-id="a1ff1-145">間隔</span><span class="sxs-lookup"><span data-stu-id="a1ff1-145">Interval</span></span> |<span data-ttu-id="a1ff1-146">30</span><span class="sxs-lookup"><span data-stu-id="a1ff1-146">30</span></span> |<span data-ttu-id="a1ff1-147">探查間隔 (秒)</span><span class="sxs-lookup"><span data-stu-id="a1ff1-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="a1ff1-148">逾時</span><span class="sxs-lookup"><span data-stu-id="a1ff1-148">Time-out</span></span> |<span data-ttu-id="a1ff1-149">30</span><span class="sxs-lookup"><span data-stu-id="a1ff1-149">30</span></span> |<span data-ttu-id="a1ff1-150">探查逾時 (秒)</span><span class="sxs-lookup"><span data-stu-id="a1ff1-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="a1ff1-151">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="a1ff1-151">Unhealthy threshold</span></span> |<span data-ttu-id="a1ff1-152">3</span><span class="sxs-lookup"><span data-stu-id="a1ff1-152">3</span></span> |<span data-ttu-id="a1ff1-153">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-153">Probe retry count.</span></span> <span data-ttu-id="a1ff1-154">連續探查失敗計數到達狀況不良臨界值後，就會將後端伺服器標示為故障。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-154">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="a1ff1-155">方案</span><span class="sxs-lookup"><span data-stu-id="a1ff1-155">Solution</span></span>

* <span data-ttu-id="a1ff1-156">確定預設網站已設定且正於 127.0.0.1 上進行接聽。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="a1ff1-157">如果 BackendHttpSetting 指定了 80 以外的連接埠，則應將預設網站設定為在該連接埠上進行接聽。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-157">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="a1ff1-158">對 http://127.0.0.1:port 的呼叫應該會傳回 HTTP 結果碼 200。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-158">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="a1ff1-159">這應該會在 30 秒逾時期間內傳回。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-159">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="a1ff1-160">確定設定的連接埠已開啟，而且沒有任何防火牆或 Azure 網路安全性群組會在所設定的連接埠上封鎖連入或連出流量。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="a1ff1-161">如果Azure 傳統 VM 或雲端服務會與 FQDN 或公用 IP 搭配使用，請確認對應的 [端點](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) 已開啟。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="a1ff1-162">如果 VM 是透過 Azure Resource Manager 所設定且位於應用程式閘道部署所在的 VNet 外部，就必須將 [網路安全性群組](../virtual-network/virtual-networks-nsg.md) 設定為允許在所需的連接埠上進行存取。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-162">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="a1ff1-163">自訂健全狀況探查的問題</span><span class="sxs-lookup"><span data-stu-id="a1ff1-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="a1ff1-164">原因</span><span class="sxs-lookup"><span data-stu-id="a1ff1-164">Cause</span></span>

<span data-ttu-id="a1ff1-165">自訂的健全狀況探查能夠對於預設探查行為提供更多彈性。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-165">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="a1ff1-166">使用自訂探查時，使用者可以設定探查間隔、要測試的 URL 和路徑，以及在將後端集區執行個體標示為狀況不良前，可接受的失敗回應次數。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-166">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="a1ff1-167">已新增下列其他屬性。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-167">The following additional properties are added.</span></span>

| <span data-ttu-id="a1ff1-168">探查屬性</span><span class="sxs-lookup"><span data-stu-id="a1ff1-168">Probe property</span></span> | <span data-ttu-id="a1ff1-169">說明</span><span class="sxs-lookup"><span data-stu-id="a1ff1-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a1ff1-170">Name</span><span class="sxs-lookup"><span data-stu-id="a1ff1-170">Name</span></span> |<span data-ttu-id="a1ff1-171">探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-171">Name of the probe.</span></span> <span data-ttu-id="a1ff1-172">此名稱用來在後端 HTTP 設定中指出探查。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-172">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="a1ff1-173">通訊協定</span><span class="sxs-lookup"><span data-stu-id="a1ff1-173">Protocol</span></span> |<span data-ttu-id="a1ff1-174">用來傳送探查的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-174">Protocol used to send the probe.</span></span> <span data-ttu-id="a1ff1-175">探查會使用後端 HTTP 設定中定義的通訊協定</span><span class="sxs-lookup"><span data-stu-id="a1ff1-175">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="a1ff1-176">Host</span><span class="sxs-lookup"><span data-stu-id="a1ff1-176">Host</span></span> |<span data-ttu-id="a1ff1-177">用來傳送探查的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-177">Host name to send the probe.</span></span> <span data-ttu-id="a1ff1-178">只有當應用程式閘道上設定多站台時適用。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="a1ff1-179">這與 VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="a1ff1-180">Path</span><span class="sxs-lookup"><span data-stu-id="a1ff1-180">Path</span></span> |<span data-ttu-id="a1ff1-181">探查的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-181">Relative path of the probe.</span></span> <span data-ttu-id="a1ff1-182">有效路徑的開頭為 '/'。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-182">The valid path starts from '/'.</span></span> <span data-ttu-id="a1ff1-183">探查會傳送到 \<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\></span><span class="sxs-lookup"><span data-stu-id="a1ff1-183">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="a1ff1-184">間隔</span><span class="sxs-lookup"><span data-stu-id="a1ff1-184">Interval</span></span> |<span data-ttu-id="a1ff1-185">探查間隔 (秒)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-185">Probe interval in seconds.</span></span> <span data-ttu-id="a1ff1-186">這是兩個連續探查之間的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-186">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="a1ff1-187">逾時</span><span class="sxs-lookup"><span data-stu-id="a1ff1-187">Time-out</span></span> |<span data-ttu-id="a1ff1-188">探查逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-188">Probe time-out in seconds.</span></span> <span data-ttu-id="a1ff1-189">如果在這個逾時期間內未收到有效的回應，則會將探查標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-189">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="a1ff1-190">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="a1ff1-190">Unhealthy threshold</span></span> |<span data-ttu-id="a1ff1-191">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-191">Probe retry count.</span></span> <span data-ttu-id="a1ff1-192">連續探查失敗計數到達狀況不良臨界值後，就會將後端伺服器標示為故障。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-192">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="a1ff1-193">方案</span><span class="sxs-lookup"><span data-stu-id="a1ff1-193">Solution</span></span>

<span data-ttu-id="a1ff1-194">確認已按照上述資料表正確設定 [自訂健全狀態探查]。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-194">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="a1ff1-195">除了上述的疑難排解步驟，也請確定下列各項：</span><span class="sxs-lookup"><span data-stu-id="a1ff1-195">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="a1ff1-196">確定已根據 [指南](application-gateway-create-probe-ps.md)正確指定探查。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-196">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="a1ff1-197">如果已將應用程式閘道設定為單一站台，根據預設，除非已在自訂探查中加以設定，否則應將主機名稱指定為 '127.0.0.1'。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-197">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="a1ff1-198">確定對 http://\<主機\>:\<連接埠\>\<路徑\> 的呼叫會傳回 HTTP 結果碼 200。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-198">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="a1ff1-199">確定 Interval、Time-out 和 UnhealtyThreshold 皆在可接受的範圍內。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-199">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="a1ff1-200">若使用 HTTPS 探查，請在後端伺服器本身設定後援憑證，以確定後端伺服器不會要求您提供 SNI。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-200">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="a1ff1-201">確定 Interval、Time-out 和 UnhealtyThreshold 皆在可接受的範圍內。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="a1ff1-202">要求逾時</span><span class="sxs-lookup"><span data-stu-id="a1ff1-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="a1ff1-203">原因</span><span class="sxs-lookup"><span data-stu-id="a1ff1-203">Cause</span></span>

<span data-ttu-id="a1ff1-204">收到使用者要求時，應用程式閘道會將設定的規則套用到該要求，並將其路由傳送到後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-204">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="a1ff1-205">其會等候一段可設定的時間間隔以接收來自後端應用程式的回應。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-205">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="a1ff1-206">根據預設，這個間隔為 **30 秒**。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="a1ff1-207">如果應用程式閘道沒有在此時間間隔內收到來自後端應用程式的回應，使用者要求就會看到 502 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="a1ff1-208">方案</span><span class="sxs-lookup"><span data-stu-id="a1ff1-208">Solution</span></span>

<span data-ttu-id="a1ff1-209">應用程式閘道允許使用者透過 BackendHttpSetting 設定此組態，接著可將之套用到其他集區。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-209">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="a1ff1-210">不同的後端集區可以有不同的 BackendHttpSetting，因此可設定不同的要求逾時。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="a1ff1-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1ff1-211">Next steps</span></span>

<span data-ttu-id="a1ff1-212">如果上述步驟無法解決問題，請開啟 [支援票證](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="a1ff1-212">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

