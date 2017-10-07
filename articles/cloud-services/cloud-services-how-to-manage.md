---
title: "aaaCommon 雲端服務的管理工作 （傳統） |Microsoft 文件"
description: "了解如何 toomanage 雲端服務的 hello Azure 傳統入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="fd390-103">如何 tooManage 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fd390-103">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd390-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fd390-104">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="fd390-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="fd390-105">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="fd390-106">在 hello**雲端服務**區域 hello Azure 傳統入口網站中，您可以更新服務角色或部署、 升級預備的部署 tooproduction、 連結資源 tooyour 雲端服務，讓您能夠查看 hello 資源相依性和小數位數 hello 資源在一起，並刪除雲端服務或部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-106">In hello **Cloud Services** area of hello Azure classic portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="fd390-107">作法：更新雲端服務角色或部署</span><span class="sxs-lookup"><span data-stu-id="fd390-107">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="fd390-108">如果您需要 tooupdate hello 應用程式程式碼為雲端服務時，使用**更新**hello 儀表板，**雲端服務** 頁面上，或**執行個體**頁面。</span><span class="sxs-lookup"><span data-stu-id="fd390-108">If you need tooupdate hello application code for your cloud service, use **Update** on hello dashboard, **Cloud Services** page, or **Instances** page.</span></span> <span data-ttu-id="fd390-109">您可以更新單一角色或所有角色。</span><span class="sxs-lookup"><span data-stu-id="fd390-109">You can update a single role or all roles.</span></span> <span data-ttu-id="fd390-110">您將需要 tooupload 新的服務封裝和服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="fd390-110">You'll need tooupload a new service package and service configuration file.</span></span>

1. <span data-ttu-id="fd390-111">在 [hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，hello 儀表板，**雲端服務**] 頁面上，或**執行個體**頁面上，按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="fd390-111">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. <span data-ttu-id="fd390-113">在**部署標籤**，輸入名稱 tooidentify hello 部署 (例如，mycloudservice4)。</span><span class="sxs-lookup"><span data-stu-id="fd390-113">In **Deployment label**, enter a name tooidentify hello deployment (for example, mycloudservice4).</span></span> <span data-ttu-id="fd390-114">您會發現下的 hello 部署標籤**快速入門**hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="fd390-114">You'll find hello deployment label under **quick start** on hello dashboard.</span></span>
3. <span data-ttu-id="fd390-115">在**封裝**，使用**瀏覽**tooupload hello 服務封裝檔 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="fd390-115">In **Package**, use **Browse** tooupload hello service package file (.cspkg).</span></span>
4. <span data-ttu-id="fd390-116">在**組態**，使用**瀏覽**tooupload hello 服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="fd390-116">In **Configuration**, use **Browse** tooupload hello service configuration file (.cscfg).</span></span>
5. <span data-ttu-id="fd390-117">在**角色**，選取**所有**hello 中的所有角色如果您想 tooupgrade 都雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-117">In **Role**, select **All** if you want tooupgrade all roles in hello cloud service.</span></span> <span data-ttu-id="fd390-118">tooperform 單一角色更新，您想要 tooupdate 選取 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="fd390-118">tooperform a single role update, select hello role you want tooupdate.</span></span> <span data-ttu-id="fd390-119">即使您選取特定角色 tooupdate，hello 服務組態檔中的 hello 更新會套用的 tooall 角色。</span><span class="sxs-lookup"><span data-stu-id="fd390-119">Even if you select a specific role tooupdate, hello updates in hello service configuration file are applied tooall roles.</span></span>
6. <span data-ttu-id="fd390-120">如果 hello 更新變更 hello 的角色數目或任何角色 hello 大小，選取 hello**角色大小或角色數目變更時，允許更新**核取方塊 tooenable hello 更新 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="fd390-120">If hello update changes hello number of roles or hello size of any role, select hello **Allow update if role sizes or number of roles changes** check box tooenable hello update tooproceed.</span></span>

    <span data-ttu-id="fd390-121">請注意，如果您變更 hello （也就是虛擬機器主控角色執行個體的 hello 大小） 的角色大小或 hello 」 角色數量時，必須重新製作映像，每個角色執行個體 （虛擬機器），而且任何本機資料將會遺失。</span><span class="sxs-lookup"><span data-stu-id="fd390-121">Be aware that if you change hello size of a role (that is, hello size of a virtual machine that hosts a role instance) or hello number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span></span>

