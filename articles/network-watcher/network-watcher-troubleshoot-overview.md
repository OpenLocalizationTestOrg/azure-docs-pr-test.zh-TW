---
title: "疑難排解在 Azure 網路監看員 aaaIntroduction tooresource |Microsoft 文件"
description: "此頁面提供 hello 網路監看員資源疑難排解功能的概觀"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: ccbe4c1c2364473aba06e709460d67c773cf25ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooresource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="864de-103">簡介 tooresource 疑難排解在 Azure 網路監看員</span><span class="sxs-lookup"><span data-stu-id="864de-103">Introduction tooresource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="864de-104">虛擬網路閘道可提供 Azure 中內部部署資源與其他虛擬網路之間的連線。</span><span class="sxs-lookup"><span data-stu-id="864de-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="864de-105">監視這些閘道和其連線是關鍵 tooensuring 通訊並不被中斷。</span><span class="sxs-lookup"><span data-stu-id="864de-105">Monitoring these gateways and their Connections is critical tooensuring communication is not broken.</span></span> <span data-ttu-id="864de-106">網路監看員提供 hello 功能 tootroubleshoot 虛擬網路閘道與連線。</span><span class="sxs-lookup"><span data-stu-id="864de-106">Network Watcher provides hello capability tootroubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="864de-107">這可以透過 hello 入口網站、 PowerShell、 CLI 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="864de-107">This can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="864de-108">呼叫時，網路監看員診斷 hello 虛擬網路閘道或連線和 hello 傳回適當結果 hello 健全狀況。</span><span class="sxs-lookup"><span data-stu-id="864de-108">When called, Network Watcher diagnoses hello health of hello virtual network gateway or connection and return hello appropriate results.</span></span> <span data-ttu-id="864de-109">此要求是長時間執行的交易，一旦完成 hello 診斷會傳回 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="864de-109">This request is a long running transaction, hello results are returned once hello diagnosis is complete.</span></span>

![入口網站][2]

## <a name="results"></a><span data-ttu-id="864de-111">結果</span><span class="sxs-lookup"><span data-stu-id="864de-111">Results</span></span>

<span data-ttu-id="864de-112">hello 初步傳回的結果就會為 hello hello 資源健全狀況的整體概況。</span><span class="sxs-lookup"><span data-stu-id="864de-112">hello preliminary results returned give an overall picture of hello health of hello resource.</span></span> <span data-ttu-id="864de-113">Hello 之後 > 一節中所示，可以提供更深入的資訊資源：</span><span class="sxs-lookup"><span data-stu-id="864de-113">Deeper information can be provided for resources as shown in hello following section:</span></span>

<span data-ttu-id="864de-114">hello 下列清單是 hello 值傳回以 hello 疑難排解應用程式開發介面：</span><span class="sxs-lookup"><span data-stu-id="864de-114">hello following list is hello values returned with hello troubleshoot API:</span></span>

