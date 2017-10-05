---
title: "針對 Azure App Service 中的 Web 應用程式設定預備環境 | Microsoft Docs"
description: "了解如何針對 Azure App Service 中的 Web 應用程式使用預備發行。"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="98601-103">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="98601-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="98601-104">當您將 Web 應用程式、Linux 上的 Web 應用程式、行動後端及 API 應用程式部署到 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 時，如果是在 [標準] 或 [進階] App Service 方案模式下執行，就可以部署到個別的部署位置，而不是預設的生產環境位置。</span><span class="sxs-lookup"><span data-stu-id="98601-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="98601-105">部署位置實際上是含有自己主機名稱的作用中應用程式。</span><span class="sxs-lookup"><span data-stu-id="98601-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="98601-106">兩個部署位置 (包括生產位置) 之間的應用程式內容與設定項目可以互相交換。</span><span class="sxs-lookup"><span data-stu-id="98601-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="98601-107">將應用程式部署至部署位置具有下列優點：</span><span class="sxs-lookup"><span data-stu-id="98601-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="98601-108">您可以先驗證預備部署位置中的應用程式變更，再將它與生產位置進行交換。</span><span class="sxs-lookup"><span data-stu-id="98601-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="98601-109">先將應用程式部署至某個位置，然後再將它交換到生產位置，可確保該位置的所有執行個體在交換到生產位置之前都已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="98601-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="98601-110">這麼做可以排除部署應用程式時的停機情況。</span><span class="sxs-lookup"><span data-stu-id="98601-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="98601-111">交換作業期間所有的流量都能順暢地重新導向，而且不會捨棄任何要求封包。</span><span class="sxs-lookup"><span data-stu-id="98601-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="98601-112">不需要預先交換驗證時，這整個工作流程可藉由設定 [自動交換](#Auto-Swap) 來自動化。</span><span class="sxs-lookup"><span data-stu-id="98601-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="98601-113">交換之後，先前具有預備應用程式的位置，現在已經有之前的生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="98601-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="98601-114">若交換到生產位置的變更不是您需要的變更，您可以立即執行相同的交換，以取回「上一個已知良好的網站」。</span><span class="sxs-lookup"><span data-stu-id="98601-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="98601-115">每個 App Service 方案模式所支援的部署位置個數都不一樣。</span><span class="sxs-lookup"><span data-stu-id="98601-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="98601-116">若要找出應用程式模式所支援的位置個數，請參閱 [App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="98601-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="98601-117">當您的應用程式擁有多個位置時，就無法變更該模式。</span><span class="sxs-lookup"><span data-stu-id="98601-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="98601-118">非生產的位置無法使用調整規模。</span><span class="sxs-lookup"><span data-stu-id="98601-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="98601-119">非生產位置不支援連結的資源管理。</span><span class="sxs-lookup"><span data-stu-id="98601-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="98601-120">只有在 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715) 中，您才能藉由暫時將非生產位置移到其他 App Service 方案模式，來避免這種對生產位置的潛在影響。</span><span class="sxs-lookup"><span data-stu-id="98601-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="98601-121">請注意，非生產位置必須先再次與生產位置共用相同模式，您才能交換這兩個位置。</span><span class="sxs-lookup"><span data-stu-id="98601-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="98601-122">新增部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-122">Add a deployment slot</span></span>
<span data-ttu-id="98601-123">應用程式必須在 [標準] 或 [高階] 模式中執行，您才能啟用多個部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="98601-124">在 [Azure 入口網站](https://portal.azure.com/)中，開啟應用程式的[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。</span><span class="sxs-lookup"><span data-stu-id="98601-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="98601-125">選擇 [部署位置] 選項，然後按一下 [新增位置]。</span><span class="sxs-lookup"><span data-stu-id="98601-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![新增部署位置][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="98601-127">如果應用程式尚未處於 [標準] 或 [高階] 模式，您將會收到訊息，指出支援啟用預備發佈的模式。</span><span class="sxs-lookup"><span data-stu-id="98601-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="98601-128">此時，您可以選取 [升級]，並瀏覽至應用程式的 [級別] 索引標籤後再繼續。</span><span class="sxs-lookup"><span data-stu-id="98601-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="98601-129">在 [新增位置] 刀鋒視窗中，指定位置名稱，然後選取是否要複製其他現有部署位置的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="98601-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="98601-130">按一下打勾記號繼續。</span><span class="sxs-lookup"><span data-stu-id="98601-130">Click the check mark to continue.</span></span>
   
    ![組態來源][ConfigurationSource1]
   
    <span data-ttu-id="98601-132">第一次新增位置時，您只會有兩個選項：從生產環境的預設位置複製設定，或者完全不複製。</span><span class="sxs-lookup"><span data-stu-id="98601-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="98601-133">建立數個位置後，就可以從生產位置以外的位置複製組態：</span><span class="sxs-lookup"><span data-stu-id="98601-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![組態來源][MultipleConfigurationSources]
4. <span data-ttu-id="98601-135">在您應用程式的資源刀鋒視窗中，按一下 [部署位置]，然後按一下某個部署位置來開啟該位置的資源刀鋒視窗，當中會含有一組計量和組態，就像任何其他應用程式一樣。</span><span class="sxs-lookup"><span data-stu-id="98601-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="98601-136">刀鋒視窗頂端顯示之位置的名稱，提醒您正在檢視部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Deployment Slot Title][StagingTitle]
5. <span data-ttu-id="98601-138">在位置的刀鋒視窗中按一下應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="98601-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="98601-139">請注意，部署位置有自己的主機名稱，同時也是作用中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="98601-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="98601-140">若要限制對部署位置的公用存取，請參閱 [App Service Web 應用程式 - 封鎖對非生產部署位置的 Web 存取](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)。</span><span class="sxs-lookup"><span data-stu-id="98601-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="98601-141">建立部署位置之後不會有任何內容。</span><span class="sxs-lookup"><span data-stu-id="98601-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="98601-142">您可以從不同的儲存機制分支，或從整個不同的儲存機制部署至位置。</span><span class="sxs-lookup"><span data-stu-id="98601-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="98601-143">您也可以變更位置的組態。</span><span class="sxs-lookup"><span data-stu-id="98601-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="98601-144">更新內容時，請使用與部署位置相關聯的發行設定檔或部署認證。</span><span class="sxs-lookup"><span data-stu-id="98601-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="98601-145">例如，您可以 [使用 Git 發行至此位置](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="98601-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="98601-146">部署位置組態</span><span class="sxs-lookup"><span data-stu-id="98601-146">Configuration for deployment slots</span></span>
<span data-ttu-id="98601-147">當您複製其他部署位置的組態時，可以編輯複製的組態。</span><span class="sxs-lookup"><span data-stu-id="98601-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="98601-148">此外，某些組態項目在交換時會遵循內容 (非位置特定)，而其他組態項目將會在交換之後保留於同一個位置中 (位置特定)。</span><span class="sxs-lookup"><span data-stu-id="98601-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="98601-149">以下清單顯示當您交換位置時會變更的組態。</span><span class="sxs-lookup"><span data-stu-id="98601-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="98601-150">**交換的設定**：</span><span class="sxs-lookup"><span data-stu-id="98601-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="98601-151">一般設定 - 例如 Framework 版本、32/64 位元、Web 通訊端</span><span class="sxs-lookup"><span data-stu-id="98601-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="98601-152">應用程式設定 (可以設定為停在某一個位置)</span><span class="sxs-lookup"><span data-stu-id="98601-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="98601-153">連接字串 (可以設定為停在某一個位置)</span><span class="sxs-lookup"><span data-stu-id="98601-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="98601-154">處理常式對應</span><span class="sxs-lookup"><span data-stu-id="98601-154">Handler mappings</span></span>
* <span data-ttu-id="98601-155">監視與診斷設定</span><span class="sxs-lookup"><span data-stu-id="98601-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="98601-156">WebJobs 內容</span><span class="sxs-lookup"><span data-stu-id="98601-156">WebJobs content</span></span>

<span data-ttu-id="98601-157">**無法交換的設定**：</span><span class="sxs-lookup"><span data-stu-id="98601-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="98601-158">發行端點</span><span class="sxs-lookup"><span data-stu-id="98601-158">Publishing endpoints</span></span>
* <span data-ttu-id="98601-159">自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="98601-159">Custom Domain Names</span></span>
* <span data-ttu-id="98601-160">SSL 憑證與繫結</span><span class="sxs-lookup"><span data-stu-id="98601-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="98601-161">擴充設定</span><span class="sxs-lookup"><span data-stu-id="98601-161">Scale settings</span></span>
* <span data-ttu-id="98601-162">WebJobs 排程器</span><span class="sxs-lookup"><span data-stu-id="98601-162">WebJobs schedulers</span></span>

<span data-ttu-id="98601-163">若要將應用程式設定或連接字串設定為停留在某一個位置 (未交換)，可存取特定位置的 [應用程式設定] 刀鋒視窗，然後針對應停留在該位置的設定項目選取 [位置設定] 方塊。</span><span class="sxs-lookup"><span data-stu-id="98601-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="98601-164">請注意，將組態項目標記為位置特定的，會在將該項目建立為無法跨所有與該應用程式相關聯的部署位置進行交換時產生影響。</span><span class="sxs-lookup"><span data-stu-id="98601-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![位置設定][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="98601-166">交換部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-166">Swap deployment slots</span></span> 
<span data-ttu-id="98601-167">您可以在您應用程式資源刀鋒視窗的**概觀**或**部署位置**檢視中交換部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98601-168">在您將應用程式從部署位置交換到生產位置之前，請確定所有非位置特定的設定已完全依照您想要在交換目標中擁有它的方式明確地加以設定。</span><span class="sxs-lookup"><span data-stu-id="98601-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="98601-169">若要交換部署位置，可按一下應用程式命令列或部署位置命令列中的 [交換] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="98601-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Swap Button][SwapButtonBar]

2. <span data-ttu-id="98601-171">請確定交換來源和交換目標都已正確設定。</span><span class="sxs-lookup"><span data-stu-id="98601-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="98601-172">交換目標通常是生產位置。</span><span class="sxs-lookup"><span data-stu-id="98601-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="98601-173">按一下 確定  來完成操作。</span><span class="sxs-lookup"><span data-stu-id="98601-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="98601-174">當操作完成時，部署位置就已交換完畢。</span><span class="sxs-lookup"><span data-stu-id="98601-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![完整的交換](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="98601-176">針對**使用預覽交換**交換類型，請參閱[使用預覽交換 (多階段交換)](#Multi-Phase)。</span><span class="sxs-lookup"><span data-stu-id="98601-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="98601-177">使用預覽交換 (多階段交換)</span><span class="sxs-lookup"><span data-stu-id="98601-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="98601-178">使用預覽交換或多階段交換，簡化組態項目的位置特定驗證，例如連接字串。</span><span class="sxs-lookup"><span data-stu-id="98601-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="98601-179">針對關鍵任務的工作負載，您想要驗證當套用生產位置的組態時應用程式的行為會如預期，且您必須在應用程式交換到生產環境*之前*執行這類驗證。</span><span class="sxs-lookup"><span data-stu-id="98601-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="98601-180">您需要的是使用預覽交換。</span><span class="sxs-lookup"><span data-stu-id="98601-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="98601-181">Linux 上的 Web 應用程式不支援使用預覽交換。</span><span class="sxs-lookup"><span data-stu-id="98601-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="98601-182">當您使用**使用預覽交換**選項時 (請參閱[交換部署位置](#Swap))，App Service 會進行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="98601-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="98601-183">目的地位置會保留不變，因此不會影響該位置上的現有工作負載 (例如生產)。</span><span class="sxs-lookup"><span data-stu-id="98601-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="98601-184">將目的地位置的組態項目套用至來源位置，包括位置特定的連接字串和應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="98601-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="98601-185">使用這些上述的組態項目重新啟動來源位置上的工作者處理序。</span><span class="sxs-lookup"><span data-stu-id="98601-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="98601-186">當您完成交換時︰將 pre-warmed-up 來源位置移到目的地位置。</span><span class="sxs-lookup"><span data-stu-id="98601-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="98601-187">目的地位置會如手動交換移到來源位置。</span><span class="sxs-lookup"><span data-stu-id="98601-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="98601-188">當您取消交換時︰將來源位置的組態項目重新套用至來源位置。</span><span class="sxs-lookup"><span data-stu-id="98601-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="98601-189">您可以完全預覽應用程式與目的地位置組態的行為模式。</span><span class="sxs-lookup"><span data-stu-id="98601-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="98601-190">當您完成驗證時，會在個別步驟中完成交換。</span><span class="sxs-lookup"><span data-stu-id="98601-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="98601-191">此步驟有額外好處，來源位置已做好使用所需的設定，且用戶端不會發生任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="98601-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="98601-192">Azure PowerShell Cmdlet 可供多階段交換的範例，包含在部署位置區段的 Azure PowerShell Cmdlet 內。</span><span class="sxs-lookup"><span data-stu-id="98601-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="98601-193">設定自動交換</span><span class="sxs-lookup"><span data-stu-id="98601-193">Configure Auto Swap</span></span>
<span data-ttu-id="98601-194">自動交換會簡化 DevOps 案例，在此案例中，您希望為該應用程式的客戶在不需冷啟動和不需關機的情況下連續部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="98601-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="98601-195">當部署位置已設為自動交換至生產位置時，每當您將程式碼更新推送至該位置時，App Service 就會在其已於該位置上做好準備之後，自動將該應用程式交換至生產位置。</span><span class="sxs-lookup"><span data-stu-id="98601-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98601-196">當您為某個位置啟用自動交換時，請確定位置設定會與適用於目標位置 (通常是生產位置) 的設定完全相同。</span><span class="sxs-lookup"><span data-stu-id="98601-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="98601-197">Linux 上的 Web 應用程式不支援自動交換。</span><span class="sxs-lookup"><span data-stu-id="98601-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="98601-198">為位置設定自動交換很容易。</span><span class="sxs-lookup"><span data-stu-id="98601-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="98601-199">請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="98601-199">Follow the steps below:</span></span>

1. <span data-ttu-id="98601-200">在**部署位置**中，選取非生產位置，然後在該位置的資源刀鋒視窗中選擇 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="98601-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="98601-201">針對 [自動交換] 選取 [開啟]、在 [自動交換位置] 中選取所需的目標位置，然後按一下命令列中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="98601-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="98601-202">確定此位置的組態設定完全適用於目標位置的組態設定。</span><span class="sxs-lookup"><span data-stu-id="98601-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="98601-203">當操作完成時，[通知] 索引標籤會有綠色的「成功」字樣閃爍顯示。</span><span class="sxs-lookup"><span data-stu-id="98601-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="98601-204">若要針對您的應用程式測試自動交換，可在 [自動交換位置] 中選取非生產的目標位置，以便先熟悉這個功能。</span><span class="sxs-lookup"><span data-stu-id="98601-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="98601-205">執行程式碼推送至該部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="98601-206">自動交換不久之後就會發生，而更新將反映於目標位置的 URL 上。</span><span class="sxs-lookup"><span data-stu-id="98601-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="98601-207">交換之後回復生產應用程式</span><span class="sxs-lookup"><span data-stu-id="98601-207">To rollback a production app after swap</span></span>
<span data-ttu-id="98601-208">若交換位置後，在生產位置中識別出錯誤，可以立即交換相同的兩個位置，將位置還原成交換前的狀態。</span><span class="sxs-lookup"><span data-stu-id="98601-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="98601-209">交換前的自訂準備</span><span class="sxs-lookup"><span data-stu-id="98601-209">Custom warm-up before swap</span></span>
<span data-ttu-id="98601-210">某些應用程式可能需要自訂的準備動作。</span><span class="sxs-lookup"><span data-stu-id="98601-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="98601-211">web.config 中的 `applicationInitialization` 組態項目可讓您指定收到要求之前要執行的自訂初始化動作。</span><span class="sxs-lookup"><span data-stu-id="98601-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="98601-212">必須等候此自訂準備完成，才會進行交換作業。</span><span class="sxs-lookup"><span data-stu-id="98601-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="98601-213">以下是範例 web.config 片段。</span><span class="sxs-lookup"><span data-stu-id="98601-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="98601-214">刪除部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-214">To delete a deployment slot</span></span>
<span data-ttu-id="98601-215">在部署位置的刀鋒視窗中，開啟部署位置的刀鋒視窗，按一下 概觀 \(預設頁面)，然後按一下命令列中的 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="98601-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![刪除部署位置][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="98601-217">適用於部署位置的 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="98601-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="98601-218">Azure PowerShell 模組提供透過 Windows PowerShell 來管理 Azure 的 Cmdlet，包括支援管理 Azure App Service 中的部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="98601-219">如需安裝與設定 Azure PowerShell，以及使用您的 Azure 訂用帳戶驗證 Azure PowerShell 的詳細資訊，請參閱 [如何安裝和設定 Microsoft Azure PowerShell](/powershell/azure/overview)(英文)。</span><span class="sxs-lookup"><span data-stu-id="98601-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="98601-220">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="98601-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="98601-221">建立部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="98601-222">起始使用預覽交換 (多階段交換) 並將目的地位置組態套用至來源位置</span><span class="sxs-lookup"><span data-stu-id="98601-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="98601-223">取消擱置中的交換 (使用預覽交換)，並還原來源位置組態</span><span class="sxs-lookup"><span data-stu-id="98601-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="98601-224">交換部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="98601-225">刪除部署位置</span><span class="sxs-lookup"><span data-stu-id="98601-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="98601-226">適用於部署位置的 Azure 命令列介面 (Azure CLI) 命令</span><span class="sxs-lookup"><span data-stu-id="98601-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="98601-227">Azure CLI 提供跨平台命令供您處理 Azure，包括支援管理 App Service 部署位置。</span><span class="sxs-lookup"><span data-stu-id="98601-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="98601-228">如需安裝與設定 Azure CLI 的相關說明，包括如何將 Azure CLI 連線至 Azure 訂用帳戶的資訊，請參閱 [安裝與設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="98601-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="98601-229">若要在 Azure CLI 中列出 Azure App Service 可用的命令，請呼叫 `azure site -h`。</span><span class="sxs-lookup"><span data-stu-id="98601-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="98601-230">針對適用於部署位置的 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 命令，請參閱 [Azure App Service Web 部署位置](/cli/azure/appservice/web/deployment/slot)。</span><span class="sxs-lookup"><span data-stu-id="98601-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="98601-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="98601-231">azure site list</span></span>
<span data-ttu-id="98601-232">如需目前訂用帳戶中應用程式的相關資訊，請呼叫 **azure site list**，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="98601-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="98601-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="98601-233">azure site create</span></span>
<span data-ttu-id="98601-234">若要建立部署位置，請呼叫 **azure site create** 並指定現有應用程式的名稱與要建立之位置的名稱，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="98601-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="98601-235">若要對新位置啟用來源控制，請使用 **--git** 選項，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="98601-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="98601-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="98601-236">azure site swap</span></span>
<span data-ttu-id="98601-237">若要將已更新的部署位置轉變成生產應用程式，請使用 **azure site swap** 命令來執行交換作業，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="98601-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="98601-238">生產應用程式不會發生任何停機事件，也不會進行冷啟動。</span><span class="sxs-lookup"><span data-stu-id="98601-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="98601-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="98601-239">azure site delete</span></span>
<span data-ttu-id="98601-240">若要刪除不再需要的部署位置，請使用 **azure site delete** 命令，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="98601-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="98601-241">請看看作用中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="98601-241">See a web app in action.</span></span> <span data-ttu-id="98601-242">[試用 App Service](https://azure.microsoft.com/try/app-service/) 並建立短期的入門應用程式 — 不需信用卡，不需任何承諾。</span><span class="sxs-lookup"><span data-stu-id="98601-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="98601-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98601-243">Next Steps</span></span>
<span data-ttu-id="98601-244">[Azure App Service Web 應用程式 - 封鎖對非生產環境部署位置的 Web 存取 (英文)](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Linux 上的 App Service 簡介](./app-service-linux-intro.md)
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="98601-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

