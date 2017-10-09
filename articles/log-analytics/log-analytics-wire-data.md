---
title: "aaaWire 中記錄分析資料方案 |Microsoft 文件"
description: "網路資料是來自具有 OMS 代理程式 (包括 Operations Manager 和 Windows 連線的代理程式) 的電腦的網路和效能彙總資料。 網路資料會結合您的記錄檔資料 toohelp 與相互關聯資料。"
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
ms.openlocfilehash: adafdf98dfbda9d87759643a1a606a84eafd1348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="wire-data-20-preview-solution-in-log-analytics"></a><span data-ttu-id="8256b-104">Log Analytics 中的 Wire Data 2.0 (預覽) 解決方案</span><span class="sxs-lookup"><span data-stu-id="8256b-104">Wire Data 2.0 (Preview) solution in Log Analytics</span></span>

![Wire Data 符號](./media/log-analytics-wire-data/wire-data2-symbol.png)

<span data-ttu-id="8256b-106">連線資料是來自具有 OMS 代理程式 (包括 Operations Manager、Windows 連線和 Linux 代理程式) 之電腦的網路和效能彙總資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-106">Wire data is consolidated network and performance data from computers with OMS agents, including Operations Manager, Windows-connected, and Linux agents.</span></span> <span data-ttu-id="8256b-107">網路資料會結合您其他的記錄檔資料 toohelp 與相互關聯資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-107">Network data is combined with your other log data toohelp you correlate data.</span></span>

<span data-ttu-id="8256b-108">此外 tooOMS 代理程式，hello 網路資料 」 解決方案會使用您電腦安裝在您的 IT 基礎結構的 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-108">In addition tooOMS agents, hello Wire Data solution uses Microsoft Dependency agents that you install on computers in your IT infrastructure.</span></span> <span data-ttu-id="8256b-109">相依性代理程式監視網路傳送資料 tooand 從您的電腦以網路層級 2-3 中的 hello [OSI 模型](https://en.wikipedia.org/wiki/OSI_model)，包括 hello 各種通訊協定和連接埠。</span><span class="sxs-lookup"><span data-stu-id="8256b-109">Dependency Agents monitor network data sent tooand from your computers for network levels 2-3 in hello [OSI model](https://en.wikipedia.org/wiki/OSI_model), including hello various protocols and ports used.</span></span> <span data-ttu-id="8256b-110">然後資料會傳送 tooLog 分析使用代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-110">Data is then sent tooLog Analytics using agents.</span></span>

> [!NOTE]
> <span data-ttu-id="8256b-111">您無法加入 hello 舊版 hello 網路資料解決方案 toonew 工作區。</span><span class="sxs-lookup"><span data-stu-id="8256b-111">You cannot add hello previous version of hello Wire Data solution toonew workspaces.</span></span> <span data-ttu-id="8256b-112">如果您擁有 hello 啟用原始網路資料解決方案，您可以繼續 toouse 它。</span><span class="sxs-lookup"><span data-stu-id="8256b-112">If you have hello original Wire Data solution enabled, you can continue toouse it.</span></span> <span data-ttu-id="8256b-113">不過，toouse 網路資料 2.0，您必須先移除 hello 原始版本。</span><span class="sxs-lookup"><span data-stu-id="8256b-113">However, toouse Wire Data 2.0, you must first remove hello original version.</span></span>

<span data-ttu-id="8256b-114">根據預設，Log Analytics 會從 Windows 內建的計數器收集記錄的資料，包括 CPU、記憶體、磁碟和網路效能資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-114">By default, Log Analytics collects logged data for CPU, memory, disk, and network performance data from counters built into Windows.</span></span> <span data-ttu-id="8256b-115">網路和其他資料收集會即時進行每個代理程式，包括子網路和 hello 電腦正在使用的應用程式層級通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8256b-115">Network and other data collection is done in real-time for each agent, including subnets and application-level protocols being used by hello computer.</span></span> <span data-ttu-id="8256b-116">Hello hello 記錄檔 索引標籤上設定 頁面上，您可以加入其他效能計數器。</span><span class="sxs-lookup"><span data-stu-id="8256b-116">You can add other performance counters on hello Settings page on hello Logs tab.</span></span>

<span data-ttu-id="8256b-117">如果您曾經使用[sFlow](http://www.sflow.org/)或其他軟體搭配[Cisco NetFlow 通訊協定](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html)然後 hello 統計資料，您會看到來自網路資料的資料將會熟悉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="8256b-117">If you've used [sFlow](http://www.sflow.org/) or other software with [Cisco's NetFlow protocol](http://www.cisco.com/c/en/us/products/collateral/ios-nx-os-software/ios-netflow/prod_white_paper0900aecd80406232.html), then hello statistics and data you see from wire data will be familiar tooyou.</span></span>

<span data-ttu-id="8256b-118">內建的記錄搜尋查詢的 hello 類型包括：</span><span class="sxs-lookup"><span data-stu-id="8256b-118">Some of hello types of built-in Log search queries include:</span></span>

- <span data-ttu-id="8256b-119">提供連線資料的代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-119">Agents that provide wire data</span></span>
- <span data-ttu-id="8256b-120">提供連線資料的代理程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8256b-120">IP address of agents providing wire data</span></span>
- <span data-ttu-id="8256b-121">依 IP 位址的輸出通訊</span><span class="sxs-lookup"><span data-stu-id="8256b-121">Outbound communications by IP addresses</span></span>
- <span data-ttu-id="8256b-122">應用程式通訊協定傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8256b-122">Number of bytes sent by application protocols</span></span>
- <span data-ttu-id="8256b-123">應用程式服務傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8256b-123">Number of bytes sent by an application service</span></span>
- <span data-ttu-id="8256b-124">不同通訊協定接收的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8256b-124">Bytes received by different protocols</span></span>
- <span data-ttu-id="8256b-125">IP 版本傳送及接收的位元組總數</span><span class="sxs-lookup"><span data-stu-id="8256b-125">Total bytes sent and received by IP version</span></span>
- <span data-ttu-id="8256b-126">可靠測量的連線平均延遲</span><span class="sxs-lookup"><span data-stu-id="8256b-126">Average latency for connections that were measured reliably</span></span>
- <span data-ttu-id="8256b-127">起始或接收網路流量的電腦處理程序</span><span class="sxs-lookup"><span data-stu-id="8256b-127">Computer processes that initiated or received network traffic</span></span>
- <span data-ttu-id="8256b-128">處理程序的網路流量</span><span class="sxs-lookup"><span data-stu-id="8256b-128">Amount of network traffic for a process</span></span>

<span data-ttu-id="8256b-129">當您使用網路資料搜尋時，您可以篩選和群組資料 tooview 資訊 hello 最上層的代理程式 」 和 「 最上層通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8256b-129">When you search using wire data, you can filter and group data tooview information about hello top agents and top protocols.</span></span> <span data-ttu-id="8256b-130">或者，您可以檢視某些電腦 (IP 位址/MAC 位址) 何時彼此通訊、持續時間，以及已傳送的資料量；基本上，就是在檢視以搜尋為基礎之網路流量的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-130">Or you can view when certain computers (IP addresses/MAC addresses) communicated with each other, for how long, and how much data was sent—basically, you view metadata about network traffic, which is search-based.</span></span>

<span data-ttu-id="8256b-131">不過，因為是檢視中繼資料，在深入的疑難排解中不見得實用。</span><span class="sxs-lookup"><span data-stu-id="8256b-131">However, since you're viewing metadata, it's not necessarily useful for in-depth troubleshooting.</span></span> <span data-ttu-id="8256b-132">Log Analytics 中的連線資料不是完整擷取的網路資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-132">Wire data in Log Analytics is not a full capture of network data.</span></span> <span data-ttu-id="8256b-133">因此，不適用於封包層級的深入疑難排解。</span><span class="sxs-lookup"><span data-stu-id="8256b-133">So, it's not intended for deep packet-level troubleshooting.</span></span> <span data-ttu-id="8256b-134">hello 使用 hello 代理程式的優點，比較 tooother 收集方法，是您不具有 tooinstall 應用裝置、 重新設定網路交換器，或執行複雜的組態。</span><span class="sxs-lookup"><span data-stu-id="8256b-134">hello advantage of using hello agent, compared tooother collection methods, is that you don't have tooinstall appliances, reconfigure your network switches, or preform complicated configurations.</span></span> <span data-ttu-id="8256b-135">網路資料就是以代理程式為基礎，您的電腦上安裝 hello 代理程式，它會監視自己的網路流量。</span><span class="sxs-lookup"><span data-stu-id="8256b-135">Wire data is simply agent-based—you install hello agent on a computer and it will monitor its own network traffic.</span></span> <span data-ttu-id="8256b-136">另一個優點是當您想 toomonitor 雲端提供者或主機服務提供者或 Microsoft Azure，情形 hello 使用者並未擁有 hello 網狀架構圖層中執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="8256b-136">Another advantage is when you want toomonitor workloads running in cloud providers or hosting service provider or Microsoft Azure, where hello user doesn't own hello fabric layer.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="8256b-137">連接的來源</span><span class="sxs-lookup"><span data-stu-id="8256b-137">Connected sources</span></span>

<span data-ttu-id="8256b-138">網路資料會從 hello Microsoft 相依性代理程式取得其資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-138">Wire Data gets its data from hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="8256b-139">hello 相依性代理程式，取決於其連線 tooLog 分析的 hello OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-139">hello Dependency Agent depends on hello OMS Agent for its connections tooLog Analytics.</span></span> <span data-ttu-id="8256b-140">這表示，伺服器必須擁有的 hello OMS 代理程式安裝和設定第一個，然後安裝 hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-140">This means that a server must have hello OMS Agent installed and configured first, and then you install hello Dependency Agent.</span></span> <span data-ttu-id="8256b-141">hello 下表描述 hello 網路資料解決方案支援的 hello 連接來源。</span><span class="sxs-lookup"><span data-stu-id="8256b-141">hello following table describes hello connected sources that hello Wire Data solution supports.</span></span>

| <span data-ttu-id="8256b-142">**連線的來源**</span><span class="sxs-lookup"><span data-stu-id="8256b-142">**Connected source**</span></span> | <span data-ttu-id="8256b-143">**支援**</span><span class="sxs-lookup"><span data-stu-id="8256b-143">**Supported**</span></span> | <span data-ttu-id="8256b-144">**說明**</span><span class="sxs-lookup"><span data-stu-id="8256b-144">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8256b-145">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-145">Windows agents</span></span> | <span data-ttu-id="8256b-146">是</span><span class="sxs-lookup"><span data-stu-id="8256b-146">Yes</span></span> | <span data-ttu-id="8256b-147">Wire Data 會分析並收集來自 Windows 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-147">Wire Data analyzes and collects data from Windows agent computers.</span></span> <br><br> <span data-ttu-id="8256b-148">在加法 toohello [OMS Agent](log-analytics-windows-agents.md)，Windows 代理程式需要 hello Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-148">In addition toohello [OMS Agent](log-analytics-windows-agents.md), Windows agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="8256b-149">請參閱 hello[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)如需完整的作業系統版本清單。</span><span class="sxs-lookup"><span data-stu-id="8256b-149">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="8256b-150">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-150">Linux agents</span></span> | <span data-ttu-id="8256b-151">是</span><span class="sxs-lookup"><span data-stu-id="8256b-151">Yes</span></span> | <span data-ttu-id="8256b-152">Wire Data 會分析並收集來自 Linux 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-152">Wire Data analyzes and collects data from Linux agent computers.</span></span><br><br> <span data-ttu-id="8256b-153">在加法 toohello [OMS Agent](log-analytics-linux-agents.md)，Linux 代理程式需要 hello Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-153">In addition toohello [OMS Agent](log-analytics-linux-agents.md), Linux agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="8256b-154">請參閱 hello[支援的作業系統](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems)如需完整的作業系統版本清單。</span><span class="sxs-lookup"><span data-stu-id="8256b-154">See hello [supported operating systems](../operations-management-suite/operations-management-suite-service-map-configure.md#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="8256b-155">System Center Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="8256b-155">System Center Operations Manager management group</span></span> | <span data-ttu-id="8256b-156">是</span><span class="sxs-lookup"><span data-stu-id="8256b-156">Yes</span></span> | <span data-ttu-id="8256b-157">Wire Data 會在連線的 [System Center Operations Manager 管理群組](log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-157">Wire Data analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](log-analytics-om-agents.md).</span></span> <br><br> <span data-ttu-id="8256b-158">直接從 hello System Center Operations Manager 代理程式電腦 tooLog 分析需要連接。</span><span class="sxs-lookup"><span data-stu-id="8256b-158">A direct connection from hello System Center Operations Manager agent computer tooLog Analytics is required.</span></span> <span data-ttu-id="8256b-159">從 hello 管理群組 tooLog 分析，就會轉送資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-159">Data is forwarded from hello management group tooLog Analytics.</span></span> |
| <span data-ttu-id="8256b-160">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8256b-160">Azure storage account</span></span> | <span data-ttu-id="8256b-161">否</span><span class="sxs-lookup"><span data-stu-id="8256b-161">No</span></span> | <span data-ttu-id="8256b-162">網路資料收集資料從代理程式的電腦，所以沒有從其資料從 Azure 儲存體 toocollect。</span><span class="sxs-lookup"><span data-stu-id="8256b-162">Wire Data collects data from agent computers, so there is no data from it toocollect from Azure Storage.</span></span> |

