---
title: "網路安全性群組與 Azure 網路監看員的 aaaIntroduction tooflow 記錄 |Microsoft 文件"
description: "此頁面說明 toouse NSG 流程記錄 Azure 網路監看員的一項功能的方式"
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
ms.openlocfilehash: da85e946147b14717144cb47d1c742057c6dfa24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooflow-logging-for-network-security-groups"></a><span data-ttu-id="cbb32-103">網路安全性群組的簡介 tooflow 記錄</span><span class="sxs-lookup"><span data-stu-id="cbb32-103">Introduction tooflow logging for Network Security Groups</span></span>

<span data-ttu-id="cbb32-104">網路安全性小組流程記錄檔是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。</span><span class="sxs-lookup"><span data-stu-id="cbb32-104">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="cbb32-105">這些流程記錄檔會寫入以 json 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。</span><span class="sxs-lookup"><span data-stu-id="cbb32-105">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

![流量記錄概觀][1]

<span data-ttu-id="cbb32-107">流程記錄目標網路安全性群組，而不會顯示 hello 相同 hello 做其他記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cbb32-107">While flow logs target Network Security Groups, they are not displayed hello same as hello other logs.</span></span> <span data-ttu-id="cbb32-108">流程記錄會儲存在儲存體帳戶和下列 hello 記錄路徑內，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="cbb32-108">Flow logs are stored only within a storage account and following hello logging path as shown in hello following example:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="cbb32-109">hello 相同套用 tooflow 記錄的其他記錄檔所見的保留原則。</span><span class="sxs-lookup"><span data-stu-id="cbb32-109">hello same retention policies as seen on other logs apply tooflow logs.</span></span> <span data-ttu-id="cbb32-110">記錄檔具有可設定為 1 天 too365 天的保留原則。</span><span class="sxs-lookup"><span data-stu-id="cbb32-110">Logs have a retention policy that can be set from 1 day too365 days.</span></span> <span data-ttu-id="cbb32-111">如果未設定保留原則，就會永遠保留 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cbb32-111">If a retention policy is not set, hello logs are maintained forever.</span></span>

## <a name="log-file"></a><span data-ttu-id="cbb32-112">記錄檔</span><span class="sxs-lookup"><span data-stu-id="cbb32-112">Log file</span></span>

<span data-ttu-id="cbb32-113">流量記錄有多個屬性。</span><span class="sxs-lookup"><span data-stu-id="cbb32-113">Flow logs have multiple properties.</span></span> <span data-ttu-id="cbb32-114">hello 下列清單是 hello NSG 流程記錄中傳回的 hello 屬性的清單：</span><span class="sxs-lookup"><span data-stu-id="cbb32-114">hello following list is a listing of hello properties that are returned within hello NSG flow log:</span></span>

