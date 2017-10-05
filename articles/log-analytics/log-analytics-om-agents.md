---
title: "將 Operations Manager 連接到 Log Analytics | Microsoft Docs"
description: "若要維護 System Center Operations Manager 中的現有投資，並使用 Log Analytics 的延伸功能，您可以整合 Operations Manager 與 OMS 工作區。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: bcfffe05dbce2824ea4933997865e8c7e86610b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-operations-manager-to-log-analytics"></a><span data-ttu-id="cdb06-103">將 Operations Manager 連接到 Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cdb06-103">Connect Operations Manager to Log Analytics</span></span>
<span data-ttu-id="cdb06-104">若要維護 System Center Operations Manager 中的現有投資，並使用 Log Analytics 的延伸功能，您可以整合 Operations Manager 與 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-104">To maintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.</span></span>  <span data-ttu-id="cdb06-105">這可讓您利用 OMS 的機會，同時繼續使用 Operations Manager：</span><span class="sxs-lookup"><span data-stu-id="cdb06-105">This allows you leverage the opportunities of OMS while continuing to use Operations Manager to:</span></span>

* <span data-ttu-id="cdb06-106">使用 Operations Manager 繼續監視 IT 服務的健全狀況</span><span class="sxs-lookup"><span data-stu-id="cdb06-106">Continue monitoring the health of your IT services with Operations Manager</span></span>
* <span data-ttu-id="cdb06-107">維護與支援事件和問題管理之 ITSM 解決方案的整合</span><span class="sxs-lookup"><span data-stu-id="cdb06-107">Maintain integration with your ITSM solutions supporting incident and problem management</span></span>
* <span data-ttu-id="cdb06-108">管理代理程式的生命週期，這些代理程式部署到內部部署以及您使用 Operations Manager 所監視的公用雲端 IaaS 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="cdb06-108">Manage the lifecycle of agents deployed to on-premises and public cloud IaaS virtual machines that you monitor with Operations Manager</span></span>

<span data-ttu-id="cdb06-109">與 System Center Operations Manager 整合後，從 Operations Manager 收集、儲存和分析資料時可發揮 OMS 速度和效率，提高服務作業策略的價值。</span><span class="sxs-lookup"><span data-stu-id="cdb06-109">Integrating with System Center Operations Manager adds value to your service operations strategy by using the speed and efficiency of OMS in collecting, storing, and analyzing data from Operations Manager.</span></span>  <span data-ttu-id="cdb06-110">OMS 有助於找出問題的關聯性，並努力查明原因和杜絕再次發生，以支援現有的問題管理程序。</span><span class="sxs-lookup"><span data-stu-id="cdb06-110">OMS helps correlate and work towards identifying the faults of problems and surfacing recurrences in support of your existing problem management process.</span></span>   <span data-ttu-id="cdb06-111">檢查效能、事件和警示資料的搜尋引擎的彈性 (具有豐富的儀表板和報告功能可透過有意義的方式公開此資料) 示範 OMS 對值得讚揚的 Operations Manager 的強度。</span><span class="sxs-lookup"><span data-stu-id="cdb06-111">The flexibility of the search engine to examine performance, event and alert data, with rich dashboards and reporting capabilities to expose this data in meaningful ways, demonstrates the strength OMS brings in complimenting Operations Manager.</span></span>

<span data-ttu-id="cdb06-112">向 Operations Manager 管理群組回報的代理程式，會根據已在 OMS 訂用帳戶中啟用的 Log Analytics 資料來源和解決方案以從您的伺服器收集資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-112">The agents reporting to the Operations Manager management group collect data from your servers based on the Log Analytics data sources and solutions you have enabled in your OMS subscription.</span></span>  <span data-ttu-id="cdb06-113">根據已啟用的解決方案，這些解決方案中的資料會從 Operations Manager 管理伺服器直接傳送給 OMS Web 服務，或者，因為代理程式所管理系統上收集的資料量，所以這些解決方案中的資料會從代理程式直接傳送給 OMS Web 服務。</span><span class="sxs-lookup"><span data-stu-id="cdb06-113">Depending on the solution you have enabled, data from these solutions are either sent directly from an Operations Manager management server to the OMS web service, or because of the volume of data collected on the agent-managed system, are sent directly from the agent to OMS web service.</span></span> <span data-ttu-id="cdb06-114">管理伺服器會直接將 OMS 資料轉送到 OMS Web 服務，永遠不會寫入 OperationsManager 或 OperationsManagerDW 資料庫。</span><span class="sxs-lookup"><span data-stu-id="cdb06-114">The management server forwards the OMS data directly to the OMS web service; it is never written to the OperationsManager or OperationsManagerDW database.</span></span>  <span data-ttu-id="cdb06-115">如果管理伺服器中斷與 OMS Web 服務的連接，則會在重新建立與 OMS 的通訊之前，將資料快取在本機。</span><span class="sxs-lookup"><span data-stu-id="cdb06-115">When a management server loses connectivity with the OMS web service, it caches the data locally until communication is re-established with OMS.</span></span>  <span data-ttu-id="cdb06-116">如果管理伺服器因發生規劃的維護或未規劃的中斷而離線，管理群組中的另一部管理伺服器會繼續與 OMS 連線。</span><span class="sxs-lookup"><span data-stu-id="cdb06-116">If the management server is offline due to planned maintenance or unplanned outage, another management server in the management group resumes connectivity with OMS.</span></span>  

<span data-ttu-id="cdb06-117">下圖描述管理伺服器與 System Center Operations Manager 管理群組中的代理程式和 OMS 之間的連接，包括方向和連接埠。</span><span class="sxs-lookup"><span data-stu-id="cdb06-117">The following diagram depicts the connection between the management servers and agents in a System Center Operations Manager management group and OMS, including the direction and ports.</span></span>   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

