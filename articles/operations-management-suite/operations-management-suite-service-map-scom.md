---
title: "aaaService 對應整合 System Center Operations Manager |Microsoft 文件"
description: "服務對應是一種 Operations Management Suite 解決方案，它會自動探索 Windows 上的應用程式元件和 Linux 系統和對應 hello 服務之間的通訊。 這篇文章討論如何使用服務對應 tooautomatically Operations Manager 中建立分散式應用程式圖表。"
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="5da99-104">服務對應與 System Center Operations Manager 的整合</span><span class="sxs-lookup"><span data-stu-id="5da99-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="5da99-105">這項功能處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="5da99-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="5da99-106">Operations Management Suite 服務對應會自動探索 Windows 和 Linux 系統上的應用程式元件，並將對應 hello 服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="5da99-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="5da99-107">服務對應可讓您 tooview 伺服器 hello 好您將項目，視為互連提供重要服務的系統。</span><span class="sxs-lookup"><span data-stu-id="5da99-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="5da99-108">服務對應可顯示在任何 TCP 連接的架構，而不需要除了 hello 代理程式安裝設定伺服器、 處理程序與連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="5da99-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="5da99-109">如需詳細資訊，請參閱 hello[服務對應文件](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="5da99-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="5da99-110">與此服務對應和 System Center Operations Manager 之間的整合，您可以在 Operations Manager 服務對應中的 hello 動態相依性地圖為基礎的自動建立分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="5da99-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5da99-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="5da99-111">Prerequisites</span></span>
* <span data-ttu-id="5da99-112">管理一組伺服器的 Operations Manager 管理群組。</span><span class="sxs-lookup"><span data-stu-id="5da99-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="5da99-113">Hello 服務對應方案啟用與 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="5da99-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="5da99-114">一組伺服器 （至少一個） 是受管理的 Operations Manager 和傳送資料 tooService 對應。</span><span class="sxs-lookup"><span data-stu-id="5da99-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="5da99-115">支援 Windows 和 Linux 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5da99-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="5da99-116">可存取 toohello hello Operations Management Suite 工作區相關聯的 Azure 訂用帳戶的服務主體。</span><span class="sxs-lookup"><span data-stu-id="5da99-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="5da99-117">如需詳細資訊，請移至太[建立服務主體](#creating-a-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="5da99-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="5da99-118">安裝 hello 服務對應管理組件</span><span class="sxs-lookup"><span data-stu-id="5da99-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="5da99-119">您可以匯入 hello Microsoft.SystemCenter.ServiceMap 管理組件配套 (Microsoft.SystemCenter.ServiceMap.mpb) 啟用 hello 和之間的整合 Operations Manager 服務對應。</span><span class="sxs-lookup"><span data-stu-id="5da99-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="5da99-120">hello 配套包含下列管理組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5da99-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="5da99-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="5da99-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="5da99-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="5da99-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="5da99-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="5da99-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="5da99-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="5da99-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="5da99-125">設定 hello 服務對應整合</span><span class="sxs-lookup"><span data-stu-id="5da99-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="5da99-126">安裝 hello 服務對應管理組件，新的節點之後**服務對應**，會顯示下**Operations Management Suite**在 hello**管理**窗格。</span><span class="sxs-lookup"><span data-stu-id="5da99-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="5da99-127">tooconfigure 服務對應整合，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="5da99-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="5da99-128">tooopen hello 組態精靈 的 hello**服務對應概觀** 窗格中，按一下 **加入工作區**。</span><span class="sxs-lookup"><span data-stu-id="5da99-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![[服務對應概觀] 窗格](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="5da99-130">在 hello**連接組態**視窗中，輸入 hello 租用戶名稱或識別碼、 應用程式識別碼 （也稱為 hello 使用者名稱或 clientID） 及 hello 服務主體的密碼，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5da99-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="5da99-131">如需詳細資訊，請移至太[建立服務主體](#creating-a-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="5da99-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![hello 連線組態視窗](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="5da99-133">在 hello**訂閱選取項目**視窗中，選取 hello Azure 訂用帳戶、 Azure 資源群組 (hello 另一個則包含 hello Operations Management Suite 工作區) 和 Operations Management Suite 工作區中，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="5da99-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![hello Operations Manager 設定 工作區](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="5da99-135">在 hello**群組選擇機器**視窗，請選擇哪些服務對應電腦群組想 toosync tooOperations 管理員。</span><span class="sxs-lookup"><span data-stu-id="5da99-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="5da99-136">按一下**新增/移除電腦群組**，選擇 hello 清單群組**可用的電腦群組**，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5da99-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="5da99-137">當您完成選取群組，請按一下**確定**toofinish。</span><span class="sxs-lookup"><span data-stu-id="5da99-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![hello Operations Manager 設定機器群組](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="5da99-139">在 hello**伺服器選取項目**視窗中，您設定 hello 服務對應的伺服器群組與您想要 Operations Manager 與服務對應 toosync hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5da99-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="5da99-140">按一下 [新增/移除伺服器]。</span><span class="sxs-lookup"><span data-stu-id="5da99-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="5da99-141">Hello 伺服器 hello 整合 toobuild 伺服器的分散式應用程式圖表，必須是：</span><span class="sxs-lookup"><span data-stu-id="5da99-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="5da99-142">由 Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="5da99-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="5da99-143">由服務對應管理</span><span class="sxs-lookup"><span data-stu-id="5da99-143">Managed by Service Map</span></span>
    * <span data-ttu-id="5da99-144">列在 hello 服務對應的伺服器群組</span><span class="sxs-lookup"><span data-stu-id="5da99-144">Listed in hello Service Map Servers Group</span></span>

    ![hello Operations Manager 設定群組](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="5da99-146">選擇性： 選取 hello 管理伺服器資源集區 toocommunicate 利用 Operations Management Suite，然後再按一下**加入工作區**。</span><span class="sxs-lookup"><span data-stu-id="5da99-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![hello Operations Manager 設定資源集區](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="5da99-148">可能需要分鐘 tooconfigure 並註冊 hello Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="5da99-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="5da99-149">設定它後，Operations Manager 會起始從 Operations Management Suite hello 第一個服務對應同步。</span><span class="sxs-lookup"><span data-stu-id="5da99-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![hello Operations Manager 設定資源集區](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="5da99-151">監視服務對應</span><span class="sxs-lookup"><span data-stu-id="5da99-151">Monitor Service Map</span></span>
<span data-ttu-id="5da99-152">新的資料夾，服務對應 hello Operations Management Suite 工作區已連接之後，會顯示在 hello**監視**hello Operations Manager 主控台窗格。</span><span class="sxs-lookup"><span data-stu-id="5da99-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![hello Operations Manager 監視中 窗格](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="5da99-154">hello 服務對應的資料夾有四個節點：</span><span class="sxs-lookup"><span data-stu-id="5da99-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="5da99-155">**作用中警示**： 列出有關 hello 通訊，Operations Manager 與服務對應的 hello 作用中警示。</span><span class="sxs-lookup"><span data-stu-id="5da99-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="5da99-156">請注意，這些警示不是正在同步處理的 tooOperations Manager 的 Operations Management Suite 的資訊警示。</span><span class="sxs-lookup"><span data-stu-id="5da99-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="5da99-157">**伺服器**： 列出 hello 監視的伺服器設定 toosync 從服務對應。</span><span class="sxs-lookup"><span data-stu-id="5da99-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![hello Operations Manager 監視的伺服器 窗格](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="5da99-159">**機器群組相依性檢視**：列出從服務對應同步處理的所有機器群組。</span><span class="sxs-lookup"><span data-stu-id="5da99-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="5da99-160">您可以按一下任何群組 tooview 其分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="5da99-160">You can click any group tooview its distributed application diagram.</span></span>

    ![hello Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="5da99-162">**伺服器相依性檢視**：列出從服務對應同步處理的所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="5da99-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="5da99-163">您可以按一下任何伺服器 tooview 其分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="5da99-163">You can click any server tooview its distributed application diagram.</span></span>

    ![hello Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="5da99-165">編輯或刪除 hello 工作區</span><span class="sxs-lookup"><span data-stu-id="5da99-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="5da99-166">您可以編輯或刪除 hello 設定工作區透過 hello**服務對應概觀**窗格 (**管理**窗格 > **Operations Management Suite**  > **服務對應**)。</span><span class="sxs-lookup"><span data-stu-id="5da99-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="5da99-167">目前您僅可設定一個 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="5da99-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![hello Operations Manager 編輯工作區 窗格](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="5da99-169">設定規則和覆寫</span><span class="sxs-lookup"><span data-stu-id="5da99-169">Configure rules and overrides</span></span>
<span data-ttu-id="5da99-170">一般而言， _Microsoft.SystemCenter.ServiceMapImport.Rule_，從服務對應建立 tooperiodically 提取資訊。</span><span class="sxs-lookup"><span data-stu-id="5da99-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="5da99-171">toochange 同步時間，您可以設定的 hello 規則覆寫 (**製作**窗格 >**規則** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="5da99-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![hello Operations Manager 會覆寫屬性 視窗](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="5da99-173">**Enabled**：啟用或停用自動更新。</span><span class="sxs-lookup"><span data-stu-id="5da99-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="5da99-174">**IntervalMinutes**： 重設 hello 更新之間的時間。</span><span class="sxs-lookup"><span data-stu-id="5da99-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="5da99-175">hello 預設間隔為一小時。</span><span class="sxs-lookup"><span data-stu-id="5da99-175">hello default interval is one hour.</span></span> <span data-ttu-id="5da99-176">若要更頻繁地 toosync server 對應，您可以變更 hello 值。</span><span class="sxs-lookup"><span data-stu-id="5da99-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="5da99-177">**Timeoutseconds 設定**： 重設 hello hello 要求逾時之前的時間長度。</span><span class="sxs-lookup"><span data-stu-id="5da99-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="5da99-178">**TimeWindowMinutes**： 重設 hello 時間間隔查詢資料。</span><span class="sxs-lookup"><span data-stu-id="5da99-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="5da99-179">預設間隔為 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5da99-179">Default is a 60-minute window.</span></span> <span data-ttu-id="5da99-180">hello 服務對應所允許的最大值為 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5da99-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="5da99-181">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="5da99-181">Known issues and limitations</span></span>

<span data-ttu-id="5da99-182">hello 目前設計顯示 hello 以下問題和限制：</span><span class="sxs-lookup"><span data-stu-id="5da99-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="5da99-183">您只能連接單一 tooa Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="5da99-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="5da99-184">雖然您可以新增伺服器 toohello 服務對應的伺服器群組手動透過 hello**製作** 窗格中，這些伺服器 hello 對應未立即同步處理。</span><span class="sxs-lookup"><span data-stu-id="5da99-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="5da99-185">它們將在 hello 下一個同步處理循環期間同步處理從服務對應。</span><span class="sxs-lookup"><span data-stu-id="5da99-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="5da99-186">如果 toohello 分散式應用程式圖表建立 hello 管理組件進行任何變更，這些變更將可能會覆寫 hello 與服務對應的下一個同步處理。</span><span class="sxs-lookup"><span data-stu-id="5da99-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="5da99-187">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="5da99-187">Create a service principal</span></span>
<span data-ttu-id="5da99-188">如需建立服務主體的官方 Azure 文件，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="5da99-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="5da99-189">使用 PowerShell 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="5da99-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="5da99-190">使用 Azure CLI 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="5da99-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="5da99-191">建立服務主體使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="5da99-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="5da99-192">意見反應</span><span class="sxs-lookup"><span data-stu-id="5da99-192">Feedback</span></span>
<span data-ttu-id="5da99-193">您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？</span><span class="sxs-lookup"><span data-stu-id="5da99-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="5da99-194">請瀏覽我們的 [User Voice 頁面 (英文)](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)，您可以在此頁面提出功能建議或對現有的建議進行投票。</span><span class="sxs-lookup"><span data-stu-id="5da99-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
