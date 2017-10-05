---
title: "設定 Operations Management Suite 中的服務對應 | Microsoft Docs"
description: "服務對應是一個 Operations Management Suite 解決方案，可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
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
ms.openlocfilehash: 0da0231f1a6c01ddd95ce7872e0e4aa47dc61f1b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configure-service-map-in-operations-management-suite"></a><span data-ttu-id="a8271-104">設定 Operations Management Suite 中的服務對應</span><span class="sxs-lookup"><span data-stu-id="a8271-104">Configure Service Map in Operations Management Suite</span></span>
<span data-ttu-id="a8271-105">服務對應可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-105">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="a8271-106">您可以使用服務對應，將伺服器視為提供重要服務的互連系統，藉此來檢視伺服器。</span><span class="sxs-lookup"><span data-stu-id="a8271-106">You can use it to view your servers as you think of them--as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="a8271-107">不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連線架構的伺服器、處理序和連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="a8271-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required, other than installation of an agent.</span></span>

<span data-ttu-id="a8271-108">本文說明設定服務對應與啟用代理程式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-108">This article describes the details of configuring Service Map and onboarding agents.</span></span> <span data-ttu-id="a8271-109">如需使用服務對應的相關資訊，請參閱[在 Operations Management Suite 中使用服務對應解決方案](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="a8271-109">For information on using Service Map, see [Use the Service Map solution in Operations Management Suite](operations-management-suite-service-map.md).</span></span>

