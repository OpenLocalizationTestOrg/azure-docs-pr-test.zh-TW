---
title: "aaaCommon 雲端服務管理工作 |Microsoft 文件"
description: "了解如何 toomanage 雲端服務的 hello Azure 入口網站。 這些範例使用 hello Azure 入口網站。"
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
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a><span data-ttu-id="2d85f-104">如何 tooManage 雲端服務</span><span class="sxs-lookup"><span data-stu-id="2d85f-104">How tooManage Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2d85f-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2d85f-105">Azure portal</span></span>](cloud-services-how-to-manage-portal.md)
> * [<span data-ttu-id="2d85f-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="2d85f-106">Azure classic portal</span></span>](cloud-services-how-to-manage.md)
>
>

<span data-ttu-id="2d85f-107">在 hello**雲端服務 （傳統）**區域 hello Azure 入口網站中，您可以更新服務角色或部署、 升級預備的部署 tooproduction、 連結資源 tooyour 雲端服務，讓您能夠查看 hello 資源相依性和小數位數 hello 資源在一起，並刪除雲端服務或部署。</span><span class="sxs-lookup"><span data-stu-id="2d85f-107">In hello **Cloud Services (classic)** area of hello Azure portal, you can update a service role or a deployment, promote a staged deployment tooproduction, link resources tooyour cloud service so that you can see hello resource dependencies and scale hello resources together, and delete a cloud service or a deployment.</span></span>

<span data-ttu-id="2d85f-108">如何 tooscale 您雲端服務可供使用的詳細資訊[這裡](cloud-services-how-to-scale-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-108">More information about how tooscale your cloud service is available [here](cloud-services-how-to-scale-portal.md).</span></span>

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a><span data-ttu-id="2d85f-109">作法：更新雲端服務角色或部署</span><span class="sxs-lookup"><span data-stu-id="2d85f-109">How to: Update a cloud service role or deployment</span></span>
<span data-ttu-id="2d85f-110">如果您需要 tooupdate hello 應用程式程式碼為雲端服務時，使用**更新**hello 雲端服務 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-110">If you need tooupdate hello application code for your cloud service, use **Update** on hello cloud service blade.</span></span> <span data-ttu-id="2d85f-111">您可以更新單一角色或所有角色。</span><span class="sxs-lookup"><span data-stu-id="2d85f-111">You can update a single role or all roles.</span></span> <span data-ttu-id="2d85f-112">tooupdate，您可以上傳新的服務封裝或服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="2d85f-112">tooupdate, you can upload a new service package or service configuration file.</span></span>

1. <span data-ttu-id="2d85f-113">在 hello [Azure 入口網站][Azure portal]，選取您想 tooupdate hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2d85f-113">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="2d85f-114">此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-114">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d85f-115">在 hello 刀鋒視窗中，按一下 hello**更新** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2d85f-115">In hello blade, click hello **Update** button.</span></span>

    ![更新按鈕](./media/cloud-services-how-to-manage-portal/update-button.png)

3. <span data-ttu-id="2d85f-117">更新 hello 部署新的服務封裝檔 (.cspkg) 和服務組態檔 (.cscfg)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-117">Update hello deployment with a new service package file (.cspkg) and service configuration file (.cscfg).</span></span>

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. <span data-ttu-id="2d85f-119">**選擇性地**更新 hello 部署標籤和 hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2d85f-119">**Optionally** update hello deployment label and hello storage account.</span></span>
5. <span data-ttu-id="2d85f-120">如果任何角色只能有一個角色執行個體，請選取 hello**即使一個或多個角色包含單一執行個體部署**tooenable hello 升級 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="2d85f-120">If any roles have only one role instance, select hello **Deploy even if one or more roles contain a single instance** tooenable hello upgrade tooproceed.</span></span>

    <span data-ttu-id="2d85f-121">要讓 Azure 保證服務在雲端服務更新期間有 99.95% 的可用性，每個角色都至少必須有兩個角色執行個體 (虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-121">Azure can only guarantee 99.95 percent service availability during a cloud service update if each role has at least two role instances (virtual machines).</span></span> <span data-ttu-id="2d85f-122">有兩個角色執行個體，一部虛擬機器處理用戶端要求更新其他 hello 時。</span><span class="sxs-lookup"><span data-stu-id="2d85f-122">With two role instances, one virtual machine processes client requests while hello other is updated.</span></span>

6. <span data-ttu-id="2d85f-123">請檢查**啟動部署**toohave hello 更新 hello hello 封裝上的傳已完成之後套用。</span><span class="sxs-lookup"><span data-stu-id="2d85f-123">Check **Start deployment** toohave hello update applied after hello upload of hello package has finished.</span></span>
7. <span data-ttu-id="2d85f-124">按一下**確定**toobegin 更新 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="2d85f-124">Click **OK** toobegin updating hello service.</span></span>

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a><span data-ttu-id="2d85f-125">如何： 交換部署 toopromote 預備的部署 tooproduction</span><span class="sxs-lookup"><span data-stu-id="2d85f-125">How to: Swap deployments toopromote a staged deployment tooproduction</span></span>
<span data-ttu-id="2d85f-126">當您決定 toodeploy 是新發行的雲端服務，階段，並在雲端服務執行環境中測試新版本。</span><span class="sxs-lookup"><span data-stu-id="2d85f-126">When you decide toodeploy a new release of a cloud service, stage and test your new release in your cloud service staging environment.</span></span> <span data-ttu-id="2d85f-127">使用**交換**哪些 hello 由兩個部署會定址，並且升級新的版本 tooproduction tooswitch hello Url。</span><span class="sxs-lookup"><span data-stu-id="2d85f-127">Use **Swap** tooswitch hello URLs by which hello two deployments are addressed and promote a new release tooproduction.</span></span>

<span data-ttu-id="2d85f-128">您可以交換部署從 hello**雲端服務**頁面或 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="2d85f-128">You can swap deployments from hello **Cloud Services** page or hello dashboard.</span></span>

1. <span data-ttu-id="2d85f-129">在 hello [Azure 入口網站][Azure portal]，選取您想 tooupdate hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2d85f-129">In hello [Azure portal][Azure portal], select hello cloud service you want tooupdate.</span></span> <span data-ttu-id="2d85f-130">此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-130">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d85f-131">在 hello 刀鋒視窗中，按一下 hello**交換** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2d85f-131">In hello blade, click hello **Swap** button.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. <span data-ttu-id="2d85f-133">hello 下列確認提示隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="2d85f-133">hello following confirmation prompt opens.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. <span data-ttu-id="2d85f-135">確認 hello 部署資訊後，按一下**確定**tooswap hello 部署。</span><span class="sxs-lookup"><span data-stu-id="2d85f-135">After you verify hello deployment information, click **OK** tooswap hello deployments.</span></span>

    <span data-ttu-id="2d85f-136">hello 部署交換很快就會因為 hello 唯一變更是 hello 虛擬 IP 位址 (Vip) hello 部署。</span><span class="sxs-lookup"><span data-stu-id="2d85f-136">hello deployment swap happens quickly because hello only thing that changes is hello virtual IP addresses (VIPs) for hello deployments.</span></span>

    <span data-ttu-id="2d85f-137">toosave 運算成本，您可以刪除 hello 預備環境部署之後您確認生產部署如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="2d85f-137">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span>

### <a name="common-questions-about-swapping-deployments"></a><span data-ttu-id="2d85f-138">交換部署的相關常見問題</span><span class="sxs-lookup"><span data-stu-id="2d85f-138">Common questions about swapping deployments</span></span>

<span data-ttu-id="2d85f-139">**交換部署的 hello 必要條件為何？**</span><span class="sxs-lookup"><span data-stu-id="2d85f-139">**What are hello prerequisites for swapping deployments?**</span></span>

<span data-ttu-id="2d85f-140">成功的部署交換有兩個主要必要條件：</span><span class="sxs-lookup"><span data-stu-id="2d85f-140">There are two key prerequisites for a successful deployment swap:</span></span>

- <span data-ttu-id="2d85f-141">如果您想要 toouse 靜態 IP 位址的生產位置，您必須保留以及您預備位置的其中一個。</span><span class="sxs-lookup"><span data-stu-id="2d85f-141">If you would like toouse a static IP address for your production slot, you must reserve one for your staging slot as well.</span></span> <span data-ttu-id="2d85f-142">否則 hello 交換就會失敗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-142">Otherwise, hello swap fails.</span></span>

- <span data-ttu-id="2d85f-143">必須先執行所有的執行個體的角色，您可以執行 hello 交換。</span><span class="sxs-lookup"><span data-stu-id="2d85f-143">All instances of your roles must be running before you can perform hello swap.</span></span> <span data-ttu-id="2d85f-144">您可以檢查 hello hello 概觀刀鋒視窗中的 hello Azure 入口網站執行個體的狀態。</span><span class="sxs-lookup"><span data-stu-id="2d85f-144">You can check hello status of your instances in hello overview blade of hello Azure portal.</span></span> <span data-ttu-id="2d85f-145">或者，您可以使用 hello [Get-azurerole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) Windows PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="2d85f-145">Alternatively, you can use hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) command in Windows PowerShell.</span></span>

<span data-ttu-id="2d85f-146">請注意，客體 OS 更新服務修復作業也可能會導致部署交換 toofail。</span><span class="sxs-lookup"><span data-stu-id="2d85f-146">Note that Guest OS updates and service healing operations can also cause deployment swaps toofail.</span></span> <span data-ttu-id="2d85f-147">如需詳細資訊，請參閱[對雲端服務部署問題進行疑難排解](cloud-services-troubleshoot-deployment-problems.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-147">For more information, see [Troubleshoot cloud service deployment problems](cloud-services-troubleshoot-deployment-problems.md).</span></span>

<span data-ttu-id="2d85f-148">**交換是否會導致我的應用程式停止運作？我應該如何處理該情況？**</span><span class="sxs-lookup"><span data-stu-id="2d85f-148">**Does a swap incur downtime for my application? How should I handle it?**</span></span>

<span data-ttu-id="2d85f-149">Hello 最後一節所述，因為它是只在 hello Azure 負載平衡器組態變更部署交換是通常速度快。</span><span class="sxs-lookup"><span data-stu-id="2d85f-149">As described in hello last section, a deployment swap is typically fast since it is just a configuration change in hello Azure load balancer.</span></span> <span data-ttu-id="2d85f-150">不過，在某些情況下，它會花費十秒以上的時間，而導致暫時性的連線失敗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-150">In some cases, however, it can take ten or more seconds and result in transient connection failures.</span></span> <span data-ttu-id="2d85f-151">toolimit 影響 tooyour 客戶，請考慮實作[用戶端重試邏輯](../best-practices-retry-general.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-151">toolimit impact tooyour customers, consider implementing [client retry logic](../best-practices-retry-general.md).</span></span>

## <a name="how-to-link-a-resource-tooa-cloud-service"></a><span data-ttu-id="2d85f-152">如何： 連結資源 tooa 雲端服務</span><span class="sxs-lookup"><span data-stu-id="2d85f-152">How to: Link a resource tooa cloud service</span></span>
<span data-ttu-id="2d85f-153">hello Azure 入口網站未連結資源 hello 目前 Azure 傳統入口網站類似在一起。</span><span class="sxs-lookup"><span data-stu-id="2d85f-153">hello Azure portal does not link resources together like hello current Azure classic portal does.</span></span> <span data-ttu-id="2d85f-154">相反地，部署額外的資源 toohello hello 雲端服務正在使用相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2d85f-154">Instead, deploy additional resources toohello same resource group being used by hello Cloud Service.</span></span>

## <a name="how-to-delete-deployments-and-a-cloud-service"></a><span data-ttu-id="2d85f-155">作法：刪除部署和雲端服務</span><span class="sxs-lookup"><span data-stu-id="2d85f-155">How to: Delete deployments and a cloud service</span></span>
<span data-ttu-id="2d85f-156">刪除雲端服務之前，您必須先刪除每個現有的部署。</span><span class="sxs-lookup"><span data-stu-id="2d85f-156">Before you can delete a cloud service, you must delete each existing deployment.</span></span>

<span data-ttu-id="2d85f-157">toosave 運算成本，您可以刪除 hello 預備環境部署之後您確認生產部署如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="2d85f-157">toosave compute costs, you can delete hello staging deployment after you verify that your production deployment is working as expected.</span></span> <span data-ttu-id="2d85f-158">您需要為停止的已部署角色執行個體支付運算成本。</span><span class="sxs-lookup"><span data-stu-id="2d85f-158">You are billed for compute costs for deployed role instances that are stopped.</span></span>

<span data-ttu-id="2d85f-159">部署或雲端服務，請使用下列程序 toodelete hello。</span><span class="sxs-lookup"><span data-stu-id="2d85f-159">Use hello following procedure toodelete a deployment or your cloud service.</span></span>

1. <span data-ttu-id="2d85f-160">在 hello [Azure 入口網站][Azure portal]，選取您想 toodelete hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2d85f-160">In hello [Azure portal][Azure portal], select hello cloud service you want toodelete.</span></span> <span data-ttu-id="2d85f-161">此步驟會開啟 hello 雲端服務執行個體 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-161">This step opens hello cloud service instance blade.</span></span>
2. <span data-ttu-id="2d85f-162">在 hello 刀鋒視窗中，按一下 hello**刪除** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="2d85f-162">In hello blade, click hello **Delete** button.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. <span data-ttu-id="2d85f-164">您可以刪除 hello 整個雲端服務，藉由檢查**雲端服務和其部署**或選擇任一個 hello**生產環境部署**或 hello**預備部署**。</span><span class="sxs-lookup"><span data-stu-id="2d85f-164">You can delete hello entire cloud service by checking **Cloud service and its deployments** or choose either hello **Production deployment** or hello **Staging deployment**.</span></span>

    ![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. <span data-ttu-id="2d85f-166">按一下 hello**刪除**hello 底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="2d85f-166">Click hello **Delete** button at hello bottom.</span></span>
5. <span data-ttu-id="2d85f-167">toodelete hello 雲端服務，請按一下**刪除雲端服務**。</span><span class="sxs-lookup"><span data-stu-id="2d85f-167">toodelete hello cloud service, click **Delete cloud service**.</span></span> <span data-ttu-id="2d85f-168">然後，在 hello 確認提示按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="2d85f-168">Then, at hello confirmation prompt, click **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="2d85f-169">當雲端服務遭到刪除，並設定監視的詳細資訊時，您必須從儲存體帳戶以手動方式刪除 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="2d85f-169">When a cloud service is deleted, and verbose monitoring is configured, you must delete hello data manually from your storage account.</span></span> <span data-ttu-id="2d85f-170">其中 toofind hello 度量資料表的相關資訊，請參閱[這](cloud-services-how-to-monitor.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="2d85f-170">For information about where toofind hello metrics tables, see [this](cloud-services-how-to-monitor.md) article.</span></span>


## <a name="how-to-find-more-information-about-failed-deployments"></a><span data-ttu-id="2d85f-171">如何： 尋找失敗部署的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="2d85f-171">How to: Find more information about failed deployments</span></span>
<span data-ttu-id="2d85f-172">hello**概觀**刀鋒視窗頂端 hello 有狀態列。</span><span class="sxs-lookup"><span data-stu-id="2d85f-172">hello **Overview** blade has a status bar at hello top.</span></span> <span data-ttu-id="2d85f-173">當您按一下 hello 列時，新刀鋒視窗中開啟，並顯示任何資訊時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="2d85f-173">When you click hello bar, a new blade opens and displays any error information.</span></span> <span data-ttu-id="2d85f-174">Hello 部署不包含任何錯誤，如果是空白的 hello 資訊刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2d85f-174">If hello deployment does not contain any errors, hello information blade is blank.</span></span>

![Cloud Services Swap](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="2d85f-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d85f-176">Next steps</span></span>
* <span data-ttu-id="2d85f-177">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-177">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="2d85f-178">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-178">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="2d85f-179">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-179">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="2d85f-180">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2d85f-180">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
