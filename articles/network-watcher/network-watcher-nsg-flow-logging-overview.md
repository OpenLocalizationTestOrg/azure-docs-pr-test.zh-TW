---
title: "Azure 網路監看員的網路安全性群組流量記錄簡介 | Microsoft Docs"
description: "本頁說明如何使用 Azure 網路監看員的 NSG 流量記錄功能"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 47d91341-16f1-45ac-85a5-e5a640f5d59e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b7a9162d6c6219b6b1c51a49cd34b9616e9d3e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-flow-logging-for-network-security-groups"></a><span data-ttu-id="c5c64-103">網路安全性群組流量記錄簡介</span><span class="sxs-lookup"><span data-stu-id="c5c64-103">Introduction to flow logging for Network Security Groups</span></span>

<span data-ttu-id="c5c64-104">網路安全性群組流量記錄是網路監看員的一項功能，可讓您檢視透過網路安全性群組傳輸之輸入和輸出 IP 流量的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c5c64-104">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="c5c64-105">這些流量記錄是以 json 格式撰寫，會顯示每一規則的輸出和輸入流量、流量套用至的 NIC、有關流量的 5 個 Tuple 資訊 (來源/目的地 IP、來源/目的地連接埠、通訊協定)，以及流量是被允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="c5c64-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

![流量記錄概觀][1]

<span data-ttu-id="c5c64-107">雖然流程記錄檔是以「網路安全性群組」為目標，但其顯示方式與其他記錄檔不同。</span><span class="sxs-lookup"><span data-stu-id="c5c64-107">While flow logs target Network Security Groups, they are not displayed the same as the other logs.</span></span> <span data-ttu-id="c5c64-108">流程記錄檔只會儲存在儲存體帳戶內，並且會採用如以下範例所示的記錄路徑：</span><span class="sxs-lookup"><span data-stu-id="c5c64-108">Flow logs are stored only within a storage account and following the logging path as shown in the following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="c5c64-109">在其他記錄上看到的保留原則也同樣適用於流量記錄。</span><span class="sxs-lookup"><span data-stu-id="c5c64-109">The same retention policies as seen on other logs apply to flow logs.</span></span> <span data-ttu-id="c5c64-110">記錄的保留原則可設定為 1 天到 365 天。</span><span class="sxs-lookup"><span data-stu-id="c5c64-110">Logs have a retention policy that can be set from 1 day to 365 days.</span></span> <span data-ttu-id="c5c64-111">如果未設定保留原則，則會永遠保留記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c5c64-111">If a retention policy is not set, the logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="c5c64-112">記錄檔</span><span class="sxs-lookup"><span data-stu-id="c5c64-112">Log file</span></span>

<span data-ttu-id="c5c64-113">流量記錄有多個屬性。</span><span class="sxs-lookup"><span data-stu-id="c5c64-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="c5c64-114">下列清單列出 NSG 流量記錄內會傳回的屬性︰</span><span class="sxs-lookup"><span data-stu-id="c5c64-114">The following list is a listing of the properties that are returned within the NSG flow log:</span></span>

