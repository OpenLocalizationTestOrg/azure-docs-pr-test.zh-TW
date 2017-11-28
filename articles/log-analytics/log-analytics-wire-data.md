---
title: "Log Analytics 中的連線資料方案 | Microsoft Docs"
description: "網路資料是來自具有 OMS 代理程式 (包括 Operations Manager 和 Windows 連線的代理程式) 的電腦的網路和效能彙總資料。 網路資料結合記錄資料可協助您將資料相互關聯。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: fc3d7127-0baa-4772-858a-5ba995d1519b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: banders
ms.openlocfilehash: eb8ae80f91b9ecad666ab7a2257d99e5669f5b88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="8c848-104">Log Analytics 中的 Wire Data 2.0 (預覽) 解決方案</span><span class="sxs-lookup"><span data-stu-id="8c848-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Wire Data 符號](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="8c848-106">連線資料是來自具有 OMS 代理程式 (包括 Operations Manager、Windows 連線和 Linux 代理程式) 之電腦的網路和效能彙總資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="8c848-107">網路資料結合其他記錄資料可協助您將資料相互關聯。</span><span class="sxs-lookup"><span data-stu-id="8c848-107">Network data is combined with your other log data to help you correlate data.</span></span>

<span data-ttu-id="8c848-108">除了 OMS 代理程式，Wire Data 解決方案還會使用您在 IT 基礎結構的電腦上所安裝的 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-108">In addition to OMS agents, the Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="8c848-109">相依性代理程式會監視往返於您電腦傳送的網路資料 (屬於 [OSI 模型](https://en.wikipedia.org/wiki/OSI_model)中的網路層級 2-3)，包括使用的各種通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c848-109">Dependency Agents monitor network data sent to and from your computers for network levels 2-3 in the [OSI model](https://en.wikipedia.org/wiki/OSI_model), including the various protocols and ports used.</span></span> <span data-ttu-id="8c848-110">然後使用代理程式將資料傳送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c848-110">Data is then sent to Log Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="8c848-111">您無法將舊版 Wire Data 解決方案新增至新的工作區。</span><span class="sxs-lookup"><span data-stu-id="8c848-111">You cannot add the previous version of the Wire Data solution to new workspaces.</span></span> <span data-ttu-id="8c848-112">如果您已啟用原始 Wire Data 解決方案，您可以繼續使用。</span><span class="sxs-lookup"><span data-stu-id="8c848-112">If you have the original Wire Data solution enabled, you can continue to use it.</span></span> <span data-ttu-id="8c848-113">不過，若要使用 Wire Data 2.0，您必須先移除原始版本。</span><span class="sxs-lookup"><span data-stu-id="8c848-113">However, to use Wire Data 2.0, you must first remove the original version.</span></span>

<span data-ttu-id="8c848-114">根據預設，Log Analytics 會從 Windows 內建的計數器收集記錄的資料，包括 CPU、記憶體、磁碟和網路效能資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="8c848-115">針對每個代理程式，都是即時收集網路和其他資料，包括電腦使用的子網路和應用程式層級通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8c848-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by the computer.</span></span> <span data-ttu-id="8c848-116">您可以在 [設定] 頁面的 [記錄檔] 索引標籤上加入其他效能計數器。</span><span class="sxs-lookup"><span data-stu-id="8c848-116">You can add other performance counters on the Settings page on the Logs tab.</span></span>

<span data-ttu-id="8c848-117">如果您曾經使用 [sFlow](http://www.sflow.org/) 或其他軟體來搭配 [Cisco NetFlow 通訊協定](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)，則會很熟悉從連線資料傳回的統計資料和資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then the statistics and data you see from wire data will be familiar to you.</span></span>

<span data-ttu-id="8c848-118">幾種內建的記錄搜尋查詢包括︰</span><span class="sxs-lookup"><span data-stu-id="8c848-118">Some of the types of built-in Log search queries include:</span></span>

- <span data-ttu-id="8c848-119">提供連線資料的代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-119">Agents that provide wire data</span></span>
- <span data-ttu-id="8c848-120">提供連線資料的代理程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8c848-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="8c848-121">依 IP 位址的輸出通訊</span><span class="sxs-lookup"><span data-stu-id="8c848-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="8c848-122">應用程式通訊協定傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8c848-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="8c848-123">應用程式服務傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8c848-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="8c848-124">不同通訊協定接收的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8c848-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="8c848-125">IP 版本傳送及接收的位元組總數</span><span class="sxs-lookup"><span data-stu-id="8c848-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="8c848-126">可靠測量的連線平均延遲</span><span class="sxs-lookup"><span data-stu-id="8c848-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="8c848-127">起始或接收網路流量的電腦處理程序</span><span class="sxs-lookup"><span data-stu-id="8c848-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="8c848-128">處理程序的網路流量</span><span class="sxs-lookup"><span data-stu-id="8c848-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="8c848-129">當您使用連線資料來搜尋時，您可以篩選和分組資料，以檢視最常用的前幾個代理程式和通訊協定的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="8c848-129">When you search using wire data, you can filter and group data to view information about the top agents and top protocols.</span></span> <span data-ttu-id="8c848-130">或者，您可以檢視某些電腦 (IP 位址/MAC 位址) 何時彼此通訊、持續時間，以及已傳送的資料量；基本上，就是在檢視以搜尋為基礎之網路流量的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="8c848-131">不過，因為是檢視中繼資料，在深入的疑難排解中不見得實用。</span><span class="sxs-lookup"><span data-stu-id="8c848-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="8c848-132">Log Analytics 中的連線資料不是完整擷取的網路資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="8c848-133">因此，不適用於封包層級的深入疑難排解。</span><span class="sxs-lookup"><span data-stu-id="8c848-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="8c848-134">相較於其他收集方法，使用代理程式的優點是您不必安裝應用裝置、重新設定網路交換器，或執行複雜的設定。</span><span class="sxs-lookup"><span data-stu-id="8c848-134">The advantage of using the agent, compared to other collection methods, is that you don't have to install appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="8c848-135">連線資料是以代理程式為基礎—在電腦上安裝代理程式，它就會監視自己的網路流量。</span><span class="sxs-lookup"><span data-stu-id="8c848-135">Wire data is simply agent-based—you install the agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="8c848-136">另一個優點是您想要監視雲端提供者、主機服務提供者或 Microsoft Azure 中執行的工作負載，而其中使用者未擁有網狀架構層級。</span><span class="sxs-lookup"><span data-stu-id="8c848-136">Another advantage is when you want to monitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where the user doesn't own the fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="8c848-137">連接的來源</span><span class="sxs-lookup"><span data-stu-id="8c848-137">Connected sources</span></span>

<span data-ttu-id="8c848-138">Wire Data 會從 Microsoft 相依性代理程式取得其資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-138">Wire Data gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="8c848-139">相依性代理程式相依於連線到 Log Analytics 的 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-139">The Dependency Agent depends on the OMS Agent for its connections to Log Analytics.</span></span> <span data-ttu-id="8c848-140">這表示，伺服器必須先安裝並設定 OMS 代理程式，然後才能安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-140">This means that a server must have the OMS Agent installed and configured first, and then you install the Dependency Agent.</span></span> <span data-ttu-id="8c848-141">下表描述 Wire Data 解決方案支援的連線來源。</span><span class="sxs-lookup"><span data-stu-id="8c848-141">The following table describes the connected sources that the Wire Data solution supports.</span></span>

| <span data-ttu-id="8c848-142">**連線的來源**</span><span class="sxs-lookup"><span data-stu-id="8c848-142">**Connected source**</span></span> | <span data-ttu-id="8c848-143">**支援**</span><span class="sxs-lookup"><span data-stu-id="8c848-143">**Supported**</span></span> | <span data-ttu-id="8c848-144">**說明**</span><span class="sxs-lookup"><span data-stu-id="8c848-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c848-145">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-145">Windows agents</span></span> | <span data-ttu-id="8c848-146">是</span><span class="sxs-lookup"><span data-stu-id="8c848-146">Yes</span></span> | <span data-ttu-id="8c848-147">Wire Data 會分析並收集來自 Windows 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="8c848-148">除了 [OMS 代理程式](log-analytics-windows-agents.md)外，Windows 代理程式還需要 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-148">In addition to the [OMS Agent](log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="8c848-149">如需作業系統版本的完整清單，請參閱[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)。</span><span class="sxs-lookup"><span data-stu-id="8c848-149">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="8c848-150">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-150">Linux agents</span></span> | <span data-ttu-id="8c848-151">是</span><span class="sxs-lookup"><span data-stu-id="8c848-151">Yes</span></span> | <span data-ttu-id="8c848-152">Wire Data 會分析並收集來自 Linux 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="8c848-153">除了 [OMS 代理程式](log-analytics-linux-agents.md)外，Linux 代理程式還需要 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-153">In addition to the [OMS Agent](log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="8c848-154">如需作業系統版本的完整清單，請參閱[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)。</span><span class="sxs-lookup"><span data-stu-id="8c848-154">See the [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="8c848-155">System Center Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="8c848-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="8c848-156">是</span><span class="sxs-lookup"><span data-stu-id="8c848-156">Yes</span></span> | <span data-ttu-id="8c848-157">Wire Data 會在連線的 [System Center Operations Manager 管理群組](log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="8c848-158">System Center Operations Manager 代理程式電腦必須直接連線到 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c848-158">A direct connection from the System Center Operations Manager agent computer to Log Analytics is required.</span></span> <span data-ttu-id="8c848-159">資料會從管理群組轉送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c848-159">Data is forwarded from the management group to Log Analytics.</span></span> |
| <span data-ttu-id="8c848-160">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8c848-160">Azure storage account</span></span> | <span data-ttu-id="8c848-161">否</span><span class="sxs-lookup"><span data-stu-id="8c848-161">No</span></span> | <span data-ttu-id="8c848-162">Wire Data 會收集來自代理程式電腦的資料，因此沒有要從 Azure 儲存體收集的資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-162">Wire Data collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="8c848-163">在 Windows 上，System Center Operations Manager 和 Log Analytics 會使用 Microsoft Monitoring Agent (MMA) 來收集和傳送資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-163">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics to gather and send data.</span></span> <span data-ttu-id="8c848-164">視內容而定，此代理程式可稱為 System Center Operations Manager 代理程式、OMS 代理程式、Log Analytics 代理程式、MMA 或直接代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-164">Depending on the context, the agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="8c848-165">System Center Operations Manager 和 Log Analytics 提供的 MMA 版本稍有不同。</span><span class="sxs-lookup"><span data-stu-id="8c848-165">System Center Operations Manager and Log Analytics provide slightly different versions of the MMA.</span></span> <span data-ttu-id="8c848-166">這些版本可以各自向 System Center Operations Manager 或 Log Analytics 報告，或同時向兩者報告。</span><span class="sxs-lookup"><span data-stu-id="8c848-166">These versions can each report to System Center Operations Manager, to Log Analytics, or to both.</span></span>

<span data-ttu-id="8c848-167">在 Linux 上，OMS Agent for Linux 會收集資料並傳送給 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c848-167">On Linux, the OMS Agent for Linux gathers and sends data to Log Analytics.</span></span> <span data-ttu-id="8c848-168">您可以在具有 OMS 直接代理程式的伺服器上，或在透過 System Center Operations Manager 管理群組連結至 Log Analytics 的伺服器上，使用 Wire Data。</span><span class="sxs-lookup"><span data-stu-id="8c848-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached to Log Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="8c848-169">在本文中，所有代理程式 (無論 Linux 或 Windows、無論是連線到 System Center Operations Manager 管理群組或直接連線到 Log Analytics) 一律稱為「OMS 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="8c848-169">In this article, references to all agents, whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Log Analytics are termed the _OMS agent_.</span></span> <span data-ttu-id="8c848-170">只有在內容需要時，我們才會使用代理程式特定的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="8c848-170">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="8c848-171">相依性代理程式本身不會傳輸任何資料，因此不需要變更防火牆或連接埠。</span><span class="sxs-lookup"><span data-stu-id="8c848-171">The Dependency Agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="8c848-172">Wire Data 中的資料一律會由 OMS 代理程式 (直接或使用 OMS 閘道) 傳輸給 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="8c848-172">The data in Wire Data is always transmitted by the OMS agent to Log Analytics, either directly or using the OMS Gateway.</span></span>

![代理程式圖表](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="8c848-174">如果您是管理群組連線到 Log Analytics 的 System Center Operations Manager 使用者：</span><span class="sxs-lookup"><span data-stu-id="8c848-174">If you are a System Center Operations Manager user with a management group connected to Log Analytics:</span></span>

- <span data-ttu-id="8c848-175">當您的 System Center Operations Manager 代理程式可透過網際網路連線到 Log Analytics 時，就不需要額外的設定。</span><span class="sxs-lookup"><span data-stu-id="8c848-175">No additional configuration is required when your System Center Operations Manager agents can access the Internet to connect to Log Analytics.</span></span>
- <span data-ttu-id="8c848-176">當您的 System Center Operations Manager 代理程式無法透過網際網路存取 Log Analytics 時，就必須設定 OMS 閘道以搭配 System Center Operations Manager 使用。</span><span class="sxs-lookup"><span data-stu-id="8c848-176">You need to configure the OMS Gateway to work with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over the Internet.</span></span>

<span data-ttu-id="8c848-177">如果您使用直接代理程式，您需要將 OMS 代理程式本身設定為連線到 Log Analytics 或 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8c848-177">If you are using the Direct Agent, you need to configure the OMS agent itself to connect to Log Analytics or to your OMS Gateway.</span></span> <span data-ttu-id="8c848-178">您可以從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=52666)下載 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8c848-178">You can download the OMS Gateway from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c848-179">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c848-179">Prerequisites</span></span>

- <span data-ttu-id="8c848-180">需要[洞察力與分析](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing)解決方案供應項目。</span><span class="sxs-lookup"><span data-stu-id="8c848-180">Requires the [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="8c848-181">如果您使用舊版 Wire Data 解決方案，則必須先將它移除。</span><span class="sxs-lookup"><span data-stu-id="8c848-181">If you're using the previous version of the Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="8c848-182">不過，您仍然可以在 Wire Data 2.0 和記錄搜尋中使用透過原始 Wire Data 解決方案擷取的所有資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-182">However, all data captured through the original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="8c848-183">必須有系統管理員權限，以便安裝或解除安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-183">Administrator privileges are required to install or uninstall the Dependency Agent.</span></span>
- <span data-ttu-id="8c848-184">相依性代理程式必須安裝在具有 64 位元作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8c848-184">The Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="8c848-185">作業系統</span><span class="sxs-lookup"><span data-stu-id="8c848-185">Operating systems</span></span>

<span data-ttu-id="8c848-186">下列幾節會列出相依性代理程式所支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="8c848-186">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="8c848-187">Wire Data 不支援任何 32 位元架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="8c848-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="8c848-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="8c848-188">Windows Server</span></span>

- <span data-ttu-id="8c848-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8c848-189">Windows Server 2016</span></span>
- <span data-ttu-id="8c848-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8c848-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="8c848-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8c848-191">Windows Server 2012</span></span>
- <span data-ttu-id="8c848-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="8c848-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="8c848-193">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="8c848-193">Windows desktop</span></span>

- <span data-ttu-id="8c848-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8c848-194">Windows 10</span></span>
- <span data-ttu-id="8c848-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8c848-195">Windows 8.1</span></span>
- <span data-ttu-id="8c848-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="8c848-196">Windows 8</span></span>
- <span data-ttu-id="8c848-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8c848-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="8c848-198">Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)</span><span class="sxs-lookup"><span data-stu-id="8c848-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="8c848-199">只支援預設版本和 SMP Linux 核心版本。</span><span class="sxs-lookup"><span data-stu-id="8c848-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="8c848-200">所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。</span><span class="sxs-lookup"><span data-stu-id="8c848-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="8c848-201">例如，不支援版本字串為 _2.6.16.21-0.8-xen_ 的系統。</span><span class="sxs-lookup"><span data-stu-id="8c848-201">For example, a system with the release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="8c848-202">不支援自訂核心，包括重新編譯的標準核心。</span><span class="sxs-lookup"><span data-stu-id="8c848-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="8c848-203">不支援 CentOSPlus 核心。</span><span class="sxs-lookup"><span data-stu-id="8c848-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="8c848-204">Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。</span><span class="sxs-lookup"><span data-stu-id="8c848-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="8c848-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="8c848-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="8c848-206">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-206">**OS version**</span></span> | <span data-ttu-id="8c848-207">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-208">7.0</span><span class="sxs-lookup"><span data-stu-id="8c848-208">7.0</span></span> | <span data-ttu-id="8c848-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="8c848-209">3.10.0-123</span></span> |
| <span data-ttu-id="8c848-210">7.1</span><span class="sxs-lookup"><span data-stu-id="8c848-210">7.1</span></span> | <span data-ttu-id="8c848-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="8c848-211">3.10.0-229</span></span> |
| <span data-ttu-id="8c848-212">7.2</span><span class="sxs-lookup"><span data-stu-id="8c848-212">7.2</span></span> | <span data-ttu-id="8c848-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="8c848-213">3.10.0-327</span></span> |
| <span data-ttu-id="8c848-214">7.3</span><span class="sxs-lookup"><span data-stu-id="8c848-214">7.3</span></span> | <span data-ttu-id="8c848-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="8c848-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="8c848-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="8c848-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="8c848-217">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-217">**OS version**</span></span> | <span data-ttu-id="8c848-218">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-219">6.0</span><span class="sxs-lookup"><span data-stu-id="8c848-219">6.0</span></span> | <span data-ttu-id="8c848-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="8c848-220">2.6.32-71</span></span> |
| <span data-ttu-id="8c848-221">6.1</span><span class="sxs-lookup"><span data-stu-id="8c848-221">6.1</span></span> | <span data-ttu-id="8c848-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="8c848-222">2.6.32-131</span></span> |
| <span data-ttu-id="8c848-223">6.2</span><span class="sxs-lookup"><span data-stu-id="8c848-223">6.2</span></span> | <span data-ttu-id="8c848-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="8c848-224">2.6.32-220</span></span> |
| <span data-ttu-id="8c848-225">6.3</span><span class="sxs-lookup"><span data-stu-id="8c848-225">6.3</span></span> | <span data-ttu-id="8c848-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="8c848-226">2.6.32-279</span></span> |
| <span data-ttu-id="8c848-227">6.4</span><span class="sxs-lookup"><span data-stu-id="8c848-227">6.4</span></span> | <span data-ttu-id="8c848-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="8c848-228">2.6.32-358</span></span> |
| <span data-ttu-id="8c848-229">6.5</span><span class="sxs-lookup"><span data-stu-id="8c848-229">6.5</span></span> | <span data-ttu-id="8c848-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="8c848-230">2.6.32-431</span></span> |
| <span data-ttu-id="8c848-231">6.6</span><span class="sxs-lookup"><span data-stu-id="8c848-231">6.6</span></span> | <span data-ttu-id="8c848-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="8c848-232">2.6.32-504</span></span> |
| <span data-ttu-id="8c848-233">6.7</span><span class="sxs-lookup"><span data-stu-id="8c848-233">6.7</span></span> | <span data-ttu-id="8c848-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="8c848-234">2.6.32-573</span></span> |
| <span data-ttu-id="8c848-235">6.8</span><span class="sxs-lookup"><span data-stu-id="8c848-235">6.8</span></span> | <span data-ttu-id="8c848-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="8c848-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="8c848-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="8c848-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="8c848-238">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-238">**OS version**</span></span> | <span data-ttu-id="8c848-239">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-240">5.8</span><span class="sxs-lookup"><span data-stu-id="8c848-240">5.8</span></span> | <span data-ttu-id="8c848-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="8c848-241">2.6.18-308</span></span> |
| <span data-ttu-id="8c848-242">5.9</span><span class="sxs-lookup"><span data-stu-id="8c848-242">5.9</span></span> | <span data-ttu-id="8c848-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="8c848-243">2.6.18-348</span></span> |
| <span data-ttu-id="8c848-244">5.10</span><span class="sxs-lookup"><span data-stu-id="8c848-244">5.10</span></span> | <span data-ttu-id="8c848-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="8c848-245">2.6.18-371</span></span> |
| <span data-ttu-id="8c848-246">5.11</span><span class="sxs-lookup"><span data-stu-id="8c848-246">5.11</span></span> | <span data-ttu-id="8c848-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="8c848-247">2.6.18-398</span></span> <br> <span data-ttu-id="8c848-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="8c848-248">2.6.18-400</span></span> <br><span data-ttu-id="8c848-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="8c848-249">2.6.18-402</span></span> <br><span data-ttu-id="8c848-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="8c848-250">2.6.18-404</span></span> <br><span data-ttu-id="8c848-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="8c848-251">2.6.18-406</span></span> <br> <span data-ttu-id="8c848-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="8c848-252">2.6.18-407</span></span> <br> <span data-ttu-id="8c848-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="8c848-253">2.6.18-408</span></span> <br> <span data-ttu-id="8c848-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="8c848-254">2.6.18-409</span></span> <br> <span data-ttu-id="8c848-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="8c848-255">2.6.18-410</span></span> <br> <span data-ttu-id="8c848-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="8c848-256">2.6.18-411</span></span> <br> <span data-ttu-id="8c848-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="8c848-257">2.6.18-412</span></span> <br> <span data-ttu-id="8c848-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="8c848-258">2.6.18-416</span></span> <br> <span data-ttu-id="8c848-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="8c848-259">2.6.18-417</span></span> <br> <span data-ttu-id="8c848-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="8c848-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="8c848-261">Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="8c848-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="8c848-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="8c848-262">Oracle Linux 6</span></span>

| <span data-ttu-id="8c848-263">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-263">**OS version**</span></span> | <span data-ttu-id="8c848-264">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-265">6.2</span><span class="sxs-lookup"><span data-stu-id="8c848-265">6.2</span></span> | <span data-ttu-id="8c848-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="8c848-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="8c848-267">6.3</span><span class="sxs-lookup"><span data-stu-id="8c848-267">6.3</span></span> | <span data-ttu-id="8c848-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8c848-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="8c848-269">6.4</span><span class="sxs-lookup"><span data-stu-id="8c848-269">6.4</span></span> | <span data-ttu-id="8c848-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8c848-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="8c848-271">6.5</span><span class="sxs-lookup"><span data-stu-id="8c848-271">6.5</span></span> | <span data-ttu-id="8c848-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="8c848-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="8c848-273">6.6</span><span class="sxs-lookup"><span data-stu-id="8c848-273">6.6</span></span> | <span data-ttu-id="8c848-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="8c848-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="8c848-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="8c848-275">Oracle Linux 5</span></span>

| <span data-ttu-id="8c848-276">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-276">**OS version**</span></span> | <span data-ttu-id="8c848-277">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-278">5.8</span><span class="sxs-lookup"><span data-stu-id="8c848-278">5.8</span></span> | <span data-ttu-id="8c848-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="8c848-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="8c848-280">5.9</span><span class="sxs-lookup"><span data-stu-id="8c848-280">5.9</span></span> | <span data-ttu-id="8c848-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8c848-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="8c848-282">5.10</span><span class="sxs-lookup"><span data-stu-id="8c848-282">5.10</span></span> | <span data-ttu-id="8c848-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8c848-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="8c848-284">5.11</span><span class="sxs-lookup"><span data-stu-id="8c848-284">5.11</span></span> | <span data-ttu-id="8c848-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8c848-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="8c848-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="8c848-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="8c848-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="8c848-287">SUSE Linux 11</span></span>

| <span data-ttu-id="8c848-288">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-288">**OS version**</span></span> | <span data-ttu-id="8c848-289">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-290">11</span><span class="sxs-lookup"><span data-stu-id="8c848-290">11</span></span> | <span data-ttu-id="8c848-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="8c848-291">2.6.27</span></span> |
| <span data-ttu-id="8c848-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="8c848-292">11 SP1</span></span> | <span data-ttu-id="8c848-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="8c848-293">2.6.32</span></span> |
| <span data-ttu-id="8c848-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="8c848-294">11 SP2</span></span> | <span data-ttu-id="8c848-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="8c848-295">3.0.13</span></span> |
| <span data-ttu-id="8c848-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="8c848-296">11 SP3</span></span> | <span data-ttu-id="8c848-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="8c848-297">3.0.76</span></span> |
| <span data-ttu-id="8c848-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="8c848-298">11 SP4</span></span> | <span data-ttu-id="8c848-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="8c848-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="8c848-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="8c848-300">SUSE Linux 10</span></span>

| <span data-ttu-id="8c848-301">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-301">**OS version**</span></span> | <span data-ttu-id="8c848-302">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="8c848-303">10 SP4</span></span> | <span data-ttu-id="8c848-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="8c848-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="8c848-305">相依性代理程式下載</span><span class="sxs-lookup"><span data-stu-id="8c848-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="8c848-306">**檔案**</span><span class="sxs-lookup"><span data-stu-id="8c848-306">**File**</span></span> | <span data-ttu-id="8c848-307">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="8c848-307">**OS**</span></span> | <span data-ttu-id="8c848-308">**版本**</span><span class="sxs-lookup"><span data-stu-id="8c848-308">**Version**</span></span> | <span data-ttu-id="8c848-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="8c848-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="8c848-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="8c848-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="8c848-311">Windows</span><span class="sxs-lookup"><span data-stu-id="8c848-311">Windows</span></span> | <span data-ttu-id="8c848-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="8c848-312">9.0.5</span></span> | <span data-ttu-id="8c848-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="8c848-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="8c848-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="8c848-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="8c848-315">Linux</span><span class="sxs-lookup"><span data-stu-id="8c848-315">Linux</span></span> | <span data-ttu-id="8c848-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="8c848-316">9.0.5</span></span> | <span data-ttu-id="8c848-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="8c848-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="8c848-318">組態</span><span class="sxs-lookup"><span data-stu-id="8c848-318">Configuration</span></span>

<span data-ttu-id="8c848-319">執行下列步驟來設定您工作區的 Wire Data 解決方案。</span><span class="sxs-lookup"><span data-stu-id="8c848-319">Perform the following steps to configure the Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="8c848-320">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Activity Log Analytics 解決方案。</span><span class="sxs-lookup"><span data-stu-id="8c848-320">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="8c848-321">在您想要取得資料的每部電腦上安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-321">Install the Dependency Agent on each computer where you want to get data.</span></span> <span data-ttu-id="8c848-322">相依性代理程式可以監視緊接鄰近點的連線，因此您可能不需要在每部電腦上都有代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-322">The Dependency Agent can monitor connections to immediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-the-dependency-agent-on-windows"></a><span data-ttu-id="8c848-323">在 Windows 上安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-323">Install the Dependency Agent on Windows</span></span>

<span data-ttu-id="8c848-324">必須有系統管理員權限，以便安裝或解除安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-324">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="8c848-325">您可以透過 InstallDependencyAgent-Windows.exe，在執行 Windows 的電腦上安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-325">The Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="8c848-326">如果您在執行此可執行檔時不使用任何選項，則會啟動以互動方式安裝的精靈。</span><span class="sxs-lookup"><span data-stu-id="8c848-326">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>

<span data-ttu-id="8c848-327">請使用下列步驟在每部執行 Windows 的電腦上安裝相依性代理程式：</span><span class="sxs-lookup"><span data-stu-id="8c848-327">Use the following steps to install the Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="8c848-328">遵循[將 Windows 電腦連線到 Azure 中的 Log Analytics 服務](log-analytics-windows-agents.md)的指示來安裝 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-328">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="8c848-329">使用上一節中的連結來下載 Windows 代理程式，然後使用下列命令來執行：InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="8c848-329">Download the Windows agent using the link in the previous section and then run it by using the following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="8c848-330">遵循精靈來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-330">Follow the wizard to install the agent.</span></span>
4. <span data-ttu-id="8c848-331">如果相依性代理程式無法啟動，請檢查記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="8c848-331">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="8c848-332">在 Windows 代理程式上，記錄檔的目錄是 %Programfiles%\Microsoft Dependency Agent\logs。</span><span class="sxs-lookup"><span data-stu-id="8c848-332">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="8c848-333">Windows 命令列</span><span class="sxs-lookup"><span data-stu-id="8c848-333">Windows command line</span></span>

<span data-ttu-id="8c848-334">使用下表中的選項以從命令列安裝。</span><span class="sxs-lookup"><span data-stu-id="8c848-334">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="8c848-335">若要查看安裝旗標的清單，請如下所示使用 /? 旗標執行安裝程式</span><span class="sxs-lookup"><span data-stu-id="8c848-335">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="8c848-336">如下所示。</span><span class="sxs-lookup"><span data-stu-id="8c848-336">flag as follows.</span></span>

<span data-ttu-id="8c848-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="8c848-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="8c848-338">**旗標**</span><span class="sxs-lookup"><span data-stu-id="8c848-338">**Flag**</span></span> | <span data-ttu-id="8c848-339">**說明**</span><span class="sxs-lookup"><span data-stu-id="8c848-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="8c848-340">取得命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="8c848-340">Get a list of the command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="8c848-341">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="8c848-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="8c848-342">Windows 相依性代理程式的檔案預設位於 C:\Program Files\Microsoft Dependency Agent。</span><span class="sxs-lookup"><span data-stu-id="8c848-342">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="8c848-343">在 Linux 上安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-343">Install the Dependency Agent on Linux</span></span>

<span data-ttu-id="8c848-344">必須有 root 權限，以便安裝或設定代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-344">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="8c848-345">透過 InstallDependencyAgent-Linux64.bin (具有自我解壓縮二進位檔的殼層指令碼) 即可在 Linux 電腦上安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-345">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="8c848-346">您可以使用 _sh_ 來執行檔案，或對檔案本身新增執行權限。</span><span class="sxs-lookup"><span data-stu-id="8c848-346">You can run the file by using _sh_ or add execute permissions to the file itself.</span></span>

<span data-ttu-id="8c848-347">請使用下列步驟在每一部 Linux 電腦上安裝相依性代理程式：</span><span class="sxs-lookup"><span data-stu-id="8c848-347">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="8c848-348">遵循[收集並管理來自 Linux 電腦的資料](log-analytics-agent-linux.md)的指示來安裝 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-348">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="8c848-349">使用上一節中的連結來下載 Linux 相依性代理程式，然後使用下列命令將它安裝為根目錄：sh InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="8c848-349">Download the Linux Dependency agent using the link in the previous section and then install it as root by using the following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="8c848-350">如果相依性代理程式無法啟動，請檢查記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="8c848-350">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="8c848-351">在 Linux 代理程式上，記錄檔的目錄是 /var/opt/microsoft/dependency-agent/log。</span><span class="sxs-lookup"><span data-stu-id="8c848-351">On Linux agents, the log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="8c848-352">若要查看安裝旗標的清單，請如下所示以 `-help` 旗標執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-352">To see a list of the installation flags, run the installation program with the `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="8c848-353">**旗標**</span><span class="sxs-lookup"><span data-stu-id="8c848-353">**Flag**</span></span> | <span data-ttu-id="8c848-354">**說明**</span><span class="sxs-lookup"><span data-stu-id="8c848-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="8c848-355">取得命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="8c848-355">Get a list of the command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="8c848-356">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="8c848-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="8c848-357">檢查權限和作業系統，但不會安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-357">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="8c848-358">相依性代理程式的檔案位於下列目錄：</span><span class="sxs-lookup"><span data-stu-id="8c848-358">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="8c848-359">**檔案**</span><span class="sxs-lookup"><span data-stu-id="8c848-359">**Files**</span></span> | <span data-ttu-id="8c848-360">**位置**</span><span class="sxs-lookup"><span data-stu-id="8c848-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-361">核心檔案</span><span class="sxs-lookup"><span data-stu-id="8c848-361">Core files</span></span> | <span data-ttu-id="8c848-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="8c848-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="8c848-363">記錄檔</span><span class="sxs-lookup"><span data-stu-id="8c848-363">Log files</span></span> | <span data-ttu-id="8c848-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="8c848-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="8c848-365">組態檔</span><span class="sxs-lookup"><span data-stu-id="8c848-365">Config files</span></span> | <span data-ttu-id="8c848-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="8c848-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="8c848-367">服務可執行檔</span><span class="sxs-lookup"><span data-stu-id="8c848-367">Service executable files</span></span> | <span data-ttu-id="8c848-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="8c848-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="8c848-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="8c848-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="8c848-370">二進位儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="8c848-370">Binary storage files</span></span> | <span data-ttu-id="8c848-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="8c848-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="8c848-372">安裝指令碼範例</span><span class="sxs-lookup"><span data-stu-id="8c848-372">Installation script examples</span></span>

<span data-ttu-id="8c848-373">使用指令碼可輕鬆地一次部署許多伺服器上的相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-373">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="8c848-374">若要在 Windows 或 Linux 上下載並安裝相依性代理程式，可以使用下列指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="8c848-374">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="8c848-375">適用於 Windows 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="8c848-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="8c848-376">適用於 Linux 的殼層指令碼</span><span class="sxs-lookup"><span data-stu-id="8c848-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="8c848-377">期望的狀態設定</span><span class="sxs-lookup"><span data-stu-id="8c848-377">Desired State Configuration</span></span>

<span data-ttu-id="8c848-378">若要透過 Desired State Configuration 部署相依性代理程式，您可以使用 xPSDesiredStateConfiguration 模組和如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8c848-378">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install the Dependency Agent

    xRemoteFile DAPackage

    {

        Uri = &quot;https://aka.ms/dependencyagentwindows&quot;

        DestinationPath = $DAPackageLocalPath

        DependsOn = &quot;[Package]OI&quot;

    }

    xPackage DA

    {

        Ensure=&quot;Present&quot;

        Name = &quot;Dependency Agent&quot;

        Path = $DAPackageLocalPath

        Arguments = '/S'

        ProductId = &quot;&quot;

        InstalledCheckRegKey = &quot;HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent&quot;

        InstalledCheckRegValueName = &quot;DisplayName&quot;

        InstalledCheckRegValueData = &quot;Dependency Agent&quot;

    }

}

```
### <a name="uninstall-the-dependency-agent"></a><span data-ttu-id="8c848-379">解除安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-379">Uninstall the Dependency Agent</span></span>

<span data-ttu-id="8c848-380">請使用下列各節來協助您移除相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-380">Use the following sections to help you remove the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="8c848-381">在 Windows 上解除安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-381">Uninstall the Dependency Agent on Windows</span></span>

<span data-ttu-id="8c848-382">系統管理員可透過控制台解除安裝 Windows 的相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-382">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="8c848-383">系統管理員也可以執行 %Programfiles%\Microsoft Dependency Agent\Uninstall.exe，以解除安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8c848-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

#### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="8c848-384">在 Linux 上解除安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8c848-384">Uninstall the Dependency Agent on Linux</span></span>

<span data-ttu-id="8c848-385">若要將「相依性代理程式」從 Linux 中完全解除安裝，您必須將代理程式本身及隨代理程式自動安裝的連接器移除。</span><span class="sxs-lookup"><span data-stu-id="8c848-385">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="8c848-386">您可以使用下列單一命令同時解除安裝這兩者：</span><span class="sxs-lookup"><span data-stu-id="8c848-386">You can uninstall both by using the following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="8c848-387">管理組件</span><span class="sxs-lookup"><span data-stu-id="8c848-387">Management packs</span></span>

<span data-ttu-id="8c848-388">在 Log Analytics 工作區中啟動 Wire Data 時，會將 300 KB 的管理組件傳送至該工作區中的所有 Windows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8c848-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="8c848-389">如果您是在[連線的管理群組](log-analytics-om-agents.md)中使用 System Center Operations Manager 代理程式，則會從 System Center Operations Manager 部署相依性監視管理組件。</span><span class="sxs-lookup"><span data-stu-id="8c848-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), the Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="8c848-390">如果代理程式是直接連線，Log Analytics 會提供管理組件。</span><span class="sxs-lookup"><span data-stu-id="8c848-390">If the agents are directly connected, Log Analytics delivers the management pack.</span></span>

<span data-ttu-id="8c848-391">管理組件名稱為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。</span><span class="sxs-lookup"><span data-stu-id="8c848-391">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="8c848-392">它會寫入至 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs。</span><span class="sxs-lookup"><span data-stu-id="8c848-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="8c848-393">管理組件所使用的資料來源是 %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;自動產生的識別碼&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。</span><span class="sxs-lookup"><span data-stu-id="8c848-393">The data source that the management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-the-solution"></a><span data-ttu-id="8c848-394">使用解決方案</span><span class="sxs-lookup"><span data-stu-id="8c848-394">Using the solution</span></span>

<span data-ttu-id="8c848-395">**安裝和設定解決方案**</span><span class="sxs-lookup"><span data-stu-id="8c848-395">**Installing and configuring the solution**</span></span>

<span data-ttu-id="8c848-396">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="8c848-396">Use the following information to install and configure the solution.</span></span>

- <span data-ttu-id="8c848-397">連線資料方案會從執行 Windows Server 2012 R2、Windows 8.1 和更新版本作業系統的電腦取得資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-397">The Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="8c848-398">您想要取得連線資料的來源電腦上需要有 Microsoft.NET Framework 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8c848-398">Microsoft .NET Framework 4.0 or later is required on computers where you want to acquire wire data from.</span></span>
- <span data-ttu-id="8c848-399">使用[從方案庫新增 Log Analytics 解決方案](log-analytics-add-solutions.md)中所述的程序，將 Wire Data 解決方案新增至您的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="8c848-399">Add the Wire Data solution to your Log Analytics workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="8c848-400">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="8c848-400">There is no further configuration required.</span></span>
- <span data-ttu-id="8c848-401">如果您想要檢視特定解決方案的連線資料，必須先將此解決方案新增至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="8c848-401">If you want to view wire data for a specific solution, you need to have the solution already added to your workspace.</span></span>

<span data-ttu-id="8c848-402">依序安裝代理程式和解決方案之後，Wire Data 2.0 磚會出現在您的工作區中。</span><span class="sxs-lookup"><span data-stu-id="8c848-402">After you have agents installed and you install the solution, the Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="8c848-403">目前，您必須使用 OMS 入口網站來檢視連線資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-403">Currently, you must use the OMS portal to view wire data.</span></span> <span data-ttu-id="8c848-404">您無法使用 Azure 入口網站來檢視連線資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-404">You cannot use the Azure portal to view wire data.</span></span>

![Wire Data 磚](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-the-wire-data-20-solution"></a><span data-ttu-id="8c848-406">使用 Wire Data 2.0 解決方案</span><span class="sxs-lookup"><span data-stu-id="8c848-406">Using the Wire Data 2.0 solution</span></span>

<span data-ttu-id="8c848-407">在 OMS 入口網站中，按一下 [Wire Data 2.0] 磚以開啟 Wire Data 儀表板。</span><span class="sxs-lookup"><span data-stu-id="8c848-407">In the OMS portal, click the **Wire Data 2.0** tile to open the Wire Data dashboard.</span></span> <span data-ttu-id="8c848-408">此儀表板包含下表中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8c848-408">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="8c848-409">每個刀鋒視窗最多會列出 10 個與該刀鋒視窗中指定範圍和時間範圍的準則相符的項目。</span><span class="sxs-lookup"><span data-stu-id="8c848-409">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="8c848-410">您可以按一下刀鋒視窗底部的 [查看全部]，或按一下刀鋒視窗標頭，以執行記錄搜尋來傳回所有記錄。</span><span class="sxs-lookup"><span data-stu-id="8c848-410">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

| <span data-ttu-id="8c848-411">**刀鋒視窗**</span><span class="sxs-lookup"><span data-stu-id="8c848-411">**Blade**</span></span> | <span data-ttu-id="8c848-412">**說明**</span><span class="sxs-lookup"><span data-stu-id="8c848-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8c848-413">擷取網路流量的代理程式數</span><span class="sxs-lookup"><span data-stu-id="8c848-413">Agents capturing network traffic</span></span> | <span data-ttu-id="8c848-414">顯示擷取網路流量的代理程式數，並列出擷取最多流量的前 10 部電腦。</span><span class="sxs-lookup"><span data-stu-id="8c848-414">Shows the number of agents that are capturing network traffic and lists the top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="8c848-415">按一下此數字可執行記錄搜尋，以搜尋 <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>。</span><span class="sxs-lookup"><span data-stu-id="8c848-415">Click the number to run a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="8c848-416">按一下清單中的電腦可執行記錄搜尋，以傳回擷取的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="8c848-416">Click a computer in the list to run a log search returning the total number of bytes captured.</span></span> |
| <span data-ttu-id="8c848-417">區域子網路數</span><span class="sxs-lookup"><span data-stu-id="8c848-417">Local Subnets</span></span> | <span data-ttu-id="8c848-418">顯示代理程式探索到的區域子網路數。</span><span class="sxs-lookup"><span data-stu-id="8c848-418">Shows the number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="8c848-419">按一下此數字可執行記錄搜尋，以搜尋 <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code>，其中列出所有子網路及透過每個子網路傳送的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="8c848-419">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with the number of bytes sent over each one.</span></span> <span data-ttu-id="8c848-420">按一下清單中的子網路可執行記錄搜尋，以傳回透過子網路傳送的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="8c848-420">Click a subnet in the list to run a log search returning the total number of bytes sent over the subnet.</span></span> |
| <span data-ttu-id="8c848-421">應用程式層級通訊協定數</span><span class="sxs-lookup"><span data-stu-id="8c848-421">Application-level Protocols</span></span> | <span data-ttu-id="8c848-422">顯示代理程式探索到的使用中應用程式層級通訊協定數。</span><span class="sxs-lookup"><span data-stu-id="8c848-422">Shows the number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="8c848-423">按一下此數字可執行記錄搜尋，以搜尋 <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>。</span><span class="sxs-lookup"><span data-stu-id="8c848-423">Click the number to run a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="8c848-424">按一下通訊協定可執行記錄搜尋，以傳回使用該通訊協定傳送的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="8c848-424">Click a protocol to run a log search returning the total number of bytes sent using the protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 儀表板](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="8c848-426">您可以使用 [擷取網路流量的代理程式數] 刀鋒視窗，來判斷電腦所耗用的網路頻寬量。</span><span class="sxs-lookup"><span data-stu-id="8c848-426">You can use the **Agents capturing network traffic** blade to determine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="8c848-427">此刀鋒視窗可協助您輕鬆找到環境中「通訊量最大」的電腦。</span><span class="sxs-lookup"><span data-stu-id="8c848-427">This blade can help you easily find the _chattiest_ computer in your environment.</span></span> <span data-ttu-id="8c848-428">這類電腦可能超載、運作異常，或使用的網路資源不尋常地過多。</span><span class="sxs-lookup"><span data-stu-id="8c848-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="8c848-430">同樣地，您可以使用 [區域子網路數] 刀鋒視窗，來判斷透過子網路移動的網路流量。</span><span class="sxs-lookup"><span data-stu-id="8c848-430">Similarly, you can use the **Local Subnets** blade to determine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="8c848-431">使用者通常會為其應用程式定義重要區域周圍的子網路。</span><span class="sxs-lookup"><span data-stu-id="8c848-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="8c848-432">此刀鋒視窗會提供這些區域的檢視。</span><span class="sxs-lookup"><span data-stu-id="8c848-432">This blade offers a view into those areas.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="8c848-434">[應用程式層級通訊協定數] 刀鋒視窗可協助了解使用中的通訊協定，因此很有用。</span><span class="sxs-lookup"><span data-stu-id="8c848-434">The **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="8c848-435">例如，您可能預期 SSH 不會用於網路環境中。</span><span class="sxs-lookup"><span data-stu-id="8c848-435">For example, you might expect SSH to not be in use in your network environment.</span></span> <span data-ttu-id="8c848-436">藉由檢視刀鋒視窗中可用的資訊，即可快速確認或否認您的預期。</span><span class="sxs-lookup"><span data-stu-id="8c848-436">Viewing information available in the blade can quickly confirm or disprove your expectation.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="8c848-438">在此範例中，您可以鑽研 SSH 詳細資料，以查看哪些電腦正在使用 SSH 及許多其他通訊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-438">In this example, you could drill-into SSH details to see which computers are using SSH and many other communication details.</span></span>

![sh 搜尋結果](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="8c848-440">它也有助於了解通訊協定流量是否隨時間增加或減少。</span><span class="sxs-lookup"><span data-stu-id="8c848-440">It's also useful to know if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="8c848-441">例如，如果應用程式所傳輸的資料量增加，可能有應該注意或值得關注的問題。</span><span class="sxs-lookup"><span data-stu-id="8c848-441">For example, if the amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="8c848-442">輸入資料</span><span class="sxs-lookup"><span data-stu-id="8c848-442">Input data</span></span>

<span data-ttu-id="8c848-443">連線資料會使用您已啟用的代理程式，來收集有關網路流量的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-443">Wire data collects metadata about network traffic using the agents that you have enabled.</span></span> <span data-ttu-id="8c848-444">每個代理程式約每隔 15 秒傳送一次資料。</span><span class="sxs-lookup"><span data-stu-id="8c848-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="8c848-445">輸出資料</span><span class="sxs-lookup"><span data-stu-id="8c848-445">Output data</span></span>

<span data-ttu-id="8c848-446">對於每種類型的輸入資料，系統會建立 _WireData_ 類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="8c848-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="8c848-447">WireData 記錄具有下表所示的屬性：</span><span class="sxs-lookup"><span data-stu-id="8c848-447">WireData records have properties shown in the following table:</span></span>

| <span data-ttu-id="8c848-448">屬性</span><span class="sxs-lookup"><span data-stu-id="8c848-448">Property</span></span> | <span data-ttu-id="8c848-449">說明</span><span class="sxs-lookup"><span data-stu-id="8c848-449">Description</span></span> |
|---|---|
| <span data-ttu-id="8c848-450">電腦</span><span class="sxs-lookup"><span data-stu-id="8c848-450">Computer</span></span> | <span data-ttu-id="8c848-451">收集資料所在的電腦名稱</span><span class="sxs-lookup"><span data-stu-id="8c848-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="8c848-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="8c848-452">TimeGenerated</span></span> | <span data-ttu-id="8c848-453">記錄的時間</span><span class="sxs-lookup"><span data-stu-id="8c848-453">Time of the record</span></span> |
| <span data-ttu-id="8c848-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="8c848-454">LocalIP</span></span> | <span data-ttu-id="8c848-455">本機電腦的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8c848-455">IP address of the local computer</span></span> |
| <span data-ttu-id="8c848-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="8c848-456">SessionState</span></span> | <span data-ttu-id="8c848-457">已連線或已中斷連線</span><span class="sxs-lookup"><span data-stu-id="8c848-457">Connected or disconnected</span></span> |
| <span data-ttu-id="8c848-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="8c848-458">ReceivedBytes</span></span> | <span data-ttu-id="8c848-459">接收的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8c848-459">Amount of bytes received</span></span> |
| <span data-ttu-id="8c848-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="8c848-460">ProtocolName</span></span> | <span data-ttu-id="8c848-461">使用的網路通訊協定名稱</span><span class="sxs-lookup"><span data-stu-id="8c848-461">Name of the network protocol used</span></span> |
| <span data-ttu-id="8c848-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="8c848-462">IPVersion</span></span> | <span data-ttu-id="8c848-463">IP 版本</span><span class="sxs-lookup"><span data-stu-id="8c848-463">IP version</span></span> |
| <span data-ttu-id="8c848-464">方向</span><span class="sxs-lookup"><span data-stu-id="8c848-464">Direction</span></span> | <span data-ttu-id="8c848-465">輸入或輸出</span><span class="sxs-lookup"><span data-stu-id="8c848-465">Inbound or outbound</span></span> |
| <span data-ttu-id="8c848-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="8c848-466">MaliciousIP</span></span> | <span data-ttu-id="8c848-467">已知惡意來源的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8c848-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="8c848-468">嚴重性</span><span class="sxs-lookup"><span data-stu-id="8c848-468">Severity</span></span> | <span data-ttu-id="8c848-469">可疑惡意程式碼嚴重性</span><span class="sxs-lookup"><span data-stu-id="8c848-469">Suspected malware severity</span></span> |
| <span data-ttu-id="8c848-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="8c848-470">RemoteIPCountry</span></span> | <span data-ttu-id="8c848-471">遠端 IP 位址的國家/地區</span><span class="sxs-lookup"><span data-stu-id="8c848-471">Country of the remote IP address</span></span> |
| <span data-ttu-id="8c848-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="8c848-472">ManagementGroupName</span></span> | <span data-ttu-id="8c848-473">Operations Manager 管理群組的名稱</span><span class="sxs-lookup"><span data-stu-id="8c848-473">Name of the Operations Manager management group</span></span> |
| <span data-ttu-id="8c848-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="8c848-474">SourceSystem</span></span> | <span data-ttu-id="8c848-475">收集資料所在的來源</span><span class="sxs-lookup"><span data-stu-id="8c848-475">Source where data was collected</span></span> |
| <span data-ttu-id="8c848-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="8c848-476">SessionStartTime</span></span> | <span data-ttu-id="8c848-477">工作階段的開始時間</span><span class="sxs-lookup"><span data-stu-id="8c848-477">Start time of session</span></span> |
| <span data-ttu-id="8c848-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="8c848-478">SessionEndTime</span></span> | <span data-ttu-id="8c848-479">工作階段的結束時間</span><span class="sxs-lookup"><span data-stu-id="8c848-479">End time of session</span></span> |
| <span data-ttu-id="8c848-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="8c848-480">LocalSubnet</span></span> | <span data-ttu-id="8c848-481">收集資料所在的子網路</span><span class="sxs-lookup"><span data-stu-id="8c848-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="8c848-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="8c848-482">LocalPortNumber</span></span> | <span data-ttu-id="8c848-483">本機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="8c848-483">Local port number</span></span> |
| <span data-ttu-id="8c848-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="8c848-484">RemoteIP</span></span> | <span data-ttu-id="8c848-485">遠端電腦所使用的遠端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8c848-485">Remote IP address used by the remote computer</span></span> |
| <span data-ttu-id="8c848-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="8c848-486">RemotePortNumber</span></span> | <span data-ttu-id="8c848-487">遠端 IP 位址所使用的連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="8c848-487">Port number used by the remote IP address</span></span> |
| <span data-ttu-id="8c848-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="8c848-488">SessionID</span></span> | <span data-ttu-id="8c848-489">識別兩個 IP 位址之間通訊工作階段的唯一值</span><span class="sxs-lookup"><span data-stu-id="8c848-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="8c848-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="8c848-490">SentBytes</span></span> | <span data-ttu-id="8c848-491">傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8c848-491">Number of bytes sent</span></span> |
| <span data-ttu-id="8c848-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="8c848-492">TotalBytes</span></span> | <span data-ttu-id="8c848-493">工作階段期間傳送的位元組總數</span><span class="sxs-lookup"><span data-stu-id="8c848-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="8c848-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="8c848-494">ApplicationProtocol</span></span> | <span data-ttu-id="8c848-495">使用的網路通訊協定類型</span><span class="sxs-lookup"><span data-stu-id="8c848-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="8c848-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="8c848-496">ProcessID</span></span> | <span data-ttu-id="8c848-497">Windows 處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="8c848-497">Windows process ID</span></span> |
| <span data-ttu-id="8c848-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="8c848-498">ProcessName</span></span> | <span data-ttu-id="8c848-499">處理序的路徑和檔案名稱</span><span class="sxs-lookup"><span data-stu-id="8c848-499">Path and file name of the process</span></span> |
| <span data-ttu-id="8c848-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="8c848-500">RemoteIPLongitude</span></span> | <span data-ttu-id="8c848-501">IP 經度值</span><span class="sxs-lookup"><span data-stu-id="8c848-501">IP longitude value</span></span> |
| <span data-ttu-id="8c848-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="8c848-502">RemoteIPLatitude</span></span> | <span data-ttu-id="8c848-503">IP 緯度值</span><span class="sxs-lookup"><span data-stu-id="8c848-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8c848-504">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c848-504">Next steps</span></span>

- <span data-ttu-id="8c848-505">[搜尋記錄檔](log-analytics-log-searches.md) 以檢視詳細的連線資料搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="8c848-505">[Search logs](log-analytics-log-searches.md) to view detailed wire data search records.</span></span>
