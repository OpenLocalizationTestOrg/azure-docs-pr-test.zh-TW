---
title: "服務對應與 System Center Operations Manager 的整合 | Microsoft Docs"
description: "服務對應是一個 Operations Management Suite 解決方案，可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。 本文說明使用服務對應在 Operations Manager 中自動建立分散式應用程式圖表。"
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
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="c6b13-104">服務對應與 System Center Operations Manager 的整合</span><span class="sxs-lookup"><span data-stu-id="c6b13-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="c6b13-105">這項功能處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="c6b13-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="c6b13-106">Operations Management Suite 服務對應可自動探索 Windows 和 Linux 系統上的應用程式元件，並對應服務之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="c6b13-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="c6b13-107">服務對應可讓您以您對伺服器的理解方式 (一個提供重要服務的互連系統) 來檢視它們。</span><span class="sxs-lookup"><span data-stu-id="c6b13-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="c6b13-108">服務對應不需要進行任何設定，只要安裝代理程式就能顯示橫跨任何 TCP 連接架構的伺服器、處理程序和連接埠之間的連線。</span><span class="sxs-lookup"><span data-stu-id="c6b13-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="c6b13-109">如需詳細資訊，請參閱[服務對應文件](operations-management-suite-service-map.md)。</span><span class="sxs-lookup"><span data-stu-id="c6b13-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="c6b13-110">透過這項服務對應與 System Center Operations Manager 之間的整合，您便可以在根據服務對應中動態相依性對應的 Operations Manager 中，自動建立分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="c6b13-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6b13-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="c6b13-111">Prerequisites</span></span>
* <span data-ttu-id="c6b13-112">管理一組伺服器的 Operations Manager 管理群組。</span><span class="sxs-lookup"><span data-stu-id="c6b13-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="c6b13-113">已啟用服務對應解決方案的 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="c6b13-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="c6b13-114">由 Operations Manager 管理並傳送資料至服務對應的一組伺服器 (至少一部)。</span><span class="sxs-lookup"><span data-stu-id="c6b13-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="c6b13-115">支援 Windows 和 Linux 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6b13-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="c6b13-116">可存取與 Operations Management Suite 工作區相關聯之 Azure 訂用帳戶的服務主體。</span><span class="sxs-lookup"><span data-stu-id="c6b13-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="c6b13-117">如需詳細資訊，請移至[建立服務主體](#creating-a-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="c6b13-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="c6b13-118">安裝服務對應管理組件</span><span class="sxs-lookup"><span data-stu-id="c6b13-118">Install the Service Map management pack</span></span>
<span data-ttu-id="c6b13-119">您必須透過匯入 Microsoft.SystemCenter.ServiceMap 管理組件配套 (Microsoft.SystemCenter.ServiceMap.mpb)，以啟用 Operations Manager 與服務對應之間的整合。</span><span class="sxs-lookup"><span data-stu-id="c6b13-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="c6b13-120">此配套包含下列管理組件︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="c6b13-121">Microsoft Service Map Application Views</span><span class="sxs-lookup"><span data-stu-id="c6b13-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="c6b13-122">Microsoft System Center Service Map Internal</span><span class="sxs-lookup"><span data-stu-id="c6b13-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="c6b13-123">Microsoft System Center Service Map Overrides</span><span class="sxs-lookup"><span data-stu-id="c6b13-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="c6b13-124">Microsoft System Center Service Map</span><span class="sxs-lookup"><span data-stu-id="c6b13-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="c6b13-125">設定服務對應整合</span><span class="sxs-lookup"><span data-stu-id="c6b13-125">Configure the Service Map integration</span></span>
<span data-ttu-id="c6b13-126">在您安裝服務對應管理組件之後，[管理] 窗格中的 [Operations Management Suite] 底下會顯示新的節點 [服務對應]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="c6b13-127">若要設定服務對應整合，請執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="c6b13-128">若要開啟設定精靈，在 [服務對應概觀] 窗格中，按一下 [新增工作區]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![[服務對應概觀] 窗格](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="c6b13-130">在 [連線設定] 視窗中，輸入租用戶名稱或識別碼、應用程式識別碼 (也稱為使用者名稱或用戶端識別碼) 以及服務主體的密碼，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="c6b13-131">如需詳細資訊，請移至[建立服務主體](#creating-a-service-principal)。</span><span class="sxs-lookup"><span data-stu-id="c6b13-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![[連線設定] 視窗](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="c6b13-133">在 [訂用帳戶選取] 視窗中，選取 Azure 訂用帳戶、Azure 資源群組 (即包含 Operations Management Suite 工作區的資源群組) 以及 Operations Management Suite 工作區，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Operations Manager 設定工作區](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="c6b13-135">在 [機器群組選取項目] 視窗中，您要選擇您想要同步至 Operations Manager 的服務對應機器群組。</span><span class="sxs-lookup"><span data-stu-id="c6b13-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="c6b13-136">按一下 [新增/移除機器群組]，從 [可用的機器群組] 清單中選擇群組，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="c6b13-137">當您完成群組選取時，按一下 [確定] 來完成。</span><span class="sxs-lookup"><span data-stu-id="c6b13-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Operations Manager 設定機器群組](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="c6b13-139">在 [伺服器選取] 視窗中，設定服務對應伺服器群組，以及您想要在 Operations Manager 和服務對應之間同步的伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6b13-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="c6b13-140">按一下 [新增/移除伺服器]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="c6b13-141">若要讓整合針對伺服器建立分散式應用程式圖表，該伺服器必須是︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="c6b13-142">由 Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="c6b13-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="c6b13-143">由服務對應管理</span><span class="sxs-lookup"><span data-stu-id="c6b13-143">Managed by Service Map</span></span>
    * <span data-ttu-id="c6b13-144">列於服務對應伺服器群組中</span><span class="sxs-lookup"><span data-stu-id="c6b13-144">Listed in the Service Map Servers Group</span></span>

    ![Operations Manager 設定群組](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="c6b13-146">選擇性︰選取管理伺服器資源集區以和 Operations Management Suite 通訊，然後按一下 [新增工作區]。</span><span class="sxs-lookup"><span data-stu-id="c6b13-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Operations Manager 設定資源集區](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="c6b13-148">設定和註冊 Operations Management Suite 工作區可能需要一分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c6b13-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="c6b13-149">完成設定之後，Operations Manager 就會從 Operations Management Suite 初始化首次的服務對應同步處理。</span><span class="sxs-lookup"><span data-stu-id="c6b13-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Operations Manager 設定資源集區](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="c6b13-151">監視服務對應</span><span class="sxs-lookup"><span data-stu-id="c6b13-151">Monitor Service Map</span></span>
<span data-ttu-id="c6b13-152">連線至 Operations Management Suite 工作區之後，Operations Manager 主控台的 [監視] 窗格中會顯示新的 [服務對應] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c6b13-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Operations Manager [監視] 窗格](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="c6b13-154">服務對應資料夾有四個節點︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="c6b13-155">**作用中警示**：列出有關 Operations Manager 和服務對應之通訊的所有作用中警示。</span><span class="sxs-lookup"><span data-stu-id="c6b13-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="c6b13-156">請注意，這些警示不是要同步至 Operations Manager 的 Operations Management Suite 警示。</span><span class="sxs-lookup"><span data-stu-id="c6b13-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="c6b13-157">**伺服器**：列出設定為從服務對應同步處理的受監視伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6b13-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Operations Manager [監視伺服器] 窗格](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="c6b13-159">**機器群組相依性檢視**：列出從服務對應同步處理的所有機器群組。</span><span class="sxs-lookup"><span data-stu-id="c6b13-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="c6b13-160">您可以按一下任何群組，以檢視其分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="c6b13-160">You can click any group to view its distributed application diagram.</span></span>

    ![Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="c6b13-162">**伺服器相依性檢視**：列出從服務對應同步處理的所有伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6b13-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="c6b13-163">您可以按一下任何伺服器，以檢視其分散式應用程式圖表。</span><span class="sxs-lookup"><span data-stu-id="c6b13-163">You can click any server to view its distributed application diagram.</span></span>

    ![Operations Manager 分散式應用程式圖表](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="c6b13-165">編輯或刪除工作區</span><span class="sxs-lookup"><span data-stu-id="c6b13-165">Edit or delete the workspace</span></span>
<span data-ttu-id="c6b13-166">您可以透過 [服務對應概觀] 窗格 ([系統管理] 窗格 > [Operations Management Suite] > [服務對應]) 編輯或刪除已設定的工作區。</span><span class="sxs-lookup"><span data-stu-id="c6b13-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="c6b13-167">目前您僅可設定一個 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="c6b13-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Operations Manager [編輯工作區] 窗格](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="c6b13-169">設定規則和覆寫</span><span class="sxs-lookup"><span data-stu-id="c6b13-169">Configure rules and overrides</span></span>
<span data-ttu-id="c6b13-170">系統會建立規則 _Microsoft.SystemCenter.ServiceMapImport.Rule_，以便定期從服務對應擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="c6b13-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="c6b13-171">若要變更同步時間，您可以設定規則的覆寫 ([撰寫] 窗格 > [規則] > [Microsoft.SystemCenter.ServiceMapImport.Rule])。</span><span class="sxs-lookup"><span data-stu-id="c6b13-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Operations Manager [覆寫內容] 視窗](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="c6b13-173">**Enabled**：啟用或停用自動更新。</span><span class="sxs-lookup"><span data-stu-id="c6b13-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="c6b13-174">**IntervalMinutes**︰重設更新之間的時間。</span><span class="sxs-lookup"><span data-stu-id="c6b13-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="c6b13-175">預設間隔是一小時。</span><span class="sxs-lookup"><span data-stu-id="c6b13-175">The default interval is one hour.</span></span> <span data-ttu-id="c6b13-176">如果您想要更頻繁地同步伺服器對應，您可以變更此值。</span><span class="sxs-lookup"><span data-stu-id="c6b13-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="c6b13-177">**TimeoutSeconds**︰重設要求逾時之前的時間長度。</span><span class="sxs-lookup"><span data-stu-id="c6b13-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="c6b13-178">**TimeWindowMinutes**：重設查詢資料的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="c6b13-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="c6b13-179">預設間隔為 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="c6b13-179">Default is a 60-minute window.</span></span> <span data-ttu-id="c6b13-180">服務對應所允許的最大值為 60 分鐘。</span><span class="sxs-lookup"><span data-stu-id="c6b13-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="c6b13-181">已知問題與限制</span><span class="sxs-lookup"><span data-stu-id="c6b13-181">Known issues and limitations</span></span>

<span data-ttu-id="c6b13-182">目前的設計有以下問題和限制︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="c6b13-183">您只能連線到單一 Operations Management Suite 工作區。</span><span class="sxs-lookup"><span data-stu-id="c6b13-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="c6b13-184">雖然您可以透過 [撰寫] 窗格將伺服器手動新增至服務對應伺服器群組，但這些伺服器的對應不會立即進行同步。</span><span class="sxs-lookup"><span data-stu-id="c6b13-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="c6b13-185">這些對應會在下一個同步週期從服務對應進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="c6b13-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="c6b13-186">如果您對管理組件所建立的「分散式應用程式圖表」進行任何變更，這些變更可能會在下一次與服務對應進行同步時遭到覆寫。</span><span class="sxs-lookup"><span data-stu-id="c6b13-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="c6b13-187">建立服務主體</span><span class="sxs-lookup"><span data-stu-id="c6b13-187">Create a service principal</span></span>
<span data-ttu-id="c6b13-188">如需建立服務主體的官方 Azure 文件，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="c6b13-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="c6b13-189">使用 PowerShell 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="c6b13-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="c6b13-190">使用 Azure CLI 建立服務主體</span><span class="sxs-lookup"><span data-stu-id="c6b13-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="c6b13-191">使用 Azure 入口網站建立服務主體</span><span class="sxs-lookup"><span data-stu-id="c6b13-191">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="c6b13-192">意見反應</span><span class="sxs-lookup"><span data-stu-id="c6b13-192">Feedback</span></span>
<span data-ttu-id="c6b13-193">您對「服務對應」或這份文件有任何意見反應要提供給我們嗎？</span><span class="sxs-lookup"><span data-stu-id="c6b13-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="c6b13-194">請瀏覽我們的 [User Voice 頁面 (英文)](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map)，您可以在此頁面提出功能建議或對現有的建議進行投票。</span><span class="sxs-lookup"><span data-stu-id="c6b13-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
