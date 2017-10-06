---
title: "aaaUse hello Operations Management Suite 中的服務對應方案 |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a><span data-ttu-id="abaeb-104">使用 Operations Management Suite 中的 hello 服務對應解決方案</span><span class="sxs-lookup"><span data-stu-id="abaeb-104">Use hello Service Map solution in Operations Management Suite</span></span>
<span data-ttu-id="abaeb-105">服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件和對應 hello 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-105">Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="abaeb-106">使用服務對應，您可以檢視您的伺服器，您會覺得 hello 方式： 做為傳送重要服務的互連系統。</span><span class="sxs-lookup"><span data-stu-id="abaeb-106">With Service Map, you can view your servers in hello way that you think of them: as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="abaeb-107">服務對應可顯示任何 TCP 連線架構跨伺服器、 處理程序與連接埠之間的連線，而不需要以外設定 hello 代理程式安裝。</span><span class="sxs-lookup"><span data-stu-id="abaeb-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required other than hello installation of an agent.</span></span>

<span data-ttu-id="abaeb-108">本文說明使用服務對應的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-108">This article describes hello details of using Service Map.</span></span> <span data-ttu-id="abaeb-109">如需設定服務對應和啟用代理程式的相關資訊，請參閱[在 Operations Management Suite 中設定服務對應解決方案](operations-management-suite-service-map-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-109">For information about configuring Service Map and onboarding agents, see [Configuring Service Map solution in Operations Management Suite](operations-management-suite-service-map-configure.md).</span></span>


## <a name="use-cases-make-your-it-processes-dependency-aware"></a><span data-ttu-id="abaeb-110">使用案例︰讓 IT 處理序可以感知相依性</span><span class="sxs-lookup"><span data-stu-id="abaeb-110">Use cases: Make your IT processes dependency aware</span></span>

### <a name="discovery"></a><span data-ttu-id="abaeb-111">探索</span><span class="sxs-lookup"><span data-stu-id="abaeb-111">Discovery</span></span>
<span data-ttu-id="abaeb-112">服務對應會自動建置跨伺服器、處理程序和協力廠商服務的一般相依性參考對應。</span><span class="sxs-lookup"><span data-stu-id="abaeb-112">Service Map automatically builds a common reference map of dependencies across your servers, processes, and third-party services.</span></span> <span data-ttu-id="abaeb-113">它會探索並將所有的 TCP 相依性，識別意外連線、 您而定，遠端協力廠商系統和相依性 tootraditional 深色區域網路，例如 Active Directory 的對應。</span><span class="sxs-lookup"><span data-stu-id="abaeb-113">It discovers and maps all TCP dependencies, identifying surprise connections, remote third-party systems you depend on, and dependencies tootraditional dark areas of your network, such as Active Directory.</span></span> <span data-ttu-id="abaeb-114">服務對應會探索受管理的系統嘗試 toomake，失敗的網路連線可幫助您識別潛在的伺服器設定不正確，服務中斷與網路問題。</span><span class="sxs-lookup"><span data-stu-id="abaeb-114">Service Map discovers failed network connections that your managed systems are attempting toomake, helping you identify potential server misconfiguration, service outage, and network issues.</span></span>

### <a name="incident-management"></a><span data-ttu-id="abaeb-115">事件管理</span><span class="sxs-lookup"><span data-stu-id="abaeb-115">Incident management</span></span>
<span data-ttu-id="abaeb-116">服務對應可協助避免問題隔離的 hello 猜測顯示連線系統的方式，並會影響彼此。</span><span class="sxs-lookup"><span data-stu-id="abaeb-116">Service Map helps eliminate hello guesswork of problem isolation by showing you how systems are connected and affecting each other.</span></span> <span data-ttu-id="abaeb-117">此外 tooidentifying 失敗的連線，它可協助識別設定不正確的負載平衡器、 令人意外或過度負載重要服務和 rogue 用戶端，例如交談 tooproduction 系統的程式開發人員電腦。</span><span class="sxs-lookup"><span data-stu-id="abaeb-117">In addition tooidentifying failed connections, it helps identify misconfigured load balancers, surprising or excessive load on critical services, and rogue clients, such as developer machines talking tooproduction systems.</span></span> <span data-ttu-id="abaeb-118">您可以使用整合式工作流程與 Operations Management Suite 變更追蹤，您也可以查看變更事件的後端的電腦或服務是否說明 hello 之事件的根本原因。</span><span class="sxs-lookup"><span data-stu-id="abaeb-118">By using integrated workflows with Operations Management Suite Change Tracking, you can also see whether a change event on a back-end machine or service explains hello root cause of an incident.</span></span>

### <a name="migration-assurance"></a><span data-ttu-id="abaeb-119">移轉保證</span><span class="sxs-lookup"><span data-stu-id="abaeb-119">Migration assurance</span></span>
<span data-ttu-id="abaeb-120">您可以使用服務對應，有效地規劃、加速和驗證 Azure 移轉，以確保沒有遺漏任何項目，且不會發生意外的中斷。</span><span class="sxs-lookup"><span data-stu-id="abaeb-120">By using Service Map, you can effectively plan, accelerate, and validate Azure migrations, which helps ensure that nothing is left behind and surprise outages do not occur.</span></span> <span data-ttu-id="abaeb-121">您可以探索所有交互相依系統的需求 toomigrate 一起、 評估系統組態和容量，以及識別是否執行中的系統仍然會提供使用者或適合用於而不移轉解除委任。</span><span class="sxs-lookup"><span data-stu-id="abaeb-121">You can discover all interdependent systems that need toomigrate together, assess system configuration and capacity, and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.</span></span> <span data-ttu-id="abaeb-122">Hello 移動完成之後，您可以檢查測試系統的用戶端負載和身分識別 tooverify 和客戶所連接。</span><span class="sxs-lookup"><span data-stu-id="abaeb-122">After hello move is complete, you can check on client load and identity tooverify that test systems and customers are connecting.</span></span> <span data-ttu-id="abaeb-123">如果子網路規劃與防火牆定義有問題，在服務對應對應中的連線失敗會為您需要連線的 toohello 系統。</span><span class="sxs-lookup"><span data-stu-id="abaeb-123">If your subnet planning and firewall definitions have issues, failed connections in Service Map maps point you toohello systems that need connectivity.</span></span>

### <a name="business-continuity"></a><span data-ttu-id="abaeb-124">業務持續性</span><span class="sxs-lookup"><span data-stu-id="abaeb-124">Business continuity</span></span>
<span data-ttu-id="abaeb-125">如果您使用 Azure Site Recovery 需要定義您的應用程式環境，服務對應的 hello 復原順序說明可能會自動告訴您如何系統依賴彼此 tooensure 修復計劃是可靠。</span><span class="sxs-lookup"><span data-stu-id="abaeb-125">If you are using Azure Site Recovery and need help defining hello recovery sequence for your application environment, Service Map can automatically show you how systems rely on each other tooensure that your recovery plan is reliable.</span></span> <span data-ttu-id="abaeb-126">藉由選擇的重要伺服器或群組，並檢視其用戶端，您可以識別哪些前端系統 toorecover hello 伺服器之後還原並在可用。</span><span class="sxs-lookup"><span data-stu-id="abaeb-126">By choosing a critical server or group and viewing its clients, you can identify which front-end systems toorecover after hello server is restored and available.</span></span> <span data-ttu-id="abaeb-127">相反地，藉由查看重要的伺服器端的相依性，您可以識別哪些系統 toorecover 焦點系統就會還原之前。</span><span class="sxs-lookup"><span data-stu-id="abaeb-127">Conversely, by looking at critical servers’ back-end dependencies, you can identify which systems toorecover before your focus systems are restored.</span></span>

### <a name="patch-management"></a><span data-ttu-id="abaeb-128">修補程式管理</span><span class="sxs-lookup"><span data-stu-id="abaeb-128">Patch management</span></span>
<span data-ttu-id="abaeb-129">服務對應，以顯示其他小組及伺服器相依於您的服務，因此您可以通知它們事先才進行修補系統增強 hello Operations Management Suite 系統更新評估貴用戶使用。</span><span class="sxs-lookup"><span data-stu-id="abaeb-129">Service Map enhances your use of hello Operations Management Suite System Update Assessment by showing you which other teams and servers depend on your service, so you can notify them in advance before you take down your systems for patching.</span></span> <span data-ttu-id="abaeb-130">服務對應也可以顯示您的服務在修補並重新啟動之後是否可用且正確連線，藉此加強 Operations Management Suite 中的修補程式管理。</span><span class="sxs-lookup"><span data-stu-id="abaeb-130">Service Map also enhances patch management in Operations Management Suite by showing you whether your services are available and properly connected after they are patched and restarted.</span></span>


