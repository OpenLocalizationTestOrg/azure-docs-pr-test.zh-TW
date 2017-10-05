---
title: "Azure Log Analytics 中的 DNS 分析解決方案 | Microsoft Docs"
description: "在 Log Analytics 中設定並使用 DNS 分析解決方案，以收集關於 DNS 基礎結構在安全性、效能及作業方面的深入解析。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 0e8fc0ffb8e0d0bdf00bea46594fe050c00b6c8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-the-dns-analytics-preview-solution"></a><span data-ttu-id="4881f-103">收集搭配 DNS 分析預覽版解決方案使用 DNS 基礎結構的深入解析</span><span class="sxs-lookup"><span data-stu-id="4881f-103">Gather insights about your DNS infrastructure with the DNS Analytics Preview solution</span></span>

![DNS 分析符號](./media/log-analytics-dns/dns-analytics-symbol.png)

<span data-ttu-id="4881f-105">本文描述如何在 Log Analytics 中設定並使用 Azure DNS 分析解決方案，以收集關於 Azure DNS 基礎結構在安全性、效能及作業方面的深入解析。</span><span class="sxs-lookup"><span data-stu-id="4881f-105">This article describes how to set up and use the Azure DNS Analytics solution in Azure Log Analytics to gather insights into DNS infrastructure on security, performance, and operations.</span></span>

<span data-ttu-id="4881f-106">DNS 分析可協助您︰</span><span class="sxs-lookup"><span data-stu-id="4881f-106">DNS Analytics helps you to:</span></span>

- <span data-ttu-id="4881f-107">指出嘗試解析惡意網域名稱的用戶端。</span><span class="sxs-lookup"><span data-stu-id="4881f-107">Identify clients that try to resolve malicious domain names.</span></span>
- <span data-ttu-id="4881f-108">指出過時的資源記錄。</span><span class="sxs-lookup"><span data-stu-id="4881f-108">Identify stale resource records.</span></span>
- <span data-ttu-id="4881f-109">指出經常查詢的網域名稱和 Talkative DNS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4881f-109">Identify frequently queried domain names and talkative DNS clients.</span></span>
- <span data-ttu-id="4881f-110">檢視 DNS 伺服器上的要求負載。</span><span class="sxs-lookup"><span data-stu-id="4881f-110">View request load on DNS servers.</span></span>
- <span data-ttu-id="4881f-111">檢視動態 DNS 註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="4881f-111">View dynamic DNS registration failures.</span></span>

<span data-ttu-id="4881f-112">此解決方案會收集、分析 Windows DNS 分析和稽核記錄，並將它與 DNS 伺服器中的其他相關資料關聯。</span><span class="sxs-lookup"><span data-stu-id="4881f-112">The solution collects, analyzes, and correlates Windows DNS analytic and audit logs and other related data from your DNS servers.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="4881f-113">連接的來源</span><span class="sxs-lookup"><span data-stu-id="4881f-113">Connected sources</span></span>

<span data-ttu-id="4881f-114">下表描述此方案支援的連線來源：</span><span class="sxs-lookup"><span data-stu-id="4881f-114">The following table describes the connected sources that are supported by this solution:</span></span>