<span data-ttu-id="cdb06-119">如果 IT 安全性原則不允許您網路上的電腦連線到網際網路，則可以將管理伺服器設定為連線到 OMS 閘道，以根據您已啟用的解決方案來接收組態資訊和傳送收集到的資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-119">If your IT security policies do not allow computers on your network to connect to the Internet, management servers can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span>  <span data-ttu-id="cdb06-120">如需如何設定 Operations Manager 管理群組以透過 OMS 閘道與 OMS 服務進行通訊的其他資訊和步驟，請參閱[使用 OMS 閘道將電腦連線到 OMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="cdb06-120">For more information and steps on how to configure your Operations Manager management group to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

## <a name="system-requirements"></a><span data-ttu-id="cdb06-121">系統需求</span><span class="sxs-lookup"><span data-stu-id="cdb06-121">System requirements</span></span>
<span data-ttu-id="cdb06-122">開始之前，請檢閱下列詳細資料，以確認符合必要條件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-122">Before starting, review the following details to verify you meet prerequisites.</span></span>

* <span data-ttu-id="cdb06-123">OMS 僅支援 Operations Manager 2016、Operations Manager 2012 SP1 UR6 和更新版本，以及 Operations Manager 2012 R2 UR2 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="cdb06-123">OMS only supports Operations Manager 2016, Operations Manager 2012 SP1 UR6 and greater, and Operations Manager 2012 R2 UR2 and greater.</span></span>  <span data-ttu-id="cdb06-124">Operations Manager 2012 SP1 UR7 和 Operations Manager 2012 R2 UR3 中已加入 Proxy 支援。</span><span class="sxs-lookup"><span data-stu-id="cdb06-124">Proxy support was added in Operations Manager 2012 SP1 UR7 and Operations Manager 2012 R2 UR3.</span></span>
* <span data-ttu-id="cdb06-125">所有 Operations Manager 代理程式必須符合最低支援需求。</span><span class="sxs-lookup"><span data-stu-id="cdb06-125">All Operations Manager agents must meet minimum support requirements.</span></span> <span data-ttu-id="cdb06-126">請確定代理程式已安裝最低更新版本，否則 Windows 代理程式流量會失敗，許多錯誤可能會填滿 Operations Manager 事件記錄。</span><span class="sxs-lookup"><span data-stu-id="cdb06-126">Ensure that agents are at the minimum update, otherwise Windows agent traffic may fail and many errors might fill the Operations Manager event log.</span></span>
* <span data-ttu-id="cdb06-127">OMS 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdb06-127">An OMS subscription.</span></span>  <span data-ttu-id="cdb06-128">如需進一步資訊，請檢閱 [開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="cdb06-128">For further information, review [Get started with Log Analytics](log-analytics-get-started.md).</span></span>

### <a name="network"></a><span data-ttu-id="cdb06-129">網路</span><span class="sxs-lookup"><span data-stu-id="cdb06-129">Network</span></span>
<span data-ttu-id="cdb06-130">下列資訊列出 Operations Manager 代理程式、管理伺服器及 Operations 主控台與 OMS 通訊所需的 Proxy 和防火牆組態資訊。</span><span class="sxs-lookup"><span data-stu-id="cdb06-130">The information below list the proxy and firewall configuration information required for the Operations Manager agent, management servers, and Operations console to communicate with OMS.</span></span>  <span data-ttu-id="cdb06-131">每個元件的流量會從您的網路輸出至 OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="cdb06-131">Traffic from each component is outbound from your network to the OMS service.</span></span>     

|<span data-ttu-id="cdb06-132">資源</span><span class="sxs-lookup"><span data-stu-id="cdb06-132">Resource</span></span> | <span data-ttu-id="cdb06-133">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="cdb06-133">Port number</span></span>| <span data-ttu-id="cdb06-134">略過 HTTPS 檢查</span><span class="sxs-lookup"><span data-stu-id="cdb06-134">Bypass HTTP Inspection</span></span>|  
|---------|------|-----------------------|  
|<span data-ttu-id="cdb06-135">**代理程式**</span><span class="sxs-lookup"><span data-stu-id="cdb06-135">**Agent**</span></span>|||  
|<span data-ttu-id="cdb06-136">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-136">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="cdb06-137">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-137">443</span></span> |<span data-ttu-id="cdb06-138">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-138">Yes</span></span>|  
|<span data-ttu-id="cdb06-139">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-139">\*.oms.opinsights.azure.com</span></span>| <span data-ttu-id="cdb06-140">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-140">443</span></span>|<span data-ttu-id="cdb06-141">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-141">Yes</span></span>|  
|<span data-ttu-id="cdb06-142">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdb06-142">\*.blob.core.windows.net</span></span>| <span data-ttu-id="cdb06-143">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-143">443</span></span>|<span data-ttu-id="cdb06-144">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-144">Yes</span></span>|  
|<span data-ttu-id="cdb06-145">\*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="cdb06-145">\*.azure-automation.net</span></span>| <span data-ttu-id="cdb06-146">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-146">443</span></span>|<span data-ttu-id="cdb06-147">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-147">Yes</span></span>|  
|<span data-ttu-id="cdb06-148">**管理伺服器**</span><span class="sxs-lookup"><span data-stu-id="cdb06-148">**Management server**</span></span>|||  
|<span data-ttu-id="cdb06-149">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-149">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="cdb06-150">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-150">443</span></span>||  
|<span data-ttu-id="cdb06-151">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdb06-151">\*.blob.core.windows.net</span></span>| <span data-ttu-id="cdb06-152">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-152">443</span></span>| <span data-ttu-id="cdb06-153">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-153">Yes</span></span>|  
|<span data-ttu-id="cdb06-154">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-154">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="cdb06-155">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-155">443</span></span>| <span data-ttu-id="cdb06-156">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-156">Yes</span></span>|  
|<span data-ttu-id="cdb06-157">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="cdb06-157">*.azure-automation.net</span></span> | <span data-ttu-id="cdb06-158">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-158">443</span></span>| <span data-ttu-id="cdb06-159">是</span><span class="sxs-lookup"><span data-stu-id="cdb06-159">Yes</span></span>|  
|<span data-ttu-id="cdb06-160">**Operations Manager 主控台至 OMS**</span><span class="sxs-lookup"><span data-stu-id="cdb06-160">**Operations Manager console to OMS**</span></span>|||  
|<span data-ttu-id="cdb06-161">service.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-161">service.systemcenteradvisor.com</span></span>| <span data-ttu-id="cdb06-162">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-162">443</span></span>||  
|<span data-ttu-id="cdb06-163">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-163">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="cdb06-164">443</span><span class="sxs-lookup"><span data-stu-id="cdb06-164">443</span></span>||  
|<span data-ttu-id="cdb06-165">\*.live.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-165">\*.live.com</span></span>| <span data-ttu-id="cdb06-166">80 和 443</span><span class="sxs-lookup"><span data-stu-id="cdb06-166">80 and 443</span></span>||  
|<span data-ttu-id="cdb06-167">\*.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-167">\*.microsoft.com</span></span>| <span data-ttu-id="cdb06-168">80 和 443</span><span class="sxs-lookup"><span data-stu-id="cdb06-168">80 and 443</span></span>||  
|<span data-ttu-id="cdb06-169">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-169">\*.microsoftonline.com</span></span>| <span data-ttu-id="cdb06-170">80 和 443</span><span class="sxs-lookup"><span data-stu-id="cdb06-170">80 and 443</span></span>||  
|<span data-ttu-id="cdb06-171">\*.mms.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="cdb06-171">\*.mms.microsoft.com</span></span>| <span data-ttu-id="cdb06-172">80 和 443</span><span class="sxs-lookup"><span data-stu-id="cdb06-172">80 and 443</span></span>||  
|<span data-ttu-id="cdb06-173">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="cdb06-173">login.windows.net</span></span>| <span data-ttu-id="cdb06-174">80 和 443</span><span class="sxs-lookup"><span data-stu-id="cdb06-174">80 and 443</span></span>||  