7. <span data-ttu-id="fd390-122">如果服務的任何角色只能有一個角色執行個體，請選取 hello**更新，即使一個或多個角色包含單一執行個體的核取方塊**tooenable hello 升級 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="fd390-122">If any service roles have only one role instance, select hello **Update even if one or more role contain a single instance check box** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="fd390-123">要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="fd390-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="fd390-124">可讓一個虛擬機器 tooprocess 用戶端要求而正在更新其他 hello。</span><span class="sxs-lookup"><span data-stu-id="fd390-124">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span>

8. <span data-ttu-id="fd390-125">按一下**確定**（勾選記號） toobegin 更新 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-125">Click **OK** (checkmark) toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="fd390-126">如何： 交換部署 toopromote 預備的部署 tooproduction</span><span class="sxs-lookup"><span data-stu-id="fd390-126">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="fd390-127">使用**交換**toopromote 雲端服務 tooproduction 預備環境部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-127">Use **Swap** toopromote a staging deployment of a cloud service tooproduction.</span></span> <span data-ttu-id="fd390-128">當您決定 toodeploy 雲端服務的新版本時，您可以階段，然後在您的客戶在生產環境中使用 hello 目前版本時，雲端服務的預備環境中測試新版本。</span><span class="sxs-lookup"><span data-stu-id="fd390-128">When you decide toodeploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using hello current release in production.</span></span> <span data-ttu-id="fd390-129">當您準備好 toopromote hello 新發行 tooproduction，您可以使用**交換**兩個部署的位址由哪些 hello tooswitch hello Url。</span><span class="sxs-lookup"><span data-stu-id="fd390-129">When you're ready toopromote hello new release tooproduction, you can use **Swap** tooswitch hello URLs by which hello two deployments are addressed.</span></span>

<span data-ttu-id="fd390-130">您可以交換部署從 hello**雲端服務**頁面或 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="fd390-130">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="fd390-131">在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 **雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="fd390-131">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="fd390-132">在 hello 清單中的雲端服務，按一下 hello 雲端服務 tooselect 它。</span><span class="sxs-lookup"><span data-stu-id="fd390-132">In hello list of cloud services, click hello cloud service tooselect it.</span></span>
3. <span data-ttu-id="fd390-133">按一下 [交換] 。</span><span class="sxs-lookup"><span data-stu-id="fd390-133">Click **Swap**.</span></span>

    <span data-ttu-id="fd390-134">hello 下列確認提示隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="fd390-134">hello following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. <span data-ttu-id="fd390-136">確認 hello 部署資訊後，按一下**是**tooswap hello 部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-136">After you verify hello deployment information, click **Yes** tooswap hello deployments.</span></span>

    <span data-ttu-id="fd390-137">hello 部署交換很快就會因為 hello 唯一變更是 hello 虛擬 IP 位址 (Vip) hello 部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-137">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="fd390-138">toosave 運算成本，您可以刪除 hello 預備環境，當您確定 hello 新增生產部署如預期執行中的 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-138">toosave compute costs, you can delete hello deployment in hello staging environment when you're sure hello new production deployment is performing as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="fd390-139">交換部署的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="fd390-139">Common questions about swapping deployments</span></span>

<span data-ttu-id="fd390-140">**交換部署的 hello 必要條件為何？**</span><span class="sxs-lookup"><span data-stu-id="fd390-140">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="fd390-141">成功的部署交換有兩個主要必要條件：</span><span class="sxs-lookup"><span data-stu-id="fd390-141">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="fd390-142">如果您想要 toouse 靜態 IP 位址的生產位置，您必須保留以及您預備位置的其中一個。</span><span class="sxs-lookup"><span data-stu-id="fd390-142">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="fd390-143">否則，hello 交換將會失敗。</span><span class="sxs-lookup"><span data-stu-id="fd390-143">Otherwise, hello swap will fail.</span></span>

- <span data-ttu-id="fd390-144">必須先執行所有的執行個體的角色，您可以執行 hello 交換。</span><span class="sxs-lookup"><span data-stu-id="fd390-144">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="fd390-145">您可以查看您的執行個體在 hello Azure 傳統入口網站或使用 hello 狀態[hello Get-azurerole 命令在 Windows PowerShell 中的](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)。</span><span class="sxs-lookup"><span data-stu-id="fd390-145">You can check hello status of your instances in hello Azure classic portal or by using [hello Get-AzureRole command in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).</span></span>

