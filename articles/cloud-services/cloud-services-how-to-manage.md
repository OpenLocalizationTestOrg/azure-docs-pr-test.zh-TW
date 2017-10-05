---
title: "常見的雲端服務管理工作 (傳統) | Microsoft Docs"
description: "了解如何在 Azure 傳統入口網站中管理雲端服務。"
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
ms.openlocfilehash: 2ee76dfcb579e53975b1f61a6590f8d78dc0961b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="f8c83-103">如何管理雲端服務</span><span class="sxs-lookup"><span data-stu-id="f8c83-103">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8c83-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f8c83-104">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="f8c83-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="f8c83-105">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="f8c83-106">在 Azure 傳統入口網站的 [ **雲端服務** ] 區域中，您可以更新服務角色或部署、將預備部署提升至生產、將資源連結至您的雲端服務以便於查看資源相依性，並將資源一起調整，以及刪除雲端服務或部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-106">In the **Cloud Services** area of the Azure classic portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="f8c83-107">作法：更新雲端服務角色或部署</span><span class="sxs-lookup"><span data-stu-id="f8c83-107">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="f8c83-108">如果您需要更新雲端服務的應用程式程式碼，請使用儀表板上、[雲端服務] 頁面上或 [執行個體] 頁面上的 [更新]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-108">If you need to update the application code for your cloud service, use **Update** on the dashboard, **Cloud Services** page, or **Instances** page.</span></span> <span data-ttu-id="f8c83-109">您可以更新單一角色或所有角色。</span><span class="sxs-lookup"><span data-stu-id="f8c83-109">You can update a single role or all roles.</span></span> <span data-ttu-id="f8c83-110">您將需要上傳新的服務套件和服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="f8c83-110">You'll need to upload a new service package and service configuration file.</span></span>

1. <span data-ttu-id="f8c83-111">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下儀表板上、[雲端服務] 頁面上或 [執行個體] 頁面上的 [更新]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-111">In the [Azure classic portal](https://manage.windowsazure.com/), on the dashboard, **Cloud Services** page, or **Instances** page, click **Update**.</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. <span data-ttu-id="f8c83-113">在 [部署標籤] 中，輸入部署的識別名稱 (例如，mycloudservice4)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-113">In **Deployment label**, enter a name to identify the deployment (for example, mycloudservice4).</span></span> <span data-ttu-id="f8c83-114">您將在儀表板的 [快速入門]  下發現此部署標籤。</span><span class="sxs-lookup"><span data-stu-id="f8c83-114">You'll find the deployment label under **quick start** on the dashboard.</span></span>
3. <span data-ttu-id="f8c83-115">在 [封裝] 中，使用 [瀏覽] 上傳服務套件檔 (.cspkg)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-115">In **Package**, use **Browse** to upload the service package file (.cspkg).</span></span>
4. <span data-ttu-id="f8c83-116">在 [組態] 中，使用 [瀏覽] 上傳服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-116">In **Configuration**, use **Browse** to upload the service configuration file (.cscfg).</span></span>
5. <span data-ttu-id="f8c83-117">若要升級雲端服務中的所有角色，請在 [角色] 中選取 [全部]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-117">In **Role**, select **All** if you want to upgrade all roles in the cloud service.</span></span> <span data-ttu-id="f8c83-118">若要執行單一角色更新，請選取您要更新的角色。</span><span class="sxs-lookup"><span data-stu-id="f8c83-118">To perform a single role update, select the role you want to update.</span></span> <span data-ttu-id="f8c83-119">即使您選取特定角色來更新，服務組態檔中的更新還是會套用至所有角色。</span><span class="sxs-lookup"><span data-stu-id="f8c83-119">Even if you select a specific role to update, the updates in the service configuration file are applied to all roles.</span></span>
6. <span data-ttu-id="f8c83-120">如果更新會造成角色數目或任何角色的大小變更，請選取 [Allow update if role sizes or number of roles changes]  核取方塊，讓更新能夠繼續。</span><span class="sxs-lookup"><span data-stu-id="f8c83-120">If the update changes the number of roles or the size of any role, select the **Allow update if role sizes or number of roles changes** check box to enable the update to proceed.</span></span>

    <span data-ttu-id="f8c83-121">請注意，如果您變更角色的大小 (亦即，角色執行個體所裝載於之虛擬機器的大小) 或角色數目，則必須重新製作每個角色執行個體 (虛擬機器) 的映像，因而遺失本機資料。</span><span class="sxs-lookup"><span data-stu-id="f8c83-121">Be aware that if you change the size of a role (that is, the size of a virtual machine that hosts a role instance) or the number of roles, each role instance (virtual machine) must be re-imaged, and any local data will be lost.</span></span>

