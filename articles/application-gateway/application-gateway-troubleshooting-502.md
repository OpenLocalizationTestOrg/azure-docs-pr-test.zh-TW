---
title: "aaaTroubleshoot Azure 應用程式閘道不正確的閘道 (502) 錯誤 |Microsoft 文件"
description: "深入了解如何 tootroubleshoot 應用程式閘道 502 錯誤"
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
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="670b9-103">疑難排解應用程式閘道中閘道不正確的錯誤</span><span class="sxs-lookup"><span data-stu-id="670b9-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

<span data-ttu-id="670b9-104">了解 tootroubleshoot 不正確的閘道 (502) 錯誤收到時使用應用程式閘道的方式。</span><span class="sxs-lookup"><span data-stu-id="670b9-104">Learn how tootroubleshoot bad gateway (502) errors received when using application gateway.</span></span>

## <a name="overview"></a><span data-ttu-id="670b9-105">概觀</span><span class="sxs-lookup"><span data-stu-id="670b9-105">Overview</span></span>

<span data-ttu-id="670b9-106">設定應用程式閘道之後, 使用者可能會遇到的 hello 錯誤的其中一個是 「 伺服器錯誤： 502-網頁伺服器收到無效的回應時做為閘道或 proxy 伺服器 」。</span><span class="sxs-lookup"><span data-stu-id="670b9-106">After configuring an application gateway, one of hello errors that users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="670b9-107">由於 toohello 下列可能會發生此錯誤的原因：</span><span class="sxs-lookup"><span data-stu-id="670b9-107">This error may happen due toohello following main reasons:</span></span>

