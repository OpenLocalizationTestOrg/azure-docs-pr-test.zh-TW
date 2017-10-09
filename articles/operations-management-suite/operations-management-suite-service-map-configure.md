---
title: "aaaConfigure Operations Management Suite 中的服務對應 |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: d3d66b45-9874-4aad-9c00-124734944b2e
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/18/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: 3127f4440f2886370f8ff617c405c6d70a926eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a><span data-ttu-id="beb09-104">設定 Operations Management Suite 中的服務對應</span><span class="sxs-lookup"><span data-stu-id="beb09-104">Configure Service Map in Operations Management Suite</span></span>
<span data-ttu-id="beb09-105">服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-105">Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="beb09-106">您可以使用您的伺服器，做為您將它們-提供重要服務的互連系統 tooview。</span><span class="sxs-lookup"><span data-stu-id="beb09-106">You can use it tooview your servers as you think of them--as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="beb09-107">不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連線架構的伺服器、處理序和連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="beb09-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required, other than installation of an agent.</span></span>

<span data-ttu-id="beb09-108">本文說明 hello 的服務對應和入門訓練的代理程式設定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-108">This article describes hello details of configuring Service Map and onboarding agents.</span></span> <span data-ttu-id="beb09-109">如需使用服務對應的資訊，請參閱[使用 Operations Management Suite 中的 hello 服務對應解決方案](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="beb09-109">For information on using Service Map, see [Use hello Service Map solution in Operations Management Suite](operations-management-suite-service-map.md).</span></span>

