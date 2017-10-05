---
title: "在 Operations Management Suite 中使用服務對應解決方案 | Microsoft Docs"
description: "服務對應是一個 Operations Management Suite 解決方案，可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。 本文會詳細說明如何在環境中部署服務對應並將它用於各種案例。"
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
ms.openlocfilehash: 2e5475a0563549ddfaa2c146e4acf94c019841ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-map-solution-in-operations-management-suite"></a><span data-ttu-id="4e3ad-104">在 Operations Management Suite 中使用服務對應解決方案</span><span class="sxs-lookup"><span data-stu-id="4e3ad-104">Use the Service Map solution in Operations Management Suite</span></span>
<span data-ttu-id="4e3ad-105">服務對應可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-105">Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="4e3ad-106">您可以藉由服務對應，將伺服器視為提供重要服務的互連系統，藉此來檢視伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-106">With Service Map, you can view your servers in the way that you think of them: as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="4e3ad-107">不需要進行任何設定，只要安裝了代理程式，服務對應就會顯示橫跨任何 TCP 連線架構的伺服器、處理序和連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-107">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required other than the installation of an agent.</span></span>

<span data-ttu-id="4e3ad-108">本文說明使用服務對應的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-108">This article describes the details of using Service Map.</span></span> <span data-ttu-id="4e3ad-109">如需設定服務對應和啟用代理程式的相關資訊，請參閱[在 Operations Management Suite 中設定服務對應解決方案](operations-management-suite-service-map-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-109">For information about configuring Service Map and onboarding agents, see [Configuring Service Map solution in Operations Management Suite](operations-management-suite-service-map-configure.md).</span></span>


## <a name="use-cases-make-your-it-processes-dependency-aware"></a><span data-ttu-id="4e3ad-110">使用案例︰讓 IT 處理序可以感知相依性</span><span class="sxs-lookup"><span data-stu-id="4e3ad-110">Use cases: Make your IT processes dependency aware</span></span>

### <a name="discovery"></a><span data-ttu-id="4e3ad-111">探索</span><span class="sxs-lookup"><span data-stu-id="4e3ad-111">Discovery</span></span>
<span data-ttu-id="4e3ad-112">服務對應會自動建置跨伺服器、處理程序和協力廠商服務的一般相依性參考對應。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-112">Service Map automatically builds a common reference map of dependencies across your servers, processes, and third-party services.</span></span> <span data-ttu-id="4e3ad-113">它會探索並對應所有 TCP 相依性，其中會識別非預期的連線、您倚賴的遠端協力廠商系統，以及與傳統網路暗區 (例如 Active Directory) 的相依性。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-113">It discovers and maps all TCP dependencies, identifying surprise connections, remote third-party systems you depend on, and dependencies to traditional dark areas of your network, such as Active Directory.</span></span> <span data-ttu-id="4e3ad-114">服務對應可探索到受管理系統嘗試進行的失敗網路連線，幫助您識別潛在的伺服器錯誤設定、服務中斷和網路問題。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-114">Service Map discovers failed network connections that your managed systems are attempting to make, helping you identify potential server misconfiguration, service outage, and network issues.</span></span>

### <a name="incident-management"></a><span data-ttu-id="4e3ad-115">事件管理</span><span class="sxs-lookup"><span data-stu-id="4e3ad-115">Incident management</span></span>
<span data-ttu-id="4e3ad-116">服務對應可藉由顯示系統的連線方式及其如何互相影響，協助您免去推敲問題所在的工作。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-116">Service Map helps eliminate the guesswork of problem isolation by showing you how systems are connected and affecting each other.</span></span> <span data-ttu-id="4e3ad-117">除了識別失敗的連線，服務對應還可協助識別設定錯誤的負載平衡器、非預期或過度負載的重要服務，以及與生產系統通訊的開發人員機器等惡意用戶端。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-117">In addition to identifying failed connections, it helps identify misconfigured load balancers, surprising or excessive load on critical services, and rogue clients, such as developer machines talking to production systems.</span></span> <span data-ttu-id="4e3ad-118">您也可以使用整合 Operations Management Suite 變更追蹤的工作流程，以查看後端機器或服務上的變更事件是否能夠說明事件的根本原因。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-118">By using integrated workflows with Operations Management Suite Change Tracking, you can also see whether a change event on a back-end machine or service explains the root cause of an incident.</span></span>

### <a name="migration-assurance"></a><span data-ttu-id="4e3ad-119">移轉保證</span><span class="sxs-lookup"><span data-stu-id="4e3ad-119">Migration assurance</span></span>
<span data-ttu-id="4e3ad-120">您可以使用服務對應，有效地規劃、加速和驗證 Azure 移轉，以確保沒有遺漏任何項目，且不會發生意外的中斷。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-120">By using Service Map, you can effectively plan, accelerate, and validate Azure migrations, which helps ensure that nothing is left behind and surprise outages do not occur.</span></span> <span data-ttu-id="4e3ad-121">您可以探索所有需要一起移轉的交互相依系統、評估系統組態和容量，以及識別執行中的系統是否仍為使用者提供服務或是應該解除委任而非移轉。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-121">You can discover all interdependent systems that need to migrate together, assess system configuration and capacity, and identify whether a running system is still serving users or is a candidate for decommissioning instead of migration.</span></span> <span data-ttu-id="4e3ad-122">移動完成之後，您可以檢查用戶端負載和身分識別，以確認測試系統和客戶之間的連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-122">After the move is complete, you can check on client load and identity to verify that test systems and customers are connecting.</span></span> <span data-ttu-id="4e3ad-123">如果子網路規劃和防火牆定義有問題，「服務對應」對應中的失敗連線會向您指出需要連線的系統。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-123">If your subnet planning and firewall definitions have issues, failed connections in Service Map maps point you to the systems that need connectivity.</span></span>

### <a name="business-continuity"></a><span data-ttu-id="4e3ad-124">業務持續性</span><span class="sxs-lookup"><span data-stu-id="4e3ad-124">Business continuity</span></span>
<span data-ttu-id="4e3ad-125">如果您使用 Azure Site Recovery，且需要協助以定義應用程式環境的復原順序，服務對應可以自動向您顯示系統彼此間的相依情形，以確保復原計畫可靠。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-125">If you are using Azure Site Recovery and need help defining the recovery sequence for your application environment, Service Map can automatically show you how systems rely on each other to ensure that your recovery plan is reliable.</span></span> <span data-ttu-id="4e3ad-126">藉由選擇重要伺服器或群組並檢視其用戶端，可以識別在伺服器還原並可用之後要復原的前端系統。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-126">By choosing a critical server or group and viewing its clients, you can identify which front-end systems to recover after the server is restored and available.</span></span> <span data-ttu-id="4e3ad-127">相反地，藉由查看重要伺服器的後端相依性，可以識別在焦點系統還原之前要復原的系統。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-127">Conversely, by looking at critical servers’ back-end dependencies, you can identify which systems to recover before your focus systems are restored.</span></span>

### <a name="patch-management"></a><span data-ttu-id="4e3ad-128">修補程式管理</span><span class="sxs-lookup"><span data-stu-id="4e3ad-128">Patch management</span></span>
<span data-ttu-id="4e3ad-129">服務對應可以指出其他哪些小組和伺服器依賴您的服務，因此您可以事先通知他們，然後才關閉系統進行修補，如此可加強 Operations Management Suite 系統更新評估的使用。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-129">Service Map enhances your use of the Operations Management Suite System Update Assessment by showing you which other teams and servers depend on your service, so you can notify them in advance before you take down your systems for patching.</span></span> <span data-ttu-id="4e3ad-130">服務對應也可以顯示您的服務在修補並重新啟動之後是否可用且正確連線，藉此加強 Operations Management Suite 中的修補程式管理。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-130">Service Map also enhances patch management in Operations Management Suite by showing you whether your services are available and properly connected after they are patched and restarted.</span></span>


