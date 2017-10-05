---
title: "Azure 網路監看員中的資源疑難排解簡介 | Microsoft Docs"
description: "本頁提供網路監看員資源疑難排解功能的概觀"
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
ms.openlocfilehash: 0d5091b682d1b25c47b224394bcc2c46366eeb2a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="a655d-103">Azure 網路監看員中的資源疑難排解簡介</span><span class="sxs-lookup"><span data-stu-id="a655d-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="a655d-104">虛擬網路閘道可提供 Azure 中內部部署資源與其他虛擬網路之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a655d-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="a655d-105">監視這些閘道器及其連線，對於確保通訊不中斷至關重要。</span><span class="sxs-lookup"><span data-stu-id="a655d-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="a655d-106">網路監看員可提供針對虛擬網路閘道和連線進行疑難排解的功能。</span><span class="sxs-lookup"><span data-stu-id="a655d-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="a655d-107">此功能可透過入口網站、PowerShell、CLI 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="a655d-107">This can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a655d-108">一經呼叫，網路監看員就會診斷虛擬網路閘道或連線的健全狀況，並傳回相關結果。</span><span class="sxs-lookup"><span data-stu-id="a655d-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="a655d-109">此要求是長時間執行的交易，一旦完成診斷就會傳回結果。</span><span class="sxs-lookup"><span data-stu-id="a655d-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

![入口網站][2]

## <a name="results"></a><span data-ttu-id="a655d-111">結果</span><span class="sxs-lookup"><span data-stu-id="a655d-111">Results</span></span>

<span data-ttu-id="a655d-112">傳回的初步結果會提供資源的整體健康情況。</span><span class="sxs-lookup"><span data-stu-id="a655d-112">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="a655d-113">可以針對資源提供如下一節所示的更深入資訊︰</span><span class="sxs-lookup"><span data-stu-id="a655d-113">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="a655d-114">下列清單是透過疑難排解 API 傳回的值︰</span><span class="sxs-lookup"><span data-stu-id="a655d-114">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="a655d-115">**startTime** - 此值是疑難排解 API 呼叫的開始時間。</span><span class="sxs-lookup"><span data-stu-id="a655d-115">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="a655d-116">**endTime** - 此值是疑難排解結束時的時間。</span><span class="sxs-lookup"><span data-stu-id="a655d-116">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="a655d-117">**code** - 如果有單一診斷失敗，此值為 UnHealthy。</span><span class="sxs-lookup"><span data-stu-id="a655d-117">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="a655d-118">**results** - 結果是在連線或虛擬網路閘道上傳回的結果集合。</span><span class="sxs-lookup"><span data-stu-id="a655d-118">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="a655d-119">**id** - 此值是錯誤類型。</span><span class="sxs-lookup"><span data-stu-id="a655d-119">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="a655d-120">**summary** - 此值是錯誤摘要。</span><span class="sxs-lookup"><span data-stu-id="a655d-120">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="a655d-121">**detailed** - 此值提供錯誤的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="a655d-121">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="a655d-122">**recommendedActions** - 此屬性是建議採取的動作集合。</span><span class="sxs-lookup"><span data-stu-id="a655d-122">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="a655d-123">**actionText** - 此值包含用於描述所要採取之動作的文字。</span><span class="sxs-lookup"><span data-stu-id="a655d-123">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="a655d-124">**actionUri** - 此值提供如何採取行動的文件URI。</span><span class="sxs-lookup"><span data-stu-id="a655d-124">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="a655d-125">**actionUriText** - 此值是動作文字的簡短說明。</span><span class="sxs-lookup"><span data-stu-id="a655d-125">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="a655d-126">下表顯示可用的不同錯誤類型 (上述清單中 results 底下的 id) 以及該錯誤是否會建立記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a655d-126">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="a655d-127">閘道器</span><span class="sxs-lookup"><span data-stu-id="a655d-127">Gateway</span></span>