## <a name="mapping-overview"></a><span data-ttu-id="abaeb-131">對應概觀</span><span class="sxs-lookup"><span data-stu-id="abaeb-131">Mapping overview</span></span>
<span data-ttu-id="abaeb-132">服務對應的代理程式收集 hello 與伺服器上安裝這些詳細 hello 每個處理序的輸入及輸出連線 TCP 連線的所有處理序的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-132">Service Map agents gather information about all TCP-connected processes on hello server where they’re installed and details about hello inbound and outbound connections for each process.</span></span> <span data-ttu-id="abaeb-133">在 hello 清單中 hello 左窗格中，您可以選取電腦或群組都在指定的時間範圍內有服務對應的代理程式 toovisualize 及其相依性。</span><span class="sxs-lookup"><span data-stu-id="abaeb-133">In hello list in hello left pane, you can select machines or groups that have Service Map agents toovisualize their dependencies over a specified time range.</span></span> <span data-ttu-id="abaeb-134">機器相依性會對應專注於特定的電腦，而它們會顯示所有 hello 機器直接 TCP 用戶端或伺服器的電腦。</span><span class="sxs-lookup"><span data-stu-id="abaeb-134">Machine dependency maps focus on a specific machine, and they show all hello machines that are direct TCP clients or servers of that machine.</span></span>  <span data-ttu-id="abaeb-135">機器群組對應會顯示多組伺服器及其相依性。</span><span class="sxs-lookup"><span data-stu-id="abaeb-135">Machine Group maps show sets of servers and their dependencies.</span></span>

![服務對應概觀](media/oms-service-map/service-map-overview.png)

<span data-ttu-id="abaeb-137">擴充機器 hello 對應 tooshow hello 與作用中的網路連線執行處理程序在 hello 選取時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="abaeb-137">Machines can be expanded in hello map tooshow hello running processes with active network connections during hello selected time range.</span></span> <span data-ttu-id="abaeb-138">展開的 tooshow 程序的詳細資料與服務對應的代理程式在遠端電腦時，只有與 hello 焦點機器進行通訊的處理序才會顯示。</span><span class="sxs-lookup"><span data-stu-id="abaeb-138">When a remote machine with a Service Map agent is expanded tooshow process details, only those processes that communicate with hello focus machine are shown.</span></span> <span data-ttu-id="abaeb-139">無代理程式連接成 hello 焦點機器的前端機器 hello 計數會指出左邊 hello hello 處理程序連線到。</span><span class="sxs-lookup"><span data-stu-id="abaeb-139">hello count of agentless front-end machines that connect into hello focus machine is indicated on hello left side of hello processes they connect to.</span></span> <span data-ttu-id="abaeb-140">如果 hello 焦點機器正在未代理程式連線 tooa 後端的電腦，hello 後端伺服器包含在伺服器連接埠群組，以及其他連接 toohello 相同連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="abaeb-140">If hello focus machine is making a connection tooa back-end machine that has no agent, hello back-end server is included in a Server Port Group, along with other connections toohello same port number.</span></span>

<span data-ttu-id="abaeb-141">根據預設，服務對應對應顯示 hello 30 分鐘的相依性資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-141">By default, Service Map maps show hello last 30 minutes of dependency information.</span></span> <span data-ttu-id="abaeb-142">Hello 階段控制項在 hello 左上方，您可以使用查詢的歷程記錄的時間範圍的總 tooone 小時 tooshow hello 中尋找相依性的如何對應過去 （例如，在事件或變更發生之前）。</span><span class="sxs-lookup"><span data-stu-id="abaeb-142">By using hello time controls at hello upper left, you can query maps for historical time ranges of up tooone hour tooshow how dependencies looked in hello past (for example, during an incident or before a change occurred).</span></span> <span data-ttu-id="abaeb-143">付費工作區的服務對應資料會儲存 30 天，免費工作區的服務對應資料則會儲存 7 天。</span><span class="sxs-lookup"><span data-stu-id="abaeb-143">Service Map data is stored for 30 days in paid workspaces, and for 7 days in free workspaces.</span></span>

## <a name="status-badges-and-border-coloring"></a><span data-ttu-id="abaeb-144">狀態徽章和框線色彩</span><span class="sxs-lookup"><span data-stu-id="abaeb-144">Status badges and border coloring</span></span>
<span data-ttu-id="abaeb-145">在 hello 底部 hello 對應中的每一部伺服器可以是一份狀態徽章傳達 hello 伺服器的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-145">At hello bottom of each server in hello map can be a list of status badges conveying status information about hello server.</span></span> <span data-ttu-id="abaeb-146">hello 徽章指出有某些 hello 伺服器從一個 hello Operations Management Suite 方案整合的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-146">hello badges indicate that there is some relevant information for hello server from one of hello Operations Management Suite solution integrations.</span></span> <span data-ttu-id="abaeb-147">按一下徽章會引導您直接 toohello hello 狀態詳細資料 hello 右窗格中。</span><span class="sxs-lookup"><span data-stu-id="abaeb-147">Clicking a badge takes you directly toohello details of hello status in hello right pane.</span></span> <span data-ttu-id="abaeb-148">hello 目前可用的狀態徽章包括警示、 服務台、 變更、 安全性和更新。</span><span class="sxs-lookup"><span data-stu-id="abaeb-148">hello currently available status badges include Alerts, Service Desk, Changes, Security, and Updates.</span></span>

<span data-ttu-id="abaeb-149">Hello 狀態徽章 hello 嚴重性，根據機器節點框線彩色紅色 （重大），黃色 （警告），或是藍色 （資訊）。</span><span class="sxs-lookup"><span data-stu-id="abaeb-149">Depending on hello severity of hello status badges, machine node borders can be colored red (critical), yellow (warning), or blue (informational).</span></span> <span data-ttu-id="abaeb-150">hello 色彩都代表任何 hello 狀態徽章的 hello 最嚴重狀態。</span><span class="sxs-lookup"><span data-stu-id="abaeb-150">hello color represents hello most severe status of any of hello status badges.</span></span> <span data-ttu-id="abaeb-151">灰色框線代表沒有狀態指標的節點。</span><span class="sxs-lookup"><span data-stu-id="abaeb-151">A gray border indicates a node that has no status indicators.</span></span>