<span data-ttu-id="8256b-163">在 Windows 中，由 System Center Operations Manager 和記錄分析 toogather hello Microsoft Monitoring Agent (MMA)，並傳送資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-163">On Windows, hello Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Log Analytics toogather and send data.</span></span> <span data-ttu-id="8256b-164">根據 hello 內容 hello 代理程式稱為 hello System Center Operations Manager 代理程式、 OMS 代理程式、 記錄分析代理程式、 MMA 或直接代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-164">Depending on hello context, hello agent is called hello System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent.</span></span> <span data-ttu-id="8256b-165">System Center Operations Manager 和 Log Analytics 提供的 hello MMA 稍有不同的版本。</span><span class="sxs-lookup"><span data-stu-id="8256b-165">System Center Operations Manager and Log Analytics provide slightly different versions of hello MMA.</span></span> <span data-ttu-id="8256b-166">這些版本可以每個報告 tooSystem Center Operations Manager、 tooLog 分析或 tooboth。</span><span class="sxs-lookup"><span data-stu-id="8256b-166">These versions can each report tooSystem Center Operations Manager, tooLog Analytics, or tooboth.</span></span>

<span data-ttu-id="8256b-167">在 Linux 上 hello OMS Agent for Linux 收集並傳送資料 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="8256b-167">On Linux, hello OMS Agent for Linux gathers and sends data tooLog Analytics.</span></span> <span data-ttu-id="8256b-168">附加的 tooLog 分析透過 System Center Operations Manager 管理群組的伺服器或與 OMS 直接代理程式伺服器上，您可以使用網路資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-168">You can use Wire Data on servers with OMS Direct Agents or on servers that are attached tooLog Analytics via System Center Operations Manager management groups.</span></span>

<span data-ttu-id="8256b-169">在本文中，參考 tooall 代理程式，是否 Linux 或 Windows 中，連接的 tooa System Center Operations Manager 管理群組，或直接 tooLog 分析是否會稱為 hello _OMS agent_。</span><span class="sxs-lookup"><span data-stu-id="8256b-169">In this article, references tooall agents, whether Linux or Windows, whether connected tooa System Center Operations Manager management group or directly tooLog Analytics are termed hello _OMS agent_.</span></span> <span data-ttu-id="8256b-170">只有當它所需的內容，我們將使用 hello hello 代理程式的特定部署名稱。</span><span class="sxs-lookup"><span data-stu-id="8256b-170">We'll use hello specific deployment name of hello agent only if it's needed for context.</span></span>

<span data-ttu-id="8256b-171">hello 相依性代理程式不會傳輸任何資料本身，並不需要任何變更 toofirewalls 或連接埠。</span><span class="sxs-lookup"><span data-stu-id="8256b-171">hello Dependency Agent does not transmit any data itself, and it does not require any changes toofirewalls or ports.</span></span> <span data-ttu-id="8256b-172">網路資料中的 hello 資料永遠傳輸的 hello OMS 代理程式 tooLog 分析，請直接或使用 hello OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="8256b-172">hello data in Wire Data is always transmitted by hello OMS agent tooLog Analytics, either directly or using hello OMS Gateway.</span></span>

![代理程式圖表](./media/log-analytics-wire-data/agents.png)

<span data-ttu-id="8256b-174">如果您是 System Center Operations Manager 使用者與管理群組連線 tooLog 分析：</span><span class="sxs-lookup"><span data-stu-id="8256b-174">If you are a System Center Operations Manager user with a management group connected tooLog Analytics:</span></span>

- <span data-ttu-id="8256b-175">System Center Operations Manager 代理程式可以存取 hello 網際網路 tooconnect tooLog 分析不時，需要任何額外的設定。</span><span class="sxs-lookup"><span data-stu-id="8256b-175">No additional configuration is required when your System Center Operations Manager agents can access hello Internet tooconnect tooLog Analytics.</span></span>
- <span data-ttu-id="8256b-176">System Center Operations Manager 代理程式無法存取記錄分析透過 hello 網際網路時，您會需要 tooconfigure hello OMS 閘道 toowork 與 System Center Operations Manager。</span><span class="sxs-lookup"><span data-stu-id="8256b-176">You need tooconfigure hello OMS Gateway toowork with System Center Operations Manager when your System Center Operations Manager agents cannot access Log Analytics over hello Internet.</span></span>