| <span data-ttu-id="a655d-128">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="a655d-128">Fault Type</span></span> | <span data-ttu-id="a655d-129">原因</span><span class="sxs-lookup"><span data-stu-id="a655d-129">Reason</span></span> | <span data-ttu-id="a655d-130">記錄檔</span><span class="sxs-lookup"><span data-stu-id="a655d-130">Log</span></span>|
|---|---|---|
| <span data-ttu-id="a655d-131">NoFault</span><span class="sxs-lookup"><span data-stu-id="a655d-131">NoFault</span></span> | <span data-ttu-id="a655d-132">未偵測到任何錯誤時。</span><span class="sxs-lookup"><span data-stu-id="a655d-132">When no error is detected.</span></span> |<span data-ttu-id="a655d-133">是</span><span class="sxs-lookup"><span data-stu-id="a655d-133">Yes</span></span>|
| <span data-ttu-id="a655d-134">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="a655d-134">GatewayNotFound</span></span> | <span data-ttu-id="a655d-135">找不到閘道或閘道尚未佈建。</span><span class="sxs-lookup"><span data-stu-id="a655d-135">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="a655d-136">否</span><span class="sxs-lookup"><span data-stu-id="a655d-136">No</span></span>|
| <span data-ttu-id="a655d-137">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="a655d-137">PlannedMaintenance</span></span> |  <span data-ttu-id="a655d-138">閘道執行個體正在進行維護。</span><span class="sxs-lookup"><span data-stu-id="a655d-138">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="a655d-139">否</span><span class="sxs-lookup"><span data-stu-id="a655d-139">No</span></span>|
| <span data-ttu-id="a655d-140">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="a655d-140">UserDrivenUpdate</span></span> | <span data-ttu-id="a655d-141">當正在更新使用者時。</span><span class="sxs-lookup"><span data-stu-id="a655d-141">When a user update is in progress.</span></span> <span data-ttu-id="a655d-142">這可能是調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="a655d-142">This could be a resize operation.</span></span> | <span data-ttu-id="a655d-143">否</span><span class="sxs-lookup"><span data-stu-id="a655d-143">No</span></span> |
| <span data-ttu-id="a655d-144">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="a655d-144">VipUnResponsive</span></span> | <span data-ttu-id="a655d-145">無法連線到閘道的主要執行個體。</span><span class="sxs-lookup"><span data-stu-id="a655d-145">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="a655d-146">健全狀況探查失敗時便會發生這種狀況。</span><span class="sxs-lookup"><span data-stu-id="a655d-146">This happens when the health probe fails.</span></span> | <span data-ttu-id="a655d-147">否</span><span class="sxs-lookup"><span data-stu-id="a655d-147">No</span></span> |
| <span data-ttu-id="a655d-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="a655d-148">PlatformInActive</span></span> | <span data-ttu-id="a655d-149">平台發生問題。</span><span class="sxs-lookup"><span data-stu-id="a655d-149">There is an issue with the platform.</span></span> | <span data-ttu-id="a655d-150">否</span><span class="sxs-lookup"><span data-stu-id="a655d-150">No</span></span>|
| <span data-ttu-id="a655d-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="a655d-151">ServiceNotRunning</span></span> | <span data-ttu-id="a655d-152">基礎服務並未執行。</span><span class="sxs-lookup"><span data-stu-id="a655d-152">The underlying service is not running.</span></span> | <span data-ttu-id="a655d-153">否</span><span class="sxs-lookup"><span data-stu-id="a655d-153">No</span></span>|
| <span data-ttu-id="a655d-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="a655d-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="a655d-155">閘道上沒有任何連線存在。</span><span class="sxs-lookup"><span data-stu-id="a655d-155">No Connections exists on the gateway.</span></span> <span data-ttu-id="a655d-156">這只是警告。</span><span class="sxs-lookup"><span data-stu-id="a655d-156">This is only a warning.</span></span>| <span data-ttu-id="a655d-157">否</span><span class="sxs-lookup"><span data-stu-id="a655d-157">No</span></span>|
| <span data-ttu-id="a655d-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="a655d-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="a655d-159">未建立連線。</span><span class="sxs-lookup"><span data-stu-id="a655d-159">Connections are not connected.</span></span> <span data-ttu-id="a655d-160">這只是警告。</span><span class="sxs-lookup"><span data-stu-id="a655d-160">This is only a warning.</span></span>| <span data-ttu-id="a655d-161">是</span><span class="sxs-lookup"><span data-stu-id="a655d-161">Yes</span></span>|
| <span data-ttu-id="a655d-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="a655d-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="a655d-163">目前的閘道 CPU 使用量 > 95%。</span><span class="sxs-lookup"><span data-stu-id="a655d-163">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="a655d-164">是</span><span class="sxs-lookup"><span data-stu-id="a655d-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="a655d-165">連線</span><span class="sxs-lookup"><span data-stu-id="a655d-165">Connection</span></span>