7. <span data-ttu-id="f8c83-122">如果有任何服務角色只有一個角色執行個體，請選取 [Update even if one or more role contain a single instance]  核取方塊，讓升級能夠繼續。</span><span class="sxs-lookup"><span data-stu-id="f8c83-122">If any service roles have only one role instance, select the **Update even if one or more role contain a single instance check box** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="f8c83-123">要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-123">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="f8c83-124">如此才能讓一個虛擬機器在受到更新時，還有另一個虛擬機器可以處理用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="f8c83-124">That enables one virtual machine to process client requests while the other is being updated.</span></span>

8. <span data-ttu-id="f8c83-125">按一下 [確定]  \(核取記號) 開始更新服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-125">Click **OK** (checkmark) to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="f8c83-126">作法：交換部署以使預備部署升格為生產部署</span><span class="sxs-lookup"><span data-stu-id="f8c83-126">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="f8c83-127">使用 [交換]  將雲端服務的預備部署升格為生產部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-127">Use **Swap** to promote a staging deployment of a cloud service to production.</span></span> <span data-ttu-id="f8c83-128">當您決定部署新版的雲端服務時，可以在雲端服務預備環境中預備並測試這個新版本，同時讓您的客戶繼續在生產部署中使用目前版本。</span><span class="sxs-lookup"><span data-stu-id="f8c83-128">When you decide to deploy a new release of a cloud service, you can stage and test your new release in your cloud service staging environment while your customers are using the current release in production.</span></span> <span data-ttu-id="f8c83-129">當您準備好要將新版部署升格為生產部署時，可以使用 [交換]  將這兩個部署的 URL 位址互換。</span><span class="sxs-lookup"><span data-stu-id="f8c83-129">When you're ready to promote the new release to production, you can use **Swap** to switch the URLs by which the two deployments are addressed.</span></span>

<span data-ttu-id="f8c83-130">您可以在 [雲端服務]  頁面或儀表板交換部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-130">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="f8c83-131">在 [Azure 傳統入口網站](https://manage.windowsazure.com/)中，按一下 [ **雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-131">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="f8c83-132">在雲端服務清單中，按一下雲端服務加以選取。</span><span class="sxs-lookup"><span data-stu-id="f8c83-132">In the list of cloud services, click the cloud service to select it.</span></span>
3. <span data-ttu-id="f8c83-133">按一下 [交換] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-133">Click **Swap**.</span></span>

    <span data-ttu-id="f8c83-134">隨即開啟下列確認提示。</span><span class="sxs-lookup"><span data-stu-id="f8c83-134">The following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. <span data-ttu-id="f8c83-136">確認部署資訊無誤之後，按一下 [是]  交換部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-136">After you verify the deployment information, click **Yes** to swap the deployments.</span></span>

    <span data-ttu-id="f8c83-137">交換部署的速度很快，因為唯一變更的是部署的虛擬 IP 位址 (VIP)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-137">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="f8c83-138">當您確定新的生產部署如預期執行時，即可刪除預備環境中的部署，以節省運算成本。</span><span class="sxs-lookup"><span data-stu-id="f8c83-138">To save compute costs, you can delete the deployment in the staging environment when you're sure the new production deployment is performing as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="f8c83-139">交換部署的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="f8c83-139">Common questions about swapping deployments</span></span>

<span data-ttu-id="f8c83-140">**交換部署有哪些必要條件？**</span><span class="sxs-lookup"><span data-stu-id="f8c83-140">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="f8c83-141">成功的部署交換有兩個主要必要條件：</span><span class="sxs-lookup"><span data-stu-id="f8c83-141">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="f8c83-142">如果您想要讓生產環境位置使用靜態 IP 位址，就必須為您的預備位置也保留一個靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8c83-142">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="f8c83-143">否則，交換將會失敗。</span><span class="sxs-lookup"><span data-stu-id="f8c83-143">Otherwise, the swap will fail.</span></span>

- <span data-ttu-id="f8c83-144">您的所有角色執行個體必須都處於執行中狀態，您才能執行交換。</span><span class="sxs-lookup"><span data-stu-id="f8c83-144">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="f8c83-145">您可以在 Azure 傳統入口網站中，或藉由使用 [Windows PowerShell 中的 Get-AzureRole 命令](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0)，來檢查執行個體的狀態。</span><span class="sxs-lookup"><span data-stu-id="f8c83-145">You can check the status of your instances in the Azure classic portal or by using [the Get-AzureRole command in Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).</span></span>