## <a name="mapping-overview"></a><span data-ttu-id="4e3ad-131">對應概觀</span><span class="sxs-lookup"><span data-stu-id="4e3ad-131">Mapping overview</span></span>
<span data-ttu-id="4e3ad-132">服務對應代理程式會收集其安裝所在伺服器上所有 TCP 連線處理程序的相關資訊，以及有關每個處理程序之輸入和輸出連線的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-132">Service Map agents gather information about all TCP-connected processes on the server where they’re installed and details about the inbound and outbound connections for each process.</span></span> <span data-ttu-id="4e3ad-133">在左窗格的清單中，可以選取具有服務對應代理程式的機器或群組，將它們在指定時間範圍內的相依性視覺化。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-133">In the list in the left pane, you can select machines or groups that have Service Map agents to visualize their dependencies over a specified time range.</span></span> <span data-ttu-id="4e3ad-134">機器相依性對應的焦點會集中在特定機器，並顯示屬於該機器的所有直接 TCP 用戶端或伺服器機器。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-134">Machine dependency maps focus on a specific machine, and they show all the machines that are direct TCP clients or servers of that machine.</span></span>  <span data-ttu-id="4e3ad-135">機器群組對應會顯示多組伺服器及其相依性。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-135">Machine Group maps show sets of servers and their dependencies.</span></span>

![服務對應概觀](media/oms-service-map/service-map-overview.png)

<span data-ttu-id="4e3ad-137">對應內的機器可以展開，以顯示所選時間範圍內具有作用中網路連線的執行中處理程序。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-137">Machines can be expanded in the map to show the running processes with active network connections during the selected time range.</span></span> <span data-ttu-id="4e3ad-138">展開具有服務對應代理程式的遠端機器以顯示處理序詳細資料時，只會顯示與焦點機器通訊的處理序。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-138">When a remote machine with a Service Map agent is expanded to show process details, only those processes that communicate with the focus machine are shown.</span></span> <span data-ttu-id="4e3ad-139">連線到焦點機器的無代理程式前端機器計數，會顯示在所連線的處理序左側。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-139">The count of agentless front-end machines that connect into the focus machine is indicated on the left side of the processes they connect to.</span></span> <span data-ttu-id="4e3ad-140">如果焦點機器連線至無代理程式的後端機器，該後端伺服器會包含在「伺服器連接埠群組」中，連同其他連線至相同連接埠號碼的連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-140">If the focus machine is making a connection to a back-end machine that has no agent, the back-end server is included in a Server Port Group, along with other connections to the same port number.</span></span>

<span data-ttu-id="4e3ad-141">根據預設，「服務對應」對應會顯示過去 30 分鐘的相依性資訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-141">By default, Service Map maps show the last 30 minutes of dependency information.</span></span> <span data-ttu-id="4e3ad-142">使用左上角的時間控制項，可查詢過往時間範圍的對應 (最長可達一小時)，以顯示相依性的過往情形 (例如在事件發生期間或變更發生之前)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-142">By using the time controls at the upper left, you can query maps for historical time ranges of up to one hour to show how dependencies looked in the past (for example, during an incident or before a change occurred).</span></span> <span data-ttu-id="4e3ad-143">付費工作區的服務對應資料會儲存 30 天，免費工作區的服務對應資料則會儲存 7 天。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-143">Service Map data is stored for 30 days in paid workspaces, and for 7 days in free workspaces.</span></span>

## <a name="status-badges-and-border-coloring"></a><span data-ttu-id="4e3ad-144">狀態徽章和框線色彩</span><span class="sxs-lookup"><span data-stu-id="4e3ad-144">Status badges and border coloring</span></span>
<span data-ttu-id="4e3ad-145">在對應中每一部伺服器的底部，可以是一串狀態徽章，傳達伺服器的相關狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-145">At the bottom of each server in the map can be a list of status badges conveying status information about the server.</span></span> <span data-ttu-id="4e3ad-146">徽章表示在其中一個 Operations Management Suite 解決方案整合中，有某些伺服器的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-146">The badges indicate that there is some relevant information for the server from one of the Operations Management Suite solution integrations.</span></span> <span data-ttu-id="4e3ad-147">按一下徽章，即會在右窗格中直接顯示狀態的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-147">Clicking a badge takes you directly to the details of the status in the right pane.</span></span> <span data-ttu-id="4e3ad-148">目前可使用的狀態徽章包括警示、服務台、變更、安全性和更新。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-148">The currently available status badges include Alerts, Service Desk, Changes, Security, and Updates.</span></span>

<span data-ttu-id="4e3ad-149">根據狀態徽章的嚴重性，機器節點框線會呈現紅色 (重大)、黃色 (警告) 或藍色 (資訊)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-149">Depending on the severity of the status badges, machine node borders can be colored red (critical), yellow (warning), or blue (informational).</span></span> <span data-ttu-id="4e3ad-150">色彩可代表任何狀態徽章最嚴重的狀態。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-150">The color represents the most severe status of any of the status badges.</span></span> <span data-ttu-id="4e3ad-151">灰色框線代表沒有狀態指標的節點。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-151">A gray border indicates a node that has no status indicators.</span></span>

