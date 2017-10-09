---
title: "aaaConnect Operations Manager tooLog 分析 |Microsoft 文件"
description: "toomaintain 您現有的投資，在 System Center Operations Manager，並使用擴充功能記錄分析，您可以整合 Operations Manager 與 OMS 工作區。"
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
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a><span data-ttu-id="c1178-103">連接 Operations Manager tooLog 分析</span><span class="sxs-lookup"><span data-stu-id="c1178-103">Connect Operations Manager tooLog Analytics</span></span>
<span data-ttu-id="c1178-104">toomaintain 您現有的投資，在 System Center Operations Manager，並使用擴充功能記錄分析，您可以整合 Operations Manager 與 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-104">toomaintain your existing investment in System Center Operations Manager and use extended capabilities with Log Analytics, you can integrate Operations Manager with your OMS workspace.</span></span>  <span data-ttu-id="c1178-105">這可讓您利用 OMS 的 hello 機會繼續 toouse Operations Manager 時要：</span><span class="sxs-lookup"><span data-stu-id="c1178-105">This allows you leverage hello opportunities of OMS while continuing toouse Operations Manager to:</span></span>

* <span data-ttu-id="c1178-106">繼續監視您的 IT 服務，與 Operations Manager hello 健全狀況</span><span class="sxs-lookup"><span data-stu-id="c1178-106">Continue monitoring hello health of your IT services with Operations Manager</span></span>
* <span data-ttu-id="c1178-107">維護與支援事件和問題管理之 ITSM 解決方案的整合</span><span class="sxs-lookup"><span data-stu-id="c1178-107">Maintain integration with your ITSM solutions supporting incident and problem management</span></span>
* <span data-ttu-id="c1178-108">管理部署的代理程式 tooon 內部和公用雲端 IaaS 虛擬機器，您使用 Operations Manager 監視 hello 生命週期</span><span class="sxs-lookup"><span data-stu-id="c1178-108">Manage hello lifecycle of agents deployed tooon-premises and public cloud IaaS virtual machines that you monitor with Operations Manager</span></span>

<span data-ttu-id="c1178-109">整合 System Center Operations Manager 與使用 hello 速度與效率中收集、 儲存及分析資料的 Operations Manager OMS 新增值 tooyour 服務作業的策略。</span><span class="sxs-lookup"><span data-stu-id="c1178-109">Integrating with System Center Operations Manager adds value tooyour service operations strategy by using hello speed and efficiency of OMS in collecting, storing, and analyzing data from Operations Manager.</span></span>  <span data-ttu-id="c1178-110">OMS 協助建立相互關聯，並朝向識別 hello 錯誤的問題和面對日數，以支援您現有的問題管理程序的工作。</span><span class="sxs-lookup"><span data-stu-id="c1178-110">OMS helps correlate and work towards identifying hello faults of problems and surfacing recurrences in support of your existing problem management process.</span></span>   <span data-ttu-id="c1178-111">hello hello 搜尋引擎 tooexamine 效能、 事件和警示資料，與豐富的儀表板的彈性和報告功能 tooexpose 有意義的方式，此資料會示範 OMS 帶來 complimenting Operations Manager 中的 hello 強度。</span><span class="sxs-lookup"><span data-stu-id="c1178-111">hello flexibility of hello search engine tooexamine performance, event and alert data, with rich dashboards and reporting capabilities tooexpose this data in meaningful ways, demonstrates hello strength OMS brings in complimenting Operations Manager.</span></span>

<span data-ttu-id="c1178-112">hello 代理程式回報 toohello Operations Manager 管理群組會從您根據 hello 記錄分析資料來源 」 和 「 您已啟用您的 OMS 訂用帳戶中解決方案的伺服器收集資料。</span><span class="sxs-lookup"><span data-stu-id="c1178-112">hello agents reporting toohello Operations Manager management group collect data from your servers based on hello Log Analytics data sources and solutions you have enabled in your OMS subscription.</span></span>  <span data-ttu-id="c1178-113">根據您已啟用的 hello 解決方案，這些解決方案的資料是 toohello OMS web 服務，或因為 hello hello 代理程式管理系統上所收集的資料磁碟區會直接傳送訊息，請傳送直接從 Operations Manager 管理伺服器從 hello 代理程式 tooOMS web 服務。</span><span class="sxs-lookup"><span data-stu-id="c1178-113">Depending on hello solution you have enabled, data from these solutions are either sent directly from an Operations Manager management server toohello OMS web service, or because of hello volume of data collected on hello agent-managed system, are sent directly from hello agent tooOMS web service.</span></span> <span data-ttu-id="c1178-114">hello 管理伺服器將轉寄 hello OMS 資料直接 toohello OMS web 服務。它永遠不會寫入 toohello OperationsManager 或 OperationsManagerDW 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c1178-114">hello management server forwards hello OMS data directly toohello OMS web service; it is never written toohello OperationsManager or OperationsManagerDW database.</span></span>  <span data-ttu-id="c1178-115">當管理伺服器失去連線能力與 hello OMS web 服務時，只有重新建立與 OMS 通訊之前，在本機快取 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="c1178-115">When a management server loses connectivity with hello OMS web service, it caches hello data locally until communication is re-established with OMS.</span></span>  <span data-ttu-id="c1178-116">如果 hello 管理伺服器已離線到期 tooplanned 維護或非計劃的中斷，hello 管理群組中的另一部管理伺服器會繼續與 OMS 的連線。</span><span class="sxs-lookup"><span data-stu-id="c1178-116">If hello management server is offline due tooplanned maintenance or unplanned outage, another management server in hello management group resumes connectivity with OMS.</span></span>  

<span data-ttu-id="c1178-117">hello 下列圖表描述 hello hello 管理伺服器與 System Center Operations Manager 管理群組和 OMS，包括 hello 方向和連接埠中的代理程式之間的連線。</span><span class="sxs-lookup"><span data-stu-id="c1178-117">hello following diagram depicts hello connection between hello management servers and agents in a System Center Operations Manager management group and OMS, including hello direction and ports.</span></span>   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