| <span data-ttu-id="4881f-115">**連線的來源**</span><span class="sxs-lookup"><span data-stu-id="4881f-115">**Connected source**</span></span> | <span data-ttu-id="4881f-116">**支援**</span><span class="sxs-lookup"><span data-stu-id="4881f-116">**Support**</span></span> | <span data-ttu-id="4881f-117">**說明**</span><span class="sxs-lookup"><span data-stu-id="4881f-117">**Description**</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4881f-118">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="4881f-118">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="4881f-119">是</span><span class="sxs-lookup"><span data-stu-id="4881f-119">Yes</span></span> | <span data-ttu-id="4881f-120">此解決方案會收集來自 Windows 代理程式的 DNS 資訊。</span><span class="sxs-lookup"><span data-stu-id="4881f-120">The solution collects DNS information from Windows agents.</span></span> |
| [<span data-ttu-id="4881f-121">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="4881f-121">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="4881f-122">否</span><span class="sxs-lookup"><span data-stu-id="4881f-122">No</span></span> | <span data-ttu-id="4881f-123">此解決方案不會收集來自直接 Linux 代理程式的 DNS 資訊。</span><span class="sxs-lookup"><span data-stu-id="4881f-123">The solution does not collect DNS information from direct Linux agents.</span></span> |
| [<span data-ttu-id="4881f-124">System Center Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="4881f-124">System Center Operations Manager management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="4881f-125">是</span><span class="sxs-lookup"><span data-stu-id="4881f-125">Yes</span></span> | <span data-ttu-id="4881f-126">此解決方案會收集來自連線 Operations Manager 管理群組的代理程式之中的 DNS 資訊。</span><span class="sxs-lookup"><span data-stu-id="4881f-126">The solution collects DNS information from agents in a connected Operations Manager management group.</span></span> <span data-ttu-id="4881f-127">Operations Manager 代理程式不需要直接連線到 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="4881f-127">A direct connection from the Operations Manager agent to the Operations Management Suite is not required.</span></span> <span data-ttu-id="4881f-128">資料會從管理群組轉送至 Operations Management Suite 存放庫。</span><span class="sxs-lookup"><span data-stu-id="4881f-128">Data is forwarded from the management group to the Operations Management Suite repository.</span></span> |
| [<span data-ttu-id="4881f-129">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4881f-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="4881f-130">否</span><span class="sxs-lookup"><span data-stu-id="4881f-130">No</span></span> | <span data-ttu-id="4881f-131">此解決方案沒有使用 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4881f-131">Azure storage isn't used by the solution.</span></span> |

### <a name="data-collection-details"></a><span data-ttu-id="4881f-132">資料收集詳細資料</span><span class="sxs-lookup"><span data-stu-id="4881f-132">Data collection details</span></span>

<span data-ttu-id="4881f-133">此解決方案會從已安裝 Log Analytics 代理程式的 DNS 伺服器收集 DNS 清查和 DNS 事件相關資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-133">The solution collects DNS inventory and DNS event-related data from the DNS servers where a Log Analytics agent is installed.</span></span> <span data-ttu-id="4881f-134">這項資料會再上傳至 Log Analytics，並顯示在解決方案儀表板中。</span><span class="sxs-lookup"><span data-stu-id="4881f-134">This data is then uploaded to Log Analytics and displayed in the solution dashboard.</span></span> <span data-ttu-id="4881f-135">清查相關資料 (例如 DNS 伺服器數目、區域和資源記錄) 的收集方式是執行 DNS PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4881f-135">Inventory-related data, such as the number of DNS servers, zones, and resource records, is collected by running the DNS PowerShell cmdlets.</span></span> <span data-ttu-id="4881f-136">此資料每兩天會更新一次。</span><span class="sxs-lookup"><span data-stu-id="4881f-136">The data is updated once every two days.</span></span> <span data-ttu-id="4881f-137">事件相關資料是以接近即時的方式，從 Windows Server 2012 R2 增強的 DNS 記錄與診斷功能所提供的[分析和稽核記錄](https://technet.microsoft.com/library/dn800669.aspx#enhanc)進行收集。</span><span class="sxs-lookup"><span data-stu-id="4881f-137">The event-related data is collected near real time from the [analytic and audit logs](https://technet.microsoft.com/library/dn800669.aspx#enhanc) provided by enhanced DNS logging and diagnostics in Windows Server 2012 R2.</span></span>

## <a name="configuration"></a><span data-ttu-id="4881f-138">組態</span><span class="sxs-lookup"><span data-stu-id="4881f-138">Configuration</span></span>

<span data-ttu-id="4881f-139">請使用下列資訊來設定此解決方案：</span><span class="sxs-lookup"><span data-stu-id="4881f-139">Use the following information to configure the solution:</span></span>

- <span data-ttu-id="4881f-140">在每部要監視的 DNS 伺服器上，都必須安裝 [Windows](log-analytics-windows-agents.md) 或 [Operations Manager](log-analytics-om-agents.md) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="4881f-140">You must have a [Windows](log-analytics-windows-agents.md) or [Operations Manager](log-analytics-om-agents.md) agent on each DNS server that you want to monitor.</span></span>
- <span data-ttu-id="4881f-141">您可以從 [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace) 將 DNS 分析解決方案新增至您的 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="4881f-141">You can add the DNS Analytics solution to your Operations Management Suite workspace from the [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace).</span></span> <span data-ttu-id="4881f-142">您也可以使用[從方案庫新增 Log Analytics 解決方案](log-analytics-add-solutions.md)中所述的程序。</span><span class="sxs-lookup"><span data-stu-id="4881f-142">You can also use the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="4881f-143">不需要進一步設定，此解決方案就會開始收集資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-143">The solution starts collecting data without the need of further configuration.</span></span> <span data-ttu-id="4881f-144">不過，您可以使用下列組態來自訂資料收集。</span><span class="sxs-lookup"><span data-stu-id="4881f-144">However, you can use the following configuration to customize data collection.</span></span>

### <a name="configure-the-solution"></a><span data-ttu-id="4881f-145">設定方案</span><span class="sxs-lookup"><span data-stu-id="4881f-145">Configure the solution</span></span>

<span data-ttu-id="4881f-146">在解決方案儀表板中，按一下 [組態] 以開啟 [DNS 分析組態] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4881f-146">On the solution dashboard, click **Configuration** to open the DNS Analytics Configuration page.</span></span> <span data-ttu-id="4881f-147">您可以進行兩種類型的組態變更︰</span><span class="sxs-lookup"><span data-stu-id="4881f-147">There are two types of configuration changes that you can make:</span></span>

- <span data-ttu-id="4881f-148">**列入白名單的網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="4881f-148">**Whitelisted Domain Names**.</span></span> <span data-ttu-id="4881f-149">該解決方案不會處理所有查閱查詢。</span><span class="sxs-lookup"><span data-stu-id="4881f-149">The solution does not process all the lookup queries.</span></span> <span data-ttu-id="4881f-150">它會維護一份網域名稱尾碼的白名單。</span><span class="sxs-lookup"><span data-stu-id="4881f-150">It maintains a whitelist of domain name suffixes.</span></span> <span data-ttu-id="4881f-151">若查閱查詢解析為符合此白名單中之網域名稱尾碼的網域名稱，此解決方案就不會處理它們。</span><span class="sxs-lookup"><span data-stu-id="4881f-151">The lookup queries that resolve to the domain names that match domain name suffixes in this whitelist are not processed by the solution.</span></span> <span data-ttu-id="4881f-152">不處理列入白名單的網域名稱，有助於最佳化傳送至 Log Analytics 的資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-152">Not processing whitelisted domain names helps to optimize the data sent to Log Analytics.</span></span> <span data-ttu-id="4881f-153">預設白名單包含熱門的公用網域名稱，例如 www.google.com 和 www.facebook.com。</span><span class="sxs-lookup"><span data-stu-id="4881f-153">The default whitelist includes popular public domain names, such as www.google.com and www.facebook.com.</span></span> <span data-ttu-id="4881f-154">您可以捲動來檢視完整的預設清單。</span><span class="sxs-lookup"><span data-stu-id="4881f-154">You can view the complete default list by scrolling.</span></span>

 <span data-ttu-id="4881f-155">您可以修改清單，將您想要檢視查閱深入解析的任何網域名稱尾碼加以新增。</span><span class="sxs-lookup"><span data-stu-id="4881f-155">You can modify the list to add any domain name suffix that you want to view lookup insights for.</span></span> <span data-ttu-id="4881f-156">您也可以將您不想要檢視查閱深入解析的任何網域名稱尾碼加以移除。</span><span class="sxs-lookup"><span data-stu-id="4881f-156">You can also remove any domain name suffix that you don't want to view lookup insights for.</span></span>

- <span data-ttu-id="4881f-157">**Talkative 用戶端閾值**。</span><span class="sxs-lookup"><span data-stu-id="4881f-157">**Talkative Client Threshold**.</span></span> <span data-ttu-id="4881f-158">超過查閱要求數目閾值的 DNS 用戶端，在 [DNS 用戶端] 刀鋒視窗中會反白顯示。</span><span class="sxs-lookup"><span data-stu-id="4881f-158">DNS clients that exceed the threshold for the number of lookup requests are highlighted in the **DNS Clients** blade.</span></span> <span data-ttu-id="4881f-159">預設閾值為 1,000。</span><span class="sxs-lookup"><span data-stu-id="4881f-159">The default threshold is 1,000.</span></span> <span data-ttu-id="4881f-160">您可以編輯閾值。</span><span class="sxs-lookup"><span data-stu-id="4881f-160">You can edit the threshold.</span></span>

    ![列入白名單的網域名稱](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a><span data-ttu-id="4881f-162">管理組件</span><span class="sxs-lookup"><span data-stu-id="4881f-162">Management packs</span></span>

<span data-ttu-id="4881f-163">如果您使用 Microsoft Monitoring Agent 連線到您的 Operations Management Suite 工作區，則會安裝下列管理組件：</span><span class="sxs-lookup"><span data-stu-id="4881f-163">If you are using the Microsoft Monitoring Agent to connect to your Operations Management Suite workspace, the following management pack is installed:</span></span>

- <span data-ttu-id="4881f-164">Microsoft DNS 資料收集器智慧套件 (Microsft.IntelligencePacks.Dns)</span><span class="sxs-lookup"><span data-stu-id="4881f-164">Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)</span></span>

<span data-ttu-id="4881f-165">如果 Operations Manager 管理群組已連線到 Operations Management Suite 工作區，當您新增此方案時，下列管理組件會安裝在 Operations Manager 中。</span><span class="sxs-lookup"><span data-stu-id="4881f-165">If your Operations Manager management group is connected to your Operations Management Suite workspace, the following management packs are installed in Operations Manager when you add this solution.</span></span> <span data-ttu-id="4881f-166">這些管理組件不需要任何組態或維護：</span><span class="sxs-lookup"><span data-stu-id="4881f-166">There is no required configuration or maintenance of these management packs:</span></span>

- <span data-ttu-id="4881f-167">Microsoft DNS 資料收集器智慧套件 (Microsft.IntelligencePacks.Dns)</span><span class="sxs-lookup"><span data-stu-id="4881f-167">Microsoft DNS Data Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)</span></span>
- <span data-ttu-id="4881f-168">Microsoft System Center Advisor DNS 分析組態 (Microsoft.IntelligencePack.Dns.Configuration)</span><span class="sxs-lookup"><span data-stu-id="4881f-168">Microsoft System Center Advisor DNS Analytics Configuration (Microsoft.IntelligencePack.Dns.Configuration)</span></span>

<span data-ttu-id="4881f-169">如需有關方案管理組件如何更新的詳細資訊，請參閱 [將 Operations Manager 連接到 Log Analytics](log-analytics-om-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="4881f-169">For more information on how solution management packs are updated, see [Connect Operations Manager to Log Analytics](log-analytics-om-agents.md).</span></span>

## <a name="use-the-dns-analytics-solution"></a><span data-ttu-id="4881f-170">使用 DNS 分析解決方案</span><span class="sxs-lookup"><span data-stu-id="4881f-170">Use the DNS Analytics solution</span></span>

<span data-ttu-id="4881f-171">本節說明所有儀表板函式及其使用方式。</span><span class="sxs-lookup"><span data-stu-id="4881f-171">This section explains all the dashboard functions and how to use them.</span></span>

<span data-ttu-id="4881f-172">將解決方案新增至您的工作區之後，[Operations Management Suite 概觀] 頁面上的解決方案圖格會提供您 DNS 基礎結構的快速摘要。</span><span class="sxs-lookup"><span data-stu-id="4881f-172">After you've added the solution to your workspace, the solution tile on the Operations Management Suite Overview page provides a quick summary of your DNS infrastructure.</span></span> <span data-ttu-id="4881f-173">它包含收集資料所在的 DNS 伺服器之數目。</span><span class="sxs-lookup"><span data-stu-id="4881f-173">It includes the number of DNS servers where the data is being collected.</span></span> <span data-ttu-id="4881f-174">它也包含用戶端在過去 24 小時內所提出的解決惡意網域之要求數目。</span><span class="sxs-lookup"><span data-stu-id="4881f-174">It also includes the number of requests made by clients to resolve malicious domains in the past 24 hours.</span></span> <span data-ttu-id="4881f-175">當您按一下圖格時，方案儀表板隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="4881f-175">When you click the tile, the solution dashboard opens.</span></span>

![DNS 分析圖格](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a><span data-ttu-id="4881f-177">解決方案儀表板</span><span class="sxs-lookup"><span data-stu-id="4881f-177">Solution dashboard</span></span>

<span data-ttu-id="4881f-178">解決方案儀表板會顯示解決方案的各種功能的摘要資訊。</span><span class="sxs-lookup"><span data-stu-id="4881f-178">The solution dashboard shows summarized information for the various features of the solution.</span></span> <span data-ttu-id="4881f-179">它也包含鑑識分析和診斷之詳細檢視的連結。</span><span class="sxs-lookup"><span data-stu-id="4881f-179">It also includes links to the detailed view for forensic analysis and diagnosis.</span></span> <span data-ttu-id="4881f-180">根據預設，會顯示過去七天的資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-180">By default, the data is shown for the last seven days.</span></span> <span data-ttu-id="4881f-181">您可以使用**日期-時間選取控制項**來變更日期與時間範圍，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="4881f-181">You can change the date and time range by using the **date-time selection control**, as shown in the following image:</span></span>

![時間選取控制項](./media/log-analytics-dns/dns-time.png)

<span data-ttu-id="4881f-183">解決方案儀表板會顯示下列刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="4881f-183">The solution dashboard shows the following blades:</span></span>

<span data-ttu-id="4881f-184">**DNS 安全性**。</span><span class="sxs-lookup"><span data-stu-id="4881f-184">**DNS Security**.</span></span> <span data-ttu-id="4881f-185">報告嘗試與惡意網域進行通訊的 DNS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="4881f-185">Reports the DNS clients that are trying to communicate with malicious domains.</span></span> <span data-ttu-id="4881f-186">藉由使用 Microsoft 威脅情報摘要，DNS 分析可以偵測嘗試存取惡意網域的用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="4881f-186">By using Microsoft threat intelligence feeds, DNS Analytics can detect client IPs that are trying to access malicious domains.</span></span> <span data-ttu-id="4881f-187">在許多情況下，受惡意程式碼感染的裝置會透過解析惡意程式碼網域名稱「撥出」至惡意網域的「命令與控制項」中心。</span><span class="sxs-lookup"><span data-stu-id="4881f-187">In many cases, malware-infected devices "dial out" to the "command and control" center of the malicious domain by resolving the malware domain name.</span></span>

![[DNS 安全性] 刀鋒視窗](./media/log-analytics-dns/dns-security-blade.png)

<span data-ttu-id="4881f-189">當您按一下清單中的用戶端 IP 時，記錄搜尋就會開啟，其中顯示個別查詢的查閱詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-189">When you click a client IP in the list, Log Search opens and shows the lookup details of the respective query.</span></span> <span data-ttu-id="4881f-190">在下列範例中，DNS 分析偵測到透過 [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot) 進行的通訊：</span><span class="sxs-lookup"><span data-stu-id="4881f-190">In the following example, DNS Analytics detected that the communication was done with an [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):</span></span>

![顯示 ircbot 的記錄搜尋結果](./media/log-analytics-dns/ircbot.png)

<span data-ttu-id="4881f-192">此資訊可協助您識別︰</span><span class="sxs-lookup"><span data-stu-id="4881f-192">The information helps you to identify the:</span></span>

- <span data-ttu-id="4881f-193">起始通訊的用戶端 IP。</span><span class="sxs-lookup"><span data-stu-id="4881f-193">Client IP that initiated the communication.</span></span>
- <span data-ttu-id="4881f-194">解析為惡意 IP 的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4881f-194">Domain name that resolves to the malicious IP.</span></span>
- <span data-ttu-id="4881f-195">網域名稱解析成的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4881f-195">IP addresses that the domain name resolves to.</span></span>
- <span data-ttu-id="4881f-196">惡意 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4881f-196">Malicious IP address.</span></span>
- <span data-ttu-id="4881f-197">問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="4881f-197">Severity of the issue.</span></span>
- <span data-ttu-id="4881f-198">將惡意 IP 列入黑名單的原因。</span><span class="sxs-lookup"><span data-stu-id="4881f-198">Reason for blacklisting the malicious IP.</span></span>
- <span data-ttu-id="4881f-199">偵測時間。</span><span class="sxs-lookup"><span data-stu-id="4881f-199">Detection time.</span></span>

<span data-ttu-id="4881f-200">**查詢的網域**。</span><span class="sxs-lookup"><span data-stu-id="4881f-200">**Domains Queried**.</span></span> <span data-ttu-id="4881f-201">提供您環境中的 DNS 用戶端最常查詢的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="4881f-201">Provides the most frequent domain names being queried by the DNS clients in your environment.</span></span> <span data-ttu-id="4881f-202">您可以檢視查詢的所有網域名稱清單。</span><span class="sxs-lookup"><span data-stu-id="4881f-202">You can view the list of all the domain names queried.</span></span> <span data-ttu-id="4881f-203">您也可以在記錄搜尋中向下切入至特定網域名稱的查閱要求詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-203">You can also drill down into the lookup request details of a specific domain name in Log Search.</span></span>

![[查詢的網域] 刀鋒視窗](./media/log-analytics-dns/domains-queried-blade.png)

<span data-ttu-id="4881f-205">**DNS 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="4881f-205">**DNS Clients**.</span></span> <span data-ttu-id="4881f-206">報告違反閾值的用戶端在所選時間週期內的查詢數目。</span><span class="sxs-lookup"><span data-stu-id="4881f-206">Reports the clients *breaching the threshold* for number of queries in the chosen time period.</span></span> <span data-ttu-id="4881f-207">您可以在記錄搜尋中檢視所有 DNS 用戶端的清單和它們所執行查詢的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-207">You can view the list of all the DNS clients and the details of the queries made by them in Log Search.</span></span>

![[DNS 用戶端] 刀鋒視窗](./media/log-analytics-dns/dns-clients-blade.png)

<span data-ttu-id="4881f-209">**動態 DNS 註冊**。</span><span class="sxs-lookup"><span data-stu-id="4881f-209">**Dynamic DNS Registrations**.</span></span> <span data-ttu-id="4881f-210">報告名稱註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="4881f-210">Reports name registration failures.</span></span> <span data-ttu-id="4881f-211">位址[資源記錄](https://en.wikipedia.org/wiki/List_of_DNS_record_types)的所有註冊失敗 (類型 A 和 AAAA) 會連同提出註冊要求的用戶端 IP 一起反白顯示。</span><span class="sxs-lookup"><span data-stu-id="4881f-211">All registration failures for address [resource records](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (Type A and AAAA) are highlighted along with the client IPs that made the registration requests.</span></span> <span data-ttu-id="4881f-212">您可以接著依照下列步驟，使用此資訊來尋找註冊失敗的根本原因︰</span><span class="sxs-lookup"><span data-stu-id="4881f-212">You can then use this information to find the root cause of the registration failure by following these steps:</span></span>

1. <span data-ttu-id="4881f-213">尋找對於用戶端嘗試更新之名稱具有權威性的區域。</span><span class="sxs-lookup"><span data-stu-id="4881f-213">Find the zone that is authoritative for the name that the client is trying to update.</span></span>

2. <span data-ttu-id="4881f-214">使用此解決方案來檢查該區域的清查資訊。</span><span class="sxs-lookup"><span data-stu-id="4881f-214">Use the solution to check the inventory information of that zone.</span></span>

3. <span data-ttu-id="4881f-215">確認已啟用該區域的動態更新。</span><span class="sxs-lookup"><span data-stu-id="4881f-215">Verify that the dynamic update for the zone is enabled.</span></span>

4. <span data-ttu-id="4881f-216">檢查該區域是否已設定安全動態更新。</span><span class="sxs-lookup"><span data-stu-id="4881f-216">Check whether the zone is configured for secure dynamic update or not.</span></span>

    ![[動態 DNS 註冊] 刀鋒視窗](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

<span data-ttu-id="4881f-218">**名稱註冊要求**。</span><span class="sxs-lookup"><span data-stu-id="4881f-218">**Name registration requests**.</span></span> <span data-ttu-id="4881f-219">上方的圖格會顯示成功和失敗之 DNS 動態更新要求的趨勢線。</span><span class="sxs-lookup"><span data-stu-id="4881f-219">The upper tile shows a trendline of successful and failed DNS dynamic update requests.</span></span> <span data-ttu-id="4881f-220">下方的圖格所列出的前 10 個用戶端，是將失敗的 DNS 更新要求傳送給 DNS 伺服器 (依失敗數目排序)。</span><span class="sxs-lookup"><span data-stu-id="4881f-220">The lower tile lists the top 10 clients that are sending failed DNS update requests to the DNS servers, sorted by the number of failures.</span></span>

![<span data-ttu-id="4881f-221">[名稱註冊要求] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="4881f-221">Name registration requests blade</span></span> ](./media/log-analytics-dns/name-reg-req-blade.png)

<span data-ttu-id="4881f-222">**範例 DDI 分析查詢**。</span><span class="sxs-lookup"><span data-stu-id="4881f-222">**Sample DDI Analytics Queries**.</span></span> <span data-ttu-id="4881f-223">包含最常見的搜尋查詢清單，會直接擷取未經處理的分析資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-223">Contains a list of the most common search queries that fetch raw analytics data directly.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![範例查詢](./media/log-analytics-dns/queries.png)

<span data-ttu-id="4881f-225">您可以使用這些查詢做為起點，建立自己的查詢以供自訂報告。</span><span class="sxs-lookup"><span data-stu-id="4881f-225">You can use these queries as a starting point for creating your own queries for customized reporting.</span></span> <span data-ttu-id="4881f-226">查詢會連結到顯示結果的 [DNS 分析記錄搜尋] 頁面︰</span><span class="sxs-lookup"><span data-stu-id="4881f-226">The queries link to the DNS Analytics Log Search page where results are displayed:</span></span>

- <span data-ttu-id="4881f-227">**DNS 伺服器清單**。</span><span class="sxs-lookup"><span data-stu-id="4881f-227">**List of DNS Servers**.</span></span> <span data-ttu-id="4881f-228">顯示所有 DNS 伺服器的清單，包含其相關聯的 FQDN、網域名稱、樹系名稱和伺服器的 IP。</span><span class="sxs-lookup"><span data-stu-id="4881f-228">Shows a list of all DNS servers with their associated FQDN, domain name, forest name, and server IPs.</span></span>
- <span data-ttu-id="4881f-229">**DNS 區域清單**。</span><span class="sxs-lookup"><span data-stu-id="4881f-229">**List of DNS Zones**.</span></span> <span data-ttu-id="4881f-230">顯示所有 DNS 區域的清單，及其相關聯的區域名稱、動態更新狀態、名稱伺服器及 DNSSEC 簽署狀態。</span><span class="sxs-lookup"><span data-stu-id="4881f-230">Shows a list of all DNS zones with the associated zone name, dynamic update status, name servers, and DNSSEC signing status.</span></span>
- <span data-ttu-id="4881f-231">**未使用的資源記錄**。</span><span class="sxs-lookup"><span data-stu-id="4881f-231">**Unused Resource Records**.</span></span> <span data-ttu-id="4881f-232">顯示所有未使用/過時資源記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="4881f-232">Shows a list of all the unused/stale resource records.</span></span> <span data-ttu-id="4881f-233">此清單包含資源記錄名稱、資源記錄類型、相關聯的 DNS 伺服器、記錄產生時間和區域名稱。</span><span class="sxs-lookup"><span data-stu-id="4881f-233">This list contains the resource record name, resource record type, the associated DNS server, record generation time, and zone name.</span></span> <span data-ttu-id="4881f-234">您可以使用此清單來找出不再使用的 DNS 資源記錄。</span><span class="sxs-lookup"><span data-stu-id="4881f-234">You can use this list to identify the DNS resource records that are no longer in use.</span></span> <span data-ttu-id="4881f-235">根據這項資訊，您可以接著從 DNS 伺服器將這些項目移除。</span><span class="sxs-lookup"><span data-stu-id="4881f-235">Based on this information, you can then remove those entries from the DNS servers.</span></span>
- <span data-ttu-id="4881f-236">**DNS 伺服器查詢負載**。</span><span class="sxs-lookup"><span data-stu-id="4881f-236">**DNS Servers Query Load**.</span></span> <span data-ttu-id="4881f-237">可顯示資訊，以便您能在 DNS 伺服器上取得 DNS 負載的檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="4881f-237">Shows information so that you can get a perspective of the DNS load on your DNS servers.</span></span> <span data-ttu-id="4881f-238">這項資訊可協助您規劃伺服器的容量。</span><span class="sxs-lookup"><span data-stu-id="4881f-238">This information can help you plan the capacity for the servers.</span></span> <span data-ttu-id="4881f-239">您可以移至 [計量] 索引標籤，將檢視變更為圖形化視覺效果。</span><span class="sxs-lookup"><span data-stu-id="4881f-239">You can go to the **Metrics** tab to change the view to a graphical visualization.</span></span> <span data-ttu-id="4881f-240">此檢視可協助您了解您的 DNS 伺服器的 DNS 負載分佈狀況。</span><span class="sxs-lookup"><span data-stu-id="4881f-240">This view helps you understand how the DNS load is distributed across your DNS servers.</span></span> <span data-ttu-id="4881f-241">它會顯示每部伺服器的 DNS 查詢速率趨勢。</span><span class="sxs-lookup"><span data-stu-id="4881f-241">It shows DNS query rate trends for each server.</span></span>

    ![DNS 伺服器查詢記錄搜尋結果](./media/log-analytics-dns/dns-servers-query-load.png)

- <span data-ttu-id="4881f-243">**DNS 區域的查詢負載**。</span><span class="sxs-lookup"><span data-stu-id="4881f-243">**DNS Zones Query Load**.</span></span> <span data-ttu-id="4881f-244">顯示受解決方案管理的 DNS 伺服器上所有區域的 DNS 區域每秒查詢統計資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-244">Shows the DNS zone-query-per-second statistics of all the zones on the DNS servers being managed by the solution.</span></span> <span data-ttu-id="4881f-245">按一下 [計量] 索引標籤，以將檢視從詳細記錄變更為圖形化的視覺效果結果。</span><span class="sxs-lookup"><span data-stu-id="4881f-245">Click the **Metrics** tab to change the view from detailed records to a graphical visualization of the results.</span></span>
- <span data-ttu-id="4881f-246">**設定事件**。</span><span class="sxs-lookup"><span data-stu-id="4881f-246">**Configuration Events**.</span></span> <span data-ttu-id="4881f-247">顯示所有的 DNS 設定變更事件和相關聯的訊息。</span><span class="sxs-lookup"><span data-stu-id="4881f-247">Shows all the DNS configuration change events and associated messages.</span></span> <span data-ttu-id="4881f-248">您可以根據事件的時間、事件識別碼、DNS 伺服器或工作類別進一步篩選這些事件。</span><span class="sxs-lookup"><span data-stu-id="4881f-248">You can then filter these events based on time of the event, event ID, DNS server, or task category.</span></span> <span data-ttu-id="4881f-249">這些資料可協助您稽核 DNS 伺服器在特定時間發生的變更。</span><span class="sxs-lookup"><span data-stu-id="4881f-249">The data can help you audit changes made to specific DNS servers at specific times.</span></span>
- <span data-ttu-id="4881f-250">**DNS 分析記錄**。</span><span class="sxs-lookup"><span data-stu-id="4881f-250">**DNS Analytical Log**.</span></span> <span data-ttu-id="4881f-251">顯示解決方案所管理的所有 DNS 伺服器上的所有分析事件。</span><span class="sxs-lookup"><span data-stu-id="4881f-251">Shows all the analytic events on all the DNS servers managed by the solution.</span></span> <span data-ttu-id="4881f-252">您可以根據事件的時間、事件識別碼、DNS 伺服器、執行查閱查詢的用戶端 IP 和查詢類型工作類別，將這些事件進一步篩選。</span><span class="sxs-lookup"><span data-stu-id="4881f-252">You can then filter these events based on time of the event, event ID, DNS server, client IP that made the lookup query, and query type task category.</span></span> <span data-ttu-id="4881f-253">DNS 伺服器分析事件可追蹤 DNS 伺服器上的活動。</span><span class="sxs-lookup"><span data-stu-id="4881f-253">DNS server analytic events enable activity tracking on the DNS server.</span></span> <span data-ttu-id="4881f-254">每次伺服器傳送或接收 DNS 資訊時，都會記錄分析事件。</span><span class="sxs-lookup"><span data-stu-id="4881f-254">An analytic event is logged each time the server sends or receives DNS information.</span></span>

### <a name="search-by-using-dns-analytics-log-search"></a><span data-ttu-id="4881f-255">使用 DNS 分析記錄搜尋來搜尋</span><span class="sxs-lookup"><span data-stu-id="4881f-255">Search by using DNS Analytics Log Search</span></span>

<span data-ttu-id="4881f-256">在 [記錄搜尋] 頁面上，您可以建立查詢。</span><span class="sxs-lookup"><span data-stu-id="4881f-256">On the Log Search page, you can create a query.</span></span> <span data-ttu-id="4881f-257">您可以使用 facet 控制項來篩選搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="4881f-257">You can filter your search results by using facet controls.</span></span> <span data-ttu-id="4881f-258">您也可以建立進階查詢來轉換、篩選和報告結果。</span><span class="sxs-lookup"><span data-stu-id="4881f-258">You can also create advanced queries to transform, filter, and report on your results.</span></span> <span data-ttu-id="4881f-259">使用下列查詢來開始：</span><span class="sxs-lookup"><span data-stu-id="4881f-259">Start by using the following queries:</span></span>

1. <span data-ttu-id="4881f-260">在**搜尋查詢方塊**中，輸入 `Type=DnsEvents` 以檢視此解決方案管理的 DNS 伺服器所產生的所有 DNS 事件。</span><span class="sxs-lookup"><span data-stu-id="4881f-260">In the **search query box**, type `Type=DnsEvents` to view all the DNS events generated by the DNS servers managed by the solution.</span></span> <span data-ttu-id="4881f-261">結果會列出與查閱查詢、動態註冊和設定變更相關之所有事件的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-261">The results list the log data for all events related to lookup queries, dynamic registrations, and configuration changes.</span></span>

    ![DnsEvents 記錄搜尋](./media/log-analytics-dns/log-search-dnsevents.png)  

    <span data-ttu-id="4881f-263">a.</span><span class="sxs-lookup"><span data-stu-id="4881f-263">a.</span></span> <span data-ttu-id="4881f-264">若要檢視查閱查詢的記錄資料，請從左側 facet 控制項選取 **LookUpQuery** 作為 **Subtype** 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="4881f-264">To view the log data for lookup queries, select **LookUpQuery** as the **Subtype** filter from the facet control on the left.</span></span> <span data-ttu-id="4881f-265">隨即顯示列出所選時間週期之查閱查詢事件的資料表。</span><span class="sxs-lookup"><span data-stu-id="4881f-265">A table that lists all the lookup query events for the selected time period is displayed.</span></span>

    <span data-ttu-id="4881f-266">b.</span><span class="sxs-lookup"><span data-stu-id="4881f-266">b.</span></span> <span data-ttu-id="4881f-267">若要檢視動態註冊的記錄資料，請從左側 facet 控制項選取 **DynamicRegistration** 作為 **Subtype** 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="4881f-267">To view the log data for dynamic registrations, select **DynamicRegistration** as the **Subtype** filter from the facet control on the left.</span></span> <span data-ttu-id="4881f-268">隨即顯示列出所選時間週期之動態註冊事件的資料表。</span><span class="sxs-lookup"><span data-stu-id="4881f-268">A table that lists all the dynamic registration events for the selected time period is displayed.</span></span>

    <span data-ttu-id="4881f-269">c.</span><span class="sxs-lookup"><span data-stu-id="4881f-269">c.</span></span> <span data-ttu-id="4881f-270">若要檢視設定變更的記錄資料，請從左側 facet 控制項選取 **ConfigurationChange** 作為 **Subtype** 篩選條件。</span><span class="sxs-lookup"><span data-stu-id="4881f-270">To view the log data for configuration changes, select **ConfigurationChange** as the **Subtype** filter from the facet control on the left.</span></span> <span data-ttu-id="4881f-271">隨即顯示列出所選時間週期之設定變更事件的資料表。</span><span class="sxs-lookup"><span data-stu-id="4881f-271">A table that lists all the configuration change events for the selected time period is displayed.</span></span>

2. <span data-ttu-id="4881f-272">在**搜尋查詢方塊**中，輸入 `Type=DnsInventory` 以檢視此解決方案管理的 DNS 伺服器的所有 DNS 清查相關資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-272">In the **search query box**, type `Type=DnsInventory` to view all the DNS inventory-related data for the DNS servers managed by the solution.</span></span> <span data-ttu-id="4881f-273">結果會列出 DNS 伺服器、DNS 區域和資源記錄的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="4881f-273">The results list the log data for DNS servers, DNS zones, and resource records.</span></span>

    ![DnsInventory 記錄搜尋](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a><span data-ttu-id="4881f-275">意見反應</span><span class="sxs-lookup"><span data-stu-id="4881f-275">Feedback</span></span>

<span data-ttu-id="4881f-276">提供意見反應的方式有兩種：</span><span class="sxs-lookup"><span data-stu-id="4881f-276">There are two ways you can give feedback:</span></span>

- <span data-ttu-id="4881f-277">**UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="4881f-277">**UserVoice**.</span></span> <span data-ttu-id="4881f-278">發表您對 DNS 分析功能的想法。</span><span class="sxs-lookup"><span data-stu-id="4881f-278">Post ideas for DNS Analytics features to work on.</span></span> <span data-ttu-id="4881f-279">請瀏覽 [Operations Management Suite UserVoice 頁面](https://aka.ms/dnsanalyticsuservoice)。</span><span class="sxs-lookup"><span data-stu-id="4881f-279">Visit the [Operations Management Suite UserVoice page](https://aka.ms/dnsanalyticsuservoice).</span></span>
- <span data-ttu-id="4881f-280">**加入我們的行列**。</span><span class="sxs-lookup"><span data-stu-id="4881f-280">**Join our cohort**.</span></span> <span data-ttu-id="4881f-281">我們始終歡迎新客戶加入我們的行列以搶先試用新功能，並協助我們改善 DNS 分析。</span><span class="sxs-lookup"><span data-stu-id="4881f-281">We're always interested in having new customers join our cohorts to get early access to new features and help us improve DNS Analytics.</span></span> <span data-ttu-id="4881f-282">如果您想加入我們的行列，請填妥這份[快速問卷調查 (英文)](https://aka.ms/dnsanalyticssurvey)。</span><span class="sxs-lookup"><span data-stu-id="4881f-282">If you are interested in joining our cohorts, fill out [this quick survey](https://aka.ms/dnsanalyticssurvey).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4881f-283">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4881f-283">Next steps</span></span>

<span data-ttu-id="4881f-284">[搜尋記錄](log-analytics-log-searches.md)以檢視詳細的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="4881f-284">[Search logs](log-analytics-log-searches.md) to view detailed DNS log records.</span></span>
