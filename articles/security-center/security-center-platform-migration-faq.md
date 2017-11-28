---
title: "aaaSecurity Center 平台移轉常見問題集 |Microsoft 文件"
description: "此常見問題集解答 hello Azure 資訊安全中心平台移轉有關的問題。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a><span data-ttu-id="0fedc-103">資訊安全中心平台移轉常見問題集</span><span class="sxs-lookup"><span data-stu-id="0fedc-103">Security Center platform migration FAQ</span></span>
<span data-ttu-id="0fedc-104">Azure 資訊安全中心早期年 6 月 2017，開始使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。</span><span class="sxs-lookup"><span data-stu-id="0fedc-104">In early June 2017, Azure Security Center began using hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="0fedc-105">詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉](security-center-platform-migration.md)。</span><span class="sxs-lookup"><span data-stu-id="0fedc-105">toolearn more, see [Azure Security Center Platform Migration](security-center-platform-migration.md).</span></span> <span data-ttu-id="0fedc-106">此常見問題集解答 hello 平台移轉有關的問題。</span><span class="sxs-lookup"><span data-stu-id="0fedc-106">This FAQ answers questions about hello platform migration.</span></span>

## <a name="data-collection-agents-and-workspaces"></a><span data-ttu-id="0fedc-107">資料收集、代理程式及工作區</span><span class="sxs-lookup"><span data-stu-id="0fedc-107">Data collection, agents, and workspaces</span></span>

### <a name="how-is-data-collected"></a><span data-ttu-id="0fedc-108">資料如何收集？</span><span class="sxs-lookup"><span data-stu-id="0fedc-108">How is data collected?</span></span>
<span data-ttu-id="0fedc-109">資訊安全中心會使用您的 Vm 所傳來 hello Microsoft Monitoring Agent toocollect 安全性資料。</span><span class="sxs-lookup"><span data-stu-id="0fedc-109">Security Center uses hello Microsoft Monitoring Agent toocollect security data from your VMs.</span></span> <span data-ttu-id="0fedc-110">hello 安全性資料包含有關安全性組態，也就是使用的 tooidentify 弱點，以及安全性事件，也就是使用的 toodetect 威脅的資訊。</span><span class="sxs-lookup"><span data-stu-id="0fedc-110">hello security data includes information about security configurations, which are used tooidentify vulnerabilities, and security events, which are used toodetect threats.</span></span> <span data-ttu-id="0fedc-111">Hello 代理程式所收集的資料會儲存在現有的記錄分析工作區連線 toohello VM 或新的資訊安全中心所建立的工作區中。</span><span class="sxs-lookup"><span data-stu-id="0fedc-111">Data collected by hello agent is stored in either an existing Log Analytics workspace connected toohello VM or a new workspace created by Security Center.</span></span> <span data-ttu-id="0fedc-112">當資訊安全中心會建立新的工作區時，hello 地理位置的 hello VM 會列入考量。</span><span class="sxs-lookup"><span data-stu-id="0fedc-112">When Security Center creates a new workspace, hello geolocation of hello VM is taken into account.</span></span>

> [!NOTE]
> <span data-ttu-id="0fedc-113">hello Microsoft Monitoring Agent 是由 hello Operations Management Suite (OMS)、 記錄分析服務和 System Center Operations Manager (SCOM) hello 使用相同的代理程式。</span><span class="sxs-lookup"><span data-stu-id="0fedc-113">hello Microsoft Monitoring Agent is hello same agent used by hello Operations Management Suite (OMS), Log Analytics service and System Center Operations Manager (SCOM).</span></span>
>
>

<span data-ttu-id="0fedc-114">當 hello 啟用資料收集，第一次，或移轉訂用帳戶時，資訊安全中心檢查 toosee hello Microsoft Monitoring Agent 已安裝為 Azure Vm 的每個擴充功能。</span><span class="sxs-lookup"><span data-stu-id="0fedc-114">When data collection is enabled for hello first time or when your subscriptions are migrated, Security Center checks toosee if hello Microsoft Monitoring Agent is already installed as an Azure extension on each of your VMs.</span></span> <span data-ttu-id="0fedc-115">如果未安裝 Microsoft Monitoring Agent hello，資訊安全中心將會：</span><span class="sxs-lookup"><span data-stu-id="0fedc-115">If hello Microsoft Monitoring Agent is not installed, then Security Center will:</span></span>