<span data-ttu-id="c1178-119">如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，管理伺服器可以設定的 tooconnect toohello OMS 閘道 tooreceive 組態資訊並傳送收集的資料取決於 hello 方案已啟用。</span><span class="sxs-lookup"><span data-stu-id="c1178-119">If your IT security policies do not allow computers on your network tooconnect toohello Internet, management servers can be configured tooconnect toohello OMS Gateway tooreceive configuration information and send collected data depending on hello solution you have enabled.</span></span>  <span data-ttu-id="c1178-120">如需詳細資訊和步驟上如何 tooconfigure OMS 閘道 toohello OMS 服務，透過您 Operations Manager 管理群組 toocommunicate 參閱[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="c1178-120">For more information and steps on how tooconfigure your Operations Manager management group toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

## <a name="system-requirements"></a><span data-ttu-id="c1178-121">系統需求</span><span class="sxs-lookup"><span data-stu-id="c1178-121">System requirements</span></span>
<span data-ttu-id="c1178-122">開始之前，請檢閱下列符合必要條件的詳細資料 tooverify hello。</span><span class="sxs-lookup"><span data-stu-id="c1178-122">Before starting, review hello following details tooverify you meet prerequisites.</span></span>

* <span data-ttu-id="c1178-123">OMS 僅支援 Operations Manager 2016、Operations Manager 2012 SP1 UR6 和更新版本，以及 Operations Manager 2012 R2 UR2 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="c1178-123">OMS only supports Operations Manager 2016, Operations Manager 2012 SP1 UR6 and greater, and Operations Manager 2012 R2 UR2 and greater.</span></span>  <span data-ttu-id="c1178-124">Operations Manager 2012 SP1 UR7 和 Operations Manager 2012 R2 UR3 中已加入 Proxy 支援。</span><span class="sxs-lookup"><span data-stu-id="c1178-124">Proxy support was added in Operations Manager 2012 SP1 UR7 and Operations Manager 2012 R2 UR3.</span></span>
* <span data-ttu-id="c1178-125">所有 Operations Manager 代理程式必須符合最低支援需求。</span><span class="sxs-lookup"><span data-stu-id="c1178-125">All Operations Manager agents must meet minimum support requirements.</span></span> <span data-ttu-id="c1178-126">確定代理程式已在 hello 最小更新，否則 Windows 代理程式的流量可能會失敗並許多錯誤可能會填滿 hello Operations Manager 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c1178-126">Ensure that agents are at hello minimum update, otherwise Windows agent traffic may fail and many errors might fill hello Operations Manager event log.</span></span>
* <span data-ttu-id="c1178-127">OMS 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1178-127">An OMS subscription.</span></span>  <span data-ttu-id="c1178-128">如需進一步資訊，請檢閱 [開始使用 Log Analytics](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c1178-128">For further information, review [Get started with Log Analytics](log-analytics-get-started.md).</span></span>

### <a name="network"></a><span data-ttu-id="c1178-129">網路</span><span class="sxs-lookup"><span data-stu-id="c1178-129">Network</span></span>
<span data-ttu-id="c1178-130">以下清單 hello proxy 和防火牆設定資訊所需的 hello Operations Manager 代理程式、 管理伺服器，以及與 OMS 的 Operations 主控台 toocommunicate hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="c1178-130">hello information below list hello proxy and firewall configuration information required for hello Operations Manager agent, management servers, and Operations console toocommunicate with OMS.</span></span>  <span data-ttu-id="c1178-131">從每個元件的流量是輸出從您的網路 toohello OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="c1178-131">Traffic from each component is outbound from your network toohello OMS service.</span></span>     

|<span data-ttu-id="c1178-132">資源</span><span class="sxs-lookup"><span data-stu-id="c1178-132">Resource</span></span> | <span data-ttu-id="c1178-133">連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="c1178-133">Port number</span></span>| <span data-ttu-id="c1178-134">略過 HTTPS 檢查</span><span class="sxs-lookup"><span data-stu-id="c1178-134">Bypass HTTP Inspection</span></span>|  
|---------|------|-----------------------|  
|<span data-ttu-id="c1178-135">**代理程式**</span><span class="sxs-lookup"><span data-stu-id="c1178-135">**Agent**</span></span>|||  
|<span data-ttu-id="c1178-136">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="c1178-136">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="c1178-137">443</span><span class="sxs-lookup"><span data-stu-id="c1178-137">443</span></span> |<span data-ttu-id="c1178-138">是</span><span class="sxs-lookup"><span data-stu-id="c1178-138">Yes</span></span>|  
|<span data-ttu-id="c1178-139">\*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="c1178-139">\*.oms.opinsights.azure.com</span></span>| <span data-ttu-id="c1178-140">443</span><span class="sxs-lookup"><span data-stu-id="c1178-140">443</span></span>|<span data-ttu-id="c1178-141">是</span><span class="sxs-lookup"><span data-stu-id="c1178-141">Yes</span></span>|  
|<span data-ttu-id="c1178-142">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="c1178-142">\*.blob.core.windows.net</span></span>| <span data-ttu-id="c1178-143">443</span><span class="sxs-lookup"><span data-stu-id="c1178-143">443</span></span>|<span data-ttu-id="c1178-144">是</span><span class="sxs-lookup"><span data-stu-id="c1178-144">Yes</span></span>|  
|<span data-ttu-id="c1178-145">\*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="c1178-145">\*.azure-automation.net</span></span>| <span data-ttu-id="c1178-146">443</span><span class="sxs-lookup"><span data-stu-id="c1178-146">443</span></span>|<span data-ttu-id="c1178-147">是</span><span class="sxs-lookup"><span data-stu-id="c1178-147">Yes</span></span>|  
|<span data-ttu-id="c1178-148">**管理伺服器**</span><span class="sxs-lookup"><span data-stu-id="c1178-148">**Management server**</span></span>|||  
|<span data-ttu-id="c1178-149">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="c1178-149">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="c1178-150">443</span><span class="sxs-lookup"><span data-stu-id="c1178-150">443</span></span>||  
|<span data-ttu-id="c1178-151">\*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="c1178-151">\*.blob.core.windows.net</span></span>| <span data-ttu-id="c1178-152">443</span><span class="sxs-lookup"><span data-stu-id="c1178-152">443</span></span>| <span data-ttu-id="c1178-153">是</span><span class="sxs-lookup"><span data-stu-id="c1178-153">Yes</span></span>|  
|<span data-ttu-id="c1178-154">\*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="c1178-154">\*.ods.opinsights.azure.com</span></span>| <span data-ttu-id="c1178-155">443</span><span class="sxs-lookup"><span data-stu-id="c1178-155">443</span></span>| <span data-ttu-id="c1178-156">是</span><span class="sxs-lookup"><span data-stu-id="c1178-156">Yes</span></span>|  
|<span data-ttu-id="c1178-157">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="c1178-157">*.azure-automation.net</span></span> | <span data-ttu-id="c1178-158">443</span><span class="sxs-lookup"><span data-stu-id="c1178-158">443</span></span>| <span data-ttu-id="c1178-159">是</span><span class="sxs-lookup"><span data-stu-id="c1178-159">Yes</span></span>|  
|<span data-ttu-id="c1178-160">**Operations Manager 主控台 tooOMS**</span><span class="sxs-lookup"><span data-stu-id="c1178-160">**Operations Manager console tooOMS**</span></span>|||  
|<span data-ttu-id="c1178-161">service.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="c1178-161">service.systemcenteradvisor.com</span></span>| <span data-ttu-id="c1178-162">443</span><span class="sxs-lookup"><span data-stu-id="c1178-162">443</span></span>||  
|<span data-ttu-id="c1178-163">\*.service.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="c1178-163">\*.service.opinsights.azure.com</span></span>| <span data-ttu-id="c1178-164">443</span><span class="sxs-lookup"><span data-stu-id="c1178-164">443</span></span>||  
|<span data-ttu-id="c1178-165">\*.live.com</span><span class="sxs-lookup"><span data-stu-id="c1178-165">\*.live.com</span></span>| <span data-ttu-id="c1178-166">80 和 443</span><span class="sxs-lookup"><span data-stu-id="c1178-166">80 and 443</span></span>||  
|<span data-ttu-id="c1178-167">\*.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="c1178-167">\*.microsoft.com</span></span>| <span data-ttu-id="c1178-168">80 和 443</span><span class="sxs-lookup"><span data-stu-id="c1178-168">80 and 443</span></span>||  
|<span data-ttu-id="c1178-169">\*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="c1178-169">\*.microsoftonline.com</span></span>| <span data-ttu-id="c1178-170">80 和 443</span><span class="sxs-lookup"><span data-stu-id="c1178-170">80 and 443</span></span>||  
|<span data-ttu-id="c1178-171">\*.mms.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="c1178-171">\*.mms.microsoft.com</span></span>| <span data-ttu-id="c1178-172">80 和 443</span><span class="sxs-lookup"><span data-stu-id="c1178-172">80 and 443</span></span>||  
|<span data-ttu-id="c1178-173">login.windows.net</span><span class="sxs-lookup"><span data-stu-id="c1178-173">login.windows.net</span></span>| <span data-ttu-id="c1178-174">80 和 443</span><span class="sxs-lookup"><span data-stu-id="c1178-174">80 and 443</span></span>||  


## <a name="connecting-operations-manager-toooms"></a><span data-ttu-id="c1178-175">連接 Operations Manager tooOMS</span><span class="sxs-lookup"><span data-stu-id="c1178-175">Connecting Operations Manager tooOMS</span></span>
<span data-ttu-id="c1178-176">執行一系列的步驟 tooconfigure 後 hello 您 Operations Manager 管理群組 tooconnect tooone 的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-176">Perform hello following series of steps tooconfigure your Operations Manager management group tooconnect tooone of your OMS workspaces.</span></span>

1. <span data-ttu-id="c1178-177">在 hello Operations Manager 主控台中，選取 hello**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-177">In hello Operations Manager console, select hello **Administration** workspace.</span></span>
2. <span data-ttu-id="c1178-178">展開 hello Operations Management Suite 節點，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="c1178-178">Expand hello Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="c1178-179">按一下 hello**註冊 tooOperations Management Suite**連結。</span><span class="sxs-lookup"><span data-stu-id="c1178-179">Click hello **Register tooOperations Management Suite** link.</span></span>
4. <span data-ttu-id="c1178-180">在 hello **Operations Management Suite 登入精靈： 驗證**頁面上，輸入 hello 電子郵件地址或電話號碼和您的 OMS 訂用帳戶，與相關聯的 hello 系統管理員帳戶的密碼，然後按一下**登入**。</span><span class="sxs-lookup"><span data-stu-id="c1178-180">On hello **Operations Management Suite Onboarding Wizard: Authentication** page, enter hello email address or phone number and password of hello administrator account that is associated with your OMS subscription, and click **Sign in**.</span></span>
5. <span data-ttu-id="c1178-181">您成功驗證，在 hello 之後**Operations Management Suite 登入精靈： 選取工作區**頁面上，會提示您 tooselect OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-181">After you are successfully authenticated, on hello **Operations Management Suite Onboarding Wizard: Select Workspace** page, you are prompted tooselect your OMS workspace.</span></span>  <span data-ttu-id="c1178-182">如果您有多個工作區中，選取 hello 您想 tooregister hello 下拉式清單中，從 hello Operations Manager 管理群組，然後按一下工作區**下一步**。</span><span class="sxs-lookup"><span data-stu-id="c1178-182">If you have more than one workspace, select hello workspace you want tooregister with hello Operations Manager management group from hello drop-down list, and then click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1178-183">Operations Manager 一次只支援一個 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-183">Operations Manager only supports one OMS workspace at a time.</span></span> <span data-ttu-id="c1178-184">hello 連接和已註冊的 tooOMS 與 hello 前一個工作區的 hello 電腦都會從 OMS 移除。</span><span class="sxs-lookup"><span data-stu-id="c1178-184">hello connection and hello computers that were registered tooOMS with hello previous workspace are removed from OMS.</span></span>
   > 
   > 
6. <span data-ttu-id="c1178-185">在 hello **Operations Management Suite 登入精靈： 摘要**頁面上，確認您的設定都正確無誤，如果按**建立**。</span><span class="sxs-lookup"><span data-stu-id="c1178-185">On hello **Operations Management Suite Onboarding Wizard: Summary** page, confirm your settings and if they are correct, click **Create**.</span></span>
7. <span data-ttu-id="c1178-186">在 hello **Operations Management Suite 登入精靈： 完成**頁面上，按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="c1178-186">On hello **Operations Management Suite Onboarding Wizard: Finish** page, click **Close**.</span></span>

### <a name="add-agent-managed-computers"></a><span data-ttu-id="c1178-187">加入代理程式所管理的電腦</span><span class="sxs-lookup"><span data-stu-id="c1178-187">Add agent-managed computers</span></span>
<span data-ttu-id="c1178-188">之後您可以設定整合的 OMS 工作區，這只會建立與 OMS 的連線，從 hello 代理程式回報 tooyour 管理群組收集任何資料。</span><span class="sxs-lookup"><span data-stu-id="c1178-188">After configuring integration with your OMS workspace, this only establishes a connection with OMS, no data is collected from hello agents reporting tooyour management group.</span></span> <span data-ttu-id="c1178-189">除非您設定特定代理程式管理的哪些電腦會收集 Log Analytics 的資料，否則不會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="c1178-189">This won’t happen until after you configure which specific agent-managed computers collects data for Log Analytics.</span></span> <span data-ttu-id="c1178-190">您可以個別選取 hello 電腦物件，或者您可以選取包含 Windows 電腦物件的群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-190">You can either select hello computer objects individually or you can select a group that contains Windows computer objects.</span></span> <span data-ttu-id="c1178-191">您無法選取包含另一個類別之執行個體 (例如邏輯磁碟或 SQL 資料庫) 的群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-191">You cannot select a group that  contains instances of another class, such as logical disks or SQL databases.</span></span>

1. <span data-ttu-id="c1178-192">開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-192">Open hello Operations Manager console and select hello **Administration** workspace.</span></span>
2. <span data-ttu-id="c1178-193">展開 hello Operations Management Suite 節點，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="c1178-193">Expand hello Operations Management Suite node and click **Connection**.</span></span>
3. <span data-ttu-id="c1178-194">按一下 hello**新增電腦/群組**底下 hello 動作連結上 hello 右邊 hello 窗格的標題。</span><span class="sxs-lookup"><span data-stu-id="c1178-194">Click hello **Add a Computer/Group** link under hello Actions heading on hello right-side of hello pane.</span></span>
4. <span data-ttu-id="c1178-195">在 hello**電腦搜尋**對話方塊中，您可以搜尋由 Operations Manager 監視電腦或群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-195">In hello **Computer Search** dialog box, you can search for computers or groups monitored by Operations Manager.</span></span> <span data-ttu-id="c1178-196">選取 電腦或群組 tooonboard tooOMS**新增**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="c1178-196">Select computers or groups tooonboard tooOMS, click **Add**, and then click **OK**.</span></span>

<span data-ttu-id="c1178-197">您可以檢視電腦和群組設定中 hello hello 受管理的電腦節點下 Operations Management Suite toocollect 資料**管理**hello Operations 主控台 工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-197">You can view computers and groups configured toocollect data from hello Managed Computers node under Operations Management Suite in hello **Administration** workspace of hello Operations console.</span></span>  <span data-ttu-id="c1178-198">您可以視需要在這裡新增或移除電腦和群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-198">From here, you can add or remove computers and groups as necessary.</span></span>

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a><span data-ttu-id="c1178-199">在 hello Operations 主控台中設定 OMS 的 proxy 設定</span><span class="sxs-lookup"><span data-stu-id="c1178-199">Configure OMS proxy settings in hello Operations console</span></span>
<span data-ttu-id="c1178-200">執行下列步驟，如果內部 proxy 伺服器 hello 管理群組與 OMS web 服務之間的 hello。</span><span class="sxs-lookup"><span data-stu-id="c1178-200">Perform hello following steps if an internal proxy server is between hello management group and OMS web service.</span></span>  <span data-ttu-id="c1178-201">這些設定都集中管理 hello 管理群組與 oms hello 領域 toocollect 資料中包含分散式的 tooagent 受管理的系統。</span><span class="sxs-lookup"><span data-stu-id="c1178-201">These settings are centrally managed from hello management group and distributed tooagent-managed systems that are included in hello scope toocollect data for OMS.</span></span>  <span data-ttu-id="c1178-202">這是有幫助的某些解決方案當許可 hello 管理伺服器和傳送資料，直接 tooOMS web 服務。</span><span class="sxs-lookup"><span data-stu-id="c1178-202">This is beneficial for when certain solutions bypass hello management server and send data directly tooOMS web service.</span></span>

1. <span data-ttu-id="c1178-203">開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-203">Open hello Operations Manager console and select hello **Administration** workspace.</span></span>
2. <span data-ttu-id="c1178-204">展開 Operations Management Suite，然後按一下連接 。</span><span class="sxs-lookup"><span data-stu-id="c1178-204">Expand Operations Management Suite, and then click **Connections**.</span></span>
3. <span data-ttu-id="c1178-205">在 hello OMS 連接 檢視中，按一下 **設定 Proxy 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="c1178-205">In hello OMS Connection view, click **Configure Proxy Server**.</span></span>
4. <span data-ttu-id="c1178-206">在**Operations Management Suite 精靈： Proxy 伺服器**頁面上，選取**使用 proxy 伺服器 tooaccess hello Operations Management Suite**，然後輸入 hello 與 hello 通訊埠編號，例如 http:// 的 URLcorpproxy:80，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="c1178-206">On **Operations Management Suite Wizard: Proxy Server** page, select **Use a proxy server tooaccess hello Operations Management Suite**, and then type hello URL with hello port number, for example, http://corpproxy:80 and then click **Finish**.</span></span>

<span data-ttu-id="c1178-207">如果您的 proxy 伺服器需要驗證，請執行 hello 下列步驟 tooconfigure 認證和需要 toopropagate toomanaged 電腦報告 tooOMS hello 管理群組中的設定。</span><span class="sxs-lookup"><span data-stu-id="c1178-207">If your proxy server requires authentication, perform hello following steps tooconfigure credentials and settings that need toopropagate toomanaged computers that reports tooOMS in hello management group.</span></span>

1. <span data-ttu-id="c1178-208">開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-208">Open hello Operations Manager console and select hello **Administration** workspace.</span></span>
2. <span data-ttu-id="c1178-209">在 [RunAs 組態] 底下，選取 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="c1178-209">Under **RunAs Configuration**, select **Profiles**.</span></span>
3. <span data-ttu-id="c1178-210">開啟 hello **System Center Advisor 執行身分設定檔 Proxy**設定檔。</span><span class="sxs-lookup"><span data-stu-id="c1178-210">Open hello **System Center Advisor Run As Profile Proxy** profile.</span></span>
4. <span data-ttu-id="c1178-211">在 hello 執行身分設定檔精靈 中，按一下 新增 toouse 的執行身分帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1178-211">In hello Run As Profile Wizard, click Add toouse a Run As account.</span></span> <span data-ttu-id="c1178-212">您可以建立[執行身分帳戶](https://technet.microsoft.com/library/hh321655.aspx)，或使用現有的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c1178-212">You can create a [Run As account](https://technet.microsoft.com/library/hh321655.aspx) or use an existing account.</span></span> <span data-ttu-id="c1178-213">此帳戶必須 toohave 足夠的權限 toopass 透過 hello proxy 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c1178-213">This account needs toohave sufficient permissions toopass through hello proxy server.</span></span>
5. <span data-ttu-id="c1178-214">tooset hello 帳戶 toomanage 中，選擇 **選取的類別、 群組或物件**，按一下 **選取...**</span><span class="sxs-lookup"><span data-stu-id="c1178-214">tooset hello account toomanage, choose **A selected class, group, or object**, click **Select…**</span></span> <span data-ttu-id="c1178-215">然後按一下群組…</span><span class="sxs-lookup"><span data-stu-id="c1178-215">and then click **Group…**</span></span> <span data-ttu-id="c1178-216">tooopen hello**群組搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="c1178-216">tooopen hello **Group Search** box.</span></span>
6. <span data-ttu-id="c1178-217">搜尋，然後選取 [Microsoft System Center Advisor 監控伺服器群組] 。</span><span class="sxs-lookup"><span data-stu-id="c1178-217">Search for and then select **Microsoft System Center Advisor Monitoring Server Group**.</span></span>  <span data-ttu-id="c1178-218">按一下**確定**選取 hello 群組 tooclose hello 之後**群組搜尋**方塊。</span><span class="sxs-lookup"><span data-stu-id="c1178-218">Click **OK** after selecting hello group tooclose hello **Group Search** box.</span></span>
7. <span data-ttu-id="c1178-219">按一下**確定**tooclose hello**新增執行身分帳戶**方塊。</span><span class="sxs-lookup"><span data-stu-id="c1178-219">Click **OK** tooclose hello **Add a Run As account** box.</span></span>
8. <span data-ttu-id="c1178-220">按一下**儲存**toocomplete hello 精靈並儲存變更。</span><span class="sxs-lookup"><span data-stu-id="c1178-220">Click **Save** toocomplete hello wizard and save your changes.</span></span>

<span data-ttu-id="c1178-221">建立 hello 連線，而且您設定的代理程式會收集和報告資料 tooOMS 之後，hello 下列組態會套用在 hello 管理群組中，不一定會依照順序：</span><span class="sxs-lookup"><span data-stu-id="c1178-221">After hello connection is created and you configure which agents will collect and report data tooOMS, hello following configuration is applied in hello management group, not necessarily in order:</span></span>

* <span data-ttu-id="c1178-222">執行身分帳戶 hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate**建立。</span><span class="sxs-lookup"><span data-stu-id="c1178-222">hello Run As Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** is created.</span></span>  <span data-ttu-id="c1178-223">相關聯的執行身分設定檔 hello **Microsoft System Center Advisor 執行做為設定檔 Blob**和目標設定為兩個類別-**集合伺服器**和**Operations Manager 管理群組**.</span><span class="sxs-lookup"><span data-stu-id="c1178-223">It is associated with hello Run As profile **Microsoft System Center Advisor Run As Profile Blob** and is targeting two classes - **Collection Server** and **Operations Manager Management Group**.</span></span>
* <span data-ttu-id="c1178-224">會建立兩個連接器。</span><span class="sxs-lookup"><span data-stu-id="c1178-224">Two connectors are created.</span></span>  <span data-ttu-id="c1178-225">第一次命名 hello **Microsoft.SystemCenter.Advisor.DataConnector**並會自動設定轉寄 hello 管理群組 tooOMS 記錄檔中的所有類別的執行個體所產生的所有警示的訂閱分析。</span><span class="sxs-lookup"><span data-stu-id="c1178-225">hello first is named **Microsoft.SystemCenter.Advisor.DataConnector** and is automatically configured with a subscription that forwards all alerts generated from instances of all classes in hello management group tooOMS Log Analytics.</span></span> <span data-ttu-id="c1178-226">hello 第二個連接器**Advisor 連接器**，這是負責與 OMS web 服務通訊以及共用資料。</span><span class="sxs-lookup"><span data-stu-id="c1178-226">hello second connector is **Advisor Connector**, which is responsible for communicating with OMS web service and sharing data.</span></span>
* <span data-ttu-id="c1178-227">代理程式和確定您已選取 toocollect 資料 hello 管理群組中的群組會加入 toohello **Microsoft System Center Advisor 監控伺服器群組**。</span><span class="sxs-lookup"><span data-stu-id="c1178-227">Agents and groups that you have selected toocollect data in hello management group is added toohello **Microsoft System Center Advisor Monitoring Server Group**.</span></span>

## <a name="management-pack-updates"></a><span data-ttu-id="c1178-228">管理組件更新</span><span class="sxs-lookup"><span data-stu-id="c1178-228">Management pack updates</span></span>
<span data-ttu-id="c1178-229">設定完成之後，hello Operations Manager 管理群組會建立與 hello OMS 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="c1178-229">After configuration is completed, hello Operations Manager management group establishes a connection with hello OMS service.</span></span>  <span data-ttu-id="c1178-230">hello 管理伺服器與 hello web 服務同步處理，並以您已啟用與 Operations Manager 整合的 hello 解決方案的管理組件的 hello 格式接收更新的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="c1178-230">hello management server synchronizes with hello web service and receive updated configuration information in hello form of management packs for hello solutions you have enabled that integrate with Operations Manager.</span></span>   <span data-ttu-id="c1178-231">Operations Manager 會檢查這些管理組件的更新，如果有更新，就會自動下載並匯入。</span><span class="sxs-lookup"><span data-stu-id="c1178-231">Operations Manager  checks for updates of these management packs and automatically download and imports them when they’re available.</span></span>  <span data-ttu-id="c1178-232">有兩個規則特別可控制這個行為︰</span><span class="sxs-lookup"><span data-stu-id="c1178-232">There are two rules in particular which control this behavior:</span></span>

* <span data-ttu-id="c1178-233">**Microsoft.SystemCenter.Advisor.MPUpdate** -hello 基底的 OMS 管理套件會更新。</span><span class="sxs-lookup"><span data-stu-id="c1178-233">**Microsoft.SystemCenter.Advisor.MPUpdate** - Updates hello base OMS management packs.</span></span> <span data-ttu-id="c1178-234">預設會每 12 小時執行一次。</span><span class="sxs-lookup"><span data-stu-id="c1178-234">Runs every 12 hours by default.</span></span>
* <span data-ttu-id="c1178-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - 更新工作區中所啟用的解決方案管理組件。</span><span class="sxs-lookup"><span data-stu-id="c1178-235">**Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Updates solution management packs enabled in your workspace.</span></span> <span data-ttu-id="c1178-236">預設會每五 (5) 分鐘執行一次。</span><span class="sxs-lookup"><span data-stu-id="c1178-236">Runs every five (5) minutes by default.</span></span>

<span data-ttu-id="c1178-237">您可以覆寫 tooeither 停用它們，以防止自動下載這兩個規則，或修改 hello 頻率 hello 管理同步處理伺服器與 OMS toodetermine 如果新的管理組件可用，且應下載的頻率。</span><span class="sxs-lookup"><span data-stu-id="c1178-237">You can override these two rules tooeither prevent automatic download by disabling them, or modify hello frequency for how often hello management server synchronizes with OMS toodetermine if a new management pack is available and should be downloaded.</span></span>  <span data-ttu-id="c1178-238">請依照下列步驟 hello[如何 tooOverride 規則或監視](https://technet.microsoft.com/library/hh212869.aspx)toomodify hello**頻率**參數的值，以秒為單位 toochange hello 同步處理排程，或修改 hello**已啟用**參數 toodisable hello 規則。</span><span class="sxs-lookup"><span data-stu-id="c1178-238">Follow hello steps [How tooOverride a Rule or Monitor](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **Frequency** parameter with a value in seconds toochange hello synchronization schedule, or modify hello **Enabled** parameter toodisable hello rules.</span></span>  <span data-ttu-id="c1178-239">目標 hello 會覆寫 tooall 類別物件的 Operations Manager 管理群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-239">Target hello overrides tooall objects of class Operations Manager Management Group.</span></span>

<span data-ttu-id="c1178-240">如果您想 toocontinue 遵循現有的變更控制程序來控制生產管理群組中的管理組件版本，您可以停用 hello 規則，並讓它們可在指定時間允許更新。</span><span class="sxs-lookup"><span data-stu-id="c1178-240">If you want toocontinue following your existing change control process for controlling management pack releases in your production management group, you can disable hello rules and enable them during specific times when updates are allowed.</span></span> <span data-ttu-id="c1178-241">如果您環境中有開發或 QA 管理群組，而且它有連線能力 toohello 網際網路，您可以設定該管理群組與 OMS 工作區 toosupport 這種情況。</span><span class="sxs-lookup"><span data-stu-id="c1178-241">If you have a development or QA management group in your environment and it has connectivity toohello Internet, you can configure that management group with an OMS workspace toosupport this scenario.</span></span>  <span data-ttu-id="c1178-242">這可讓您 tooreview，並將其發佈至您的生產管理群組之前進行評估 hello 反覆 hello OMS 管理套件版本。</span><span class="sxs-lookup"><span data-stu-id="c1178-242">This allows you tooreview and evaluate hello iterative releases of hello OMS management packs before releasing them into your production management group.</span></span>

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a><span data-ttu-id="c1178-243">切換 Operations Manager 群組 tooa 新 OMS 工作區</span><span class="sxs-lookup"><span data-stu-id="c1178-243">Switch an Operations Manager group tooa new OMS Workspace</span></span>
1. <span data-ttu-id="c1178-244">登入 tooyour OMS 訂用帳戶，並建立工作區中的[Microsoft Operations Management Suite](http://oms.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="c1178-244">Log in tooyour OMS subscription and create a workspace in [Microsoft Operations Management Suite](http://oms.microsoft.com/).</span></span>
2. <span data-ttu-id="c1178-245">選取 hello hello Operations Manager 系統管理員角色的成員的帳戶開啟 hello Operations Manager 主控台**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-245">Open hello Operations Manager console with an account that is a member of hello Operations Manager Administrators role and select hello **Administration** workspace.</span></span>
3. <span data-ttu-id="c1178-246">展開 Operations Management Suite，選取 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="c1178-246">Expand Operations Management Suite, and select **Connections**.</span></span>
4. <span data-ttu-id="c1178-247">選取 hello**重新設定作業 Management Suite** hello 中介層 hello 窗格的一邊上的連結。</span><span class="sxs-lookup"><span data-stu-id="c1178-247">Select hello **Re-configure Operation Management Suite** link on hello middle-side of hello pane.</span></span>
5. <span data-ttu-id="c1178-248">請遵循 hello **Operations Management Suite 登入精靈**，然後輸入 hello 電子郵件地址或電話號碼和 hello 與新的 OMS 工作區相關聯的系統管理員帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="c1178-248">Follow hello **Operations Management Suite Onboarding Wizard** and enter hello email address or phone number and password of hello administrator account that is associated with your new OMS workspace.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c1178-249">hello **Operations Management Suite 登入精靈： 選取工作區**頁面會顯示使用中的 hello 現有工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-249">hello **Operations Management Suite Onboarding Wizard: Select Workspace** page presents hello existing workspace that is in use.</span></span>
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a><span data-ttu-id="c1178-250">驗證 Operations Manager 與 OMS 的整合</span><span class="sxs-lookup"><span data-stu-id="c1178-250">Validate Operations Manager Integration with OMS</span></span>
<span data-ttu-id="c1178-251">有幾個不同的方式，您可以確認您的 OMS tooOperations Manager 整合成功。</span><span class="sxs-lookup"><span data-stu-id="c1178-251">There are a few different ways you can verify that your OMS tooOperations Manager integration is successful.</span></span>

### <a name="tooconfirm-integration-from-hello-oms-portal"></a><span data-ttu-id="c1178-252">tooconfirm 整合，從 hello OMS 入口網站</span><span class="sxs-lookup"><span data-stu-id="c1178-252">tooconfirm integration from hello OMS portal</span></span>
1. <span data-ttu-id="c1178-253">在 hello OMS 入口網站中，按一下 hello**設定**磚</span><span class="sxs-lookup"><span data-stu-id="c1178-253">In hello OMS portal, click hello **Settings** tile</span></span>
2. <span data-ttu-id="c1178-254">選取 [連接的來源]。</span><span class="sxs-lookup"><span data-stu-id="c1178-254">Select  **Connected Sources**.</span></span>
3. <span data-ttu-id="c1178-255">在 hello 資料表 hello System Center Operations Manager 一節，您應該會看到 hello hello 管理群組名稱的前次收到資料時，與 hello 數目的代理程式和一起列出。</span><span class="sxs-lookup"><span data-stu-id="c1178-255">In hello table under hello System Center Operations Manager section, you should see hello name of hello management group listed with hello number of agents and status when data was last received.</span></span>
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. <span data-ttu-id="c1178-257">請注意 hello**工作區識別碼**下 hello 左方 hello 設定頁面的值。</span><span class="sxs-lookup"><span data-stu-id="c1178-257">Note hello **Workspace ID** value under hello left-side of hello Settings page.</span></span>  <span data-ttu-id="c1178-258">以下您將根據 Operations Manager 管理群組來驗證此值。</span><span class="sxs-lookup"><span data-stu-id="c1178-258">You validate it against your Operations Manager management group below.</span></span>  

### <a name="tooconfirm-integration-from-hello-operations-console"></a><span data-ttu-id="c1178-259">從 hello Operations 主控台 tooconfirm 整合</span><span class="sxs-lookup"><span data-stu-id="c1178-259">tooconfirm integration from hello Operations console</span></span>
1. <span data-ttu-id="c1178-260">開啟 hello Operations Manager 主控台並選取 hello**管理**工作區。</span><span class="sxs-lookup"><span data-stu-id="c1178-260">Open hello Operations Manager console and select hello **Administration** workspace.</span></span>
2. <span data-ttu-id="c1178-261">選取**管理組件**在 hello**尋找：**文字方塊中輸入**Advisor**或**智慧**。</span><span class="sxs-lookup"><span data-stu-id="c1178-261">Select **Management Packs** and in hello **Look for:** text box type **Advisor** or **Intelligence**.</span></span>
3. <span data-ttu-id="c1178-262">根據您已啟用的 hello 解決方案，您會看到 hello 搜尋結果中列出的對應管理組件。</span><span class="sxs-lookup"><span data-stu-id="c1178-262">Depending on hello solutions you have enabled, you see a corresponding management pack listed in hello search results.</span></span>  <span data-ttu-id="c1178-263">例如，如果您已啟用 hello 警示管理解決方案，hello 管理組件 Microsoft System Center Advisor 警示管理是 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="c1178-263">For example, if you have enabled hello Alert Management solution, hello management pack Microsoft System Center Advisor Alert Management is in hello list.</span></span>
4. <span data-ttu-id="c1178-264">從 hello**監視**檢視中，瀏覽 toohello **Operations 管理 Suite\Health 狀態**檢視。</span><span class="sxs-lookup"><span data-stu-id="c1178-264">From hello **Monitoring** view, navigate toohello **Operations Management Suite\Health State** view.</span></span>  <span data-ttu-id="c1178-265">選取管理伺服器在 hello **Management Server 狀態** 窗格中，在 hello**詳細資料檢視**窗格確認屬性的 hello 值**驗證服務 URI**符合 hello OMS 工作區識別碼。</span><span class="sxs-lookup"><span data-stu-id="c1178-265">Select a Management server under hello **Management Server State** pane, and in hello **Detail View** pane confirm hello value for property **Authentication service URI** matches hello OMS Workspace ID.</span></span>
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a><span data-ttu-id="c1178-267">移除與 OMS 的整合</span><span class="sxs-lookup"><span data-stu-id="c1178-267">Remove Integration with OMS</span></span>
<span data-ttu-id="c1178-268">當您不再需要您的 Operations Manager 管理群組與 OMS 工作區之間的整合時，有數個必要步驟 tooproperly 移除 hello 連線和 hello 管理群組中的組態。</span><span class="sxs-lookup"><span data-stu-id="c1178-268">When you no longer require integration between your Operations Manager management group and OMS workspace, there are several steps required tooproperly remove hello connection and configuration in hello management group.</span></span> <span data-ttu-id="c1178-269">hello 下列程序，您已刪除的管理群組的 hello 參考更新您的 OMS 工作區，刪除 hello OMS 連接器，然後再刪除管理組件支援 OMS。</span><span class="sxs-lookup"><span data-stu-id="c1178-269">hello following procedure has you update your OMS workspace by deleting hello reference of your management group, delete hello OMS connectors, and then delete management packs supporting OMS.</span></span>   

<span data-ttu-id="c1178-270">您已啟用與 Operations Manager 整合的 hello 解決方案的管理組件和 hello 管理組件以 hello OMS 服務的必要的 toosupport 整合無法輕鬆地從 hello 管理群組刪除。</span><span class="sxs-lookup"><span data-stu-id="c1178-270">Management packs for hello solutions you have enabled that integrate with Operations Manager and hello management packs required toosupport integration with hello OMS service cannot be easily deleted from hello management group.</span></span>  <span data-ttu-id="c1178-271">這是因為某些 hello OMS 管理套件的其他相關的管理組件相依性。</span><span class="sxs-lookup"><span data-stu-id="c1178-271">This is because some of hello OMS management packs have dependencies on other related management packs.</span></span>  <span data-ttu-id="c1178-272">toodelete 管理組件，因為相依於其他管理組件中，下載 hello 指令碼[移除相依性的管理組件](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e)從 TechNet 指令碼中心。</span><span class="sxs-lookup"><span data-stu-id="c1178-272">toodelete management packs having a dependency on other management packs, download hello script [remove a management pack with dependencies](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) from TechNet Script Center.</span></span>  

1. <span data-ttu-id="c1178-273">Hello Operations Manager 系統管理員角色的成員的帳戶開啟 Operations Manager 命令殼層 hello。</span><span class="sxs-lookup"><span data-stu-id="c1178-273">Open hello Operations Manager Command Shell with an account that is a member of hello Operations Manager Administrators role.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="c1178-274">請確認您沒有任何自訂的管理組件 hello word Advisor 或 IntelligencePack hello 名稱，再繼續進行，否則 hello 步驟 hello 管理群組中刪除它們。</span><span class="sxs-lookup"><span data-stu-id="c1178-274">Verify you do not have any custom management packs with hello word Advisor or IntelligencePack in hello name before proceeding, otherwise hello following steps delete them from hello management group.</span></span>
    > 

2. <span data-ttu-id="c1178-275">Hello 命令殼層提示字元中輸入`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="c1178-275">From hello command shell prompt, type `Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
3. <span data-ttu-id="c1178-276">接著輸入 `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span><span class="sxs-lookup"><span data-stu-id="c1178-276">Next type, `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`</span></span>
4. <span data-ttu-id="c1178-277">tooremove 任何管理組件，剩餘的有相依的其他 System Center Advisor 管理組件，請使用 hello 指令碼*RecursiveRemove.ps1*您從先前 hello TechNet 指令碼中心下載。</span><span class="sxs-lookup"><span data-stu-id="c1178-277">tooremove any management packs remaining which have a dependency on other System Center Advisor management packs, use hello script *RecursiveRemove.ps1* you downloaded from hello TechNet Script Center earlier.</span></span>  
 
    > [!NOTE]
    > <span data-ttu-id="c1178-278">請勿刪除 hello Microsoft System Center Advisor 或 Microsoft System Center 內部 Advisor 管理組件。</span><span class="sxs-lookup"><span data-stu-id="c1178-278">Do not delete hello Microsoft System Center Advisor or Microsoft System Center Advisor Internal management packs.</span></span>  
    >  

5. <span data-ttu-id="c1178-279">Hello Operations Manager 系統管理員角色成員的帳戶開啟 hello Operations Manager Operations 主控台。</span><span class="sxs-lookup"><span data-stu-id="c1178-279">Open hello Operations Manager Operations console with an account that is a member of hello Operations Manager Administrators role.</span></span>
6. <span data-ttu-id="c1178-280">在下**管理**，選取 hello**管理組件**節點在 hello**尋找：**方塊中，輸入**Advisor**並確認 hello下列管理組件仍會匯入管理群組：</span><span class="sxs-lookup"><span data-stu-id="c1178-280">Under **Administration**, select hello **Management Packs** node and in hello **Look for:** box, type **Advisor** and verify hello following management packs are still imported in your management group:</span></span>
   
   * <span data-ttu-id="c1178-281">Microsoft System Center Advisor</span><span class="sxs-lookup"><span data-stu-id="c1178-281">Microsoft System Center Advisor</span></span>
   * <span data-ttu-id="c1178-282">Microsoft System Center Advisor Internal</span><span class="sxs-lookup"><span data-stu-id="c1178-282">Microsoft System Center Advisor Internal</span></span>
7. <span data-ttu-id="c1178-283">在 hello OMS 入口網站中，按一下 hello**設定**磚。</span><span class="sxs-lookup"><span data-stu-id="c1178-283">In hello OMS portal, click hello **Settings** tile.</span></span>
8. <span data-ttu-id="c1178-284">選取 [連接的來源] 。</span><span class="sxs-lookup"><span data-stu-id="c1178-284">Select **Connected Sources**.</span></span>
9. <span data-ttu-id="c1178-285">在 System Center Operations Manager 區段 hello hello 資料表，您應該會看到 hello 名稱要 tooremove hello 工作區中的 hello 管理群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-285">In hello table under hello System Center Operations Manager section, you should see hello name of hello management group you want tooremove from hello workspace.</span></span>  <span data-ttu-id="c1178-286">Hello] 欄下方**最後一筆資料**，按一下 [**移除**。</span><span class="sxs-lookup"><span data-stu-id="c1178-286">Under hello column **Last Data**, click **Remove**.</span></span>  
   
    > [!NOTE]
    > <span data-ttu-id="c1178-287">hello**移除**連結將無法使用之前在 14 天後如果沒有偵測到從 hello 連線的管理群組的活動。</span><span class="sxs-lookup"><span data-stu-id="c1178-287">hello **Remove** link will not be available until after 14 days if there is no activity detected from hello connected management group.</span></span>  
    > 

10. <span data-ttu-id="c1178-288">會出現一個視窗，詢問您想要移除 hello tooproceed tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="c1178-288">A window will appear asking you tooconfirm that you want tooproceed with hello removal.</span></span>  <span data-ttu-id="c1178-289">按一下**是**tooproceed。</span><span class="sxs-lookup"><span data-stu-id="c1178-289">Click **Yes** tooproceed.</span></span> 

<span data-ttu-id="c1178-290">toodelete hello 兩個連接器-Microsoft.SystemCenter.Advisor.DataConnector 和 Advisor 連接器、 儲存 hello tooyour 電腦以下的 PowerShell 指令碼及執行使用 hello 遵循範例：</span><span class="sxs-lookup"><span data-stu-id="c1178-290">toodelete hello two connectors - Microsoft.SystemCenter.Advisor.DataConnector and Advisor Connector, save hello PowerShell script below tooyour computer and execute using hello following examples:</span></span>

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> <span data-ttu-id="c1178-291">hello 電腦執行此指令碼，如果不是管理伺服器，應該根據 hello 版本的管理群組安裝 hello Operations Manager 命令殼層。</span><span class="sxs-lookup"><span data-stu-id="c1178-291">hello computer you run this script from, if not a management server, should have hello Operations Manager command shell installed depending on hello version of your management group.</span></span>
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
    # Configures a connector with hello specified name.
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
    # Removes a connector with hello specified name.
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

<span data-ttu-id="c1178-292">在未來的 hello 如果您計劃重新連線管理群組 tooan OMS 工作區，您的需要 toore 匯入 hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` hello 最新的更新彙總從管理組件檔案套用 tooyour 管理群組。</span><span class="sxs-lookup"><span data-stu-id="c1178-292">In hello future if you plan on reconnecting your management group tooan OMS workspace, you  need toore-import hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack file from hello most recent update rollup applied tooyour management group.</span></span>  <span data-ttu-id="c1178-293">您可以找到此檔案在 hello`%ProgramFiles%\Microsoft System Center 2012`或 hello`System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups`資料夾。</span><span class="sxs-lookup"><span data-stu-id="c1178-293">You can find this file in hello `%ProgramFiles%\Microsoft System Center 2012` or hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1178-294">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1178-294">Next steps</span></span>
<span data-ttu-id="c1178-295">tooadd 功能和收集資料，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="c1178-295">tooadd functionality and gather data, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>