## <a name="dependency-agent-downloads"></a><span data-ttu-id="beb09-110">相依性代理程式下載</span><span class="sxs-lookup"><span data-stu-id="beb09-110">Dependency Agent downloads</span></span>
| <span data-ttu-id="beb09-111">檔案</span><span class="sxs-lookup"><span data-stu-id="beb09-111">File</span></span> | <span data-ttu-id="beb09-112">作業系統</span><span class="sxs-lookup"><span data-stu-id="beb09-112">OS</span></span> | <span data-ttu-id="beb09-113">版本</span><span class="sxs-lookup"><span data-stu-id="beb09-113">Version</span></span> | <span data-ttu-id="beb09-114">SHA-256</span><span class="sxs-lookup"><span data-stu-id="beb09-114">SHA-256</span></span> |
|:--|:--|:--|:--|
| [<span data-ttu-id="beb09-115">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="beb09-115">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="beb09-116">Windows</span><span class="sxs-lookup"><span data-stu-id="beb09-116">Windows</span></span> | <span data-ttu-id="beb09-117">9.0.5</span><span class="sxs-lookup"><span data-stu-id="beb09-117">9.0.5</span></span> | <span data-ttu-id="beb09-118">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="beb09-118">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="beb09-119">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="beb09-119">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="beb09-120">Linux</span><span class="sxs-lookup"><span data-stu-id="beb09-120">Linux</span></span> | <span data-ttu-id="beb09-121">9.0.5</span><span class="sxs-lookup"><span data-stu-id="beb09-121">9.0.5</span></span> | <span data-ttu-id="beb09-122">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="beb09-122">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |


## <a name="connected-sources"></a><span data-ttu-id="beb09-123">連接的來源</span><span class="sxs-lookup"><span data-stu-id="beb09-123">Connected sources</span></span>
<span data-ttu-id="beb09-124">服務對應由 hello Microsoft 相依性代理程式取得資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-124">Service Map gets its data from hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="beb09-125">hello 相依性代理程式，取決於其連線 tooOperations Management Suite 的 hello OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-125">hello Dependency Agent depends on hello OMS Agent for its connections tooOperations Management Suite.</span></span> <span data-ttu-id="beb09-126">這表示伺服器必須擁有的 hello OMS 代理程式安裝和設定，然後再 hello 可以安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-126">This means that a server must have hello OMS Agent installed and configured first, and then hello Dependency Agent can be installed.</span></span> <span data-ttu-id="beb09-127">hello 下表描述 hello 服務對應解決方案支援的 hello 連接來源。</span><span class="sxs-lookup"><span data-stu-id="beb09-127">hello following table describes hello connected sources that hello Service Map solution supports.</span></span>

| <span data-ttu-id="beb09-128">連線的來源</span><span class="sxs-lookup"><span data-stu-id="beb09-128">Connected source</span></span> | <span data-ttu-id="beb09-129">支援</span><span class="sxs-lookup"><span data-stu-id="beb09-129">Supported</span></span> | <span data-ttu-id="beb09-130">說明</span><span class="sxs-lookup"><span data-stu-id="beb09-130">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="beb09-131">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="beb09-131">Windows agents</span></span> | <span data-ttu-id="beb09-132">是</span><span class="sxs-lookup"><span data-stu-id="beb09-132">Yes</span></span> | <span data-ttu-id="beb09-133">服務對應會分析並收集來自 Windows 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-133">Service Map analyzes and collects data from Windows agent computers.</span></span> <br><br><span data-ttu-id="beb09-134">在加法 toohello [OMS Agent](../log-analytics/log-analytics-windows-agents.md)，Windows 代理程式需要 hello Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-134">In addition toohello [OMS Agent](../log-analytics/log-analytics-windows-agents.md), Windows agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="beb09-135">請參閱 hello[支援的作業系統](#supported-operating-systems)如需完整的作業系統版本清單。</span><span class="sxs-lookup"><span data-stu-id="beb09-135">See hello [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="beb09-136">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="beb09-136">Linux agents</span></span> | <span data-ttu-id="beb09-137">是</span><span class="sxs-lookup"><span data-stu-id="beb09-137">Yes</span></span> | <span data-ttu-id="beb09-138">服務對應會分析並收集來自 Linux 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-138">Service Map analyzes and collects data from Linux agent computers.</span></span> <br><br><span data-ttu-id="beb09-139">在加法 toohello [OMS Agent](../log-analytics/log-analytics-linux-agents.md)，Linux 代理程式需要 hello Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-139">In addition toohello [OMS Agent](../log-analytics/log-analytics-linux-agents.md), Linux agents require hello Microsoft Dependency Agent.</span></span> <span data-ttu-id="beb09-140">請參閱 hello[支援的作業系統](#supported-operating-systems)如需完整的作業系統版本清單。</span><span class="sxs-lookup"><span data-stu-id="beb09-140">See hello [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="beb09-141">System Center Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="beb09-141">System Center Operations Manager management group</span></span> | <span data-ttu-id="beb09-142">是</span><span class="sxs-lookup"><span data-stu-id="beb09-142">Yes</span></span> | <span data-ttu-id="beb09-143">服務對應會在連線的 [System Center Operations Manager 管理群組](../log-analytics/log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-143">Service Map analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](../log-analytics/log-analytics-om-agents.md).</span></span> <br><br><span data-ttu-id="beb09-144">直接從 hello System Center Operations Manager 代理程式電腦 tooOperations Management Suite 的資訊需要連接。</span><span class="sxs-lookup"><span data-stu-id="beb09-144">A direct connection from hello System Center Operations Manager agent computer tooOperations Management Suite is required.</span></span> <span data-ttu-id="beb09-145">從 hello 管理群組 toohello Operations Management Suite 儲存機制，就會轉送資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-145">Data is forwarded from hello management group toohello Operations Management Suite repository.</span></span>|
| <span data-ttu-id="beb09-146">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="beb09-146">Azure storage account</span></span> | <span data-ttu-id="beb09-147">否</span><span class="sxs-lookup"><span data-stu-id="beb09-147">No</span></span> | <span data-ttu-id="beb09-148">服務對應收集資料從代理程式的電腦，所以沒有從其資料從 Azure 儲存體 toocollect。</span><span class="sxs-lookup"><span data-stu-id="beb09-148">Service Map collects data from agent computers, so there is no data from it toocollect from Azure Storage.</span></span> |

<span data-ttu-id="beb09-149">服務對應僅支援 64 位元平台。</span><span class="sxs-lookup"><span data-stu-id="beb09-149">Service Map supports only 64-bit platforms.</span></span>

<span data-ttu-id="beb09-150">在 Windows 中，hello Microsoft Monitoring Agent (MMA) 會使用 System Center Operations Manager 和 Operations Management Suite toogather 和監視資料傳送。</span><span class="sxs-lookup"><span data-stu-id="beb09-150">On Windows, hello Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Operations Management Suite toogather and send monitoring data.</span></span> <span data-ttu-id="beb09-151">（此代理程式稱為 hello System Center Operations Manager 代理程式、 OMS 代理程式、 記錄分析代理程式、 MMA 或直接代理程式，視 hello 內容而定）。System Center Operations Manager 和 Operations Management Suite 提供不同外的 hello 方塊 hello MMA 版本。</span><span class="sxs-lookup"><span data-stu-id="beb09-151">(This agent is called hello System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent, depending on hello context.) System Center Operations Manager and Operations Management Suite provide different out-of-hello box versions of hello MMA.</span></span> <span data-ttu-id="beb09-152">這些版本可以每個報告 tooSystem Center Operations Manager、 tooOperations Management Suite 或 tooboth。</span><span class="sxs-lookup"><span data-stu-id="beb09-152">These versions can each report tooSystem Center Operations Manager, tooOperations Management Suite, or tooboth.</span></span>  

<span data-ttu-id="beb09-153">在 Linux 上 hello Linux 收集和監視資料 tooOperations Management Suite 的資訊傳送的 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-153">On Linux, hello OMS Agent for Linux gathers and sends monitoring data tooOperations Management Suite.</span></span> <span data-ttu-id="beb09-154">附加的 tooOperations Management Suite，透過 System Center Operations Manager 管理群組的伺服器或與 OMS 直接代理程式伺服器上，您可以使用服務對應。</span><span class="sxs-lookup"><span data-stu-id="beb09-154">You can use Service Map on servers with OMS Direct Agents or on servers that are attached tooOperations Management Suite via System Center Operations Manager management groups.</span></span>  

<span data-ttu-id="beb09-155">在本文中，我們將是否參照 tooall 代理程式-Linux 或 Windows 中，是否連接 tooa System Center Operations Manager 管理群組，或直接 tooOperations Management Suite-如 hello 「 OMS 代理程式 」。</span><span class="sxs-lookup"><span data-stu-id="beb09-155">In this article, we'll refer tooall agents--whether Linux or Windows, whether connected tooa System Center Operations Manager management group or directly tooOperations Management Suite--as hello "OMS Agent."</span></span> <span data-ttu-id="beb09-156">只有當它所需的內容，我們將使用 hello hello 代理程式的特定部署名稱。</span><span class="sxs-lookup"><span data-stu-id="beb09-156">We'll use hello specific deployment name of hello agent only if it's needed for context.</span></span>

<span data-ttu-id="beb09-157">hello 服務對應的代理程式不會傳輸任何資料本身，並不需要任何變更 toofirewalls 或連接埠。</span><span class="sxs-lookup"><span data-stu-id="beb09-157">hello Service Map agent does not transmit any data itself, and it does not require any changes toofirewalls or ports.</span></span> <span data-ttu-id="beb09-158">服務對應中的 hello 資料一律被經由 hello OMS Agent tooOperations Management Suite，直接或透過 hello OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="beb09-158">hello data in Service Map is always transmitted by hello OMS Agent tooOperations Management Suite, either directly or via hello OMS Gateway.</span></span>

![服務對應代理程式](media/oms-service-map/agents.png)

<span data-ttu-id="beb09-160">如果您是 System Center Operations Manager 的客戶與管理群組連線 tooOperations Management Suite 的資訊：</span><span class="sxs-lookup"><span data-stu-id="beb09-160">If you are a System Center Operations Manager customer with a management group connected tooOperations Management Suite:</span></span>

- <span data-ttu-id="beb09-161">如果您的 System Center Operations Manager 代理程式能夠存取 hello 網際網路 tooconnect tooOperations Management Suite，其他就不需要設定。</span><span class="sxs-lookup"><span data-stu-id="beb09-161">If your System Center Operations Manager agents can access hello Internet tooconnect tooOperations Management Suite, no additional configuration is required.</span></span>  
- <span data-ttu-id="beb09-162">如果您的 System Center Operations Manager 代理程式無法透過 hello 網際網路存取 Operations Management Suite，您需要 tooconfigure hello OMS 閘道 toowork 與 System Center Operations Manager。</span><span class="sxs-lookup"><span data-stu-id="beb09-162">If your System Center Operations Manager agents cannot access Operations Management Suite over hello Internet, you need tooconfigure hello OMS Gateway toowork with System Center Operations Manager.</span></span>
  
<span data-ttu-id="beb09-163">如果您使用 hello OMS 直接代理程式，您需要 tooconfigure hello OMS 代理程式本身，tooconnect tooOperations Management Suite 的資訊或 tooyour OMS 閘道也一樣。</span><span class="sxs-lookup"><span data-stu-id="beb09-163">If you are using hello OMS Direct Agent, you need tooconfigure hello OMS Agent itself tooconnect tooOperations Management Suite or tooyour OMS Gateway.</span></span> <span data-ttu-id="beb09-164">hello OMS 閘道可以從下載 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666)。</span><span class="sxs-lookup"><span data-stu-id="beb09-164">hello OMS Gateway can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

### <a name="management-packs"></a><span data-ttu-id="beb09-165">管理組件</span><span class="sxs-lookup"><span data-stu-id="beb09-165">Management packs</span></span>
<span data-ttu-id="beb09-166">Operations Management Suite 工作區中啟動服務對應時，300 KB 管理組件會傳送 tooall hello Windows 伺服器，該工作區中。</span><span class="sxs-lookup"><span data-stu-id="beb09-166">When Service Map is activated in an Operations Management Suite workspace, a 300-KB management pack is sent tooall hello Windows servers in that workspace.</span></span> <span data-ttu-id="beb09-167">如果您使用 System Center Operations Manager 代理程式在[連線的管理群組](../log-analytics/log-analytics-om-agents.md)，hello 服務對應管理組件從 System Center Operations Manager 部署。</span><span class="sxs-lookup"><span data-stu-id="beb09-167">If you are using System Center Operations Manager agents in a [connected management group](../log-analytics/log-analytics-om-agents.md), hello Service Map management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="beb09-168">如果 hello 代理程式直接連接，Operations Management Suite 提供 hello 管理組件。</span><span class="sxs-lookup"><span data-stu-id="beb09-168">If hello agents are directly connected, Operations Management Suite delivers hello management pack.</span></span>

<span data-ttu-id="beb09-169">hello 管理組件是名為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。</span><span class="sxs-lookup"><span data-stu-id="beb09-169">hello management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="beb09-170">它的書面的 too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management packs\<。</span><span class="sxs-lookup"><span data-stu-id="beb09-170">It's written too%Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\.</span></span> <span data-ttu-id="beb09-171">hello hello 管理組件使用的資料來源為 %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID > \Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。</span><span class="sxs-lookup"><span data-stu-id="beb09-171">hello data source that hello management pack uses is %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="installation"></a><span data-ttu-id="beb09-172">安裝</span><span class="sxs-lookup"><span data-stu-id="beb09-172">Installation</span></span>
### <a name="install-hello-dependency-agent-on-microsoft-windows"></a><span data-ttu-id="beb09-173">在 Microsoft Windows 上安裝 hello 相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="beb09-173">Install hello Dependency Agent on Microsoft Windows</span></span>
<span data-ttu-id="beb09-174">系統管理員權限需要的 tooinstall 或解除安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-174">Administrator privileges are required tooinstall or uninstall hello agent.</span></span>

<span data-ttu-id="beb09-175">hello 相依性代理程式已安裝於 Windows 電腦透過 InstallDependencyAgent Windows.exe。</span><span class="sxs-lookup"><span data-stu-id="beb09-175">hello Dependency Agent is installed on Windows computers through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="beb09-176">如果您執行這個可執行檔不使用任何選項時，它會啟動精靈，您可以依照 tooinstall 以互動方式。</span><span class="sxs-lookup"><span data-stu-id="beb09-176">If you run this executable file without any options, it starts a wizard that you can follow tooinstall interactively.</span></span>  

<span data-ttu-id="beb09-177">使用下列步驟 tooinstall hello 相依性代理程式在每一部 Windows 電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="beb09-177">Use hello following steps tooinstall hello Dependency Agent on each Windows computer:</span></span>

1.  <span data-ttu-id="beb09-178">安裝 hello OMS 代理程式使用 hello 指示[連接 Windows Azure 中的記錄分析服務的電腦 toohello](../log-analytics/log-analytics-windows-agents.md)。</span><span class="sxs-lookup"><span data-stu-id="beb09-178">Install hello OMS Agent by using hello instructions at [Connect Windows computers toohello Log Analytics service in Azure](../log-analytics/log-analytics-windows-agents.md).</span></span>
2.  <span data-ttu-id="beb09-179">下載 hello Windows 代理程式，並執行，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="beb09-179">Download hello Windows agent and run it by using hello following command:</span></span> <br>`InstallDependencyAgent-Windows.exe`
3.  <span data-ttu-id="beb09-180">請遵循 hello 精靈 tooinstall hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-180">Follow hello wizard tooinstall hello agent.</span></span>
4.  <span data-ttu-id="beb09-181">Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-181">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="beb09-182">Windows 代理程式上, hello 記錄檔目錄為 %Programfiles%\Microsoft 相依性 Agent\logs。</span><span class="sxs-lookup"><span data-stu-id="beb09-182">On Windows agents, hello log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span> 

#### <a name="windows-command-line"></a><span data-ttu-id="beb09-183">Windows 命令列</span><span class="sxs-lookup"><span data-stu-id="beb09-183">Windows command line</span></span>
<span data-ttu-id="beb09-184">使用命令列中的下列資料表 tooinstall hello 的選項。</span><span class="sxs-lookup"><span data-stu-id="beb09-184">Use options from hello following table tooinstall from a command line.</span></span> <span data-ttu-id="beb09-185">toosee hello 安裝旗標，使用 hello 執行 hello 安裝程式的清單 /？</span><span class="sxs-lookup"><span data-stu-id="beb09-185">toosee a list of hello installation flags, run hello installer by using hello /?</span></span> <span data-ttu-id="beb09-186">如下所示。</span><span class="sxs-lookup"><span data-stu-id="beb09-186">flag as follows.</span></span>

    InstallDependencyAgent-Windows.exe /?

| <span data-ttu-id="beb09-187">旗標</span><span class="sxs-lookup"><span data-stu-id="beb09-187">Flag</span></span> | <span data-ttu-id="beb09-188">說明</span><span class="sxs-lookup"><span data-stu-id="beb09-188">Description</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-189">/?</span><span class="sxs-lookup"><span data-stu-id="beb09-189">/?</span></span> | <span data-ttu-id="beb09-190">取得 hello 命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="beb09-190">Get a list of hello command-line options.</span></span> |
| <span data-ttu-id="beb09-191">/S</span><span class="sxs-lookup"><span data-stu-id="beb09-191">/S</span></span> | <span data-ttu-id="beb09-192">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="beb09-192">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="beb09-193">根據預設，hello Windows 相依性代理程式的檔案會放置於 C:\Program Files\Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-193">Files for hello Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-hello-dependency-agent-on-linux"></a><span data-ttu-id="beb09-194">Linux 上安裝 hello 相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="beb09-194">Install hello Dependency Agent on Linux</span></span>
<span data-ttu-id="beb09-195">將根目錄存取必要的 tooinstall 或 hello 代理程式設定。</span><span class="sxs-lookup"><span data-stu-id="beb09-195">Root access is required tooinstall or configure hello agent.</span></span>

<span data-ttu-id="beb09-196">hello 相依性代理程式會安裝在透過 InstallDependencyAgent Linux64.bin，與自我解壓縮二進位的殼層指令碼的 Linux 電腦上。</span><span class="sxs-lookup"><span data-stu-id="beb09-196">hello Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="beb09-197">您可以使用 sh 執行 hello 檔案或新增執行權限 toohello 檔案本身。</span><span class="sxs-lookup"><span data-stu-id="beb09-197">You can run hello file by using sh or add execute permissions toohello file itself.</span></span>
 
<span data-ttu-id="beb09-198">使用下列步驟 tooinstall hello 相依性代理程式在每一部 Linux 電腦上的 hello:</span><span class="sxs-lookup"><span data-stu-id="beb09-198">Use hello following steps tooinstall hello Dependency Agent on each Linux computer:</span></span>

1.  <span data-ttu-id="beb09-199">安裝 hello OMS 代理程式使用 hello 指示[收集和管理資料從 Linux 電腦](https://technet.microsoft.com/library/mt622052.aspx)。</span><span class="sxs-lookup"><span data-stu-id="beb09-199">Install hello OMS Agent by using hello instructions at [Collect and manage data from Linux computers](https://technet.microsoft.com/library/mt622052.aspx).</span></span>
2.  <span data-ttu-id="beb09-200">使用下列命令的 hello，hello Linux 相依性代理程式安裝為根：</span><span class="sxs-lookup"><span data-stu-id="beb09-200">Install hello Linux Dependency agent as root by using hello following command:</span></span><br>`sh InstallDependencyAgent-Linux64.bin`
3.  <span data-ttu-id="beb09-201">Toostart hello 相依性代理程式時，請檢查 hello 記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-201">If hello Dependency Agent fails toostart, check hello logs for detailed error information.</span></span> <span data-ttu-id="beb09-202">Linux 代理程式，在 hello 記錄目錄不是 /var/opt/microsoft/dependency-agent/log。</span><span class="sxs-lookup"><span data-stu-id="beb09-202">On Linux agents, hello log directory is /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="beb09-203">toosee hello 安裝旗標，執行與 hello 安裝程式的清單 hello-說明旗標，如下所示。</span><span class="sxs-lookup"><span data-stu-id="beb09-203">toosee a list of hello installation flags, run hello installation program with hello -help flag as follows.</span></span>

    InstallDependencyAgent-Linux64.bin -help

| <span data-ttu-id="beb09-204">旗標</span><span class="sxs-lookup"><span data-stu-id="beb09-204">Flag</span></span> | <span data-ttu-id="beb09-205">說明</span><span class="sxs-lookup"><span data-stu-id="beb09-205">Description</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-206">-help</span><span class="sxs-lookup"><span data-stu-id="beb09-206">-help</span></span> | <span data-ttu-id="beb09-207">取得 hello 命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="beb09-207">Get a list of hello command-line options.</span></span> |
| <span data-ttu-id="beb09-208">-s</span><span class="sxs-lookup"><span data-stu-id="beb09-208">-s</span></span> | <span data-ttu-id="beb09-209">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="beb09-209">Perform a silent installation with no user prompts.</span></span> |
| <span data-ttu-id="beb09-210">--check</span><span class="sxs-lookup"><span data-stu-id="beb09-210">--check</span></span> | <span data-ttu-id="beb09-211">檢查權限與 hello 作業系統，但不是安裝 hello 代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-211">Check permissions and hello operating system but do not install hello agent.</span></span> |

<span data-ttu-id="beb09-212">Hello 相依性代理程式的檔案會放置於 hello 下列目錄：</span><span class="sxs-lookup"><span data-stu-id="beb09-212">Files for hello Dependency Agent are placed in hello following directories:</span></span>

| <span data-ttu-id="beb09-213">檔案</span><span class="sxs-lookup"><span data-stu-id="beb09-213">Files</span></span> | <span data-ttu-id="beb09-214">位置</span><span class="sxs-lookup"><span data-stu-id="beb09-214">Location</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-215">核心檔案</span><span class="sxs-lookup"><span data-stu-id="beb09-215">Core files</span></span> | <span data-ttu-id="beb09-216">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="beb09-216">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="beb09-217">記錄檔</span><span class="sxs-lookup"><span data-stu-id="beb09-217">Log files</span></span> | <span data-ttu-id="beb09-218">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="beb09-218">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="beb09-219">組態檔</span><span class="sxs-lookup"><span data-stu-id="beb09-219">Config files</span></span> | <span data-ttu-id="beb09-220">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="beb09-220">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="beb09-221">服務可執行檔</span><span class="sxs-lookup"><span data-stu-id="beb09-221">Service executable files</span></span> | <span data-ttu-id="beb09-222">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="beb09-222">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><span data-ttu-id="beb09-223">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="beb09-223">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="beb09-224">二進位儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="beb09-224">Binary storage files</span></span> | <span data-ttu-id="beb09-225">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="beb09-225">/var/opt/microsoft/dependency-agent/storage</span></span> |

## <a name="installation-script-examples"></a><span data-ttu-id="beb09-226">安裝指令碼範例</span><span class="sxs-lookup"><span data-stu-id="beb09-226">Installation script examples</span></span>
<span data-ttu-id="beb09-227">tooeasily 部署 hello 相依性代理程式在許多伺服器上的一次，它可協助 toouse 指令碼。</span><span class="sxs-lookup"><span data-stu-id="beb09-227">tooeasily deploy hello Dependency Agent on many servers at once, it helps toouse a script.</span></span> <span data-ttu-id="beb09-228">您可以使用下列指令碼範例 toodownload hello 和 hello 相依性代理程式安裝在 Windows 或 Linux。</span><span class="sxs-lookup"><span data-stu-id="beb09-228">You can use hello following script examples toodownload and install hello Dependency Agent on either Windows or Linux.</span></span>

### <a name="powershell-script-for-windows"></a><span data-ttu-id="beb09-229">適用於 Windows 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="beb09-229">PowerShell script for Windows</span></span>
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a><span data-ttu-id="beb09-230">適用於 Linux 的殼層指令碼</span><span class="sxs-lookup"><span data-stu-id="beb09-230">Shell script for Linux</span></span>
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a><span data-ttu-id="beb09-231">期望的狀態設定</span><span class="sxs-lookup"><span data-stu-id="beb09-231">Desired State Configuration</span></span>
<span data-ttu-id="beb09-232">toodeploy hello 相依性代理程式透過預期狀態設定，您可以使用 hello xPSDesiredStateConfiguration 模組和有點類似 hello 下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="beb09-232">toodeploy hello Dependency Agent via Desired State Configuration, you can use hello xPSDesiredStateConfiguration module and a bit of code like hello following:</span></span>
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install hello Dependency Agent
    xRemoteFile DAPackage 
    {
        Uri = "https://aka.ms/dependencyagentwindows"
        DestinationPath = $DAPackageLocalPath
    }

    xPackage DA
    {
        Ensure="Present"
        Name = "Dependency Agent"
        Path = $DAPackageLocalPath
        Arguments = '/S'
        ProductId = ""
        InstalledCheckRegKey = "HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\DependencyAgent"
        InstalledCheckRegValueName = "DisplayName"
        InstalledCheckRegValueData = "Dependency Agent"
        DependsOn = "[xRemoteFile]DAPackage"
    }
  }
}
```

## <a name="uninstallation"></a><span data-ttu-id="beb09-233">解除安裝</span><span class="sxs-lookup"><span data-stu-id="beb09-233">Uninstallation</span></span>
### <a name="uninstall-hello-dependency-agent-on-windows"></a><span data-ttu-id="beb09-234">解除安裝相依性代理程式在 Windows hello</span><span class="sxs-lookup"><span data-stu-id="beb09-234">Uninstall hello Dependency Agent on Windows</span></span>
<span data-ttu-id="beb09-235">系統管理員可以解除安裝 hello 相依性代理程式的 Windows 控制台。</span><span class="sxs-lookup"><span data-stu-id="beb09-235">An administrator can uninstall hello Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="beb09-236">系統管理員也可以執行 %Programfiles%\Microsoft 相依性 Agent\Uninstall.exe toouninstall hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-236">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe toouninstall hello Dependency Agent.</span></span>

### <a name="uninstall-hello-dependency-agent-on-linux"></a><span data-ttu-id="beb09-237">解除安裝 hello Linux 上的相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="beb09-237">Uninstall hello Dependency Agent on Linux</span></span>
<span data-ttu-id="beb09-238">toocompletely 解除安裝 hello 相依性代理程式從 Linux，您必須移除 hello 代理程式本身並 hello hello 代理程式會自動安裝的連接器。</span><span class="sxs-lookup"><span data-stu-id="beb09-238">toocompletely uninstall hello Dependency Agent from Linux, you must remove hello agent itself and hello connector, which is installed automatically with hello agent.</span></span> <span data-ttu-id="beb09-239">您可以使用下列單一命令的 hello 同時解除安裝：</span><span class="sxs-lookup"><span data-stu-id="beb09-239">You can uninstall both by using hello following single command:</span></span>

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a><span data-ttu-id="beb09-240">疑難排解</span><span class="sxs-lookup"><span data-stu-id="beb09-240">Troubleshooting</span></span>
<span data-ttu-id="beb09-241">如果您在安裝或執行服務對應時遇到任何問題，本節內容可以提供協助。</span><span class="sxs-lookup"><span data-stu-id="beb09-241">If you have any problems installing or running Service Map, this section can help you.</span></span> <span data-ttu-id="beb09-242">如果您仍然無法解決問題，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="beb09-242">If you still can't resolve your problem, please contact Microsoft Support.</span></span>

### <a name="dependency-agent-installation-problems"></a><span data-ttu-id="beb09-243">相依性代理程式安裝問題</span><span class="sxs-lookup"><span data-stu-id="beb09-243">Dependency Agent installation problems</span></span>
#### <a name="installer-asks-for-a-reboot"></a><span data-ttu-id="beb09-244">安裝程式會要求重新開機</span><span class="sxs-lookup"><span data-stu-id="beb09-244">Installer asks for a reboot</span></span>
<span data-ttu-id="beb09-245">相依性代理程式 hello*通常*不需要安裝或解除安裝後的重新開機。</span><span class="sxs-lookup"><span data-stu-id="beb09-245">hello Dependency Agent *generally* does not require a reboot upon installation or uninstallation.</span></span> <span data-ttu-id="beb09-246">不過，在某些罕見的情況下，Windows Server 需要重新開機 toocontinue 與安裝。</span><span class="sxs-lookup"><span data-stu-id="beb09-246">However, in certain rare cases, Windows Server requires a reboot toocontinue with an installation.</span></span> <span data-ttu-id="beb09-247">這會為相依性，通常 hello Microsoft Visual c + + 可轉散發套件，因為鎖定的檔案需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="beb09-247">This happens when a dependency, usually hello Microsoft Visual C++ Redistributable, requires a reboot because of a locked file.</span></span>

#### <a name="message-unable-tooinstall-dependency-agent-visual-studio-runtime-libraries-failed-tooinstall-code--codenumber-appears"></a><span data-ttu-id="beb09-248">訊息 「 無法 tooinstall 相依性代理程式： Visual Studio 執行階段程式庫無法 tooinstall (程式碼 = [code_number])"會出現</span><span class="sxs-lookup"><span data-stu-id="beb09-248">Message "Unable tooinstall Dependency Agent: Visual Studio Runtime libraries failed tooinstall (code = [code_number])" appears</span></span>

<span data-ttu-id="beb09-249">hello Microsoft 相依性代理程式是建置在 hello Microsoft Visual Studio 執行階段程式庫。</span><span class="sxs-lookup"><span data-stu-id="beb09-249">hello Microsoft Dependency Agent is built on hello Microsoft Visual Studio runtime libraries.</span></span> <span data-ttu-id="beb09-250">如果在 hello 程式庫安裝期間發生問題，您會收到訊息。</span><span class="sxs-lookup"><span data-stu-id="beb09-250">You'll get a message if there's a problem during installation of hello libraries.</span></span> 

<span data-ttu-id="beb09-251">安裝程式-執行階段程式庫 hello hello %LOCALAPPDATA%\temp 資料夾中建立記錄檔。</span><span class="sxs-lookup"><span data-stu-id="beb09-251">hello runtime library installers create logs in hello %LOCALAPPDATA%\temp folder.</span></span> <span data-ttu-id="beb09-252">hello 檔案是 dd_vcredist_arch_yyyymmddhhmmss.log，其中*arch* 「 x86 」 或 「 amd64 」 和*yyyymmddhhmmss*是 hello 日期和時間 （24 小時制） 建立 hello 記錄時。</span><span class="sxs-lookup"><span data-stu-id="beb09-252">hello file is dd_vcredist_arch_yyyymmddhhmmss.log, where *arch* is "x86" or "amd64" and *yyyymmddhhmmss* is hello date and time (24-hour clock) when hello log was created.</span></span> <span data-ttu-id="beb09-253">hello 記錄提供有關 hello 問題會封鎖安裝詳細資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-253">hello log provides details about hello problem that's blocking installation.</span></span>

<span data-ttu-id="beb09-254">它可能會很有用的 tooinstall hello[最新的執行階段程式庫](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)自行第一次。</span><span class="sxs-lookup"><span data-stu-id="beb09-254">It might be useful tooinstall hello [latest runtime libraries](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) yourself first.</span></span>

<span data-ttu-id="beb09-255">hello 下表列出程式碼數字和建議的解決方式。</span><span class="sxs-lookup"><span data-stu-id="beb09-255">hello following table lists code numbers and suggested resolutions.</span></span>

| <span data-ttu-id="beb09-256">代碼</span><span class="sxs-lookup"><span data-stu-id="beb09-256">Code</span></span> | <span data-ttu-id="beb09-257">說明</span><span class="sxs-lookup"><span data-stu-id="beb09-257">Description</span></span> | <span data-ttu-id="beb09-258">解決方案</span><span class="sxs-lookup"><span data-stu-id="beb09-258">Resolution</span></span> |
|:--|:--|:--|
| <span data-ttu-id="beb09-259">0x17</span><span class="sxs-lookup"><span data-stu-id="beb09-259">0x17</span></span> | <span data-ttu-id="beb09-260">hello 程式庫安裝程式需要尚未安裝 Windows update。</span><span class="sxs-lookup"><span data-stu-id="beb09-260">hello library installer requires a Windows update that hasn't been installed.</span></span> | <span data-ttu-id="beb09-261">查看 hello 最新文件庫安裝程式記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="beb09-261">Look in hello most recent library installer log.</span></span><br><br><span data-ttu-id="beb09-262">如果參考太"Windows8.1-KB2999226-x64.msu 」 後面接著一條線 」 錯誤 0x80240017： 失敗的 tooexecute MSU 封裝時，「 您沒有 hello 必要條件 tooinstall KB2999226。</span><span class="sxs-lookup"><span data-stu-id="beb09-262">If a reference too"Windows8.1-KB2999226-x64.msu" is followed by a line "Error 0x80240017: Failed tooexecute MSU package," you don't have hello prerequisites tooinstall KB2999226.</span></span> <span data-ttu-id="beb09-263">請依照下列中的 hello 必要條件 > 一節中的 hello 指示[通用的 C 執行階段中 Windows](https://support.microsoft.com/kb/2999226)。</span><span class="sxs-lookup"><span data-stu-id="beb09-263">Follow hello instructions in hello prerequisites section in [Universal C Runtime in Windows](https://support.microsoft.com/kb/2999226).</span></span> <span data-ttu-id="beb09-264">您可能會需要 toorun Windows Update 並多次重新開機順序 tooinstall hello 必要條件。</span><span class="sxs-lookup"><span data-stu-id="beb09-264">You might need toorun Windows Update and reboot multiple times in order tooinstall hello prerequisites.</span></span><br><br><span data-ttu-id="beb09-265">重新執行 hello Microsoft 相依性代理程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-265">Run hello Microsoft Dependency Agent installer again.</span></span> |

### <a name="post-installation-issues"></a><span data-ttu-id="beb09-266">安裝後問題</span><span class="sxs-lookup"><span data-stu-id="beb09-266">Post-installation issues</span></span>
#### <a name="server-doesnt-appear-in-service-map"></a><span data-ttu-id="beb09-267">伺服器未出現在服務對應中</span><span class="sxs-lookup"><span data-stu-id="beb09-267">Server doesn't appear in Service Map</span></span>
<span data-ttu-id="beb09-268">如果您的相依性代理程式安裝成功，但您沒有看到您的伺服器 hello 服務對應方案：</span><span class="sxs-lookup"><span data-stu-id="beb09-268">If your Dependency Agent installation succeeded, but you don't see your server in hello Service Map solution:</span></span>
* <span data-ttu-id="beb09-269">Hello 相依性代理程式安裝成功？</span><span class="sxs-lookup"><span data-stu-id="beb09-269">Is hello Dependency Agent installed successfully?</span></span> <span data-ttu-id="beb09-270">您可以藉由檢查 toosee，如果 hello 服務已安裝並執行驗證這點。</span><span class="sxs-lookup"><span data-stu-id="beb09-270">You can validate this by checking toosee if hello service is installed and running.</span></span><br><br><span data-ttu-id="beb09-271">
**Windows**： 尋找 hello 服務名為 「 Microsoft 相依性代理程式 」。</span><span class="sxs-lookup"><span data-stu-id="beb09-271">
**Windows**: Look for hello service named "Microsoft Dependency Agent."</span></span><br><span data-ttu-id="beb09-272">
**Linux**： 尋找 hello 執行程序 「 microsoft-相依性-代理程式。 」</span><span class="sxs-lookup"><span data-stu-id="beb09-272">
**Linux**: Look for hello running process "microsoft-dependency-agent."</span></span>

* <span data-ttu-id="beb09-273">您位於 hello[免費定價層的 Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)？ hello 免費方案允許 toofive 唯一的服務對應伺服器。</span><span class="sxs-lookup"><span data-stu-id="beb09-273">Are you on hello [Free pricing tier of Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)? hello Free plan allows for up toofive unique Service Map servers.</span></span> <span data-ttu-id="beb09-274">任何後續伺服器則不會顯示在服務對應，即使 hello 先前五個不會再傳送資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-274">Any subsequent servers won't show up in Service Map, even if hello prior five are no longer sending data.</span></span>

* <span data-ttu-id="beb09-275">是您伺服器傳送記錄檔和效能資料 tooOperations Management Suite 的資訊？</span><span class="sxs-lookup"><span data-stu-id="beb09-275">Is your server sending log and perf data tooOperations Management Suite?</span></span> <span data-ttu-id="beb09-276">移 tooLog 搜尋，並執行下列查詢，為您的電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="beb09-276">Go tooLog Search and run hello following query for your computer:</span></span> 

        * Computer="<your computer name here>" | measure count() by Type
        
  <span data-ttu-id="beb09-277">您在 hello 結果中取得各種事件？</span><span class="sxs-lookup"><span data-stu-id="beb09-277">Did you get a variety of events in hello results?</span></span> <span data-ttu-id="beb09-278">是新 hello 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="beb09-278">Is hello data recent?</span></span> <span data-ttu-id="beb09-279">如果是這樣，您的 OMS 代理程式是運作正常，而與 hello Operations Management Suite 服務通訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-279">If so, your OMS Agent is operating correctly and communicating with hello Operations Management Suite service.</span></span> <span data-ttu-id="beb09-280">如果沒有，請檢查您的伺服器上的 OMS 代理程式 hello: [OMS Agent for Windows 疑難排解](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)或[OMS Agent for Linux 疑難排解](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="beb09-280">If not, check hello OMS Agent on your server: [OMS Agent for Windows troubleshooting](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) or [OMS Agent for Linux troubleshooting](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).</span></span>

#### <a name="server-appears-in-service-map-but-has-no-processes"></a><span data-ttu-id="beb09-281">伺服器顯示在服務對應中，但是沒有任何處理序</span><span class="sxs-lookup"><span data-stu-id="beb09-281">Server appears in Service Map but has no processes</span></span>
<span data-ttu-id="beb09-282">如果您看到您在服務對應的伺服器，但有任何程序或連接的資料，表示該 hello 相依性代理程式已安裝且正在執行，但未載入 hello 核心驅動程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-282">If you see your server in Service Map, but it has no process or connection data, that indicates that hello Dependency Agent is installed and running, but hello kernel driver didn't load.</span></span> 

<span data-ttu-id="beb09-283">請檢查 hello C:\Program Files\Microsoft 相依性 Agent\logs\wrapper.log 檔案 (Windows) 或 /var/opt/microsoft/dependency-agent/log/service.log 檔案 (Linux)。</span><span class="sxs-lookup"><span data-stu-id="beb09-283">Check hello C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log file (Windows) or /var/opt/microsoft/dependency-agent/log/service.log file (Linux).</span></span> <span data-ttu-id="beb09-284">hello hello 檔案最後一行應該指出為什麼 hello 核心未載入。</span><span class="sxs-lookup"><span data-stu-id="beb09-284">hello last lines of hello file should indicate why hello kernel didn't load.</span></span> <span data-ttu-id="beb09-285">例如，hello 核心可能不支援在 Linux 上如果更新您的核心。</span><span class="sxs-lookup"><span data-stu-id="beb09-285">For example, hello kernel might not be supported on Linux if you updated your kernel.</span></span>

## <a name="data-collection"></a><span data-ttu-id="beb09-286">資料收集</span><span class="sxs-lookup"><span data-stu-id="beb09-286">Data collection</span></span>
<span data-ttu-id="beb09-287">您可以預期每個代理程式 tootransmit 大約每日，視您系統相依性是在多複雜的 25 MB。</span><span class="sxs-lookup"><span data-stu-id="beb09-287">You can expect each agent tootransmit roughly 25 MB per day, depending on how complex your system dependencies are.</span></span> <span data-ttu-id="beb09-288">每個代理程式每隔 15 秒就會傳送服務對應相依性資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-288">Each agent sends Service Map dependency data every 15 seconds.</span></span>  

<span data-ttu-id="beb09-289">hello 相依性代理程式通常會耗用 0.1%的系統記憶體和 0.1%的系統 CPU。</span><span class="sxs-lookup"><span data-stu-id="beb09-289">hello Dependency Agent typically consumes 0.1 percent of system memory and 0.1 percent of system CPU.</span></span>

## <a name="supported-azure-regions"></a><span data-ttu-id="beb09-290">支援的 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="beb09-290">Supported Azure regions</span></span>
<span data-ttu-id="beb09-291">服務對應是目前可用於下列 Azure 區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="beb09-291">Service Map is currently available in hello following Azure regions:</span></span>
- <span data-ttu-id="beb09-292">美國東部</span><span class="sxs-lookup"><span data-stu-id="beb09-292">East US</span></span>
- <span data-ttu-id="beb09-293">西歐</span><span class="sxs-lookup"><span data-stu-id="beb09-293">West Europe</span></span>
- <span data-ttu-id="beb09-294">美國中西部</span><span class="sxs-lookup"><span data-stu-id="beb09-294">West Central US</span></span>


## <a name="supported-operating-systems"></a><span data-ttu-id="beb09-295">受支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="beb09-295">Supported operating systems</span></span>
<span data-ttu-id="beb09-296">hello 下列各節列出 hello 支援的作業系統 hello 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="beb09-296">hello following sections list hello supported operating systems for hello Dependency Agent.</span></span> <span data-ttu-id="beb09-297">服務對應不支援任何 32 位元架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="beb09-297">Service Map doesn't support 32-bit architectures for any operating system.</span></span>

### <a name="windows-server"></a><span data-ttu-id="beb09-298">Windows Server</span><span class="sxs-lookup"><span data-stu-id="beb09-298">Windows Server</span></span>
- <span data-ttu-id="beb09-299">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="beb09-299">Windows Server 2016</span></span>
- <span data-ttu-id="beb09-300">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="beb09-300">Windows Server 2012 R2</span></span>
- <span data-ttu-id="beb09-301">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="beb09-301">Windows Server 2012</span></span>
- <span data-ttu-id="beb09-302">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="beb09-302">Windows Server 2008 R2 SP1</span></span>

### <a name="windows-desktop"></a><span data-ttu-id="beb09-303">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="beb09-303">Windows desktop</span></span>
- <span data-ttu-id="beb09-304">Windows 10</span><span class="sxs-lookup"><span data-stu-id="beb09-304">Windows 10</span></span>
- <span data-ttu-id="beb09-305">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="beb09-305">Windows 8.1</span></span>
- <span data-ttu-id="beb09-306">Windows 8</span><span class="sxs-lookup"><span data-stu-id="beb09-306">Windows 8</span></span>
- <span data-ttu-id="beb09-307">Windows 7</span><span class="sxs-lookup"><span data-stu-id="beb09-307">Windows 7</span></span>

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="beb09-308">Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)</span><span class="sxs-lookup"><span data-stu-id="beb09-308">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>
- <span data-ttu-id="beb09-309">只支援預設版本和 SMP Linux 核心版本。</span><span class="sxs-lookup"><span data-stu-id="beb09-309">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="beb09-310">所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。</span><span class="sxs-lookup"><span data-stu-id="beb09-310">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="beb09-311">例如，"2.6.16.21-0.8-xen"hello 版本字串的系統不支援。</span><span class="sxs-lookup"><span data-stu-id="beb09-311">For example, a system with hello release string of "2.6.16.21-0.8-xen" is not supported.</span></span>
- <span data-ttu-id="beb09-312">不支援自訂核心，包括重新編譯的標準核心。</span><span class="sxs-lookup"><span data-stu-id="beb09-312">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="beb09-313">不支援 CentOSPlus 核心。</span><span class="sxs-lookup"><span data-stu-id="beb09-313">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="beb09-314">Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。</span><span class="sxs-lookup"><span data-stu-id="beb09-314">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>


#### <a name="red-hat-linux-7"></a><span data-ttu-id="beb09-315">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="beb09-315">Red Hat Linux 7</span></span>
| <span data-ttu-id="beb09-316">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-316">OS version</span></span> | <span data-ttu-id="beb09-317">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-317">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-318">7.0</span><span class="sxs-lookup"><span data-stu-id="beb09-318">7.0</span></span> | <span data-ttu-id="beb09-319">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="beb09-319">3.10.0-123</span></span> |
| <span data-ttu-id="beb09-320">7.1</span><span class="sxs-lookup"><span data-stu-id="beb09-320">7.1</span></span> | <span data-ttu-id="beb09-321">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="beb09-321">3.10.0-229</span></span> |
| <span data-ttu-id="beb09-322">7.2</span><span class="sxs-lookup"><span data-stu-id="beb09-322">7.2</span></span> | <span data-ttu-id="beb09-323">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="beb09-323">3.10.0-327</span></span> |
| <span data-ttu-id="beb09-324">7.3</span><span class="sxs-lookup"><span data-stu-id="beb09-324">7.3</span></span> | <span data-ttu-id="beb09-325">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="beb09-325">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="beb09-326">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="beb09-326">Red Hat Linux 6</span></span>
| <span data-ttu-id="beb09-327">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-327">OS version</span></span> | <span data-ttu-id="beb09-328">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-328">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-329">6.0</span><span class="sxs-lookup"><span data-stu-id="beb09-329">6.0</span></span> | <span data-ttu-id="beb09-330">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="beb09-330">2.6.32-71</span></span> |
| <span data-ttu-id="beb09-331">6.1</span><span class="sxs-lookup"><span data-stu-id="beb09-331">6.1</span></span> | <span data-ttu-id="beb09-332">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="beb09-332">2.6.32-131</span></span> |
| <span data-ttu-id="beb09-333">6.2</span><span class="sxs-lookup"><span data-stu-id="beb09-333">6.2</span></span> | <span data-ttu-id="beb09-334">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="beb09-334">2.6.32-220</span></span> |
| <span data-ttu-id="beb09-335">6.3</span><span class="sxs-lookup"><span data-stu-id="beb09-335">6.3</span></span> | <span data-ttu-id="beb09-336">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="beb09-336">2.6.32-279</span></span> |
| <span data-ttu-id="beb09-337">6.4</span><span class="sxs-lookup"><span data-stu-id="beb09-337">6.4</span></span> | <span data-ttu-id="beb09-338">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="beb09-338">2.6.32-358</span></span> |
| <span data-ttu-id="beb09-339">6.5</span><span class="sxs-lookup"><span data-stu-id="beb09-339">6.5</span></span> | <span data-ttu-id="beb09-340">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="beb09-340">2.6.32-431</span></span> |
| <span data-ttu-id="beb09-341">6.6</span><span class="sxs-lookup"><span data-stu-id="beb09-341">6.6</span></span> | <span data-ttu-id="beb09-342">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="beb09-342">2.6.32-504</span></span> |
| <span data-ttu-id="beb09-343">6.7</span><span class="sxs-lookup"><span data-stu-id="beb09-343">6.7</span></span> | <span data-ttu-id="beb09-344">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="beb09-344">2.6.32-573</span></span> |
| <span data-ttu-id="beb09-345">6.8</span><span class="sxs-lookup"><span data-stu-id="beb09-345">6.8</span></span> | <span data-ttu-id="beb09-346">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="beb09-346">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="beb09-347">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="beb09-347">Red Hat Linux 5</span></span>
| <span data-ttu-id="beb09-348">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-348">OS version</span></span> | <span data-ttu-id="beb09-349">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-349">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="beb09-350">5.8</span><span class="sxs-lookup"><span data-stu-id="beb09-350">5.8</span></span> | <span data-ttu-id="beb09-351">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="beb09-351">2.6.18-308</span></span> |
| <span data-ttu-id="beb09-352">5.9</span><span class="sxs-lookup"><span data-stu-id="beb09-352">5.9</span></span> | <span data-ttu-id="beb09-353">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="beb09-353">2.6.18-348</span></span> |
| <span data-ttu-id="beb09-354">5.10</span><span class="sxs-lookup"><span data-stu-id="beb09-354">5.10</span></span> | <span data-ttu-id="beb09-355">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="beb09-355">2.6.18-371</span></span> |
| <span data-ttu-id="beb09-356">5.11</span><span class="sxs-lookup"><span data-stu-id="beb09-356">5.11</span></span> | <span data-ttu-id="beb09-357">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="beb09-357">2.6.18-398</span></span><br><span data-ttu-id="beb09-358">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="beb09-358">2.6.18-400</span></span><br><span data-ttu-id="beb09-359">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="beb09-359">2.6.18-402</span></span><br><span data-ttu-id="beb09-360">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="beb09-360">2.6.18-404</span></span><br><span data-ttu-id="beb09-361">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="beb09-361">2.6.18-406</span></span><br><span data-ttu-id="beb09-362">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="beb09-362">2.6.18-407</span></span><br><span data-ttu-id="beb09-363">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="beb09-363">2.6.18-408</span></span><br><span data-ttu-id="beb09-364">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="beb09-364">2.6.18-409</span></span><br><span data-ttu-id="beb09-365">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="beb09-365">2.6.18-410</span></span><br><span data-ttu-id="beb09-366">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="beb09-366">2.6.18-411</span></span><br><span data-ttu-id="beb09-367">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="beb09-367">2.6.18-412</span></span><br><span data-ttu-id="beb09-368">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="beb09-368">2.6.18-416</span></span><br><span data-ttu-id="beb09-369">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="beb09-369">2.6.18-417</span></span><br><span data-ttu-id="beb09-370">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="beb09-370">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="beb09-371">Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="beb09-371">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="beb09-372">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="beb09-372">Oracle Linux 6</span></span>
| <span data-ttu-id="beb09-373">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-373">OS version</span></span> | <span data-ttu-id="beb09-374">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-374">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="beb09-375">6.2</span><span class="sxs-lookup"><span data-stu-id="beb09-375">6.2</span></span> | <span data-ttu-id="beb09-376">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="beb09-376">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="beb09-377">6.3</span><span class="sxs-lookup"><span data-stu-id="beb09-377">6.3</span></span> | <span data-ttu-id="beb09-378">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="beb09-378">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="beb09-379">6.4</span><span class="sxs-lookup"><span data-stu-id="beb09-379">6.4</span></span> | <span data-ttu-id="beb09-380">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="beb09-380">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="beb09-381">6.5</span><span class="sxs-lookup"><span data-stu-id="beb09-381">6.5</span></span> | <span data-ttu-id="beb09-382">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="beb09-382">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="beb09-383">6.6</span><span class="sxs-lookup"><span data-stu-id="beb09-383">6.6</span></span> | <span data-ttu-id="beb09-384">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="beb09-384">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="beb09-385">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="beb09-385">Oracle Linux 5</span></span>

| <span data-ttu-id="beb09-386">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-386">OS version</span></span> | <span data-ttu-id="beb09-387">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-387">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="beb09-388">5.8</span><span class="sxs-lookup"><span data-stu-id="beb09-388">5.8</span></span> | <span data-ttu-id="beb09-389">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="beb09-389">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="beb09-390">5.9</span><span class="sxs-lookup"><span data-stu-id="beb09-390">5.9</span></span> | <span data-ttu-id="beb09-391">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="beb09-391">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="beb09-392">5.10</span><span class="sxs-lookup"><span data-stu-id="beb09-392">5.10</span></span> | <span data-ttu-id="beb09-393">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="beb09-393">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="beb09-394">5.11</span><span class="sxs-lookup"><span data-stu-id="beb09-394">5.11</span></span> | <span data-ttu-id="beb09-395">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="beb09-395">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="beb09-396">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="beb09-396">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="beb09-397">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="beb09-397">SUSE Linux 11</span></span>
| <span data-ttu-id="beb09-398">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-398">OS version</span></span> | <span data-ttu-id="beb09-399">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-399">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="beb09-400">11</span><span class="sxs-lookup"><span data-stu-id="beb09-400">11</span></span> | <span data-ttu-id="beb09-401">2.6.27</span><span class="sxs-lookup"><span data-stu-id="beb09-401">2.6.27</span></span> |
| <span data-ttu-id="beb09-402">11 SP1</span><span class="sxs-lookup"><span data-stu-id="beb09-402">11 SP1</span></span> | <span data-ttu-id="beb09-403">2.6.32</span><span class="sxs-lookup"><span data-stu-id="beb09-403">2.6.32</span></span> |
| <span data-ttu-id="beb09-404">11 SP2</span><span class="sxs-lookup"><span data-stu-id="beb09-404">11 SP2</span></span> | <span data-ttu-id="beb09-405">3.0.13</span><span class="sxs-lookup"><span data-stu-id="beb09-405">3.0.13</span></span> |
| <span data-ttu-id="beb09-406">11 SP3</span><span class="sxs-lookup"><span data-stu-id="beb09-406">11 SP3</span></span> | <span data-ttu-id="beb09-407">3.0.76</span><span class="sxs-lookup"><span data-stu-id="beb09-407">3.0.76</span></span> |
| <span data-ttu-id="beb09-408">11 SP4</span><span class="sxs-lookup"><span data-stu-id="beb09-408">11 SP4</span></span> | <span data-ttu-id="beb09-409">3.0.101</span><span class="sxs-lookup"><span data-stu-id="beb09-409">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="beb09-410">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="beb09-410">SUSE Linux 10</span></span>
| <span data-ttu-id="beb09-411">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="beb09-411">OS version</span></span> | <span data-ttu-id="beb09-412">核心版本</span><span class="sxs-lookup"><span data-stu-id="beb09-412">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="beb09-413">10 SP4</span><span class="sxs-lookup"><span data-stu-id="beb09-413">10 SP4</span></span> | <span data-ttu-id="beb09-414">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="beb09-414">2.6.16.60</span></span> |

## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="beb09-415">診斷和使用量資料</span><span class="sxs-lookup"><span data-stu-id="beb09-415">Diagnostic and usage data</span></span>
<span data-ttu-id="beb09-416">Microsoft 會自動收集貴用戶使用服務對應服務的 hello 的使用方式和效能資料。</span><span class="sxs-lookup"><span data-stu-id="beb09-416">Microsoft automatically collects usage and performance data through your use of hello Service Map service.</span></span> <span data-ttu-id="beb09-417">Microsoft 會使用此資料 tooprovide 並提升 hello 品質、 安全性與 hello 服務對應服務的完整性。</span><span class="sxs-lookup"><span data-stu-id="beb09-417">Microsoft uses this data tooprovide and improve hello quality, security, and integrity of hello Service Map service.</span></span> <span data-ttu-id="beb09-418">資料包括您的軟體，如作業系統和版本 hello 組態相關資訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-418">Data includes information about hello configuration of your software, like operating system and version.</span></span> <span data-ttu-id="beb09-419">它也會包含 IP 位址、 DNS 名稱和工作站名稱中順序 tooprovide 正確且有效率地疑難排解功能。</span><span class="sxs-lookup"><span data-stu-id="beb09-419">It also includes IP address, DNS name, and workstation name in order tooprovide accurate and efficient troubleshooting capabilities.</span></span> <span data-ttu-id="beb09-420">我們不會收集姓名、地址或其他連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="beb09-420">We do not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="beb09-421">如需有關資料收集與使用方式的詳細資訊，請參閱 hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132)。</span><span class="sxs-lookup"><span data-stu-id="beb09-421">For more information on data collection and usage, see hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>



## <a name="next-steps"></a><span data-ttu-id="beb09-422">後續步驟</span><span class="sxs-lookup"><span data-stu-id="beb09-422">Next steps</span></span>
- <span data-ttu-id="beb09-423">了解如何太[使用服務對應](operations-management-suite-service-map.md)部署和設定之後。</span><span class="sxs-lookup"><span data-stu-id="beb09-423">Learn how too[use Service Map](operations-management-suite-service-map.md) after it has been deployed and configured.</span></span>