<span data-ttu-id="fd390-146">請注意，客體作業系統更新和服務修復作業也可能會導致部署交換 toofail。</span><span class="sxs-lookup"><span data-stu-id="fd390-146">Note that guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="fd390-147">如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="fd390-148">**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**</span><span class="sxs-lookup"><span data-stu-id="fd390-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="fd390-149">Hello 最後一節所述，部署交換通常是非常快速因為它是只在 hello Azure 負載平衡器組態變更。</span><span class="sxs-lookup"><span data-stu-id="fd390-149">As described in hello last section, a deployment swap is typically very fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="fd390-150">不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="fd390-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="fd390-151">toolimit 影響 tooyour 客戶，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="fd390-152">如何： 連結資源 tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fd390-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="fd390-153">tooshow 您的雲端服務相依於其他資源，您可以將連結的 Azure SQL Database 執行個體或儲存體帳戶 toohello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-153">tooshow your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account toohello cloud service.</span></span> <span data-ttu-id="fd390-154">您可以連結，並取消連結資源的 hello**連結的資源**頁面，然後再監視其 hello 雲端服務儀表板上的使用量。</span><span class="sxs-lookup"><span data-stu-id="fd390-154">You can link and unlink resources on hello **Linked Resources** page, and then monitor their usage on hello cloud service dashboard.</span></span> <span data-ttu-id="fd390-155">如果監視開啟連結的儲存體帳戶，您可以監視 hello 雲端服務儀表板上的要求總數。</span><span class="sxs-lookup"><span data-stu-id="fd390-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on hello cloud service dashboard.</span></span>

