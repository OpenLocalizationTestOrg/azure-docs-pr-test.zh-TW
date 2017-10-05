---
title: "常見的雲端服務管理工作 | Microsoft Docs"
description: "了解如何在 Azure 入口網站中管理雲端服務。 這些範例使用 Azure 入口網站。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 4650cebe18153e3b10bbec685a66a590348c99e9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-manage-cloud-services"></a><span data-ttu-id="014b9-104">如何管理雲端服務</span><span class="sxs-lookup"><span data-stu-id="014b9-104">How to Manage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="014b9-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="014b9-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="014b9-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="014b9-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="014b9-107">在 Azure 入口網站的 [雲端服務 (傳統)] 區域中，您可以更新服務角色或部署、將預備部署提升至生產、將資源連結至您的雲端服務以便於查看資源相依性，並將資源一起調整，以及刪除雲端服務或部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-107">In the **Cloud Services (classic)** area of the Azure portal, you can update a service role or a deployment, promote a staged deployment to production, link resources to your cloud service so that you can see the resource dependencies and scale the resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="014b9-108">如需如何調整雲端服務的詳細資訊，可在 [這裡](cloud-services-how-to-scale-portal.md)取得。</span><span class="sxs-lookup"><span data-stu-id="014b9-108">More information about how to scale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="014b9-109">作法：更新雲端服務角色或部署</span><span class="sxs-lookup"><span data-stu-id="014b9-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="014b9-110">如果您需要更新雲端服務的應用程式程式碼，請使用雲端服務刀鋒視窗上的 [ **更新** ]。</span><span class="sxs-lookup"><span data-stu-id="014b9-110">If you need to update the application code for your cloud service, use **Update** on the cloud service blade.</span></span> <span data-ttu-id="014b9-111">您可以更新單一角色或所有角色。</span><span class="sxs-lookup"><span data-stu-id="014b9-111">You can update a single role or all roles.</span></span> <span data-ttu-id="014b9-112">您可以上傳新的服務封裝或服務組態檔來更新。</span><span class="sxs-lookup"><span data-stu-id="014b9-112">To update, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="014b9-113">在 [Azure 入口網站][Azure portal]中，選取您想要更新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-113">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="014b9-114">這會開啟雲端服務執行個體刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="014b9-114">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="014b9-115">在刀鋒視窗中，按一下 [更新]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="014b9-115">In the blade, click the **Update** button.</span></span>

    ![更新按鈕](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="014b9-117">使用新的服務封裝檔 (.cspkg) 和服務組態檔 (.cscfg) 更新部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-117">Update the deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="014b9-119">**選擇性** 更新部署標籤和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="014b9-119">**Optionally** update the deployment label and the storage account.</span></span>
5. <span data-ttu-id="014b9-120">如果有任何角色只有一個角色執行個體，請選取 [即使一個或多個角色包含單一執行個體，也要部署]  ，讓升級能夠繼續。</span><span class="sxs-lookup"><span data-stu-id="014b9-120">If any roles have only one role instance, select the **Deploy even if one or more roles contain a single instance** to enable the upgrade to proceed.</span></span>

    <span data-ttu-id="014b9-121">要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="014b9-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="014b9-122">有兩個角色執行個體，其中一部虛擬機器會在另一部虛擬機器更新時處理用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="014b9-122">With two role instances, one virtual machine processes client requests while the other is updated.</span></span>

6. <span data-ttu-id="014b9-123">在封裝上傳完成之後，選取 [開始部署]  以套用更新。</span><span class="sxs-lookup"><span data-stu-id="014b9-123">Check **Start deployment** to have the update applied after the upload of the package has finished.</span></span>
7. <span data-ttu-id="014b9-124">按一下 [確定]  開始更新服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-124">Click **OK** to begin updating the service.</span></span>

## <a name="how-to-swap-deployments-to-promote-a-staged-deployment-to-production"></a><span data-ttu-id="014b9-125">作法：交換部署以使預備部署升格為生產部署</span><span class="sxs-lookup"><span data-stu-id="014b9-125">How to: Swap deployments to promote a staged deployment to production</span></span>
<span data-ttu-id="014b9-126">當您決定部署新版的雲端服務時，可以在您的雲端服務預備環境中，預備並測試新版本。</span><span class="sxs-lookup"><span data-stu-id="014b9-126">When you decide to deploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="014b9-127">使用 [交換]  將這兩個部署的 URL 位址互換，並將新版本升級為生產部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-127">Use **Swap** to switch the URLs by which the two deployments are addressed and promote a new release to production.</span></span>

<span data-ttu-id="014b9-128">您可以在 [雲端服務]  頁面或儀表板交換部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-128">You can swap deployments from the **Cloud Services** page or the dashboard.</span></span>

1. <span data-ttu-id="014b9-129">在 [Azure 入口網站][Azure portal]中，選取您想要更新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-129">In the [Azure portal][Azure portal], select the cloud service you want to update.</span></span> <span data-ttu-id="014b9-130">這會開啟雲端服務執行個體刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="014b9-130">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="014b9-131">在刀鋒視窗中，按一下 [ **交換** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="014b9-131">In the blade, click the **Swap** button.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="014b9-133">隨即開啟下列確認提示。</span><span class="sxs-lookup"><span data-stu-id="014b9-133">The following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="014b9-135">確認部署資訊之後，按一下 [ **是** ] 交換部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-135">After you verify the deployment information, click **OK** to swap the deployments.</span></span>

    <span data-ttu-id="014b9-136">交換部署的速度很快，因為唯一變更的是部署的虛擬 IP 位址 (VIP)。</span><span class="sxs-lookup"><span data-stu-id="014b9-136">The deployment swap happens quickly because the only thing that changes is the virtual IP addresses (VIPs) for the deployments.</span></span>

    <span data-ttu-id="014b9-137">為了節省運算成本，您可以在確認生產部署如預期運作之後刪除預備部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-137">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="014b9-138">交換部署的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="014b9-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="014b9-139">**交換部署有哪些必要條件？**</span><span class="sxs-lookup"><span data-stu-id="014b9-139">**What are the prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="014b9-140">成功的部署交換有兩個主要必要條件：</span><span class="sxs-lookup"><span data-stu-id="014b9-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="014b9-141">如果您想要讓生產環境位置使用靜態 IP 位址，就必須為您的預備位置也保留一個靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="014b9-141">If you would like to use a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="014b9-142">否則，交換會失敗。</span><span class="sxs-lookup"><span data-stu-id="014b9-142">Otherwise, the swap fails.</span></span>

- <span data-ttu-id="014b9-143">您的所有角色執行個體必須都處於執行中狀態，您才能執行交換。</span><span class="sxs-lookup"><span data-stu-id="014b9-143">All instances of your roles must be running before you can perform the swap.</span></span> <span data-ttu-id="014b9-144">您可以在 Azure 入口網站的 [概觀] 刀鋒視窗中檢查您的執行個體狀態。</span><span class="sxs-lookup"><span data-stu-id="014b9-144">You can check the status of your instances in the overview blade of the Azure portal.</span></span> <span data-ttu-id="014b9-145">或者，也可以使用 Windows PowerShell 的 [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) 命令。</span><span class="sxs-lookup"><span data-stu-id="014b9-145">Alternatively, you can use the [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="014b9-146">請注意，客體 OS 更新和服務修復作業也可能導致部署交換失敗。</span><span class="sxs-lookup"><span data-stu-id="014b9-146">Note that Guest OS updates and service healing operations can also cause deployment swaps to fail.</span></span> <span data-ttu-id="014b9-147">如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="014b9-148">**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**</span><span class="sxs-lookup"><span data-stu-id="014b9-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="014b9-149">如最後一節中所述，部署交換通常很快，因為它只是 Azure 負載平衡器中的設定變更。</span><span class="sxs-lookup"><span data-stu-id="014b9-149">As described in the last section, a deployment swap is typically fast since it is just a configuration change in the Azure load balancer.</span></span> <span data-ttu-id="014b9-150">不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="014b9-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="014b9-151">若要限縮對您客戶造成的影響，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-151">To limit impact to your customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-to-a-cloud-service"></a><span data-ttu-id="014b9-152">作法：將資源連結到雲端服務</span><span class="sxs-lookup"><span data-stu-id="014b9-152">How to: Link a resource to a cloud service</span></span>
<span data-ttu-id="014b9-153">Azure 入口網站不會像目前 Azure 傳統入口網站一樣將資源連結一起。</span><span class="sxs-lookup"><span data-stu-id="014b9-153">The Azure portal does not link resources together like the current Azure classic portal does.</span></span> <span data-ttu-id="014b9-154">相反地，會在雲端服務所使用的相同資源群組中部署額外的資源。</span><span class="sxs-lookup"><span data-stu-id="014b9-154">Instead, deploy additional resources to the same resource group being used by the Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="014b9-155">作法：刪除部署和雲端服務</span><span class="sxs-lookup"><span data-stu-id="014b9-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="014b9-156">刪除雲端服務之前，您必須先刪除每個現有的部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="014b9-157">為了節省運算成本，您可以在確認生產部署如預期運作之後刪除預備部署。</span><span class="sxs-lookup"><span data-stu-id="014b9-157">To save compute costs, you can delete the staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="014b9-158">您需要為停止的已部署角色執行個體支付運算成本。</span><span class="sxs-lookup"><span data-stu-id="014b9-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="014b9-159">使用下列程序，刪除部署或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-159">Use the following procedure to delete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="014b9-160">在 [Azure 入口網站][Azure portal]中，選取您想要刪除的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-160">In the [Azure portal][Azure portal], select the cloud service you want to delete.</span></span> <span data-ttu-id="014b9-161">這會開啟雲端服務執行個體刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="014b9-161">This step opens the cloud service instance blade.</span></span>
2. <span data-ttu-id="014b9-162">在刀鋒視窗中，按一下 [ **刪除** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="014b9-162">In the blade, click the **Delete** button.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="014b9-164">您可以勾選 [雲端服務及其部署]，或是選擇 [生產部署] 或 [預備部署]，即可刪除整個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="014b9-164">You can delete the entire cloud service by checking **Cloud service and its deployments** or choose either the **Production deployment** or the **Staging deployment**.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="014b9-166">按一下底部的 [ **刪除** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="014b9-166">Click the **Delete** button at the bottom.</span></span>
5. <span data-ttu-id="014b9-167">若要刪除雲端服務，請按一下 [刪除雲端服務] 。</span><span class="sxs-lookup"><span data-stu-id="014b9-167">To delete the cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="014b9-168">然後，在確認提示處按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="014b9-168">Then, at the confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="014b9-169">當刪除雲端服務並且已設定詳細監視時，您必須從儲存體帳戶中手動刪除資料。</span><span class="sxs-lookup"><span data-stu-id="014b9-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete the data manually from your storage account.</span></span> <span data-ttu-id="014b9-170">如需何處可找到這些度量表的相關資訊，請參閱 [這篇](cloud-services-how-to-monitor.md) 文章。</span><span class="sxs-lookup"><span data-stu-id="014b9-170">For information about where to find the metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="014b9-171">如何： 尋找失敗部署的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="014b9-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="014b9-172">[概觀] 刀鋒視窗上方有狀態列。</span><span class="sxs-lookup"><span data-stu-id="014b9-172">The **Overview** blade has a status bar at the top.</span></span> <span data-ttu-id="014b9-173">當您按一下該列時，即會開啟新的刀鋒視窗，並顯示任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="014b9-173">When you click the bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="014b9-174">如果部署不包含任何錯誤，則 [資訊] 刀鋒視窗會是空白的。</span><span class="sxs-lookup"><span data-stu-id="014b9-174">If the deployment does not contain any errors, the information blade is blank.</span></span>

![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="014b9-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="014b9-176">Next steps</span></span>
* <span data-ttu-id="014b9-177">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="014b9-178">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-178">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="014b9-179">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="014b9-180">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="014b9-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