## <a name="connecting-operations-manager-to-oms"></a><span data-ttu-id="cdb06-175">將 Operations Manager 連接到 OMS</span><span class="sxs-lookup"><span data-stu-id="cdb06-175">Connecting Operations Manager to OMS</span></span>
<span data-ttu-id="cdb06-176">執行下列一系列的步驟，設定 Operations Manager 管理群組來連接到其中一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-176">Perform the following series of steps to configure your Operations Manager management group to connect to one of your OMS workspaces.</span></span>

1. <span data-ttu-id="cdb06-177">在 Operations Manager 主控台中，選取 [管理]  工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-177">In the Operations Manager console, select the **Administration** workspace.</span></span>
2. <span data-ttu-id="cdb06-178">展開 Operations Management Suite 節點，然後按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-178">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="cdb06-179">按一下 [註冊到 Operations Management Suite]  連結。</span><span class="sxs-lookup"><span data-stu-id="cdb06-179">Click the **Register to Operations Management Suite** link.</span></span>
4. <span data-ttu-id="cdb06-180">在 [Operations Management Suite 登入精靈：驗證] 頁面上，輸入與 OMS 訂用帳戶相關聯之系統管理員帳戶的電子郵件地址或電話號碼和密碼，然後按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-180">On the **Operations Management Suite Onboarding Wizard: Authentication** page, enter the email address or phone number and password of the administrator account that is associated with your OMS subscription, and click **Sign in**.</span></span>
5. <span data-ttu-id="cdb06-181">成功通過驗證之後，在 [Operations Management Suite 登入精靈: 選取工作區] 頁面上，系統會提示您選取 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-181">After you are successfully authenticated, on the **Operations Management Suite Onboarding Wizard: Select Workspace** page, you are prompted to select your OMS workspace.</span></span>  <span data-ttu-id="cdb06-182">如果您有多個工作區，請從下拉式清單中選取您想要向 Operations Manager 管理群組註冊的工作區，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-182">If you have more than one workspace, select the workspace you want to register with the Operations Manager management group from the drop-down list, and then click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cdb06-183">Operations Manager 一次只支援一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-183">Operations Manager only supports one OMS workspace at a time.</span></span> <span data-ttu-id="cdb06-184">會從 OMS 移除連接以及使用前一個工作區向 OMS 註冊的電腦。</span><span class="sxs-lookup"><span data-stu-id="cdb06-184">The connection and the computers that were registered to OMS with the previous workspace are removed from OMS.</span></span>
   > 
   > 
6. <span data-ttu-id="cdb06-185">在 [Operations Management Suite 登入精靈：摘要] 頁面上，確認您的設定，如果正確無誤，請按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-185">On the **Operations Management Suite Onboarding Wizard: Summary** page, confirm your settings and if they are correct, click **Create**.</span></span>
7. <span data-ttu-id="cdb06-186">在 [Operations Management Suite 登入精靈：完成] 頁面上，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-186">On the **Operations Management Suite Onboarding Wizard: Finish** page, click **Close**.</span></span>