- <span data-ttu-id="0fedc-116">在 hello VM 上安裝 hello Microsoft Monitoring agent</span><span class="sxs-lookup"><span data-stu-id="0fedc-116">install hello Microsoft Monitoring agent on hello VM</span></span>
   - <span data-ttu-id="0fedc-117">已建立，資訊安全中心的工作區存在於相同的地理位置為 hello VM，hello 的 hello 代理程式已連線的 toothis 工作區</span><span class="sxs-lookup"><span data-stu-id="0fedc-117">if a workspace created by Security Center already exists in hello same geolocation as hello VM, hello agent is connected toothis workspace</span></span>
   - <span data-ttu-id="0fedc-118">如果工作區不存在，資訊安全中心會建立新的資源群組和預設工作區中的地理位置，並連接 hello 代理程式 toothat 工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-118">if a workspace does not exist, Security Center creates a new resource group and default workspace in that geolocation, and connect hello agent toothat workspace.</span></span> <span data-ttu-id="0fedc-119">hello hello 工作區和資源群組的命名慣例如下：</span><span class="sxs-lookup"><span data-stu-id="0fedc-119">hello naming convention for hello workspace and resource group are:</span></span>

       <span data-ttu-id="0fedc-120">工作區：DefaultWorkspace-[subscription-ID]-[geo]</span><span class="sxs-lookup"><span data-stu-id="0fedc-120">Workspace: DefaultWorkspace-[subscription-ID]-[geo]</span></span>

       <span data-ttu-id="0fedc-121">資源群組：DefaultResouceGroup-[geo]</span><span class="sxs-lookup"><span data-stu-id="0fedc-121">Resource Group: DefaultResouceGroup-[geo]</span></span>
- <span data-ttu-id="0fedc-122">安裝資訊安全中心方案上 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="0fedc-122">install a Security Center solution on hello workspace</span></span>