<span data-ttu-id="8256b-177">如果您使用 hello 直接代理程式，您需要 tooconfigure hello OMS 代理程式本身，tooconnect tooLog 分析或 tooyour OMS 閘道也一樣。</span><span class="sxs-lookup"><span data-stu-id="8256b-177">If you are using hello Direct Agent, you need tooconfigure hello OMS agent itself tooconnect tooLog Analytics or tooyour OMS Gateway.</span></span> <span data-ttu-id="8256b-178">您可以從 hello 下載 hello OMS 閘道[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666)。</span><span class="sxs-lookup"><span data-stu-id="8256b-178">You can download hello OMS Gateway from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8256b-179">必要條件</span><span class="sxs-lookup"><span data-stu-id="8256b-179">Prerequisites</span></span>

- <span data-ttu-id="8256b-180">需要 hello[深入剖析和分析](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing)解決方案供應項目。</span><span class="sxs-lookup"><span data-stu-id="8256b-180">Requires hello [Insight and Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite-pricing) solution offer.</span></span>
- <span data-ttu-id="8256b-181">如果您使用網路資料解決方案 hello hello 舊版本，您必須先將它移除。</span><span class="sxs-lookup"><span data-stu-id="8256b-181">If you're using hello previous version of hello Wire Data solution, you must first remove it.</span></span> <span data-ttu-id="8256b-182">不過，透過 hello 原始的網路資料解決方案擷取所有資料都是網路資料 2.0 和記錄搜尋中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="8256b-182">However, all data captured through hello original Wire Data solution is still available in Wire Data 2.0 and log search.</span></span>
- <span data-ttu-id="8256b-183">系統管理員權限需要的 tooinstall 或解除安裝 hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-183">Administrator privileges are required tooinstall or uninstall hello Dependency Agent.</span></span>
- <span data-ttu-id="8256b-184">hello 相依性代理程式必須安裝具有 64 位元作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="8256b-184">hello Dependency Agent must be installed on a computer with a 64-bit operating system.</span></span>

### <a name="operating-systems"></a><span data-ttu-id="8256b-185">作業系統</span><span class="sxs-lookup"><span data-stu-id="8256b-185">Operating systems</span></span>

<span data-ttu-id="8256b-186">hello 下列各節列出 hello 支援的作業系統 hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-186">hello following sections list hello supported operating systems for hello Dependency Agent.</span></span> <span data-ttu-id="8256b-187">Wire Data 不支援任何 32 位元架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="8256b-187">Wire Data doesn't support 32-bit architectures for any operating system.</span></span>

#### <a name="windows-server"></a><span data-ttu-id="8256b-188">Windows Server</span><span class="sxs-lookup"><span data-stu-id="8256b-188">Windows Server</span></span>

- <span data-ttu-id="8256b-189">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="8256b-189">Windows Server 2016</span></span>
- <span data-ttu-id="8256b-190">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8256b-190">Windows Server 2012 R2</span></span>
- <span data-ttu-id="8256b-191">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="8256b-191">Windows Server 2012</span></span>
- <span data-ttu-id="8256b-192">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="8256b-192">Windows Server 2008 R2 SP1</span></span>

#### <a name="windows-desktop"></a><span data-ttu-id="8256b-193">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="8256b-193">Windows desktop</span></span>

- <span data-ttu-id="8256b-194">Windows 10</span><span class="sxs-lookup"><span data-stu-id="8256b-194">Windows 10</span></span>
- <span data-ttu-id="8256b-195">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="8256b-195">Windows 8.1</span></span>
- <span data-ttu-id="8256b-196">Windows 8</span><span class="sxs-lookup"><span data-stu-id="8256b-196">Windows 8</span></span>
- <span data-ttu-id="8256b-197">Windows 7</span><span class="sxs-lookup"><span data-stu-id="8256b-197">Windows 7</span></span>

#### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="8256b-198">Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)</span><span class="sxs-lookup"><span data-stu-id="8256b-198">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>

- <span data-ttu-id="8256b-199">只支援預設版本和 SMP Linux 核心版本。</span><span class="sxs-lookup"><span data-stu-id="8256b-199">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="8256b-200">所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。</span><span class="sxs-lookup"><span data-stu-id="8256b-200">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="8256b-201">例如，與 hello 版本字串的系統_2.6.16.21-0.8-xen_不支援。</span><span class="sxs-lookup"><span data-stu-id="8256b-201">For example, a system with hello release string of _2.6.16.21-0.8-xen_ is not supported.</span></span>
- <span data-ttu-id="8256b-202">不支援自訂核心，包括重新編譯的標準核心。</span><span class="sxs-lookup"><span data-stu-id="8256b-202">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="8256b-203">不支援 CentOSPlus 核心。</span><span class="sxs-lookup"><span data-stu-id="8256b-203">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="8256b-204">Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。</span><span class="sxs-lookup"><span data-stu-id="8256b-204">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>

#### <a name="red-hat-linux-7"></a><span data-ttu-id="8256b-205">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="8256b-205">Red Hat Linux 7</span></span>

| <span data-ttu-id="8256b-206">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-206">**OS version**</span></span> | <span data-ttu-id="8256b-207">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-207">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-208">7.0</span><span class="sxs-lookup"><span data-stu-id="8256b-208">7.0</span></span> | <span data-ttu-id="8256b-209">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="8256b-209">3.10.0-123</span></span> |
| <span data-ttu-id="8256b-210">7.1</span><span class="sxs-lookup"><span data-stu-id="8256b-210">7.1</span></span> | <span data-ttu-id="8256b-211">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="8256b-211">3.10.0-229</span></span> |
| <span data-ttu-id="8256b-212">7.2</span><span class="sxs-lookup"><span data-stu-id="8256b-212">7.2</span></span> | <span data-ttu-id="8256b-213">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="8256b-213">3.10.0-327</span></span> |
| <span data-ttu-id="8256b-214">7.3</span><span class="sxs-lookup"><span data-stu-id="8256b-214">7.3</span></span> | <span data-ttu-id="8256b-215">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="8256b-215">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="8256b-216">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="8256b-216">Red Hat Linux 6</span></span>

| <span data-ttu-id="8256b-217">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-217">**OS version**</span></span> | <span data-ttu-id="8256b-218">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-218">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-219">6.0</span><span class="sxs-lookup"><span data-stu-id="8256b-219">6.0</span></span> | <span data-ttu-id="8256b-220">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="8256b-220">2.6.32-71</span></span> |
| <span data-ttu-id="8256b-221">6.1</span><span class="sxs-lookup"><span data-stu-id="8256b-221">6.1</span></span> | <span data-ttu-id="8256b-222">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="8256b-222">2.6.32-131</span></span> |
| <span data-ttu-id="8256b-223">6.2</span><span class="sxs-lookup"><span data-stu-id="8256b-223">6.2</span></span> | <span data-ttu-id="8256b-224">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="8256b-224">2.6.32-220</span></span> |
| <span data-ttu-id="8256b-225">6.3</span><span class="sxs-lookup"><span data-stu-id="8256b-225">6.3</span></span> | <span data-ttu-id="8256b-226">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="8256b-226">2.6.32-279</span></span> |
| <span data-ttu-id="8256b-227">6.4</span><span class="sxs-lookup"><span data-stu-id="8256b-227">6.4</span></span> | <span data-ttu-id="8256b-228">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="8256b-228">2.6.32-358</span></span> |
| <span data-ttu-id="8256b-229">6.5</span><span class="sxs-lookup"><span data-stu-id="8256b-229">6.5</span></span> | <span data-ttu-id="8256b-230">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="8256b-230">2.6.32-431</span></span> |
| <span data-ttu-id="8256b-231">6.6</span><span class="sxs-lookup"><span data-stu-id="8256b-231">6.6</span></span> | <span data-ttu-id="8256b-232">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="8256b-232">2.6.32-504</span></span> |
| <span data-ttu-id="8256b-233">6.7</span><span class="sxs-lookup"><span data-stu-id="8256b-233">6.7</span></span> | <span data-ttu-id="8256b-234">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="8256b-234">2.6.32-573</span></span> |
| <span data-ttu-id="8256b-235">6.8</span><span class="sxs-lookup"><span data-stu-id="8256b-235">6.8</span></span> | <span data-ttu-id="8256b-236">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="8256b-236">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="8256b-237">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="8256b-237">Red Hat Linux 5</span></span>