* <span data-ttu-id="864de-115">**startTime** -此值為 hello hello 疑難排解應用程式開發介面呼叫已啟動的時間。</span><span class="sxs-lookup"><span data-stu-id="864de-115">**startTime** - This value is hello time hello troubleshoot API call started.</span></span>
* <span data-ttu-id="864de-116">**endTime** -此值為 hello hello 疑難排解結束的時間。</span><span class="sxs-lookup"><span data-stu-id="864de-116">**endTime** - This value is hello time when hello troubleshooting ended.</span></span>
* <span data-ttu-id="864de-117">**code** - 如果有單一診斷失敗，此值為 UnHealthy。</span><span class="sxs-lookup"><span data-stu-id="864de-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="864de-118">**結果**-結果是 hello 連接或 hello 虛擬網路閘道上傳回結果的集合。</span><span class="sxs-lookup"><span data-stu-id="864de-118">**results** - Results is a collection of results returned on hello Connection or hello virtual network gateway.</span></span>
    * <span data-ttu-id="864de-119">**識別碼**-此值為 hello 錯誤類型。</span><span class="sxs-lookup"><span data-stu-id="864de-119">**id** - This value is hello fault type.</span></span>
    * <span data-ttu-id="864de-120">**摘要**-此值為 hello 錯誤的摘要。</span><span class="sxs-lookup"><span data-stu-id="864de-120">**summary** - This value is a summary of hello fault.</span></span>
    * <span data-ttu-id="864de-121">**詳細**-這個值會提供 hello 錯誤的詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="864de-121">**detailed** - This value provides a detailed description of hello fault.</span></span>
    * <span data-ttu-id="864de-122">**recommendedActions** -這個屬性是建議的動作 tootake 的集合。</span><span class="sxs-lookup"><span data-stu-id="864de-122">**recommendedActions** - This property is a collection of recommended actions tootake.</span></span>
      * <span data-ttu-id="864de-123">**actionText** -這個值包含描述何種動作 tootake 的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="864de-123">**actionText** - This value contains hello text describing what action tootake.</span></span>
      * <span data-ttu-id="864de-124">**actionUri** -這個值提供如何 hello URI toodocumentation tooact。</span><span class="sxs-lookup"><span data-stu-id="864de-124">**actionUri** - This value provides hello URI toodocumentation on how tooact.</span></span>
      * <span data-ttu-id="864de-125">**actionUriText** -此值為 hello 動作文字的簡短描述。</span><span class="sxs-lookup"><span data-stu-id="864de-125">**actionUriText** - This value is a short description of hello action text.</span></span>

<span data-ttu-id="864de-126">下列表格顯示 hello 不同的錯誤類型 (在從上述清單中的 hello 結果 id) 所提供的 hello 和如果 hello 錯誤就會建立記錄檔。</span><span class="sxs-lookup"><span data-stu-id="864de-126">hello following tables show hello different fault types (id under results from hello preceding list) that are available and if hello fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="864de-127">閘道器</span><span class="sxs-lookup"><span data-stu-id="864de-127">Gateway</span></span>

