---
title: "aaaSecurity 監視 Azure 資訊安全中心 |Microsoft 文件"
description: "這篇文章可協助您 tooget 入門監視 Azure 資訊安全中心中的功能。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a><span data-ttu-id="d3f61-103">Azure 資訊安全中心的安全性健康情況監視</span><span class="sxs-lookup"><span data-stu-id="d3f61-103">Security health monitoring in Azure Security Center</span></span>
<span data-ttu-id="d3f61-104">這篇文章可協助您使用 hello Azure 資訊安全中心 toomonitor 符合原則中的監視功能。</span><span class="sxs-lookup"><span data-stu-id="d3f61-104">This article helps you use hello monitoring capabilities in Azure Security Center toomonitor compliance with policies.</span></span>

## <a name="what-is-security-health-monitoring"></a><span data-ttu-id="d3f61-105">什麼是安全性健康情況監視？</span><span class="sxs-lookup"><span data-stu-id="d3f61-105">What is security health monitoring?</span></span>
<span data-ttu-id="d3f61-106">我們通常將為監看及等候事件 toooccur，以便我們可以反應 toohello 狀況監視。</span><span class="sxs-lookup"><span data-stu-id="d3f61-106">We often think of monitoring as watching and waiting for an event toooccur so that we can react toohello situation.</span></span> <span data-ttu-id="d3f61-107">安全性監視是指 toohaving 稽核時，不符合組織的標準或最佳作法 tooidentify 系統資源的主動式策略。</span><span class="sxs-lookup"><span data-stu-id="d3f61-107">Security monitoring refers toohaving a proactive strategy that audits your resources tooidentify systems that do not meet organizational standards or best practices.</span></span>

## <a name="monitoring-security-health"></a><span data-ttu-id="d3f61-108">監視安全性健全狀況</span><span class="sxs-lookup"><span data-stu-id="d3f61-108">Monitoring security health</span></span>
<span data-ttu-id="d3f61-109">啟用後[安全性原則](security-center-policies.md)訂用帳戶的資源資訊安全中心會分析 hello 安全性資源 tooidentify 的潛在弱點的風險。</span><span class="sxs-lookup"><span data-stu-id="d3f61-109">After you enable [security policies](security-center-policies.md) for a subscription’s resources, Security Center analyzes hello security of your resources tooidentify potential vulnerabilities.</span></span> <span data-ttu-id="d3f61-110">您可以立即取得網路組態的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d3f61-110">Information about your network configuration is available instantly.</span></span> <span data-ttu-id="d3f61-111">可能需要一小時或更多有關虛擬機器組態，例如安全性更新狀態和作業系統設定、 toobecome 可用。</span><span class="sxs-lookup"><span data-stu-id="d3f61-111">It may take an hour or more for information about virtual machine configuration, such as security update status and operating system configuration, toobecome available.</span></span> <span data-ttu-id="d3f61-112">您可以檢視您的資源和任何問題 hello 安全性狀態中 hello**防止**> 一節。</span><span class="sxs-lookup"><span data-stu-id="d3f61-112">You can view hello security state of your resources and any issues in hello **Prevention** section.</span></span> <span data-ttu-id="d3f61-113">您也可以檢視這些問題的清單上 hello**建議**磚。</span><span class="sxs-lookup"><span data-stu-id="d3f61-113">You can also view a list of those issues on hello **Recommendations** tile.</span></span>