| <span data-ttu-id="8256b-238">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-238">**OS version**</span></span> | <span data-ttu-id="8256b-239">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-239">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-240">5.8</span><span class="sxs-lookup"><span data-stu-id="8256b-240">5.8</span></span> | <span data-ttu-id="8256b-241">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="8256b-241">2.6.18-308</span></span> |
| <span data-ttu-id="8256b-242">5.9</span><span class="sxs-lookup"><span data-stu-id="8256b-242">5.9</span></span> | <span data-ttu-id="8256b-243">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="8256b-243">2.6.18-348</span></span> |
| <span data-ttu-id="8256b-244">5.10</span><span class="sxs-lookup"><span data-stu-id="8256b-244">5.10</span></span> | <span data-ttu-id="8256b-245">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="8256b-245">2.6.18-371</span></span> |
| <span data-ttu-id="8256b-246">5.11</span><span class="sxs-lookup"><span data-stu-id="8256b-246">5.11</span></span> | <span data-ttu-id="8256b-247">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="8256b-247">2.6.18-398</span></span> <br> <span data-ttu-id="8256b-248">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="8256b-248">2.6.18-400</span></span> <br><span data-ttu-id="8256b-249">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="8256b-249">2.6.18-402</span></span> <br><span data-ttu-id="8256b-250">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="8256b-250">2.6.18-404</span></span> <br><span data-ttu-id="8256b-251">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="8256b-251">2.6.18-406</span></span> <br> <span data-ttu-id="8256b-252">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="8256b-252">2.6.18-407</span></span> <br> <span data-ttu-id="8256b-253">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="8256b-253">2.6.18-408</span></span> <br> <span data-ttu-id="8256b-254">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="8256b-254">2.6.18-409</span></span> <br> <span data-ttu-id="8256b-255">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="8256b-255">2.6.18-410</span></span> <br> <span data-ttu-id="8256b-256">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="8256b-256">2.6.18-411</span></span> <br> <span data-ttu-id="8256b-257">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="8256b-257">2.6.18-412</span></span> <br> <span data-ttu-id="8256b-258">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="8256b-258">2.6.18-416</span></span> <br> <span data-ttu-id="8256b-259">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="8256b-259">2.6.18-417</span></span> <br> <span data-ttu-id="8256b-260">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="8256b-260">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="8256b-261">Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="8256b-261">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="8256b-262">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="8256b-262">Oracle Linux 6</span></span>

| <span data-ttu-id="8256b-263">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-263">**OS version**</span></span> | <span data-ttu-id="8256b-264">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-264">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-265">6.2</span><span class="sxs-lookup"><span data-stu-id="8256b-265">6.2</span></span> | <span data-ttu-id="8256b-266">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="8256b-266">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="8256b-267">6.3</span><span class="sxs-lookup"><span data-stu-id="8256b-267">6.3</span></span> | <span data-ttu-id="8256b-268">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8256b-268">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="8256b-269">6.4</span><span class="sxs-lookup"><span data-stu-id="8256b-269">6.4</span></span> | <span data-ttu-id="8256b-270">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8256b-270">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="8256b-271">6.5</span><span class="sxs-lookup"><span data-stu-id="8256b-271">6.5</span></span> | <span data-ttu-id="8256b-272">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="8256b-272">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="8256b-273">6.6</span><span class="sxs-lookup"><span data-stu-id="8256b-273">6.6</span></span> | <span data-ttu-id="8256b-274">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="8256b-274">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="8256b-275">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="8256b-275">Oracle Linux 5</span></span>

| <span data-ttu-id="8256b-276">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-276">**OS version**</span></span> | <span data-ttu-id="8256b-277">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-277">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-278">5.8</span><span class="sxs-lookup"><span data-stu-id="8256b-278">5.8</span></span> | <span data-ttu-id="8256b-279">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="8256b-279">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="8256b-280">5.9</span><span class="sxs-lookup"><span data-stu-id="8256b-280">5.9</span></span> | <span data-ttu-id="8256b-281">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8256b-281">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="8256b-282">5.10</span><span class="sxs-lookup"><span data-stu-id="8256b-282">5.10</span></span> | <span data-ttu-id="8256b-283">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8256b-283">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="8256b-284">5.11</span><span class="sxs-lookup"><span data-stu-id="8256b-284">5.11</span></span> | <span data-ttu-id="8256b-285">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="8256b-285">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="8256b-286">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="8256b-286">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="8256b-287">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="8256b-287">SUSE Linux 11</span></span>

| <span data-ttu-id="8256b-288">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-288">**OS version**</span></span> | <span data-ttu-id="8256b-289">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-289">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-290">11</span><span class="sxs-lookup"><span data-stu-id="8256b-290">11</span></span> | <span data-ttu-id="8256b-291">2.6.27</span><span class="sxs-lookup"><span data-stu-id="8256b-291">2.6.27</span></span> |
| <span data-ttu-id="8256b-292">11 SP1</span><span class="sxs-lookup"><span data-stu-id="8256b-292">11 SP1</span></span> | <span data-ttu-id="8256b-293">2.6.32</span><span class="sxs-lookup"><span data-stu-id="8256b-293">2.6.32</span></span> |
| <span data-ttu-id="8256b-294">11 SP2</span><span class="sxs-lookup"><span data-stu-id="8256b-294">11 SP2</span></span> | <span data-ttu-id="8256b-295">3.0.13</span><span class="sxs-lookup"><span data-stu-id="8256b-295">3.0.13</span></span> |
| <span data-ttu-id="8256b-296">11 SP3</span><span class="sxs-lookup"><span data-stu-id="8256b-296">11 SP3</span></span> | <span data-ttu-id="8256b-297">3.0.76</span><span class="sxs-lookup"><span data-stu-id="8256b-297">3.0.76</span></span> |
| <span data-ttu-id="8256b-298">11 SP4</span><span class="sxs-lookup"><span data-stu-id="8256b-298">11 SP4</span></span> | <span data-ttu-id="8256b-299">3.0.101</span><span class="sxs-lookup"><span data-stu-id="8256b-299">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="8256b-300">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="8256b-300">SUSE Linux 10</span></span>

| <span data-ttu-id="8256b-301">**作業系統版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-301">**OS version**</span></span> | <span data-ttu-id="8256b-302">**核心版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-302">**Kernel version**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-303">10 SP4</span><span class="sxs-lookup"><span data-stu-id="8256b-303">10 SP4</span></span> | <span data-ttu-id="8256b-304">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="8256b-304">2.6.16.60</span></span> |

#### <a name="dependency-agent-downloads"></a><span data-ttu-id="8256b-305">相依性代理程式下載</span><span class="sxs-lookup"><span data-stu-id="8256b-305">Dependency Agent downloads</span></span>