* <span data-ttu-id="670b9-108">Azure 應用程式閘道的[後端集區未設定或空白](#empty-backendaddresspool)。</span><span class="sxs-lookup"><span data-stu-id="670b9-108">Azure Application Gateway's [back-end pool is not configured or empty](#empty-backendaddresspool).</span></span>
* <span data-ttu-id="670b9-109">無 hello Vm 或中的執行個體的[虛擬機器擴展集均狀況良好](#unhealthy-instances-in-backendaddresspool)。</span><span class="sxs-lookup"><span data-stu-id="670b9-109">None of hello VMs or instances in [VM Scale Set are healthy](#unhealthy-instances-in-backendaddresspool).</span></span>
* <span data-ttu-id="670b9-110">後端 Vm 或執行個體的虛擬機器擴展集[toohello 沒有回應的預設健全狀況探查](#problems-with-default-health-probe.md)。</span><span class="sxs-lookup"><span data-stu-id="670b9-110">Back-end VMs or instances of VM Scale Set are [not responding toohello default health probe](#problems-with-default-health-probe.md).</span></span>
* <span data-ttu-id="670b9-111">無效或不適當的[自訂健康情況探查設定](#problems-with-custom-health-probe.md)。</span><span class="sxs-lookup"><span data-stu-id="670b9-111">Invalid or improper [configuration of custom health probes](#problems-with-custom-health-probe.md).</span></span>
* <span data-ttu-id="670b9-112">使用者要求的[要求逾期或連線問題](#request-time-out)。</span><span class="sxs-lookup"><span data-stu-id="670b9-112">[Request time out or connectivity issues](#request-time-out) with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="670b9-113">空白的 BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="670b9-113">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="670b9-114">原因</span><span class="sxs-lookup"><span data-stu-id="670b9-114">Cause</span></span>

<span data-ttu-id="670b9-115">如果 hello 應用程式閘道有沒有 Vm 或虛擬機器擴展集設定 hello 後端位址集區中，它無法路由傳送任何客戶要求，並會擲回不正確的閘道錯誤。</span><span class="sxs-lookup"><span data-stu-id="670b9-115">If hello Application Gateway has no VMs or VM Scale Set configured in hello back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="670b9-116">方案</span><span class="sxs-lookup"><span data-stu-id="670b9-116">Solution</span></span>

<span data-ttu-id="670b9-117">請確定 hello 後端位址集區不是空的。</span><span class="sxs-lookup"><span data-stu-id="670b9-117">Ensure that hello back-end address pool is not empty.</span></span> <span data-ttu-id="670b9-118">這可透過 PowerShell、CLI 或入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="670b9-118">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="670b9-119">hello hello 上述 cmdlet 的輸出應該包含非空白的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="670b9-119">hello output from hello preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="670b9-120">下列範例會傳回兩個針對後端 VM 使用 FQDN 或 IP 位址設定的集區。</span><span class="sxs-lookup"><span data-stu-id="670b9-120">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="670b9-121">hello 的 hello BackendAddressPool 佈建狀態必須是 「 已成功 」。</span><span class="sxs-lookup"><span data-stu-id="670b9-121">hello provisioning state of hello BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="670b9-122">BackendAddressPoolsText：</span><span class="sxs-lookup"><span data-stu-id="670b9-122">BackendAddressPoolsText:</span></span>

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

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="670b9-123">BackendAddressPool 中狀況不良的執行個體</span><span class="sxs-lookup"><span data-stu-id="670b9-123">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="670b9-124">原因</span><span class="sxs-lookup"><span data-stu-id="670b9-124">Cause</span></span>

<span data-ttu-id="670b9-125">如果所有 BackendAddressPool hello 執行個體都均狀況不良，應用程式閘道將不會包含任何後端 tooroute 使用者的要求。</span><span class="sxs-lookup"><span data-stu-id="670b9-125">If all hello instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end tooroute user request to.</span></span> <span data-ttu-id="670b9-126">後端執行個體的狀況良好，但沒有部署的 hello 需要應用程式時，這也可能是 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="670b9-126">This could also be hello case when back-end instances are healthy but do not have hello required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="670b9-127">方案</span><span class="sxs-lookup"><span data-stu-id="670b9-127">Solution</span></span>

<span data-ttu-id="670b9-128">請確認 hello 執行個體的狀況良好，然後 hello 應用程式已正確設定。</span><span class="sxs-lookup"><span data-stu-id="670b9-128">Ensure that hello instances are healthy and hello application is properly configured.</span></span> <span data-ttu-id="670b9-129">核取 hello 後端執行個體是否已從中的其他 VM 可以 toorespond tooa ping hello 相同的 VNet。</span><span class="sxs-lookup"><span data-stu-id="670b9-129">Check if hello back-end instances are able toorespond tooa ping from another VM in hello same VNet.</span></span> <span data-ttu-id="670b9-130">如果設定為公用的結束點，請確定瀏覽器要求 toohello web 應用程式能否提供服務。</span><span class="sxs-lookup"><span data-stu-id="670b9-130">If configured with a public end point, ensure that a browser request toohello web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="670b9-131">預設健全狀況探查的問題</span><span class="sxs-lookup"><span data-stu-id="670b9-131">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="670b9-132">原因</span><span class="sxs-lookup"><span data-stu-id="670b9-132">Cause</span></span>

<span data-ttu-id="670b9-133">502 錯誤也可能是經常 hello 預設健全狀況探查的指標是無法 tooreach 後端 Vm。</span><span class="sxs-lookup"><span data-stu-id="670b9-133">502 errors can also be frequent indicators that hello default health probe is not able tooreach back-end VMs.</span></span> <span data-ttu-id="670b9-134">當已佈建應用程式閘道執行個體時，它會自動設定預設健全狀況探查 tooeach BackendAddressPool 使用 hello BackendHttpSetting 的屬性。</span><span class="sxs-lookup"><span data-stu-id="670b9-134">When an Application Gateway instance is provisioned, it automatically configures a default health probe tooeach BackendAddressPool using properties of hello BackendHttpSetting.</span></span> <span data-ttu-id="670b9-135">沒有使用者輸入所需的 tooset 此探查。</span><span class="sxs-lookup"><span data-stu-id="670b9-135">No user input is required tooset this probe.</span></span> <span data-ttu-id="670b9-136">具體而言，設定負載平衡規則時，會在 BackendHttpSetting 和 BackendAddressPool 之間建立關聯。</span><span class="sxs-lookup"><span data-stu-id="670b9-136">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="670b9-137">預設探查已針對每個這些關聯並定期的健全狀況檢查連接 tooeach 中的執行個體 hello BackendAddressPool hello hello BackendHttpSetting 元素中指定的連接埠的應用程式閘道啟動。</span><span class="sxs-lookup"><span data-stu-id="670b9-137">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection tooeach instance in hello BackendAddressPool at hello port specified in hello BackendHttpSetting element.</span></span> <span data-ttu-id="670b9-138">下表列出 hello hello 預設健全狀況探查相關聯的值。</span><span class="sxs-lookup"><span data-stu-id="670b9-138">Following table lists hello values associated with hello default health probe.</span></span>

| <span data-ttu-id="670b9-139">探查屬性</span><span class="sxs-lookup"><span data-stu-id="670b9-139">Probe property</span></span> | <span data-ttu-id="670b9-140">值</span><span class="sxs-lookup"><span data-stu-id="670b9-140">Value</span></span> | <span data-ttu-id="670b9-141">說明</span><span class="sxs-lookup"><span data-stu-id="670b9-141">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="670b9-142">探查 URL</span><span class="sxs-lookup"><span data-stu-id="670b9-142">Probe URL</span></span> |<span data-ttu-id="670b9-143">http://127.0.0.1/</span><span class="sxs-lookup"><span data-stu-id="670b9-143">http://127.0.0.1/</span></span> |<span data-ttu-id="670b9-144">URL 路徑</span><span class="sxs-lookup"><span data-stu-id="670b9-144">URL path</span></span> |
| <span data-ttu-id="670b9-145">間隔</span><span class="sxs-lookup"><span data-stu-id="670b9-145">Interval</span></span> |<span data-ttu-id="670b9-146">30</span><span class="sxs-lookup"><span data-stu-id="670b9-146">30</span></span> |<span data-ttu-id="670b9-147">探查間隔 (秒)</span><span class="sxs-lookup"><span data-stu-id="670b9-147">Probe interval in seconds</span></span> |
| <span data-ttu-id="670b9-148">逾時</span><span class="sxs-lookup"><span data-stu-id="670b9-148">Time-out</span></span> |<span data-ttu-id="670b9-149">30</span><span class="sxs-lookup"><span data-stu-id="670b9-149">30</span></span> |<span data-ttu-id="670b9-150">探查逾時 (秒)</span><span class="sxs-lookup"><span data-stu-id="670b9-150">Probe time-out in seconds</span></span> |
| <span data-ttu-id="670b9-151">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="670b9-151">Unhealthy threshold</span></span> |<span data-ttu-id="670b9-152">3</span><span class="sxs-lookup"><span data-stu-id="670b9-152">3</span></span> |<span data-ttu-id="670b9-153">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="670b9-153">Probe retry count.</span></span> <span data-ttu-id="670b9-154">hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。</span><span class="sxs-lookup"><span data-stu-id="670b9-154">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="670b9-155">方案</span><span class="sxs-lookup"><span data-stu-id="670b9-155">Solution</span></span>

* <span data-ttu-id="670b9-156">確定預設網站已設定且正於 127.0.0.1 上進行接聽。</span><span class="sxs-lookup"><span data-stu-id="670b9-156">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="670b9-157">如果 BackendHttpSetting 指定 80 以外的通訊埠，hello 預設網站應該設定的 toolisten 在該連接埠。</span><span class="sxs-lookup"><span data-stu-id="670b9-157">If BackendHttpSetting specifies a port other than 80, hello default site should be configured toolisten at that port.</span></span>
* <span data-ttu-id="670b9-158">hello 呼叫 toohttp://127.0.0.1:port 應該會傳回 HTTP 結果碼為 200。</span><span class="sxs-lookup"><span data-stu-id="670b9-158">hello call toohttp://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="670b9-159">這應該會傳回 hello 30 秒逾時期間內。</span><span class="sxs-lookup"><span data-stu-id="670b9-159">This should be returned within hello 30 sec time-out period.</span></span>
* <span data-ttu-id="670b9-160">確定設定的連接埠已開啟，並確認沒有任何防火牆規則或 Azure 網路安全性群組，會封鎖設定的 hello 連接埠上的傳入或傳出流量。</span><span class="sxs-lookup"><span data-stu-id="670b9-160">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on hello port configured.</span></span>
* <span data-ttu-id="670b9-161">如果 FQDN 或公用 IP 與使用 Azure 傳統 Vm 或雲端服務，請確定該 hello 對應[端點](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json)開啟。</span><span class="sxs-lookup"><span data-stu-id="670b9-161">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that hello corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="670b9-162">如果 hello VM 設定透過 Azure Resource Manager，而且超出 hello 應用程式閘道部署所在的 VNet[網路安全性群組](../virtual-network/virtual-networks-nsg.md)必須設定 hello tooallow 存取所需的連接埠。</span><span class="sxs-lookup"><span data-stu-id="670b9-162">If hello VM is configured via Azure Resource Manager and is outside hello VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured tooallow access on hello desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="670b9-163">自訂健全狀況探查的問題</span><span class="sxs-lookup"><span data-stu-id="670b9-163">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="670b9-164">原因</span><span class="sxs-lookup"><span data-stu-id="670b9-164">Cause</span></span>

<span data-ttu-id="670b9-165">自訂的健全狀況探查允許更大的彈性 toohello 預設探查行為。</span><span class="sxs-lookup"><span data-stu-id="670b9-165">Custom health probes allow additional flexibility toohello default probing behavior.</span></span> <span data-ttu-id="670b9-166">當使用自訂探查時，使用者可以設定 hello 探查間隔、 hello URL 路徑 tootest，以及多少失敗的回應 tooaccept 再將標示為狀況不良的 hello 後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="670b9-166">When using custom probes, users can configure hello probe interval, hello URL, and path tootest, and how many failed responses tooaccept before marking hello back-end pool instance as unhealthy.</span></span> <span data-ttu-id="670b9-167">會新增下列其他屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="670b9-167">hello following additional properties are added.</span></span>

| <span data-ttu-id="670b9-168">探查屬性</span><span class="sxs-lookup"><span data-stu-id="670b9-168">Probe property</span></span> | <span data-ttu-id="670b9-169">說明</span><span class="sxs-lookup"><span data-stu-id="670b9-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="670b9-170">名稱</span><span class="sxs-lookup"><span data-stu-id="670b9-170">Name</span></span> |<span data-ttu-id="670b9-171">Hello 探查的名稱。</span><span class="sxs-lookup"><span data-stu-id="670b9-171">Name of hello probe.</span></span> <span data-ttu-id="670b9-172">這個名稱是使用的 toorefer toohello 探查後端 HTTP 設定中。</span><span class="sxs-lookup"><span data-stu-id="670b9-172">This name is used toorefer toohello probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="670b9-173">通訊協定</span><span class="sxs-lookup"><span data-stu-id="670b9-173">Protocol</span></span> |<span data-ttu-id="670b9-174">使用 toosend hello 探查通訊協定。</span><span class="sxs-lookup"><span data-stu-id="670b9-174">Protocol used toosend hello probe.</span></span> <span data-ttu-id="670b9-175">hello 探查使用 hello hello 後端 HTTP 設定中所定義的通訊協定</span><span class="sxs-lookup"><span data-stu-id="670b9-175">hello probe uses hello protocol defined in hello back-end HTTP settings</span></span> |
| <span data-ttu-id="670b9-176">Host</span><span class="sxs-lookup"><span data-stu-id="670b9-176">Host</span></span> |<span data-ttu-id="670b9-177">主機名稱 toosend hello 探查。</span><span class="sxs-lookup"><span data-stu-id="670b9-177">Host name toosend hello probe.</span></span> <span data-ttu-id="670b9-178">只有當應用程式閘道上設定多站台時適用。</span><span class="sxs-lookup"><span data-stu-id="670b9-178">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="670b9-179">這與 VM 主機名稱不同。</span><span class="sxs-lookup"><span data-stu-id="670b9-179">This is different from VM host name.</span></span> |
| <span data-ttu-id="670b9-180">Path</span><span class="sxs-lookup"><span data-stu-id="670b9-180">Path</span></span> |<span data-ttu-id="670b9-181">Hello 探查相對路徑。</span><span class="sxs-lookup"><span data-stu-id="670b9-181">Relative path of hello probe.</span></span> <span data-ttu-id="670b9-182">hello 有效路徑的開頭 '/'。</span><span class="sxs-lookup"><span data-stu-id="670b9-182">hello valid path starts from '/'.</span></span> <span data-ttu-id="670b9-183">太傳送嗨探查\<通訊協定\>://\<主機\>:\<連接埠\>\<路徑\></span><span class="sxs-lookup"><span data-stu-id="670b9-183">hello probe is sent too\<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="670b9-184">間隔</span><span class="sxs-lookup"><span data-stu-id="670b9-184">Interval</span></span> |<span data-ttu-id="670b9-185">探查間隔 (秒)。</span><span class="sxs-lookup"><span data-stu-id="670b9-185">Probe interval in seconds.</span></span> <span data-ttu-id="670b9-186">這是兩個連續探查 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="670b9-186">This is hello time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="670b9-187">逾時</span><span class="sxs-lookup"><span data-stu-id="670b9-187">Time-out</span></span> |<span data-ttu-id="670b9-188">探查逾時 (秒)。</span><span class="sxs-lookup"><span data-stu-id="670b9-188">Probe time-out in seconds.</span></span> <span data-ttu-id="670b9-189">如果這個逾時期限內未收到有效的回應，hello 探查被標示為失敗。</span><span class="sxs-lookup"><span data-stu-id="670b9-189">If a valid response is not received within this time-out period, hello probe is marked as failed.</span></span> |
| <span data-ttu-id="670b9-190">狀況不良臨界值</span><span class="sxs-lookup"><span data-stu-id="670b9-190">Unhealthy threshold</span></span> |<span data-ttu-id="670b9-191">探查重試計數。</span><span class="sxs-lookup"><span data-stu-id="670b9-191">Probe retry count.</span></span> <span data-ttu-id="670b9-192">hello 連續探查失敗計數達到 hello 狀況不良閾值後，hello 後端伺服器標記為。</span><span class="sxs-lookup"><span data-stu-id="670b9-192">hello back-end server is marked down after hello consecutive probe failure count reaches hello unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="670b9-193">方案</span><span class="sxs-lookup"><span data-stu-id="670b9-193">Solution</span></span>

<span data-ttu-id="670b9-194">驗證自訂健全狀況探查已正確設定為上述資料表中的 hello 該 hello。</span><span class="sxs-lookup"><span data-stu-id="670b9-194">Validate that hello Custom Health Probe is configured correctly as hello preceding table.</span></span> <span data-ttu-id="670b9-195">除了上述 toohello 疑難排解步驟，也請確定 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="670b9-195">In addition toohello preceding troubleshooting steps, also ensure hello following:</span></span>

* <span data-ttu-id="670b9-196">請根據 hello 指定正確的 hello 探查[指南](application-gateway-create-probe-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="670b9-196">Ensure that hello probe is correctly specified as per hello [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="670b9-197">如果應用程式閘道設定為單一站台，依預設 hello 主機名稱應指定為 '127.0.0.1'，除非否則在自訂探查設定。</span><span class="sxs-lookup"><span data-stu-id="670b9-197">If Application Gateway is configured for a single site, by default hello Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="670b9-198">請確定呼叫 toohttp: / /\<主機\>:\<連接埠\>\<路徑\>會傳回 HTTP 結果碼為 200。</span><span class="sxs-lookup"><span data-stu-id="670b9-198">Ensure that a call toohttp://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="670b9-199">請確認間隔、 逾時和 UnhealtyThreshold hello 可接受範圍內。</span><span class="sxs-lookup"><span data-stu-id="670b9-199">Ensure that Interval, Time-out and UnhealtyThreshold are within hello acceptable ranges.</span></span>
* <span data-ttu-id="670b9-200">如果使用 HTTPS 探查，請確定該 hello 後端伺服器不需要 SNI hello 後端伺服器本身上設定 fallback 憑證。</span><span class="sxs-lookup"><span data-stu-id="670b9-200">If using an HTTPS probe, make sure that hello backend server doesn't require SNI by configuring a fallback certificate on hello backend server itself.</span></span> 
* <span data-ttu-id="670b9-201">請確認間隔、 逾時與 UnhealtyThreshold hello 可接受範圍內。</span><span class="sxs-lookup"><span data-stu-id="670b9-201">Ensure that Interval, Time-out, and UnhealtyThreshold are within hello acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="670b9-202">要求逾時</span><span class="sxs-lookup"><span data-stu-id="670b9-202">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="670b9-203">原因</span><span class="sxs-lookup"><span data-stu-id="670b9-203">Cause</span></span>

<span data-ttu-id="670b9-204">當收到使用者的要求時，應用程式閘道套用 hello 設定規則 toohello 要求，並將其路由 tooa 後端集區執行個體。</span><span class="sxs-lookup"><span data-stu-id="670b9-204">When a user request is received, Application Gateway applies hello configured rules toohello request and routes it tooa back-end pool instance.</span></span> <span data-ttu-id="670b9-205">可設定的間隔時間 hello 後端執行個體回應的等候。</span><span class="sxs-lookup"><span data-stu-id="670b9-205">It waits for a configurable interval of time for a response from hello back-end instance.</span></span> <span data-ttu-id="670b9-206">根據預設，這個間隔為 **30 秒**。</span><span class="sxs-lookup"><span data-stu-id="670b9-206">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="670b9-207">如果應用程式閘道沒有在此時間間隔內收到來自後端應用程式的回應，使用者要求就會看到 502 錯誤。</span><span class="sxs-lookup"><span data-stu-id="670b9-207">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="670b9-208">方案</span><span class="sxs-lookup"><span data-stu-id="670b9-208">Solution</span></span>

<span data-ttu-id="670b9-209">應用程式閘道可讓使用者 tooconfigure BackendHttpSetting，這可以是則會套用 toodifferent 集區透過此設定。</span><span class="sxs-lookup"><span data-stu-id="670b9-209">Application Gateway allows users tooconfigure this setting via BackendHttpSetting, which can be then applied toodifferent pools.</span></span> <span data-ttu-id="670b9-210">不同的後端集區可以有不同的 BackendHttpSetting，因此可設定不同的要求逾時。</span><span class="sxs-lookup"><span data-stu-id="670b9-210">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="670b9-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="670b9-211">Next steps</span></span>

<span data-ttu-id="670b9-212">如果 hello 上述步驟無法解決 hello 問題，請開啟[支援票證](https://azure.microsoft.com/support/options/)。</span><span class="sxs-lookup"><span data-stu-id="670b9-212">If hello preceding steps do not resolve hello issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