| <span data-ttu-id="864de-128">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="864de-128">Fault Type</span></span> | <span data-ttu-id="864de-129">原因</span><span class="sxs-lookup"><span data-stu-id="864de-129">Reason</span></span> | <span data-ttu-id="864de-130">記錄檔</span><span class="sxs-lookup"><span data-stu-id="864de-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="864de-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="864de-131">NoFault</span></span> | <span data-ttu-id="864de-132">未偵測到任何錯誤時。</span><span class="sxs-lookup"><span data-stu-id="864de-132">When no error is detected.</span></span> |<span data-ttu-id="864de-133">是</span><span class="sxs-lookup"><span data-stu-id="864de-133">Yes</span></span>|
| <span data-ttu-id="864de-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="864de-134">GatewayNotFound</span></span> | <span data-ttu-id="864de-135">找不到閘道或閘道尚未佈建。</span><span class="sxs-lookup"><span data-stu-id="864de-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="864de-136">否</span><span class="sxs-lookup"><span data-stu-id="864de-136">No</span></span>|
| <span data-ttu-id="864de-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="864de-137">PlannedMaintenance</span></span> |  <span data-ttu-id="864de-138">閘道執行個體正在進行維護。</span><span class="sxs-lookup"><span data-stu-id="864de-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="864de-139">否</span><span class="sxs-lookup"><span data-stu-id="864de-139">No</span></span>|
| <span data-ttu-id="864de-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="864de-140">UserDrivenUpdate</span></span> | <span data-ttu-id="864de-141">當正在更新使用者時。</span><span class="sxs-lookup"><span data-stu-id="864de-141">When a user update is in progress.</span></span> <span data-ttu-id="864de-142">這可能是調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="864de-142">This could be a resize operation.</span></span> | <span data-ttu-id="864de-143">否</span><span class="sxs-lookup"><span data-stu-id="864de-143">No</span></span> |
| <span data-ttu-id="864de-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="864de-144">VipUnResponsive</span></span> | <span data-ttu-id="864de-145">無法連線到 hello hello 閘道的主要執行個體。</span><span class="sxs-lookup"><span data-stu-id="864de-145">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="864de-146">這會 hello 健全狀況探查失敗。</span><span class="sxs-lookup"><span data-stu-id="864de-146">This happens when hello health probe fails.</span></span> | <span data-ttu-id="864de-147">否</span><span class="sxs-lookup"><span data-stu-id="864de-147">No</span></span> |
| <span data-ttu-id="864de-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="864de-148">PlatformInActive</span></span> | <span data-ttu-id="864de-149">沒有與 hello 平台的問題。</span><span class="sxs-lookup"><span data-stu-id="864de-149">There is an issue with hello platform.</span></span> | <span data-ttu-id="864de-150">否</span><span class="sxs-lookup"><span data-stu-id="864de-150">No</span></span>|
| <span data-ttu-id="864de-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="864de-151">ServiceNotRunning</span></span> | <span data-ttu-id="864de-152">hello 基礎服務並未執行。</span><span class="sxs-lookup"><span data-stu-id="864de-152">hello underlying service is not running.</span></span> | <span data-ttu-id="864de-153">否</span><span class="sxs-lookup"><span data-stu-id="864de-153">No</span></span>|
| <span data-ttu-id="864de-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="864de-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="864de-155">沒有連線存在 hello 閘道上。</span><span class="sxs-lookup"><span data-stu-id="864de-155">No Connections exists on hello gateway.</span></span> <span data-ttu-id="864de-156">這只是警告。</span><span class="sxs-lookup"><span data-stu-id="864de-156">This is only a warning.</span></span>| <span data-ttu-id="864de-157">否</span><span class="sxs-lookup"><span data-stu-id="864de-157">No</span></span>|
| <span data-ttu-id="864de-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="864de-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="864de-159">未建立連線。</span><span class="sxs-lookup"><span data-stu-id="864de-159">Connections are not connected.</span></span> <span data-ttu-id="864de-160">這只是警告。</span><span class="sxs-lookup"><span data-stu-id="864de-160">This is only a warning.</span></span>| <span data-ttu-id="864de-161">是</span><span class="sxs-lookup"><span data-stu-id="864de-161">Yes</span></span>|
| <span data-ttu-id="864de-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="864de-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="864de-163">hello 目前閘道器 CPU 使用量為 > 95%。</span><span class="sxs-lookup"><span data-stu-id="864de-163">hello current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="864de-164">是</span><span class="sxs-lookup"><span data-stu-id="864de-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="864de-165">連線</span><span class="sxs-lookup"><span data-stu-id="864de-165">Connection</span></span>

