---
title: "在 Azure 網路監看員 aaaIntroduction tooconnectivity 核取 |Microsoft 文件"
description: "此頁面提供 hello 網路監看員連線功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 52fc4547f167cea2992a046859dc0550d136e80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooconnectivity-check-in-azure-network-watcher"></a><span data-ttu-id="1537c-103">Azure 網路監看員的簡介 tooconnectivity 簽入</span><span class="sxs-lookup"><span data-stu-id="1537c-103">Introduction tooconnectivity check in Azure Network Watcher</span></span>

<span data-ttu-id="1537c-104">hello 連線功能的網路監看員提供 hello 功能 toocheck 直接的 TCP 連線，從虛擬機器 tooa 虛擬機器 (VM)、 完整的網域名稱 (FQDN) 的 URI，或 IPv4 位址。</span><span class="sxs-lookup"><span data-stu-id="1537c-104">hello connectivity feature of Network Watcher provides hello capability toocheck a direct TCP connection from a virtual machine tooa virtual machine (VM), fully qualified domain name (FQDN), URI, or IPv4 address.</span></span> <span data-ttu-id="1537c-105">網路案例很複雜，它們在實作時使用網路安全性群組、防火牆、使用者定義的路由和 Azure 所提供的資源。</span><span class="sxs-lookup"><span data-stu-id="1537c-105">Network scenarios are complex, they are implemented using Network Security Groups, firewalls, User-defined routes, and resources provided by Azure.</span></span> <span data-ttu-id="1537c-106">複雜的設定使得針對連線問題進行疑難排解成為一項挑戰。</span><span class="sxs-lookup"><span data-stu-id="1537c-106">Complex configurations make troubleshooting connectivity issues challenging.</span></span> <span data-ttu-id="1537c-107">網路監看員有助於縮短的時間 toofind hello 和偵測連線問題。</span><span class="sxs-lookup"><span data-stu-id="1537c-107">Network Watcher helps reduce hello amount of time toofind and detect connectivity issues.</span></span> <span data-ttu-id="1537c-108">傳回的 hello 結果可以提供深入了解有連線問題是否由於 tooa 平台或使用者組態問題。</span><span class="sxs-lookup"><span data-stu-id="1537c-108">hello results returned can provide insights into whether a connectivity issue is due tooa platform or a user configuration issue.</span></span> <span data-ttu-id="1537c-109">連線可以使用 [PowerShell](network-watcher-connectivity-powershell.md)、[Azure CLI](network-watcher-connectivity-cli.md) 和 [REST API](network-watcher-connectivity-rest.md) 來檢查。</span><span class="sxs-lookup"><span data-stu-id="1537c-109">Connectivity can be checked with [PowerShell](network-watcher-connectivity-powershell.md), [Azure CLI](network-watcher-connectivity-cli.md), and [REST API](network-watcher-connectivity-rest.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1537c-110">連線檢查需要虛擬機器延伸模組 `AzureNetworkWatcherExtension`。</span><span class="sxs-lookup"><span data-stu-id="1537c-110">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1537c-111">Hello 擴充功能安裝在 Windows VM 上瀏覽[Azure 網路監看員的代理程式適用於 Windows 的虛擬機器擴充功能](../virtual-machines/windows/extensions-nwa.md)和如 Linux VM，請造訪[Azure 網路監看員的代理程式虛擬機器擴充功能，適用於 Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="1537c-111">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="response"></a><span data-ttu-id="1537c-112">Response</span><span class="sxs-lookup"><span data-stu-id="1537c-112">Response</span></span>

<span data-ttu-id="1537c-113">下表中的 hello 顯示 hello 連線能力檢查已完成執行時，傳回的屬性。</span><span class="sxs-lookup"><span data-stu-id="1537c-113">hello following table shows hello properties returned when a connectivity check has finished running.</span></span>

|<span data-ttu-id="1537c-114">屬性</span><span class="sxs-lookup"><span data-stu-id="1537c-114">Property</span></span>  |<span data-ttu-id="1537c-115">說明</span><span class="sxs-lookup"><span data-stu-id="1537c-115">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="1537c-116">ConnectionStatus</span><span class="sxs-lookup"><span data-stu-id="1537c-116">ConnectionStatus</span></span>     | <span data-ttu-id="1537c-117">hello hello 連線能力檢查狀態。</span><span class="sxs-lookup"><span data-stu-id="1537c-117">hello status of hello connectivity check.</span></span> <span data-ttu-id="1537c-118">可能的結果是 **Reachable** 和 **Unreachable**。</span><span class="sxs-lookup"><span data-stu-id="1537c-118">Possible results are **Reachable** and **Unreachable**.</span></span>        |
|<span data-ttu-id="1537c-119">AvgLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="1537c-119">AvgLatencyInMs</span></span>     | <span data-ttu-id="1537c-120">平均延遲期間 hello 連線能力檢查，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="1537c-120">Average latency during hello connectivity check in milliseconds.</span></span> <span data-ttu-id="1537c-121">(只有在檢查狀態為可連線時顯示)</span><span class="sxs-lookup"><span data-stu-id="1537c-121">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="1537c-122">MinLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="1537c-122">MinLatencyInMs</span></span>     | <span data-ttu-id="1537c-123">Hello 連線期間的最小延遲檢查，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="1537c-123">Minimum latency during hello connectivity check in milliseconds.</span></span> <span data-ttu-id="1537c-124">(只有在檢查狀態為可連線時顯示)</span><span class="sxs-lookup"><span data-stu-id="1537c-124">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="1537c-125">MaxLatencyInMs</span><span class="sxs-lookup"><span data-stu-id="1537c-125">MaxLatencyInMs</span></span>     | <span data-ttu-id="1537c-126">最大延遲期間 hello 連線檢查以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="1537c-126">Maximum latency during hello connectivity check in milliseconds.</span></span> <span data-ttu-id="1537c-127">(只有在檢查狀態為可連線時顯示)</span><span class="sxs-lookup"><span data-stu-id="1537c-127">(Only shown if check status is reachable)</span></span>        |
|<span data-ttu-id="1537c-128">ProbesSent</span><span class="sxs-lookup"><span data-stu-id="1537c-128">ProbesSent</span></span>     | <span data-ttu-id="1537c-129">Hello 檢查期間傳送的探查數目。</span><span class="sxs-lookup"><span data-stu-id="1537c-129">Number of probes sent during hello check.</span></span> <span data-ttu-id="1537c-130">最大值是 100。</span><span class="sxs-lookup"><span data-stu-id="1537c-130">Max value is 100.</span></span>        |
|<span data-ttu-id="1537c-131">ProbesFailed</span><span class="sxs-lookup"><span data-stu-id="1537c-131">ProbesFailed</span></span>     | <span data-ttu-id="1537c-132">Hello 檢查期間失敗的探查數目。</span><span class="sxs-lookup"><span data-stu-id="1537c-132">Number of probes that failed during hello check.</span></span> <span data-ttu-id="1537c-133">最大值是 100。</span><span class="sxs-lookup"><span data-stu-id="1537c-133">Max value is 100.</span></span>        |
|<span data-ttu-id="1537c-134">Hops</span><span class="sxs-lookup"><span data-stu-id="1537c-134">Hops</span></span>     | <span data-ttu-id="1537c-135">躍點路徑來躍點從來源 toodestination。</span><span class="sxs-lookup"><span data-stu-id="1537c-135">Hop by hop path from source toodestination.</span></span>        |
|<span data-ttu-id="1537c-136">Hops[].Type</span><span class="sxs-lookup"><span data-stu-id="1537c-136">Hops[].Type</span></span>     | <span data-ttu-id="1537c-137">資源類型。</span><span class="sxs-lookup"><span data-stu-id="1537c-137">Type of resource.</span></span> <span data-ttu-id="1537c-138">可能的值為 **Source**、**VirtualAppliance**、**VnetLocal** 和 **Internet**。</span><span class="sxs-lookup"><span data-stu-id="1537c-138">Possible values are **Source**, **VirtualAppliance**, **VnetLocal**, and **Internet**.</span></span>        |
|<span data-ttu-id="1537c-139">Hops[].Id</span><span class="sxs-lookup"><span data-stu-id="1537c-139">Hops[].Id</span></span> | <span data-ttu-id="1537c-140">Hello 躍點的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="1537c-140">Unique identifier of hello hop.</span></span>|
|<span data-ttu-id="1537c-141">Hops[].Address</span><span class="sxs-lookup"><span data-stu-id="1537c-141">Hops[].Address</span></span> | <span data-ttu-id="1537c-142">Hello 躍點 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1537c-142">IP address of hello hop.</span></span>|
|<span data-ttu-id="1537c-143">Hops[].ResourceId</span><span class="sxs-lookup"><span data-stu-id="1537c-143">Hops[].ResourceId</span></span> | <span data-ttu-id="1537c-144">Hello 躍點如果 hello 躍點是一項 Azure 資源的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="1537c-144">ResourceID of hello hop if hello hop is an Azure resource.</span></span> <span data-ttu-id="1537c-145">如果是網際網路資源，ResourceID 是 **Internet**。</span><span class="sxs-lookup"><span data-stu-id="1537c-145">If it is an internet resource, ResourceID is **Internet**.</span></span> |
|<span data-ttu-id="1537c-146">Hops[].NextHopIds</span><span class="sxs-lookup"><span data-stu-id="1537c-146">Hops[].NextHopIds</span></span> | <span data-ttu-id="1537c-147">hello hello 採取的下一個躍點的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="1537c-147">hello unique identifier of hello next hop taken.</span></span>|
|<span data-ttu-id="1537c-148">Hops[].Issues</span><span class="sxs-lookup"><span data-stu-id="1537c-148">Hops[].Issues</span></span> | <span data-ttu-id="1537c-149">在該躍點的 hello 檢查期間遇到之問題的集合。</span><span class="sxs-lookup"><span data-stu-id="1537c-149">A collection of issues that were encountered during hello check at that hop.</span></span> <span data-ttu-id="1537c-150">如果有任何問題，hello 值是空白的。</span><span class="sxs-lookup"><span data-stu-id="1537c-150">If there were no issues, hello value is blank.</span></span>|
|<span data-ttu-id="1537c-151">Hops[].Issues[].Origin</span><span class="sxs-lookup"><span data-stu-id="1537c-151">Hops[].Issues[].Origin</span></span> | <span data-ttu-id="1537c-152">在 hello 目前躍點，在發生問題。</span><span class="sxs-lookup"><span data-stu-id="1537c-152">At hello current hop, where issue occurred.</span></span> <span data-ttu-id="1537c-153">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="1537c-153">Possible values are:</span></span><br/> <span data-ttu-id="1537c-154">**輸入**-位於 hello 連結從 hello 前一個躍點 toohello 目前躍點的問題</span><span class="sxs-lookup"><span data-stu-id="1537c-154">**Inbound** - Issue is on hello link from hello previous hop toohello current hop</span></span><br/><span data-ttu-id="1537c-155">**輸出**-位於 hello 連結從 hello 目前躍點 toohello 下一個躍點的問題</span><span class="sxs-lookup"><span data-stu-id="1537c-155">**Outbound** - Issue is on hello link from hello current hop toohello next hop</span></span><br/><span data-ttu-id="1537c-156">**本機**-位於 hello 目前躍點的問題。</span><span class="sxs-lookup"><span data-stu-id="1537c-156">**Local** - Issue is on hello current hop.</span></span>|
|<span data-ttu-id="1537c-157">Hops[].Issues[].Severity</span><span class="sxs-lookup"><span data-stu-id="1537c-157">Hops[].Issues[].Severity</span></span> | <span data-ttu-id="1537c-158">hello 偵測到的 hello 問題嚴重性。</span><span class="sxs-lookup"><span data-stu-id="1537c-158">hello severity of hello issue detected.</span></span> <span data-ttu-id="1537c-159">可能的值為 **Error** 和 **Warning**。</span><span class="sxs-lookup"><span data-stu-id="1537c-159">Possible values are **Error** and **Warning**.</span></span> |
|<span data-ttu-id="1537c-160">Hops[].Issues[].Type</span><span class="sxs-lookup"><span data-stu-id="1537c-160">Hops[].Issues[].Type</span></span> |<span data-ttu-id="1537c-161">找到問題的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="1537c-161">hello type of issue found.</span></span> <span data-ttu-id="1537c-162">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="1537c-162">Possible values are:</span></span> <br/><span data-ttu-id="1537c-163">**CPU**</span><span class="sxs-lookup"><span data-stu-id="1537c-163">**CPU**</span></span><br/><span data-ttu-id="1537c-164">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="1537c-164">**Memory**</span></span><br/><span data-ttu-id="1537c-165">**GuestFirewall**</span><span class="sxs-lookup"><span data-stu-id="1537c-165">**GuestFirewall**</span></span><br/><span data-ttu-id="1537c-166">**DnsResolution**</span><span class="sxs-lookup"><span data-stu-id="1537c-166">**DnsResolution**</span></span><br/><span data-ttu-id="1537c-167">**NetworkSecurityRule**</span><span class="sxs-lookup"><span data-stu-id="1537c-167">**NetworkSecurityRule**</span></span><br/><span data-ttu-id="1537c-168">**UserDefinedRoute**</span><span class="sxs-lookup"><span data-stu-id="1537c-168">**UserDefinedRoute**</span></span> |
|<span data-ttu-id="1537c-169">Hops[].Issues[].Context</span><span class="sxs-lookup"><span data-stu-id="1537c-169">Hops[].Issues[].Context</span></span> |<span data-ttu-id="1537c-170">找到的 hello 問題有關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1537c-170">Details regarding hello issue found.</span></span>|
|<span data-ttu-id="1537c-171">Hops[].Issues[].Context[].key</span><span class="sxs-lookup"><span data-stu-id="1537c-171">Hops[].Issues[].Context[].key</span></span> |<span data-ttu-id="1537c-172">傳回的 hello 機碼值組的機碼。</span><span class="sxs-lookup"><span data-stu-id="1537c-172">Key of hello key value pair returned.</span></span>|
|<span data-ttu-id="1537c-173">Hops[].Issues[].Context[].value</span><span class="sxs-lookup"><span data-stu-id="1537c-173">Hops[].Issues[].Context[].value</span></span> |<span data-ttu-id="1537c-174">傳回 hello 機碼值組的值。</span><span class="sxs-lookup"><span data-stu-id="1537c-174">Value of hello key value pair returned.</span></span>|

<span data-ttu-id="1537c-175">hello 以下是上一個躍點找到問題的範例。</span><span class="sxs-lookup"><span data-stu-id="1537c-175">hello following is an example of an issue found on a hop.</span></span>

```json
"Issues": [
    {
        "Origin": "Outbound",
        "Severity": "Error",
        "Type": "NetworkSecurityRule",
        "Context": [
            {
                "key": "RuleName",
                "value": "UserRule_Port80"
            }
        ]
    }
]
```
## <a name="fault-types"></a><span data-ttu-id="1537c-176">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="1537c-176">Fault types</span></span>

<span data-ttu-id="1537c-177">hello 連線能力檢查傳回 hello 連線相關的錯誤類型。</span><span class="sxs-lookup"><span data-stu-id="1537c-177">hello connectivity check returns fault types about hello connection.</span></span> <span data-ttu-id="1537c-178">hello 下表提供 hello 傳回目前的錯誤類型的清單。</span><span class="sxs-lookup"><span data-stu-id="1537c-178">hello following table provides a list of hello current fault types returned.</span></span>

|<span data-ttu-id="1537c-179">類型</span><span class="sxs-lookup"><span data-stu-id="1537c-179">Type</span></span>  |<span data-ttu-id="1537c-180">說明</span><span class="sxs-lookup"><span data-stu-id="1537c-180">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="1537c-181">CPU</span><span class="sxs-lookup"><span data-stu-id="1537c-181">CPU</span></span>     | <span data-ttu-id="1537c-182">高 CPU 使用率。</span><span class="sxs-lookup"><span data-stu-id="1537c-182">High CPU utilization.</span></span>       |
|<span data-ttu-id="1537c-183">記憶體</span><span class="sxs-lookup"><span data-stu-id="1537c-183">Memory</span></span>     | <span data-ttu-id="1537c-184">高記憶體使用率。</span><span class="sxs-lookup"><span data-stu-id="1537c-184">High Memory utilization.</span></span>       |
|<span data-ttu-id="1537c-185">GuestFirewall</span><span class="sxs-lookup"><span data-stu-id="1537c-185">GuestFirewall</span></span>     | <span data-ttu-id="1537c-186">由於 tooa 虛擬機器防火牆組態會封鎖流量。</span><span class="sxs-lookup"><span data-stu-id="1537c-186">Traffic is blocked due tooa virtual machine firewall configuration.</span></span>        |
|<span data-ttu-id="1537c-187">DNSResolution</span><span class="sxs-lookup"><span data-stu-id="1537c-187">DNSResolution</span></span>     | <span data-ttu-id="1537c-188">Hello 目的地位址的 DNS 解析失敗。</span><span class="sxs-lookup"><span data-stu-id="1537c-188">DNS resolution failed for hello destination address.</span></span>        |
|<span data-ttu-id="1537c-189">NetworkSecurityRule</span><span class="sxs-lookup"><span data-stu-id="1537c-189">NetworkSecurityRule</span></span>    | <span data-ttu-id="1537c-190">NSG 規則封鎖流量 (傳回規則)</span><span class="sxs-lookup"><span data-stu-id="1537c-190">Traffic is blocked by an NSG Rule (Rule is returned)</span></span>        |
|<span data-ttu-id="1537c-191">UserDefinedRoute</span><span class="sxs-lookup"><span data-stu-id="1537c-191">UserDefinedRoute</span></span>|<span data-ttu-id="1537c-192">流量會卸除，因為 tooa 使用者定義或系統路由。</span><span class="sxs-lookup"><span data-stu-id="1537c-192">Traffic is dropped due tooa user defined or system route.</span></span> |

### <a name="next-steps"></a><span data-ttu-id="1537c-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1537c-193">Next steps</span></span>

<span data-ttu-id="1537c-194">深入了解如何瀏覽 tooverify 連線 tooa 資源：[檢查連線與 Azure 網路監看員](network-watcher-connectivity-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="1537c-194">Learn how tooverify connectivity tooa resource by visiting: [Check connectivity with Azure Network Watcher](network-watcher-connectivity-powershell.md).</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png