* <span data-ttu-id="cbb32-115">**時間**-時間時記錄 hello 事件</span><span class="sxs-lookup"><span data-stu-id="cbb32-115">**time** - Time when hello event was logged</span></span>
* <span data-ttu-id="cbb32-116">**systemId** - 網路安全性群組資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="cbb32-116">**systemId** - Network Security Group resource Id.</span></span>
* <span data-ttu-id="cbb32-117">**類別**-hello 類別 hello 事件，這是永遠是 NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="cbb32-117">**category** - hello category of hello event, this is always be NetworkSecurityGroupFlowEvent</span></span>
* <span data-ttu-id="cbb32-118">**resourceid** -hello hello NSG 的資源 Id</span><span class="sxs-lookup"><span data-stu-id="cbb32-118">**resourceid** - hello resource Id of hello NSG</span></span>
* <span data-ttu-id="cbb32-119">**operationName** - 一律是 NetworkSecurityGroupFlowEvents</span><span class="sxs-lookup"><span data-stu-id="cbb32-119">**operationName** - Always NetworkSecurityGroupFlowEvents</span></span>
* <span data-ttu-id="cbb32-120">**屬性**-hello 流程的屬性集合</span><span class="sxs-lookup"><span data-stu-id="cbb32-120">**properties** - A collection of properties of hello flow</span></span>
    * <span data-ttu-id="cbb32-121">**版本**-hello 流程記錄事件結構描述版本號碼</span><span class="sxs-lookup"><span data-stu-id="cbb32-121">**Version** - Version number of hello Flow Log event schema</span></span>
    * <span data-ttu-id="cbb32-122">**flows** - 流量的集合。</span><span class="sxs-lookup"><span data-stu-id="cbb32-122">**flows** - A collection of flows.</span></span> <span data-ttu-id="cbb32-123">這個屬性有多個適用於不同規則的項目</span><span class="sxs-lookup"><span data-stu-id="cbb32-123">This property has multiple entries for different rules</span></span>
        * <span data-ttu-id="cbb32-124">**規則**-列出哪些 hello 流量的規則</span><span class="sxs-lookup"><span data-stu-id="cbb32-124">**rule** - Rule for which hello flows are listed</span></span>
            * <span data-ttu-id="cbb32-125">**flows** - 流量的集合</span><span class="sxs-lookup"><span data-stu-id="cbb32-125">**flows** - a collection of flows</span></span>
                * <span data-ttu-id="cbb32-126">**mac** -hello hello 收集 hello 流程所在的 VM hello NIC 的 MAC 位址</span><span class="sxs-lookup"><span data-stu-id="cbb32-126">**mac** - hello MAC address of hello NIC for hello VM where hello flow was collected</span></span>
                * <span data-ttu-id="cbb32-127">**flowTuples** -包含以逗號分隔格式的 hello 流程 tuple 的多個屬性的字串</span><span class="sxs-lookup"><span data-stu-id="cbb32-127">**flowTuples** - A string that contains multiple properties for hello flow tuple in comma-separated format</span></span>
                    * <span data-ttu-id="cbb32-128">**時間戳記**-hello 流程發生 UNIX EPOCH 格式時，這個值會是 hello 時間戳記</span><span class="sxs-lookup"><span data-stu-id="cbb32-128">**Time Stamp** - This value is hello time stamp of when hello flow occurred in UNIX EPOCH format</span></span>
                    * <span data-ttu-id="cbb32-129">**來源 IP** -hello 來源 IP</span><span class="sxs-lookup"><span data-stu-id="cbb32-129">**Source IP** - hello source IP</span></span>
                    * <span data-ttu-id="cbb32-130">**目的地 IP** -hello 目的地 IP</span><span class="sxs-lookup"><span data-stu-id="cbb32-130">**Destination IP** - hello destination IP</span></span>
                    * <span data-ttu-id="cbb32-131">**來源連接埠**-hello 來源連接埠</span><span class="sxs-lookup"><span data-stu-id="cbb32-131">**Source Port** - hello source port</span></span>
                    * <span data-ttu-id="cbb32-132">**目的地連接埠**-hello 目的地連接埠</span><span class="sxs-lookup"><span data-stu-id="cbb32-132">**Destination Port** - hello destination Port</span></span>
                    * <span data-ttu-id="cbb32-133">**通訊協定**-hello hello 流量的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="cbb32-133">**Protocol** - hello protocol of hello flow.</span></span> <span data-ttu-id="cbb32-134">有效值為 **T** (若為 TCP) 和 **U** (若為 UDP)</span><span class="sxs-lookup"><span data-stu-id="cbb32-134">Valid values are **T** for TCP and **U** for UDP</span></span>
                    * <span data-ttu-id="cbb32-135">**流量流程**-hello hello 流量的方向。</span><span class="sxs-lookup"><span data-stu-id="cbb32-135">**Traffic Flow** - hello direction of hello traffic flow.</span></span> <span data-ttu-id="cbb32-136">有效值為 **I** (若為輸入) 和 **O** (若為輸出)。</span><span class="sxs-lookup"><span data-stu-id="cbb32-136">Valid values are **I** for inbound and **O** for outbound.</span></span>
                    * <span data-ttu-id="cbb32-137">**流量** - 流量受到允許或拒絕。</span><span class="sxs-lookup"><span data-stu-id="cbb32-137">**Traffic** - Whether traffic was allowed or denied.</span></span> <span data-ttu-id="cbb32-138">有效值為 **A** (若允許) 和 **D** (若拒絕)。</span><span class="sxs-lookup"><span data-stu-id="cbb32-138">Valid values are **A** for allowed and **D** for denied.</span></span>


<span data-ttu-id="cbb32-139">hello 的範例如下的流量記錄檔。</span><span class="sxs-lookup"><span data-stu-id="cbb32-139">hello following is an example of a Flow log.</span></span> <span data-ttu-id="cbb32-140">您可以看到有遵循 hello hello 前面一節中所述的屬性清單的多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="cbb32-140">As you can see there are multiple records that follow hello property list described in hello preceding section.</span></span> 

> [!NOTE]
> <span data-ttu-id="cbb32-141">Hello flowTuples 屬性中的值是以逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="cbb32-141">Values in hello flowTuples property are a comma-separated list.</span></span>
 
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

## <a name="next-steps"></a><span data-ttu-id="cbb32-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbb32-142">Next steps</span></span>

<span data-ttu-id="cbb32-143">了解 tooenable 流程造訪的記錄方式[啟用流程記錄](network-watcher-nsg-flow-logging-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="cbb32-143">Learn how tooenable Flow logs by visiting [Enabling Flow logging](network-watcher-nsg-flow-logging-portal.md).</span></span>

<span data-ttu-id="cbb32-144">瀏覽[網路安全性群組 (NSG) 的 Log Analytics](../virtual-network/virtual-network-nsg-manage-log.md)，以了解 NSG 記錄。</span><span class="sxs-lookup"><span data-stu-id="cbb32-144">Learn about NSG logging by visiting [Log analytics for network security groups (NSGs)](../virtual-network/virtual-network-nsg-manage-log.md).</span></span>

<span data-ttu-id="cbb32-145">瀏覽[使用 IP 流量驗證來驗證流量](network-watcher-check-ip-flow-verify-portal.md)，以了解流量在 VM 上受到允許或拒絕</span><span class="sxs-lookup"><span data-stu-id="cbb32-145">Find out if traffic is allowed or denied on a VM by visiting [Verify traffic with IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-overview/figure1.png