<span data-ttu-id="f8c83-146">請注意，客體 OS 更新和服務修復作業也可能導致部署交換失敗。</span><span class="sxs-lookup"><span data-stu-id="f8c83-146">Note that guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="f8c83-147">如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-147">See [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md) for more details.</span></span>

<span data-ttu-id="f8c83-148">**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**</span><span class="sxs-lookup"><span data-stu-id="f8c83-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="f8c83-149">如最後一節所述，部署交換通常非常快，因為它只是 Azure 負載平衡器中的組態變更。</span><span class="sxs-lookup"><span data-stu-id="f8c83-149">As described in the last section, a deployment swap is typically very fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="f8c83-150">不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="f8c83-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="f8c83-151">若要限縮對您客戶造成的影響，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="f8c83-152">作法：將資源連結到雲端服務</span><span class="sxs-lookup"><span data-stu-id="f8c83-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="f8c83-153">若要顯示您的雲端服務對其他資源的依存性，您可以將 Azure SQL Database 執行個體或儲存體帳戶連結到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-153">To show your cloud service's dependencies on other resources, you can link an Azure SQL Database instance or a storage account to the cloud service.</span></span> <span data-ttu-id="f8c83-154">您可以在 [ **連結的資源** ] 頁面上連結和取消連結資源，然後在雲端服務儀表板上監視其使用率。</span><span class="sxs-lookup"><span data-stu-id="f8c83-154">You can link and unlink resources on the **Linked Resources** page, and then monitor their usage on the cloud service dashboard.</span></span> <span data-ttu-id="f8c83-155">如果連結的儲存體帳戶已開啟監視功能，則您可以在雲端服務儀表板上監視 [要求總數]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-155">If a linked storage account has monitoring turned on, you can monitor Total Requests on the cloud service dashboard.</span></span>

<span data-ttu-id="f8c83-156">您可以使用 [連結]  將新的或現有 SQL Database 執行個體或儲存體帳戶連結到您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-156">Use **Link** to link a new or existing SQL Database instance or storage account to your cloud service.</span></span> <span data-ttu-id="f8c83-157">然後，您便可以在 [調整]  頁面上調整資料庫以及使用該資料庫的雲端服務角色。</span><span class="sxs-lookup"><span data-stu-id="f8c83-157">You can then scale the database along with the cloud service role that is using it on the **Scale** page.</span></span> <span data-ttu-id="f8c83-158">(儲存體帳戶會在使用量增加時自動調整。)如需詳細資訊，請參閱[如何調整雲端服務和連結的資源](cloud-services-how-to-scale.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-158">(A storage account scales automatically as usage increases.) For more information, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

<span data-ttu-id="f8c83-159">您也可以在 Azure 傳統入口網站的 **資料庫** 節點中監視、管理和調整資料庫。</span><span class="sxs-lookup"><span data-stu-id="f8c83-159">You also can monitor, manage, and scale the database in the **Databases** node of the Azure classic portal.</span></span>

<span data-ttu-id="f8c83-160">在這種情況下，將資源「連結」並不會將您的應用程式連接到資源。</span><span class="sxs-lookup"><span data-stu-id="f8c83-160">"Linking" a resource in this sense doesn't connect your app to the resource.</span></span> <span data-ttu-id="f8c83-161">如果您使用 [連結] 建立新的資料庫，則需要將連接字串新增至應用程式程式碼，然後升級雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-161">If you create a new database using **Link**, you'll need to add the connection strings to your application code and then upgrade the cloud service.</span></span> <span data-ttu-id="f8c83-162">如果您的應用程式使用連結的儲存體帳戶中的資源，您也需要新增連接字串。</span><span class="sxs-lookup"><span data-stu-id="f8c83-162">You'll also need to add connection strings if your app uses resources in a linked storage account.</span></span>

<span data-ttu-id="f8c83-163">下列程序說明如何將新的 SQL Database 執行個體 (部署於新的 SQL Database 伺服器上) 連結到雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-163">The following procedure describes how to link a new SQL Database instance, deployed on a new SQL Database server, to a cloud service.</span></span>

