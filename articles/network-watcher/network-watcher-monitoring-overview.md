---
title: "Azure 網路監看員簡介 | Microsoft Docs"
description: "本頁概述用於監視並以視覺化方式呈現 Azure 中網路連線資源的網路監看員服務"
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
ms.openlocfilehash: 18aa9837742082535a115efd47bdc4b8dfda8a6b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-network-monitoring-overview"></a><span data-ttu-id="8c71d-103">Azure 網路監視概觀</span><span class="sxs-lookup"><span data-stu-id="8c71d-103">Azure network monitoring overview</span></span>

<span data-ttu-id="8c71d-104">客戶可藉由安排和組合各種個別的網路資源 (例如 VNet、ExpressRoute、應用程式閘道、負載平衡器等等)，在 Azure 中建置端對端網路。</span><span class="sxs-lookup"><span data-stu-id="8c71d-104">Customers build an end-to-end network in Azure by orchestrating and composing various individual network resources such as VNet, ExpressRoute, Application Gateway, Load balancers, and more.</span></span> <span data-ttu-id="8c71d-105">每個網路資源都可進行監視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-105">Monitoring is available on each of the network resources.</span></span> <span data-ttu-id="8c71d-106">我們將這種監視稱為資源層級監視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-106">We refer to this monitoring as resource level monitoring.</span></span>

<span data-ttu-id="8c71d-107">端對端網路可能會有複雜的組態和資源互動，而產生需要透過網路監看員來進行案例式監視的複雜案例。</span><span class="sxs-lookup"><span data-stu-id="8c71d-107">The end to end network can have complex configurations and interactions between resources, creating complex scenarios that need scenario-based monitoring through Network Watcher.</span></span>

<span data-ttu-id="8c71d-108">本文將探討案例和資源層級的監視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-108">This article covers scenario and resource level monitoring.</span></span> <span data-ttu-id="8c71d-109">Azure 中的網路監視功能相當完善，主要涵蓋類別有二種︰</span><span class="sxs-lookup"><span data-stu-id="8c71d-109">Network monitoring in Azure is comprehensive and covers two broad categories:</span></span>