| <span data-ttu-id="8256b-306">**檔案**</span><span class="sxs-lookup"><span data-stu-id="8256b-306">**File**</span></span> | <span data-ttu-id="8256b-307">**作業系統**</span><span class="sxs-lookup"><span data-stu-id="8256b-307">**OS**</span></span> | <span data-ttu-id="8256b-308">**版本**</span><span class="sxs-lookup"><span data-stu-id="8256b-308">**Version**</span></span> | <span data-ttu-id="8256b-309">**SHA-256**</span><span class="sxs-lookup"><span data-stu-id="8256b-309">**SHA-256**</span></span> |
| --- | --- | --- | --- |
| [<span data-ttu-id="8256b-310">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="8256b-310">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="8256b-311">Windows</span><span class="sxs-lookup"><span data-stu-id="8256b-311">Windows</span></span> | <span data-ttu-id="8256b-312">9.0.5</span><span class="sxs-lookup"><span data-stu-id="8256b-312">9.0.5</span></span> | <span data-ttu-id="8256b-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="8256b-313">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="8256b-314">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="8256b-314">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="8256b-315">Linux</span><span class="sxs-lookup"><span data-stu-id="8256b-315">Linux</span></span> | <span data-ttu-id="8256b-316">9.0.5</span><span class="sxs-lookup"><span data-stu-id="8256b-316">9.0.5</span></span> | <span data-ttu-id="8256b-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="8256b-317">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |



## <a name="configuration"></a><span data-ttu-id="8256b-318">組態</span><span class="sxs-lookup"><span data-stu-id="8256b-318">Configuration</span></span>

<span data-ttu-id="8256b-319">執行下列步驟 tooconfigure hello 您工作區的網路資料解決方案的 hello。</span><span class="sxs-lookup"><span data-stu-id="8256b-319">Perform hello following steps tooconfigure hello Wire Data solution for your workspaces.</span></span>

1. <span data-ttu-id="8256b-320">啟用從 hello hello 活動記錄分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="8256b-320">Enable hello Activity Log Analytics solution from hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WireData2OMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="8256b-321">您要 tooget 資料所在的每一部電腦上安裝 hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-321">Install hello Dependency Agent on each computer where you want tooget data.</span></span> <span data-ttu-id="8256b-322">hello 相依性代理程式可以監視連線 tooimmediate 鄰近項目，因此您可能不需要在每一部電腦上的代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-322">hello Dependency Agent can monitor connections tooimmediate neighbors, so you might not need an agent on every computer.</span></span>

### <a name="install-hello-dependency-agent-on-windows"></a><span data-ttu-id="8256b-323">在 Windows 上安裝 hello 相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-323">Install hello Dependency Agent on Windows</span></span>

<span data-ttu-id="8256b-324">系統管理員權限需要的 tooinstall 或解除安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-324">Administrator privileges are required tooinstall or uninstall hello agent.</span></span>

<span data-ttu-id="8256b-325">hello 相依性代理程式會透過 InstallDependencyAgent Windows.exe 執行 Windows 的電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="8256b-325">hello Dependency Agent is installed on computers running Windows through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="8256b-326">如果您執行這個可執行檔不使用任何選項時，它會啟動精靈，您可以依照 tooinstall 以互動方式。</span><span class="sxs-lookup"><span data-stu-id="8256b-326">If you run this executable file without any options, it starts a wizard that you can follow tooinstall interactively.</span></span>

<span data-ttu-id="8256b-327">使用下列步驟 tooinstall hello 相依性代理程式在每一部執行 Windows 的電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="8256b-327">Use hello following steps tooinstall hello Dependency Agent on each computer running Windows:</span></span>

1. <span data-ttu-id="8256b-328">安裝 hello OMS 代理程式使用 hello 指示[連接 Windows Azure 中的記錄分析服務的電腦 toohello](log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="8256b-328">Install hello OMS Agent by using hello instructions at [Connect Windows computers toohello Log Analytics service in Azure](log-analytics-windows-agents.md).</span></span>
2. <span data-ttu-id="8256b-329">下載使用 hello 連結 hello 前一節中的 hello Windows 代理程式，然後使用下列命令的 hello 執行它： InstallDependencyAgent Windows.exe</span><span class="sxs-lookup"><span data-stu-id="8256b-329">Download hello Windows agent using hello link in hello previous section and then run it by using hello following command: InstallDependencyAgent-Windows.exe</span></span>
3. <span data-ttu-id="8256b-330">請遵循 hello 精靈 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-330">Follow hello wizard tooinstall hello agent.</span></span>
4. <span data-ttu-id="8256b-331">Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="8256b-331">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="8256b-332">Windows 代理程式上, hello 記錄檔目錄為 %Programfiles%\Microsoft 相依性 Agent\logs。</span><span class="sxs-lookup"><span data-stu-id="8256b-332">On Windows agents, hello log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span>

#### <a name="windows-command-line"></a><span data-ttu-id="8256b-333">Windows 命令列</span><span class="sxs-lookup"><span data-stu-id="8256b-333">Windows command line</span></span>

<span data-ttu-id="8256b-334">使用命令列中的下列資料表 tooinstall hello 的選項。</span><span class="sxs-lookup"><span data-stu-id="8256b-334">Use options from hello following table tooinstall from a command line.</span></span> <span data-ttu-id="8256b-335">toosee hello 安裝旗標，使用 hello 執行 hello 安裝程式的清單 /？</span><span class="sxs-lookup"><span data-stu-id="8256b-335">toosee a list of hello installation flags, run hello installer by using hello /?</span></span> <span data-ttu-id="8256b-336">如下所示。</span><span class="sxs-lookup"><span data-stu-id="8256b-336">flag as follows.</span></span>

<span data-ttu-id="8256b-337">InstallDependencyAgent-Windows.exe /?</span><span class="sxs-lookup"><span data-stu-id="8256b-337">InstallDependencyAgent-Windows.exe /?</span></span>

| <span data-ttu-id="8256b-338">**旗標**</span><span class="sxs-lookup"><span data-stu-id="8256b-338">**Flag**</span></span> | <span data-ttu-id="8256b-339">**說明**</span><span class="sxs-lookup"><span data-stu-id="8256b-339">**Description**</span></span> |
| --- | --- |
| <code>/?</code> | <span data-ttu-id="8256b-340">取得 hello 命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="8256b-340">Get a list of hello command-line options.</span></span> |
| <code>/S</code> | <span data-ttu-id="8256b-341">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="8256b-341">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="8256b-342">根據預設，hello Windows 相依性代理程式的檔案會放置於 C:\Program Files\Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-342">Files for hello Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-hello-dependency-agent-on-linux"></a><span data-ttu-id="8256b-343">Linux 上安裝 hello 相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-343">Install hello Dependency Agent on Linux</span></span>

<span data-ttu-id="8256b-344">將根目錄存取必要的 tooinstall 或 hello 代理程式設定。</span><span class="sxs-lookup"><span data-stu-id="8256b-344">Root access is required tooinstall or configure hello agent.</span></span>

<span data-ttu-id="8256b-345">hello 相依性代理程式會安裝在透過 InstallDependencyAgent Linux64.bin，與自我解壓縮二進位的殼層指令碼的 Linux 電腦上。</span><span class="sxs-lookup"><span data-stu-id="8256b-345">hello Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="8256b-346">您可以使用執行 hello 檔_sh_ ，或將執行權限 toohello 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="8256b-346">You can run hello file by using _sh_ or add execute permissions toohello file itself.</span></span>

<span data-ttu-id="8256b-347">使用下列步驟 tooinstall hello 相依性代理程式在每一部 Linux 電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="8256b-347">Use hello following steps tooinstall hello Dependency Agent on each Linux computer:</span></span>

1. <span data-ttu-id="8256b-348">安裝 hello OMS 代理程式使用 hello 指示[收集和管理資料從 Linux 電腦](log-analytics-agent-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="8256b-348">Install hello OMS Agent by using hello instructions at [Collect and manage data from Linux computers](log-analytics-agent-linux.md).</span></span>
2. <span data-ttu-id="8256b-349">下載使用 hello 連結 hello 前一節中的 hello Linux 相依性代理程式，然後將它安裝為根，使用下列命令的 hello: sh InstallDependencyAgent Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="8256b-349">Download hello Linux Dependency agent using hello link in hello previous section and then install it as root by using hello following command: sh InstallDependencyAgent-Linux64.bin</span></span>
3. <span data-ttu-id="8256b-350">Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="8256b-350">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="8256b-351">在 Linux 代理程式上, hello 記錄檔目錄是： /var/opt/microsoft/dependency-agent/log。</span><span class="sxs-lookup"><span data-stu-id="8256b-351">On Linux agents, hello log directory is: /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="8256b-352">toosee hello 安裝旗標，以 hello 執行 hello 安裝程式的清單`-help`旗標，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8256b-352">toosee a list of hello installation flags, run hello installation program with hello `-help` flag as follows.</span></span>

```
InstallDependencyAgent-Linux64.bin -help
```

| <span data-ttu-id="8256b-353">**旗標**</span><span class="sxs-lookup"><span data-stu-id="8256b-353">**Flag**</span></span> | <span data-ttu-id="8256b-354">**說明**</span><span class="sxs-lookup"><span data-stu-id="8256b-354">**Description**</span></span> |
| --- | --- |
| <code>-help</code> | <span data-ttu-id="8256b-355">取得 hello 命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="8256b-355">Get a list of hello command-line options.</span></span> |
| <code>-s</code> | <span data-ttu-id="8256b-356">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="8256b-356">Perform a silent installation with no user prompts.</span></span> |
| <code>--check</code> | <span data-ttu-id="8256b-357">檢查權限與 hello 作業系統，但不是安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-357">Check permissions and hello operating system but do not install hello agent.</span></span> |

<span data-ttu-id="8256b-358">Hello 相依性代理程式的檔案會放置於 hello 下列目錄：</span><span class="sxs-lookup"><span data-stu-id="8256b-358">Files for hello Dependency Agent are placed in hello following directories:</span></span>

| <span data-ttu-id="8256b-359">**檔案**</span><span class="sxs-lookup"><span data-stu-id="8256b-359">**Files**</span></span> | <span data-ttu-id="8256b-360">**位置**</span><span class="sxs-lookup"><span data-stu-id="8256b-360">**Location**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-361">核心檔案</span><span class="sxs-lookup"><span data-stu-id="8256b-361">Core files</span></span> | <span data-ttu-id="8256b-362">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="8256b-362">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="8256b-363">記錄檔</span><span class="sxs-lookup"><span data-stu-id="8256b-363">Log files</span></span> | <span data-ttu-id="8256b-364">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="8256b-364">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="8256b-365">組態檔</span><span class="sxs-lookup"><span data-stu-id="8256b-365">Config files</span></span> | <span data-ttu-id="8256b-366">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="8256b-366">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="8256b-367">服務可執行檔</span><span class="sxs-lookup"><span data-stu-id="8256b-367">Service executable files</span></span> | <span data-ttu-id="8256b-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="8256b-368">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><br><span data-ttu-id="8256b-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="8256b-369">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="8256b-370">二進位儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="8256b-370">Binary storage files</span></span> | <span data-ttu-id="8256b-371">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="8256b-371">/var/opt/microsoft/dependency-agent/storage</span></span> |

### <a name="installation-script-examples"></a><span data-ttu-id="8256b-372">安裝指令碼範例</span><span class="sxs-lookup"><span data-stu-id="8256b-372">Installation script examples</span></span>

<span data-ttu-id="8256b-373">tooeasily 部署 hello 相依性代理程式在許多伺服器上的一次，它可協助 toouse 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8256b-373">tooeasily deploy hello Dependency Agent on many servers at once, it helps toouse a script.</span></span> <span data-ttu-id="8256b-374">您可以使用下列指令碼範例 toodownload hello 和 hello 相依性代理程式安裝在 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="8256b-374">You can use hello following script examples toodownload and install hello Dependency Agent on either Windows or Linux.</span></span>

#### <a name="powershell-script-for-windows"></a><span data-ttu-id="8256b-375">適用於 Windows 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="8256b-375">PowerShell script for Windows</span></span>

```PowerShell

Invoke-WebRequest &quot;https://aka.ms/dependencyagentwindows&quot; -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S

```

#### <a name="shell-script-for-linux"></a><span data-ttu-id="8256b-376">適用於 Linux 的殼層指令碼</span><span class="sxs-lookup"><span data-stu-id="8256b-376">Shell script for Linux</span></span>

```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
```

```
sh InstallDependencyAgent-Linux64.bin -s
```

### <a name="desired-state-configuration"></a><span data-ttu-id="8256b-377">期望的狀態設定</span><span class="sxs-lookup"><span data-stu-id="8256b-377">Desired State Configuration</span></span>

<span data-ttu-id="8256b-378">toodeploy hello 相依性代理程式透過預期狀態設定，您可以使用 hello xPSDesiredStateConfiguration 模組和有點類似 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8256b-378">toodeploy hello Dependency Agent via Desired State Configuration, you can use hello xPSDesiredStateConfiguration module and a bit of code like hello following:</span></span>

```
Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = &quot;C:\InstallDependencyAgent-Windows.exe&quot;



Node $NodeName

{

    # Download and install hello Dependency Agent

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
### <a name="uninstall-hello-dependency-agent"></a><span data-ttu-id="8256b-379">解除安裝 hello 相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-379">Uninstall hello Dependency Agent</span></span>

<span data-ttu-id="8256b-380">使用下列各節 toohelp 移除 hello 相依性代理程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="8256b-380">Use hello following sections toohelp you remove hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-windows"></a><span data-ttu-id="8256b-381">解除安裝相依性代理程式在 Windows hello</span><span class="sxs-lookup"><span data-stu-id="8256b-381">Uninstall hello Dependency Agent on Windows</span></span>

<span data-ttu-id="8256b-382">系統管理員可以解除安裝 hello 相依性代理程式的 Windows 控制台。</span><span class="sxs-lookup"><span data-stu-id="8256b-382">An administrator can uninstall hello Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="8256b-383">系統管理員也可以執行 %Programfiles%\Microsoft 相依性 Agent\Uninstall.exe toouninstall hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="8256b-383">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe toouninstall hello Dependency Agent.</span></span>

#### <a name="uninstall-hello-dependency-agent-on-linux"></a><span data-ttu-id="8256b-384">解除安裝 hello Linux 上的相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="8256b-384">Uninstall hello Dependency Agent on Linux</span></span>

<span data-ttu-id="8256b-385">toocompletely 解除安裝 hello 相依性代理程式從 Linux，您必須移除 hello 代理程式本身並 hello hello 代理程式會自動安裝的連接器。</span><span class="sxs-lookup"><span data-stu-id="8256b-385">toocompletely uninstall hello Dependency Agent from Linux, you must remove hello agent itself and hello connector, which is installed automatically with hello agent.</span></span> <span data-ttu-id="8256b-386">您可以使用下列單一命令的 hello 同時解除安裝：</span><span class="sxs-lookup"><span data-stu-id="8256b-386">You can uninstall both by using hello following single command:</span></span>

```
rpm -e dependency-agent dependency-agent-connector
```

## <a name="management-packs"></a><span data-ttu-id="8256b-387">管理組件</span><span class="sxs-lookup"><span data-stu-id="8256b-387">Management packs</span></span>

<span data-ttu-id="8256b-388">啟動網路資料時，記錄分析工作區中，300 KB 管理組件會傳送 tooall hello Windows 伺服器，該工作區中。</span><span class="sxs-lookup"><span data-stu-id="8256b-388">When Wire Data is activated in a Log Analytics workspace, a 300-KB management pack is sent tooall hello Windows servers in that workspace.</span></span> <span data-ttu-id="8256b-389">如果您使用 System Center Operations Manager 代理程式在[連線的管理群組](log-analytics-om-agents.md)，hello 相依性監視管理組件從 System Center Operations Manager 部署。</span><span class="sxs-lookup"><span data-stu-id="8256b-389">If you are using System Center Operations Manager agents in a [connected management group](log-analytics-om-agents.md), hello Dependency Monitor management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="8256b-390">如果 hello 代理程式並直接連接，記錄分析會傳遞 hello 管理組件。</span><span class="sxs-lookup"><span data-stu-id="8256b-390">If hello agents are directly connected, Log Analytics delivers hello management pack.</span></span>

<span data-ttu-id="8256b-391">hello 管理組件是名為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。</span><span class="sxs-lookup"><span data-stu-id="8256b-391">hello management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="8256b-392">它會寫入至 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs。</span><span class="sxs-lookup"><span data-stu-id="8256b-392">It's written to: %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span></span> <span data-ttu-id="8256b-393">hello hello 管理組件使用的資料來源是: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。</span><span class="sxs-lookup"><span data-stu-id="8256b-393">hello data source that hello management pack uses is: %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources&lt;AutoGeneratedID&gt;\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="using-hello-solution"></a><span data-ttu-id="8256b-394">使用 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="8256b-394">Using hello solution</span></span>

<span data-ttu-id="8256b-395">**安裝和設定 hello 方案**</span><span class="sxs-lookup"><span data-stu-id="8256b-395">**Installing and configuring hello solution**</span></span>

<span data-ttu-id="8256b-396">使用下列資訊 tooinstall hello 並設定 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="8256b-396">Use hello following information tooinstall and configure hello solution.</span></span>

- <span data-ttu-id="8256b-397">hello 網路資料解決方案擷取資料，從執行 Windows Server 2012 R2、 Windows 8.1 和更新版本的作業系統的電腦。</span><span class="sxs-lookup"><span data-stu-id="8256b-397">hello Wire Data solution acquires data from computers running Windows Server 2012 R2, Windows 8.1, and later operating systems.</span></span>
- <span data-ttu-id="8256b-398">您想要從 tooacquire 網路資料的電腦上需要 Microsoft.NET Framework 4.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8256b-398">Microsoft .NET Framework 4.0 or later is required on computers where you want tooacquire wire data from.</span></span>
- <span data-ttu-id="8256b-399">新增 hello 網路資料解決方案 tooyour 記錄分析工作區中使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="8256b-399">Add hello Wire Data solution tooyour Log Analytics workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="8256b-400">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="8256b-400">There is no further configuration required.</span></span>
- <span data-ttu-id="8256b-401">如果您想要特定解決方案 tooview 網路資料，您需要已加入的 toohave hello 解決方案 tooyour 工作區。</span><span class="sxs-lookup"><span data-stu-id="8256b-401">If you want tooview wire data for a specific solution, you need toohave hello solution already added tooyour workspace.</span></span>

<span data-ttu-id="8256b-402">已安裝的代理程式並安裝 hello 方案之後，hello 網路資料 2.0 磚會出現在您的工作區中。</span><span class="sxs-lookup"><span data-stu-id="8256b-402">After you have agents installed and you install hello solution, hello Wire Data 2.0 tile appears in your workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="8256b-403">目前，您必須使用 hello OMS 入口網站 tooview 網路資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-403">Currently, you must use hello OMS portal tooview wire data.</span></span> <span data-ttu-id="8256b-404">您無法使用 hello Azure 入口網站 tooview 網路資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-404">You cannot use hello Azure portal tooview wire data.</span></span>

![Wire Data 磚](./media/log-analytics-wire-data/wire-data-tile.png)

## <a name="using-hello-wire-data-20-solution"></a><span data-ttu-id="8256b-406">使用網路資料 2.0 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="8256b-406">Using hello Wire Data 2.0 solution</span></span>

<span data-ttu-id="8256b-407">在 hello OMS 入口網站中，按一下 hello**網路資料 2.0**磚 tooopen hello 網路資料儀表板。</span><span class="sxs-lookup"><span data-stu-id="8256b-407">In hello OMS portal, click hello **Wire Data 2.0** tile tooopen hello Wire Data dashboard.</span></span> <span data-ttu-id="8256b-408">hello 儀表板會納入 hello 下表中的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8256b-408">hello dashboard includes hello blades in hello following table.</span></span> <span data-ttu-id="8256b-409">每個刀鋒視窗會列出 too10 hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。</span><span class="sxs-lookup"><span data-stu-id="8256b-409">Each blade lists up too10 items matching that blade's criteria for hello specified scope and time range.</span></span> <span data-ttu-id="8256b-410">您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello 的 hello 刀鋒視窗，或按一下 hello 刀鋒視窗中的標頭。</span><span class="sxs-lookup"><span data-stu-id="8256b-410">You can run a log search that returns all records by clicking **See all** at hello bottom of hello blade or by clicking hello blade header.</span></span>

| <span data-ttu-id="8256b-411">**刀鋒視窗**</span><span class="sxs-lookup"><span data-stu-id="8256b-411">**Blade**</span></span> | <span data-ttu-id="8256b-412">**說明**</span><span class="sxs-lookup"><span data-stu-id="8256b-412">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8256b-413">擷取網路流量的代理程式數</span><span class="sxs-lookup"><span data-stu-id="8256b-413">Agents capturing network traffic</span></span> | <span data-ttu-id="8256b-414">顯示 hello 會擷取網路流量的代理程式數目，並列出 hello top 10 的電腦所擷取的流量。</span><span class="sxs-lookup"><span data-stu-id="8256b-414">Shows hello number of agents that are capturing network traffic and lists hello top 10 computers that are capturing traffic.</span></span> <span data-ttu-id="8256b-415">按一下 記錄搜尋 hello 數字 toorun <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>。</span><span class="sxs-lookup"><span data-stu-id="8256b-415">Click hello number toorun a log search for <code>Type:WireData &#124; measure Sum(TotalBytes) by Computer &#124; top 500000</code>.</span></span> <span data-ttu-id="8256b-416">按一下電腦，在 hello 清單 toorun 傳回 hello 的總位元組數所擷取的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="8256b-416">Click a computer in hello list toorun a log search returning hello total number of bytes captured.</span></span> |
| <span data-ttu-id="8256b-417">區域子網路數</span><span class="sxs-lookup"><span data-stu-id="8256b-417">Local Subnets</span></span> | <span data-ttu-id="8256b-418">顯示 hello 本機子網路探索代理程式數目。</span><span class="sxs-lookup"><span data-stu-id="8256b-418">Shows hello number of local subnets that agents have discovered.</span></span>  <span data-ttu-id="8256b-419">按一下 記錄搜尋 hello 數字 toorun<code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code>其中列出所有子網路與 hello 透過每個傳送的位元組數目。</span><span class="sxs-lookup"><span data-stu-id="8256b-419">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by LocalSubnet</code> that lists all subnets with hello number of bytes sent over each one.</span></span> <span data-ttu-id="8256b-420">按一下 子網路中 hello 清單 toorun 傳回 hello 的總位元組數 hello 子網路上傳送的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="8256b-420">Click a subnet in hello list toorun a log search returning hello total number of bytes sent over hello subnet.</span></span> |
| <span data-ttu-id="8256b-421">應用程式層級通訊協定數</span><span class="sxs-lookup"><span data-stu-id="8256b-421">Application-level Protocols</span></span> | <span data-ttu-id="8256b-422">探索到代理程式，請在使用中，顯示 hello 一些應用程式層級通訊協定。</span><span class="sxs-lookup"><span data-stu-id="8256b-422">Shows hello number of application-level protocols in use, as discovered by agents.</span></span> <span data-ttu-id="8256b-423">按一下 記錄搜尋 hello 數字 toorun <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>。</span><span class="sxs-lookup"><span data-stu-id="8256b-423">Click hello number toorun a log search for <code>Type:WireData &#124; Measure Sum(TotalBytes) by ApplicationProtocol</code>.</span></span> <span data-ttu-id="8256b-424">按一下 通訊協定 toorun 傳回 hello 的總位元組數傳送嗨通訊協定的使用記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="8256b-424">Click a protocol toorun a log search returning hello total number of bytes sent using hello protocol.</span></span> |

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Wire Data 儀表板](./media/log-analytics-wire-data/wire-data-dash.png)

<span data-ttu-id="8256b-426">您可以使用 hello**擷取網路流量的代理程式**刀鋒視窗 toodetermine 電腦使用多少網路頻寬。</span><span class="sxs-lookup"><span data-stu-id="8256b-426">You can use hello **Agents capturing network traffic** blade toodetermine how much network bandwidth is being consumed by computers.</span></span> <span data-ttu-id="8256b-427">此刀鋒視窗可協助您輕鬆地尋找 hello _chattiest_您環境中的電腦。</span><span class="sxs-lookup"><span data-stu-id="8256b-427">This blade can help you easily find hello _chattiest_ computer in your environment.</span></span> <span data-ttu-id="8256b-428">這類電腦可能超載、運作異常，或使用的網路資源不尋常地過多。</span><span class="sxs-lookup"><span data-stu-id="8256b-428">Such computers could be overloaded, acting abnormally, or using more network resources than normal.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example01.png)

<span data-ttu-id="8256b-430">同樣地，您可以使用 hello**本機子網路**刀鋒視窗 toodetermine 網路流量移動您的子網路。</span><span class="sxs-lookup"><span data-stu-id="8256b-430">Similarly, you can use hello **Local Subnets** blade toodetermine how much network traffic is moving through your subnets.</span></span> <span data-ttu-id="8256b-431">使用者通常會為其應用程式定義重要區域周圍的子網路。</span><span class="sxs-lookup"><span data-stu-id="8256b-431">Users often define subnets around critical areas for their applications.</span></span> <span data-ttu-id="8256b-432">此刀鋒視窗會提供這些區域的檢視。</span><span class="sxs-lookup"><span data-stu-id="8256b-432">This blade offers a view into those areas.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example02.png)

<span data-ttu-id="8256b-434">hello**應用程式層級通訊協定**刀鋒視窗中很有用，所以很有幫助知道通訊協定正在使用中。</span><span class="sxs-lookup"><span data-stu-id="8256b-434">hello **Application-level Protocols** blade is useful because it's helpful know what protocols are in use.</span></span> <span data-ttu-id="8256b-435">例如，您可能預期 SSH toonot 在您的網路環境中使用。</span><span class="sxs-lookup"><span data-stu-id="8256b-435">For example, you might expect SSH toonot be in use in your network environment.</span></span> <span data-ttu-id="8256b-436">檢視可用在 hello 刀鋒視窗中的資訊可以快速地確認，或 disprove 您預期的情況。</span><span class="sxs-lookup"><span data-stu-id="8256b-436">Viewing information available in hello blade can quickly confirm or disprove your expectation.</span></span>

![記錄搜尋範例](./media/log-analytics-wire-data/log-search-example03.png)

<span data-ttu-id="8256b-438">在此範例中，您可以向下切入到 SSH 詳細資料 toosee 哪些電腦使用 SSH 和許多其他的通訊詳細資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-438">In this example, you could drill-into SSH details toosee which computers are using SSH and many other communication details.</span></span>

![sh 搜尋結果](./media/log-analytics-wire-data/ssh-details.png)

<span data-ttu-id="8256b-440">它也是很有用的 tooknow 如果通訊協定流量會增加或減少一段時間。</span><span class="sxs-lookup"><span data-stu-id="8256b-440">It's also useful tooknow if protocol traffic is increasing or decreasing over time.</span></span> <span data-ttu-id="8256b-441">比方說，如果資料是應用程式所傳送的 hello 數量增加，這可能是一些您應該注意，或者，您可能會發現值得注意。</span><span class="sxs-lookup"><span data-stu-id="8256b-441">For example, if hello amount of data being transmitted by an application is increasing, that might be something you should be aware of, or that you might find noteworthy.</span></span>

## <a name="input-data"></a><span data-ttu-id="8256b-442">輸入資料</span><span class="sxs-lookup"><span data-stu-id="8256b-442">Input data</span></span>

<span data-ttu-id="8256b-443">網路資料會收集網路流量使用您已啟用的 hello 代理程式的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-443">Wire data collects metadata about network traffic using hello agents that you have enabled.</span></span> <span data-ttu-id="8256b-444">每個代理程式約每隔 15 秒傳送一次資料。</span><span class="sxs-lookup"><span data-stu-id="8256b-444">Each agent sends data about every 15 seconds.</span></span>

## <a name="output-data"></a><span data-ttu-id="8256b-445">輸出資料</span><span class="sxs-lookup"><span data-stu-id="8256b-445">Output data</span></span>

<span data-ttu-id="8256b-446">對於每種類型的輸入資料，系統會建立 _WireData_ 類型的記錄。</span><span class="sxs-lookup"><span data-stu-id="8256b-446">A record with a type of _WireData_ is created for each type of input data.</span></span> <span data-ttu-id="8256b-447">WireData 記錄都有屬性 hello 下表所示：</span><span class="sxs-lookup"><span data-stu-id="8256b-447">WireData records have properties shown in hello following table:</span></span>

| <span data-ttu-id="8256b-448">屬性</span><span class="sxs-lookup"><span data-stu-id="8256b-448">Property</span></span> | <span data-ttu-id="8256b-449">說明</span><span class="sxs-lookup"><span data-stu-id="8256b-449">Description</span></span> |
|---|---|
| <span data-ttu-id="8256b-450">電腦</span><span class="sxs-lookup"><span data-stu-id="8256b-450">Computer</span></span> | <span data-ttu-id="8256b-451">收集資料所在的電腦名稱</span><span class="sxs-lookup"><span data-stu-id="8256b-451">Computer name where data was collected</span></span> |
| <span data-ttu-id="8256b-452">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="8256b-452">TimeGenerated</span></span> | <span data-ttu-id="8256b-453">Hello 記錄的時間</span><span class="sxs-lookup"><span data-stu-id="8256b-453">Time of hello record</span></span> |
| <span data-ttu-id="8256b-454">LocalIP</span><span class="sxs-lookup"><span data-stu-id="8256b-454">LocalIP</span></span> | <span data-ttu-id="8256b-455">Hello 本機電腦的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8256b-455">IP address of hello local computer</span></span> |
| <span data-ttu-id="8256b-456">SessionState</span><span class="sxs-lookup"><span data-stu-id="8256b-456">SessionState</span></span> | <span data-ttu-id="8256b-457">已連線或已中斷連線</span><span class="sxs-lookup"><span data-stu-id="8256b-457">Connected or disconnected</span></span> |
| <span data-ttu-id="8256b-458">ReceivedBytes</span><span class="sxs-lookup"><span data-stu-id="8256b-458">ReceivedBytes</span></span> | <span data-ttu-id="8256b-459">接收的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8256b-459">Amount of bytes received</span></span> |
| <span data-ttu-id="8256b-460">ProtocolName</span><span class="sxs-lookup"><span data-stu-id="8256b-460">ProtocolName</span></span> | <span data-ttu-id="8256b-461">使用 hello 網路通訊協定名稱</span><span class="sxs-lookup"><span data-stu-id="8256b-461">Name of hello network protocol used</span></span> |
| <span data-ttu-id="8256b-462">IPVersion</span><span class="sxs-lookup"><span data-stu-id="8256b-462">IPVersion</span></span> | <span data-ttu-id="8256b-463">IP 版本</span><span class="sxs-lookup"><span data-stu-id="8256b-463">IP version</span></span> |
| <span data-ttu-id="8256b-464">方向</span><span class="sxs-lookup"><span data-stu-id="8256b-464">Direction</span></span> | <span data-ttu-id="8256b-465">輸入或輸出</span><span class="sxs-lookup"><span data-stu-id="8256b-465">Inbound or outbound</span></span> |
| <span data-ttu-id="8256b-466">MaliciousIP</span><span class="sxs-lookup"><span data-stu-id="8256b-466">MaliciousIP</span></span> | <span data-ttu-id="8256b-467">已知惡意來源的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8256b-467">IP address of a known malicious source</span></span> |
| <span data-ttu-id="8256b-468">嚴重性</span><span class="sxs-lookup"><span data-stu-id="8256b-468">Severity</span></span> | <span data-ttu-id="8256b-469">可疑惡意程式碼嚴重性</span><span class="sxs-lookup"><span data-stu-id="8256b-469">Suspected malware severity</span></span> |
| <span data-ttu-id="8256b-470">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="8256b-470">RemoteIPCountry</span></span> | <span data-ttu-id="8256b-471">國家/地區的 hello 遠端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8256b-471">Country of hello remote IP address</span></span> |
| <span data-ttu-id="8256b-472">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="8256b-472">ManagementGroupName</span></span> | <span data-ttu-id="8256b-473">Hello Operations Manager 管理群組的名稱</span><span class="sxs-lookup"><span data-stu-id="8256b-473">Name of hello Operations Manager management group</span></span> |
| <span data-ttu-id="8256b-474">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="8256b-474">SourceSystem</span></span> | <span data-ttu-id="8256b-475">收集資料所在的來源</span><span class="sxs-lookup"><span data-stu-id="8256b-475">Source where data was collected</span></span> |
| <span data-ttu-id="8256b-476">SessionStartTime</span><span class="sxs-lookup"><span data-stu-id="8256b-476">SessionStartTime</span></span> | <span data-ttu-id="8256b-477">工作階段的開始時間</span><span class="sxs-lookup"><span data-stu-id="8256b-477">Start time of session</span></span> |
| <span data-ttu-id="8256b-478">SessionEndTime</span><span class="sxs-lookup"><span data-stu-id="8256b-478">SessionEndTime</span></span> | <span data-ttu-id="8256b-479">工作階段的結束時間</span><span class="sxs-lookup"><span data-stu-id="8256b-479">End time of session</span></span> |
| <span data-ttu-id="8256b-480">LocalSubnet</span><span class="sxs-lookup"><span data-stu-id="8256b-480">LocalSubnet</span></span> | <span data-ttu-id="8256b-481">收集資料所在的子網路</span><span class="sxs-lookup"><span data-stu-id="8256b-481">Subnet where data was collected</span></span> |
| <span data-ttu-id="8256b-482">LocalPortNumber</span><span class="sxs-lookup"><span data-stu-id="8256b-482">LocalPortNumber</span></span> | <span data-ttu-id="8256b-483">本機連接埠號碼</span><span class="sxs-lookup"><span data-stu-id="8256b-483">Local port number</span></span> |
| <span data-ttu-id="8256b-484">RemoteIP</span><span class="sxs-lookup"><span data-stu-id="8256b-484">RemoteIP</span></span> | <span data-ttu-id="8256b-485">使用 hello 遠端電腦的遠端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="8256b-485">Remote IP address used by hello remote computer</span></span> |
| <span data-ttu-id="8256b-486">RemotePortNumber</span><span class="sxs-lookup"><span data-stu-id="8256b-486">RemotePortNumber</span></span> | <span data-ttu-id="8256b-487">Hello 遠端 IP 位址所使用的通訊埠編號</span><span class="sxs-lookup"><span data-stu-id="8256b-487">Port number used by hello remote IP address</span></span> |
| <span data-ttu-id="8256b-488">SessionID</span><span class="sxs-lookup"><span data-stu-id="8256b-488">SessionID</span></span> | <span data-ttu-id="8256b-489">識別兩個 IP 位址之間通訊工作階段的唯一值</span><span class="sxs-lookup"><span data-stu-id="8256b-489">A unique value that identifies communication session between two IP addresses</span></span> |
| <span data-ttu-id="8256b-490">SentBytes</span><span class="sxs-lookup"><span data-stu-id="8256b-490">SentBytes</span></span> | <span data-ttu-id="8256b-491">傳送的位元組數目</span><span class="sxs-lookup"><span data-stu-id="8256b-491">Number of bytes sent</span></span> |
| <span data-ttu-id="8256b-492">TotalBytes</span><span class="sxs-lookup"><span data-stu-id="8256b-492">TotalBytes</span></span> | <span data-ttu-id="8256b-493">工作階段期間傳送的位元組總數</span><span class="sxs-lookup"><span data-stu-id="8256b-493">Total number of bytes sent during session</span></span> |
| <span data-ttu-id="8256b-494">ApplicationProtocol</span><span class="sxs-lookup"><span data-stu-id="8256b-494">ApplicationProtocol</span></span> | <span data-ttu-id="8256b-495">使用的網路通訊協定類型</span><span class="sxs-lookup"><span data-stu-id="8256b-495">Type of network protocol used</span></span>   |
| <span data-ttu-id="8256b-496">ProcessID</span><span class="sxs-lookup"><span data-stu-id="8256b-496">ProcessID</span></span> | <span data-ttu-id="8256b-497">Windows 處理序識別碼</span><span class="sxs-lookup"><span data-stu-id="8256b-497">Windows process ID</span></span> |
| <span data-ttu-id="8256b-498">ProcessName</span><span class="sxs-lookup"><span data-stu-id="8256b-498">ProcessName</span></span> | <span data-ttu-id="8256b-499">Hello 處理程序路徑和檔案名稱</span><span class="sxs-lookup"><span data-stu-id="8256b-499">Path and file name of hello process</span></span> |
| <span data-ttu-id="8256b-500">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="8256b-500">RemoteIPLongitude</span></span> | <span data-ttu-id="8256b-501">IP 經度值</span><span class="sxs-lookup"><span data-stu-id="8256b-501">IP longitude value</span></span> |
| <span data-ttu-id="8256b-502">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="8256b-502">RemoteIPLatitude</span></span> | <span data-ttu-id="8256b-503">IP 緯度值</span><span class="sxs-lookup"><span data-stu-id="8256b-503">IP latitude value</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8256b-504">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8256b-504">Next steps</span></span>

- <span data-ttu-id="8256b-505">[搜尋記錄](log-analytics-log-searches.md)tooview 詳細的網路資料搜尋記錄。</span><span class="sxs-lookup"><span data-stu-id="8256b-505">[Search logs](log-analytics-log-searches.md) tooview detailed wire data search records.</span></span>
