---
title: "aaaIntroduction tooAzure 網路監看員 |Microsoft 文件"
description: "此頁面提供的 hello 網路監看員監視的服務概觀，並以視覺化方式檢視網路連線在 Azure 中的資源"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a><span data-ttu-id="02159-103">Azure 網路監視概觀</span><span class="sxs-lookup"><span data-stu-id="02159-103">Azure network monitoring overview</span></span>

<span data-ttu-id="02159-104">客戶可藉由安排和組合各種個別的網路資源 (例如 VNet、ExpressRoute、應用程式閘道、負載平衡器等等)，在 Azure 中建置端對端網路。</span><span class="sxs-lookup"><span data-stu-id="02159-104">Customers build an end-to-end network in Azure by orchestrating and composing various individual network resources such as VNet, ExpressRoute, Application Gateway, Load balancers, and more.</span></span> <span data-ttu-id="02159-105">使用每個 hello 網路資源的監視。</span><span class="sxs-lookup"><span data-stu-id="02159-105">Monitoring is available on each of hello network resources.</span></span> <span data-ttu-id="02159-106">我們 toothis 監視做為資源層級的監視。</span><span class="sxs-lookup"><span data-stu-id="02159-106">We refer toothis monitoring as resource level monitoring.</span></span>

<span data-ttu-id="02159-107">hello 結束 tooend 網路可具有複雜的組態和資源，建立複雜的案例需要的案例為基礎的監視透過網路監看員之間的互動。</span><span class="sxs-lookup"><span data-stu-id="02159-107">hello end tooend network can have complex configurations and interactions between resources, creating complex scenarios that need scenario-based monitoring through Network Watcher.</span></span>

<span data-ttu-id="02159-108">本文將探討案例和資源層級的監視。</span><span class="sxs-lookup"><span data-stu-id="02159-108">This article covers scenario and resource level monitoring.</span></span> <span data-ttu-id="02159-109">Azure 中的網路監視功能相當完善，主要涵蓋類別有二種︰</span><span class="sxs-lookup"><span data-stu-id="02159-109">Network monitoring in Azure is comprehensive and covers two broad categories:</span></span>