| <span data-ttu-id="864de-166">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="864de-166">Fault Type</span></span> | <span data-ttu-id="864de-167">原因</span><span class="sxs-lookup"><span data-stu-id="864de-167">Reason</span></span> | <span data-ttu-id="864de-168">記錄檔</span><span class="sxs-lookup"><span data-stu-id="864de-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="864de-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="864de-169">NoFault</span></span> | <span data-ttu-id="864de-170">未偵測到任何錯誤時。</span><span class="sxs-lookup"><span data-stu-id="864de-170">When no error is detected.</span></span> |<span data-ttu-id="864de-171">是</span><span class="sxs-lookup"><span data-stu-id="864de-171">Yes</span></span>|
| <span data-ttu-id="864de-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="864de-172">GatewayNotFound</span></span> | <span data-ttu-id="864de-173">找不到閘道或閘道尚未佈建。</span><span class="sxs-lookup"><span data-stu-id="864de-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="864de-174">否</span><span class="sxs-lookup"><span data-stu-id="864de-174">No</span></span>|
| <span data-ttu-id="864de-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="864de-175">PlannedMaintenance</span></span> | <span data-ttu-id="864de-176">閘道執行個體正在進行維護。</span><span class="sxs-lookup"><span data-stu-id="864de-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="864de-177">否</span><span class="sxs-lookup"><span data-stu-id="864de-177">No</span></span>|
| <span data-ttu-id="864de-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="864de-178">UserDrivenUpdate</span></span> | <span data-ttu-id="864de-179">當正在更新使用者時。</span><span class="sxs-lookup"><span data-stu-id="864de-179">When a user update is in progress.</span></span> <span data-ttu-id="864de-180">這可能是調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="864de-180">This could be a resize operation.</span></span>  | <span data-ttu-id="864de-181">否</span><span class="sxs-lookup"><span data-stu-id="864de-181">No</span></span> |
| <span data-ttu-id="864de-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="864de-182">VipUnResponsive</span></span> | <span data-ttu-id="864de-183">無法連線到 hello hello 閘道的主要執行個體。</span><span class="sxs-lookup"><span data-stu-id="864de-183">Cannot reach hello primary instance of hello Gateway.</span></span> <span data-ttu-id="864de-184">它會發生在 hello 健全狀況探查失敗。</span><span class="sxs-lookup"><span data-stu-id="864de-184">It happens when hello health probe fails.</span></span> | <span data-ttu-id="864de-185">否</span><span class="sxs-lookup"><span data-stu-id="864de-185">No</span></span> |
| <span data-ttu-id="864de-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="864de-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="864de-187">缺少連線組態。</span><span class="sxs-lookup"><span data-stu-id="864de-187">Connection configuration is missing.</span></span> | <span data-ttu-id="864de-188">否</span><span class="sxs-lookup"><span data-stu-id="864de-188">No</span></span> |
| <span data-ttu-id="864de-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="864de-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="864de-190">hello 連接會標示為 「 已中斷連線]。</span><span class="sxs-lookup"><span data-stu-id="864de-190">hello Connection is marked "disconnected".</span></span> |<span data-ttu-id="864de-191">否</span><span class="sxs-lookup"><span data-stu-id="864de-191">No</span></span>|
| <span data-ttu-id="864de-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="864de-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="864de-193">hello 基礎服務沒有設定連接的 hello。</span><span class="sxs-lookup"><span data-stu-id="864de-193">hello underlying service does not have hello Connection configured.</span></span> | <span data-ttu-id="864de-194">是</span><span class="sxs-lookup"><span data-stu-id="864de-194">Yes</span></span> |
| <span data-ttu-id="864de-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="864de-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="864de-196">基礎服務的 hello 會標示為待命。</span><span class="sxs-lookup"><span data-stu-id="864de-196">hello underlying service is marked as standby.</span></span>| <span data-ttu-id="864de-197">是</span><span class="sxs-lookup"><span data-stu-id="864de-197">Yes</span></span>|
| <span data-ttu-id="864de-198">驗證</span><span class="sxs-lookup"><span data-stu-id="864de-198">Authentication</span></span> | <span data-ttu-id="864de-199">預先共用的金鑰不相符。</span><span class="sxs-lookup"><span data-stu-id="864de-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="864de-200">是</span><span class="sxs-lookup"><span data-stu-id="864de-200">Yes</span></span>|
| <span data-ttu-id="864de-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="864de-201">PeerReachability</span></span> | <span data-ttu-id="864de-202">無法連線到 hello 對等的閘道。</span><span class="sxs-lookup"><span data-stu-id="864de-202">hello peer gateway is not reachable.</span></span> | <span data-ttu-id="864de-203">是</span><span class="sxs-lookup"><span data-stu-id="864de-203">Yes</span></span>|
| <span data-ttu-id="864de-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="864de-204">IkePolicyMismatch</span></span> | <span data-ttu-id="864de-205">hello 等閘道有 Azure 不支援的 IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="864de-205">hello peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="864de-206">是</span><span class="sxs-lookup"><span data-stu-id="864de-206">Yes</span></span>|
| <span data-ttu-id="864de-207">WfpParse 錯誤</span><span class="sxs-lookup"><span data-stu-id="864de-207">WfpParse Error</span></span> | <span data-ttu-id="864de-208">剖析 hello WFP 記錄時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="864de-208">An error occurred parsing hello WFP log.</span></span> |<span data-ttu-id="864de-209">是</span><span class="sxs-lookup"><span data-stu-id="864de-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="864de-210">支援的閘道類型</span><span class="sxs-lookup"><span data-stu-id="864de-210">Supported Gateway types</span></span>