<span data-ttu-id="d3f61-114">如需有關如何 tooapply 建議事項，讀取[實作 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f61-114">For more information about how tooapply recommendations, read [Implementing security recommendations in Azure Security Center](security-center-recommendations.md).</span></span>

<span data-ttu-id="d3f61-115">在 hello**防止** 區段中，您可以監視您的資源 hello 安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="d3f61-115">Under hello **Prevention** section, you can monitor hello security state of your resources.</span></span> <span data-ttu-id="d3f61-116">在下列範例的 hello，您可以查看每項資源的磚 （運算、 網路功能、 存放裝置 （& s） 資料和應用程式） 中具有已識別問題的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="d3f61-116">In hello following example, you can see that in each resource's tile (Compute, Networking, Storage & data, and Application) has hello total number of issues that were identified.</span></span>

![資源安全性健康情況圖格](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a><span data-ttu-id="d3f61-118">監視計算</span><span class="sxs-lookup"><span data-stu-id="d3f61-118">Monitor compute</span></span>
<span data-ttu-id="d3f61-119">當您按一下**計算**磚，hello**計算**開啟刀鋒視窗會顯示三個索引標籤：</span><span class="sxs-lookup"><span data-stu-id="d3f61-119">When you click **Compute** tile, hello **Compute** blade that opens shows three tabs:</span></span>

- <span data-ttu-id="d3f61-120">**概觀**︰監視和虛擬機器建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-120">**Overview**: monitoring and virtual machine recommendations.</span></span>
- <span data-ttu-id="d3f61-121">**虛擬機器**︰列出所有虛擬機器及其目前的安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="d3f61-121">**Virtual Machines**: list all all virtual machines and its current security state.</span></span>
- <span data-ttu-id="d3f61-122">**雲端服務**︰資訊安全中心監視的所有 Web 和背景工作角色清單。</span><span class="sxs-lookup"><span data-stu-id="d3f61-122">**Cloud Services**: list of all web and worker roles monitored by Security Center.</span></span>

![遺失的系統更新 (依虛擬機器)](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

<span data-ttu-id="d3f61-124">在每個索引標籤中，您可以擁有多個區段，並在每個區段中，您可以選取個別選項 toosee hello 的更多詳細建議步驟 tooaddress 該特定問題。</span><span class="sxs-lookup"><span data-stu-id="d3f61-124">In each tab you can have multiple sections, and in each section, you can select an individual option toosee more details about hello recommended steps tooaddress that particular issue.</span></span> 

#### <a name="monitoring-recommendations"></a><span data-ttu-id="d3f61-125">監視建議</span><span class="sxs-lookup"><span data-stu-id="d3f61-125">Monitoring recommendations</span></span>
<span data-ttu-id="d3f61-126">本節說明已初始化的資料收集和其目前狀態的虛擬機器的 hello 總數。</span><span class="sxs-lookup"><span data-stu-id="d3f61-126">This section shows hello total number of virtual machines that were initialized for data collection and their current statuses.</span></span> <span data-ttu-id="d3f61-127">所有虛擬機器都有初始化的資料收集之後，就會準備 tooreceive 資訊安全中心的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="d3f61-127">After all virtual machines have data collection initialized, they will be ready tooreceive Security Center security policies.</span></span> <span data-ttu-id="d3f61-128">當您按一下這個項目時，hello **VM 代理程式已遺失或沒有回應**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d3f61-128">When you click this entry, hello **VM Agent is missing or not responding** blade opens.</span></span> 

![遺失的系統更新 (依虛擬機器)](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a><span data-ttu-id="d3f61-130">虛擬機器建議</span><span class="sxs-lookup"><span data-stu-id="d3f61-130">Virtual machine recommendations</span></span>
<span data-ttu-id="d3f61-131">本節提供一組 Azure 資訊安全中心所監視之[每個虛擬機器的建議](security-center-virtual-machine-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f61-131">This section has a set of [recommendations for each virtual machine](security-center-virtual-machine-recommendations.md) that Azure Security Center monitors.</span></span> <span data-ttu-id="d3f61-132">hello 第一個資料行列出 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-132">hello first column lists hello recommendation.</span></span> <span data-ttu-id="d3f61-133">hello 第二個資料行顯示 hello 總數會受到該項建議的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f61-133">hello second column shows hello total number of virtual machines that are affected by that recommendation.</span></span> <span data-ttu-id="d3f61-134">hello 第三個資料行顯示 hello hello 問題嚴重性 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-134">hello third column shows hello severity of hello issue as illustrated in hello following screenshot.</span></span>

![虛擬機器建議](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> <span data-ttu-id="d3f61-136">有至少一個公用端點的虛擬機器會顯示在 hello**網路健全狀況**刀鋒視窗中 hello**網路拓樸**清單。</span><span class="sxs-lookup"><span data-stu-id="d3f61-136">Only virtual machines that have at least one public endpoint are shown in hello **Networking Health** blade in hello **Network topology** list.</span></span>
>
>

<span data-ttu-id="d3f61-137">每個建議在經過點選之後，都會有一組可供執行的動作。</span><span class="sxs-lookup"><span data-stu-id="d3f61-137">Each recommendation has a set of actions that you can perform after you click it.</span></span> <span data-ttu-id="d3f61-138">比方說，如果您按一下**遺漏的系統更新**，hello**遺漏的系統更新**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="d3f61-138">For example, if you click **Missing system updates**, hello **Missing system updates** blade opens.</span></span> <span data-ttu-id="d3f61-139">它會列出遺失的修補程式和 hello hello 遺失更新的嚴重性 hello 下列所示的 hello 虛擬機器螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="d3f61-139">It lists hello virtual machines that are missing patches and hello severity of hello missing update as shown in hello following screenshot.</span></span>

![虛擬機器遺失的系統更新](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

<span data-ttu-id="d3f61-141">hello**遺漏的系統更新**刀鋒視窗中顯示的資料表以 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d3f61-141">hello **Missing system updates** blade shows a table with hello following information:</span></span>

* <span data-ttu-id="d3f61-142">**虛擬機器**: hello hello 遺失更新的虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="d3f61-142">**VIRTUAL MACHINE**: hello name of hello virtual machine that is missing updates.</span></span>
* <span data-ttu-id="d3f61-143">**系統更新**: hello 的系統更新遺漏的數目。</span><span class="sxs-lookup"><span data-stu-id="d3f61-143">**SYSTEM UPDATES**: hello number of system updates that are missing.</span></span>
* <span data-ttu-id="d3f61-144">**上次掃描時間**: hello 時間資訊安全中心上次掃描更新 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f61-144">**LAST SCAN TIME**: hello time that Security Center last scanned hello virtual machine for updates.</span></span>
* <span data-ttu-id="d3f61-145">**狀態**: hello hello 建議的目前狀態：</span><span class="sxs-lookup"><span data-stu-id="d3f61-145">**STATE**: hello current state of hello recommendation:</span></span>
  * <span data-ttu-id="d3f61-146">**開啟**: hello 建議的解決不尚未。</span><span class="sxs-lookup"><span data-stu-id="d3f61-146">**Open**: hello recommendation has not been addressed yet.</span></span>
  * <span data-ttu-id="d3f61-147">**正在進行中**: hello 建議目前正在套用的 toothose 資源，並由您不需要任何動作。</span><span class="sxs-lookup"><span data-stu-id="d3f61-147">**In Progress**: hello recommendation is currently being applied toothose resources, and no action is required by you.</span></span>
  * <span data-ttu-id="d3f61-148">**解析**: hello 建議已經完成。</span><span class="sxs-lookup"><span data-stu-id="d3f61-148">**Resolved**: hello recommendation was already finished.</span></span> <span data-ttu-id="d3f61-149">（當 hello 問題已經解決時，hello 項目會呈暗灰色）。</span><span class="sxs-lookup"><span data-stu-id="d3f61-149">(When hello issue has been resolved, hello entry is dimmed).</span></span>
* <span data-ttu-id="d3f61-150">**嚴重性**： 描述該特定建議事項的 hello 嚴重性：</span><span class="sxs-lookup"><span data-stu-id="d3f61-150">**SEVERITY**: Describes hello severity of that particular recommendation:</span></span>
  * <span data-ttu-id="d3f61-151">**高**：某個有意義的資源 (應用程式、虛擬機器或網路安全性群組) 有弱點存在，並且需要注意。</span><span class="sxs-lookup"><span data-stu-id="d3f61-151">**High**: A vulnerability exists with a meaningful resource (application, virtual machine, or network security group) and requires attention.</span></span>
  * <span data-ttu-id="d3f61-152">**媒體**： 非關鍵的或額外的步驟是必要的 toocomplete 處理序或消除弱點。</span><span class="sxs-lookup"><span data-stu-id="d3f61-152">**Medium**: Non-critical or additional steps are required toocomplete a process or eliminate a vulnerability.</span></span>
  * <span data-ttu-id="d3f61-153">**低**：應該處理但不需要立即注意的弱點。</span><span class="sxs-lookup"><span data-stu-id="d3f61-153">**Low**: A vulnerability should be addressed but does not require immediate attention.</span></span> <span data-ttu-id="d3f61-154">(根據預設，不呈現低的建議，但是如果您想 tooview，您可以篩選低建議它們。)</span><span class="sxs-lookup"><span data-stu-id="d3f61-154">(By default, low recommendations are not presented, but you can filter on low recommendations if you want tooview them.)</span></span>

<span data-ttu-id="d3f61-155">tooview hello 建議的詳細資訊，請按一下 hello hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="d3f61-155">tooview hello recommendation details, click hello name of hello virtual machine.</span></span> <span data-ttu-id="d3f61-156">該虛擬機器的新刀鋒視窗會開啟 hello 的更新清單中 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-156">A new blade for that virtual machine opens with hello list of updates as shown in hello following screenshot.</span></span>

![特定虛擬機器遺失的系統更新](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> <span data-ttu-id="d3f61-158">hello 安全性建議事項會與 hello hello 相同**建議**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3f61-158">hello security recommendations here are hello same as those in hello **Recommendations** blade.</span></span> <span data-ttu-id="d3f61-159">請參閱 hello[實作 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)發行項，如需有關如何 tooresolve 建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-159">See hello [Implementing security recommendations in Azure Security Center](security-center-recommendations.md) article for more information about how tooresolve recommendations.</span></span> <span data-ttu-id="d3f61-160">這僅適用於虛擬機器，也適用於所有 hello 中可用的資源不只**資源健全狀況**磚。</span><span class="sxs-lookup"><span data-stu-id="d3f61-160">This is applicable not only for virtual machines but also for all resources that are available in hello **Resource Health** tile.</span></span>
>
>

#### <a name="virtual-machines-section"></a><span data-ttu-id="d3f61-161">虛擬機器區段</span><span class="sxs-lookup"><span data-stu-id="d3f61-161">Virtual machines section</span></span>
<span data-ttu-id="d3f61-162">hello 虛擬機器 區段可讓您的所有虛擬機器和建議事項概觀。</span><span class="sxs-lookup"><span data-stu-id="d3f61-162">hello virtual machines section gives you an overview of all virtual machines and recommendations.</span></span> <span data-ttu-id="d3f61-163">每個資料行代表一組建議 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-163">Each column represents one set of recommendations as shown in hello following screenshot:</span></span>

![所有虛擬機器和建議的概觀](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

<span data-ttu-id="d3f61-165">hello 圖示出現在每個建議可協助您 tooquickly 識別需要注意和 hello 類型建議事項的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f61-165">hello icon that appears under each recommendation helps you tooquickly identify hello virtual machines that need attention and hello type of recommendation.</span></span>

<span data-ttu-id="d3f61-166">Hello 上述範例中，在一部虛擬機器會具有關於端點保護的重要建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-166">In hello previous example, one virtual machine has a critical recommendation regarding endpoint protection.</span></span> <span data-ttu-id="d3f61-167">tooget 需 hello 虛擬機器，按一下它。</span><span class="sxs-lookup"><span data-stu-id="d3f61-167">tooget more information about hello virtual machine, click it.</span></span> <span data-ttu-id="d3f61-168">開啟的新刀鋒視窗表示此虛擬機器中 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-168">A new blade that opens represents this virtual machine as shown in hello following screenshot.</span></span>

![虛擬機器安全性詳細資料](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

<span data-ttu-id="d3f61-170">此刀鋒視窗有 hello 虛擬機器的 hello 安全性詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d3f61-170">This blade has hello security details for hello virtual machine.</span></span> <span data-ttu-id="d3f61-171">在 hello 這個刀鋒視窗底部，您可以看到 hello 建議動作並 hello 的每個問題的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="d3f61-171">At hello bottom of this blade, you can see hello recommended action and hello severity of each issue.</span></span>

#### <a name="cloud-services-section"></a><span data-ttu-id="d3f61-172">雲端服務區段</span><span class="sxs-lookup"><span data-stu-id="d3f61-172">Cloud services section</span></span>
<span data-ttu-id="d3f61-173">雲端服務的建議是時建立的 hello 作業系統版本已過期 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-173">For cloud services, a recommendation is created when hello operating system version is out of date as shown in hello following screenshot:</span></span>

![雲端服務的健康情況狀態](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

<span data-ttu-id="d3f61-175">在此案例中，您需要在建議 （這不是 hello 前一個範例的 hello 案例），您需要 toofollow hello 步驟 hello 建議 tooupdate hello 作業系統版本。</span><span class="sxs-lookup"><span data-stu-id="d3f61-175">In a scenario where you do have recommendation (which is not hello case for hello previous example), you need toofollow hello steps in hello recommendation tooupdate hello operating system version.</span></span> <span data-ttu-id="d3f61-176">當有可用的更新時，您會有警示 （紅色或橙色-取決於 hello hello 問題嚴重性）。</span><span class="sxs-lookup"><span data-stu-id="d3f61-176">When an update is available, you will have an alert (red or orange - depends on hello severity of hello issue).</span></span> <span data-ttu-id="d3f61-177">當您按一下此警示的 hello WebRole1 （與您的 web 應用程式自動部署 tooIIS 執行 Windows Server） 或 WorkerRole1 （與您的 web 應用程式自動部署 tooIIS 執行 Windows Server） 的資料列時的新刀鋒視窗隨即開啟並更詳細建議 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-177">When you click on this alert in hello WebRole1 (runs Windows Server with your web app automatically deployed tooIIS) or WorkerRole1 (runs Windows Server with your web app automatically deployed tooIIS) rows, a new blade opens with more details about this recommendation as shown in hello following screenshot:</span></span>

![雲端服務詳細資料](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

<span data-ttu-id="d3f61-179">toosee 的更精準解釋這項建議中，按一下**更新的 OS 版本**下 hello**描述**資料行。</span><span class="sxs-lookup"><span data-stu-id="d3f61-179">toosee a more prescriptive explanation about this recommendation, click **Update OS version** under hello **DESCRIPTION** column.</span></span> <span data-ttu-id="d3f61-180">hello**更新的 OS 版本 （預覽）**刀鋒視窗會開啟具有更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d3f61-180">hello **Update OS version (Preview)** blade opens with more details.</span></span>

![雲端服務建議](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a><span data-ttu-id="d3f61-182">監視虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d3f61-182">Monitor virtual networks</span></span>
<span data-ttu-id="d3f61-183">當您按一下**網路**磚，hello**網路**刀鋒視窗會開啟含有詳細 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-183">When you click **Networking** tile, hello **Networking** blade opens with more details as shown in hello following screenshot:</span></span>

![網路刀鋒視窗](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a><span data-ttu-id="d3f61-185">網路功能的建議</span><span class="sxs-lookup"><span data-stu-id="d3f61-185">Networking recommendations</span></span>
<span data-ttu-id="d3f61-186">Hello 虛擬機器的資源健全狀況資訊，例如此刀鋒視窗會提供在 hello hello 刀鋒視窗的頂端和受監視的網路清單問題的摘要的清單 hello 下方。</span><span class="sxs-lookup"><span data-stu-id="d3f61-186">Like hello virtual machine's resource health information, this blade provides a summarized list of issues at hello top of hello blade and a list of monitored networks on hello bottom.</span></span>

<span data-ttu-id="d3f61-187">hello 網路狀態分解 > 一節列出潛在的安全性問題，並提供[建議](security-center-network-recommendations.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f61-187">hello networking status breakdown section lists potential security issues and offers [recommendations](security-center-network-recommendations.md).</span></span> <span data-ttu-id="d3f61-188">可能的問題包括：</span><span class="sxs-lookup"><span data-stu-id="d3f61-188">Possible issues can include:</span></span>

* <span data-ttu-id="d3f61-189">未安裝新一代防火牆 (NGFW)</span><span class="sxs-lookup"><span data-stu-id="d3f61-189">Next-Generation Firewall (NGFW) not installed</span></span>
* <span data-ttu-id="d3f61-190">未啟用子網路上的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="d3f61-190">Network security groups on subnets not enabled</span></span>
* <span data-ttu-id="d3f61-191">未啟用虛擬機器上的網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="d3f61-191">Network security groups on virtual machines not enabled</span></span>
* <span data-ttu-id="d3f61-192">限制透過公用外部端點的外部存取</span><span class="sxs-lookup"><span data-stu-id="d3f61-192">Restrict external access through public external endpoint</span></span>
* <span data-ttu-id="d3f61-193">狀況良好的網際網路面向端點</span><span class="sxs-lookup"><span data-stu-id="d3f61-193">Healthy Internet facing endpoints</span></span>

<span data-ttu-id="d3f61-194">當您按一下建議時，hello 下列範例所示的新刀鋒視窗會開啟 hello 建議相關的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d3f61-194">When you click a recommendation, a new blade opens with more details about hello recommendation as shown in hello following example.</span></span>

![Hello 網路刀鋒視窗中的建議的詳細資料](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

<span data-ttu-id="d3f61-196">在此範例中，hello**設定遺失的網路安全性群組的子網路**刀鋒視窗中有一份子網路和虛擬機器遺失的網路安全性群組保護。</span><span class="sxs-lookup"><span data-stu-id="d3f61-196">In this example, hello **Configure Missing Network Security Groups for Subnets** blade has a list of subnets and virtual machines that are missing network security group protection.</span></span> <span data-ttu-id="d3f61-197">如果您按一下 hello 子網路 toowhich 想 tooapply hello 網路安全性群組，會開啟另一個刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d3f61-197">If you click hello subnet toowhich you want tooapply hello network security group, another blade opens.</span></span>

<span data-ttu-id="d3f61-198">在 hello**選擇網路安全性群組**刀鋒視窗中，您可以選取 hello 最適當的網路安全性群組 hello 的子網路，或者您可以建立新的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="d3f61-198">In hello **Choose network security group** blade, you can select hello most appropriate network security group for hello subnet, or you can create a new network security group.</span></span>

#### <a name="internet-facing-endpoints-section"></a><span data-ttu-id="d3f61-199">網際網路面向端點區段</span><span class="sxs-lookup"><span data-stu-id="d3f61-199">Internet facing endpoints section</span></span>
<span data-ttu-id="d3f61-200">在 [hello**網際網路對向端點**] 區段中，您可以看到 hello 目前未設定與網際網路對向端點和其目前狀態的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f61-200">In hello **Internet facing endpoints** section, you can see hello virtual machines that are currently configured with an Internet facing endpoint and its current status.</span></span>

![使用網際網路面向端點所設定的虛擬機器和狀態](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

<span data-ttu-id="d3f61-202">此資料表具有代表 hello 虛擬機器，hello 網際網路對向的 IP 位址的 hello 端點名稱和 hello 目前的網路安全性群組 hello 嚴重性狀態和 hello NGFW。</span><span class="sxs-lookup"><span data-stu-id="d3f61-202">This table has hello endpoint name that represents hello virtual machine, hello Internet facing IP address, and hello current severity status of hello network security group and hello NGFW.</span></span> <span data-ttu-id="d3f61-203">hello 表格是依嚴重性排序：</span><span class="sxs-lookup"><span data-stu-id="d3f61-203">hello table is sorted by severity:</span></span>

* <span data-ttu-id="d3f61-204">紅色 (在頂端)：高優先順序，應立即處理</span><span class="sxs-lookup"><span data-stu-id="d3f61-204">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="d3f61-205">橘色︰中等優先順序，應儘速處理</span><span class="sxs-lookup"><span data-stu-id="d3f61-205">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="d3f61-206">綠色 (最後一個)︰健康狀態</span><span class="sxs-lookup"><span data-stu-id="d3f61-206">Green (last one): Healthy state</span></span>

#### <a name="networking-topology-section"></a><span data-ttu-id="d3f61-207">網路拓撲區段</span><span class="sxs-lookup"><span data-stu-id="d3f61-207">Networking topology section</span></span>
<span data-ttu-id="d3f61-208">hello**網路拓樸**區段具有 hello 資源的階層式檢視中 hello 下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-208">hello **Networking topology** section has a hierarchical view of hello resources as shown in hello following screenshot:</span></span>

![網路拓撲區段中資源的階層式檢視](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

<span data-ttu-id="d3f61-210">此資料表是依嚴重性排序 (虛擬機器和子網路)︰</span><span class="sxs-lookup"><span data-stu-id="d3f61-210">This table is sorted (virtual machines and subnets) by severity:</span></span>

* <span data-ttu-id="d3f61-211">紅色 (在頂端)：高優先順序，應立即處理</span><span class="sxs-lookup"><span data-stu-id="d3f61-211">Red (on top): High priority and should be addressed immediately</span></span>
* <span data-ttu-id="d3f61-212">橘色︰中等優先順序，應儘速處理</span><span class="sxs-lookup"><span data-stu-id="d3f61-212">Orange: Medium priority and should be addressed as soon as possible</span></span>
* <span data-ttu-id="d3f61-213">綠色 (最後一個)︰健康狀態</span><span class="sxs-lookup"><span data-stu-id="d3f61-213">Green (last one): Healthy state</span></span>

<span data-ttu-id="d3f61-214">在此拓撲檢視中的 hello 第一個層級具有[虛擬網路](../virtual-network/virtual-networks-overview.md)，[虛擬網路閘道](/vpn-gateway/vpn-gateway-site-to-site-create.md)，和[虛擬網路 （傳統）](/virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f61-214">In this topology view, hello first level has [virtual networks](../virtual-network/virtual-networks-overview.md), [virtual network gateways](/vpn-gateway/vpn-gateway-site-to-site-create.md), and [virtual networks (classic)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> <span data-ttu-id="d3f61-215">hello 第二個層級的子網路，而且 hello 第三個層級 hello 隸屬 toothose 子網路的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="d3f61-215">hello second level has subnets, and hello third level has hello virtual machines that belong toothose subnets.</span></span> <span data-ttu-id="d3f61-216">hello 右邊的資料行具有 hello hello 網路安全性群組，為這些資源的目前狀態中 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="d3f61-216">hello right column has hello current status of hello network security group for those resources, as shown in hello following example:</span></span>

![Hello 網路安全性群組的 網路拓樸區段的狀態](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

<span data-ttu-id="d3f61-218">hello 此刀鋒視窗的下半部都有 hello 建議此虛擬機器，類似 toowhat 先前所述。</span><span class="sxs-lookup"><span data-stu-id="d3f61-218">hello bottom part of this blade has hello recommendations for this virtual machine, which is similar toowhat is described previously.</span></span> <span data-ttu-id="d3f61-219">您可以按一下 更多建議 toolearn 或套用 hello 所需的安全性控制或組態。</span><span class="sxs-lookup"><span data-stu-id="d3f61-219">You can click a recommendation toolearn more or apply hello needed security control or configuration.</span></span>

### <a name="monitor-storage--data"></a><span data-ttu-id="d3f61-220">監視儲存體和資料</span><span class="sxs-lookup"><span data-stu-id="d3f61-220">Monitor Storage & data</span></span>

<span data-ttu-id="d3f61-221">當您按一下**儲存體與資料**在 hello**防止**區段，hello**資料資源**刀鋒視窗中開啟 SQL 和儲存體的建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-221">When you click **Storage & data** in hello **Prevention** section, hello **Data Resources** blade opens with recommendations for SQL and Storage.</span></span> <span data-ttu-id="d3f61-222">它也有[建議](security-center-sql-service-recommendations.md)hello 一般健全狀況狀態的 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d3f61-222">It also has [recommendations](security-center-sql-service-recommendations.md) for hello general health state of hello database.</span></span> <span data-ttu-id="d3f61-223">如需儲存體加密的詳細資訊，請閱讀[在 Azure 資訊安全中心啟用 Azure 儲存體帳戶的加密](security-center-enable-encryption-for-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="d3f61-223">For more information about storage encryption, read [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md).</span></span>

![資料資源](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

<span data-ttu-id="d3f61-225">在下**SQL 建議**，您可以按一下任何建議以及取得更多相關詳細資料進一步的動作 tooresolve 發生問題。</span><span class="sxs-lookup"><span data-stu-id="d3f61-225">Under **SQL Recommendations**, You can click any recommendation and get more details about further action tooresolve an issue.</span></span> <span data-ttu-id="d3f61-226">hello 下列範例顯示 hello hello 擴充**SQL database 上的資料庫稽核與威脅偵測**建議。</span><span class="sxs-lookup"><span data-stu-id="d3f61-226">hello following example shows hello expansion of hello **Database Auditing & Threat detection on SQL databases** recommendation.</span></span>

![有關 SQL 建議的詳細資料](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

<span data-ttu-id="d3f61-228">hello **SQL 資料庫上的啟用稽核與威脅偵測**分頁有 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d3f61-228">hello **Enable Auditing & Threat detection on SQL databases** blade has hello following information:</span></span>

* <span data-ttu-id="d3f61-229">SQL 資料庫的清單</span><span class="sxs-lookup"><span data-stu-id="d3f61-229">A list of SQL databases</span></span>
* <span data-ttu-id="d3f61-230">hello 伺服器所在它們位於</span><span class="sxs-lookup"><span data-stu-id="d3f61-230">hello server on which they are located</span></span>
* <span data-ttu-id="d3f61-231">此設定是否繼承自 hello 伺服器，或如果它是唯一的這個資料庫中的相關資訊</span><span class="sxs-lookup"><span data-stu-id="d3f61-231">Information about whether this setting was inherited from hello server or if it is unique in this database</span></span>
* <span data-ttu-id="d3f61-232">hello 目前狀態</span><span class="sxs-lookup"><span data-stu-id="d3f61-232">hello current state</span></span>
* <span data-ttu-id="d3f61-233">hello hello 問題嚴重性</span><span class="sxs-lookup"><span data-stu-id="d3f61-233">hello severity of hello issue</span></span>

<span data-ttu-id="d3f61-234">當您按一下 hello 資料庫 tooaddress 這項建議時，hello**稽核與威脅偵測**刀鋒視窗會開啟 hello 遵循畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-234">When you click hello database tooaddress this recommendation, hello **Auditing & Threat detection** blade opens as shown in hello following screen.</span></span>

![稽核與威脅的偵測刀鋒視窗](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

<span data-ttu-id="d3f61-236">tooenable 稽核，選取**ON**下 hello**稽核**選項。</span><span class="sxs-lookup"><span data-stu-id="d3f61-236">tooenable auditing, select **ON** under hello **Auditing** option.</span></span>

### <a name="monitor-applications"></a><span data-ttu-id="d3f61-237">監視應用程式</span><span class="sxs-lookup"><span data-stu-id="d3f61-237">Monitor applications</span></span>

<span data-ttu-id="d3f61-238">如果您的 Azure 工作負載會有應用程式位於[（建立透過 Azure 資源管理員） 的虛擬機器](../azure-resource-manager/resource-manager-deployment-model.md)公開的 web 連接埠 （TCP 連接埠 80 和 443），與資訊安全中心可以監視這些 tooidentify 潛在的安全性問題並建議補救步驟。</span><span class="sxs-lookup"><span data-stu-id="d3f61-238">If your Azure workload has applications located in [virtual machines (created through Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) with exposed web ports (TCP ports 80 and 443), Security Center can monitor those tooidentify potential security issues and recommend remediation steps.</span></span> <span data-ttu-id="d3f61-239">當您按一下 hello**應用程式**磚，hello**應用程式**刀鋒視窗會開啟與 hello 中建議的一連串**應用程式建議**> 一節。</span><span class="sxs-lookup"><span data-stu-id="d3f61-239">When you click hello **Applications** tile, hello **Applications** blade opens with a series of recommendations in hello **Application recommendations** section.</span></span> <span data-ttu-id="d3f61-240">它也會顯示每個主機/虛擬 IP 的 hello 應用程式分解 hello 下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-240">It also shows hello application breakdown per host/virtual IP as shown in hello following screenshot.</span></span>

![應用程式安全性健全狀況](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

<span data-ttu-id="d3f61-242">就像您未與 hello 其他建議，您可以按一下建議 toosee 詳細 hello 問題及如何 tooremediate。</span><span class="sxs-lookup"><span data-stu-id="d3f61-242">Just like you did with hello other recommendations, you can click a recommendation toosee more details about hello issue and how tooremediate.</span></span> <span data-ttu-id="d3f61-243">hello hello 遵循圖所示的範例是已被識別為不安全的 web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d3f61-243">hello example shown in hello following figure is an application that was identified as an unsecure web application.</span></span> <span data-ttu-id="d3f61-244">當您選取已被視為不安全的 hello 應用程式時，另一個刀鋒視窗會開啟以 hello 下列可用的選項：</span><span class="sxs-lookup"><span data-stu-id="d3f61-244">When you select hello application that was considered not secure, another blade opens with hello following option available:</span></span>

![不安全之應用程式的相關詳細資料](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

<span data-ttu-id="d3f61-246">此刀鋒視窗會有此應用程式的所有建議清單。</span><span class="sxs-lookup"><span data-stu-id="d3f61-246">This blade will have a list of all recommendations for this application.</span></span> <span data-ttu-id="d3f61-247">當您按一下 hello**加入 web 應用程式防火牆**建議、 hello**加入 Web 應用程式防火牆**刀鋒視窗中開啟您 tooinstall 選項與 web 應用程式的防火牆 (WAF) 從合作夥伴擔任下列螢幕擷取畫面所示的 hello。</span><span class="sxs-lookup"><span data-stu-id="d3f61-247">When you click hello **Add a web application firewall** recommendation, hello **Add a Web Application Firewall** blade opens with options for you tooinstall a web application firewall (WAF) from a partner as shown in hello following screenshot.</span></span>

![新增 Web 應用程式防火牆對話方塊](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a><span data-ttu-id="d3f61-249">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d3f61-249">See also</span></span>
<span data-ttu-id="d3f61-250">在本文中，您學到如何 toouse 監視 Azure 資訊安全中心中的功能。</span><span class="sxs-lookup"><span data-stu-id="d3f61-250">In this article, you learned how toouse monitoring capabilities in Azure Security Center.</span></span> <span data-ttu-id="d3f61-251">toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="d3f61-251">toolearn more about Azure Security Center, see hello following:</span></span>

* <span data-ttu-id="d3f61-252">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)： 深入了解如何在 Azure 資訊安全中心 tooconfigure 安全性設定。</span><span class="sxs-lookup"><span data-stu-id="d3f61-252">[Setting security policies in Azure Security Center](security-center-policies.md): Learn how tooconfigure security settings in Azure Security Center.</span></span>
* <span data-ttu-id="d3f61-253">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)： 了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="d3f61-253">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md): Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="d3f61-254">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)： 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="d3f61-254">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md): Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="d3f61-255">[Azure 資訊安全中心常見問題集](security-center-faq.md)： 尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="d3f61-255">[Azure Security Center FAQ](security-center-faq.md): Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="d3f61-256">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)：尋找有關 Azure 安全性與相容性的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="d3f61-256">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/): Find blog posts about Azure security and compliance.</span></span>