![狀態徽章](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a><span data-ttu-id="abaeb-153">機器群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-153">Machine Groups</span></span>
<span data-ttu-id="abaeb-154">電腦群組可讓您 toosee 對應集中在一組伺服器，不只一個，才可看到的一個對應中的多層式應用程式或伺服器叢集的所有 hello 成員。</span><span class="sxs-lookup"><span data-stu-id="abaeb-154">Machine Groups allow you toosee maps centered around a set of servers, not just one so you can see all hello members of a multi-tier application or server cluster in one map.</span></span>

<span data-ttu-id="abaeb-155">使用者選取的伺服器屬於群組在一起，並選擇 hello 群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="abaeb-155">Users select which servers belong in a group together and choose a name for hello group.</span></span>  <span data-ttu-id="abaeb-156">然後，您可以選擇 tooview hello 群組的所有處理程序和連線，或檢視只有 hello 處理程序和連線的直接關聯 toohello hello 群組的其他成員。</span><span class="sxs-lookup"><span data-stu-id="abaeb-156">You can then choose tooview hello group with all of its processes and connections, or view it with only hello processes and connections that directly relate toohello other members of hello group.</span></span>

![機器群組](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a><span data-ttu-id="abaeb-158">建立機器群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-158">Creating a Machine Group</span></span>
<span data-ttu-id="abaeb-159">toocreate 群組、 選取 hello 電腦您要在 hello 機器清單，然後按一下**新增 toogroup**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-159">toocreate a group, select hello machine or machines you want in hello Machines list and click **Add toogroup**.</span></span>

![建立群組](media/oms-service-map/machine-groups-create.png)

<span data-ttu-id="abaeb-161">您可以選擇**建立新**為 hello 群組命名。</span><span class="sxs-lookup"><span data-stu-id="abaeb-161">There, you can choose **Create new** and give hello group a name.</span></span>

![為群組命名](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
><span data-ttu-id="abaeb-163">電腦群組目前限制的 too10 伺服器，但我們計劃 tooincrease 這項限制推出。</span><span class="sxs-lookup"><span data-stu-id="abaeb-163">Machine groups are currently limited too10 servers, but we plan tooincrease this limit soon.</span></span>

### <a name="viewing-a-group"></a><span data-ttu-id="abaeb-164">檢視群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-164">Viewing a Group</span></span>
<span data-ttu-id="abaeb-165">一旦您已建立一些群組，您可以選擇 hello 群組 索引標籤中檢視它們。</span><span class="sxs-lookup"><span data-stu-id="abaeb-165">Once you’ve created some groups, you can view them by choosing hello Groups tab.</span></span>

![[群組] 索引標籤](media/oms-service-map/machine-groups-tab.png)

<span data-ttu-id="abaeb-167">該電腦群組，然後選取 hello 群組名稱 tooview hello 對應。</span><span class="sxs-lookup"><span data-stu-id="abaeb-167">Then select hello Group name tooview hello map for that Machine Group.</span></span>
<span data-ttu-id="abaeb-168">![電腦群組](media/oms-service-map/machine-group.png)hello 機器屬於 toohello 群組所述 hello 對應中的白色。</span><span class="sxs-lookup"><span data-stu-id="abaeb-168">![Machine Group](media/oms-service-map/machine-group.png) hello machines that belong toohello group are outlined in white in hello map.</span></span>

<span data-ttu-id="abaeb-169">擴充 hello 群組會列出組成 hello 機器群組的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="abaeb-169">Expanding hello Group will list hello machines that make up hello Machine Group.</span></span>

![機器群組的機器](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a><span data-ttu-id="abaeb-171">依處理序篩選</span><span class="sxs-lookup"><span data-stu-id="abaeb-171">Filter by processes</span></span>
<span data-ttu-id="abaeb-172">您可以切換顯示 hello 群組中的所有處理程序和連線之間的 hello 地圖檢視，並只 hello 的直接關聯 toohello 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="abaeb-172">You can toggle hello map view between showing all processes and connections in hello Group and only hello ones that directly relate toohello Machine Group.</span></span>  <span data-ttu-id="abaeb-173">hello 預設檢視是 tooshow 所有處理程序。</span><span class="sxs-lookup"><span data-stu-id="abaeb-173">hello default view is tooshow all processes.</span></span>  <span data-ttu-id="abaeb-174">您可以在 hello 上方 hello 地圖的篩選圖示，即可變更 hello 檢視。</span><span class="sxs-lookup"><span data-stu-id="abaeb-174">You can change hello view by clicking hello filter icon above hello map.</span></span>

![篩選群組](media/oms-service-map/machine-groups-filter.png)

<span data-ttu-id="abaeb-176">當**所有處理程序**已選取，hello 對應會包含所有處理程序和每部 hello 電腦上的連線 hello 群組中。</span><span class="sxs-lookup"><span data-stu-id="abaeb-176">When **All processes** is selected, hello map will include all processes and connections on each of hello machines in hello Group.</span></span>

![機器群組的所有處理序](media/oms-service-map/machine-groups-all.png)

<span data-ttu-id="abaeb-178">如果您變更只 hello 檢視 tooshow**群組連線處理程序**，會縮小 hello 對應 tooonly 向這些處理程序和連線的直接連接 tooother 機器 hello 群組中建立的簡化的檢視。</span><span class="sxs-lookup"><span data-stu-id="abaeb-178">If you change hello view tooshow only **group-connected processes**, hello map will be narrowed down tooonly those processes and connections that are directly connected tooother machines in hello group, creating a simplified view.</span></span>

![機器群組的已篩選處理序](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a><span data-ttu-id="abaeb-180">新增機器 tooa 群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-180">Adding machines tooa group</span></span>
<span data-ttu-id="abaeb-181">tooadd 機器 tooan 現有的群組，請檢查 hello 方塊，然後再按一下 下一步的 toohello 機器**新增 toogroup**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-181">tooadd machines tooan existing group, check hello boxes next toohello machines you want and then click **Add toogroup**.</span></span>  <span data-ttu-id="abaeb-182">然後，選擇要 tooadd hello 機器 hello 群組。</span><span class="sxs-lookup"><span data-stu-id="abaeb-182">Then, choose hello group you want tooadd hello machines to.</span></span>
 
### <a name="removing-machines-from-a-group"></a><span data-ttu-id="abaeb-183">從群組移除多部機器</span><span class="sxs-lookup"><span data-stu-id="abaeb-183">Removing machines from a group</span></span>
<span data-ttu-id="abaeb-184">在 hello 群組 清單中，展開 hello 群組名稱 toolist hello 機器 hello 電腦群組中。</span><span class="sxs-lookup"><span data-stu-id="abaeb-184">In hello Groups List, expand hello group name toolist hello machines in hello Machine Group.</span></span>  <span data-ttu-id="abaeb-185">然後，按一下 hello 省略符號功能表下一步 toohello 機器 tooremove 並選擇**移除**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-185">Then, click on hello ellipsis menu next toohello machine you want tooremove and choose **Remove**.</span></span>

![從群組移除機器](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a><span data-ttu-id="abaeb-187">移除或重新命名群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-187">Removing or renaming a group</span></span>
<span data-ttu-id="abaeb-188">按一下 hello 省略符號功能表下一步 toohello 群組名稱在 hello 群組清單中。</span><span class="sxs-lookup"><span data-stu-id="abaeb-188">Click on hello ellipsis menu next toohello group name in hello Group List.</span></span>

![機器群組功能表](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a><span data-ttu-id="abaeb-190">角色圖示</span><span class="sxs-lookup"><span data-stu-id="abaeb-190">Role icons</span></span>
<span data-ttu-id="abaeb-191">某些處理序在機器上扮演特殊角色︰Web 伺服器、應用程式伺服器及資料庫等。</span><span class="sxs-lookup"><span data-stu-id="abaeb-191">Certain processes serve particular roles on machines: web servers, application servers, database, and so on.</span></span> <span data-ttu-id="abaeb-192">服務對應程序加上附註，並識別概覽 hello 角色處理程序或伺服器上所扮演的角色圖示 toohelp 機器方塊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-192">Service Map annotates process and machine boxes with role icons toohelp identify at a glance hello role a process or server plays.</span></span>

| <span data-ttu-id="abaeb-193">角色圖示</span><span class="sxs-lookup"><span data-stu-id="abaeb-193">Role icon</span></span> | <span data-ttu-id="abaeb-194">說明</span><span class="sxs-lookup"><span data-stu-id="abaeb-194">Description</span></span> |
|:--|:--|
| ![Web 伺服器](media/oms-service-map/role-web-server.png) | <span data-ttu-id="abaeb-196">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="abaeb-196">Web server</span></span> |
| ![應用程式伺服器](media/oms-service-map/role-application-server.png) | <span data-ttu-id="abaeb-198">應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="abaeb-198">Application server</span></span> |
| ![資料庫伺服器](media/oms-service-map/role-database.png) | <span data-ttu-id="abaeb-200">資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="abaeb-200">Database server</span></span> |
| ![LDAP 伺服器](media/oms-service-map/role-ldap.png) | <span data-ttu-id="abaeb-202">LDAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="abaeb-202">LDAP server</span></span> |
| ![SMB 伺服器](media/oms-service-map/role-smb.png) | <span data-ttu-id="abaeb-204">SMB 伺服器</span><span class="sxs-lookup"><span data-stu-id="abaeb-204">SMB server</span></span> |

![角色圖示](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a><span data-ttu-id="abaeb-206">失敗的連線</span><span class="sxs-lookup"><span data-stu-id="abaeb-206">Failed connections</span></span>
<span data-ttu-id="abaeb-207">失敗的連線會顯示在服務對應的對應處理程序和電腦，並以紅色虛線指出用戶端系統失敗 tooreach 程序或連接埠。</span><span class="sxs-lookup"><span data-stu-id="abaeb-207">Failed connections are shown in Service Map maps for processes and computers, with a dashed red line indicating that a client system is failing tooreach a process or port.</span></span> <span data-ttu-id="abaeb-208">如果該系統是 hello 一個嘗試 hello 無法連線，連線失敗會報告從任何具有已部署的服務對應代理程式的系統。</span><span class="sxs-lookup"><span data-stu-id="abaeb-208">Failed connections are reported from any system with a deployed Service Map agent if that system is hello one attempting hello failed connection.</span></span> <span data-ttu-id="abaeb-209">服務對應觀察失敗 tooestablish 的 TCP 通訊端連線的測量此處理程序。</span><span class="sxs-lookup"><span data-stu-id="abaeb-209">Service Map measures this process by observing TCP sockets that fail tooestablish a connection.</span></span> <span data-ttu-id="abaeb-210">此失敗可能源自防火牆後面，hello 用戶端或伺服器中設定不正確或無法使用遠端服務。</span><span class="sxs-lookup"><span data-stu-id="abaeb-210">This failure could result from a firewall, a misconfiguration in hello client or server, or a remote service being unavailable.</span></span>

![失敗的連線](media/oms-service-map/failed-connections.png)

<span data-ttu-id="abaeb-212">了解失敗的連線有助於疑難排解、移轉驗證、安全性分析和整體架構理解。</span><span class="sxs-lookup"><span data-stu-id="abaeb-212">Understanding failed connections can help with troubleshooting, migration validation, security analysis, and overall architectural understanding.</span></span> <span data-ttu-id="abaeb-213">失敗的連接有時候無害的但它們通常指直接 tooa 問題，例如容錯移轉環境突然變得無法存取或無法 tootalk 正在雲端移轉後的兩個應用程式層級。</span><span class="sxs-lookup"><span data-stu-id="abaeb-213">Failed connections are sometimes harmless, but they often point directly tooa problem, such as a failover environment suddenly becoming unreachable, or two application tiers being unable tootalk after a cloud migration.</span></span>

## <a name="client-groups"></a><span data-ttu-id="abaeb-214">用戶端群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-214">Client Groups</span></span>
<span data-ttu-id="abaeb-215">用戶端群組是在 hello 地圖上代表沒有相依性代理程式的用戶端電腦的方塊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-215">Client Groups are boxes on hello map that represent client machines that do not have Dependency Agents.</span></span> <span data-ttu-id="abaeb-216">單一用戶端群組代表 hello 的個別處理序或電腦的用戶端。</span><span class="sxs-lookup"><span data-stu-id="abaeb-216">A single Client Group represents hello clients for an individual process or machine.</span></span>

![用戶端群組](media/oms-service-map/client-groups.png)

<span data-ttu-id="abaeb-218">toosee hello 的用戶端群組選取 hello 群組中的 hello 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="abaeb-218">toosee hello IP addresses of hello servers in a Client Group, select hello group.</span></span> <span data-ttu-id="abaeb-219">hello 群組的 hello 內容會列在 hello**用戶端群組內容**窗格。</span><span class="sxs-lookup"><span data-stu-id="abaeb-219">hello contents of hello group are listed in hello **Client Group Properties** pane.</span></span>

![用戶端群組屬性](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a><span data-ttu-id="abaeb-221">伺服器連接埠群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-221">Server Port Groups</span></span>
<span data-ttu-id="abaeb-222">伺服器連接埠群組是方塊，代表沒有相依性代理程式的伺服器上的伺服器連接埠。</span><span class="sxs-lookup"><span data-stu-id="abaeb-222">Server Port Groups are boxes that represent server ports on servers that do not have Dependency Agents.</span></span> <span data-ttu-id="abaeb-223">hello 方塊包含 hello 伺服器連接埠以及連線 toothat 通訊埠與伺服器的 hello 數目的計數。</span><span class="sxs-lookup"><span data-stu-id="abaeb-223">hello box contains hello server port and a count of hello number of servers with connections toothat port.</span></span> <span data-ttu-id="abaeb-224">展開 hello 方塊 toosee hello 個別伺服器和連接。</span><span class="sxs-lookup"><span data-stu-id="abaeb-224">Expand hello box toosee hello individual servers and connections.</span></span> <span data-ttu-id="abaeb-225">如果在 [hello] 方塊中只有一部伺服器，會列出 hello 名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="abaeb-225">If there is only one server in hello box, hello name or IP address is listed.</span></span>

![伺服器連接埠群組](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a><span data-ttu-id="abaeb-227">內容功能表</span><span class="sxs-lookup"><span data-stu-id="abaeb-227">Context menu</span></span>
<span data-ttu-id="abaeb-228">按一下頂端 hello hello 省略符號 （...） 的任何伺服器的權限會顯示 hello 內容功能表，該伺服器。</span><span class="sxs-lookup"><span data-stu-id="abaeb-228">Clicking hello ellipsis (...) at hello top right of any server displays hello context menu for that server.</span></span>

![失敗的連線](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a><span data-ttu-id="abaeb-230">載入伺服器對應</span><span class="sxs-lookup"><span data-stu-id="abaeb-230">Load server map</span></span>
<span data-ttu-id="abaeb-231">按一下**負載 Server 對應**會帶您 tooa hello 選取的伺服器做為新焦點機器 hello 與新的對應。</span><span class="sxs-lookup"><span data-stu-id="abaeb-231">Clicking **Load Server Map** takes you tooa new map with hello selected server as hello new focus machine.</span></span>

### <a name="show-self-links"></a><span data-ttu-id="abaeb-232">顯示自我連結</span><span class="sxs-lookup"><span data-stu-id="abaeb-232">Show self-links</span></span>
<span data-ttu-id="abaeb-233">按一下**顯示 Self-Links**重繪 hello 伺服器節點，包括任何自我連結，這些是 TCP 連線的開始及結束於 hello 伺服器中的程序。</span><span class="sxs-lookup"><span data-stu-id="abaeb-233">Clicking **Show Self-Links** redraws hello server node, including any self-links, which are TCP connections that start and end on processes within hello server.</span></span> <span data-ttu-id="abaeb-234">如果自我連結會顯示，太 hello 功能表命令變更**隱藏 Self-Links**，如此一來，您可以將它們關閉。</span><span class="sxs-lookup"><span data-stu-id="abaeb-234">If self-links are shown, hello menu command changes too**Hide Self-Links**, so that you can turn them off.</span></span>

## <a name="computer-summary"></a><span data-ttu-id="abaeb-235">電腦摘要</span><span class="sxs-lookup"><span data-stu-id="abaeb-235">Computer summary</span></span>
<span data-ttu-id="abaeb-236">hello**機器摘要**窗格包含伺服器的作業系統、 相依性計數，以及資料從其他的 Operations Management Suite 方案的概觀。</span><span class="sxs-lookup"><span data-stu-id="abaeb-236">hello **Machine Summary** pane includes an overview of a server's operating system, dependency counts, and data from other Operations Management Suite solutions.</span></span> <span data-ttu-id="abaeb-237">這些資料包括效能計量、服務台票證、變更追蹤、安全性和更新。</span><span class="sxs-lookup"><span data-stu-id="abaeb-237">Such data includes performance metrics, service desk tickets, change tracking, security, and updates.</span></span>

![[機器摘要] 窗格](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a><span data-ttu-id="abaeb-239">電腦和處理序屬性</span><span class="sxs-lookup"><span data-stu-id="abaeb-239">Computer and process properties</span></span>
<span data-ttu-id="abaeb-240">當您巡覽服務對應圖時，您可以選取機器和處理序 toogain 有關的其他內容及其屬性。</span><span class="sxs-lookup"><span data-stu-id="abaeb-240">When you navigate a Service Map map, you can select machines and processes toogain additional context about their properties.</span></span> <span data-ttu-id="abaeb-241">機器提供 DNS 名稱、 IPv4 位址、 CPU 和記憶體容量、 VM 類型、 作業系統和版本，最後重新啟動時間和 hello 識別碼及其 Operations Management Suite 和服務對應的代理程式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-241">Machines provide information about DNS name, IPv4 addresses, CPU and memory capacity, VM type, operating system and version, last reboot time, and hello IDs of their Operations Management Suite and Service Map agents.</span></span>

![[機器屬性] 窗格](media/oms-service-map/machine-properties.png)

<span data-ttu-id="abaeb-243">處理序詳細資料是收集自作業系統中繼資料，其內容與執行中的處理序有關，包括處理序名稱、處理序描述、使用者名稱和網域 (在 Windows 上)、公司名稱、產品名稱、產品版本、工作目錄、命令列，以及處理序開始時間。</span><span class="sxs-lookup"><span data-stu-id="abaeb-243">You can gather process details from operating-system metadata about running processes, including process name, process description, user name and domain (on Windows), company name, product name, product version, working directory, command line, and process start time.</span></span>

![[處理序屬性] 窗格](media/oms-service-map/process-properties.png)

<span data-ttu-id="abaeb-245">hello**程序摘要**窗格提供 hello 處理序的連線，包括其繫結連接埠、 輸入及輸出連線的其他資訊和失敗的連線。</span><span class="sxs-lookup"><span data-stu-id="abaeb-245">hello **Process Summary** pane provides additional information about hello process’s connectivity, including its bound ports, inbound and outbound connections, and failed connections.</span></span>

![[處理序摘要] 窗格](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a><span data-ttu-id="abaeb-247">Operations Management Suite 警示整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-247">Operations Management Suite Alerts integration</span></span>
<span data-ttu-id="abaeb-248">服務對應整合與 hello 選取時間範圍中的 hello 選伺服器的 Operations Management Suite 警示 tooshow 引發警示。</span><span class="sxs-lookup"><span data-stu-id="abaeb-248">Service Map integrates with Operations Management Suite Alerts tooshow fired alerts for hello selected server in hello selected time range.</span></span> <span data-ttu-id="abaeb-249">hello 伺服器顯示的圖示，如果沒有目前的警示和 hello**機器警示**窗格會列出 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="abaeb-249">hello server displays an icon if there are current alerts, and hello **Machine Alerts** pane lists hello alerts.</span></span>

![[機器警示] 窗格](media/oms-service-map/machine-alerts.png)

<span data-ttu-id="abaeb-251">tooenable 服務對應 toodisplay 相關警示，會建立警示規則引發特定的電腦。</span><span class="sxs-lookup"><span data-stu-id="abaeb-251">tooenable Service Map toodisplay relevant alerts, create an alert rule that fires for a specific computer.</span></span> <span data-ttu-id="abaeb-252">toocreate 適當的警示：</span><span class="sxs-lookup"><span data-stu-id="abaeb-252">toocreate proper alerts:</span></span>
- <span data-ttu-id="abaeb-253">包含子句 toogroup 電腦 (例如，**電腦間隔為 1 分鐘**)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-253">Include a clause toogroup by computer (for example, **by Computer interval 1minute**).</span></span>
- <span data-ttu-id="abaeb-254">選擇 tooalert 根據度量的度量。</span><span class="sxs-lookup"><span data-stu-id="abaeb-254">Choose tooalert based on metric measurement.</span></span>

![警示組態](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a><span data-ttu-id="abaeb-256">Operations Management Suite 記錄事件整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-256">Operations Management Suite log events integration</span></span>
<span data-ttu-id="abaeb-257">服務對應與整合記錄搜尋 tooshow hello 選伺服器的所有可用的記錄事件計數 hello 選取時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="abaeb-257">Service Map integrates with Log Search tooshow a count of all available log events for hello selected server during hello selected time range.</span></span> <span data-ttu-id="abaeb-258">您可以按一下 hello 清單中的事件計數 toojump tooLog 搜尋任何資料列，並查看 hello 個別記錄事件。</span><span class="sxs-lookup"><span data-stu-id="abaeb-258">You can click any row in hello list of event counts toojump tooLog Search and see hello individual log events.</span></span>

![[機器記錄事件] 窗格](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a><span data-ttu-id="abaeb-260">Operations Management Suite 服務台整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-260">Operations Management Suite Service Desk integration</span></span>
<span data-ttu-id="abaeb-261">在這兩種解決方案都已啟用並設定您的 Operations Management Suite 工作區中，而自動與 hello IT 服務管理連接器的服務對應整合。</span><span class="sxs-lookup"><span data-stu-id="abaeb-261">Service Map integration with hello IT Service Management Connector is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span> <span data-ttu-id="abaeb-262">服務對應中的 hello 整合會標示為 「 服務台。 」</span><span class="sxs-lookup"><span data-stu-id="abaeb-262">hello integration in Service Map is labeled "Service Desk."</span></span> <span data-ttu-id="abaeb-263">如需詳細資訊，請參閱[使用 IT 服務管理連接器將 ITSM 工作項目集中管理](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-263">For more information, see [Centrally manage ITSM work items using IT Service Management Connector](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).</span></span>

<span data-ttu-id="abaeb-264">hello**機器服務台**窗格會列出所有 hello 選伺服器 hello 選取時間範圍內的 IT 服務管理事件。</span><span class="sxs-lookup"><span data-stu-id="abaeb-264">hello **Machine Service Desk** pane lists all IT Service Management events for hello selected server in hello selected time range.</span></span> <span data-ttu-id="abaeb-265">如果沒有目前的項目和 hello 機器服務台窗格會列出這些 hello 伺服器就會顯示圖示。</span><span class="sxs-lookup"><span data-stu-id="abaeb-265">hello server displays an icon if there are current items and hello Machine Service Desk pane lists them.</span></span>

![[機器服務台] 窗格](media/oms-service-map/service-desk.png)

<span data-ttu-id="abaeb-267">tooopen hello 項目，在您連接 ITSM 解決方案中，按一下**檢視工作項目**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-267">tooopen hello item in your connected ITSM solution, click **View Work Item**.</span></span>

<span data-ttu-id="abaeb-268">按一下 記錄搜尋中的 hello 項目的 tooview hello 詳細資料**記錄搜尋中顯示**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-268">tooview hello details of hello item in Log Search, click **Show in Log Search**.</span></span>


## <a name="operations-management-suite-change-tracking-integration"></a><span data-ttu-id="abaeb-269">Operations Management Suite 變更追蹤整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-269">Operations Management Suite Change Tracking integration</span></span>
<span data-ttu-id="abaeb-270">當「服務對應」和「變更追蹤」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="abaeb-270">Service Map integration with Change Tracking is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="abaeb-271">hello**機器變更追蹤**窗格會列出所有變更，以最新的 hello 第一次，以及連結 toodrill 向 tooLog 搜尋其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-271">hello **Machine Change Tracking** pane lists all changes, with hello most recent first, along with a link toodrill down tooLog Search for additional details.</span></span>

![[機器變更追蹤] 窗格](media/oms-service-map/change-tracking.png)

<span data-ttu-id="abaeb-273">hello 以下影像是您可能會看到 ConfigurationChange 事件的詳細的檢視選取後**顯示在 記錄分析**。</span><span class="sxs-lookup"><span data-stu-id="abaeb-273">hello following image is a detailed view of a ConfigurationChange event that you might see after you select **Show in Log Analytics**.</span></span>

![ConfigurationChange 事件](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a><span data-ttu-id="abaeb-275">Operations Management Suite 效能整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-275">Operations Management Suite performance integration</span></span>
<span data-ttu-id="abaeb-276">hello**機器效能** 窗格會顯示 hello 選伺服器的標準效能度量。</span><span class="sxs-lookup"><span data-stu-id="abaeb-276">hello **Machine Performance** pane displays standard performance metrics for hello selected server.</span></span> <span data-ttu-id="abaeb-277">hello 度量包括 CPU 使用率、 記憶體使用量、 網路傳送和接收的位元組和一份 hello 上層處理程序，透過網路傳送和接收的位元組。</span><span class="sxs-lookup"><span data-stu-id="abaeb-277">hello metrics include CPU utilization, memory utilization, network bytes sent and received, and a list of hello top processes by network bytes sent and received.</span></span> <span data-ttu-id="abaeb-278">tooget hello 網路效能資料，您也必須啟用 hello Operations Management Suite 中的網路資料 2.0 方案。</span><span class="sxs-lookup"><span data-stu-id="abaeb-278">tooget hello network performance data, you must also have enabled hello Wire Data 2.0 solution in Operations Management Suite.</span></span>

![[機器效能] 窗格](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a><span data-ttu-id="abaeb-280">Operations Management Suite 安全性整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-280">Operations Management Suite Security integration</span></span>
<span data-ttu-id="abaeb-281">當「服務對應」和「安全性與稽核」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="abaeb-281">Service Map integration with Security and Audit is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="abaeb-282">hello**機器安全性** 窗格會顯示 hello hello 選伺服器的 Operations Management Suite 安全性和稽核解決方案的資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-282">hello **Machine Security** pane shows data from hello Operations Management Suite Security and Audit solution for hello selected server.</span></span> <span data-ttu-id="abaeb-283">hello 窗格會列出 hello 選取時間範圍內任何未處理的安全性問題 hello 伺服器的摘要。</span><span class="sxs-lookup"><span data-stu-id="abaeb-283">hello pane lists a summary of any outstanding security issues for hello server during hello selected time range.</span></span> <span data-ttu-id="abaeb-284">按一下任何 hello 安全性問題的演習向下到記錄檔中搜尋相關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-284">Clicking any of hello security issues drills down into a Log Search for details about them.</span></span>

![[機器安全性] 窗格](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a><span data-ttu-id="abaeb-286">Operations Management Suite 更新整合</span><span class="sxs-lookup"><span data-stu-id="abaeb-286">Operations Management Suite Updates integration</span></span>
<span data-ttu-id="abaeb-287">當「服務對應」和「更新管理」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="abaeb-287">Service Map integration with Update Management is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="abaeb-288">hello**機器更新** 窗格會顯示 hello hello 選伺服器的 Operations Management Suite 更新管理方案的資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-288">hello **Machine Updates** pane displays data from hello Operations Management Suite Update Management solution for hello selected server.</span></span> <span data-ttu-id="abaeb-289">hello 窗格會列出任何遺失的更新伺服器 hello 摘要 hello 選取時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="abaeb-289">hello pane lists a summary of any missing updates for hello server during hello selected time range.</span></span>

![[機器變更追蹤] 窗格](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a><span data-ttu-id="abaeb-291">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="abaeb-291">Log Analytics records</span></span>
<span data-ttu-id="abaeb-292">服務對應的電腦和處理序清查資料可供在 Log Analytics 中進行[搜尋](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-292">Service Map computer and process inventory data is available for [search](../log-analytics/log-analytics-log-searches.md) in Log Analytics.</span></span> <span data-ttu-id="abaeb-293">您可以套用這個資料 tooscenarios 包含移轉規劃、 容量分析、 探索與視需要效能疑難排解。</span><span class="sxs-lookup"><span data-stu-id="abaeb-293">You can apply this data tooscenarios that include migration planning, capacity analysis, discovery, and on-demand performance troubleshooting.</span></span>

<span data-ttu-id="abaeb-294">每小時每個唯一的電腦和程序就會產生一個記錄，此外 toohello 記錄處理程序或電腦啟動或是初始 tooService 時所產生的對應字元。</span><span class="sxs-lookup"><span data-stu-id="abaeb-294">One record is generated per hour for each unique computer and process, in addition toohello records that are generated when a process or computer starts or is on-boarded tooService Map.</span></span> <span data-ttu-id="abaeb-295">這些記錄 hello 下表中都有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="abaeb-295">These records have hello properties in hello following tables.</span></span> <span data-ttu-id="abaeb-296">toofields hello hello ServiceMap Azure 資源管理員 API 中的電腦資源的對應欄位 hello 與 hello ServiceMapComputer_CL 事件中的值。</span><span class="sxs-lookup"><span data-stu-id="abaeb-296">hello fields and values in hello ServiceMapComputer_CL events map toofields of hello Machine resource in hello ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="abaeb-297">hello 欄位和值在 hello ServiceMapProcess_CL 事件 toohello 的欄位對應 hello hello ServiceMap Azure 資源管理員 API 中的處理序資源。</span><span class="sxs-lookup"><span data-stu-id="abaeb-297">hello fields and values in hello ServiceMapProcess_CL events map toohello fields of hello Process resource in hello ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="abaeb-298">hello ResourceName_s 欄位符合 hello 對應的資源管理員資源 hello [名稱] 欄位。</span><span class="sxs-lookup"><span data-stu-id="abaeb-298">hello ResourceName_s field matches hello name field in hello corresponding Resource Manager resource.</span></span> 

>[!NOTE]
><span data-ttu-id="abaeb-299">當服務對應功能成長時，這些欄位是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="abaeb-299">As Service Map features grow, these fields are subject toochange.</span></span>

<span data-ttu-id="abaeb-300">有 tooidentify 獨特的程序和電腦，您可以使用內部產生的屬性：</span><span class="sxs-lookup"><span data-stu-id="abaeb-300">There are internally generated properties you can use tooidentify unique processes and computers:</span></span>

- <span data-ttu-id="abaeb-301">電腦： 使用 ResourceId 或 ResourceName_s toouniquely 識別 Operations Management Suite 工作區中的電腦。</span><span class="sxs-lookup"><span data-stu-id="abaeb-301">Computer: Use ResourceId or ResourceName_s toouniquely identify a computer within an Operations Management Suite workspace.</span></span>
- <span data-ttu-id="abaeb-302">程序： 使用 ResourceId toouniquely 識別 Operations Management Suite 工作區中的處理序。</span><span class="sxs-lookup"><span data-stu-id="abaeb-302">Process: Use ResourceId toouniquely identify a process within an Operations Management Suite workspace.</span></span> <span data-ttu-id="abaeb-303">ResourceName_s 內是唯一的 hello hello 機器的 hello 處理序正在執行 (MachineResourceName_s) 內容</span><span class="sxs-lookup"><span data-stu-id="abaeb-303">ResourceName_s is unique within hello context of hello machine on which hello process is running (MachineResourceName_s)</span></span> 

<span data-ttu-id="abaeb-304">指定的處理序和指定的時間範圍內的電腦可以存在多個記錄，因為查詢可以傳回多筆記錄的 hello 同一部電腦或處理程序。</span><span class="sxs-lookup"><span data-stu-id="abaeb-304">Because multiple records can exist for a specified process and computer in a specified time range, queries can return more than one record for hello same computer or process.</span></span> <span data-ttu-id="abaeb-305">只有 tooinclude hello 的最近記錄，加入"|重複資料刪除 ResourceId"toohello 查詢。</span><span class="sxs-lookup"><span data-stu-id="abaeb-305">tooinclude only hello most recent record, add "| dedup ResourceId" toohello query.</span></span>

### <a name="servicemapcomputercl-records"></a><span data-ttu-id="abaeb-306">ServiceMapComputer_CL 記錄</span><span class="sxs-lookup"><span data-stu-id="abaeb-306">ServiceMapComputer_CL records</span></span>
<span data-ttu-id="abaeb-307">類型為 *ServiceMapComputer_CL* 的記錄會有伺服器 (具有服務對應代理程式) 的清查資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-307">Records with a type of *ServiceMapComputer_CL* have inventory data for servers with Service Map agents.</span></span> <span data-ttu-id="abaeb-308">這些記錄 hello 下表中都有 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="abaeb-308">These records have hello properties in hello following table:</span></span>

| <span data-ttu-id="abaeb-309">屬性</span><span class="sxs-lookup"><span data-stu-id="abaeb-309">Property</span></span> | <span data-ttu-id="abaeb-310">說明</span><span class="sxs-lookup"><span data-stu-id="abaeb-310">Description</span></span> |
|:--|:--|
| <span data-ttu-id="abaeb-311">類型</span><span class="sxs-lookup"><span data-stu-id="abaeb-311">Type</span></span> | <span data-ttu-id="abaeb-312">*ServiceMapComputer_CL*</span><span class="sxs-lookup"><span data-stu-id="abaeb-312">*ServiceMapComputer_CL*</span></span> |
| <span data-ttu-id="abaeb-313">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="abaeb-313">SourceSystem</span></span> | <span data-ttu-id="abaeb-314">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="abaeb-314">*OpsManager*</span></span> |
| <span data-ttu-id="abaeb-315">ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-315">ResourceId</span></span> | <span data-ttu-id="abaeb-316">hello hello 工作區中的機器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="abaeb-316">hello unique identifier for a machine within hello workspace</span></span> |
| <span data-ttu-id="abaeb-317">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-317">ResourceName_s</span></span> | <span data-ttu-id="abaeb-318">hello hello 工作區中的機器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="abaeb-318">hello unique identifier for a machine within hello workspace</span></span> |
| <span data-ttu-id="abaeb-319">ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-319">ComputerName_s</span></span> | <span data-ttu-id="abaeb-320">hello 電腦 FQDN</span><span class="sxs-lookup"><span data-stu-id="abaeb-320">hello computer FQDN</span></span> |
| <span data-ttu-id="abaeb-321">Ipv4Addresses_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-321">Ipv4Addresses_s</span></span> | <span data-ttu-id="abaeb-322">Hello 伺服器的 IPv4 位址的清單</span><span class="sxs-lookup"><span data-stu-id="abaeb-322">A list of hello server's IPv4 addresses</span></span> |
| <span data-ttu-id="abaeb-323">Ipv6Addresses_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-323">Ipv6Addresses_s</span></span> | <span data-ttu-id="abaeb-324">一份 hello 伺服器的 IPv6 位址</span><span class="sxs-lookup"><span data-stu-id="abaeb-324">A list of hello server's IPv6 addresses</span></span> |
| <span data-ttu-id="abaeb-325">DnsNames_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-325">DnsNames_s</span></span> | <span data-ttu-id="abaeb-326">DNS 名稱的陣列</span><span class="sxs-lookup"><span data-stu-id="abaeb-326">An array of DNS names</span></span> |
| <span data-ttu-id="abaeb-327">OperatingSystemFamily_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-327">OperatingSystemFamily_s</span></span> | <span data-ttu-id="abaeb-328">Windows 或 Linux</span><span class="sxs-lookup"><span data-stu-id="abaeb-328">Windows or Linux</span></span> |
| <span data-ttu-id="abaeb-329">OperatingSystemFullName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-329">OperatingSystemFullName_s</span></span> | <span data-ttu-id="abaeb-330">hello hello 作業系統的完整名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-330">hello full name of hello operating system</span></span>  |
| <span data-ttu-id="abaeb-331">Bitness_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-331">Bitness_s</span></span> | <span data-ttu-id="abaeb-332">hello 位元版本的 hello 機器 （32 位元或 64 位元）</span><span class="sxs-lookup"><span data-stu-id="abaeb-332">hello bitness of hello machine (32-bit or 64-bit)</span></span>  |
| <span data-ttu-id="abaeb-333">PhysicalMemory_d</span><span class="sxs-lookup"><span data-stu-id="abaeb-333">PhysicalMemory_d</span></span> | <span data-ttu-id="abaeb-334">hello 實體記憶體 （mb）</span><span class="sxs-lookup"><span data-stu-id="abaeb-334">hello physical memory in MB</span></span> |
| <span data-ttu-id="abaeb-335">Cpus_d</span><span class="sxs-lookup"><span data-stu-id="abaeb-335">Cpus_d</span></span> | <span data-ttu-id="abaeb-336">hello Cpu 數目</span><span class="sxs-lookup"><span data-stu-id="abaeb-336">hello number of CPUs</span></span> |
| <span data-ttu-id="abaeb-337">CpuSpeed_d</span><span class="sxs-lookup"><span data-stu-id="abaeb-337">CpuSpeed_d</span></span> | <span data-ttu-id="abaeb-338">hello 以 mhz 為單位的 CPU 速度</span><span class="sxs-lookup"><span data-stu-id="abaeb-338">hello CPU speed in MHz</span></span>|
| <span data-ttu-id="abaeb-339">VirtualizationState_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-339">VirtualizationState_s</span></span> | <span data-ttu-id="abaeb-340">*unknown**physical**virtual* *hypervisor*</span><span class="sxs-lookup"><span data-stu-id="abaeb-340">*unknown*, *physical*, *virtual*, *hypervisor*</span></span> |
| <span data-ttu-id="abaeb-341">VirtualMachineType_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-341">VirtualMachineType_s</span></span> | <span data-ttu-id="abaeb-342">*hyperv*、*vmware* 等等</span><span class="sxs-lookup"><span data-stu-id="abaeb-342">*hyperv*, *vmware*, and so on</span></span> |
| <span data-ttu-id="abaeb-343">VirtualMachineNativeMachineId_g</span><span class="sxs-lookup"><span data-stu-id="abaeb-343">VirtualMachineNativeMachineId_g</span></span> | <span data-ttu-id="abaeb-344">hello 其 hypervisor 所指派的 VM 識別碼</span><span class="sxs-lookup"><span data-stu-id="abaeb-344">hello VM ID as assigned by its hypervisor</span></span> |
| <span data-ttu-id="abaeb-345">VirtualMachineName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-345">VirtualMachineName_s</span></span> | <span data-ttu-id="abaeb-346">hello VM 的 hello 名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-346">hello name of hello VM</span></span> |
| <span data-ttu-id="abaeb-347">BootTime_t</span><span class="sxs-lookup"><span data-stu-id="abaeb-347">BootTime_t</span></span> | <span data-ttu-id="abaeb-348">hello 開機時間</span><span class="sxs-lookup"><span data-stu-id="abaeb-348">hello boot time</span></span> |



### <a name="servicemapprocesscl-type-records"></a><span data-ttu-id="abaeb-349">ServiceMapProcess_CL 類型記錄</span><span class="sxs-lookup"><span data-stu-id="abaeb-349">ServiceMapProcess_CL Type records</span></span>
<span data-ttu-id="abaeb-350">類型為 *ServiceMapProcess_CL* 的記錄會有伺服器 (具有服務對應代理程式) 上 TCP 連線處理程序的清查資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-350">Records with a type of *ServiceMapProcess_CL* have inventory data for TCP-connected processes on servers with Service Map agents.</span></span> <span data-ttu-id="abaeb-351">這些記錄 hello 下表中都有 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="abaeb-351">These records have hello properties in hello following table:</span></span>

| <span data-ttu-id="abaeb-352">屬性</span><span class="sxs-lookup"><span data-stu-id="abaeb-352">Property</span></span> | <span data-ttu-id="abaeb-353">說明</span><span class="sxs-lookup"><span data-stu-id="abaeb-353">Description</span></span> |
|:--|:--|
| <span data-ttu-id="abaeb-354">類型</span><span class="sxs-lookup"><span data-stu-id="abaeb-354">Type</span></span> | <span data-ttu-id="abaeb-355">*ServiceMapProcess_CL*</span><span class="sxs-lookup"><span data-stu-id="abaeb-355">*ServiceMapProcess_CL*</span></span> |
| <span data-ttu-id="abaeb-356">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="abaeb-356">SourceSystem</span></span> | <span data-ttu-id="abaeb-357">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="abaeb-357">*OpsManager*</span></span> |
| <span data-ttu-id="abaeb-358">ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-358">ResourceId</span></span> | <span data-ttu-id="abaeb-359">hello hello 工作區中的處理序的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="abaeb-359">hello unique identifier for a process within hello workspace</span></span> |
| <span data-ttu-id="abaeb-360">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-360">ResourceName_s</span></span> | <span data-ttu-id="abaeb-361">hello hello 執行所在的電腦中的處理序的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="abaeb-361">hello unique identifier for a process within hello machine on which it is running</span></span>|
| <span data-ttu-id="abaeb-362">MachineResourceName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-362">MachineResourceName_s</span></span> | <span data-ttu-id="abaeb-363">hello 機器 hello 資源名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-363">hello resource name of hello machine</span></span> |
| <span data-ttu-id="abaeb-364">ExecutableName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-364">ExecutableName_s</span></span> | <span data-ttu-id="abaeb-365">hello hello 程序可執行檔名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-365">hello name of hello process executable</span></span> |
| <span data-ttu-id="abaeb-366">StartTime_t</span><span class="sxs-lookup"><span data-stu-id="abaeb-366">StartTime_t</span></span> | <span data-ttu-id="abaeb-367">hello 程序集區開始時間</span><span class="sxs-lookup"><span data-stu-id="abaeb-367">hello process pool start time</span></span> |
| <span data-ttu-id="abaeb-368">FirstPid_d</span><span class="sxs-lookup"><span data-stu-id="abaeb-368">FirstPid_d</span></span> | <span data-ttu-id="abaeb-369">hello hello 程序集區中的第一個 PID</span><span class="sxs-lookup"><span data-stu-id="abaeb-369">hello first PID in hello process pool</span></span> |
| <span data-ttu-id="abaeb-370">Description_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-370">Description_s</span></span> | <span data-ttu-id="abaeb-371">hello 程序描述</span><span class="sxs-lookup"><span data-stu-id="abaeb-371">hello process description</span></span> |
| <span data-ttu-id="abaeb-372">CompanyName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-372">CompanyName_s</span></span> | <span data-ttu-id="abaeb-373">hello hello 公司名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-373">hello name of hello company</span></span> |
| <span data-ttu-id="abaeb-374">InternalName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-374">InternalName_s</span></span> | <span data-ttu-id="abaeb-375">hello 內部名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-375">hello internal name</span></span> |
| <span data-ttu-id="abaeb-376">ProductName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-376">ProductName_s</span></span> | <span data-ttu-id="abaeb-377">hello hello 產品名稱</span><span class="sxs-lookup"><span data-stu-id="abaeb-377">hello name of hello product</span></span> |
| <span data-ttu-id="abaeb-378">ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-378">ProductVersion_s</span></span> | <span data-ttu-id="abaeb-379">hello 產品版本</span><span class="sxs-lookup"><span data-stu-id="abaeb-379">hello product version</span></span> |
| <span data-ttu-id="abaeb-380">FileVersion_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-380">FileVersion_s</span></span> | <span data-ttu-id="abaeb-381">hello 檔案版本</span><span class="sxs-lookup"><span data-stu-id="abaeb-381">hello file version</span></span> |
| <span data-ttu-id="abaeb-382">CommandLine_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-382">CommandLine_s</span></span> | <span data-ttu-id="abaeb-383">hello 命令列</span><span class="sxs-lookup"><span data-stu-id="abaeb-383">hello command line</span></span> |
| <span data-ttu-id="abaeb-384">ExecutablePath _s</span><span class="sxs-lookup"><span data-stu-id="abaeb-384">ExecutablePath _s</span></span> | <span data-ttu-id="abaeb-385">hello 路徑 toohello 可執行檔</span><span class="sxs-lookup"><span data-stu-id="abaeb-385">hello path toohello executable file</span></span> |
| <span data-ttu-id="abaeb-386">WorkingDirectory_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-386">WorkingDirectory_s</span></span> | <span data-ttu-id="abaeb-387">hello 工作目錄</span><span class="sxs-lookup"><span data-stu-id="abaeb-387">hello working directory</span></span> |
| <span data-ttu-id="abaeb-388">UserName</span><span class="sxs-lookup"><span data-stu-id="abaeb-388">UserName</span></span> | <span data-ttu-id="abaeb-389">hello 的 hello 處理序執行的帳戶</span><span class="sxs-lookup"><span data-stu-id="abaeb-389">hello account under which hello process is executing</span></span> |
| <span data-ttu-id="abaeb-390">UserDomain</span><span class="sxs-lookup"><span data-stu-id="abaeb-390">UserDomain</span></span> | <span data-ttu-id="abaeb-391">hello 的 hello 處理序執行的網域</span><span class="sxs-lookup"><span data-stu-id="abaeb-391">hello domain under which hello process is executing</span></span> |


## <a name="sample-log-searches"></a><span data-ttu-id="abaeb-392">記錄檔搜尋範例</span><span class="sxs-lookup"><span data-stu-id="abaeb-392">Sample log searches</span></span>

### <a name="list-all-known-machines"></a><span data-ttu-id="abaeb-393">列出所有已知的機器</span><span class="sxs-lookup"><span data-stu-id="abaeb-393">List all known machines</span></span>
<span data-ttu-id="abaeb-394">Type=ServiceMapComputer_CL | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-394">Type=ServiceMapComputer_CL | dedup ResourceId</span></span>

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a><span data-ttu-id="abaeb-395">列出所有受管理電腦的 hello 實體記憶體容量。</span><span class="sxs-lookup"><span data-stu-id="abaeb-395">List hello physical memory capacity of all managed computers.</span></span>
<span data-ttu-id="abaeb-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span></span>

### <a name="list-computer-name-dns-ip-and-os"></a><span data-ttu-id="abaeb-397">列出電腦名稱、DNS、IP 和 OS。</span><span class="sxs-lookup"><span data-stu-id="abaeb-397">List computer name, DNS, IP, and OS.</span></span>
<span data-ttu-id="abaeb-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span></span>

### <a name="find-all-processes-with-sql-in-hello-command-line"></a><span data-ttu-id="abaeb-399">Hello 命令列中找到以"sql"的所有處理程序</span><span class="sxs-lookup"><span data-stu-id="abaeb-399">Find all processes with "sql" in hello command line</span></span>
<span data-ttu-id="abaeb-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-resource-name"></a><span data-ttu-id="abaeb-401">以資源名稱尋找機器 (最新的記錄)</span><span class="sxs-lookup"><span data-stu-id="abaeb-401">Find a machine (most recent record) by resource name</span></span>
<span data-ttu-id="abaeb-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-ip-address"></a><span data-ttu-id="abaeb-403">以 IP 位址尋找機器 (最新的記錄)</span><span class="sxs-lookup"><span data-stu-id="abaeb-403">Find a machine (most recent record) by IP address</span></span>
<span data-ttu-id="abaeb-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span></span>

### <a name="list-all-known-processes-on-a-specified-machine"></a><span data-ttu-id="abaeb-405">列出指定機器上的所有已知處理序</span><span class="sxs-lookup"><span data-stu-id="abaeb-405">List all known processes on a specified machine</span></span>
<span data-ttu-id="abaeb-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="abaeb-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="list-all-computers-running-sql"></a><span data-ttu-id="abaeb-407">列出所有執行 SQL 的電腦</span><span class="sxs-lookup"><span data-stu-id="abaeb-407">List all computers running SQL</span></span>
<span data-ttu-id="abaeb-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span></span>

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a><span data-ttu-id="abaeb-409">列出資料中心內所有唯一 curl 產品版本</span><span class="sxs-lookup"><span data-stu-id="abaeb-409">List all unique product versions of curl in my datacenter</span></span>
<span data-ttu-id="abaeb-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span></span>

### <a name="create-a-computer-group-of-all-computers-running-centos"></a><span data-ttu-id="abaeb-411">為所有執行 CentOS 的電腦建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="abaeb-411">Create a computer group of all computers running CentOS</span></span>
<span data-ttu-id="abaeb-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="abaeb-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span></span>


## <a name="rest-api"></a><span data-ttu-id="abaeb-413">REST API</span><span class="sxs-lookup"><span data-stu-id="abaeb-413">REST API</span></span>
<span data-ttu-id="abaeb-414">Hello 伺服器、 處理序及相依性的所有資料在服務對應透過 hello[服務對應 REST API](https://docs.microsoft.com/rest/api/servicemap/)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-414">All hello server, process, and dependency data in Service Map is available via hello [Service Map REST API](https://docs.microsoft.com/rest/api/servicemap/).</span></span>


## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="abaeb-415">診斷和使用量資料</span><span class="sxs-lookup"><span data-stu-id="abaeb-415">Diagnostic and usage data</span></span>
<span data-ttu-id="abaeb-416">Microsoft 會自動收集貴用戶使用服務對應服務的 hello 的使用方式和效能資料。</span><span class="sxs-lookup"><span data-stu-id="abaeb-416">Microsoft automatically collects usage and performance data through your use of hello Service Map service.</span></span> <span data-ttu-id="abaeb-417">Microsoft 會使用此資料 tooprovide 並提升 hello 品質、 安全性與 hello 服務對應服務的完整性。</span><span class="sxs-lookup"><span data-stu-id="abaeb-417">Microsoft uses this data tooprovide and improve hello quality, security, and integrity of hello Service Map service.</span></span> <span data-ttu-id="abaeb-418">tooprovide 正確且有效率地疑難排解功能，hello 資料包括您的軟體，例如作業系統和版本、 IP 位址、 DNS 名稱，以及工作站名稱 hello 組態相關資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-418">tooprovide accurate and efficient troubleshooting capabilities, hello data includes information about hello configuration of your software, such as operating system and version, IP address, DNS name, and workstation name.</span></span> <span data-ttu-id="abaeb-419">Microsoft 不會收集姓名、地址或其他連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="abaeb-419">Microsoft does not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="abaeb-420">如需有關資料收集與使用方式的詳細資訊，請參閱 hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-420">For more information about data collection and usage, see hello [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>


## <a name="next-steps"></a><span data-ttu-id="abaeb-421">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abaeb-421">Next steps</span></span>
<span data-ttu-id="abaeb-422">深入了解[記錄搜尋](../log-analytics/log-analytics-log-searches.md)服務對應所收集的記錄分析 tooretrieve 資料中。</span><span class="sxs-lookup"><span data-stu-id="abaeb-422">Learn more about [log searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooretrieve data that's collected by Service Map.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="abaeb-423">疑難排解</span><span class="sxs-lookup"><span data-stu-id="abaeb-423">Troubleshooting</span></span>
<span data-ttu-id="abaeb-424">請參閱 hello[疑難排解 hello 設定服務對應文件區段](operations-management-suite-service-map-configure.md#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="abaeb-424">See hello [Troubleshooting section of hello Configuring Service Map document](operations-management-suite-service-map-configure.md#troubleshooting).</span></span>


## <a name="feedback"></a><span data-ttu-id="abaeb-425">意見反應</span><span class="sxs-lookup"><span data-stu-id="abaeb-425">Feedback</span></span>
<span data-ttu-id="abaeb-426">您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？</span><span class="sxs-lookup"><span data-stu-id="abaeb-426">Do you have any feedback for us about Service Map or this documentation?</span></span>  <span data-ttu-id="abaeb-427">請瀏覽我們的[使用者意見頁面](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) \(英文\)，您可以在此頁面提出功能建議或對現有的建議進行投票。</span><span class="sxs-lookup"><span data-stu-id="abaeb-427">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.</span></span>