* <span data-ttu-id="8c71d-110">[**網路監看員**](#network-watcher) - 網路監看員的功能隨附了案例式監視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-110">[**Network Watcher**](#network-watcher) - Scenario-based monitoring is provided with the features in Network Watcher.</span></span> <span data-ttu-id="8c71d-111">這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。</span><span class="sxs-lookup"><span data-stu-id="8c71d-111">This service includes packet capture, next hop, IP flow verify, security group view, NSG flow logs.</span></span> <span data-ttu-id="8c71d-112">案例層級監視可提供端對端的網路資源檢視，而非個別的網路資源監視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-112">Scenario level monitoring provides an end to end view of network resources in contrast to individual network resource monitoring.</span></span>
* <span data-ttu-id="8c71d-113">[**資源監視**](#network-resource-level-monitoring) - 資源層級監視由診斷記錄、計量、疑難排解和資源健全狀況這四個功能所組成。</span><span class="sxs-lookup"><span data-stu-id="8c71d-113">[**Resource monitoring**](#network-resource-level-monitoring) - Resource level monitoring comprises of four features, diagnostic logs, metrics, troubleshooting, and resource health.</span></span> <span data-ttu-id="8c71d-114">這些功能全是建置在網路資源層級。</span><span class="sxs-lookup"><span data-stu-id="8c71d-114">All these features are built at the network resource level.</span></span>

## <a name="network-watcher"></a><span data-ttu-id="8c71d-115">網路監看員</span><span class="sxs-lookup"><span data-stu-id="8c71d-115">Network Watcher</span></span>

<span data-ttu-id="8c71d-116">網路監看員是一項區域性服務，可讓您監視與診斷位於和進出 Azure 的網路案例層級條件。</span><span class="sxs-lookup"><span data-stu-id="8c71d-116">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="8c71d-117">網路監看員提供的網路診斷和視覺效果工具，可幫助您了解、診斷及洞悉您在 Azure 中的網路。</span><span class="sxs-lookup"><span data-stu-id="8c71d-117">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

<span data-ttu-id="8c71d-118">網路監看員目前具有下列功能︰</span><span class="sxs-lookup"><span data-stu-id="8c71d-118">Network Watcher currently has the following capabilities:</span></span>

* <span data-ttu-id="8c71d-119">**[拓撲](network-watcher-topology-overview.md)** - 提供網路層級檢視，顯示資源群組中的網路資源之間的各種相互連線和關聯。</span><span class="sxs-lookup"><span data-stu-id="8c71d-119">**[Topology](network-watcher-topology-overview.md)** - Provides a network level view showing the various interconnections and associations between network resources in a resource group.</span></span>
* <span data-ttu-id="8c71d-120">**[變動的封包擷取](network-watcher-packet-capture-overview.md)** - 擷取進出虛擬機器的封包資料。</span><span class="sxs-lookup"><span data-stu-id="8c71d-120">**[Variable Packet capture](network-watcher-packet-capture-overview.md)** - Captures packet data in and out of a virtual machine.</span></span> <span data-ttu-id="8c71d-121">進階篩選選項和微調控制項 (例如能夠設定時間和大小限制) 可讓您靈活擷取資料。</span><span class="sxs-lookup"><span data-stu-id="8c71d-121">Advanced filtering options and fine-tuned controls such as being able to set time and size limitations provide versatility.</span></span> <span data-ttu-id="8c71d-122">封包資料可以 .cap 格式儲存在 Blob 存放區或本機磁碟上。</span><span class="sxs-lookup"><span data-stu-id="8c71d-122">The packet data can be stored in a blob store or on the local disk in .cap format.</span></span>
* <span data-ttu-id="8c71d-123">**[IP 流量驗證](network-watcher-ip-flow-verify-overview.md)** - 根據流量資訊 5-tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 檢查是否允許或拒絕封包。</span><span class="sxs-lookup"><span data-stu-id="8c71d-123">**[IP flow verify](network-watcher-ip-flow-verify-overview.md)** - Checks if a packet is allowed or denied based on flow information 5-tuple packet parameters (Destination IP, Source IP, Destination Port, Source Port, and Protocol).</span></span> <span data-ttu-id="8c71d-124">如果封包遭到安全性群組拒絕，則會傳回拒絕封包的規則和群組。</span><span class="sxs-lookup"><span data-stu-id="8c71d-124">If the packet is denied by a security group, the rule and group that denied the packet is returned.</span></span>
* <span data-ttu-id="8c71d-125">**[下一個躍點](network-watcher-next-hop-overview.md)** - 決定在 Azure 網路網狀架構中路由傳送之封包的下一個躍點，讓您得以診斷任何設定錯誤的使用者定義路由。</span><span class="sxs-lookup"><span data-stu-id="8c71d-125">**[Next hop](network-watcher-next-hop-overview.md)** - Determines the next hop for packets being routed in the Azure Network Fabric, enabling you to diagnose any misconfigured user-defined routes.</span></span>
* <span data-ttu-id="8c71d-126">**[安全性群組檢視](network-watcher-security-group-view-overview.md)** - 取得套用至 VM 的有效和已套用安全性規則。</span><span class="sxs-lookup"><span data-stu-id="8c71d-126">**[Security group view](network-watcher-security-group-view-overview.md)** - Gets the effective and applied security rules that are applied on a VM.</span></span>
* <span data-ttu-id="8c71d-127">**[NSG 流量記錄](network-watcher-nsg-flow-logging-overview.md)** - 網路安全性群組的流量記錄可讓您擷取群組中的安全性規則所允許或拒絕之流量的相關記錄。</span><span class="sxs-lookup"><span data-stu-id="8c71d-127">**[NSG Flow logging](network-watcher-nsg-flow-logging-overview.md)** - Flow logs for Network Security Groups enable you to capture logs related to traffic that are allowed or denied by the security rules in the group.</span></span> <span data-ttu-id="8c71d-128">流量是由 5-tuple 資訊加以定義，這些資訊分別是來源 IP、目的地 IP、來源連接埠、目的地連接埠和通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8c71d-128">The flow is defined by a 5-tuple information – Source IP, Destination IP, Source Port, Destination Port and Protocol.</span></span>
* <span data-ttu-id="8c71d-129">**[虛擬網路閘道和連線疑難排解](network-watcher-troubleshoot-manage-rest.md)** - 提供針對虛擬網路閘道和連線進行疑難排解的能力。</span><span class="sxs-lookup"><span data-stu-id="8c71d-129">**[Virtual Network Gateway and Connection troubleshooting](network-watcher-troubleshoot-manage-rest.md)** - Provides the ability to troubleshoot Virtual Network Gateways and Connections.</span></span>
* <span data-ttu-id="8c71d-130">**[網路訂用帳戶限制](#network-subscription-limits)** - 可讓您檢視網路資源使用量與限制。</span><span class="sxs-lookup"><span data-stu-id="8c71d-130">**[Network subscription limits](#network-subscription-limits)** - Enables you to view network resource usage against limits.</span></span>
* <span data-ttu-id="8c71d-131">**[設定診斷記錄](#diagnostic-logs)** - 提供單一窗格以供啟用或停用資源群組中網路資源的診斷記錄。</span><span class="sxs-lookup"><span data-stu-id="8c71d-131">**[Configuring Diagnostics Log](#diagnostic-logs)** – Provides a single pane to enable or disable Diagnostics logs for network resources in a resource group.</span></span>
* <span data-ttu-id="8c71d-132">**[連線 (預覽)](network-watcher-connectivity-overview.md)** - 確認是否可以建立從虛擬機器到指定端點的直接 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="8c71d-132">**[Connectivity (Preview)](network-watcher-connectivity-overview.md)** - Verifies the possibility of establishing a direct TCP connection from a virtual machine to a given endpoint.</span></span>

### <a name="role-based-access-control-rbac-in-network-watcher"></a><span data-ttu-id="8c71d-133">網路監看員的角色型存取控制 (RBAC)</span><span class="sxs-lookup"><span data-stu-id="8c71d-133">Role-based Access Control (RBAC) in Network Watcher</span></span>

<span data-ttu-id="8c71d-134">網路監看員使用 [Azure 角色型存取控制 (RBAC) 模型](../active-directory/role-based-access-control-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="8c71d-134">Network watcher uses the [Azure Role-Based Access Control (RBAC) model](../active-directory/role-based-access-control-what-is.md).</span></span> <span data-ttu-id="8c71d-135">網路監看員需要下列權限。</span><span class="sxs-lookup"><span data-stu-id="8c71d-135">The following permissions are required by the Network Watcher.</span></span> <span data-ttu-id="8c71d-136">請務必確定用來起始網路監看員 API 或從入口網站使用網路監看員的角色具有所需存取權。</span><span class="sxs-lookup"><span data-stu-id="8c71d-136">It is important to make sure that the role used for initiating Network Watcher APIs or using Network Watcher from the portal has the required access.</span></span>

|<span data-ttu-id="8c71d-137">資源</span><span class="sxs-lookup"><span data-stu-id="8c71d-137">Resource</span></span>| <span data-ttu-id="8c71d-138">權限</span><span class="sxs-lookup"><span data-stu-id="8c71d-138">Permission</span></span>|
|---|---| 
|<span data-ttu-id="8c71d-139">Microsoft.Storage/</span><span class="sxs-lookup"><span data-stu-id="8c71d-139">Microsoft.Storage/</span></span> |<span data-ttu-id="8c71d-140">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-140">Read</span></span>|
|<span data-ttu-id="8c71d-141">Microsoft.Authorization/</span><span class="sxs-lookup"><span data-stu-id="8c71d-141">Microsoft.Authorization/</span></span>| <span data-ttu-id="8c71d-142">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-142">Read</span></span>| 
|<span data-ttu-id="8c71d-143">Microsoft.Resources/subscriptions/resourceGroups/</span><span class="sxs-lookup"><span data-stu-id="8c71d-143">Microsoft.Resources/subscriptions/resourceGroups/</span></span>| <span data-ttu-id="8c71d-144">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-144">Read</span></span>|
|<span data-ttu-id="8c71d-145">Microsoft.Storage/storageAccounts/listServiceSas/</span><span class="sxs-lookup"><span data-stu-id="8c71d-145">Microsoft.Storage/storageAccounts/listServiceSas/</span></span> | <span data-ttu-id="8c71d-146">動作</span><span class="sxs-lookup"><span data-stu-id="8c71d-146">Action</span></span>|
|<span data-ttu-id="8c71d-147">Microsoft.Storage/storageAccounts/listAccountSas/</span><span class="sxs-lookup"><span data-stu-id="8c71d-147">Microsoft.Storage/storageAccounts/listAccountSas/</span></span> |<span data-ttu-id="8c71d-148">動作</span><span class="sxs-lookup"><span data-stu-id="8c71d-148">Action</span></span>|
|<span data-ttu-id="8c71d-149">Microsoft.Storage/storageAccounts/listKeys/</span><span class="sxs-lookup"><span data-stu-id="8c71d-149">Microsoft.Storage/storageAccounts/listKeys/</span></span> | <span data-ttu-id="8c71d-150">動作</span><span class="sxs-lookup"><span data-stu-id="8c71d-150">Action</span></span>|
|<span data-ttu-id="8c71d-151">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="8c71d-151">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="8c71d-152">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-152">Read</span></span>|
|<span data-ttu-id="8c71d-153">Microsoft.Compute/virtualMachines/</span><span class="sxs-lookup"><span data-stu-id="8c71d-153">Microsoft.Compute/virtualMachines/</span></span> |<span data-ttu-id="8c71d-154">寫入</span><span class="sxs-lookup"><span data-stu-id="8c71d-154">Write</span></span>|
|<span data-ttu-id="8c71d-155">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="8c71d-155">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="8c71d-156">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-156">Read</span></span>|
|<span data-ttu-id="8c71d-157">Microsoft.Compute/virtualMachineScaleSets/</span><span class="sxs-lookup"><span data-stu-id="8c71d-157">Microsoft.Compute/virtualMachineScaleSets/</span></span> |<span data-ttu-id="8c71d-158">寫入</span><span class="sxs-lookup"><span data-stu-id="8c71d-158">Write</span></span>|
|<span data-ttu-id="8c71d-159">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="8c71d-159">Microsoft.Network/networkWatchers/packetCaptures/</span></span> |<span data-ttu-id="8c71d-160">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-160">Read</span></span>|
|<span data-ttu-id="8c71d-161">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="8c71d-161">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="8c71d-162">寫入</span><span class="sxs-lookup"><span data-stu-id="8c71d-162">Write</span></span>|
|<span data-ttu-id="8c71d-163">Microsoft.Network/networkWatchers/packetCaptures/</span><span class="sxs-lookup"><span data-stu-id="8c71d-163">Microsoft.Network/networkWatchers/packetCaptures/</span></span>| <span data-ttu-id="8c71d-164">刪除</span><span class="sxs-lookup"><span data-stu-id="8c71d-164">Delete</span></span>|
|<span data-ttu-id="8c71d-165">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="8c71d-165">Microsoft.Network/networkWatchers/</span></span> |<span data-ttu-id="8c71d-166">寫入</span><span class="sxs-lookup"><span data-stu-id="8c71d-166">Write</span></span> |
|<span data-ttu-id="8c71d-167">Microsoft.Network/networkWatchers/</span><span class="sxs-lookup"><span data-stu-id="8c71d-167">Microsoft.Network/networkWatchers/</span></span>| <span data-ttu-id="8c71d-168">讀取</span><span class="sxs-lookup"><span data-stu-id="8c71d-168">Read</span></span> |
|<span data-ttu-id="8c71d-169">Microsoft.Insights/alertRules/</span><span class="sxs-lookup"><span data-stu-id="8c71d-169">Microsoft.Insights/alertRules/</span></span> |*|
|<span data-ttu-id="8c71d-170">Microsoft.Support/</span><span class="sxs-lookup"><span data-stu-id="8c71d-170">Microsoft.Support/</span></span> | *|

### <a name="network-subscription-limits"></a><span data-ttu-id="8c71d-171">網路訂用帳戶限制</span><span class="sxs-lookup"><span data-stu-id="8c71d-171">Network subscription limits</span></span>

<span data-ttu-id="8c71d-172">網路訂用帳戶限制可為您提供區域中，訂用帳戶的每個網路資源使用量詳細資料與可用資源數上限的對照情況。</span><span class="sxs-lookup"><span data-stu-id="8c71d-172">Network subscription limits provide you with details of the usage of each of the network resource in a subscription in a region against the maximum number of resources available.</span></span>

![網路訂用帳戶限制][nsl]

## <a name="network-resource-level-monitoring"></a><span data-ttu-id="8c71d-174">網路資源層級監視</span><span class="sxs-lookup"><span data-stu-id="8c71d-174">Network resource level monitoring</span></span>

<span data-ttu-id="8c71d-175">資源層級監視可使用下列功能︰</span><span class="sxs-lookup"><span data-stu-id="8c71d-175">The following features are available for resource level monitoring:</span></span>

### <a name="audit-log"></a><span data-ttu-id="8c71d-176">稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="8c71d-176">Audit log</span></span>

<span data-ttu-id="8c71d-177">做為網路組態一部分所執行的作業會記錄下來。</span><span class="sxs-lookup"><span data-stu-id="8c71d-177">Operations performed as part of the configuration of networks are logged.</span></span> <span data-ttu-id="8c71d-178">這些記錄可在 Azure 入口網站中檢視，或使用 Power BI 之類的 Microsoft 工具或協力廠商工具來擷取。</span><span class="sxs-lookup"><span data-stu-id="8c71d-178">These logs can be viewed in the Azure portal or retrieved using Microsoft tools such as Power BI or third-party tools.</span></span> <span data-ttu-id="8c71d-179">稽核記錄可透過入口網站、PowerShell、CLI 和 Rest API 來取得。</span><span class="sxs-lookup"><span data-stu-id="8c71d-179">Audit logs are available through the portal, PowerShell, CLI, and Rest API.</span></span> <span data-ttu-id="8c71d-180">如需稽核記錄的詳細資訊，請參閱[使用 Resource Manager 來稽核作業](../resource-group-audit.md)</span><span class="sxs-lookup"><span data-stu-id="8c71d-180">For more information on Audit logs, see [Audit operations with Resource Manager](../resource-group-audit.md)</span></span>

<span data-ttu-id="8c71d-181">針對所有網路資源所進行的作業都會有稽核記錄。</span><span class="sxs-lookup"><span data-stu-id="8c71d-181">Audit logs are available for operations done on all network resources.</span></span>

### <a name="metrics"></a><span data-ttu-id="8c71d-182">度量</span><span class="sxs-lookup"><span data-stu-id="8c71d-182">Metrics</span></span>

<span data-ttu-id="8c71d-183">計量是在一段時間內所收集到的效能測量數據和計數器。</span><span class="sxs-lookup"><span data-stu-id="8c71d-183">Metrics are performance measurements and counters collected over a period of time.</span></span> <span data-ttu-id="8c71d-184">計量目前適用於應用程式閘道。</span><span class="sxs-lookup"><span data-stu-id="8c71d-184">Metrics are currently available for Application Gateway.</span></span> <span data-ttu-id="8c71d-185">計量可用來根據臨界值觸發警示。</span><span class="sxs-lookup"><span data-stu-id="8c71d-185">Metrics can be used to trigger alerts based on threshold.</span></span> <span data-ttu-id="8c71d-186">請參閱[應用程式閘道診斷](../application-gateway/application-gateway-diagnostics.md)，以檢視如何使用計量來建立警示。</span><span class="sxs-lookup"><span data-stu-id="8c71d-186">See [Application Gateway Diagnostics](../application-gateway/application-gateway-diagnostics.md) to view how metrics can be used to create alerts.</span></span>

![計量檢視][metrics]

### <a name="diagnostic-logs"></a><span data-ttu-id="8c71d-188">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="8c71d-188">Diagnostic logs</span></span>

<span data-ttu-id="8c71d-189">網路資源會定期和自發地建立事件，並記錄到儲存體帳戶、傳送到事件中樞或 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c71d-189">Periodic and spontaneous events are created by network resources and logged in storage accounts, sent to an Event Hub, or Log Analytics.</span></span> <span data-ttu-id="8c71d-190">這些記錄可讓您深入了解資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="8c71d-190">These logs provide insights into the health of a resource.</span></span> <span data-ttu-id="8c71d-191">您可以在 Power BI 和 Log Analytics 等工具中檢視這些記錄。</span><span class="sxs-lookup"><span data-stu-id="8c71d-191">These logs can be viewed in tools such as Power BI and Log Analytics.</span></span> <span data-ttu-id="8c71d-192">若要了解如何檢視診斷記錄，請瀏覽 [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="8c71d-192">To learn how to view diagnostic logs, visit [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).</span></span>

<span data-ttu-id="8c71d-193">診斷記錄適用於[負載平衡器](../load-balancer/load-balancer-monitor-log.md)、[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)、路由和[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)。</span><span class="sxs-lookup"><span data-stu-id="8c71d-193">Diagnostic logs are available for [Load Balancer](../load-balancer/load-balancer-monitor-log.md), [Network Security Groups](../virtual-network/virtual-network-nsg-manage-log.md), Routes, and [Application Gateway](../application-gateway/application-gateway-diagnostics.md).</span></span>

<span data-ttu-id="8c71d-194">網路監看員提供診斷記錄檢視。</span><span class="sxs-lookup"><span data-stu-id="8c71d-194">Network Watcher provides a diagnostic logs view.</span></span> <span data-ttu-id="8c71d-195">此檢視包含所有支援診斷記錄的網路資源。</span><span class="sxs-lookup"><span data-stu-id="8c71d-195">This view contains all networking resources that support diagnostic logging.</span></span> <span data-ttu-id="8c71d-196">從這個檢視中，您可以方便且快速地啟用和停用網路資源。</span><span class="sxs-lookup"><span data-stu-id="8c71d-196">From this view, you can enable and disable networking resources conveniently and quickly.</span></span>

![logs][logs]

### <a name="troubleshooting"></a><span data-ttu-id="8c71d-198">疑難排解</span><span class="sxs-lookup"><span data-stu-id="8c71d-198">Troubleshooting</span></span>

<span data-ttu-id="8c71d-199">網路資源現已提供 [疑難排解] 刀鋒視窗，這項入口網站體驗可診斷與個別資源相關聯的常見問題。</span><span class="sxs-lookup"><span data-stu-id="8c71d-199">The troubleshooting blade, an experience in the portal, is provided on network resources today to diagnose common problems associated with an individual resource.</span></span> <span data-ttu-id="8c71d-200">這項體驗適用於下列網路資源：ExpressRoute、VPN 閘道、應用程式閘道、網路安全性記錄、路由、DNS、負載平衡器和流量管理員。</span><span class="sxs-lookup"><span data-stu-id="8c71d-200">This experience is available for the following network resources - ExpressRoute, VPN Gateway, Application Gateway, Network Security Logs, Routes, DNS, Load Balancer, and Traffic Manager.</span></span> <span data-ttu-id="8c71d-201">若要深入了解資源層級的疑難排解，請瀏覽[使用 Azure 疑難排解來診斷和解決問題](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span><span class="sxs-lookup"><span data-stu-id="8c71d-201">To learn more about resource level troubleshooting, visit [Diagnose and resolve issues with Azure Troubleshooting](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)</span></span>

![疑難排解資訊][TS]

### <a name="resource-health"></a><span data-ttu-id="8c71d-203">資源健康情況</span><span class="sxs-lookup"><span data-stu-id="8c71d-203">Resource health</span></span>

<span data-ttu-id="8c71d-204">系統會定期提供網路資源的健康情況。</span><span class="sxs-lookup"><span data-stu-id="8c71d-204">The health of a network resource is provided on a periodic basis.</span></span> <span data-ttu-id="8c71d-205">這類資源包括 VPN 閘道與 VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="8c71d-205">Such resources include VPN Gateway and VPN tunnel.</span></span> <span data-ttu-id="8c71d-206">資源健全狀況可在 Azure 入口網站上取得。</span><span class="sxs-lookup"><span data-stu-id="8c71d-206">Resource health is accessible on the Azure portal.</span></span> <span data-ttu-id="8c71d-207">若要深入了解資源健全狀況，請瀏覽[資源健全狀況概觀](../resource-health/resource-health-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8c71d-207">To learn more about resource health, visit [Resource Health Overview](../resource-health/resource-health-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c71d-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c71d-208">Next steps</span></span>

<span data-ttu-id="8c71d-209">在了解網路監看員之後，您可以接著學習︰</span><span class="sxs-lookup"><span data-stu-id="8c71d-209">After learning about Network Watcher, you can learn to:</span></span>

<span data-ttu-id="8c71d-210">在 VM 上執行封包擷取，請瀏覽 [Azure 入口網站中的變動封包擷取](network-watcher-packet-capture-manage-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8c71d-210">Do a packet capture on your VM by visiting [Variable packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md)</span></span>

<span data-ttu-id="8c71d-211">使用[警示觸發的封包擷取](network-watcher-alert-triggered-packet-capture.md)執行主動監視和診斷。</span><span class="sxs-lookup"><span data-stu-id="8c71d-211">Perform proactive monitoring and diagnostics using [alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md).</span></span>

<span data-ttu-id="8c71d-212">使用開放原始碼工具，透過[使用 Wireshark 分析封包擷取](network-watcher-deep-packet-inspection.md)來偵測安全性弱點。</span><span class="sxs-lookup"><span data-stu-id="8c71d-212">Detect security vulnerabilities with [Analyzing packet capture with Wireshark](network-watcher-deep-packet-inspection.md), using open source tools.</span></span>

<span data-ttu-id="8c71d-213">了解 Azure 的一些其他重要[網路功能](../networking/networking-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8c71d-213">Learn about some of the other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