<span data-ttu-id="0fedc-123">hello hello 工作區的位置根據 hello 的 hello VM 的位置。</span><span class="sxs-lookup"><span data-stu-id="0fedc-123">hello location of hello workspace is based on hello location of hello VM.</span></span> <span data-ttu-id="0fedc-124">詳細資訊，請參閱 toolearn[資料安全性](security-center-data-security.md)。</span><span class="sxs-lookup"><span data-stu-id="0fedc-124">toolearn more, see [Data Security](security-center-data-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0fedc-125">先前 tooplatform 移轉的資訊安全中心收集安全性資料從您的 Vm 使用 hello Azure 監視的代理程式和資料儲存在儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fedc-125">Prior tooplatform migration, Security Center collected security data from your VMs using hello Azure Monitoring Agent, and data was stored in your storage account.</span></span> <span data-ttu-id="0fedc-126">Hello 平台進行移轉之後，資訊安全中心會使用 Microsoft Monitoring Agent hello 和工作區 toocollect 和市集 hello 相同的資料。</span><span class="sxs-lookup"><span data-stu-id="0fedc-126">After hello platform migration, Security Center uses hello Microsoft Monitoring Agent and workspace toocollect and store hello same data.</span></span> <span data-ttu-id="0fedc-127">hello 移轉之後，就可以移除 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0fedc-127">hello storage account can be removed after hello migration.</span></span>
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a><span data-ttu-id="0fedc-128">收費 hello 資訊安全中心所建立的工作區上的 OMS 記錄分析的嗎？</span><span class="sxs-lookup"><span data-stu-id="0fedc-128">Am I billed for Log Analytics or OMS on hello workspaces created by Security Center?</span></span>
<span data-ttu-id="0fedc-129">否。</span><span class="sxs-lookup"><span data-stu-id="0fedc-129">No.</span></span> <span data-ttu-id="0fedc-130">資訊安全中心所建立的工作區雖然設定以每節點之 OMS 計費，但實際上不會產生 OMS 費用。</span><span class="sxs-lookup"><span data-stu-id="0fedc-130">Workspaces created by Security Center, while configured for OMS per node billing, do not incur OMS charges.</span></span> <span data-ttu-id="0fedc-131">資訊安全中心計費會永遠根據您的資訊安全中心安全性原則和 hello 解決方案安裝在工作區：</span><span class="sxs-lookup"><span data-stu-id="0fedc-131">Security Center billing is always based on your Security Center security policy and hello solutions installed on a workspace:</span></span>

- <span data-ttu-id="0fedc-132">**免費層次**– 資訊安全中心 hello 'SecurityCenterFree' 方案安裝 hello 預設工作區上。</span><span class="sxs-lookup"><span data-stu-id="0fedc-132">**Free tier** – Security Center installs hello 'SecurityCenterFree' solution on hello default workspace.</span></span> <span data-ttu-id="0fedc-133">您不必再支付 hello 免費層。</span><span class="sxs-lookup"><span data-stu-id="0fedc-133">You are not billed for hello Free tier.</span></span>
- <span data-ttu-id="0fedc-134">**標準層**– 資訊安全中心安裝 hello 'SecurityCenterFree' 和 'Security' 方案 hello 預設工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-134">**Standard tier** – Security Center installs hello 'SecurityCenterFree' and 'Security’ solutions on hello default workspace.</span></span>

<span data-ttu-id="0fedc-135">如需詳細資訊，請參閱[資訊安全中心價格](https://azure.microsoft.com/pricing/details/security-center/)。</span><span class="sxs-lookup"><span data-stu-id="0fedc-135">For more information on pricing, see [Security Center pricing](https://azure.microsoft.com/pricing/details/security-center/).</span></span> <span data-ttu-id="0fedc-136">hello 定價頁面位址變更 toosecurity 資料存放區，並在 2017 年 6 月計算按比例分配計費啟動。</span><span class="sxs-lookup"><span data-stu-id="0fedc-136">hello pricing page addresses changes toosecurity data storage and prorated billing starting in June 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="0fedc-137">hello OMS 定價層的資訊安全中心所建立的工作區不會影響帳單資訊安全中心。</span><span class="sxs-lookup"><span data-stu-id="0fedc-137">hello OMS pricing tier of workspaces created by Security Center does not affect Security Center billing.</span></span>
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a><span data-ttu-id="0fedc-138">可以刪除 hello 資訊安全中心所建立的預設工作區嗎？</span><span class="sxs-lookup"><span data-stu-id="0fedc-138">Can I delete hello default workspaces created by Security Center?</span></span>
<span data-ttu-id="0fedc-139">**建議您不要刪除 hello 預設工作區。**</span><span class="sxs-lookup"><span data-stu-id="0fedc-139">**Deleting hello default workspace is not recommended.**</span></span> <span data-ttu-id="0fedc-140">資訊安全中心使用 hello 預設工作區 toostore 安全性資料從您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="0fedc-140">Security Center uses hello default workspaces toostore security data from your VMs.</span></span>  <span data-ttu-id="0fedc-141">如果您刪除工作區中，資訊安全中心，而且無法 toocollect 這項資料的一些安全性建議，且無法使用警示</span><span class="sxs-lookup"><span data-stu-id="0fedc-141">If you delete a workspace, Security Center is unable toocollect this data and some security recommendations and alerts are unavailable</span></span>

<span data-ttu-id="0fedc-142">toorecover 移除 hello hello Vm 連接的 toohello 刪除工作區上的 Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="0fedc-142">toorecover, remove hello Microsoft Monitoring Agent on hello VMs connected toohello deleted workspace.</span></span> <span data-ttu-id="0fedc-143">資訊安全中心重新安裝 hello 代理程式，並建立新的預設工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-143">Security Center reinstalls hello agent and creates new default workspaces.</span></span>

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a><span data-ttu-id="0fedc-144">如果做為擴充 hello VM 上已安裝 hello Microsoft Monitoring Agent 嗎？</span><span class="sxs-lookup"><span data-stu-id="0fedc-144">What if hello Microsoft Monitoring Agent was already installed as an extension on hello VM?</span></span>
<span data-ttu-id="0fedc-145">資訊安全中心不會覆寫現有的連線 toouser 工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-145">Security Center does not override existing connections toouser workspaces.</span></span> <span data-ttu-id="0fedc-146">資訊安全中心的存放區安全性資料 hello hello 工作區中的 VM 從已連線。</span><span class="sxs-lookup"><span data-stu-id="0fedc-146">Security Center stores security data from hello VM in hello workspace already connected.</span></span>

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a><span data-ttu-id="0fedc-147">如果我有 Microsoft Monitoring Agent 安裝 hello 機器上，但不是能作為擴充功能？</span><span class="sxs-lookup"><span data-stu-id="0fedc-147">What if I had a Microsoft Monitoring Agent installed on hello machine but not as an extension?</span></span>
<span data-ttu-id="0fedc-148">如果 hello Microsoft Monitoring Agent 直接安裝在 hello VM （不是 Azure 擴充功能）、 資訊安全中心不會安裝 Microsoft Monitoring Agent hello 和安全性監視的內容會受到限制。</span><span class="sxs-lookup"><span data-stu-id="0fedc-148">If hello Microsoft Monitoring Agent is installed directly on hello VM (not as an Azure extension), Security Center will not install hello Microsoft Monitoring Agent and security monitoring will be limited.</span></span>

### <a name="what-is-hello-impact-of-removing-these-extensions"></a><span data-ttu-id="0fedc-149">移除這些擴充功能的 hello 影響為何？</span><span class="sxs-lookup"><span data-stu-id="0fedc-149">What is hello impact of removing these extensions?</span></span>
<span data-ttu-id="0fedc-150">如果您要移除 hello Microsoft 監視功能延伸模組，資訊安全中心不是 hello VM 可以 toocollect 安全性資料，而且某些安全性建議和警示是無法使用。</span><span class="sxs-lookup"><span data-stu-id="0fedc-150">If you remove hello Microsoft Monitoring Extension, Security Center is not able toocollect security data from hello VM and some security recommendations and alerts are unavailable.</span></span> <span data-ttu-id="0fedc-151">24 小時內，資訊安全中心會決定 hello VM 遺漏 hello 延伸模組，並重新安裝 hello 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0fedc-151">Within 24 hours, Security Center determines that hello VM is missing hello extension and reinstalls hello extension.</span></span>

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a><span data-ttu-id="0fedc-152">如何停止 hello 自動代理程式安裝和工作區建立？</span><span class="sxs-lookup"><span data-stu-id="0fedc-152">How do I stop hello automatic agent installation and workspace creation?</span></span>
<span data-ttu-id="0fedc-153">您可以關閉資料收集 hello 安全性原則中訂用帳戶，但不是建議這樣。</span><span class="sxs-lookup"><span data-stu-id="0fedc-153">You can turn off data collection for your subscriptions in hello security policy but this is not recommended.</span></span> <span data-ttu-id="0fedc-154">關閉資料收集會限制資訊安全中心的建議和警示。</span><span class="sxs-lookup"><span data-stu-id="0fedc-154">Turning off data collection limits Security Center recommendations and alerts.</span></span> <span data-ttu-id="0fedc-155">資料收集都需要訂閱 hello 標準定價層。</span><span class="sxs-lookup"><span data-stu-id="0fedc-155">Data collection is required for subscriptions on hello Standard pricing tier.</span></span> <span data-ttu-id="0fedc-156">toodisable 資料收集：</span><span class="sxs-lookup"><span data-stu-id="0fedc-156">toodisable data collection:</span></span>

1. <span data-ttu-id="0fedc-157">如果您的訂用帳戶設定為 hello 標準層，開啟 hello 該訂用帳戶的安全性原則，然後選取 hello**免費**層。</span><span class="sxs-lookup"><span data-stu-id="0fedc-157">If your subscription is configured for hello Standard tier, open hello security policy for that subscription and select hello **Free** tier.</span></span>

   ![定價層 ][1]

2. <span data-ttu-id="0fedc-159">接下來，會關閉選取的資料收集**關閉**上 hello**安全性原則-資料收集**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="0fedc-159">Next, turn off data collection by selecting **Off** on hello **Security policy – Data collection** blade.</span></span>

   ![資料收集][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a><span data-ttu-id="0fedc-161">我要如何移除資訊安全中心安裝的 OMS 擴充功能？</span><span class="sxs-lookup"><span data-stu-id="0fedc-161">How do I remove OMS extensions installed by Security Center?</span></span>
<span data-ttu-id="0fedc-162">您可以手動移除 hello Microsoft Monitoring Agent。</span><span class="sxs-lookup"><span data-stu-id="0fedc-162">You can manually remove hello Microsoft Monitoring Agent.</span></span> <span data-ttu-id="0fedc-163">關閉資料收集會限制資訊安全中心的建議和警示，所以不建議您這麼做。</span><span class="sxs-lookup"><span data-stu-id="0fedc-163">This is not recommended as it limits Security Center recommendations and alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="0fedc-164">如果已啟用資料收集，資訊安全中心將會重新安裝 hello 代理程式之後您將它移除。</span><span class="sxs-lookup"><span data-stu-id="0fedc-164">If data collection is enabled, Security Center will reinstall hello agent after you remove it.</span></span>  <span data-ttu-id="0fedc-165">您必須手動移除 hello 代理程式之前，先 toodisable 資料收集。</span><span class="sxs-lookup"><span data-stu-id="0fedc-165">You need toodisable data collection before manually removing hello agent.</span></span> <span data-ttu-id="0fedc-166">請參閱[如何停止 hello 自動代理程式安裝和工作區建立？](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?)如需停用資料收集的指示。</span><span class="sxs-lookup"><span data-stu-id="0fedc-166">See [How do I stop hello automatic agent installation and workspace creation?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) for instructions on disabling data collection.</span></span>
>
>

<span data-ttu-id="0fedc-167">toomanually 移除 hello 代理程式：</span><span class="sxs-lookup"><span data-stu-id="0fedc-167">toomanually remove hello agent:</span></span>

1.  <span data-ttu-id="0fedc-168">在 hello 入口網站中，開啟**記錄分析**。</span><span class="sxs-lookup"><span data-stu-id="0fedc-168">In hello portal, open **Log Analytics**.</span></span>
2.  <span data-ttu-id="0fedc-169">在 hello 記錄分析刀鋒視窗中，選取工作區：</span><span class="sxs-lookup"><span data-stu-id="0fedc-169">On hello Log Analytics blade, select a workspace:</span></span>
3.  <span data-ttu-id="0fedc-170">選取您不想 toomonitor，並選取每個 VM**中斷連線**。</span><span class="sxs-lookup"><span data-stu-id="0fedc-170">Select each VM that you don’t want toomonitor and select **Disconnect**.</span></span>

   ![移除 hello 代理程式][3]

> [!NOTE]
> <span data-ttu-id="0fedc-172">如果 Linux VM 已經有不含副檔名的 OMS 代理程式，移除 hello 延伸模組會移除 hello 代理程式和 hello 客戶有 tooreinstall 它。</span><span class="sxs-lookup"><span data-stu-id="0fedc-172">If a Linux VM already has a non-extension OMS agent, removing hello extension removes hello agent as well and hello customer has tooreinstall it.</span></span>
>
>

## <a name="existing-oms-customers"></a><span data-ttu-id="0fedc-173">現有的 OMS 客戶</span><span class="sxs-lookup"><span data-stu-id="0fedc-173">Existing OMS customers</span></span>

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a><span data-ttu-id="0fedc-174">資訊安全中心是否會覆寫任何虛擬機器及工作區之間現有的連線？</span><span class="sxs-lookup"><span data-stu-id="0fedc-174">Does Security Center override any existing connections between VMs and workspaces?</span></span>
<span data-ttu-id="0fedc-175">如果 VM 已經有 hello 安裝為 Azure 擴充功能的 Microsoft Monitoring Agent，資訊安全中心不會覆寫 hello 現有工作區的連接。</span><span class="sxs-lookup"><span data-stu-id="0fedc-175">If a VM already has hello Microsoft Monitoring Agent installed as an Azure extension, Security Center does not override hello existing workspace connection.</span></span> <span data-ttu-id="0fedc-176">相反地，資訊安全中心會使用 hello 現有的工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-176">Instead, Security Center uses hello existing workspace.</span></span>

<span data-ttu-id="0fedc-177">資訊安全中心方案上 hello 工作區中安裝如果不存在，且 hello 方案套用只有 toohello 相關 Vm。</span><span class="sxs-lookup"><span data-stu-id="0fedc-177">A Security Center solution is installed on hello workspace if not present already, and hello solution is applied only toohello relevant VMs.</span></span> <span data-ttu-id="0fedc-178">當您加入方案時，它會自動部署預設 tooall Windows 和 Linux 代理程式連接的 tooyour 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-178">When you add a solution, it's automatically deployed by default tooall Windows and Linux agents connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="0fedc-179">[方案目標](../operations-management-suite/operations-management-suite-solution-targeting.md)，這是一項 OMS 功能，可讓您 tooapply 範圍 tooyour 解決方案。</span><span class="sxs-lookup"><span data-stu-id="0fedc-179">[Solution Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), which is an OMS feature, allows you tooapply a scope tooyour solutions.</span></span>

<span data-ttu-id="0fedc-180">如果 hello Microsoft Monitoring Agent 直接安裝上 hello VM （不是 Azure 擴充功能）、 資訊安全中心不會安裝 Microsoft Monitoring Agent hello 和安全性監視會受到限制。</span><span class="sxs-lookup"><span data-stu-id="0fedc-180">If hello Microsoft Monitoring Agent is installed directly on hello VM (not as an Azure extension), Security Center will not install hello Microsoft Monitoring Agent and security monitoring is limited.</span></span>

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a><span data-ttu-id="0fedc-181">如果我認為 hello 資料平台移轉中斷其中一個 Vm 我和我的工作區之間的 hello 連線我該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="0fedc-181">What should I do if I suspect that hello data platform migration broke hello connection between one of my VMs and my workspace?</span></span>
<span data-ttu-id="0fedc-182">這種情況不應發生。</span><span class="sxs-lookup"><span data-stu-id="0fedc-182">This should not happen.</span></span> <span data-ttu-id="0fedc-183">如果還是會發生，然後[建立 Azure 支援人員要求](../azure-supportability/how-to-create-azure-support-request.md)而且包含下列詳細資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="0fedc-183">If it does happen, then [Create an Azure support request](../azure-supportability/how-to-create-azure-support-request.md) and include hello following details:</span></span>

- <span data-ttu-id="0fedc-184">hello Azure 資源識別碼 hello 影響 VM</span><span class="sxs-lookup"><span data-stu-id="0fedc-184">hello Azure resource ID of hello impacted VM</span></span>
- <span data-ttu-id="0fedc-185">hello Azure 資源識別碼 hello hello 的連線已中斷之前，請先 hello 延伸上設定的工作區</span><span class="sxs-lookup"><span data-stu-id="0fedc-185">hello Azure resource ID of hello workspace configured on hello extension before hello connection was broken</span></span>
- <span data-ttu-id="0fedc-186">hello 代理程式和先前已安裝的版本</span><span class="sxs-lookup"><span data-stu-id="0fedc-186">hello agent and version that was previously installed</span></span>

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a><span data-ttu-id="0fedc-187">資訊安全中心是否會在我現有的 OMS 工作區上安裝解決方案？</span><span class="sxs-lookup"><span data-stu-id="0fedc-187">Does Security Center install solutions on my existing OMS workspaces?</span></span> <span data-ttu-id="0fedc-188">Hello 的計費方式有哪些？</span><span class="sxs-lookup"><span data-stu-id="0fedc-188">What are hello billing implications?</span></span>
<span data-ttu-id="0fedc-189">資訊安全中心識別 VM 是已連接的 tooa 建立工作區，資訊安全中心 」 可根據 tooyour 定價層此工作區的解決方案。</span><span class="sxs-lookup"><span data-stu-id="0fedc-189">When Security Center identifies that a VM is already connected tooa workspace you created, Security Center enables solutions on this workspace according tooyour pricing tier.</span></span> <span data-ttu-id="0fedc-190">hello 解決方案透過相關的 Azure Vm，會套用只有 toohello[方案目標](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)，因此 hello 計費會維持為 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="0fedc-190">hello solutions are applied only toohello relevant Azure VMs, via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), so hello billing remains hello same.</span></span>

- <span data-ttu-id="0fedc-191">**免費層次**– 資訊安全中心 hello 'SecurityCenterFree' 方案安裝 hello 工作區上。</span><span class="sxs-lookup"><span data-stu-id="0fedc-191">**Free tier** – Security Center installs hello 'SecurityCenterFree' solution on hello workspace.</span></span> <span data-ttu-id="0fedc-192">您不必再支付 hello 免費層。</span><span class="sxs-lookup"><span data-stu-id="0fedc-192">You are not billed for hello Free tier.</span></span>
- <span data-ttu-id="0fedc-193">**標準層**– 資訊安全中心安裝 hello 'SecurityCenterFree' 和 'Security' 方案 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-193">**Standard tier** – Security Center installs hello 'SecurityCenterFree' and 'Security' solutions on hello workspace.</span></span>

   ![預設工作區的解決方案][4]

> [!NOTE]
> <span data-ttu-id="0fedc-195">hello 'Security' 方案中記錄分析是 hello 安全性和稽核解決方案在 OMS 中。</span><span class="sxs-lookup"><span data-stu-id="0fedc-195">hello ‘Security’ solution in Log Analytics is hello Security & Audit solution in OMS.</span></span>
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a><span data-ttu-id="0fedc-196">在 我的環境中已經有工作區，可以如何使用它們 toocollect 安全性資料嗎？</span><span class="sxs-lookup"><span data-stu-id="0fedc-196">I already have workspaces in my environment, can I use them toocollect security data?</span></span>
<span data-ttu-id="0fedc-197">如果 VM 已經有 hello 安裝為 Azure 擴充功能的 Microsoft Monitoring Agent，資訊安全中心會使用 hello 現有連線的工作區。</span><span class="sxs-lookup"><span data-stu-id="0fedc-197">If a VM already has hello Microsoft Monitoring Agent installed as an Azure extension, Security Center uses hello existing connected workspace.</span></span> <span data-ttu-id="0fedc-198">資訊安全中心方案上 hello 工作區中安裝如果不存在，而且 hello 方案套用只有 toohello 相關 Vm 透過[方案目標](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting)。</span><span class="sxs-lookup"><span data-stu-id="0fedc-198">A Security Center solution is installed on hello workspace if not present already, and hello solution is applied only toohello relevant VMs via [solution targeting](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).</span></span>

<span data-ttu-id="0fedc-199">資訊安全中心進行安裝時 hello Microsoft Monitoring Agent 在 Vm 上，它會使用 hello 預設 workspace(s) 資訊安全中心所建立。</span><span class="sxs-lookup"><span data-stu-id="0fedc-199">When Security Center installs hello Microsoft Monitoring Agent on VMs, it uses hello default workspace(s) created by Security Center.</span></span> <span data-ttu-id="0fedc-200">推出客戶將能夠 tooconfigure 哪些 workspace(s) 可用。</span><span class="sxs-lookup"><span data-stu-id="0fedc-200">Soon customers will be able tooconfigure which workspace(s) are used.</span></span>

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a><span data-ttu-id="0fedc-201">我的工作區上已經有安全性解決方案。</span><span class="sxs-lookup"><span data-stu-id="0fedc-201">I already have security solution on my workspaces.</span></span> <span data-ttu-id="0fedc-202">Hello 的計費方式有哪些？</span><span class="sxs-lookup"><span data-stu-id="0fedc-202">What are hello billing implications?</span></span>
<span data-ttu-id="0fedc-203">hello 安全性和稽核解決方案是使用的 tooenable 安全性中心標準層功能的 Azure Vm。</span><span class="sxs-lookup"><span data-stu-id="0fedc-203">hello Security & Audit solution is used tooenable Security Center Standard tier features for Azure VMs.</span></span> <span data-ttu-id="0fedc-204">如果工作區上已安裝 hello 安全性和稽核解決方案，資訊安全中心會使用 hello 現有的方案。</span><span class="sxs-lookup"><span data-stu-id="0fedc-204">If hello Security & Audit solution is already installed on a workspace, Security Center uses hello existing solution.</span></span> <span data-ttu-id="0fedc-205">收費不會改變。</span><span class="sxs-lookup"><span data-stu-id="0fedc-205">There is no change in billing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fedc-206">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0fedc-206">Next steps</span></span>
<span data-ttu-id="0fedc-207">toolearn 解 hello 資訊安全中心平台移轉，請參閱</span><span class="sxs-lookup"><span data-stu-id="0fedc-207">toolearn more about hello Security Center platform migration, see</span></span>

- [<span data-ttu-id="0fedc-208">Azure 資訊安全中心平台移轉</span><span class="sxs-lookup"><span data-stu-id="0fedc-208">Azure Security Center Platform Migration</span></span>](security-center-platform-migration.md)
- [<span data-ttu-id="0fedc-209">Azure 資訊安全中心疑難排解指南</span><span class="sxs-lookup"><span data-stu-id="0fedc-209">Azure Security Center Troubleshooting Guide</span></span>](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