### <a name="add-agent-managed-computers"></a><span data-ttu-id="cdb06-187">加入代理程式所管理的電腦</span><span class="sxs-lookup"><span data-stu-id="cdb06-187">Add agent-managed computers</span></span>
<span data-ttu-id="cdb06-188">設定與 OMS 工作區的整合之後，這只會建立與 OMS 的連接，並不會從向管理群組回報的代理程式收集任何資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-188">After configuring integration with your OMS workspace, this only establishes a connection with OMS, no data is collected from the agents reporting to your management group.</span></span> <span data-ttu-id="cdb06-189">除非您設定特定代理程式管理的哪些電腦會收集 Log Analytics 的資料，否則不會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="cdb06-189">This won’t happen until after you configure which specific agent-managed computers collects data for Log Analytics.</span></span> <span data-ttu-id="cdb06-190">您可以個別選取電腦物件，也可以選取包含 Windows 電腦物件的群組。</span><span class="sxs-lookup"><span data-stu-id="cdb06-190">You can either select the computer objects individually or you can select a group that contains Windows computer objects.</span></span> <span data-ttu-id="cdb06-191">您無法選取包含另一個類別之執行個體 (例如邏輯磁碟或 SQL 資料庫) 的群組。</span><span class="sxs-lookup"><span data-stu-id="cdb06-191">You cannot select a group that  contains instances of another class, such as logical disks or SQL databases.</span></span>

1. <span data-ttu-id="cdb06-192">開啟 Operations Manager 主控台，然後選取 [ **管理** ] 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-192">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="cdb06-193">展開 Operations Management Suite 節點，然後按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-193">Expand the Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="cdb06-194">按一下窗格右側之 [執行] 標題下方的 [加入電腦/群組]  連結。</span><span class="sxs-lookup"><span data-stu-id="cdb06-194">Click the **Add a Computer/Group** link under the Actions heading on the right-side of the pane.</span></span>
4. <span data-ttu-id="cdb06-195">在 [電腦搜尋] 對話方塊中，您可以搜尋 Operations Manager 監視的電腦或群組。</span><span class="sxs-lookup"><span data-stu-id="cdb06-195">In the **Computer Search** dialog box, you can search for computers or groups monitored by Operations Manager.</span></span> <span data-ttu-id="cdb06-196">選取電腦或群組以登入 OMS，並按一下 [新增]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-196">Select computers or groups to onboard to OMS, click **Add**, and then click **OK**.</span></span>

<span data-ttu-id="cdb06-197">在 Operations 主控台的 [管理]  工作區中，您可以檢視電腦和群組，這些電腦和群組設定成收集來自 Operations Management Suite 下方之 [受管理的電腦] 節點的資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-197">You can view computers and groups configured to collect data from the Managed Computers node under Operations Management Suite in the **Administration** workspace of the Operations console.</span></span>  <span data-ttu-id="cdb06-198">您可以視需要在這裡新增或移除電腦和群組。</span><span class="sxs-lookup"><span data-stu-id="cdb06-198">From here, you can add or remove computers and groups as necessary.</span></span>

### <a name="configure-oms-proxy-settings-in-the-operations-console"></a><span data-ttu-id="cdb06-199">在 Operations 主控台中設定 OMS Proxy 設定</span><span class="sxs-lookup"><span data-stu-id="cdb06-199">Configure OMS proxy settings in the Operations console</span></span>
<span data-ttu-id="cdb06-200">如果內部 Proxy 伺服器位在管理群組與 OMS Web 服務之間，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="cdb06-200">Perform the following steps if an internal proxy server is between the management group and OMS web service.</span></span>  <span data-ttu-id="cdb06-201">這些設定是從管理群組進行集中管理，並且散發至範圍中所含的代理程式所管理系統，來收集 OMS 的資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-201">These settings are centrally managed from the management group and distributed to agent-managed systems that are included in the scope to collect data for OMS.</span></span>  <span data-ttu-id="cdb06-202">特定解決方案略過管理伺服器並將資料直接傳送給 OMS Web 服務時，這十分有幫助。</span><span class="sxs-lookup"><span data-stu-id="cdb06-202">This is beneficial for when certain solutions bypass the management server and send data directly to OMS web service.</span></span>