| <span data-ttu-id="a655d-166">錯誤類型</span><span class="sxs-lookup"><span data-stu-id="a655d-166">Fault Type</span></span> | <span data-ttu-id="a655d-167">原因</span><span class="sxs-lookup"><span data-stu-id="a655d-167">Reason</span></span> | <span data-ttu-id="a655d-168">記錄檔</span><span class="sxs-lookup"><span data-stu-id="a655d-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="a655d-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="a655d-169">NoFault</span></span> | <span data-ttu-id="a655d-170">未偵測到任何錯誤時。</span><span class="sxs-lookup"><span data-stu-id="a655d-170">When no error is detected.</span></span> |<span data-ttu-id="a655d-171">是</span><span class="sxs-lookup"><span data-stu-id="a655d-171">Yes</span></span>|
| <span data-ttu-id="a655d-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="a655d-172">GatewayNotFound</span></span> | <span data-ttu-id="a655d-173">找不到閘道或閘道尚未佈建。</span><span class="sxs-lookup"><span data-stu-id="a655d-173">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="a655d-174">否</span><span class="sxs-lookup"><span data-stu-id="a655d-174">No</span></span>|
| <span data-ttu-id="a655d-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="a655d-175">PlannedMaintenance</span></span> | <span data-ttu-id="a655d-176">閘道執行個體正在進行維護。</span><span class="sxs-lookup"><span data-stu-id="a655d-176">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="a655d-177">否</span><span class="sxs-lookup"><span data-stu-id="a655d-177">No</span></span>|
| <span data-ttu-id="a655d-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="a655d-178">UserDrivenUpdate</span></span> | <span data-ttu-id="a655d-179">當正在更新使用者時。</span><span class="sxs-lookup"><span data-stu-id="a655d-179">When a user update is in progress.</span></span> <span data-ttu-id="a655d-180">這可能是調整大小作業。</span><span class="sxs-lookup"><span data-stu-id="a655d-180">This could be a resize operation.</span></span>  | <span data-ttu-id="a655d-181">否</span><span class="sxs-lookup"><span data-stu-id="a655d-181">No</span></span> |
| <span data-ttu-id="a655d-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="a655d-182">VipUnResponsive</span></span> | <span data-ttu-id="a655d-183">無法連線到閘道的主要執行個體。</span><span class="sxs-lookup"><span data-stu-id="a655d-183">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="a655d-184">健全狀況探查失敗時便會發生這種狀況。</span><span class="sxs-lookup"><span data-stu-id="a655d-184">It happens when the health probe fails.</span></span> | <span data-ttu-id="a655d-185">否</span><span class="sxs-lookup"><span data-stu-id="a655d-185">No</span></span> |
| <span data-ttu-id="a655d-186">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="a655d-186">ConnectionEntityNotFound</span></span> | <span data-ttu-id="a655d-187">缺少連線組態。</span><span class="sxs-lookup"><span data-stu-id="a655d-187">Connection configuration is missing.</span></span> | <span data-ttu-id="a655d-188">否</span><span class="sxs-lookup"><span data-stu-id="a655d-188">No</span></span> |
| <span data-ttu-id="a655d-189">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="a655d-189">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="a655d-190">連線標記為「已中斷連線」。</span><span class="sxs-lookup"><span data-stu-id="a655d-190">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="a655d-191">否</span><span class="sxs-lookup"><span data-stu-id="a655d-191">No</span></span>|
| <span data-ttu-id="a655d-192">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="a655d-192">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="a655d-193">基礎服務未設定連線。</span><span class="sxs-lookup"><span data-stu-id="a655d-193">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="a655d-194">是</span><span class="sxs-lookup"><span data-stu-id="a655d-194">Yes</span></span> |
| <span data-ttu-id="a655d-195">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="a655d-195">ConnectionMarkedStandy</span></span> | <span data-ttu-id="a655d-196">基礎服務標記為「待命」。</span><span class="sxs-lookup"><span data-stu-id="a655d-196">The underlying service is marked as standby.</span></span>| <span data-ttu-id="a655d-197">是</span><span class="sxs-lookup"><span data-stu-id="a655d-197">Yes</span></span>|
| <span data-ttu-id="a655d-198">驗證</span><span class="sxs-lookup"><span data-stu-id="a655d-198">Authentication</span></span> | <span data-ttu-id="a655d-199">預先共用的金鑰不相符。</span><span class="sxs-lookup"><span data-stu-id="a655d-199">Preshared Key mismatch.</span></span> | <span data-ttu-id="a655d-200">是</span><span class="sxs-lookup"><span data-stu-id="a655d-200">Yes</span></span>|
| <span data-ttu-id="a655d-201">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="a655d-201">PeerReachability</span></span> | <span data-ttu-id="a655d-202">無法連線到對等閘道。</span><span class="sxs-lookup"><span data-stu-id="a655d-202">The peer gateway is not reachable.</span></span> | <span data-ttu-id="a655d-203">是</span><span class="sxs-lookup"><span data-stu-id="a655d-203">Yes</span></span>|
| <span data-ttu-id="a655d-204">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="a655d-204">IkePolicyMismatch</span></span> | <span data-ttu-id="a655d-205">對等閘道的 IKE 原則不受 Azure 支援。</span><span class="sxs-lookup"><span data-stu-id="a655d-205">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="a655d-206">是</span><span class="sxs-lookup"><span data-stu-id="a655d-206">Yes</span></span>|
| <span data-ttu-id="a655d-207">WfpParse 錯誤</span><span class="sxs-lookup"><span data-stu-id="a655d-207">WfpParse Error</span></span> | <span data-ttu-id="a655d-208">剖析 WFP 記錄時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a655d-208">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="a655d-209">是</span><span class="sxs-lookup"><span data-stu-id="a655d-209">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="a655d-210">支援的閘道類型</span><span class="sxs-lookup"><span data-stu-id="a655d-210">Supported Gateway types</span></span>