## <a name="dependency-agent-downloads"></a><span data-ttu-id="a8271-110">相依性代理程式下載</span><span class="sxs-lookup"><span data-stu-id="a8271-110">Dependency Agent downloads</span></span>
| <span data-ttu-id="a8271-111">檔案</span><span class="sxs-lookup"><span data-stu-id="a8271-111">File</span></span> | <span data-ttu-id="a8271-112">作業系統</span><span class="sxs-lookup"><span data-stu-id="a8271-112">OS</span></span> | <span data-ttu-id="a8271-113">版本</span><span class="sxs-lookup"><span data-stu-id="a8271-113">Version</span></span> | <span data-ttu-id="a8271-114">SHA-256</span><span class="sxs-lookup"><span data-stu-id="a8271-114">SHA-256</span></span> |
|:--|:--|:--|:--|
| [<span data-ttu-id="a8271-115">InstallDependencyAgent-Windows.exe</span><span class="sxs-lookup"><span data-stu-id="a8271-115">InstallDependencyAgent-Windows.exe</span></span>](https://aka.ms/dependencyagentwindows) | <span data-ttu-id="a8271-116">Windows</span><span class="sxs-lookup"><span data-stu-id="a8271-116">Windows</span></span> | <span data-ttu-id="a8271-117">9.0.5</span><span class="sxs-lookup"><span data-stu-id="a8271-117">9.0.5</span></span> | <span data-ttu-id="a8271-118">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span><span class="sxs-lookup"><span data-stu-id="a8271-118">73B3F6A2A76A08D58F72A550947FF839B588591C48E6EDDD6DDF73AA3FD82B43</span></span> |
| [<span data-ttu-id="a8271-119">InstallDependencyAgent-Linux64.bin</span><span class="sxs-lookup"><span data-stu-id="a8271-119">InstallDependencyAgent-Linux64.bin</span></span>](https://aka.ms/dependencyagentlinux) | <span data-ttu-id="a8271-120">Linux</span><span class="sxs-lookup"><span data-stu-id="a8271-120">Linux</span></span> | <span data-ttu-id="a8271-121">9.0.5</span><span class="sxs-lookup"><span data-stu-id="a8271-121">9.0.5</span></span> | <span data-ttu-id="a8271-122">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span><span class="sxs-lookup"><span data-stu-id="a8271-122">A1BAD0B36EBF79F2B69113A07FCF48C68D90BD169C722689F9C83C69FC032371</span></span> |


## <a name="connected-sources"></a><span data-ttu-id="a8271-123">連接的來源</span><span class="sxs-lookup"><span data-stu-id="a8271-123">Connected sources</span></span>
<span data-ttu-id="a8271-124">服務對應會從 Microsoft 相依性代理程式取得它的資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-124">Service Map gets its data from the Microsoft Dependency Agent.</span></span> <span data-ttu-id="a8271-125">「相依性代理程式」有賴於 OMS 代理程式，以連線至 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="a8271-125">The Dependency Agent depends on the OMS Agent for its connections to Operations Management Suite.</span></span> <span data-ttu-id="a8271-126">這表示，伺服器必須先安裝並設定 OMS 代理程式，然後才能安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-126">This means that a server must have the OMS Agent installed and configured first, and then the Dependency Agent can be installed.</span></span> <span data-ttu-id="a8271-127">下表描述服務對應解決方案支援的連線來源。</span><span class="sxs-lookup"><span data-stu-id="a8271-127">The following table describes the connected sources that the Service Map solution supports.</span></span>

| <span data-ttu-id="a8271-128">連線的來源</span><span class="sxs-lookup"><span data-stu-id="a8271-128">Connected source</span></span> | <span data-ttu-id="a8271-129">支援</span><span class="sxs-lookup"><span data-stu-id="a8271-129">Supported</span></span> | <span data-ttu-id="a8271-130">說明</span><span class="sxs-lookup"><span data-stu-id="a8271-130">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a8271-131">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-131">Windows agents</span></span> | <span data-ttu-id="a8271-132">是</span><span class="sxs-lookup"><span data-stu-id="a8271-132">Yes</span></span> | <span data-ttu-id="a8271-133">服務對應會分析並收集來自 Windows 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-133">Service Map analyzes and collects data from Windows agent computers.</span></span> <br><br><span data-ttu-id="a8271-134">除了 [OMS 代理程式](../log-analytics/log-analytics-windows-agents.md)外，Windows 代理程式還需要 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-134">In addition to the [OMS Agent](../log-analytics/log-analytics-windows-agents.md), Windows agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="a8271-135">如需作業系統版本的完整清單，請參閱[支援的作業系統](#supported-operating-systems)。</span><span class="sxs-lookup"><span data-stu-id="a8271-135">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="a8271-136">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-136">Linux agents</span></span> | <span data-ttu-id="a8271-137">是</span><span class="sxs-lookup"><span data-stu-id="a8271-137">Yes</span></span> | <span data-ttu-id="a8271-138">服務對應會分析並收集來自 Linux 代理程式電腦的資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-138">Service Map analyzes and collects data from Linux agent computers.</span></span> <br><br><span data-ttu-id="a8271-139">除了 [OMS 代理程式](../log-analytics/log-analytics-linux-agents.md)外，Linux 代理程式還需要 Microsoft 相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-139">In addition to the [OMS Agent](../log-analytics/log-analytics-linux-agents.md), Linux agents require the Microsoft Dependency Agent.</span></span> <span data-ttu-id="a8271-140">如需作業系統版本的完整清單，請參閱[支援的作業系統](#supported-operating-systems)。</span><span class="sxs-lookup"><span data-stu-id="a8271-140">See the [supported operating systems](#supported-operating-systems) for a complete list of operating system versions.</span></span> |
| <span data-ttu-id="a8271-141">System Center Operations Manager 管理群組</span><span class="sxs-lookup"><span data-stu-id="a8271-141">System Center Operations Manager management group</span></span> | <span data-ttu-id="a8271-142">是</span><span class="sxs-lookup"><span data-stu-id="a8271-142">Yes</span></span> | <span data-ttu-id="a8271-143">服務對應會在連線的 [System Center Operations Manager 管理群組](../log-analytics/log-analytics-om-agents.md)中，分析並收集來自 Windows 和 Linux 代理程式的資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-143">Service Map analyzes and collects data from Windows and Linux agents in a connected [System Center Operations Manager management group](../log-analytics/log-analytics-om-agents.md).</span></span> <br><br><span data-ttu-id="a8271-144">System Center Operations Manager 代理程式電腦必須直接連線到 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="a8271-144">A direct connection from the System Center Operations Manager agent computer to Operations Management Suite is required.</span></span> <span data-ttu-id="a8271-145">資料會從管理群組轉送至 Operations Management Suite 存放庫。</span><span class="sxs-lookup"><span data-stu-id="a8271-145">Data is forwarded from the management group to the Operations Management Suite repository.</span></span>|
| <span data-ttu-id="a8271-146">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a8271-146">Azure storage account</span></span> | <span data-ttu-id="a8271-147">否</span><span class="sxs-lookup"><span data-stu-id="a8271-147">No</span></span> | <span data-ttu-id="a8271-148">服務對應會收集來自代理程式電腦的資料，因此不會從 Azure 儲存體收集資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-148">Service Map collects data from agent computers, so there is no data from it to collect from Azure Storage.</span></span> |

<span data-ttu-id="a8271-149">服務對應僅支援 64 位元平台。</span><span class="sxs-lookup"><span data-stu-id="a8271-149">Service Map supports only 64-bit platforms.</span></span>

<span data-ttu-id="a8271-150">在 Windows 中，System Center Operations Manager 和 Operations Management Suite 都使用 Microsoft Monitoring Agent (MMA) 來收集和傳送監視資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-150">On Windows, the Microsoft Monitoring Agent (MMA) is used by both System Center Operations Manager and Operations Management Suite to gather and send monitoring data.</span></span> <span data-ttu-id="a8271-151">(視內容而定，此代理程式可稱為 System Center Operations Manager 代理程式、OMS 代理程式、Log Analytics 代理程式、MMA 或直接代理程式)。System Center Operations Manager 和 Operations Management Suite 提供不同的內建 MMA 版本。</span><span class="sxs-lookup"><span data-stu-id="a8271-151">(This agent is called the System Center Operations Manager Agent, OMS Agent, Log Analytics Agent, MMA, or Direct Agent, depending on the context.) System Center Operations Manager and Operations Management Suite provide different out-of-the box versions of the MMA.</span></span> <span data-ttu-id="a8271-152">這些版本可以各自向 System Center Operations Manager 或 Operations Management Suite 報告，或同時向兩者報告。</span><span class="sxs-lookup"><span data-stu-id="a8271-152">These versions can each report to System Center Operations Manager, to Operations Management Suite, or to both.</span></span>  

<span data-ttu-id="a8271-153">在 Linux 上，適用於 Linux 的 OMS 代理程式會收集監視資料並傳送給 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="a8271-153">On Linux, the OMS Agent for Linux gathers and sends monitoring data to Operations Management Suite.</span></span> <span data-ttu-id="a8271-154">在具有 OMS 直接代理程式的伺服器上，或在透過 System Center Operations Manager 管理群組連結至 Operations Management Suite 的伺服器上，您可以使用服務對應。</span><span class="sxs-lookup"><span data-stu-id="a8271-154">You can use Service Map on servers with OMS Direct Agents or on servers that are attached to Operations Management Suite via System Center Operations Manager management groups.</span></span>  

<span data-ttu-id="a8271-155">在本文中，所有代理程式 (無論 Linux 或 Windows、無論是連線到 System Center Operations Manager 管理群組或直接連線到 Operations Management Suite) 一律稱為「OMS 代理程式」。</span><span class="sxs-lookup"><span data-stu-id="a8271-155">In this article, we'll refer to all agents--whether Linux or Windows, whether connected to a System Center Operations Manager management group or directly to Operations Management Suite--as the "OMS Agent."</span></span> <span data-ttu-id="a8271-156">只有在內容需要時，我們才會使用代理程式特定的部署名稱。</span><span class="sxs-lookup"><span data-stu-id="a8271-156">We'll use the specific deployment name of the agent only if it's needed for context.</span></span>

<span data-ttu-id="a8271-157">服務對應代理程式本身不會傳輸任何資料，因此不需要變更防火牆或連接埠。</span><span class="sxs-lookup"><span data-stu-id="a8271-157">The Service Map agent does not transmit any data itself, and it does not require any changes to firewalls or ports.</span></span> <span data-ttu-id="a8271-158">服務對應的資料一律會由 OMS 代理程式 (直接或透過 OMS 閘道) 傳輸給 Operations Management Suite。</span><span class="sxs-lookup"><span data-stu-id="a8271-158">The data in Service Map is always transmitted by the OMS Agent to Operations Management Suite, either directly or via the OMS Gateway.</span></span>

![服務對應代理程式](media/oms-service-map/agents.png)

<span data-ttu-id="a8271-160">如果您是管理群組連線到 Operations Management Suite 的 System Center Operations Manager 客戶：</span><span class="sxs-lookup"><span data-stu-id="a8271-160">If you are a System Center Operations Manager customer with a management group connected to Operations Management Suite:</span></span>

- <span data-ttu-id="a8271-161">如果您的 System Center Operations Manager 代理程式可透過網際網路連線到 Operations Management Suite，就不需要額外的設定。</span><span class="sxs-lookup"><span data-stu-id="a8271-161">If your System Center Operations Manager agents can access the Internet to connect to Operations Management Suite, no additional configuration is required.</span></span>  
- <span data-ttu-id="a8271-162">如果您的 System Center Operations Manager 代理程式無法透過網際網路存取 Operations Management Suite，就必須設定 OMS 閘道以搭配 System Center Operations Manager 使用。</span><span class="sxs-lookup"><span data-stu-id="a8271-162">If your System Center Operations Manager agents cannot access Operations Management Suite over the Internet, you need to configure the OMS Gateway to work with System Center Operations Manager.</span></span>
  
<span data-ttu-id="a8271-163">如果您使用 OMS 直接代理程式，則需要將 OMS 代理程式本身設定為連線至 Operations Management Suite 或 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="a8271-163">If you are using the OMS Direct Agent, you need to configure the OMS Agent itself to connect to Operations Management Suite or to your OMS Gateway.</span></span> <span data-ttu-id="a8271-164">您可以從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=52666)下載 OMS 閘道。</span><span class="sxs-lookup"><span data-stu-id="a8271-164">The OMS Gateway can be downloaded from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=52666).</span></span>

### <a name="management-packs"></a><span data-ttu-id="a8271-165">管理組件</span><span class="sxs-lookup"><span data-stu-id="a8271-165">Management packs</span></span>
<span data-ttu-id="a8271-166">在 Operations Management Suite 工作區中啟動服務對應時，會將 300 KB 的管理組件傳送至該工作區中的所有 Windows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a8271-166">When Service Map is activated in an Operations Management Suite workspace, a 300-KB management pack is sent to all the Windows servers in that workspace.</span></span> <span data-ttu-id="a8271-167">如果您是在[連線的管理群組](../log-analytics/log-analytics-om-agents.md)中使用 System Center Operations Manager 代理程式，則會從 System Center Operations Manager 來部署服務對應管理組件。</span><span class="sxs-lookup"><span data-stu-id="a8271-167">If you are using System Center Operations Manager agents in a [connected management group](../log-analytics/log-analytics-om-agents.md), the Service Map management pack is deployed from System Center Operations Manager.</span></span> <span data-ttu-id="a8271-168">如果代理程式是直接連線，Operations Management Suite 會提供管理組件。</span><span class="sxs-lookup"><span data-stu-id="a8271-168">If the agents are directly connected, Operations Management Suite delivers the management pack.</span></span>

<span data-ttu-id="a8271-169">管理組件名稱為 Microsoft.IntelligencePacks.ApplicationDependencyMonitor。</span><span class="sxs-lookup"><span data-stu-id="a8271-169">The management pack is named Microsoft.IntelligencePacks.ApplicationDependencyMonitor.</span></span> <span data-ttu-id="a8271-170">它會寫入至 %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\。</span><span class="sxs-lookup"><span data-stu-id="a8271-170">It's written to %Programfiles%\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs\.</span></span> <span data-ttu-id="a8271-171">管理組件所使用的資料來源是 %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll。</span><span class="sxs-lookup"><span data-stu-id="a8271-171">The data source that the management pack uses is %Program files%\Microsoft Monitoring Agent\Agent\Health Service State\Resources\<AutoGeneratedID>\Microsoft.EnterpriseManagement.Advisor.ApplicationDependencyMonitorDataSource.dll.</span></span>

## <a name="installation"></a><span data-ttu-id="a8271-172">安裝</span><span class="sxs-lookup"><span data-stu-id="a8271-172">Installation</span></span>
### <a name="install-the-dependency-agent-on-microsoft-windows"></a><span data-ttu-id="a8271-173">在 Microsoft Windows 上安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-173">Install the Dependency Agent on Microsoft Windows</span></span>
<span data-ttu-id="a8271-174">必須有系統管理員權限，以便安裝或解除安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-174">Administrator privileges are required to install or uninstall the agent.</span></span>

<span data-ttu-id="a8271-175">您可以透過 InstallDependencyAgent-Windows.exe，在 Windows 電腦上安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-175">The Dependency Agent is installed on Windows computers through InstallDependencyAgent-Windows.exe.</span></span> <span data-ttu-id="a8271-176">如果您在執行此可執行檔時不使用任何選項，則會啟動以互動方式安裝的精靈。</span><span class="sxs-lookup"><span data-stu-id="a8271-176">If you run this executable file without any options, it starts a wizard that you can follow to install interactively.</span></span>  

<span data-ttu-id="a8271-177">請使用下列步驟在每一部 Windows 電腦上安裝相依性代理程式：</span><span class="sxs-lookup"><span data-stu-id="a8271-177">Use the following steps to install the Dependency Agent on each Windows computer:</span></span>

1.  <span data-ttu-id="a8271-178">依照[將 Windows 電腦連線到 Azure 中的 Log Analytics 服務](../log-analytics/log-analytics-windows-agents.md)的指示來安裝 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-178">Install the OMS Agent by using the instructions at [Connect Windows computers to the Log Analytics service in Azure](../log-analytics/log-analytics-windows-agents.md).</span></span>
2.  <span data-ttu-id="a8271-179">下載 Windows 代理程式，並以下列命令來執行：</span><span class="sxs-lookup"><span data-stu-id="a8271-179">Download the Windows agent and run it by using the following command:</span></span> <br>`InstallDependencyAgent-Windows.exe`
3.  <span data-ttu-id="a8271-180">遵循精靈來安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-180">Follow the wizard to install the agent.</span></span>
4.  <span data-ttu-id="a8271-181">如果相依性代理程式無法啟動，請檢查記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-181">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="a8271-182">在 Windows 代理程式上，記錄檔的目錄是 %Programfiles%\Microsoft Dependency Agent\logs。</span><span class="sxs-lookup"><span data-stu-id="a8271-182">On Windows agents, the log directory is %Programfiles%\Microsoft Dependency Agent\logs.</span></span> 

#### <a name="windows-command-line"></a><span data-ttu-id="a8271-183">Windows 命令列</span><span class="sxs-lookup"><span data-stu-id="a8271-183">Windows command line</span></span>
<span data-ttu-id="a8271-184">使用下表中的選項以從命令列安裝。</span><span class="sxs-lookup"><span data-stu-id="a8271-184">Use options from the following table to install from a command line.</span></span> <span data-ttu-id="a8271-185">若要查看安裝旗標的清單，請如下所示使用 /? 旗標執行安裝程式</span><span class="sxs-lookup"><span data-stu-id="a8271-185">To see a list of the installation flags, run the installer by using the /?</span></span> <span data-ttu-id="a8271-186">。</span><span class="sxs-lookup"><span data-stu-id="a8271-186">flag as follows.</span></span>

    InstallDependencyAgent-Windows.exe /?

| <span data-ttu-id="a8271-187">旗標</span><span class="sxs-lookup"><span data-stu-id="a8271-187">Flag</span></span> | <span data-ttu-id="a8271-188">說明</span><span class="sxs-lookup"><span data-stu-id="a8271-188">Description</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-189">/?</span><span class="sxs-lookup"><span data-stu-id="a8271-189">/?</span></span> | <span data-ttu-id="a8271-190">取得命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="a8271-190">Get a list of the command-line options.</span></span> |
| <span data-ttu-id="a8271-191">/S</span><span class="sxs-lookup"><span data-stu-id="a8271-191">/S</span></span> | <span data-ttu-id="a8271-192">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="a8271-192">Perform a silent installation with no user prompts.</span></span> |

<span data-ttu-id="a8271-193">Windows 相依性代理程式的檔案預設位於 C:\Program Files\Microsoft Dependency Agent。</span><span class="sxs-lookup"><span data-stu-id="a8271-193">Files for the Windows Dependency Agent are placed in C:\Program Files\Microsoft Dependency Agent by default.</span></span>

### <a name="install-the-dependency-agent-on-linux"></a><span data-ttu-id="a8271-194">在 Linux 上安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-194">Install the Dependency Agent on Linux</span></span>
<span data-ttu-id="a8271-195">必須有 root 權限，以便安裝或設定代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-195">Root access is required to install or configure the agent.</span></span>

<span data-ttu-id="a8271-196">透過 InstallDependencyAgent-Linux64.bin (具有自我解壓縮二進位檔的殼層指令碼) 即可在 Linux 電腦上安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-196">The Dependency Agent is installed on Linux computers through InstallDependencyAgent-Linux64.bin, a shell script with a self-extracting binary.</span></span> <span data-ttu-id="a8271-197">您可以使用 sh 來執行檔案，或對檔案本身新增執行權限。</span><span class="sxs-lookup"><span data-stu-id="a8271-197">You can run the file by using sh or add execute permissions to the file itself.</span></span>
 
<span data-ttu-id="a8271-198">請使用下列步驟在每一部 Linux 電腦上安裝相依性代理程式：</span><span class="sxs-lookup"><span data-stu-id="a8271-198">Use the following steps to install the Dependency Agent on each Linux computer:</span></span>

1.  <span data-ttu-id="a8271-199">依照[收集並管理來自 Linux 電腦的資料](https://technet.microsoft.com/library/mt622052.aspx)的指示來安裝 OMS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-199">Install the OMS Agent by using the instructions at [Collect and manage data from Linux computers](https://technet.microsoft.com/library/mt622052.aspx).</span></span>
2.  <span data-ttu-id="a8271-200">使用下列命令，以 root 身分安裝 Linux 相依性代理程式：</span><span class="sxs-lookup"><span data-stu-id="a8271-200">Install the Linux Dependency agent as root by using the following command:</span></span><br>`sh InstallDependencyAgent-Linux64.bin`
3.  <span data-ttu-id="a8271-201">如果相依性代理程式無法啟動，請檢查記錄檔以取得詳細的錯誤資訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-201">If the Dependency Agent fails to start, check the logs for detailed error information.</span></span> <span data-ttu-id="a8271-202">在 Linux 代理程式上，記錄檔的目錄是 /var/opt/microsoft/dependency-agent/log。</span><span class="sxs-lookup"><span data-stu-id="a8271-202">On Linux agents, the log directory is /var/opt/microsoft/dependency-agent/log.</span></span>

<span data-ttu-id="a8271-203">若要查看安裝旗標的清單，請如下所示以 -help 旗標執行安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-203">To see a list of the installation flags, run the installation program with the -help flag as follows.</span></span>

    InstallDependencyAgent-Linux64.bin -help

| <span data-ttu-id="a8271-204">旗標</span><span class="sxs-lookup"><span data-stu-id="a8271-204">Flag</span></span> | <span data-ttu-id="a8271-205">說明</span><span class="sxs-lookup"><span data-stu-id="a8271-205">Description</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-206">-help</span><span class="sxs-lookup"><span data-stu-id="a8271-206">-help</span></span> | <span data-ttu-id="a8271-207">取得命令列選項的清單。</span><span class="sxs-lookup"><span data-stu-id="a8271-207">Get a list of the command-line options.</span></span> |
| <span data-ttu-id="a8271-208">-s</span><span class="sxs-lookup"><span data-stu-id="a8271-208">-s</span></span> | <span data-ttu-id="a8271-209">執行無訊息安裝，不會出現任何使用者提示。</span><span class="sxs-lookup"><span data-stu-id="a8271-209">Perform a silent installation with no user prompts.</span></span> |
| <span data-ttu-id="a8271-210">--check</span><span class="sxs-lookup"><span data-stu-id="a8271-210">--check</span></span> | <span data-ttu-id="a8271-211">檢查權限和作業系統，但不會安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-211">Check permissions and the operating system but do not install the agent.</span></span> |

<span data-ttu-id="a8271-212">相依性代理程式的檔案位於下列目錄：</span><span class="sxs-lookup"><span data-stu-id="a8271-212">Files for the Dependency Agent are placed in the following directories:</span></span>

| <span data-ttu-id="a8271-213">檔案</span><span class="sxs-lookup"><span data-stu-id="a8271-213">Files</span></span> | <span data-ttu-id="a8271-214">位置</span><span class="sxs-lookup"><span data-stu-id="a8271-214">Location</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-215">核心檔案</span><span class="sxs-lookup"><span data-stu-id="a8271-215">Core files</span></span> | <span data-ttu-id="a8271-216">/opt/microsoft/dependency-agent</span><span class="sxs-lookup"><span data-stu-id="a8271-216">/opt/microsoft/dependency-agent</span></span> |
| <span data-ttu-id="a8271-217">記錄檔</span><span class="sxs-lookup"><span data-stu-id="a8271-217">Log files</span></span> | <span data-ttu-id="a8271-218">/var/opt/microsoft/dependency-agent/log</span><span class="sxs-lookup"><span data-stu-id="a8271-218">/var/opt/microsoft/dependency-agent/log</span></span> |
| <span data-ttu-id="a8271-219">組態檔</span><span class="sxs-lookup"><span data-stu-id="a8271-219">Config files</span></span> | <span data-ttu-id="a8271-220">/etc/opt/microsoft/dependency-agent/config</span><span class="sxs-lookup"><span data-stu-id="a8271-220">/etc/opt/microsoft/dependency-agent/config</span></span> |
| <span data-ttu-id="a8271-221">服務可執行檔</span><span class="sxs-lookup"><span data-stu-id="a8271-221">Service executable files</span></span> | <span data-ttu-id="a8271-222">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span><span class="sxs-lookup"><span data-stu-id="a8271-222">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent</span></span><br><span data-ttu-id="a8271-223">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span><span class="sxs-lookup"><span data-stu-id="a8271-223">/opt/microsoft/dependency-agent/bin/microsoft-dependency-agent-manager</span></span> |
| <span data-ttu-id="a8271-224">二進位儲存體檔案</span><span class="sxs-lookup"><span data-stu-id="a8271-224">Binary storage files</span></span> | <span data-ttu-id="a8271-225">/var/opt/microsoft/dependency-agent/storage</span><span class="sxs-lookup"><span data-stu-id="a8271-225">/var/opt/microsoft/dependency-agent/storage</span></span> |

## <a name="installation-script-examples"></a><span data-ttu-id="a8271-226">安裝指令碼範例</span><span class="sxs-lookup"><span data-stu-id="a8271-226">Installation script examples</span></span>
<span data-ttu-id="a8271-227">使用指令碼可輕鬆地一次部署許多伺服器上的相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-227">To easily deploy the Dependency Agent on many servers at once, it helps to use a script.</span></span> <span data-ttu-id="a8271-228">若要在 Windows 或 Linux 上下載並安裝相依性代理程式，可以使用下列指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="a8271-228">You can use the following script examples to download and install the Dependency Agent on either Windows or Linux.</span></span>

### <a name="powershell-script-for-windows"></a><span data-ttu-id="a8271-229">適用於 Windows 的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="a8271-229">PowerShell script for Windows</span></span>
```PowerShell
Invoke-WebRequest "https://aka.ms/dependencyagentwindows" -OutFile InstallDependencyAgent-Windows.exe

.\InstallDependencyAgent-Windows.exe /S
```

### <a name="shell-script-for-linux"></a><span data-ttu-id="a8271-230">適用於 Linux 的殼層指令碼</span><span class="sxs-lookup"><span data-stu-id="a8271-230">Shell script for Linux</span></span>
```
wget --content-disposition https://aka.ms/dependencyagentlinux -O InstallDependencyAgent-Linux64.bin
sh InstallDependencyAgent-Linux64.bin -s
```

## <a name="desired-state-configuration"></a><span data-ttu-id="a8271-231">期望的狀態設定</span><span class="sxs-lookup"><span data-stu-id="a8271-231">Desired State Configuration</span></span>
<span data-ttu-id="a8271-232">若要透過 Desired State Configuration 部署相依性代理程式，您可以使用 xPSDesiredStateConfiguration 模組和如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="a8271-232">To deploy the Dependency Agent via Desired State Configuration, you can use the xPSDesiredStateConfiguration module and a bit of code like the following:</span></span>
```
configuration ServiceMap {

Import-DscResource -ModuleName xPSDesiredStateConfiguration

$DAPackageLocalPath = "C:\InstallDependencyAgent-Windows.exe"

Node localhost
{ 
    # Download and install the Dependency Agent
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

## <a name="uninstallation"></a><span data-ttu-id="a8271-233">解除安裝</span><span class="sxs-lookup"><span data-stu-id="a8271-233">Uninstallation</span></span>
### <a name="uninstall-the-dependency-agent-on-windows"></a><span data-ttu-id="a8271-234">在 Windows 上解除安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-234">Uninstall the Dependency Agent on Windows</span></span>
<span data-ttu-id="a8271-235">系統管理員可透過控制台解除安裝 Windows 的相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-235">An administrator can uninstall the Dependency Agent for Windows through Control Panel.</span></span>

<span data-ttu-id="a8271-236">系統管理員也可以執行 %Programfiles%\Microsoft Dependency Agent\Uninstall.exe，以解除安裝相依性代理程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-236">An administrator can also run %Programfiles%\Microsoft Dependency Agent\Uninstall.exe to uninstall the Dependency Agent.</span></span>

### <a name="uninstall-the-dependency-agent-on-linux"></a><span data-ttu-id="a8271-237">在 Linux 上解除安裝相依性代理程式</span><span class="sxs-lookup"><span data-stu-id="a8271-237">Uninstall the Dependency Agent on Linux</span></span>
<span data-ttu-id="a8271-238">若要將「相依性代理程式」從 Linux 中完全解除安裝，您必須將代理程式本身及隨代理程式自動安裝的連接器移除。</span><span class="sxs-lookup"><span data-stu-id="a8271-238">To completely uninstall the Dependency Agent from Linux, you must remove the agent itself and the connector, which is installed automatically with the agent.</span></span> <span data-ttu-id="a8271-239">您可以使用下列單一命令同時解除安裝這兩者：</span><span class="sxs-lookup"><span data-stu-id="a8271-239">You can uninstall both by using the following single command:</span></span>

    rpm -e dependency-agent dependency-agent-connector

## <a name="troubleshooting"></a><span data-ttu-id="a8271-240">疑難排解</span><span class="sxs-lookup"><span data-stu-id="a8271-240">Troubleshooting</span></span>
<span data-ttu-id="a8271-241">如果您在安裝或執行服務對應時遇到任何問題，本節內容可以提供協助。</span><span class="sxs-lookup"><span data-stu-id="a8271-241">If you have any problems installing or running Service Map, this section can help you.</span></span> <span data-ttu-id="a8271-242">如果您仍然無法解決問題，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="a8271-242">If you still can't resolve your problem, please contact Microsoft Support.</span></span>

### <a name="dependency-agent-installation-problems"></a><span data-ttu-id="a8271-243">相依性代理程式安裝問題</span><span class="sxs-lookup"><span data-stu-id="a8271-243">Dependency Agent installation problems</span></span>
#### <a name="installer-asks-for-a-reboot"></a><span data-ttu-id="a8271-244">安裝程式會要求重新開機</span><span class="sxs-lookup"><span data-stu-id="a8271-244">Installer asks for a reboot</span></span>
<span data-ttu-id="a8271-245">相依性代理程式*通常*不需要在安裝或解除安裝之後重新開機。</span><span class="sxs-lookup"><span data-stu-id="a8271-245">The Dependency Agent *generally* does not require a reboot upon installation or uninstallation.</span></span> <span data-ttu-id="a8271-246">不過，在某些罕見情況下，Windows Server 需要重新開機，才能繼續進行安裝。</span><span class="sxs-lookup"><span data-stu-id="a8271-246">However, in certain rare cases, Windows Server requires a reboot to continue with an installation.</span></span> <span data-ttu-id="a8271-247">這會在相依性 (通常是 Microsoft Visual C++ 可轉散發套件) 因為鎖定的檔案而需要重新開機時發生。</span><span class="sxs-lookup"><span data-stu-id="a8271-247">This happens when a dependency, usually the Microsoft Visual C++ Redistributable, requires a reboot because of a locked file.</span></span>

#### <a name="message-unable-to-install-dependency-agent-visual-studio-runtime-libraries-failed-to-install-code--codenumber-appears"></a><span data-ttu-id="a8271-248">顯示「無法安裝相依性代理程式︰無法安裝 Visual Studio 執行階段程式庫 (程式碼 = [code_number])」訊息</span><span class="sxs-lookup"><span data-stu-id="a8271-248">Message "Unable to install Dependency Agent: Visual Studio Runtime libraries failed to install (code = [code_number])" appears</span></span>

<span data-ttu-id="a8271-249">Microsoft 相依性代理程式建置於 Microsoft Visual Studio 執行階段程式庫之上。</span><span class="sxs-lookup"><span data-stu-id="a8271-249">The Microsoft Dependency Agent is built on the Microsoft Visual Studio runtime libraries.</span></span> <span data-ttu-id="a8271-250">如果程式庫安裝期間發生問題，就會出現訊息。</span><span class="sxs-lookup"><span data-stu-id="a8271-250">You'll get a message if there's a problem during installation of the libraries.</span></span> 

<span data-ttu-id="a8271-251">執行階段程式庫安裝程式會在 %LOCALAPPDATA%\temp 資料夾中建立記錄。</span><span class="sxs-lookup"><span data-stu-id="a8271-251">The runtime library installers create logs in the %LOCALAPPDATA%\temp folder.</span></span> <span data-ttu-id="a8271-252">檔案將會是 dd_vcredist_arch_yyyymmddhhmmss.log，其中 *arch* 是 "x86" 或 "amd64"，*yyyymmddhhmmss* 是建立記錄的日期和時間 (24 小時制)。</span><span class="sxs-lookup"><span data-stu-id="a8271-252">The file is dd_vcredist_arch_yyyymmddhhmmss.log, where *arch* is "x86" or "amd64" and *yyyymmddhhmmss* is the date and time (24-hour clock) when the log was created.</span></span> <span data-ttu-id="a8271-253">記錄會提供導致無法安裝之問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-253">The log provides details about the problem that's blocking installation.</span></span>

<span data-ttu-id="a8271-254">如果可以先自行安裝[最新的執行階段程式庫](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)，將會十分有用。</span><span class="sxs-lookup"><span data-stu-id="a8271-254">It might be useful to install the [latest runtime libraries](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) yourself first.</span></span>

<span data-ttu-id="a8271-255">下表列出代碼和建議的解決方式。</span><span class="sxs-lookup"><span data-stu-id="a8271-255">The following table lists code numbers and suggested resolutions.</span></span>

| <span data-ttu-id="a8271-256">代碼</span><span class="sxs-lookup"><span data-stu-id="a8271-256">Code</span></span> | <span data-ttu-id="a8271-257">說明</span><span class="sxs-lookup"><span data-stu-id="a8271-257">Description</span></span> | <span data-ttu-id="a8271-258">解決方案</span><span class="sxs-lookup"><span data-stu-id="a8271-258">Resolution</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a8271-259">0x17</span><span class="sxs-lookup"><span data-stu-id="a8271-259">0x17</span></span> | <span data-ttu-id="a8271-260">程式庫安裝程式會要求尚未安裝的 Windows 更新。</span><span class="sxs-lookup"><span data-stu-id="a8271-260">The library installer requires a Windows update that hasn't been installed.</span></span> | <span data-ttu-id="a8271-261">查看最新的程式庫安裝程式記錄。</span><span class="sxs-lookup"><span data-stu-id="a8271-261">Look in the most recent library installer log.</span></span><br><br><span data-ttu-id="a8271-262">如果提到 "Windows8.1-KB2999226-x64.msu"，隨後一行是 "Error 0x80240017: Failed to execute MSU package"，則表示您尚未具備安裝 KB2999226 所需的必要條件。</span><span class="sxs-lookup"><span data-stu-id="a8271-262">If a reference to "Windows8.1-KB2999226-x64.msu" is followed by a line "Error 0x80240017: Failed to execute MSU package," you don't have the prerequisites to install KB2999226.</span></span> <span data-ttu-id="a8271-263">請依照 [Windows 中的通用 C 執行階段](https://support.microsoft.com/kb/2999226) \(機器翻譯\) 中必要條件一節的指示進行。</span><span class="sxs-lookup"><span data-stu-id="a8271-263">Follow the instructions in the prerequisites section in [Universal C Runtime in Windows](https://support.microsoft.com/kb/2999226).</span></span> <span data-ttu-id="a8271-264">您可能需要執行 Windows Update 並重新開機多次，才能安裝必要條件。</span><span class="sxs-lookup"><span data-stu-id="a8271-264">You might need to run Windows Update and reboot multiple times in order to install the prerequisites.</span></span><br><br><span data-ttu-id="a8271-265">再次執行 Microsoft 相依性代理程式安裝程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-265">Run the Microsoft Dependency Agent installer again.</span></span> |

### <a name="post-installation-issues"></a><span data-ttu-id="a8271-266">安裝後問題</span><span class="sxs-lookup"><span data-stu-id="a8271-266">Post-installation issues</span></span>
#### <a name="server-doesnt-appear-in-service-map"></a><span data-ttu-id="a8271-267">伺服器未出現在服務對應中</span><span class="sxs-lookup"><span data-stu-id="a8271-267">Server doesn't appear in Service Map</span></span>
<span data-ttu-id="a8271-268">如果相依性代理程式安裝成功，但是在服務對應解決方案中沒有看到您的伺服器︰</span><span class="sxs-lookup"><span data-stu-id="a8271-268">If your Dependency Agent installation succeeded, but you don't see your server in the Service Map solution:</span></span>
* <span data-ttu-id="a8271-269">相依性代理程式是否安裝成功？</span><span class="sxs-lookup"><span data-stu-id="a8271-269">Is the Dependency Agent installed successfully?</span></span> <span data-ttu-id="a8271-270">您可以查看是否已安裝服務並且執行，以便驗證。</span><span class="sxs-lookup"><span data-stu-id="a8271-270">You can validate this by checking to see if the service is installed and running.</span></span><br><br><span data-ttu-id="a8271-271">
**Windows**︰尋找名稱為「Microsoft 相依性代理程式」的服務。</span><span class="sxs-lookup"><span data-stu-id="a8271-271">
**Windows**: Look for the service named "Microsoft Dependency Agent."</span></span><br><span data-ttu-id="a8271-272">
**Linux**：尋找執行中的處理序 "microsoft-dependency-agent"。</span><span class="sxs-lookup"><span data-stu-id="a8271-272">
**Linux**: Look for the running process "microsoft-dependency-agent."</span></span>

* <span data-ttu-id="a8271-273">您是否屬於 [Operations Management Suite/Log Analytics 的免費定價層](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)？</span><span class="sxs-lookup"><span data-stu-id="a8271-273">Are you on the [Free pricing tier of Operations Management Suite/Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers)?</span></span> <span data-ttu-id="a8271-274">免費方案允許最多五個唯一的服務對應伺服器。</span><span class="sxs-lookup"><span data-stu-id="a8271-274">The Free plan allows for up to five unique Service Map servers.</span></span> <span data-ttu-id="a8271-275">任何後續伺服器則不會顯示在服務對應中，即使先前五個伺服器不會再傳送資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-275">Any subsequent servers won't show up in Service Map, even if the prior five are no longer sending data.</span></span>

* <span data-ttu-id="a8271-276">您的伺服器是否將記錄和效能資料傳送到 Operations Management Suite？</span><span class="sxs-lookup"><span data-stu-id="a8271-276">Is your server sending log and perf data to Operations Management Suite?</span></span> <span data-ttu-id="a8271-277">移至 [記錄搜尋]，然後為您的電腦執行下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="a8271-277">Go to Log Search and run the following query for your computer:</span></span> 

        * Computer="<your computer name here>" | measure count() by Type
        
  <span data-ttu-id="a8271-278">您是否在結果中取得各種事件？</span><span class="sxs-lookup"><span data-stu-id="a8271-278">Did you get a variety of events in the results?</span></span> <span data-ttu-id="a8271-279">是否為最新的資料？</span><span class="sxs-lookup"><span data-stu-id="a8271-279">Is the data recent?</span></span> <span data-ttu-id="a8271-280">如果是，表示 OMS 代理程式運作正常，並且可與 Operations Management Suite 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-280">If so, your OMS Agent is operating correctly and communicating with the Operations Management Suite service.</span></span> <span data-ttu-id="a8271-281">如果不是，請檢查您伺服器上的 OMS 代理程式︰[適用於 Windows 的 OMS 代理程式疑難排解](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues)或[適用於 Linux 的 OMS 代理程式疑難排解](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="a8271-281">If not, check the OMS Agent on your server: [OMS Agent for Windows troubleshooting](https://support.microsoft.com/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues) or [OMS Agent for Linux troubleshooting](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md).</span></span>

#### <a name="server-appears-in-service-map-but-has-no-processes"></a><span data-ttu-id="a8271-282">伺服器顯示在服務對應中，但是沒有任何處理序</span><span class="sxs-lookup"><span data-stu-id="a8271-282">Server appears in Service Map but has no processes</span></span>
<span data-ttu-id="a8271-283">如果在服務對應中看到您的伺服器，但是沒有處理序或連線資料，則表示相依性代理程式已安裝且正在執行，但未載入核心驅動程式。</span><span class="sxs-lookup"><span data-stu-id="a8271-283">If you see your server in Service Map, but it has no process or connection data, that indicates that the Dependency Agent is installed and running, but the kernel driver didn't load.</span></span> 

<span data-ttu-id="a8271-284">請檢查 C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log file (Windows) 檔案或 /var/opt/microsoft/dependency-agent/log/service.log 檔案 (Linux)。</span><span class="sxs-lookup"><span data-stu-id="a8271-284">Check the C:\Program Files\Microsoft Dependency Agent\logs\wrapper.log file (Windows) or /var/opt/microsoft/dependency-agent/log/service.log file (Linux).</span></span> <span data-ttu-id="a8271-285">檔案的最後幾行應該會指出未載入核心的原因。</span><span class="sxs-lookup"><span data-stu-id="a8271-285">The last lines of the file should indicate why the kernel didn't load.</span></span> <span data-ttu-id="a8271-286">例如，若您更新過核心，在 Linux 上可能會不受支援。</span><span class="sxs-lookup"><span data-stu-id="a8271-286">For example, the kernel might not be supported on Linux if you updated your kernel.</span></span>

## <a name="data-collection"></a><span data-ttu-id="a8271-287">資料收集</span><span class="sxs-lookup"><span data-stu-id="a8271-287">Data collection</span></span>
<span data-ttu-id="a8271-288">視系統相依性的複雜程度而定，每個代理程式每天預計會傳輸大約 25 MB。</span><span class="sxs-lookup"><span data-stu-id="a8271-288">You can expect each agent to transmit roughly 25 MB per day, depending on how complex your system dependencies are.</span></span> <span data-ttu-id="a8271-289">每個代理程式每隔 15 秒就會傳送服務對應相依性資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-289">Each agent sends Service Map dependency data every 15 seconds.</span></span>  

<span data-ttu-id="a8271-290">相依性代理程式一般會耗用 0.1% 的系統記憶體和 0.1% 的系統 CPU。</span><span class="sxs-lookup"><span data-stu-id="a8271-290">The Dependency Agent typically consumes 0.1 percent of system memory and 0.1 percent of system CPU.</span></span>

## <a name="supported-azure-regions"></a><span data-ttu-id="a8271-291">支援的 Azure 區域</span><span class="sxs-lookup"><span data-stu-id="a8271-291">Supported Azure regions</span></span>
<span data-ttu-id="a8271-292">服務對應目前已在以下 Azure 區域中推出：</span><span class="sxs-lookup"><span data-stu-id="a8271-292">Service Map is currently available in the following Azure regions:</span></span>
- <span data-ttu-id="a8271-293">美國東部</span><span class="sxs-lookup"><span data-stu-id="a8271-293">East US</span></span>
- <span data-ttu-id="a8271-294">西歐</span><span class="sxs-lookup"><span data-stu-id="a8271-294">West Europe</span></span>
- <span data-ttu-id="a8271-295">美國中西部</span><span class="sxs-lookup"><span data-stu-id="a8271-295">West Central US</span></span>


## <a name="supported-operating-systems"></a><span data-ttu-id="a8271-296">受支援的作業系統</span><span class="sxs-lookup"><span data-stu-id="a8271-296">Supported operating systems</span></span>
<span data-ttu-id="a8271-297">下列幾節會列出相依性代理程式所支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a8271-297">The following sections list the supported operating systems for the Dependency Agent.</span></span> <span data-ttu-id="a8271-298">服務對應不支援任何 32 位元架構的作業系統。</span><span class="sxs-lookup"><span data-stu-id="a8271-298">Service Map doesn't support 32-bit architectures for any operating system.</span></span>

### <a name="windows-server"></a><span data-ttu-id="a8271-299">Windows Server</span><span class="sxs-lookup"><span data-stu-id="a8271-299">Windows Server</span></span>
- <span data-ttu-id="a8271-300">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a8271-300">Windows Server 2016</span></span>
- <span data-ttu-id="a8271-301">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a8271-301">Windows Server 2012 R2</span></span>
- <span data-ttu-id="a8271-302">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a8271-302">Windows Server 2012</span></span>
- <span data-ttu-id="a8271-303">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="a8271-303">Windows Server 2008 R2 SP1</span></span>

### <a name="windows-desktop"></a><span data-ttu-id="a8271-304">Windows 桌面</span><span class="sxs-lookup"><span data-stu-id="a8271-304">Windows desktop</span></span>
- <span data-ttu-id="a8271-305">Windows 10</span><span class="sxs-lookup"><span data-stu-id="a8271-305">Windows 10</span></span>
- <span data-ttu-id="a8271-306">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a8271-306">Windows 8.1</span></span>
- <span data-ttu-id="a8271-307">Windows 8</span><span class="sxs-lookup"><span data-stu-id="a8271-307">Windows 8</span></span>
- <span data-ttu-id="a8271-308">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a8271-308">Windows 7</span></span>

### <a name="red-hat-enterprise-linux-centos-linux-and-oracle-linux-with-rhel-kernel"></a><span data-ttu-id="a8271-309">Red Hat Enterprise Linux、CentOS Linux 和 Oracle Linux (搭載 RHEL 核心)</span><span class="sxs-lookup"><span data-stu-id="a8271-309">Red Hat Enterprise Linux, CentOS Linux, and Oracle Linux (with RHEL Kernel)</span></span>
- <span data-ttu-id="a8271-310">只支援預設版本和 SMP Linux 核心版本。</span><span class="sxs-lookup"><span data-stu-id="a8271-310">Only default and SMP Linux kernel releases are supported.</span></span>
- <span data-ttu-id="a8271-311">所有 Linux 散發套件皆不支援非標準的核心版本 (例如 PAE 和 Xen)。</span><span class="sxs-lookup"><span data-stu-id="a8271-311">Nonstandard kernel releases, such as PAE and Xen, are not supported for any Linux distribution.</span></span> <span data-ttu-id="a8271-312">舉例來說，版本字串為「2.6.16.21-0.8-xen」的系統就不受支援。</span><span class="sxs-lookup"><span data-stu-id="a8271-312">For example, a system with the release string of "2.6.16.21-0.8-xen" is not supported.</span></span>
- <span data-ttu-id="a8271-313">不支援自訂核心，包括重新編譯的標準核心。</span><span class="sxs-lookup"><span data-stu-id="a8271-313">Custom kernels, including recompiles of standard kernels, are not supported.</span></span>
- <span data-ttu-id="a8271-314">不支援 CentOSPlus 核心。</span><span class="sxs-lookup"><span data-stu-id="a8271-314">CentOSPlus kernel is not supported.</span></span>
- <span data-ttu-id="a8271-315">Oracle Unbreakable Enterprise Kernel (UEK) 在本文稍後的章節有相關討論。</span><span class="sxs-lookup"><span data-stu-id="a8271-315">Oracle Unbreakable Enterprise Kernel (UEK) is covered in a later section of this article.</span></span>


#### <a name="red-hat-linux-7"></a><span data-ttu-id="a8271-316">Red Hat Linux 7</span><span class="sxs-lookup"><span data-stu-id="a8271-316">Red Hat Linux 7</span></span>
| <span data-ttu-id="a8271-317">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-317">OS version</span></span> | <span data-ttu-id="a8271-318">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-318">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-319">7.0</span><span class="sxs-lookup"><span data-stu-id="a8271-319">7.0</span></span> | <span data-ttu-id="a8271-320">3.10.0-123</span><span class="sxs-lookup"><span data-stu-id="a8271-320">3.10.0-123</span></span> |
| <span data-ttu-id="a8271-321">7.1</span><span class="sxs-lookup"><span data-stu-id="a8271-321">7.1</span></span> | <span data-ttu-id="a8271-322">3.10.0-229</span><span class="sxs-lookup"><span data-stu-id="a8271-322">3.10.0-229</span></span> |
| <span data-ttu-id="a8271-323">7.2</span><span class="sxs-lookup"><span data-stu-id="a8271-323">7.2</span></span> | <span data-ttu-id="a8271-324">3.10.0-327</span><span class="sxs-lookup"><span data-stu-id="a8271-324">3.10.0-327</span></span> |
| <span data-ttu-id="a8271-325">7.3</span><span class="sxs-lookup"><span data-stu-id="a8271-325">7.3</span></span> | <span data-ttu-id="a8271-326">3.10.0-514</span><span class="sxs-lookup"><span data-stu-id="a8271-326">3.10.0-514</span></span> |

#### <a name="red-hat-linux-6"></a><span data-ttu-id="a8271-327">Red Hat Linux 6</span><span class="sxs-lookup"><span data-stu-id="a8271-327">Red Hat Linux 6</span></span>
| <span data-ttu-id="a8271-328">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-328">OS version</span></span> | <span data-ttu-id="a8271-329">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-329">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-330">6.0</span><span class="sxs-lookup"><span data-stu-id="a8271-330">6.0</span></span> | <span data-ttu-id="a8271-331">2.6.32-71</span><span class="sxs-lookup"><span data-stu-id="a8271-331">2.6.32-71</span></span> |
| <span data-ttu-id="a8271-332">6.1</span><span class="sxs-lookup"><span data-stu-id="a8271-332">6.1</span></span> | <span data-ttu-id="a8271-333">2.6.32-131</span><span class="sxs-lookup"><span data-stu-id="a8271-333">2.6.32-131</span></span> |
| <span data-ttu-id="a8271-334">6.2</span><span class="sxs-lookup"><span data-stu-id="a8271-334">6.2</span></span> | <span data-ttu-id="a8271-335">2.6.32-220</span><span class="sxs-lookup"><span data-stu-id="a8271-335">2.6.32-220</span></span> |
| <span data-ttu-id="a8271-336">6.3</span><span class="sxs-lookup"><span data-stu-id="a8271-336">6.3</span></span> | <span data-ttu-id="a8271-337">2.6.32-279</span><span class="sxs-lookup"><span data-stu-id="a8271-337">2.6.32-279</span></span> |
| <span data-ttu-id="a8271-338">6.4</span><span class="sxs-lookup"><span data-stu-id="a8271-338">6.4</span></span> | <span data-ttu-id="a8271-339">2.6.32-358</span><span class="sxs-lookup"><span data-stu-id="a8271-339">2.6.32-358</span></span> |
| <span data-ttu-id="a8271-340">6.5</span><span class="sxs-lookup"><span data-stu-id="a8271-340">6.5</span></span> | <span data-ttu-id="a8271-341">2.6.32-431</span><span class="sxs-lookup"><span data-stu-id="a8271-341">2.6.32-431</span></span> |
| <span data-ttu-id="a8271-342">6.6</span><span class="sxs-lookup"><span data-stu-id="a8271-342">6.6</span></span> | <span data-ttu-id="a8271-343">2.6.32-504</span><span class="sxs-lookup"><span data-stu-id="a8271-343">2.6.32-504</span></span> |
| <span data-ttu-id="a8271-344">6.7</span><span class="sxs-lookup"><span data-stu-id="a8271-344">6.7</span></span> | <span data-ttu-id="a8271-345">2.6.32-573</span><span class="sxs-lookup"><span data-stu-id="a8271-345">2.6.32-573</span></span> |
| <span data-ttu-id="a8271-346">6.8</span><span class="sxs-lookup"><span data-stu-id="a8271-346">6.8</span></span> | <span data-ttu-id="a8271-347">2.6.32-642</span><span class="sxs-lookup"><span data-stu-id="a8271-347">2.6.32-642</span></span> |

#### <a name="red-hat-linux-5"></a><span data-ttu-id="a8271-348">Red Hat Linux 5</span><span class="sxs-lookup"><span data-stu-id="a8271-348">Red Hat Linux 5</span></span>
| <span data-ttu-id="a8271-349">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-349">OS version</span></span> | <span data-ttu-id="a8271-350">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-350">Kernel version</span></span> |
|:--|:--|
| <span data-ttu-id="a8271-351">5.8</span><span class="sxs-lookup"><span data-stu-id="a8271-351">5.8</span></span> | <span data-ttu-id="a8271-352">2.6.18-308</span><span class="sxs-lookup"><span data-stu-id="a8271-352">2.6.18-308</span></span> |
| <span data-ttu-id="a8271-353">5.9</span><span class="sxs-lookup"><span data-stu-id="a8271-353">5.9</span></span> | <span data-ttu-id="a8271-354">2.6.18-348</span><span class="sxs-lookup"><span data-stu-id="a8271-354">2.6.18-348</span></span> |
| <span data-ttu-id="a8271-355">5.10</span><span class="sxs-lookup"><span data-stu-id="a8271-355">5.10</span></span> | <span data-ttu-id="a8271-356">2.6.18-371</span><span class="sxs-lookup"><span data-stu-id="a8271-356">2.6.18-371</span></span> |
| <span data-ttu-id="a8271-357">5.11</span><span class="sxs-lookup"><span data-stu-id="a8271-357">5.11</span></span> | <span data-ttu-id="a8271-358">2.6.18-398</span><span class="sxs-lookup"><span data-stu-id="a8271-358">2.6.18-398</span></span><br><span data-ttu-id="a8271-359">2.6.18-400</span><span class="sxs-lookup"><span data-stu-id="a8271-359">2.6.18-400</span></span><br><span data-ttu-id="a8271-360">2.6.18-402</span><span class="sxs-lookup"><span data-stu-id="a8271-360">2.6.18-402</span></span><br><span data-ttu-id="a8271-361">2.6.18-404</span><span class="sxs-lookup"><span data-stu-id="a8271-361">2.6.18-404</span></span><br><span data-ttu-id="a8271-362">2.6.18-406</span><span class="sxs-lookup"><span data-stu-id="a8271-362">2.6.18-406</span></span><br><span data-ttu-id="a8271-363">2.6.18-407</span><span class="sxs-lookup"><span data-stu-id="a8271-363">2.6.18-407</span></span><br><span data-ttu-id="a8271-364">2.6.18-408</span><span class="sxs-lookup"><span data-stu-id="a8271-364">2.6.18-408</span></span><br><span data-ttu-id="a8271-365">2.6.18-409</span><span class="sxs-lookup"><span data-stu-id="a8271-365">2.6.18-409</span></span><br><span data-ttu-id="a8271-366">2.6.18-410</span><span class="sxs-lookup"><span data-stu-id="a8271-366">2.6.18-410</span></span><br><span data-ttu-id="a8271-367">2.6.18-411</span><span class="sxs-lookup"><span data-stu-id="a8271-367">2.6.18-411</span></span><br><span data-ttu-id="a8271-368">2.6.18-412</span><span class="sxs-lookup"><span data-stu-id="a8271-368">2.6.18-412</span></span><br><span data-ttu-id="a8271-369">2.6.18-416</span><span class="sxs-lookup"><span data-stu-id="a8271-369">2.6.18-416</span></span><br><span data-ttu-id="a8271-370">2.6.18-417</span><span class="sxs-lookup"><span data-stu-id="a8271-370">2.6.18-417</span></span><br><span data-ttu-id="a8271-371">2.6.18-419</span><span class="sxs-lookup"><span data-stu-id="a8271-371">2.6.18-419</span></span> |

#### <a name="oracle-enterprise-linux-with-unbreakable-enterprise-kernel"></a><span data-ttu-id="a8271-372">Oracle Enterprise Linux 搭載 Unbreakable Enterprise Kernel</span><span class="sxs-lookup"><span data-stu-id="a8271-372">Oracle Enterprise Linux with Unbreakable Enterprise Kernel</span></span>

#### <a name="oracle-linux-6"></a><span data-ttu-id="a8271-373">Oracle Linux 6</span><span class="sxs-lookup"><span data-stu-id="a8271-373">Oracle Linux 6</span></span>
| <span data-ttu-id="a8271-374">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-374">OS version</span></span> | <span data-ttu-id="a8271-375">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-375">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="a8271-376">6.2</span><span class="sxs-lookup"><span data-stu-id="a8271-376">6.2</span></span> | <span data-ttu-id="a8271-377">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="a8271-377">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="a8271-378">6.3</span><span class="sxs-lookup"><span data-stu-id="a8271-378">6.3</span></span> | <span data-ttu-id="a8271-379">Oracle 2.6.39-200 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="a8271-379">Oracle 2.6.39-200 (UEK R2)</span></span> |
| <span data-ttu-id="a8271-380">6.4</span><span class="sxs-lookup"><span data-stu-id="a8271-380">6.4</span></span> | <span data-ttu-id="a8271-381">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="a8271-381">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="a8271-382">6.5</span><span class="sxs-lookup"><span data-stu-id="a8271-382">6.5</span></span> | <span data-ttu-id="a8271-383">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="a8271-383">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |
| <span data-ttu-id="a8271-384">6.6</span><span class="sxs-lookup"><span data-stu-id="a8271-384">6.6</span></span> | <span data-ttu-id="a8271-385">Oracle 2.6.39-400 (UEK R2 i386)</span><span class="sxs-lookup"><span data-stu-id="a8271-385">Oracle 2.6.39-400 (UEK R2 i386)</span></span> |

#### <a name="oracle-linux-5"></a><span data-ttu-id="a8271-386">Oracle Linux 5</span><span class="sxs-lookup"><span data-stu-id="a8271-386">Oracle Linux 5</span></span>

| <span data-ttu-id="a8271-387">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-387">OS version</span></span> | <span data-ttu-id="a8271-388">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-388">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="a8271-389">5.8</span><span class="sxs-lookup"><span data-stu-id="a8271-389">5.8</span></span> | <span data-ttu-id="a8271-390">Oracle 2.6.32-300 (UEK R1)</span><span class="sxs-lookup"><span data-stu-id="a8271-390">Oracle 2.6.32-300 (UEK R1)</span></span> |
| <span data-ttu-id="a8271-391">5.9</span><span class="sxs-lookup"><span data-stu-id="a8271-391">5.9</span></span> | <span data-ttu-id="a8271-392">Oracle 2.6.39-300 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="a8271-392">Oracle 2.6.39-300 (UEK R2)</span></span> |
| <span data-ttu-id="a8271-393">5.10</span><span class="sxs-lookup"><span data-stu-id="a8271-393">5.10</span></span> | <span data-ttu-id="a8271-394">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="a8271-394">Oracle 2.6.39-400 (UEK R2)</span></span> |
| <span data-ttu-id="a8271-395">5.11</span><span class="sxs-lookup"><span data-stu-id="a8271-395">5.11</span></span> | <span data-ttu-id="a8271-396">Oracle 2.6.39-400 (UEK R2)</span><span class="sxs-lookup"><span data-stu-id="a8271-396">Oracle 2.6.39-400 (UEK R2)</span></span> |

#### <a name="suse-linux-enterprise-server"></a><span data-ttu-id="a8271-397">SUSE Linux Enterprise Server</span><span class="sxs-lookup"><span data-stu-id="a8271-397">SUSE Linux Enterprise Server</span></span>

#### <a name="suse-linux-11"></a><span data-ttu-id="a8271-398">SUSE Linux 11</span><span class="sxs-lookup"><span data-stu-id="a8271-398">SUSE Linux 11</span></span>
| <span data-ttu-id="a8271-399">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-399">OS version</span></span> | <span data-ttu-id="a8271-400">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-400">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="a8271-401">11</span><span class="sxs-lookup"><span data-stu-id="a8271-401">11</span></span> | <span data-ttu-id="a8271-402">2.6.27</span><span class="sxs-lookup"><span data-stu-id="a8271-402">2.6.27</span></span> |
| <span data-ttu-id="a8271-403">11 SP1</span><span class="sxs-lookup"><span data-stu-id="a8271-403">11 SP1</span></span> | <span data-ttu-id="a8271-404">2.6.32</span><span class="sxs-lookup"><span data-stu-id="a8271-404">2.6.32</span></span> |
| <span data-ttu-id="a8271-405">11 SP2</span><span class="sxs-lookup"><span data-stu-id="a8271-405">11 SP2</span></span> | <span data-ttu-id="a8271-406">3.0.13</span><span class="sxs-lookup"><span data-stu-id="a8271-406">3.0.13</span></span> |
| <span data-ttu-id="a8271-407">11 SP3</span><span class="sxs-lookup"><span data-stu-id="a8271-407">11 SP3</span></span> | <span data-ttu-id="a8271-408">3.0.76</span><span class="sxs-lookup"><span data-stu-id="a8271-408">3.0.76</span></span> |
| <span data-ttu-id="a8271-409">11 SP4</span><span class="sxs-lookup"><span data-stu-id="a8271-409">11 SP4</span></span> | <span data-ttu-id="a8271-410">3.0.101</span><span class="sxs-lookup"><span data-stu-id="a8271-410">3.0.101</span></span> |

#### <a name="suse-linux-10"></a><span data-ttu-id="a8271-411">SUSE Linux 10</span><span class="sxs-lookup"><span data-stu-id="a8271-411">SUSE Linux 10</span></span>
| <span data-ttu-id="a8271-412">作業系統版本</span><span class="sxs-lookup"><span data-stu-id="a8271-412">OS version</span></span> | <span data-ttu-id="a8271-413">核心版本</span><span class="sxs-lookup"><span data-stu-id="a8271-413">Kernel version</span></span>
|:--|:--|
| <span data-ttu-id="a8271-414">10 SP4</span><span class="sxs-lookup"><span data-stu-id="a8271-414">10 SP4</span></span> | <span data-ttu-id="a8271-415">2.6.16.60</span><span class="sxs-lookup"><span data-stu-id="a8271-415">2.6.16.60</span></span> |

## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="a8271-416">診斷和使用量資料</span><span class="sxs-lookup"><span data-stu-id="a8271-416">Diagnostic and usage data</span></span>
<span data-ttu-id="a8271-417">當您使用服務對應服務時，Microsoft 會自動收集使用量和效能資料。</span><span class="sxs-lookup"><span data-stu-id="a8271-417">Microsoft automatically collects usage and performance data through your use of the Service Map service.</span></span> <span data-ttu-id="a8271-418">Microsoft 使用這項資料來提供和改進服務對應服務的品質、安全性和完整性。</span><span class="sxs-lookup"><span data-stu-id="a8271-418">Microsoft uses this data to provide and improve the quality, security, and integrity of the Service Map service.</span></span> <span data-ttu-id="a8271-419">這項資料包含軟體組態 (如作業系統和版本) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-419">Data includes information about the configuration of your software, like operating system and version.</span></span> <span data-ttu-id="a8271-420">它也會包含 IP 位址、DNS 名稱和工作站名稱，以便能夠正確且有效率地進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="a8271-420">It also includes IP address, DNS name, and workstation name in order to provide accurate and efficient troubleshooting capabilities.</span></span> <span data-ttu-id="a8271-421">我們不會收集姓名、地址或其他連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="a8271-421">We do not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="a8271-422">如需有關資料收集與使用方式的詳細資訊，請參閱 [Microsoft 線上服務隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=512132)。</span><span class="sxs-lookup"><span data-stu-id="a8271-422">For more information on data collection and usage, see the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>



## <a name="next-steps"></a><span data-ttu-id="a8271-423">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8271-423">Next steps</span></span>
- <span data-ttu-id="a8271-424">部署和設定後，了解如何[使用服務對應](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="a8271-424">Learn how to [use Service Map](operations-management-suite-service-map.md) after it has been deployed and configured.</span></span>