* <span data-ttu-id="02159-110">[**網路監看員**](#network-watcher) -提供以案例為基礎監視使用中網路監看員的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="02159-110">[**Network Watcher**](#network-watcher) - Scenario-based monitoring is provided with hello features in Network Watcher.</span></span> <span data-ttu-id="02159-111">這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。</span><span class="sxs-lookup"><span data-stu-id="02159-111">This service includes packet capture, next hop, IP flow verify, security group view, NSG flow logs.</span></span> <span data-ttu-id="02159-112">案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。</span><span class="sxs-lookup"><span data-stu-id="02159-112">Scenario level monitoring provides an end tooend view of network resources in contrast tooindividual network resource monitoring.</span></span>
* <span data-ttu-id="02159-113">[**資源監視**](#network-resource-level-monitoring) - 資源層級監視由診斷記錄、計量、疑難排解和資源健全狀況這四個功能所組成。</span><span class="sxs-lookup"><span data-stu-id="02159-113">[**Resource monitoring**](#network-resource-level-monitoring) - Resource level monitoring comprises of four features, diagnostic logs, metrics, troubleshooting, and resource health.</span></span> <span data-ttu-id="02159-114">所有這些功能是建置在 hello 網路資源層級。</span><span class="sxs-lookup"><span data-stu-id="02159-114">All these features are built at hello network resource level.</span></span>

## <a name="network-watcher"></a><span data-ttu-id="02159-115">網路監看員</span><span class="sxs-lookup"><span data-stu-id="02159-115">Network Watcher</span></span>

<span data-ttu-id="02159-116">網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。</span><span class="sxs-lookup"><span data-stu-id="02159-116">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="02159-117">網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。</span><span class="sxs-lookup"><span data-stu-id="02159-117">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

<span data-ttu-id="02159-118">網路監看員目前具有下列功能的 hello:</span><span class="sxs-lookup"><span data-stu-id="02159-118">Network Watcher currently has hello following capabilities:</span></span>

* <span data-ttu-id="02159-119">**[拓樸](network-watcher-topology-overview.md)** -提供網路層級檢視顯示 hello 各種 connect 和資源群組中的網路資源之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="02159-119">**[Topology](network-watcher-topology-overview.md)** - Provides a network level view showing hello various interconnections and associations between network resources in a resource group.</span></span>
* <span data-ttu-id="02159-120">**[變動的封包擷取](network-watcher-packet-capture-overview.md)** - 擷取進出虛擬機器的封包資料。</span><span class="sxs-lookup"><span data-stu-id="02159-120">**[Variable Packet capture](network-watcher-packet-capture-overview.md)** - Captures packet data in and out of a virtual machine.</span></span> <span data-ttu-id="02159-121">進階篩選選項和微調的控制項，例如無法 tooset 加上時間和大小限制會提供彈性。</span><span class="sxs-lookup"><span data-stu-id="02159-121">Advanced filtering options and fine-tuned controls such as being able tooset time and size limitations provide versatility.</span></span> <span data-ttu-id="02159-122">hello 封包資料可以儲存在 blob 存放區或 hello.cap 格式的本機磁碟上。</span><span class="sxs-lookup"><span data-stu-id="02159-122">hello packet data can be stored in a blob store or on hello local disk in .cap format.</span></span>
* <span data-ttu-id="02159-123">**[IP 流量驗證](network-watcher-ip-flow-verify-overview.md)** - 根據流量資訊 5-tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 檢查是否允許或拒絕封包。</span><span class="sxs-lookup"><span data-stu-id="02159-123">**[IP flow verify](network-watcher-ip-flow-verify-overview.md)** - Checks if a packet is allowed or denied based on flow information 5-tuple packet parameters (Destination IP, Source IP, Destination Port, Source Port, and Protocol).</span></span> <span data-ttu-id="02159-124">如果安全性群組遭拒絕 hello 封包，hello 規則，並拒絕 hello 封包的群組會傳回。</span><span class="sxs-lookup"><span data-stu-id="02159-124">If hello packet is denied by a security group, hello rule and group that denied hello packet is returned.</span></span>
* <span data-ttu-id="02159-125">**[下一個躍點](network-watcher-next-hop-overview.md)** -決定 hello 封包路由傳送 hello Azure 網路網狀架構，讓您 toodiagnose 任何設定錯誤的使用者定義的路由中下一個躍點。</span><span class="sxs-lookup"><span data-stu-id="02159-125">**[Next hop](network-watcher-next-hop-overview.md)** - Determines hello next hop for packets being routed in hello Azure Network Fabric, enabling you toodiagnose any misconfigured user-defined routes.</span></span>
* <span data-ttu-id="02159-126">**[安全性的群組檢視](network-watcher-security-group-view-overview.md)** -取得 hello 有效且套用安全性規則，可在 VM 上套用。</span><span class="sxs-lookup"><span data-stu-id="02159-126">**[Security group view](network-watcher-security-group-view-overview.md)** - Gets hello effective and applied security rules that are applied on a VM.</span></span>
* <span data-ttu-id="02159-127">**[NSG 流程記錄](network-watcher-nsg-flow-logging-overview.md)** -網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。</span><span class="sxs-lookup"><span data-stu-id="02159-127">**[NSG Flow logging](network-watcher-nsg-flow-logging-overview.md)** - Flow logs for Network Security Groups enable you toocapture logs related tootraffic that are allowed or denied by hello security rules in hello group.</span></span> <span data-ttu-id="02159-128">hello 流程是由 5-tuple 資訊 – 來源 IP、 目的地 IP、 來源連接埠，目的地連接埠和通訊協定定義。</span><span class="sxs-lookup"><span data-stu-id="02159-128">hello flow is defined by a 5-tuple information – Source IP, Destination IP, Source Port, Destination Port and Protocol.</span></span>
* <span data-ttu-id="02159-129">**[虛擬網路閘道與連接疑難排解](network-watcher-troubleshoot-manage-rest.md)** -提供 hello 能力 tootroubleshoot 虛擬網路閘道與連線。</span><span class="sxs-lookup"><span data-stu-id="02159-129">**[Virtual Network Gateway and Connection troubleshooting](network-watcher-troubleshoot-manage-rest.md)** - Provides hello ability tootroubleshoot Virtual Network Gateways and Connections.</span></span>
* <span data-ttu-id="02159-130">**[訂用帳戶限制的網路](#network-subscription-limits)** -可讓您限制對 tooview 網路資源使用狀況。</span><span class="sxs-lookup"><span data-stu-id="02159-130">**[Network subscription limits](#network-subscription-limits)** - Enables you tooview network resource usage against limits.</span></span>
* <span data-ttu-id="02159-131">**[設定診斷記錄](#diagnostic-logs)** – 提供單一窗格 tooenable 或停用網路資源的資源群組中的診斷記錄檔。</span><span class="sxs-lookup"><span data-stu-id="02159-131">**[Configuring Diagnostics Log](#diagnostic-logs)** – Provides a single pane tooenable or disable Diagnostics logs for network resources in a resource group.</span></span>
* <span data-ttu-id="02159-132">**[連線能力 （預覽）](network-watcher-connectivity-overview.md)**  -確認 hello 可能會建立從虛擬機器 tooa 指定端點的直接 TCP 連接。</span><span class="sxs-lookup"><span data-stu-id="02159-132">**[Connectivity (Preview)](network-watcher-connectivity-overview.md)** - Verifies hello possibility of establishing a direct TCP connection from a virtual machine tooa given endpoint.</span></span>

### <a name="role-based-access-control-rbac-in-network-watcher"></a><span data-ttu-id="02159-133">網路監看員的角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="02159-133">Role-based Access Control (RBAC) in Network Watcher</span></span>

<span data-ttu-id="02159-134">網路監看員會使用 hello[所有存取控制 (RBAC) 模型](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="02159-134">Network watcher uses hello [Azure Role-Based Access Control (RBAC) model](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="02159-135">需要下列權限的 hello hello 網路監看員。</span><span class="sxs-lookup"><span data-stu-id="02159-135">hello following permissions are required by hello Network Watcher.</span></span> <span data-ttu-id="02159-136">重要 toomake 確定用於初始網路監看員應用程式開發介面或從 hello 入口網站中使用網路監看員該 hello 角色擁有 hello 需要存取它。</span><span class="sxs-lookup"><span data-stu-id="02159-136">It is important toomake sure that hello role used for initiating Network Watcher APIs or using Network Watcher from hello portal has hello required access.</span></span>

|<span data-ttu-id="02159-137">資源</span><span class="sxs-lookup"><span data-stu-id="02159-137">Resource</span></span>| <span data-ttu-id="02159-138">權限</span><span class="sxs-lookup"><span data-stu-id="02159-138">Permission</span></span>|
|---|---| 
|<span data-ttu-id="02159-139">Microsoft.Storage/</span><span class="sxs-lookup"><span data-stu-id="02159-139">Microsoft.Storage/</span></span> |<span data-ttu-id="02159-140">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-140">Read</span></span>|
|<span data-ttu-id="02159-141">Microsoft.Authorization/</span><span class="sxs-lookup"><span data-stu-id="02159-141">Microsoft.Authorization/</span></span>| <span data-ttu-id="02159-142">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-142">Read</span></span>| 
|<span data-ttu-id="02159-143">Microsoft.Resources/subscriptions/resourceGroups/</span><span class="sxs-lookup"><span data-stu-id="02159-143">Microsoft.Resources/subscriptions/resourceGroups/</span></span>| <span data-ttu-id="02159-144">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-144">Read</span></span>|
|<span data-ttu-id="02159-145">Microsoft.Storage/storageAccounts/listServiceSas/</span><span class="sxs-lookup"><span data-stu-id="02159-145">Microsoft.Storage/storageAccounts/listServiceSas/</span></span> | <span data-ttu-id="02159-146">動作</span><span class="sxs-lookup"><span data-stu-id="02159-146">Action</span></span>|
|<span data-ttu-id="02159-147">Microsoft.Storage/storageAccounts/listAccountSas/</span><span class="sxs-lookup"><span data-stu-id="02159-147">Microsoft.Storage/storageAccounts/listAccountSas/</span></span> |<span data-ttu-id="02159-148">動作</span><span class="sxs-lookup"><span data-stu-id="02159-148">Action</span></span>|
|<span data-ttu-id="02159-149">Microsoft.Storage/storageAccounts/listKeys/</span><span class="sxs-lookup"><span data-stu-id="02159-149">Microsoft.Storage/storageAccounts/listKeys/</span></span> | <span data-ttu-id="02159-150">動作</span><span class="sxs-lookup"><span data-stu-id="02159-150">Action</span></span>|
|<span data-ttu-id="02159-151">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="02159-151">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="02159-152">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-152">Read</span></span>|
|<span data-ttu-id="02159-153">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="02159-153">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="02159-154">寫入</span><span class="sxs-lookup"><span data-stu-id="02159-154">Write</span></span>|
|<span data-ttu-id="02159-155">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="02159-155">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="02159-156">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-156">Read</span></span>|
|<span data-ttu-id="02159-157">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="02159-157">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="02159-158">寫入</span><span class="sxs-lookup"><span data-stu-id="02159-158">Write</span></span>|
|<span data-ttu-id="02159-159">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="02159-159">Microsoft.Network/networkWatchers/packetCaptures/</span></span> |<span data-ttu-id="02159-160">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-160">Read</span></span>|
|<span data-ttu-id="02159-161">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="02159-161">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="02159-162">寫入</span><span class="sxs-lookup"><span data-stu-id="02159-162">Write</span></span>|
|<span data-ttu-id="02159-163">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="02159-163">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="02159-164">刪除</span><span class="sxs-lookup"><span data-stu-id="02159-164">Delete</span></span>|
|<span data-ttu-id="02159-165">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="02159-165">Microsoft.Network/networkWatchers/</span></span> |<span data-ttu-id="02159-166">寫入</span><span class="sxs-lookup"><span data-stu-id="02159-166">Write</span></span> |
|<span data-ttu-id="02159-167">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="02159-167">Microsoft.Network/networkWatchers/</span></span>| <span data-ttu-id="02159-168">讀取</span><span class="sxs-lookup"><span data-stu-id="02159-168">Read</span></span> |
|<span data-ttu-id="02159-169">Microsoft.Insights/alertRules/</span><span class="sxs-lookup"><span data-stu-id="02159-169">Microsoft.Insights/alertRules/</span></span> |*|
|<span data-ttu-id="02159-170">Microsoft.Support/</span><span class="sxs-lookup"><span data-stu-id="02159-170">Microsoft.Support/</span></span> | *|

### <a name="network-subscription-limits"></a><span data-ttu-id="02159-171">網路訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="02159-171">Network subscription limits</span></span>

<span data-ttu-id="02159-172">網路訂用帳戶限制為您提供的每個訂用帳戶中針對 hello 的可用資源的最大數目的區域中的 hello 網路資源的 hello 使用量的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02159-172">Network subscription limits provide you with details of hello usage of each of hello network resource in a subscription in a region against hello maximum number of resources available.</span></span>

![網路訂用帳戶限制][nsl]

## <a name="network-resource-level-monitoring"></a><span data-ttu-id="02159-174">網路資源層級監視</span><span class="sxs-lookup"><span data-stu-id="02159-174">Network resource level monitoring</span></span>

<span data-ttu-id="02159-175">下列功能的 hello 可供資源層級的監視：</span><span class="sxs-lookup"><span data-stu-id="02159-175">hello following features are available for resource level monitoring:</span></span>

### <a name="audit-log"></a><span data-ttu-id="02159-176">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="02159-176">Audit log</span></span>

<span data-ttu-id="02159-177">Hello 的網路組態的一部分執行的作業記錄。</span><span class="sxs-lookup"><span data-stu-id="02159-177">Operations performed as part of hello configuration of networks are logged.</span></span> <span data-ttu-id="02159-178">這些記錄檔可以在 hello Azure 入口網站中檢視，或使用 Microsoft 工具，例如 Power BI 或協力廠商工具來擷取。</span><span class="sxs-lookup"><span data-stu-id="02159-178">These logs can be viewed in hello Azure portal or retrieved using Microsoft tools such as Power BI or third-party tools.</span></span> <span data-ttu-id="02159-179">稽核記錄檔皆可透過 hello 入口網站、 PowerShell、 CLI 和 Rest API。</span><span class="sxs-lookup"><span data-stu-id="02159-179">Audit logs are available through hello portal, PowerShell, CLI, and Rest API.</span></span> <span data-ttu-id="02159-180">如需稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../resource-group-audit.md)</span><span class="sxs-lookup"><span data-stu-id="02159-180">For more information on Audit logs, see [Audit operations with Resource Manager](../resource-group-audit.md)</span></span>

<span data-ttu-id="02159-181">針對所有網路資源所進行的作業都會有稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="02159-181">Audit logs are available for operations done on all network resources.</span></span>

### <a name="metrics"></a><span data-ttu-id="02159-182">度量</span><span class="sxs-lookup"><span data-stu-id="02159-182">Metrics</span></span>

<span data-ttu-id="02159-183">計量是在一段時間內所收集到的效能測量數據和計數器。</span><span class="sxs-lookup"><span data-stu-id="02159-183">Metrics are performance measurements and counters collected over a period of time.</span></span> <span data-ttu-id="02159-184">計量目前適用於應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="02159-184">Metrics are currently available for Application Gateway.</span></span> <span data-ttu-id="02159-185">度量可以是使用的 tootrigger 警示臨界值為基礎。</span><span class="sxs-lookup"><span data-stu-id="02159-185">Metrics can be used tootrigger alerts based on threshold.</span></span> <span data-ttu-id="02159-186">請參閱[應用程式閘道診斷](../application-gateway/application-gateway-diagnostics.md)tooview 度量可以列印文件的是，請使用的 toocreate 警示。</span><span class="sxs-lookup"><span data-stu-id="02159-186">See [Application Gateway Diagnostics](../application-gateway/application-gateway-diagnostics.md) tooview how metrics can be used toocreate alerts.</span></span>

![計量檢視][metrics]

### <a name="diagnostic-logs"></a><span data-ttu-id="02159-188">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="02159-188">Diagnostic logs</span></span>

<span data-ttu-id="02159-189">定期和即時事件建立的網路資源，登入傳送 tooan 事件中心 」 或 「 記錄分析的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="02159-189">Periodic and spontaneous events are created by network resources and logged in storage accounts, sent tooan Event Hub, or Log Analytics.</span></span> <span data-ttu-id="02159-190">這些記錄檔提供深入了解資源的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="02159-190">These logs provide insights into hello health of a resource.</span></span> <span data-ttu-id="02159-191">您可以在 Power BI 和 Log Analytics 等工具中檢視這些記錄。</span><span class="sxs-lookup"><span data-stu-id="02159-191">These logs can be viewed in tools such as Power BI and Log Analytics.</span></span> <span data-ttu-id="02159-192">toolearn tooview 診斷記錄檔的瀏覽[記錄分析](../log-analytics/log-analytics-azure-networking-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="02159-192">toolearn how tooview diagnostic logs, visit [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>

<span data-ttu-id="02159-193">診斷記錄適用於[負載平衡器](../load-balancer/load-balancer-monitor-log.md)、[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)、路由和[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="02159-193">Diagnostic logs are available for [Load Balancer](../load-balancer/load-balancer-monitor-log.md), [Network Security Groups](../virtual-network/virtual-network-nsg-manage-log.md), Routes, and [Application Gateway](../application-gateway/application-gateway-diagnostics.md).</span></span>

<span data-ttu-id="02159-194">網路監看員提供診斷記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="02159-194">Network Watcher provides a diagnostic logs view.</span></span> <span data-ttu-id="02159-195">此檢視包含所有支援診斷記錄的網路資源。</span><span class="sxs-lookup"><span data-stu-id="02159-195">This view contains all networking resources that support diagnostic logging.</span></span> <span data-ttu-id="02159-196">從這個檢視中，您可以方便且快速地啟用和停用網路資源。</span><span class="sxs-lookup"><span data-stu-id="02159-196">From this view, you can enable and disable networking resources conveniently and quickly.</span></span>

![logs][logs]

### <a name="troubleshooting"></a><span data-ttu-id="02159-198">疑難排解</span><span class="sxs-lookup"><span data-stu-id="02159-198">Troubleshooting</span></span>

<span data-ttu-id="02159-199">hello 疑難排解刀鋒視窗中，在 hello 入口網站的經驗提供網路資源上今天 toodiagnose 個別資源相關聯的常見問題。</span><span class="sxs-lookup"><span data-stu-id="02159-199">hello troubleshooting blade, an experience in hello portal, is provided on network resources today toodiagnose common problems associated with an individual resource.</span></span> <span data-ttu-id="02159-200">使用下列的網路資源，ExpressRoute、 VPN 閘道、 應用程式閘道、 網路安全性記錄檔、 路由、 DNS、 負載平衡器和 Traffic Manager 的 hello 這項體驗。</span><span class="sxs-lookup"><span data-stu-id="02159-200">This experience is available for hello following network resources - ExpressRoute, VPN Gateway, Application Gateway, Network Security Logs, Routes, DNS, Load Balancer, and Traffic Manager.</span></span> <span data-ttu-id="02159-201">toolearn 進一步了解資源層級進行疑難排解，請瀏覽[Azure 疑難排解的診斷和解決問題](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span><span class="sxs-lookup"><span data-stu-id="02159-201">toolearn more about resource level troubleshooting, visit [Diagnose and resolve issues with Azure Troubleshooting](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span></span>

![疑難排解資訊][TS]

### <a name="resource-health"></a><span data-ttu-id="02159-203">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="02159-203">Resource health</span></span>

<span data-ttu-id="02159-204">定期執行提供的網路資源的 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="02159-204">hello health of a network resource is provided on a periodic basis.</span></span> <span data-ttu-id="02159-205">這類資源包括 VPN 閘道與 VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="02159-205">Such resources include VPN Gateway and VPN tunnel.</span></span> <span data-ttu-id="02159-206">在 hello Azure 入口網站上存取資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="02159-206">Resource health is accessible on hello Azure portal.</span></span> <span data-ttu-id="02159-207">toolearn 深入了解資源健全狀況，請瀏覽[資源健全狀況概觀](../resource-health/resource-health-overview.md)</span><span class="sxs-lookup"><span data-stu-id="02159-207">toolearn more about resource health, visit [Resource Health Overview](../resource-health/resource-health-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="02159-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02159-208">Next steps</span></span>

<span data-ttu-id="02159-209">在了解網路監看員之後，您可以接著學習︰</span><span class="sxs-lookup"><span data-stu-id="02159-209">After learning about Network Watcher, you can learn to:</span></span>

<span data-ttu-id="02159-210">請勿在您的 VM 上的封包擷取造訪[hello Azure 入口網站中的變數的封包擷取](network-watcher-packet-capture-manage-portal.md)</span><span class="sxs-lookup"><span data-stu-id="02159-210">Do a packet capture on your VM by visiting [Variable packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md)</span></span>

<span data-ttu-id="02159-211">使用[警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)執行主動監視和診斷。</span><span class="sxs-lookup"><span data-stu-id="02159-211">Perform proactive monitoring and diagnostics using [alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span></span>

<span data-ttu-id="02159-212">使用開放原始碼工具，透過[使用 Wireshark 分析封包擷取](network-watcher-deep-packet-inspection.md)來偵測安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="02159-212">Detect security vulnerabilities with [Analyzing packet capture with Wireshark](network-watcher-deep-packet-inspection.md), using open source tools.</span></span>

<span data-ttu-id="02159-213">深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。</span><span class="sxs-lookup"><span data-stu-id="02159-213">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