<span data-ttu-id="864de-211">hello 下列清單顯示 hello 支援顯示支援的閘道和連接與疑難排解網路監看員。</span><span class="sxs-lookup"><span data-stu-id="864de-211">hello following list shows hello support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="864de-212">**閘道類型**</span><span class="sxs-lookup"><span data-stu-id="864de-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="864de-213">VPN</span><span class="sxs-lookup"><span data-stu-id="864de-213">VPN</span></span>      | <span data-ttu-id="864de-214">支援</span><span class="sxs-lookup"><span data-stu-id="864de-214">Supported</span></span>        |
|<span data-ttu-id="864de-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="864de-215">ExpressRoute</span></span> | <span data-ttu-id="864de-216">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-216">Not Supported</span></span> |
|<span data-ttu-id="864de-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="864de-217">Hypernet</span></span> | <span data-ttu-id="864de-218">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-218">Not Supported</span></span>|
|<span data-ttu-id="864de-219">**VPN 類型**</span><span class="sxs-lookup"><span data-stu-id="864de-219">**VPN types**</span></span> | |
|<span data-ttu-id="864de-220">路由式</span><span class="sxs-lookup"><span data-stu-id="864de-220">Route Based</span></span> | <span data-ttu-id="864de-221">支援</span><span class="sxs-lookup"><span data-stu-id="864de-221">Supported</span></span>|
|<span data-ttu-id="864de-222">原則式</span><span class="sxs-lookup"><span data-stu-id="864de-222">Policy Based</span></span> | <span data-ttu-id="864de-223">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-223">Not Supported</span></span>|
|<span data-ttu-id="864de-224">**連線類型**</span><span class="sxs-lookup"><span data-stu-id="864de-224">**Connection types**</span></span>||
|<span data-ttu-id="864de-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="864de-225">IPSec</span></span>| <span data-ttu-id="864de-226">支援</span><span class="sxs-lookup"><span data-stu-id="864de-226">Supported</span></span>|
|<span data-ttu-id="864de-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="864de-227">VNet2Vnet</span></span>| <span data-ttu-id="864de-228">支援</span><span class="sxs-lookup"><span data-stu-id="864de-228">Supported</span></span>|
|<span data-ttu-id="864de-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="864de-229">ExpressRoute</span></span>| <span data-ttu-id="864de-230">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-230">Not Supported</span></span>|
|<span data-ttu-id="864de-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="864de-231">Hypernet</span></span>| <span data-ttu-id="864de-232">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-232">Not Supported</span></span>|
|<span data-ttu-id="864de-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="864de-233">VPNClient</span></span>| <span data-ttu-id="864de-234">不支援</span><span class="sxs-lookup"><span data-stu-id="864de-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="864de-235">記錄檔</span><span class="sxs-lookup"><span data-stu-id="864de-235">Log files</span></span>

<span data-ttu-id="864de-236">hello 資源疑難排解記錄檔會儲存在儲存體帳戶中，資源疑難排解完成之後。</span><span class="sxs-lookup"><span data-stu-id="864de-236">hello resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="864de-237">hello 下列影像顯示 hello 範例內容，卻造成錯誤的呼叫。</span><span class="sxs-lookup"><span data-stu-id="864de-237">hello following image shows hello example contents of a call that resulted in an error.</span></span>

![zip 檔案][1]

> [!NOTE]
> <span data-ttu-id="864de-239">在某些情況下，只有一群 hello 記錄檔會寫入 toostorage。</span><span class="sxs-lookup"><span data-stu-id="864de-239">In some cases, only a subset of hello logs files is written toostorage.</span></span>