![狀態徽章](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a><span data-ttu-id="4e3ad-153">機器群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-153">Machine Groups</span></span>
<span data-ttu-id="4e3ad-154">機器群組可顯示以一組伺服器為中心的對應，而不只是單一伺服器的對應。因此，您可以在單一對應中看到多層式應用程式或伺服器叢集的所有成員。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-154">Machine Groups allow you to see maps centered around a set of servers, not just one so you can see all the members of a multi-tier application or server cluster in one map.</span></span>

<span data-ttu-id="4e3ad-155">使用者可選取伺服器所屬的群組，並選擇該群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-155">Users select which servers belong in a group together and choose a name for the group.</span></span>  <span data-ttu-id="4e3ad-156">之後，您可以選擇要檢視該群組及其所有處理序與連線，或是只檢視該群組與群組其他成員直接相關的處理序和連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-156">You can then choose to view the group with all of its processes and connections, or view it with only the processes and connections that directly relate to the other members of the group.</span></span>

![機器群組](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a><span data-ttu-id="4e3ad-158">建立機器群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-158">Creating a Machine Group</span></span>
<span data-ttu-id="4e3ad-159">若要建立群組，請在 [機器] 清單中選取您想要的一或多部機器，然後按一下 [加入群組]。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-159">To create a group, select the machine or machines you want in the Machines list and click **Add to group**.</span></span>

![建立群組](media/oms-service-map/machine-groups-create.png)

<span data-ttu-id="4e3ad-161">在該處選擇 [新建]，並指定群組名稱。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-161">There, you can choose **Create new** and give the group a name.</span></span>

![為群組命名](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
><span data-ttu-id="4e3ad-163">機器群組目前的限制是 10 部伺服器，但預計短期內會提高此限制。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-163">Machine groups are currently limited to 10 servers, but we plan to increase this limit soon.</span></span>

### <a name="viewing-a-group"></a><span data-ttu-id="4e3ad-164">檢視群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-164">Viewing a Group</span></span>
<span data-ttu-id="4e3ad-165">建立群組之後，可以選擇 [群組] 索引標籤來檢視所建立的群組。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-165">Once you’ve created some groups, you can view them by choosing the Groups tab.</span></span>

![[群組] 索引標籤](media/oms-service-map/machine-groups-tab.png)

<span data-ttu-id="4e3ad-167">然後，選取該群組名稱以檢視該機器群組的對應。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-167">Then select the Group name to view the map for that Machine Group.</span></span>
<span data-ttu-id="4e3ad-168">![機器群組](media/oms-service-map/machine-group.png)屬於該群組的機器在對應中會以白色框線框住。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-168">![Machine Group](media/oms-service-map/machine-group.png) The machines that belong to the group are outlined in white in the map.</span></span>

<span data-ttu-id="4e3ad-169">展開該群組，將會列出組成機器群組的機器。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-169">Expanding the Group will list the machines that make up the Machine Group.</span></span>

![機器群組的機器](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a><span data-ttu-id="4e3ad-171">依處理序篩選</span><span class="sxs-lookup"><span data-stu-id="4e3ad-171">Filter by processes</span></span>
<span data-ttu-id="4e3ad-172">對應檢視可切換為顯示群組中的所有處理序和連線，或是僅和機器群組直接相關的處理序和連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-172">You can toggle the map view between showing all processes and connections in the Group and only the ones that directly relate to the Machine Group.</span></span>  <span data-ttu-id="4e3ad-173">預設檢視是顯示所有處理序。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-173">The default view is to show all processes.</span></span>  <span data-ttu-id="4e3ad-174">您可以按一下對應上方的篩選圖示來變更檢視。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-174">You can change the view by clicking the filter icon above the map.</span></span>

![篩選群組](media/oms-service-map/machine-groups-filter.png)

<span data-ttu-id="4e3ad-176">選取 [所有處理序] 時，對應將包含群組中每部機器的所有處理序和連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-176">When **All processes** is selected, the map will include all processes and connections on each of the machines in the Group.</span></span>

![機器群組的所有處理序](media/oms-service-map/machine-groups-all.png)

<span data-ttu-id="4e3ad-178">如果您變更檢視為只顯示 [已與群組連線的處理序]，對應的範圍會縮小至只和群組中其他機器直接相關的處理序和連線，以形成精簡的檢視。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-178">If you change the view to show only **group-connected processes**, the map will be narrowed down to only those processes and connections that are directly connected to other machines in the group, creating a simplified view.</span></span>

![機器群組的已篩選處理序](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-to-a-group"></a><span data-ttu-id="4e3ad-180">將機器加入群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-180">Adding machines to a group</span></span>
<span data-ttu-id="4e3ad-181">若要將機器加入現有的群組，請核取您所需機器旁的方塊，然後按一下 [加入群組]。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-181">To add machines to an existing group, check the boxes next to the machines you want and then click **Add to group**.</span></span>  <span data-ttu-id="4e3ad-182">然後，選擇您想在其中加入機器的群組。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-182">Then, choose the group you want to add the machines to.</span></span>
 
### <a name="removing-machines-from-a-group"></a><span data-ttu-id="4e3ad-183">從群組移除多部機器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-183">Removing machines from a group</span></span>
<span data-ttu-id="4e3ad-184">在 [群組] 清單中，展開群組名稱以列出機器群組中的機器。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-184">In the Groups List, expand the group name to list the machines in the Machine Group.</span></span>  <span data-ttu-id="4e3ad-185">然後，按一下您想移除之機器旁的省略符號功能表，然後選擇 [移除]。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-185">Then, click on the ellipsis menu next to the machine you want to remove and choose **Remove**.</span></span>

![從群組移除機器](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a><span data-ttu-id="4e3ad-187">移除或重新命名群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-187">Removing or renaming a group</span></span>
<span data-ttu-id="4e3ad-188">按一下 [群組] 清單中群組名稱旁的省略符號功能表。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-188">Click on the ellipsis menu next to the group name in the Group List.</span></span>

![機器群組功能表](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a><span data-ttu-id="4e3ad-190">角色圖示</span><span class="sxs-lookup"><span data-stu-id="4e3ad-190">Role icons</span></span>
<span data-ttu-id="4e3ad-191">某些處理序在機器上扮演特殊角色︰Web 伺服器、應用程式伺服器及資料庫等。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-191">Certain processes serve particular roles on machines: web servers, application servers, database, and so on.</span></span> <span data-ttu-id="4e3ad-192">服務對應會為程序和機器方塊加上角色圖示註解，以協助您一下就識別出程序或伺服器所扮演的角色。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-192">Service Map annotates process and machine boxes with role icons to help identify at a glance the role a process or server plays.</span></span>

| <span data-ttu-id="4e3ad-193">角色圖示</span><span class="sxs-lookup"><span data-stu-id="4e3ad-193">Role icon</span></span> | <span data-ttu-id="4e3ad-194">說明</span><span class="sxs-lookup"><span data-stu-id="4e3ad-194">Description</span></span> |
|:--|:--|
| ![Web 伺服器](media/oms-service-map/role-web-server.png) | <span data-ttu-id="4e3ad-196">Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-196">Web server</span></span> |
| ![應用程式伺服器](media/oms-service-map/role-application-server.png) | <span data-ttu-id="4e3ad-198">應用程式伺服器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-198">Application server</span></span> |
| ![資料庫伺服器](media/oms-service-map/role-database.png) | <span data-ttu-id="4e3ad-200">資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-200">Database server</span></span> |
| ![LDAP 伺服器](media/oms-service-map/role-ldap.png) | <span data-ttu-id="4e3ad-202">LDAP 伺服器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-202">LDAP server</span></span> |
| ![SMB 伺服器](media/oms-service-map/role-smb.png) | <span data-ttu-id="4e3ad-204">SMB 伺服器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-204">SMB server</span></span> |

![角色圖示](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a><span data-ttu-id="4e3ad-206">失敗的連線</span><span class="sxs-lookup"><span data-stu-id="4e3ad-206">Failed connections</span></span>
<span data-ttu-id="4e3ad-207">「服務對應」對應內會顯示處理序和機器的失敗連線，並以紅色虛線指示用戶端系統無法連線到處理序或連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-207">Failed connections are shown in Service Map maps for processes and computers, with a dashed red line indicating that a client system is failing to reach a process or port.</span></span> <span data-ttu-id="4e3ad-208">已部署服務對應代理程式的系統如果就是嘗試進行失敗連線的系統，則會報告失敗的連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-208">Failed connections are reported from any system with a deployed Service Map agent if that system is the one attempting the failed connection.</span></span> <span data-ttu-id="4e3ad-209">服務對應會觀察無法建立連線的 TCP 通訊端，藉以衡量此處理序。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-209">Service Map measures this process by observing TCP sockets that fail to establish a connection.</span></span> <span data-ttu-id="4e3ad-210">連線失敗的原因可能是防火牆、用戶端或伺服器設定不正確，或遠端服務無法使用。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-210">This failure could result from a firewall, a misconfiguration in the client or server, or a remote service being unavailable.</span></span>

![失敗的連線](media/oms-service-map/failed-connections.png)

<span data-ttu-id="4e3ad-212">了解失敗的連線有助於疑難排解、移轉驗證、安全性分析和整體架構理解。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-212">Understanding failed connections can help with troubleshooting, migration validation, security analysis, and overall architectural understanding.</span></span> <span data-ttu-id="4e3ad-213">失敗的連線有時無害，但它們通常直指問題所在，例如容錯移轉環境突然變成無法連線，或兩個應用程式層在雲端移轉之後無法通訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-213">Failed connections are sometimes harmless, but they often point directly to a problem, such as a failover environment suddenly becoming unreachable, or two application tiers being unable to talk after a cloud migration.</span></span>

## <a name="client-groups"></a><span data-ttu-id="4e3ad-214">用戶端群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-214">Client Groups</span></span>
<span data-ttu-id="4e3ad-215">用戶端群組是對應上的方塊，代表沒有相依性代理程式的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-215">Client Groups are boxes on the map that represent client machines that do not have Dependency Agents.</span></span> <span data-ttu-id="4e3ad-216">單一用戶端群組代表個別處理序或機器的用戶端。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-216">A single Client Group represents the clients for an individual process or machine.</span></span>

![用戶端群組](media/oms-service-map/client-groups.png)

<span data-ttu-id="4e3ad-218">若要查看用戶端群組中伺服器的 IP 位址，選取群組。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-218">To see the IP addresses of the servers in a Client Group, select the group.</span></span> <span data-ttu-id="4e3ad-219">群組的內容會列在 [用戶端群組屬性] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-219">The contents of the group are listed in the **Client Group Properties** pane.</span></span>

![用戶端群組屬性](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a><span data-ttu-id="4e3ad-221">伺服器連接埠群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-221">Server Port Groups</span></span>
<span data-ttu-id="4e3ad-222">伺服器連接埠群組是方塊，代表沒有相依性代理程式的伺服器上的伺服器連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-222">Server Port Groups are boxes that represent server ports on servers that do not have Dependency Agents.</span></span> <span data-ttu-id="4e3ad-223">此方塊包含伺服器連接埠，以及與該連接埠連線的伺服器數目。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-223">The box contains the server port and a count of the number of servers with connections to that port.</span></span> <span data-ttu-id="4e3ad-224">展開方塊可查看個別伺服器和連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-224">Expand the box to see the individual servers and connections.</span></span> <span data-ttu-id="4e3ad-225">如果在方塊中只有一部伺服器，則會列出其名稱或 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-225">If there is only one server in the box, the name or IP address is listed.</span></span>

![伺服器連接埠群組](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a><span data-ttu-id="4e3ad-227">內容功能表</span><span class="sxs-lookup"><span data-stu-id="4e3ad-227">Context menu</span></span>
<span data-ttu-id="4e3ad-228">按一下任何伺服器右上角的省略符號 (...)，會顯示該伺服器的內容功能表。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-228">Clicking the ellipsis (...) at the top right of any server displays the context menu for that server.</span></span>

![失敗的連線](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a><span data-ttu-id="4e3ad-230">載入伺服器對應</span><span class="sxs-lookup"><span data-stu-id="4e3ad-230">Load server map</span></span>
<span data-ttu-id="4e3ad-231">按一下 [載入伺服器對應] 會導向新的對應，並以所選取的伺服器做為新的焦點機器。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-231">Clicking **Load Server Map** takes you to a new map with the selected server as the new focus machine.</span></span>

### <a name="show-self-links"></a><span data-ttu-id="4e3ad-232">顯示自我連結</span><span class="sxs-lookup"><span data-stu-id="4e3ad-232">Show self-links</span></span>
<span data-ttu-id="4e3ad-233">按一下 [顯示自我連結] 將會重繪包括任何自我連結的伺服器節點。自我連結即是以伺服器內處理序做為開始和結束的 TCP 連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-233">Clicking **Show Self-Links** redraws the server node, including any self-links, which are TCP connections that start and end on processes within the server.</span></span> <span data-ttu-id="4e3ad-234">如果顯示了自我連結，功能表命令會變更為 [隱藏自我連結]，就可以將它們關閉。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-234">If self-links are shown, the menu command changes to **Hide Self-Links**, so that you can turn them off.</span></span>

## <a name="computer-summary"></a><span data-ttu-id="4e3ad-235">電腦摘要</span><span class="sxs-lookup"><span data-stu-id="4e3ad-235">Computer summary</span></span>
<span data-ttu-id="4e3ad-236">[機器摘要] 窗格包含伺服器作業系統的概觀、相依性計數，以及其他 Operations Management Suite 解決方案的資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-236">The **Machine Summary** pane includes an overview of a server's operating system, dependency counts, and data from other Operations Management Suite solutions.</span></span> <span data-ttu-id="4e3ad-237">這些資料包括效能計量、服務台票證、變更追蹤、安全性和更新。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-237">Such data includes performance metrics, service desk tickets, change tracking, security, and updates.</span></span>

![[機器摘要] 窗格](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a><span data-ttu-id="4e3ad-239">電腦和處理序屬性</span><span class="sxs-lookup"><span data-stu-id="4e3ad-239">Computer and process properties</span></span>
<span data-ttu-id="4e3ad-240">在瀏覽「服務對應」對應時，可以選取機器和處理序來取得其他有關其屬性的內容。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-240">When you navigate a Service Map map, you can select machines and processes to gain additional context about their properties.</span></span> <span data-ttu-id="4e3ad-241">機器會提供下列相關資訊：DNS 名稱、IPv4 位址、CPU 和記憶體容量、VM 類型、作業系統和版本、上次重新開機時間，以及其 Operations Management Suite 和服務對應代理程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-241">Machines provide information about DNS name, IPv4 addresses, CPU and memory capacity, VM type, operating system and version, last reboot time, and the IDs of their Operations Management Suite and Service Map agents.</span></span>

![[機器屬性] 窗格](media/oms-service-map/machine-properties.png)

<span data-ttu-id="4e3ad-243">處理序詳細資料是收集自作業系統中繼資料，其內容與執行中的處理序有關，包括處理序名稱、處理序描述、使用者名稱和網域 (在 Windows 上)、公司名稱、產品名稱、產品版本、工作目錄、命令列，以及處理序開始時間。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-243">You can gather process details from operating-system metadata about running processes, including process name, process description, user name and domain (on Windows), company name, product name, product version, working directory, command line, and process start time.</span></span>

![[處理序屬性] 窗格](media/oms-service-map/process-properties.png)

<span data-ttu-id="4e3ad-245">[處理序摘要] 窗格會提供其他有關該處理序連線的資訊，包括其繫結連接埠、輸入及輸出連線，以及失敗的連線。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-245">The **Process Summary** pane provides additional information about the process’s connectivity, including its bound ports, inbound and outbound connections, and failed connections.</span></span>

![[處理序摘要] 窗格](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a><span data-ttu-id="4e3ad-247">Operations Management Suite 警示整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-247">Operations Management Suite Alerts integration</span></span>
<span data-ttu-id="4e3ad-248">服務對應會與 Operations Management Suite 警示整合，以顯示所選時間範圍內針對所選伺服器觸發的警示。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-248">Service Map integrates with Operations Management Suite Alerts to show fired alerts for the selected server in the selected time range.</span></span> <span data-ttu-id="4e3ad-249">如果有最新警示，伺服器會顯示圖示，且 [機器警示] 窗格會列出警示。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-249">The server displays an icon if there are current alerts, and the **Machine Alerts** pane lists the alerts.</span></span>

![[機器警示] 窗格](media/oms-service-map/machine-alerts.png)

<span data-ttu-id="4e3ad-251">若要讓服務對應顯示相關警示，請建立針對特定電腦觸發的警示規則。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-251">To enable Service Map to display relevant alerts, create an alert rule that fires for a specific computer.</span></span> <span data-ttu-id="4e3ad-252">若要建立適當的警示︰</span><span class="sxs-lookup"><span data-stu-id="4e3ad-252">To create proper alerts:</span></span>
- <span data-ttu-id="4e3ad-253">包含依電腦群組的子句，例如，**by Computer interval 1minute** (依 1 分鐘的電腦間隔)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-253">Include a clause to group by computer (for example, **by Computer interval 1minute**).</span></span>
- <span data-ttu-id="4e3ad-254">選擇依據計量量值來發出警示。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-254">Choose to alert based on metric measurement.</span></span>

![警示組態](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a><span data-ttu-id="4e3ad-256">Operations Management Suite 記錄事件整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-256">Operations Management Suite log events integration</span></span>
<span data-ttu-id="4e3ad-257">服務對應會與記錄搜尋整合，以顯示所選時間範圍期間，適用於所選伺服器的所有可用記錄事件計數。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-257">Service Map integrates with Log Search to show a count of all available log events for the selected server during the selected time range.</span></span> <span data-ttu-id="4e3ad-258">您可以按一下事件計數清單中的任一列，以移至記錄搜尋並查看個別的記錄事件。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-258">You can click any row in the list of event counts to jump to Log Search and see the individual log events.</span></span>

![[機器記錄事件] 窗格](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a><span data-ttu-id="4e3ad-260">Operations Management Suite 服務台整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-260">Operations Management Suite Service Desk integration</span></span>
<span data-ttu-id="4e3ad-261">當「服務對應」和「IT 服務管理連接器」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-261">Service Map integration with the IT Service Management Connector is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span> <span data-ttu-id="4e3ad-262">服務對應中的整合會標示為「服務台」。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-262">The integration in Service Map is labeled "Service Desk."</span></span> <span data-ttu-id="4e3ad-263">如需詳細資訊，請參閱[使用 IT 服務管理連接器將 ITSM 工作項目集中管理](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-263">For more information, see [Centrally manage ITSM work items using IT Service Management Connector](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).</span></span>

<span data-ttu-id="4e3ad-264">[機器服務台] 窗格會列出所選時間範圍內所選伺服器的所有 IT 服務管理事件。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-264">The **Machine Service Desk** pane lists all IT Service Management events for the selected server in the selected time range.</span></span> <span data-ttu-id="4e3ad-265">如果有最新項目，伺服器會顯示圖示，且 [機器服務台] 窗格會列出這些項目。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-265">The server displays an icon if there are current items and the Machine Service Desk pane lists them.</span></span>

![[機器服務台] 窗格](media/oms-service-map/service-desk.png)

<span data-ttu-id="4e3ad-267">若要在連線的 ITSM 解決方案中開啟項目，請按一下 [檢視工作項目]。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-267">To open the item in your connected ITSM solution, click **View Work Item**.</span></span>

<span data-ttu-id="4e3ad-268">若要檢視記錄搜尋中項目的詳細資料，請按一下 [在記錄搜尋中顯示]。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-268">To view the details of the item in Log Search, click **Show in Log Search**.</span></span>


## <a name="operations-management-suite-change-tracking-integration"></a><span data-ttu-id="4e3ad-269">Operations Management Suite 變更追蹤整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-269">Operations Management Suite Change Tracking integration</span></span>
<span data-ttu-id="4e3ad-270">當「服務對應」和「變更追蹤」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-270">Service Map integration with Change Tracking is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="4e3ad-271">[機器變更追蹤] 窗格會列出所有變更，從最新排到最舊，並有連結可供向下鑽研記錄搜尋，以取得其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-271">The **Machine Change Tracking** pane lists all changes, with the most recent first, along with a link to drill down to Log Search for additional details.</span></span>

![[機器變更追蹤] 窗格](media/oms-service-map/change-tracking.png)

<span data-ttu-id="4e3ad-273">下圖是選取 [在 Log Analytics 中顯示] 之後，可能會看到的 ConfigurationChange 事件詳細檢視。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-273">The following image is a detailed view of a ConfigurationChange event that you might see after you select **Show in Log Analytics**.</span></span>

![ConfigurationChange 事件](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a><span data-ttu-id="4e3ad-275">Operations Management Suite 效能整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-275">Operations Management Suite performance integration</span></span>
<span data-ttu-id="4e3ad-276">[機器效能] 窗格會顯示所選伺服器的標準效能計量。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-276">The **Machine Performance** pane displays standard performance metrics for the selected server.</span></span> <span data-ttu-id="4e3ad-277">這些計量包含 CPU 使用率、記憶體使用率、傳送和接收的網路位元組，以及按照傳送和接收的網路位元組排序的前幾個處理序清單。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-277">The metrics include CPU utilization, memory utilization, network bytes sent and received, and a list of the top processes by network bytes sent and received.</span></span> <span data-ttu-id="4e3ad-278">若要取得網路效能資料，您也必須在 Operations Management Suite 中啟用 Wire Data 2.0 解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-278">To get the network performance data, you must also have enabled the Wire Data 2.0 solution in Operations Management Suite.</span></span>

![[機器效能] 窗格](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a><span data-ttu-id="4e3ad-280">Operations Management Suite 安全性整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-280">Operations Management Suite Security integration</span></span>
<span data-ttu-id="4e3ad-281">當「服務對應」和「安全性與稽核」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-281">Service Map integration with Security and Audit is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="4e3ad-282">[機器安全性] 窗格會顯示 Operations Management Suite 安全性與稽核解決方案中針對所選伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-282">The **Machine Security** pane shows data from the Operations Management Suite Security and Audit solution for the selected server.</span></span> <span data-ttu-id="4e3ad-283">此窗格會列出所選時間範圍內伺服器任何未處理之安全性問題的摘要。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-283">The pane lists a summary of any outstanding security issues for the server during the selected time range.</span></span> <span data-ttu-id="4e3ad-284">按一下任一安全性問題會向下鑽研到記錄搜尋，以顯示關於安全性問題的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-284">Clicking any of the security issues drills down into a Log Search for details about them.</span></span>

![[機器安全性] 窗格](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a><span data-ttu-id="4e3ad-286">Operations Management Suite 更新整合</span><span class="sxs-lookup"><span data-stu-id="4e3ad-286">Operations Management Suite Updates integration</span></span>
<span data-ttu-id="4e3ad-287">當「服務對應」和「更新管理」這兩個解決方案皆已在 Operations Management Suite 工作區中啟用並設定時，便會自動進行整合。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-287">Service Map integration with Update Management is automatic when both solutions are enabled and configured in your Operations Management Suite workspace.</span></span>

<span data-ttu-id="4e3ad-288">[機器更新] 窗格會顯示 Operations Management Suite 更新管理解決方案中針對所選伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-288">The **Machine Updates** pane displays data from the Operations Management Suite Update Management solution for the selected server.</span></span> <span data-ttu-id="4e3ad-289">此窗格會列出所選時間範圍內伺服器所缺少之任何更新的摘要。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-289">The pane lists a summary of any missing updates for the server during the selected time range.</span></span>

![[機器變更追蹤] 窗格](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a><span data-ttu-id="4e3ad-291">Log Analytics 記錄</span><span class="sxs-lookup"><span data-stu-id="4e3ad-291">Log Analytics records</span></span>
<span data-ttu-id="4e3ad-292">服務對應的電腦和處理序清查資料可供在 Log Analytics 中進行[搜尋](../log-analytics/log-analytics-log-searches.md)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-292">Service Map computer and process inventory data is available for [search](../log-analytics/log-analytics-log-searches.md) in Log Analytics.</span></span> <span data-ttu-id="4e3ad-293">您可以將此資料套用至各種案例，包括移轉規劃、容量分析、探索和隨選效能疑難排解。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-293">You can apply this data to scenarios that include migration planning, capacity analysis, discovery, and on-demand performance troubleshooting.</span></span>

<span data-ttu-id="4e3ad-294">除了當處理序或電腦啟動時或是新增到服務對應時所產生的記錄外，每小時還會為每個唯一的電腦和處理序產生一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-294">One record is generated per hour for each unique computer and process, in addition to the records that are generated when a process or computer starts or is on-boarded to Service Map.</span></span> <span data-ttu-id="4e3ad-295">這些記錄具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-295">These records have the properties in the following tables.</span></span> <span data-ttu-id="4e3ad-296">ServiceMapComputer_CL 事件中的欄位和值對應到 ServiceMap Azure Resource Manager API 中的機器資源欄位。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-296">The fields and values in the ServiceMapComputer_CL events map to fields of the Machine resource in the ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="4e3ad-297">ServiceMapProcess_CL 事件中的欄位和值對應到 ServiceMap Azure Resource Manager API 中的處理序資源欄位。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-297">The fields and values in the ServiceMapProcess_CL events map to the fields of the Process resource in the ServiceMap Azure Resource Manager API.</span></span> <span data-ttu-id="4e3ad-298">ResourceName_s 欄位會符合對應 Resource Manager 資源中的名稱欄位。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-298">The ResourceName_s field matches the name field in the corresponding Resource Manager resource.</span></span> 

>[!NOTE]
><span data-ttu-id="4e3ad-299">在服務對應功能增加之際，這些欄位可能會隨之變更。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-299">As Service Map features grow, these fields are subject to change.</span></span>

<span data-ttu-id="4e3ad-300">有可用來識別唯一處理程序和電腦的內部產生屬性︰</span><span class="sxs-lookup"><span data-stu-id="4e3ad-300">There are internally generated properties you can use to identify unique processes and computers:</span></span>

- <span data-ttu-id="4e3ad-301">電腦：使用 ResourceId 或 ResourceName_s 來唯一識別 Operations Management Suite 工作區中的電腦。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-301">Computer: Use ResourceId or ResourceName_s to uniquely identify a computer within an Operations Management Suite workspace.</span></span>
- <span data-ttu-id="4e3ad-302">處理序：使用 ResourceId 來唯一識別 Operations Management Suite 工作區中的處理序。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-302">Process: Use ResourceId to uniquely identify a process within an Operations Management Suite workspace.</span></span> <span data-ttu-id="4e3ad-303">ResourceName_s 在執行處理序的機器 (MachineResourceName_s) 的環境中是唯一的</span><span class="sxs-lookup"><span data-stu-id="4e3ad-303">ResourceName_s is unique within the context of the machine on which the process is running (MachineResourceName_s)</span></span> 

<span data-ttu-id="4e3ad-304">因為在指定時間範圍內可以有多筆指定處理序和電腦的記錄，針對相同電腦或處理序的查詢可能會傳回多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-304">Because multiple records can exist for a specified process and computer in a specified time range, queries can return more than one record for the same computer or process.</span></span> <span data-ttu-id="4e3ad-305">若只要包含最新的記錄，請在查詢中加入 "| dedup ResourceId"。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-305">To include only the most recent record, add "| dedup ResourceId" to the query.</span></span>

### <a name="servicemapcomputercl-records"></a><span data-ttu-id="4e3ad-306">ServiceMapComputer_CL 記錄</span><span class="sxs-lookup"><span data-stu-id="4e3ad-306">ServiceMapComputer_CL records</span></span>
<span data-ttu-id="4e3ad-307">類型為 *ServiceMapComputer_CL* 的記錄會有伺服器 (具有服務對應代理程式) 的清查資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-307">Records with a type of *ServiceMapComputer_CL* have inventory data for servers with Service Map agents.</span></span> <span data-ttu-id="4e3ad-308">這些記錄具有下表中的屬性：</span><span class="sxs-lookup"><span data-stu-id="4e3ad-308">These records have the properties in the following table:</span></span>

| <span data-ttu-id="4e3ad-309">屬性</span><span class="sxs-lookup"><span data-stu-id="4e3ad-309">Property</span></span> | <span data-ttu-id="4e3ad-310">說明</span><span class="sxs-lookup"><span data-stu-id="4e3ad-310">Description</span></span> |
|:--|:--|
| <span data-ttu-id="4e3ad-311">類型</span><span class="sxs-lookup"><span data-stu-id="4e3ad-311">Type</span></span> | <span data-ttu-id="4e3ad-312">*ServiceMapComputer_CL*</span><span class="sxs-lookup"><span data-stu-id="4e3ad-312">*ServiceMapComputer_CL*</span></span> |
| <span data-ttu-id="4e3ad-313">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4e3ad-313">SourceSystem</span></span> | <span data-ttu-id="4e3ad-314">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="4e3ad-314">*OpsManager*</span></span> |
| <span data-ttu-id="4e3ad-315">ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-315">ResourceId</span></span> | <span data-ttu-id="4e3ad-316">工作區中機器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e3ad-316">The unique identifier for a machine within the workspace</span></span> |
| <span data-ttu-id="4e3ad-317">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-317">ResourceName_s</span></span> | <span data-ttu-id="4e3ad-318">工作區中機器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e3ad-318">The unique identifier for a machine within the workspace</span></span> |
| <span data-ttu-id="4e3ad-319">ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-319">ComputerName_s</span></span> | <span data-ttu-id="4e3ad-320">電腦 FQDN</span><span class="sxs-lookup"><span data-stu-id="4e3ad-320">The computer FQDN</span></span> |
| <span data-ttu-id="4e3ad-321">Ipv4Addresses_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-321">Ipv4Addresses_s</span></span> | <span data-ttu-id="4e3ad-322">伺服器的 IPv4 位址清單</span><span class="sxs-lookup"><span data-stu-id="4e3ad-322">A list of the server's IPv4 addresses</span></span> |
| <span data-ttu-id="4e3ad-323">Ipv6Addresses_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-323">Ipv6Addresses_s</span></span> | <span data-ttu-id="4e3ad-324">伺服器的 IPv6 位址清單</span><span class="sxs-lookup"><span data-stu-id="4e3ad-324">A list of the server's IPv6 addresses</span></span> |
| <span data-ttu-id="4e3ad-325">DnsNames_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-325">DnsNames_s</span></span> | <span data-ttu-id="4e3ad-326">DNS 名稱的陣列</span><span class="sxs-lookup"><span data-stu-id="4e3ad-326">An array of DNS names</span></span> |
| <span data-ttu-id="4e3ad-327">OperatingSystemFamily_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-327">OperatingSystemFamily_s</span></span> | <span data-ttu-id="4e3ad-328">Windows 或 Linux</span><span class="sxs-lookup"><span data-stu-id="4e3ad-328">Windows or Linux</span></span> |
| <span data-ttu-id="4e3ad-329">OperatingSystemFullName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-329">OperatingSystemFullName_s</span></span> | <span data-ttu-id="4e3ad-330">作業系統的完整名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-330">The full name of the operating system</span></span>  |
| <span data-ttu-id="4e3ad-331">Bitness_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-331">Bitness_s</span></span> | <span data-ttu-id="4e3ad-332">機器的運算位元數 (32 位元或 64 位元)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-332">The bitness of the machine (32-bit or 64-bit)</span></span>  |
| <span data-ttu-id="4e3ad-333">PhysicalMemory_d</span><span class="sxs-lookup"><span data-stu-id="4e3ad-333">PhysicalMemory_d</span></span> | <span data-ttu-id="4e3ad-334">實體記憶體 (MB)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-334">The physical memory in MB</span></span> |
| <span data-ttu-id="4e3ad-335">Cpus_d</span><span class="sxs-lookup"><span data-stu-id="4e3ad-335">Cpus_d</span></span> | <span data-ttu-id="4e3ad-336">CPU 數目</span><span class="sxs-lookup"><span data-stu-id="4e3ad-336">The number of CPUs</span></span> |
| <span data-ttu-id="4e3ad-337">CpuSpeed_d</span><span class="sxs-lookup"><span data-stu-id="4e3ad-337">CpuSpeed_d</span></span> | <span data-ttu-id="4e3ad-338">CPU 速度 (MHz)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-338">The CPU speed in MHz</span></span>|
| <span data-ttu-id="4e3ad-339">VirtualizationState_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-339">VirtualizationState_s</span></span> | <span data-ttu-id="4e3ad-340">*unknown**physical**virtual* *hypervisor*</span><span class="sxs-lookup"><span data-stu-id="4e3ad-340">*unknown*, *physical*, *virtual*, *hypervisor*</span></span> |
| <span data-ttu-id="4e3ad-341">VirtualMachineType_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-341">VirtualMachineType_s</span></span> | <span data-ttu-id="4e3ad-342">*hyperv*、*vmware* 等等</span><span class="sxs-lookup"><span data-stu-id="4e3ad-342">*hyperv*, *vmware*, and so on</span></span> |
| <span data-ttu-id="4e3ad-343">VirtualMachineNativeMachineId_g</span><span class="sxs-lookup"><span data-stu-id="4e3ad-343">VirtualMachineNativeMachineId_g</span></span> | <span data-ttu-id="4e3ad-344">VM 識別碼 (由其 Hypervisor 指派)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-344">The VM ID as assigned by its hypervisor</span></span> |
| <span data-ttu-id="4e3ad-345">VirtualMachineName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-345">VirtualMachineName_s</span></span> | <span data-ttu-id="4e3ad-346">VM 的名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-346">The name of the VM</span></span> |
| <span data-ttu-id="4e3ad-347">BootTime_t</span><span class="sxs-lookup"><span data-stu-id="4e3ad-347">BootTime_t</span></span> | <span data-ttu-id="4e3ad-348">開機時間</span><span class="sxs-lookup"><span data-stu-id="4e3ad-348">The boot time</span></span> |



### <a name="servicemapprocesscl-type-records"></a><span data-ttu-id="4e3ad-349">ServiceMapProcess_CL 類型記錄</span><span class="sxs-lookup"><span data-stu-id="4e3ad-349">ServiceMapProcess_CL Type records</span></span>
<span data-ttu-id="4e3ad-350">類型為 *ServiceMapProcess_CL* 的記錄會有伺服器 (具有服務對應代理程式) 上 TCP 連線處理程序的清查資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-350">Records with a type of *ServiceMapProcess_CL* have inventory data for TCP-connected processes on servers with Service Map agents.</span></span> <span data-ttu-id="4e3ad-351">這些記錄具有下表中的屬性：</span><span class="sxs-lookup"><span data-stu-id="4e3ad-351">These records have the properties in the following table:</span></span>

| <span data-ttu-id="4e3ad-352">屬性</span><span class="sxs-lookup"><span data-stu-id="4e3ad-352">Property</span></span> | <span data-ttu-id="4e3ad-353">說明</span><span class="sxs-lookup"><span data-stu-id="4e3ad-353">Description</span></span> |
|:--|:--|
| <span data-ttu-id="4e3ad-354">類型</span><span class="sxs-lookup"><span data-stu-id="4e3ad-354">Type</span></span> | <span data-ttu-id="4e3ad-355">*ServiceMapProcess_CL*</span><span class="sxs-lookup"><span data-stu-id="4e3ad-355">*ServiceMapProcess_CL*</span></span> |
| <span data-ttu-id="4e3ad-356">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4e3ad-356">SourceSystem</span></span> | <span data-ttu-id="4e3ad-357">*OpsManager*</span><span class="sxs-lookup"><span data-stu-id="4e3ad-357">*OpsManager*</span></span> |
| <span data-ttu-id="4e3ad-358">ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-358">ResourceId</span></span> | <span data-ttu-id="4e3ad-359">工作區中處理序的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e3ad-359">The unique identifier for a process within the workspace</span></span> |
| <span data-ttu-id="4e3ad-360">ResourceName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-360">ResourceName_s</span></span> | <span data-ttu-id="4e3ad-361">在執行處理序的機器上，處理序的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e3ad-361">The unique identifier for a process within the machine on which it is running</span></span>|
| <span data-ttu-id="4e3ad-362">MachineResourceName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-362">MachineResourceName_s</span></span> | <span data-ttu-id="4e3ad-363">機器的資源名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-363">The resource name of the machine</span></span> |
| <span data-ttu-id="4e3ad-364">ExecutableName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-364">ExecutableName_s</span></span> | <span data-ttu-id="4e3ad-365">處理序可執行檔的名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-365">The name of the process executable</span></span> |
| <span data-ttu-id="4e3ad-366">StartTime_t</span><span class="sxs-lookup"><span data-stu-id="4e3ad-366">StartTime_t</span></span> | <span data-ttu-id="4e3ad-367">處理序集區的開始時間</span><span class="sxs-lookup"><span data-stu-id="4e3ad-367">The process pool start time</span></span> |
| <span data-ttu-id="4e3ad-368">FirstPid_d</span><span class="sxs-lookup"><span data-stu-id="4e3ad-368">FirstPid_d</span></span> | <span data-ttu-id="4e3ad-369">處理序集區中的第一個 PID</span><span class="sxs-lookup"><span data-stu-id="4e3ad-369">The first PID in the process pool</span></span> |
| <span data-ttu-id="4e3ad-370">Description_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-370">Description_s</span></span> | <span data-ttu-id="4e3ad-371">處理序的描述</span><span class="sxs-lookup"><span data-stu-id="4e3ad-371">The process description</span></span> |
| <span data-ttu-id="4e3ad-372">CompanyName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-372">CompanyName_s</span></span> | <span data-ttu-id="4e3ad-373">公司的名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-373">The name of the company</span></span> |
| <span data-ttu-id="4e3ad-374">InternalName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-374">InternalName_s</span></span> | <span data-ttu-id="4e3ad-375">內部名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-375">The internal name</span></span> |
| <span data-ttu-id="4e3ad-376">ProductName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-376">ProductName_s</span></span> | <span data-ttu-id="4e3ad-377">產品的名稱</span><span class="sxs-lookup"><span data-stu-id="4e3ad-377">The name of the product</span></span> |
| <span data-ttu-id="4e3ad-378">ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-378">ProductVersion_s</span></span> | <span data-ttu-id="4e3ad-379">產品版本</span><span class="sxs-lookup"><span data-stu-id="4e3ad-379">The product version</span></span> |
| <span data-ttu-id="4e3ad-380">FileVersion_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-380">FileVersion_s</span></span> | <span data-ttu-id="4e3ad-381">檔案版本</span><span class="sxs-lookup"><span data-stu-id="4e3ad-381">The file version</span></span> |
| <span data-ttu-id="4e3ad-382">CommandLine_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-382">CommandLine_s</span></span> | <span data-ttu-id="4e3ad-383">命令列</span><span class="sxs-lookup"><span data-stu-id="4e3ad-383">The command line</span></span> |
| <span data-ttu-id="4e3ad-384">ExecutablePath _s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-384">ExecutablePath _s</span></span> | <span data-ttu-id="4e3ad-385">可執行檔的路徑</span><span class="sxs-lookup"><span data-stu-id="4e3ad-385">The path to the executable file</span></span> |
| <span data-ttu-id="4e3ad-386">WorkingDirectory_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-386">WorkingDirectory_s</span></span> | <span data-ttu-id="4e3ad-387">工作目錄</span><span class="sxs-lookup"><span data-stu-id="4e3ad-387">The working directory</span></span> |
| <span data-ttu-id="4e3ad-388">UserName</span><span class="sxs-lookup"><span data-stu-id="4e3ad-388">UserName</span></span> | <span data-ttu-id="4e3ad-389">執行處理序的帳戶</span><span class="sxs-lookup"><span data-stu-id="4e3ad-389">The account under which the process is executing</span></span> |
| <span data-ttu-id="4e3ad-390">UserDomain</span><span class="sxs-lookup"><span data-stu-id="4e3ad-390">UserDomain</span></span> | <span data-ttu-id="4e3ad-391">執行處理序的網域</span><span class="sxs-lookup"><span data-stu-id="4e3ad-391">The domain under which the process is executing</span></span> |


## <a name="sample-log-searches"></a><span data-ttu-id="4e3ad-392">記錄搜尋範例</span><span class="sxs-lookup"><span data-stu-id="4e3ad-392">Sample log searches</span></span>

### <a name="list-all-known-machines"></a><span data-ttu-id="4e3ad-393">列出所有已知的機器</span><span class="sxs-lookup"><span data-stu-id="4e3ad-393">List all known machines</span></span>
<span data-ttu-id="4e3ad-394">Type=ServiceMapComputer_CL | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-394">Type=ServiceMapComputer_CL | dedup ResourceId</span></span>

### <a name="list-the-physical-memory-capacity-of-all-managed-computers"></a><span data-ttu-id="4e3ad-395">列出所有受管理電腦的實體記憶體容量。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-395">List the physical memory capacity of all managed computers.</span></span>
<span data-ttu-id="4e3ad-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-396">Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId</span></span>

### <a name="list-computer-name-dns-ip-and-os"></a><span data-ttu-id="4e3ad-397">列出電腦名稱、DNS、IP 和 OS。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-397">List computer name, DNS, IP, and OS.</span></span>
<span data-ttu-id="4e3ad-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-398">Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId</span></span>

### <a name="find-all-processes-with-sql-in-the-command-line"></a><span data-ttu-id="4e3ad-399">在命令列中尋找具有「sql」的所有處理程序</span><span class="sxs-lookup"><span data-stu-id="4e3ad-399">Find all processes with "sql" in the command line</span></span>
<span data-ttu-id="4e3ad-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-400">Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-resource-name"></a><span data-ttu-id="4e3ad-401">以資源名稱尋找機器 (最新的記錄)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-401">Find a machine (most recent record) by resource name</span></span>
<span data-ttu-id="4e3ad-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-402">Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="find-a-machine-most-recent-record-by-ip-address"></a><span data-ttu-id="4e3ad-403">以 IP 位址尋找機器 (最新的記錄)</span><span class="sxs-lookup"><span data-stu-id="4e3ad-403">Find a machine (most recent record) by IP address</span></span>
<span data-ttu-id="4e3ad-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-404">Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId</span></span>

### <a name="list-all-known-processes-on-a-specified-machine"></a><span data-ttu-id="4e3ad-405">列出指定機器上的所有已知處理序</span><span class="sxs-lookup"><span data-stu-id="4e3ad-405">List all known processes on a specified machine</span></span>
<span data-ttu-id="4e3ad-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span><span class="sxs-lookup"><span data-stu-id="4e3ad-406">Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId</span></span>

### <a name="list-all-computers-running-sql"></a><span data-ttu-id="4e3ad-407">列出所有執行 SQL 的電腦</span><span class="sxs-lookup"><span data-stu-id="4e3ad-407">List all computers running SQL</span></span>
<span data-ttu-id="4e3ad-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-408">Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s</span></span>

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a><span data-ttu-id="4e3ad-409">列出資料中心內所有唯一 curl 產品版本</span><span class="sxs-lookup"><span data-stu-id="4e3ad-409">List all unique product versions of curl in my datacenter</span></span>
<span data-ttu-id="4e3ad-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-410">Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s</span></span>

### <a name="create-a-computer-group-of-all-computers-running-centos"></a><span data-ttu-id="4e3ad-411">為所有執行 CentOS 的電腦建立電腦群組</span><span class="sxs-lookup"><span data-stu-id="4e3ad-411">Create a computer group of all computers running CentOS</span></span>
<span data-ttu-id="4e3ad-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span><span class="sxs-lookup"><span data-stu-id="4e3ad-412">Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s</span></span>


## <a name="rest-api"></a><span data-ttu-id="4e3ad-413">REST API</span><span class="sxs-lookup"><span data-stu-id="4e3ad-413">REST API</span></span>
<span data-ttu-id="4e3ad-414">服務對應中所有的伺服器、處理序及相依性資料，都可透過[服務對應 REST API](https://docs.microsoft.com/rest/api/servicemap/) 取得。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-414">All the server, process, and dependency data in Service Map is available via the [Service Map REST API](https://docs.microsoft.com/rest/api/servicemap/).</span></span>


## <a name="diagnostic-and-usage-data"></a><span data-ttu-id="4e3ad-415">診斷和使用量資料</span><span class="sxs-lookup"><span data-stu-id="4e3ad-415">Diagnostic and usage data</span></span>
<span data-ttu-id="4e3ad-416">當您使用服務對應服務時，Microsoft 會自動收集使用量和效能資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-416">Microsoft automatically collects usage and performance data through your use of the Service Map service.</span></span> <span data-ttu-id="4e3ad-417">Microsoft 使用這項資料來提供和改進服務對應服務的品質、安全性和完整性。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-417">Microsoft uses this data to provide and improve the quality, security, and integrity of the Service Map service.</span></span> <span data-ttu-id="4e3ad-418">資料中包含軟體設定的相關資訊，像是作業系統與版本、IP 位址、DNS 名稱和工作站名稱，以便能夠正確且有效率地進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-418">To provide accurate and efficient troubleshooting capabilities, the data includes information about the configuration of your software, such as operating system and version, IP address, DNS name, and workstation name.</span></span> <span data-ttu-id="4e3ad-419">Microsoft 不會收集姓名、地址或其他連絡資訊。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-419">Microsoft does not collect names, addresses, or other contact information.</span></span>

<span data-ttu-id="4e3ad-420">如需有關資料收集與使用方式的詳細資訊，請參閱 [Microsoft 線上服務隱私權聲明](https://go.microsoft.com/fwlink/?LinkId=512132)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-420">For more information about data collection and usage, see the [Microsoft Online Services Privacy Statement](https://go.microsoft.com/fwlink/?LinkId=512132).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4e3ad-421">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e3ad-421">Next steps</span></span>
<span data-ttu-id="4e3ad-422">深入了解 Log Analytics 中的[記錄搜尋](../log-analytics/log-analytics-log-searches.md)，以擷取服務對應所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-422">Learn more about [log searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to retrieve data that's collected by Service Map.</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="4e3ad-423">疑難排解</span><span class="sxs-lookup"><span data-stu-id="4e3ad-423">Troubleshooting</span></span>
<span data-ttu-id="4e3ad-424">請參閱[設定服務對應文件的疑難排解小節](operations-management-suite-service-map-configure.md#troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-424">See the [Troubleshooting section of the Configuring Service Map document](operations-management-suite-service-map-configure.md#troubleshooting).</span></span>


## <a name="feedback"></a><span data-ttu-id="4e3ad-425">意見反應</span><span class="sxs-lookup"><span data-stu-id="4e3ad-425">Feedback</span></span>
<span data-ttu-id="4e3ad-426">您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？</span><span class="sxs-lookup"><span data-stu-id="4e3ad-426">Do you have any feedback for us about Service Map or this documentation?</span></span>  <span data-ttu-id="4e3ad-427">請瀏覽我們的[使用者意見頁面](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) \(英文\)，您可以在此頁面提出功能建議或對現有的建議進行投票。</span><span class="sxs-lookup"><span data-stu-id="4e3ad-427">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote up existing suggestions.</span></span>