<span data-ttu-id="fd390-156">使用**連結**toolink 新的或現有 SQL Database 執行個體或儲存體帳戶 tooyour 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-156">Use **Link** toolink a new or existing SQL Database instance or storage account tooyour cloud service.</span></span> <span data-ttu-id="fd390-157">然後，您可以調整 hello 資料庫正在使用它在 hello 的 hello 雲端服務角色以及**標尺**頁面。</span><span class="sxs-lookup"><span data-stu-id="fd390-157">You can then scale hello database along with hello cloud service role that is using it on hello **Scale** page.</span></span> <span data-ttu-id="fd390-158">(儲存體帳戶會在使用量增加時自動調整。)如需詳細資訊，請參閱[如何 tooScale 雲端服務和連結的資源](cloud-services-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-158">(A storage account scales automatically as usage increases.) For more information, see [How tooScale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="fd390-159">您也可以監視、 管理及調整 hello 資料庫在 hello**資料庫**hello Azure 傳統入口網站的節點。</span><span class="sxs-lookup"><span data-stu-id="fd390-159">You also can monitor, manage, and scale hello database in hello **Databases** node of hello Azure classic portal.</span></span>

<span data-ttu-id="fd390-160">「 連結 」 資源，這一點而言並不會連接您的應用程式 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="fd390-160">"Linking" a resource in this sense doesn't connect your app toohello resource.</span></span> <span data-ttu-id="fd390-161">如果您建立新的資料庫使用**連結**，您將需要 tooadd hello 連接字串 tooyour 應用程式程式碼，接著再升級 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-161">If you create a new database using **Link**, you'll need tooadd hello connection strings tooyour application code and then upgrade hello cloud service.</span></span> <span data-ttu-id="fd390-162">如果您的應用程式會使用資源的連結儲存體帳戶中，您也會需要 tooadd 連接字串。</span><span class="sxs-lookup"><span data-stu-id="fd390-162">You'll also need tooadd connection strings if your app uses resources in a linked storage account.</span></span>

<span data-ttu-id="fd390-163">hello 遵循程序描述如何 toolink 新的 SQL Database 執行個體上部署新的 SQL Database 伺服器，tooa 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="fd390-163">hello following procedure describes how toolink a new SQL Database instance, deployed on a new SQL Database server, tooa cloud service.</span></span>

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a><span data-ttu-id="fd390-164">toolink SQL Database 執行個體 tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="fd390-164">toolink a SQL Database instance tooa cloud service</span></span>
1. <span data-ttu-id="fd390-165">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="fd390-165">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="fd390-166">然後按一下 hello hello 雲端服務 tooopen hello 儀表板的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd390-166">Then click hello name of hello cloud service tooopen hello dashboard.</span></span>
2. <span data-ttu-id="fd390-167">按一下 [Linked Resources] 。</span><span class="sxs-lookup"><span data-stu-id="fd390-167">Click **Linked Resources**.</span></span>

    <span data-ttu-id="fd390-168">hello**連結的資源**頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="fd390-168">hello **Linked Resources** page opens.</span></span>

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. <span data-ttu-id="fd390-170">按一下 [連結資源] 或 [連結]。</span><span class="sxs-lookup"><span data-stu-id="fd390-170">Click either **Link a Resource** or **Link**.</span></span>

    <span data-ttu-id="fd390-171">hello**連結資源**精靈 隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="fd390-171">hello **Link Resource** wizard starts.</span></span>

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. <span data-ttu-id="fd390-173">按一下 [建立新的資源] 或 [連結現有的資源]。</span><span class="sxs-lookup"><span data-stu-id="fd390-173">Click **Create a new resource** or **Link an existing resource**.</span></span>
5. <span data-ttu-id="fd390-174">選擇資源 toolink hello 類型。</span><span class="sxs-lookup"><span data-stu-id="fd390-174">Choose hello type of resource toolink.</span></span> <span data-ttu-id="fd390-175">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下  **SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="fd390-175">In hello [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span></span> <span data-ttu-id="fd390-176">（hello Azure 傳統入口網站支援連結儲存體帳戶 tooa 雲端服務）。</span><span class="sxs-lookup"><span data-stu-id="fd390-176">(Only hello Azure classic portal supports linking a storage account tooa cloud service.)</span></span>
6. <span data-ttu-id="fd390-177">toocomplete hello 的資料庫組態，遵循 hello 的說明 中的指示**SQL 資料庫**hello Azure 傳統入口網站的區域。</span><span class="sxs-lookup"><span data-stu-id="fd390-177">toocomplete hello database configuration, follow instructions in help for hello **SQL Databases** area of hello Azure classic portal.</span></span>

    <span data-ttu-id="fd390-178">您可以遵循連結作業 hello 訊息區域中的 hello hello 進度。</span><span class="sxs-lookup"><span data-stu-id="fd390-178">You can follow hello progress of hello linking operation in hello message area.</span></span>

    <span data-ttu-id="fd390-179">連結完成時，您可以監視 hello hello 雲端服務儀表板上的 hello 連結資源的狀態。</span><span class="sxs-lookup"><span data-stu-id="fd390-179">When linking is complete, you can monitor hello status of hello linked resource on hello cloud service dashboard.</span></span> <span data-ttu-id="fd390-180">如需擴充連結的 SQL Database 的資訊，請參閱[如何 tooScale 雲端服務和連結的資源](cloud-services-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-180">For information about scaling a linked SQL Database, see [How tooScale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

### <a name="toounlink-a-linked-resource"></a><span data-ttu-id="fd390-181">toounlink 連結的資源</span><span class="sxs-lookup"><span data-stu-id="fd390-181">toounlink a linked resource</span></span>
1. <span data-ttu-id="fd390-182">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="fd390-182">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="fd390-183">然後按一下 hello hello 雲端服務 tooopen hello 儀表板的名稱。</span><span class="sxs-lookup"><span data-stu-id="fd390-183">Then click hello name of hello cloud service tooopen hello dashboard.</span></span>
2. <span data-ttu-id="fd390-184">按一下**連結的資源**，然後選取 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="fd390-184">Click **Linked Resources**, and then select hello resource.</span></span>
3. <span data-ttu-id="fd390-185">按一下 [取消連結] 。</span><span class="sxs-lookup"><span data-stu-id="fd390-185">Click **Unlink**.</span></span> <span data-ttu-id="fd390-186">然後按一下 **是**在 hello 確認提示。</span><span class="sxs-lookup"><span data-stu-id="fd390-186">Then click **Yes** at hello confirmation prompt.</span></span>

    <span data-ttu-id="fd390-187">取消連結 SQL Database 有 hello 資料庫或應用程式 hello toohello 資料庫的連接上沒有作用。</span><span class="sxs-lookup"><span data-stu-id="fd390-187">Unlinking a SQL Database has no effect on hello database or hello application's connections toohello database.</span></span> <span data-ttu-id="fd390-188">您仍然可以管理在 hello hello 資料庫**SQL 資料庫**hello Azure 傳統入口網站的區域。</span><span class="sxs-lookup"><span data-stu-id="fd390-188">You can still manage hello database in hello **SQL Databases** area of hello Azure classic portal.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="fd390-189">作法：刪除部署和雲端服務</span><span class="sxs-lookup"><span data-stu-id="fd390-189">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="fd390-190">刪除雲端服務之前，您必須先刪除每個現有的部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-190">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="fd390-191">toosave 運算成本，確認您的生產環境部署的運作正常之後，可以刪除您的預備環境部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-191">toosave compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="fd390-192">只要角色執行個體存在，您就需要為其支付運算成本，即使雲端服務未執行也一樣。</span><span class="sxs-lookup"><span data-stu-id="fd390-192">You are billed compute costs for role instances even if a cloud service is not running.</span></span>

<span data-ttu-id="fd390-193">部署或雲端服務，請使用下列程序 toodelete hello。</span><span class="sxs-lookup"><span data-stu-id="fd390-193">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="fd390-194">在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，按一下 **雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="fd390-194">In hello [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="fd390-195">選取 hello 雲端服務，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="fd390-195">Select hello cloud service, and then click **Delete**.</span></span> <span data-ttu-id="fd390-196">（tooselect 雲端服務，而不需要開啟 hello 儀表板中，按一下任何位置 hello 雲端服務項目中的 hello 名稱除外）。</span><span class="sxs-lookup"><span data-stu-id="fd390-196">(tooselect a cloud service without opening hello dashboard, click anywhere except hello name in hello cloud service entry.)</span></span>

    <span data-ttu-id="fd390-197">如果您擁有預備環境或生產環境部署，您會看到下列其中一個在 hello hello 視窗底部選擇類似 toohello 的功能表。</span><span class="sxs-lookup"><span data-stu-id="fd390-197">If you have a deployment in staging or production, you will see a menu of choices similar toohello following one at hello bottom of hello window.</span></span> <span data-ttu-id="fd390-198">您可以刪除 hello 雲端服務之前，您必須刪除現有的部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-198">Before you can delete hello cloud service, you must delete any existing deployments.</span></span>

    ![Delete Menu](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. <span data-ttu-id="fd390-200">toodelete 部署中，按一下**刪除生產部署**或**刪除預備環境部署**。</span><span class="sxs-lookup"><span data-stu-id="fd390-200">toodelete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span></span> <span data-ttu-id="fd390-201">然後，在 hello 確認提示按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="fd390-201">Then, at hello confirmation prompt, click **Yes**.</span></span>
4. <span data-ttu-id="fd390-202">如果您計劃 toodelete hello 雲端服務，請重複步驟 3，如有需要 toodelete 您其他的部署。</span><span class="sxs-lookup"><span data-stu-id="fd390-202">If you plan toodelete hello cloud service, repeat step 3, if needed, toodelete your other deployment.</span></span>
5. <span data-ttu-id="fd390-203">toodelete hello 雲端服務，請按一下**刪除雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="fd390-203">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="fd390-204">然後，在 hello 確認提示按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="fd390-204">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="fd390-205">如果設定為您的雲端服務的詳細資訊監視，Azure 不會刪除監視資料，從儲存體帳戶，當您刪除 hello 雲端服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="fd390-205">If verbose monitoring is configured for your cloud service, Azure does not delete hello monitoring data from your storage account when you delete hello cloud service.</span></span> <span data-ttu-id="fd390-206">您以手動方式需要 toodelete hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fd390-206">You will need toodelete hello data manually.</span></span> <span data-ttu-id="fd390-207">其中 toofind hello 度量資料表的相關資訊，請參閱 「 如何： 存取外部 hello Azure 傳統入口網站的詳細資訊監視資料 」 中[tooMonitor 雲端服務如何](cloud-services-how-to-monitor.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-207">For information about where toofind hello metrics tables, see "How to: Access verbose monitoring data outside hello Azure classic portal" in [How tooMonitor Cloud Services](cloud-services-how-to-monitor.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fd390-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd390-208">Next steps</span></span>
* <span data-ttu-id="fd390-209">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="fd390-210">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-210">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="fd390-211">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="fd390-212">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="fd390-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>