<span data-ttu-id="864de-240">如需從 azure 儲存體帳戶下載檔案的指示，請參閱太[開始使用適用於.NET 的 Azure Blob 儲存體使用](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="864de-240">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="864de-241">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="864de-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="864de-242">儲存體總管的詳細資訊可以在這裡找到在 hello 下列連結：[存放裝置總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="864de-242">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="864de-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="864de-243">ConnectionStats.txt</span></span>

<span data-ttu-id="864de-244">hello **ConnectionStats.txt**檔案包含的 hello 連線，包括輸入和輸出的位元組、 連線狀態，以及已建立連線的 hello 時間 hello 的整體統計資料。</span><span class="sxs-lookup"><span data-stu-id="864de-244">hello **ConnectionStats.txt** file contains overall stats of hello Connection, including ingress and egress bytes, Connection status, and hello time hello Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="864de-245">Hello hello zip 檔案中傳回的唯一疑難排解應用程式開發介面的 hello 呼叫 toohello 恢復狀況良好，如果是**ConnectionStats.txt**檔案。</span><span class="sxs-lookup"><span data-stu-id="864de-245">If hello call toohello troubleshooting API returns healthy, hello only thing returned in hello zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="864de-246">下列範例類似 toohello hello 這個檔案的內容︰</span><span class="sxs-lookup"><span data-stu-id="864de-246">hello contents of this file are similar toohello following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="864de-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="864de-247">CPUStats.txt</span></span>

<span data-ttu-id="864de-248">hello **CPUStats.txt**檔案包含 CPU 使用量，以及適用於測試的 hello 階段的記憶體。</span><span class="sxs-lookup"><span data-stu-id="864de-248">hello **CPUStats.txt** file contains CPU usage and memory available at hello time of testing.</span></span>  <span data-ttu-id="864de-249">下列範例類似 toohello 是這個檔案 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="864de-249">hello contents of this file is similar toohello following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="864de-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="864de-250">IKEErrors.txt</span></span>

<span data-ttu-id="864de-251">hello **IKEErrors.txt**檔案包含在監視期間找不到任何 IKE 錯誤。</span><span class="sxs-lookup"><span data-stu-id="864de-251">hello **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="864de-252">hello 下列範例顯示 hello IKEErrors.txt 之檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="864de-252">hello following example shows hello contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="864de-253">您的錯誤可能是根據 hello 問題而不同。</span><span class="sxs-lookup"><span data-stu-id="864de-253">Your errors may be different depending on hello issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="864de-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="864de-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="864de-255">hello **Scrubbed wfpdiag.txt**記錄檔包含 hello wfp 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="864de-255">hello **Scrubbed-wfpdiag.txt** log file contains hello wfp log.</span></span> <span data-ttu-id="864de-256">此記錄包含套件置放和 IKE/AuthIP 失敗的記錄。</span><span class="sxs-lookup"><span data-stu-id="864de-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="864de-257">hello 下列範例顯示 hello hello Scrubbed wfpdiag.txt 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="864de-257">hello following example shows hello contents of hello Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="864de-258">在此範例中，連線 hello 共用的金鑰不正確，因為從 hello 下 hello 第 3 個列所示。</span><span class="sxs-lookup"><span data-stu-id="864de-258">In this example, hello shared key of a Connection was not correct as can be seen from hello 3rd line from hello bottom.</span></span> <span data-ttu-id="864de-259">下列範例中的 hello 為 hello 記錄可能會根據 hello 問題很冗長只 hello 整個記錄檔的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="864de-259">hello following example is just a snippet of hello entire log, as hello log can be lengthy depending on hello issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from hello high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="864de-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="864de-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="864de-261">hello **wfpdiag.txt.sum**檔案是顯示 hello 緩衝區和處理的事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="864de-261">hello **wfpdiag.txt.sum** file is a log showing hello buffers and events processed.</span></span>

<span data-ttu-id="864de-262">hello 下列範例是 hello wfpdiag.txt.sum 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="864de-262">hello following example is hello contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="864de-263">後續步驟</span><span class="sxs-lookup"><span data-stu-id="864de-263">Next steps</span></span>

<span data-ttu-id="864de-264">了解如何 toodiagnose VPN 閘道和透過連線 hello 入口網站瀏覽[閘道疑難排解-Azure 入口網站](network-watcher-troubleshoot-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="864de-264">Learn how toodiagnose VPN Gateways and Connections through hello portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