<span data-ttu-id="a655d-211">下列清單顯示網路監看員疑難排解所支援的閘道和連線。</span><span class="sxs-lookup"><span data-stu-id="a655d-211">The following list shows the support shows which gateways and connections are supported with Network Watcher troubleshooting.</span></span>
|  |  |
|---------|---------|
|<span data-ttu-id="a655d-212">**閘道類型**</span><span class="sxs-lookup"><span data-stu-id="a655d-212">**Gateway types**</span></span>   |         |
|<span data-ttu-id="a655d-213">VPN</span><span class="sxs-lookup"><span data-stu-id="a655d-213">VPN</span></span>      | <span data-ttu-id="a655d-214">支援</span><span class="sxs-lookup"><span data-stu-id="a655d-214">Supported</span></span>        |
|<span data-ttu-id="a655d-215">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a655d-215">ExpressRoute</span></span> | <span data-ttu-id="a655d-216">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-216">Not Supported</span></span> |
|<span data-ttu-id="a655d-217">Hypernet</span><span class="sxs-lookup"><span data-stu-id="a655d-217">Hypernet</span></span> | <span data-ttu-id="a655d-218">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-218">Not Supported</span></span>|
|<span data-ttu-id="a655d-219">**VPN 類型**</span><span class="sxs-lookup"><span data-stu-id="a655d-219">**VPN types**</span></span> | |
|<span data-ttu-id="a655d-220">路由式</span><span class="sxs-lookup"><span data-stu-id="a655d-220">Route Based</span></span> | <span data-ttu-id="a655d-221">支援</span><span class="sxs-lookup"><span data-stu-id="a655d-221">Supported</span></span>|
|<span data-ttu-id="a655d-222">原則式</span><span class="sxs-lookup"><span data-stu-id="a655d-222">Policy Based</span></span> | <span data-ttu-id="a655d-223">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-223">Not Supported</span></span>|
|<span data-ttu-id="a655d-224">**連線類型**</span><span class="sxs-lookup"><span data-stu-id="a655d-224">**Connection types**</span></span>||
|<span data-ttu-id="a655d-225">IPsec</span><span class="sxs-lookup"><span data-stu-id="a655d-225">IPSec</span></span>| <span data-ttu-id="a655d-226">支援</span><span class="sxs-lookup"><span data-stu-id="a655d-226">Supported</span></span>|
|<span data-ttu-id="a655d-227">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="a655d-227">VNet2Vnet</span></span>| <span data-ttu-id="a655d-228">支援</span><span class="sxs-lookup"><span data-stu-id="a655d-228">Supported</span></span>|
|<span data-ttu-id="a655d-229">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="a655d-229">ExpressRoute</span></span>| <span data-ttu-id="a655d-230">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-230">Not Supported</span></span>|
|<span data-ttu-id="a655d-231">Hypernet</span><span class="sxs-lookup"><span data-stu-id="a655d-231">Hypernet</span></span>| <span data-ttu-id="a655d-232">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-232">Not Supported</span></span>|
|<span data-ttu-id="a655d-233">VPNClient</span><span class="sxs-lookup"><span data-stu-id="a655d-233">VPNClient</span></span>| <span data-ttu-id="a655d-234">不支援</span><span class="sxs-lookup"><span data-stu-id="a655d-234">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="a655d-235">記錄檔</span><span class="sxs-lookup"><span data-stu-id="a655d-235">Log files</span></span>