* <span data-ttu-id="c5c64-115">**time** - 事件的記錄時間</span><span class="sxs-lookup"><span data-stu-id="c5c64-115">**time** - Time when the event was logged</span></span>
* <span data-ttu-id="c5c64-116">**systemId** - 網路安全性群組資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="c5c64-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="c5c64-117">**category** - 事件的類別，此屬性一律是 NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="c5c64-117">**category** - The category of the event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="c5c64-118">**resourceid** - NSG 的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="c5c64-118">**resourceid** - The resource Id of the NSG</span></span>
* <span data-ttu-id="c5c64-119">**operationName** - 一律是 NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="c5c64-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="c5c64-120">**properties** - 流量屬性的集合</span><span class="sxs-lookup"><span data-stu-id="c5c64-120">**properties** - A collection of properties of the flow</span></span>
    * <span data-ttu-id="c5c64-121">**Version** - 流量記錄事件結構描述的版本號碼</span><span class="sxs-lookup"><span data-stu-id="c5c64-121">**Version** - Version number of the Flow Log event schema</span></span>
    * <span data-ttu-id="c5c64-122">**flows** - 流量的集合。</span><span class="sxs-lookup"><span data-stu-id="c5c64-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="c5c64-123">這個屬性有多個適用於不同規則的項目</span><span class="sxs-lookup"><span data-stu-id="c5c64-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="c5c64-124">**rule** - 做為流量列出依據的規則</span><span class="sxs-lookup"><span data-stu-id="c5c64-124">**rule** - Rule for which the flows are listed</span></span>
            * <span data-ttu-id="c5c64-125">**flows** - 流量的集合</span><span class="sxs-lookup"><span data-stu-id="c5c64-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="c5c64-126">**mac** - 流量收集所在 VM 之 NIC 的 MAC 位址</span><span class="sxs-lookup"><span data-stu-id="c5c64-126">**mac** - The MAC address of the NIC for the VM where the flow was collected</span></span>
                * <span data-ttu-id="c5c64-127">**flowTuples** - 包含多個流量 tuple 屬性的逗號分隔格式字串</span><span class="sxs-lookup"><span data-stu-id="c5c64-127">**flowTuples** - A string that contains multiple properties for the flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="c5c64-128">**時間戳記** - 這個值是流量發生時的時間戳記，格式為 UNIX EPOCH</span><span class="sxs-lookup"><span data-stu-id="c5c64-128">**Time Stamp** - This value is the time stamp of when the flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="c5c64-129">**來源 IP** - 來源 IP</span><span class="sxs-lookup"><span data-stu-id="c5c64-129">**Source IP** - The source IP</span></span>
                    * <span data-ttu-id="c5c64-130">**目的地 IP** - 目的地 IP</span><span class="sxs-lookup"><span data-stu-id="c5c64-130">**Destination IP** - The destination IP</span></span>
                    * <span data-ttu-id="c5c64-131">**來源連接埠** - 來源連接埠</span><span class="sxs-lookup"><span data-stu-id="c5c64-131">**Source Port** - The source port</span></span>
                    * <span data-ttu-id="c5c64-132">**目的地連接埠** - 目的地連接埠</span><span class="sxs-lookup"><span data-stu-id="c5c64-132">**Destination Port** - The destination Port</span></span>
                    * <span data-ttu-id="c5c64-133">**通訊協定** - 流量的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="c5c64-133">**Protocol** - The protocol of the flow.</span></span> <span data-ttu-id="c5c64-134">有效值為 **T** (若為 TCP) 和 **U** (若為 UDP)</span><span class="sxs-lookup"><span data-stu-id="c5c64-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="c5c64-135">**流量流動** - 流量的流動方向。</span><span class="sxs-lookup"><span data-stu-id="c5c64-135">**Traffic Flow** - The direction of the traffic flow.</span></span> <span data-ttu-id="c5c64-136">有效值為 **I** (若為輸入) 和 **O** (若為輸出)。</span><span class="sxs-lookup"><span data-stu-id="c5c64-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="c5c64-137">**流量** - 流量受到允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="c5c64-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="c5c64-138">有效值為 **A** (若允許) 和 **D** (若拒絕)。</span><span class="sxs-lookup"><span data-stu-id="c5c64-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="c5c64-139">以下是流量記錄的範例。</span><span class="sxs-lookup"><span data-stu-id="c5c64-139">The following is an example of a Flow log.</span></span> <span data-ttu-id="c5c64-140">如您所見，有多筆記錄遵循上一節所述的屬性清單。</span><span class="sxs-lookup"><span data-stu-id="c5c64-140">As you can see there are multiple records that follow the property list described in the preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="c5c64-141">flowTuples 屬性中的值是逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="c5c64-141">Values in the flowTuples property are a comma-separated list.</span></span>
 
```json
{
    "records": 
    [
        
        {
             "time": "2017-02-16T22:00:32.8950000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282421,42.119.146.95,10.1.0.4,51529,5358,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282370,163.28.66.17,10.1.0.4,61771,3389,T,I,A","1487282393,5.39.218.34,10.1.0.4,58596,3389,T,I,A","1487282393,91.224.160.154,10.1.0.4,61540,3389,T,I,A","1487282423,13.76.89.229,10.1.0.4,53163,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:01:32.8960000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282481,195.78.210.194,10.1.0.4,53,1732,U,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282435,61.129.251.68,10.1.0.4,57776,3389,T,I,A","1487282454,84.25.174.170,10.1.0.4,59085,3389,T,I,A","1487282477,77.68.9.50,10.1.0.4,65078,3389,T,I,A"]}]}]}
        }
        ,
        {
             "time": "2017-02-16T22:02:32.9040000Z",
             "systemId": "2c002c16-72f3-4dc5-b391-3444c3527434",
             "category": "NetworkSecurityGroupFlowEvent",
             "resourceId": "/SUBSCRIPTIONS/00000000-0000-0000-0000-000000000000/RESOURCEGROUPS/FABRIKAMRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/FABRIAKMVM1-NSG",
             "operationName": "NetworkSecurityGroupFlowEvents",
             "properties": {"Version":1,"flows":[{"rule":"DefaultRule_DenyAllInBound","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282492,175.182.69.29,10.1.0.4,28918,5358,T,I,D","1487282505,71.6.216.55,10.1.0.4,8080,8080,T,I,D"]}]},{"rule":"UserRule_default-allow-rdp","flows":[{"mac":"000D3AF8801A","flowTuples":["1487282512,91.224.160.154,10.1.0.4,59046,3389,T,I,A"]}]}]}
        }
        ,
        ...
```

## <a name="next-steps"></a><span data-ttu-id="c5c64-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c5c64-142">Next steps</span></span>

<span data-ttu-id="c5c64-143">瀏覽[啟用流量記錄](network-watcher-nsg-flow-logging-portal.md)，以了解如何啟用流量記錄。</span><span class="sxs-lookup"><span data-stu-id="c5c64-143">Learn how to enable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="c5c64-144">瀏覽[網路安全性群組 (NSG) 的 Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md)，以了解 NSG 記錄。</span><span class="sxs-lookup"><span data-stu-id="c5c64-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="c5c64-145">瀏覽[使用 IP 流量驗證來驗證流量](network-watcher-check-ip-flow-verify-portal.md)，以了解流量在 VM 上受到允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="c5c64-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