1. <span data-ttu-id="cdb06-203">開啟 Operations Manager 主控台，然後選取 [ **管理** ] 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-203">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="cdb06-204">展開 Operations Management Suite，然後按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-204">Expand Operations Management Suite, and then click **Connections**.</span></span>
3. <span data-ttu-id="cdb06-205">在 [OMS 連線] 檢視中，按一下 [設定 Proxy 伺服器] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-205">In the OMS Connection view, click **Configure Proxy Server**.</span></span>
4. <span data-ttu-id="cdb06-206">在 [Operations Management Suite 精靈：Proxy 伺服器] 頁面上，選取 [使用 Proxy 伺服器來存取 Operations Management Suite]，然後輸入具有連接埠號碼的 URL (例如， http://corpproxy:80 )，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-206">On **Operations Management Suite Wizard: Proxy Server** page, select **Use a proxy server to access the Operations Management Suite**, and then type the URL with the port number, for example, http://corpproxy:80 and then click **Finish**.</span></span>

<span data-ttu-id="cdb06-207">如果 Proxy 伺服器需要驗證，請執行下列步驟來設定認證和設定，這些需要傳播到管理群組中向 OMS 回報的受管理電腦。</span><span class="sxs-lookup"><span data-stu-id="cdb06-207">If your proxy server requires authentication, perform the following steps to configure credentials and settings that need to propagate to managed computers that reports to OMS in the management group.</span></span>

1. <span data-ttu-id="cdb06-208">開啟 Operations Manager 主控台，然後選取 [ **管理** ] 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-208">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="cdb06-209">在 [RunAs 組態] 底下，選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-209">Under **RunAs Configuration**, select **Profiles**.</span></span>
3. <span data-ttu-id="cdb06-210">開啟 [ **System Center Advisor 執行身份設定檔 Proxy** ] 設定檔。</span><span class="sxs-lookup"><span data-stu-id="cdb06-210">Open the **System Center Advisor Run As Profile Proxy** profile.</span></span>
4. <span data-ttu-id="cdb06-211">在 [執行身分設定檔精靈] 中，按一下 [加入] 使用執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdb06-211">In the Run As Profile Wizard, click Add to use a Run As account.</span></span> <span data-ttu-id="cdb06-212">您可以建立[執行身分帳戶](https://technet.microsoft.com/library/hh321655.aspx)，或使用現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cdb06-212">You can create a [Run As account](https://technet.microsoft.com/library/hh321655.aspx) or use an existing account.</span></span> <span data-ttu-id="cdb06-213">此帳戶必須有足夠的權限，才能通過 Proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="cdb06-213">This account needs to have sufficient permissions to pass through the proxy server.</span></span>
5. <span data-ttu-id="cdb06-214">若要設定帳戶來管理，請選擇 [選取的類別、群組或物件]，按一下 [選取…]</span><span class="sxs-lookup"><span data-stu-id="cdb06-214">To set the account to manage, choose **A selected class, group, or object**, click **Select…**</span></span> <span data-ttu-id="cdb06-215">然後按一下 [群組…]</span><span class="sxs-lookup"><span data-stu-id="cdb06-215">and then click **Group…**</span></span> <span data-ttu-id="cdb06-216">開啟 [群組搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="cdb06-216">to open the **Group Search** box.</span></span>
6. <span data-ttu-id="cdb06-217">搜尋，然後選取 [Microsoft System Center Advisor 監控伺服器群組] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-217">Search for and then select **Microsoft System Center Advisor Monitoring Server Group**.</span></span>  <span data-ttu-id="cdb06-218">選取群組之後，按一下 [確定] 關閉 [群組搜尋] 方塊。</span><span class="sxs-lookup"><span data-stu-id="cdb06-218">Click **OK** after selecting the group to close the **Group Search** box.</span></span>
7. <span data-ttu-id="cdb06-219">按一下 [確定] 以關閉 [新增執行身分帳戶] 方塊。</span><span class="sxs-lookup"><span data-stu-id="cdb06-219">Click **OK** to close the **Add a Run As account** box.</span></span>
8. <span data-ttu-id="cdb06-220">按一下 [儲存]  完成精靈並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="cdb06-220">Click **Save** to complete the wizard and save your changes.</span></span>

<span data-ttu-id="cdb06-221">建立連線並設定哪些代理程式將收集資料並回報給 OMS 之後，管理群組中就會套用下列組態，但未必依照下列順序︰</span><span class="sxs-lookup"><span data-stu-id="cdb06-221">After the connection is created and you configure which agents will collect and report data to OMS, the following configuration is applied in the management group, not necessarily in order:</span></span>

* <span data-ttu-id="cdb06-222">建立執行身分帳戶 **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-222">The Run As Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** is created.</span></span>  <span data-ttu-id="cdb06-223">它是與執行身分設定檔 **Microsoft System Center Advisor Run As Profile Blob** 相關聯，而且將目標設為兩個類別：[收集伺服器] 和 [Operations Manager 管理群組]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-223">It is associated with the Run As profile **Microsoft System Center Advisor Run As Profile Blob** and is targeting two classes - **Collection Server** and **Operations Manager Management Group**.</span></span>
* <span data-ttu-id="cdb06-224">會建立兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="cdb06-224">Two connectors are created.</span></span>  <span data-ttu-id="cdb06-225">第一個稱為 **Microsoft.SystemCenter.Advisor.DataConnector**，並自動以一個訂用帳戶設定，這個訂用帳戶會將管理群組中所有類別之執行個體產生的所有警示轉送給 OMS Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="cdb06-225">The first is named **Microsoft.SystemCenter.Advisor.DataConnector** and is automatically configured with a subscription that forwards all alerts generated from instances of all classes in the management group to OMS Log Analytics.</span></span> <span data-ttu-id="cdb06-226">第二個連接器是 **Advisor 連接器**，負責與 OMS Web 服務進行通訊以及共用資料。</span><span class="sxs-lookup"><span data-stu-id="cdb06-226">The second connector is **Advisor Connector**, which is responsible for communicating with OMS web service and sharing data.</span></span>
* <span data-ttu-id="cdb06-227">您在管理群組中已選擇來收集資料的代理程式和群組，將會新增至 [Microsoft System Center Advisor 監控伺服器群組]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-227">Agents and groups that you have selected to collect data in the management group is added to the **Microsoft System Center Advisor Monitoring Server Group**.</span></span>

## <a name="management-pack-updates"></a><span data-ttu-id="cdb06-228">管理組件更新</span><span class="sxs-lookup"><span data-stu-id="cdb06-228">Management pack updates</span></span>
<span data-ttu-id="cdb06-229">組態完成之後，Operations Manager 管理群組就會建立與 OMS 服務的連接。</span><span class="sxs-lookup"><span data-stu-id="cdb06-229">After configuration is completed, the Operations Manager management group establishes a connection with the OMS service.</span></span>  <span data-ttu-id="cdb06-230">針對您已啟用且與 Operations Manager 整合的解決方案，管理伺服器會與 Web 服務同步處理，並以管理組件的形式接收更新的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="cdb06-230">The management server synchronizes with the web service and receive updated configuration information in the form of management packs for the solutions you have enabled that integrate with Operations Manager.</span></span>   <span data-ttu-id="cdb06-231">Operations Manager 會檢查這些管理組件的更新，如果有更新，就會自動下載並匯入。</span><span class="sxs-lookup"><span data-stu-id="cdb06-231">Operations Manager  checks for updates of these management packs and automatically download and imports them when they’re available.</span></span>  <span data-ttu-id="cdb06-232">有兩個規則特別可控制這個行為︰</span><span class="sxs-lookup"><span data-stu-id="cdb06-232">There are two rules in particular which control this behavior:</span></span>

* <span data-ttu-id="cdb06-233">**Microsoft.SystemCenter.Advisor.MPUpdate** - 更新基底 OMS 管理組件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-233">**Microsoft.SystemCenter.Advisor.MPUpdate** - Updates the base OMS management packs.</span></span> <span data-ttu-id="cdb06-234">預設會每 12 小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="cdb06-234">Runs every 12 hours by default.</span></span>
* <span data-ttu-id="cdb06-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - 更新工作區中所啟用的解決方案管理組件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Updates solution management packs enabled in your workspace.</span></span> <span data-ttu-id="cdb06-236">預設會每五 (5) 分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="cdb06-236">Runs every five (5) minutes by default.</span></span>

<span data-ttu-id="cdb06-237">您可以透過停用來覆寫這兩個規則以防止自動下載，或者修改管理伺服器與 OMS 同步處理之頻率的頻率，來決定新的管理組件是否可用而且應該予以下載。</span><span class="sxs-lookup"><span data-stu-id="cdb06-237">You can override these two rules to either prevent automatic download by disabling them, or modify the frequency for how often the management server synchronizes with OMS to determine if a new management pack is available and should be downloaded.</span></span>  <span data-ttu-id="cdb06-238">遵循[如何覆寫規則或監視器](https://technet.microsoft.com/library/hh212869.aspx)步驟，使用值 (秒) 修改 [頻率] 參數來變更同步處理排程，或修改 [已啟用] 參數來停用規則。</span><span class="sxs-lookup"><span data-stu-id="cdb06-238">Follow the steps [How to Override a Rule or Monitor](https://technet.microsoft.com/library/hh212869.aspx) to modify the **Frequency** parameter with a value in seconds to change the synchronization schedule, or modify the **Enabled** parameter to disable the rules.</span></span>  <span data-ttu-id="cdb06-239">將目標設為覆寫 [Operations Manager 管理群組] 類別的所有物件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-239">Target the overrides to all objects of class Operations Manager Management Group.</span></span>

<span data-ttu-id="cdb06-240">如果您想要繼續遵循現有的變更控制程序來控制生產管理群組中的管理組件發行版本，則可以停用規則，並在允許更新時於特定期間啟用它們。</span><span class="sxs-lookup"><span data-stu-id="cdb06-240">If you want to continue following your existing change control process for controlling management pack releases in your production management group, you can disable the rules and enable them during specific times when updates are allowed.</span></span> <span data-ttu-id="cdb06-241">如果您的環境中有開發或 QA 管理群組，而且該管理群組連接到網際網路，則可以設定該管理群組與 OMS 工作區，以支援此案例。</span><span class="sxs-lookup"><span data-stu-id="cdb06-241">If you have a development or QA management group in your environment and it has connectivity to the Internet, you can configure that management group with an OMS workspace to support this scenario.</span></span>  <span data-ttu-id="cdb06-242">這可讓您先檢閱和評估 OMS 管理組件的反覆版本，再發行到生產管理群組。</span><span class="sxs-lookup"><span data-stu-id="cdb06-242">This allows you to review and evaluate the iterative releases of the OMS management packs before releasing them into your production management group.</span></span>

## <a name="switch-an-operations-manager-group-to-a-new-oms-workspace"></a><span data-ttu-id="cdb06-243">將 Operations Manager 群組切換到新的 OMS 工作區</span><span class="sxs-lookup"><span data-stu-id="cdb06-243">Switch an Operations Manager group to a new OMS Workspace</span></span>
1. <span data-ttu-id="cdb06-244">登入 OMS 訂用帳戶，然後在 [Microsoft Operations Management Suite](http://oms.microsoft.com/) 中建立工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-244">Log in to your OMS subscription and create a workspace in [Microsoft Operations Management Suite](http://oms.microsoft.com/).</span></span>
2. <span data-ttu-id="cdb06-245">使用身為 Operations Manager 系統管理員角色成員的帳戶開啟 Operations Manager 主控台，然後選取 [管理]  工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-245">Open the Operations Manager console with an account that is a member of the Operations Manager Administrators role and select the **Administration** workspace.</span></span>
3. <span data-ttu-id="cdb06-246">展開 Operations Management Suite，選取 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-246">Expand Operations Management Suite, and select **Connections**.</span></span>
4. <span data-ttu-id="cdb06-247">選取窗格中間的 [重新設定 Operation Management Suite]  連結。</span><span class="sxs-lookup"><span data-stu-id="cdb06-247">Select the **Re-configure Operation Management Suite** link on the middle-side of the pane.</span></span>
5. <span data-ttu-id="cdb06-248">遵循 [Operations Management Suite 登入精靈]  進行，輸入與新的 OMS 工作區相關聯之系統管理員帳戶的電子郵件地址或電話號碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="cdb06-248">Follow the **Operations Management Suite Onboarding Wizard** and enter the email address or phone number and password of the administrator account that is associated with your new OMS workspace.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cdb06-249">[Operations Management Suite 登入精靈：選取工作區] 頁面會顯示使用中的現有工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-249">The **Operations Management Suite Onboarding Wizard: Select Workspace** page presents the existing workspace that is in use.</span></span>
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a><span data-ttu-id="cdb06-250">驗證 Operations Manager 與 OMS 的整合</span><span class="sxs-lookup"><span data-stu-id="cdb06-250">Validate Operations Manager Integration with OMS</span></span>
<span data-ttu-id="cdb06-251">您有幾種不同的方式可以確認 OMS 與 Operations Manager 的整合成功。</span><span class="sxs-lookup"><span data-stu-id="cdb06-251">There are a few different ways you can verify that your OMS to Operations Manager integration is successful.</span></span>

### <a name="to-confirm-integration-from-the-oms-portal"></a><span data-ttu-id="cdb06-252">從 OMS 入口網站確認整合</span><span class="sxs-lookup"><span data-stu-id="cdb06-252">To confirm integration from the OMS portal</span></span>
1. <span data-ttu-id="cdb06-253">在 OMS 入口網站中，按一下 [設定] 圖格</span><span class="sxs-lookup"><span data-stu-id="cdb06-253">In the OMS portal, click the **Settings** tile</span></span>
2. <span data-ttu-id="cdb06-254">選取 [連接的來源]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-254">Select  **Connected Sources**.</span></span>
3. <span data-ttu-id="cdb06-255">在 [System Center Operations Manager] 區段下方的表格中，您應該會看到管理群組名稱，還會列出上次收到資料時的代理程式數目和狀態。</span><span class="sxs-lookup"><span data-stu-id="cdb06-255">In the table under the System Center Operations Manager section, you should see the name of the management group listed with the number of agents and status when data was last received.</span></span>
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. <span data-ttu-id="cdb06-257">請記下 [設定] 頁面左下方的 [工作區識別碼]  值。</span><span class="sxs-lookup"><span data-stu-id="cdb06-257">Note the **Workspace ID** value under the left-side of the Settings page.</span></span>  <span data-ttu-id="cdb06-258">以下您將根據 Operations Manager 管理群組來驗證此值。</span><span class="sxs-lookup"><span data-stu-id="cdb06-258">You validate it against your Operations Manager management group below.</span></span>  

### <a name="to-confirm-integration-from-the-operations-console"></a><span data-ttu-id="cdb06-259">從 Operations 主控台確認整合</span><span class="sxs-lookup"><span data-stu-id="cdb06-259">To confirm integration from the Operations console</span></span>
1. <span data-ttu-id="cdb06-260">開啟 Operations Manager 主控台，然後選取 [ **管理** ] 工作區。</span><span class="sxs-lookup"><span data-stu-id="cdb06-260">Open the Operations Manager console and select the **Administration** workspace.</span></span>
2. <span data-ttu-id="cdb06-261">選取 [管理組件]，並在 [尋找:] 文字方塊中輸入 **Advisor** 或 **Intelligence**。</span><span class="sxs-lookup"><span data-stu-id="cdb06-261">Select **Management Packs** and in the **Look for:** text box type **Advisor** or **Intelligence**.</span></span>
3. <span data-ttu-id="cdb06-262">根據您已啟用的解決方案，您會看到搜尋結果中列出對應的管理組件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-262">Depending on the solutions you have enabled, you see a corresponding management pack listed in the search results.</span></span>  <span data-ttu-id="cdb06-263">例如，如果您已啟用警示管理解決方案，則 [Microsoft System Center Advisor 警示管理] 管理組件會在清單中。</span><span class="sxs-lookup"><span data-stu-id="cdb06-263">For example, if you have enabled the Alert Management solution, the management pack Microsoft System Center Advisor Alert Management is in the list.</span></span>
4. <span data-ttu-id="cdb06-264">從 [監視] 檢視中，瀏覽至 [Operations Management Suite\健全狀況狀態] 檢視。</span><span class="sxs-lookup"><span data-stu-id="cdb06-264">From the **Monitoring** view, navigate to the **Operations Management Suite\Health State** view.</span></span>  <span data-ttu-id="cdb06-265">在 [管理伺服器狀態] 窗格下選取管理伺服器，然後在 [詳細資料檢視] 窗格中，確認 [驗證服務 URI] 屬性的值符合 OMS 工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="cdb06-265">Select a Management server under the **Management Server State** pane, and in the **Detail View** pane confirm the value for property **Authentication service URI** matches the OMS Workspace ID.</span></span>
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a><span data-ttu-id="cdb06-267">移除與 OMS 的整合</span><span class="sxs-lookup"><span data-stu-id="cdb06-267">Remove Integration with OMS</span></span>
<span data-ttu-id="cdb06-268">當您不再需要整合 Operations Manager 管理群組和 OMS 工作區時，需要執行幾個步驟，才能適當移除管理群組中的連接和組態。</span><span class="sxs-lookup"><span data-stu-id="cdb06-268">When you no longer require integration between your Operations Manager management group and OMS workspace, there are several steps required to properly remove the connection and configuration in the management group.</span></span> <span data-ttu-id="cdb06-269">下列程序可讓您刪除管理群組的參考來更新 OMS 工作區、刪除 OM 連接器，然後刪除支援 OMS 的管理組件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-269">The following procedure has you update your OMS workspace by deleting the reference of your management group, delete the OMS connectors, and then delete management packs supporting OMS.</span></span>   

<span data-ttu-id="cdb06-270">已啟用且與 Operations Manager 整合之解決方案的管理組件，以及支援與 OMS 服務整合所需的管理組件，都無法輕易地從管理群組中刪除。</span><span class="sxs-lookup"><span data-stu-id="cdb06-270">Management packs for the solutions you have enabled that integrate with Operations Manager and the management packs required to support integration with the OMS service cannot be easily deleted from the management group.</span></span>  <span data-ttu-id="cdb06-271">這是因為有些 OMS 管理組件與其他相關管理組件相依。</span><span class="sxs-lookup"><span data-stu-id="cdb06-271">This is because some of the OMS management packs have dependencies on other related management packs.</span></span>  <span data-ttu-id="cdb06-272">若要刪除與其他管理組件相依的管理組件，請從 TechNet 指令碼中心下載[移除具有相依性的管理組件](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) (英文) 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cdb06-272">To delete management packs having a dependency on other management packs, download the script [remove a management pack with dependencies](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) from TechNet Script Center.</span></span>  

1. <span data-ttu-id="cdb06-273">使用身為 Operations Manager 系統管理員角色成員的帳戶開啟 Operations Manager 命令殼層。</span><span class="sxs-lookup"><span data-stu-id="cdb06-273">Open the Operations Manager Command Shell with an account that is a member of the Operations Manager Administrators role.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="cdb06-274">繼續之前，請確認您的任何自訂管理組件名稱中沒有 Advisor 或 IntelligencePack 這個字，否則下列步驟會從管理群組中刪除它們。</span><span class="sxs-lookup"><span data-stu-id="cdb06-274">Verify you do not have any custom management packs with the word Advisor or IntelligencePack in the name before proceeding, otherwise the following steps delete them from the management group.</span></span>
    > 

2. <span data-ttu-id="cdb06-275">從命令殼層提示字元中，輸入 `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="cdb06-275">From the command shell prompt, type `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
3. <span data-ttu-id="cdb06-276">接著輸入 `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="cdb06-276">Next type, `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
4. <span data-ttu-id="cdb06-277">若要移除與其他 System Center Advisor 管理組件具有相依性的任何其餘管理組件，請使用您稍早從 TechNet 指令碼中心下載的 *RecursiveRemove.ps1* 指令碼。</span><span class="sxs-lookup"><span data-stu-id="cdb06-277">To remove any management packs remaining which have a dependency on other System Center Advisor management packs, use the script *RecursiveRemove.ps1* you downloaded from the TechNet Script Center earlier.</span></span>  
 
    > [!NOTE]
    > <span data-ttu-id="cdb06-278">請不要刪除 Microsoft System Center Advisor 或 Microsoft System Center Advisor Internal 管理組件。</span><span class="sxs-lookup"><span data-stu-id="cdb06-278">Do not delete the Microsoft System Center Advisor or Microsoft System Center Advisor Internal management packs.</span></span>  
    >  

5. <span data-ttu-id="cdb06-279">使用身為 Operations Manager 系統管理員角色成員的帳戶開啟 Operations Manager Operations 主控台。</span><span class="sxs-lookup"><span data-stu-id="cdb06-279">Open the Operations Manager Operations console with an account that is a member of the Operations Manager Administrators role.</span></span>
6. <span data-ttu-id="cdb06-280">在 [管理] 下，選取 [管理組件] 節點，然後在 [尋找:] 方塊中輸入 **Advisor**，並確認下列管理組件仍匯入到管理群組中︰</span><span class="sxs-lookup"><span data-stu-id="cdb06-280">Under **Administration**, select the **Management Packs** node and in the **Look for:** box, type **Advisor** and verify the following management packs are still imported in your management group:</span></span>
   
   * <span data-ttu-id="cdb06-281">Microsoft System Center Advisor</span><span class="sxs-lookup"><span data-stu-id="cdb06-281">Microsoft System Center Advisor</span></span>
   * <span data-ttu-id="cdb06-282">Microsoft System Center Advisor Internal</span><span class="sxs-lookup"><span data-stu-id="cdb06-282">Microsoft System Center Advisor Internal</span></span>
7. <span data-ttu-id="cdb06-283">在 OMS 入口網站中，按一下 [設定] 圖格。</span><span class="sxs-lookup"><span data-stu-id="cdb06-283">In the OMS portal, click the **Settings** tile.</span></span>
8. <span data-ttu-id="cdb06-284">選取 [連接的來源] 。</span><span class="sxs-lookup"><span data-stu-id="cdb06-284">Select **Connected Sources**.</span></span>
9. <span data-ttu-id="cdb06-285">在 [System Center Operations Manager] 區段下方的表格中，您應該會看到想要從工作區移除的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="cdb06-285">In the table under the System Center Operations Manager section, you should see the name of the management group you want to remove from the workspace.</span></span>  <span data-ttu-id="cdb06-286">在 [最後一筆資料] 資料行之下，按一下 [移除]。</span><span class="sxs-lookup"><span data-stu-id="cdb06-286">Under the column **Last Data**, click **Remove**.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="cdb06-287">在偵測到已連線的管理群組有 14 天沒有任何活動之後，[移除] 連結才能使用。</span><span class="sxs-lookup"><span data-stu-id="cdb06-287">The **Remove** link will not be available until after 14 days if there is no activity detected from the connected management group.</span></span>  
    > 

10. <span data-ttu-id="cdb06-288">將出現視窗，要求您確認想要繼續移除。</span><span class="sxs-lookup"><span data-stu-id="cdb06-288">A window will appear asking you to confirm that you want to proceed with the removal.</span></span>  <span data-ttu-id="cdb06-289">按一下 [是]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="cdb06-289">Click **Yes** to proceed.</span></span> 

<span data-ttu-id="cdb06-290">若要刪除兩個連接器 - Microsoft.SystemCenter.Advisor.DataConnector 和 Advisor 連接器，請將以下 PowerShell 指令碼儲存至您的電腦，並使用下列範例來執行：</span><span class="sxs-lookup"><span data-stu-id="cdb06-290">To delete the two connectors - Microsoft.SystemCenter.Advisor.DataConnector and Advisor Connector, save the PowerShell script below to your computer and execute using the following examples:</span></span>

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> <span data-ttu-id="cdb06-291">您執行此指令碼的電腦 (如果不是管理伺服器) 應該已安裝 Operations Manager 命令殼層，視您的管理群組版本而定。</span><span class="sxs-lookup"><span data-stu-id="cdb06-291">The computer you run this script from, if not a management server, should have the Operations Manager command shell installed depending on the version of your management group.</span></span>
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with the specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with the specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

<span data-ttu-id="cdb06-292">未來，如果您打算將管理群組重新連接至 OMS 工作區，您需要從套用到管理群組的最新更新彙總套件中，重新匯入 `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` 管理組件檔案。</span><span class="sxs-lookup"><span data-stu-id="cdb06-292">In the future if you plan on reconnecting your management group to an OMS workspace, you  need to re-import the `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack file from the most recent update rollup applied to your management group.</span></span>  <span data-ttu-id="cdb06-293">您可以在 `%ProgramFiles%\Microsoft System Center 2012` 或 `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` 資料夾中找到此檔案。</span><span class="sxs-lookup"><span data-stu-id="cdb06-293">You can find this file in the `%ProgramFiles%\Microsoft System Center 2012` or the `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdb06-294">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cdb06-294">Next steps</span></span>
<span data-ttu-id="cdb06-295">若要新增功能和收集資料，請參閱[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="cdb06-295">To add functionality and gather data, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>