<span data-ttu-id="a655d-236">在資源疑難排解完成之後，資源疑難排解記錄檔會儲存在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="a655d-236">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="a655d-237">下圖顯示造成錯誤的呼叫內容範例。</span><span class="sxs-lookup"><span data-stu-id="a655d-237">The following image shows the example contents of a call that resulted in an error.</span></span>

![zip 檔案][1]

> [!NOTE]
> <span data-ttu-id="a655d-239">在某些情況下，只有部分的記錄檔會寫入至儲存體。</span><span class="sxs-lookup"><span data-stu-id="a655d-239">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="a655d-240">如需從 Azure 儲存體帳戶下載檔案的指示，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="a655d-240">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a655d-241">另一項可用工具為儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="a655d-241">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a655d-242">有關儲存體總管的詳細資訊可以在下列連結找到︰[儲存體總管](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a655d-242">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="a655d-243">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="a655d-243">ConnectionStats.txt</span></span>

<span data-ttu-id="a655d-244">**ConnectionStats.txt** 檔案包含連線的整體統計資料，包括輸入和輸出位元組、連線狀態，以及連線的建立時間。</span><span class="sxs-lookup"><span data-stu-id="a655d-244">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="a655d-245">如果疑難排解 API 的呼叫傳回狀況良好，則 zip 檔案中傳回的唯一項目是 **ConnectionStats.txt** 檔案。</span><span class="sxs-lookup"><span data-stu-id="a655d-245">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="a655d-246">此檔案的內容類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="a655d-246">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="a655d-247">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="a655d-247">CPUStats.txt</span></span>

<span data-ttu-id="a655d-248">**CPUStats.txt** 檔案包含測試階段可用的 CPU 使用量與記憶體。</span><span class="sxs-lookup"><span data-stu-id="a655d-248">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="a655d-249">此檔案的內容類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="a655d-249">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="a655d-250">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="a655d-250">IKEErrors.txt</span></span>

<span data-ttu-id="a655d-251">**IKEErrors.txt** 檔案包含在監視期間找到的任何 IKE 錯誤。</span><span class="sxs-lookup"><span data-stu-id="a655d-251">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="a655d-252">下列範例顯示 IKEErrors.txt 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a655d-252">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="a655d-253">您的錯誤可能因問題而有所不同。</span><span class="sxs-lookup"><span data-stu-id="a655d-253">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="a655d-254">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="a655d-254">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="a655d-255">**Scrubbed-wfpdiag.txt** 記錄檔包含 wfp 記錄。</span><span class="sxs-lookup"><span data-stu-id="a655d-255">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="a655d-256">此記錄包含套件置放和 IKE/AuthIP 失敗的記錄。</span><span class="sxs-lookup"><span data-stu-id="a655d-256">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="a655d-257">下列範例顯示 Scrubbed-wfpdiag.txt 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a655d-257">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="a655d-258">在此範例中，連線的共用金鑰不正確 (可以從底部算起的第 3 行看出來)。</span><span class="sxs-lookup"><span data-stu-id="a655d-258">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="a655d-259">下列範例是只是整個記錄的某個片段，因為視問題而定，記錄可能很冗長。</span><span class="sxs-lookup"><span data-stu-id="a655d-259">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="a655d-260">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="a655d-260">wfpdiag.txt.sum</span></span>

<span data-ttu-id="a655d-261">**wfpdiag.txt.sum** 檔案是顯示已處理緩衝區和事件的記錄。</span><span class="sxs-lookup"><span data-stu-id="a655d-261">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="a655d-262">下列範例是 wfpdiag.txt.sum 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="a655d-262">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="a655d-263">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a655d-263">Next steps</span></span>

<span data-ttu-id="a655d-264">瀏覽[閘道疑難排解 - Azure 入口網站](network-watcher-troubleshoot-manage-portal.md)，了解如何透過入口網站診斷 VPN 閘道與連線。</span><span class="sxs-lookup"><span data-stu-id="a655d-264">Learn how to diagnose VPN Gateways and Connections through the portal by visiting [Gateway troubleshooting - Azure portal](network-watcher-troubleshoot-manage-portal.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