### <a name="to-link-a-sql-database-instance-to-a-cloud-service"></a><span data-ttu-id="f8c83-164">將 SQL Database 執行個體連結到雲端服務</span><span class="sxs-lookup"><span data-stu-id="f8c83-164">To link a SQL Database instance to a cloud service</span></span>
1. <span data-ttu-id="f8c83-165">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [ **雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-165">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="f8c83-166">然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="f8c83-166">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="f8c83-167">按一下 [Linked Resources] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-167">Click **Linked Resources**.</span></span>

    <span data-ttu-id="f8c83-168">[Linked Resources]  頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f8c83-168">The **Linked Resources** page opens.</span></span>

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. <span data-ttu-id="f8c83-170">按一下 [連結資源] 或 [連結]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-170">Click either **Link a Resource** or **Link**.</span></span>

    <span data-ttu-id="f8c83-171">[Link Resource]  精靈隨即啟動。</span><span class="sxs-lookup"><span data-stu-id="f8c83-171">The **Link Resource** wizard starts.</span></span>

    ![Link Page1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. <span data-ttu-id="f8c83-173">按一下 [建立新的資源] 或 [連結現有的資源]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-173">Click **Create a new resource** or **Link an existing resource**.</span></span>
5. <span data-ttu-id="f8c83-174">選擇要連結的資源類型。</span><span class="sxs-lookup"><span data-stu-id="f8c83-174">Choose the type of resource to link.</span></span> <span data-ttu-id="f8c83-175">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [ **SQL Database**]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-175">In the [Azure classic portal](http://manage.windowsazure.com/), click **SQL Database**.</span></span> <span data-ttu-id="f8c83-176">(只有 Azure 傳統入口網站支援將儲存體帳戶連結到雲端服務。)</span><span class="sxs-lookup"><span data-stu-id="f8c83-176">(Only the Azure classic portal supports linking a storage account to a cloud service.)</span></span>
6. <span data-ttu-id="f8c83-177">若要完成資料庫組態，請依照 Azure 傳統入口網站中 [ **SQL Database** ] 區域的說明中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="f8c83-177">To complete the database configuration, follow instructions in help for the **SQL Databases** area of the Azure classic portal.</span></span>

    <span data-ttu-id="f8c83-178">您可以在訊息區域中追蹤連結作業的進度。</span><span class="sxs-lookup"><span data-stu-id="f8c83-178">You can follow the progress of the linking operation in the message area.</span></span>

    <span data-ttu-id="f8c83-179">連結完成時，您可以在雲端服務儀表板上監視已連結資源的狀態。</span><span class="sxs-lookup"><span data-stu-id="f8c83-179">When linking is complete, you can monitor the status of the linked resource on the cloud service dashboard.</span></span> <span data-ttu-id="f8c83-180">如需關於調整已連結之 SQL Database 的詳細資訊，請參閱 [如何調整雲端服務和連結的資源](cloud-services-how-to-scale.md)(英文)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-180">For information about scaling a linked SQL Database, see [How to Scale a Cloud Service and Linked Resources](cloud-services-how-to-scale.md).</span></span>

### <a name="to-unlink-a-linked-resource"></a><span data-ttu-id="f8c83-181">取消連結已連結的資源</span><span class="sxs-lookup"><span data-stu-id="f8c83-181">To unlink a linked resource</span></span>
1. <span data-ttu-id="f8c83-182">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [ **雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-182">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span> <span data-ttu-id="f8c83-183">然後按一下雲端服務的名稱以開啟儀表板。</span><span class="sxs-lookup"><span data-stu-id="f8c83-183">Then click the name of the cloud service to open the dashboard.</span></span>
2. <span data-ttu-id="f8c83-184">按一下 [Linked Resources] ，然後選取資源。</span><span class="sxs-lookup"><span data-stu-id="f8c83-184">Click **Linked Resources**, and then select the resource.</span></span>
3. <span data-ttu-id="f8c83-185">按一下 [取消連結] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-185">Click **Unlink**.</span></span> <span data-ttu-id="f8c83-186">然後在確認提示處按一下 [是]  。</span><span class="sxs-lookup"><span data-stu-id="f8c83-186">Then click **Yes** at the confirmation prompt.</span></span>

    <span data-ttu-id="f8c83-187">取消連結 SQL Database 並不會影響資料庫或是應用程式與資料庫的連線。</span><span class="sxs-lookup"><span data-stu-id="f8c83-187">Unlinking a SQL Database has no effect on the database or the application's connections to the database.</span></span> <span data-ttu-id="f8c83-188">您還是可以在 Azure 傳統入口網站的 [ **SQL Database** ] 區域中管理資料庫。</span><span class="sxs-lookup"><span data-stu-id="f8c83-188">You can still manage the database in the **SQL Databases** area of the Azure classic portal.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="f8c83-189">作法：刪除部署和雲端服務</span><span class="sxs-lookup"><span data-stu-id="f8c83-189">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="f8c83-190">刪除雲端服務之前，您必須先刪除每個現有的部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-190">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="f8c83-191">為了節省運算成本，您可以在確認生產部署如預期運作之後刪除預備部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-191">To save compute costs, you can delete your staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="f8c83-192">只要角色執行個體存在，您就需要為其支付運算成本，即使雲端服務未執行也一樣。</span><span class="sxs-lookup"><span data-stu-id="f8c83-192">You are billed compute costs for role instances even if a cloud service is not running.</span></span>

<span data-ttu-id="f8c83-193">使用下列程序，刪除部署或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f8c83-193">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="f8c83-194">在 [Azure 傳統入口網站](http://manage.windowsazure.com/)中，按一下 [ **雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-194">In the [Azure classic portal](http://manage.windowsazure.com/), click **Cloud Services**.</span></span>
2. <span data-ttu-id="f8c83-195">選取雲端服務，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-195">Select the cloud service, and then click **Delete**.</span></span> <span data-ttu-id="f8c83-196">(若要選取雲端服務而不開啟儀表板，請在雲端服務項目中按一下名稱以外的任何位置。)</span><span class="sxs-lookup"><span data-stu-id="f8c83-196">(To select a cloud service without opening the dashboard, click anywhere except the name in the cloud service entry.)</span></span>

    <span data-ttu-id="f8c83-197">如果您有預備或生產的部署，則會在視窗底部看到與下面類似的選項功能表。</span><span class="sxs-lookup"><span data-stu-id="f8c83-197">If you have a deployment in staging or production, you will see a menu of choices similar to the following one at the bottom of the window.</span></span> <span data-ttu-id="f8c83-198">刪除雲端服務之前，您必須先刪除任何現有的部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-198">Before you can delete the cloud service, you must delete any existing deployments.</span></span>

    ![Delete Menu](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. <span data-ttu-id="f8c83-200">若要刪除部署，請按一下 [刪除生產部署] 或 [刪除預備部署]。</span><span class="sxs-lookup"><span data-stu-id="f8c83-200">To delete a deployment, click **Delete production deployment** or **Delete staging deployment**.</span></span> <span data-ttu-id="f8c83-201">然後，在確認提示處按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-201">Then, at the confirmation prompt, click **Yes**.</span></span>
4. <span data-ttu-id="f8c83-202">如果您計劃刪除雲端服務，請重複步驟 3 (如果需要) 來刪除另一個部署。</span><span class="sxs-lookup"><span data-stu-id="f8c83-202">If you plan to delete the cloud service, repeat step 3, if needed, to delete your other deployment.</span></span>
5. <span data-ttu-id="f8c83-203">若要刪除雲端服務，請按一下 [刪除雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-203">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="f8c83-204">然後，在確認提示處按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="f8c83-204">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c83-205">如果對雲端服務設定了詳細資訊監視，則當您刪除該雲端服務時，Azure 並不會從您的儲存體帳戶中刪除監視資料。</span><span class="sxs-lookup"><span data-stu-id="f8c83-205">If verbose monitoring is configured for your cloud service, Azure does not delete the monitoring data from your storage account when you delete the cloud service.</span></span> <span data-ttu-id="f8c83-206">您將需要手動刪除資料。</span><span class="sxs-lookup"><span data-stu-id="f8c83-206">You will need to delete the data manually.</span></span> <span data-ttu-id="f8c83-207">如需有關何處可找到這些計量資料表的詳細資訊，請參閱 [如何監視雲端服務](cloud-services-how-to-monitor.md)中的＜作法：從 Azure 傳統入口網站外部存取詳細資訊監視資料＞。</span><span class="sxs-lookup"><span data-stu-id="f8c83-207">For information about where to find the metrics tables, see "How to: Access verbose monitoring data outside the Azure classic portal" in [How to Monitor Cloud Services](cloud-services-how-to-monitor.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f8c83-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8c83-208">Next steps</span></span>
* <span data-ttu-id="f8c83-209">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-209">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="f8c83-210">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-210">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="f8c83-211">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-211">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="f8c83-212">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="f8c83-212">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>
