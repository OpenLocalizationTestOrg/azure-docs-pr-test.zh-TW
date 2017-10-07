---
title: "設定預備環境中 Azure App Service web 應用程式的 aaaSet |Microsoft 文件"
description: "了解 toouse 分段發行 Azure App Service 中的 web 應用程式的安裝。"
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
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="a0e00-103">在 Azure App Service 中設定預備環境</span><span class="sxs-lookup"><span data-stu-id="a0e00-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="a0e00-104">當您部署您的 web 應用程式、 Linux、 行動裝置的後端，以及 API 應用程式的 web 應用程式太[App Service](http://go.microsoft.com/fwlink/?LinkId=529714)，hello 中執行時，您可以部署 tooa 不同的部署位置，而不是 hello 預設生產位置**標準**或**Premium**應用程式服務計劃模式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="a0e00-105">部署位置實際上是含有自己主機名稱的作用中應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="a0e00-106">應用程式內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="a0e00-107">部署您的應用程式 tooa 部署位置有 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="a0e00-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="a0e00-108">您可以先再與 hello 生產位置交換驗證預備部署位置中的應用程式變更。</span><span class="sxs-lookup"><span data-stu-id="a0e00-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="a0e00-109">第一次部署的應用程式 tooa 位置和交換至生產環境來確保 hello 位置的所有執行個體正在交換至生產環境之前會就緒。</span><span class="sxs-lookup"><span data-stu-id="a0e00-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="a0e00-110">這麼做可以排除部署應用程式時的停機情況。</span><span class="sxs-lookup"><span data-stu-id="a0e00-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="a0e00-111">hello 流量重新導向，隨選和交換作業之後的任何要求都會被卸除。</span><span class="sxs-lookup"><span data-stu-id="a0e00-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="a0e00-112">不需要預先交換驗證時，這整個工作流程可藉由設定 [自動交換](#Auto-Swap) 來自動化。</span><span class="sxs-lookup"><span data-stu-id="a0e00-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="a0e00-113">交換之後, hello 位置使用先前執行的應用程式現在具有 hello 先前的生產環境應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="a0e00-114">如果 hello 變更成 hello 生產位置交換未如您所預期，您可以執行的 hello 相同交換立即 tooget 您 「 上次已知良好的站台 」 備份。</span><span class="sxs-lookup"><span data-stu-id="a0e00-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="a0e00-115">每個 App Service 方案模式所支援的部署位置個數都不一樣。</span><span class="sxs-lookup"><span data-stu-id="a0e00-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="a0e00-116">您的應用程式模式可支援 toofind 出 hello 的插槽數目，請參閱[應用程式服務定價](https://azure.microsoft.com/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="a0e00-117">當您的應用程式有多個位置時，您無法變更 hello 模式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="a0e00-118">非生產的位置無法使用調整規模。</span><span class="sxs-lookup"><span data-stu-id="a0e00-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="a0e00-119">非生產位置不支援連結的資源管理。</span><span class="sxs-lookup"><span data-stu-id="a0e00-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="a0e00-120">在 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)，暫時移動 hello 非生產位置 tooa 不同應用程式服務計劃模式可以避免此潛在的影響，在生產環境位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="a0e00-121">請注意該 hello 非生產位置必須再次共用 hello hello 生產位置之前，您可以交換 hello 兩個位置具有相同的模式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="a0e00-122">新增部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-122">Add a deployment slot</span></span>
<span data-ttu-id="a0e00-123">hello 應用程式必須執行 hello**標準**或**Premium**您 tooenable 多個部署位置中的模式順序。</span><span class="sxs-lookup"><span data-stu-id="a0e00-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="a0e00-124">在 hello [Azure 入口網站](https://portal.azure.com/)，開啟您的應用程式[資源刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="a0e00-125">選擇 hello**部署位置**選項，然後按一下 **加入位置**。</span><span class="sxs-lookup"><span data-stu-id="a0e00-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![新增部署位置][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="a0e00-127">如果 hello 應用程式已不在 hello**標準**或**Premium**模式中，您會收到訊息，指出啟用預備的發行的 hello 支援模式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="a0e00-128">此時，您擁有 hello 選項 tooselect**升級**並瀏覽 toohello**標尺** 索引標籤，應用程式才能繼續。</span><span class="sxs-lookup"><span data-stu-id="a0e00-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="a0e00-129">在 hello**加入位置**刀鋒視窗中，輸入 hello 插槽的名稱，然後選取是否 tooclone 應用程式組態，從另一個現有的部署位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="a0e00-130">按一下 hello 核取記號 toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a0e00-130">Click hello check mark toocontinue.</span></span>
   
    ![組態來源][ConfigurationSource1]
   
    <span data-ttu-id="a0e00-132">hello 第一次加入位置，您只需要兩個選擇： hello 預設位置在生產環境中，或完全無法執行的複製組態。</span><span class="sxs-lookup"><span data-stu-id="a0e00-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="a0e00-133">建立數個位置之後，您會從實際執行其中一個 hello 以外的位置無法 tooclone 組態：</span><span class="sxs-lookup"><span data-stu-id="a0e00-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![組態來源][MultipleConfigurationSources]
4. <span data-ttu-id="a0e00-135">在您的應用程式資源刀鋒視窗中，按一下**部署位置**，然後按一下該位置的資源刀鋒視窗中，使用一組度量與組態，就像任何其他應用程式的部署位置 tooopen。</span><span class="sxs-lookup"><span data-stu-id="a0e00-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="a0e00-136">hello hello 插槽的名稱會顯示您要檢視在頂端的 hello 刀鋒視窗 tooremind hello hello 部署位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Deployment Slot Title][StagingTitle]
5. <span data-ttu-id="a0e00-138">按一下 在 hello 插槽刀鋒視窗中的 hello 應用程式 URL。</span><span class="sxs-lookup"><span data-stu-id="a0e00-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="a0e00-139">請注意，hello 部署位置具有本身的主機名稱也是即時應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="a0e00-140">toolimit 公用存取 toohello 部署位置，請參閱[App Service Web 應用程式 – 區塊 web 存取 toonon 生產部署位置](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="a0e00-141">建立部署位置之後不會有任何內容。</span><span class="sxs-lookup"><span data-stu-id="a0e00-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="a0e00-142">您可以部署不同的儲存機制分支或完全不同的儲存機制從 toohello 位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="a0e00-143">您也可以變更 hello 位置的組態。</span><span class="sxs-lookup"><span data-stu-id="a0e00-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="a0e00-144">使用 hello 發行設定檔或部署認證更新內容的 hello 部署位置與相關聯。</span><span class="sxs-lookup"><span data-stu-id="a0e00-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="a0e00-145">例如，您可以[發行 toothis 插槽與 git](app-service-deploy-local-git.md)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="a0e00-146">部署位置組態</span><span class="sxs-lookup"><span data-stu-id="a0e00-146">Configuration for deployment slots</span></span>
<span data-ttu-id="a0e00-147">當您複製另一個部署位置的組態時，hello 複製的設定為可編輯。</span><span class="sxs-lookup"><span data-stu-id="a0e00-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="a0e00-148">此外，某些組態項目會依照 hello 內容之間的交換 （沒有位置特定） 其他組態項目都會保留在相同位置 （在特定位置） 的交換之後 hello 時。</span><span class="sxs-lookup"><span data-stu-id="a0e00-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="a0e00-149">hello 下列清單顯示 hello 組態，當交換位置將會變更。</span><span class="sxs-lookup"><span data-stu-id="a0e00-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="a0e00-150">**交換的設定**：</span><span class="sxs-lookup"><span data-stu-id="a0e00-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="a0e00-151">一般設定 - 例如 Framework 版本、32/64 位元、Web 通訊端</span><span class="sxs-lookup"><span data-stu-id="a0e00-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="a0e00-152">（可設定的 toostick tooa 位置） 的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="a0e00-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="a0e00-153">（可設定的 toostick tooa 位置） 的連接字串</span><span class="sxs-lookup"><span data-stu-id="a0e00-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="a0e00-154">處理常式對應</span><span class="sxs-lookup"><span data-stu-id="a0e00-154">Handler mappings</span></span>
* <span data-ttu-id="a0e00-155">監視與診斷設定</span><span class="sxs-lookup"><span data-stu-id="a0e00-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="a0e00-156">WebJobs 內容</span><span class="sxs-lookup"><span data-stu-id="a0e00-156">WebJobs content</span></span>

<span data-ttu-id="a0e00-157">**無法交換的設定**：</span><span class="sxs-lookup"><span data-stu-id="a0e00-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="a0e00-158">發行端點</span><span class="sxs-lookup"><span data-stu-id="a0e00-158">Publishing endpoints</span></span>
* <span data-ttu-id="a0e00-159">自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="a0e00-159">Custom Domain Names</span></span>
* <span data-ttu-id="a0e00-160">SSL 憑證與繫結</span><span class="sxs-lookup"><span data-stu-id="a0e00-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="a0e00-161">擴充設定</span><span class="sxs-lookup"><span data-stu-id="a0e00-161">Scale settings</span></span>
* <span data-ttu-id="a0e00-162">WebJobs 排程器</span><span class="sxs-lookup"><span data-stu-id="a0e00-162">WebJobs schedulers</span></span>

<span data-ttu-id="a0e00-163">應用程式設定或連接字串 toostick tooa 位置 （不交換），存取 hello tooconfigure**應用程式設定**刀鋒視窗中的特定位置，然後選取 hello**位置設定**hello 方塊應盡可能 hello 位置的組態項目。</span><span class="sxs-lookup"><span data-stu-id="a0e00-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="a0e00-164">請注意，將標記的組態項目為特定位置的效果 hello 的跨 hello 應用程式相關聯的所有 hello 部署位置，建立做為不抽換的項目。</span><span class="sxs-lookup"><span data-stu-id="a0e00-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![位置設定][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="a0e00-166">交換部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-166">Swap deployment slots</span></span> 
<span data-ttu-id="a0e00-167">您可以交換部署位置中 hello**概觀**或**部署位置**檢視您的應用程式資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a0e00-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0e00-168">您可以交換部署位置中的應用程式到實際執行環境之前，請確定所有非位置的特定設定已完全依照您想要 toohave 在 hello 交換的目標。</span><span class="sxs-lookup"><span data-stu-id="a0e00-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="a0e00-169">tooswap 部署位置，按一下 hello**交換**hello 的 hello 應用程式的命令列中，或部署位置 hello 命令列中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a0e00-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Swap Button][SwapButtonBar]

2. <span data-ttu-id="a0e00-171">請確定該 hello 交換來源和交換目標都已正確設定。</span><span class="sxs-lookup"><span data-stu-id="a0e00-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="a0e00-172">Hello 交換目標通常就是 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="a0e00-173">按一下**確定**toocomplete hello 作業。</span><span class="sxs-lookup"><span data-stu-id="a0e00-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="a0e00-174">Hello 作業完成時，已交換 hello 部署位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![完整的交換](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="a0e00-176">Hello**使用預覽交換**交換類型，請參閱[預覽 （多階段交換） 的交換](#Multi-Phase)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="a0e00-177">使用預覽交換 (多階段交換)</span><span class="sxs-lookup"><span data-stu-id="a0e00-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="a0e00-178">使用預覽交換或多階段交換，簡化組態項目的位置特定驗證，例如連接字串。</span><span class="sxs-lookup"><span data-stu-id="a0e00-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="a0e00-179">針對關鍵任務工作負載，您想 toovalidate hello 應用程式的行為如預期般套用 hello 生產位置的組態時，而且您必須執行這類驗證*之前*hello 應用程式會交換至生產環境。</span><span class="sxs-lookup"><span data-stu-id="a0e00-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="a0e00-180">您需要的是使用預覽交換。</span><span class="sxs-lookup"><span data-stu-id="a0e00-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e00-181">Linux 上的 Web 應用程式不支援使用預覽交換。</span><span class="sxs-lookup"><span data-stu-id="a0e00-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="a0e00-182">當您使用 hello**預覽交換**選項 (請參閱[交換部署位置](#Swap))，應用程式服務未遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="a0e00-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="a0e00-183">保留 hello 目的地位置未變更所以現有的工作負載上該位置 （例如生產環境） 不會受到影響。</span><span class="sxs-lookup"><span data-stu-id="a0e00-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="a0e00-184">適用於 hello 的 hello 目的地位置 toohello 來源位置，包括 hello 插槽特有的連接字串和應用程式設定的組態項目。</span><span class="sxs-lookup"><span data-stu-id="a0e00-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="a0e00-185">重新啟動 hello 來源位置使用這些先前提及的組態項目上的 hello 工作者處理序。</span><span class="sxs-lookup"><span data-stu-id="a0e00-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="a0e00-186">當您完成 hello 交換： hello 目的地插槽移 hello 前 warmed 向上來源位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="a0e00-187">hello 目的地位置會移到 hello 與手動交換的來源位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="a0e00-188">當您取消 hello 交換： hello 的 hello 來源位置 toohello 來源位置的組態項目會重新套用。</span><span class="sxs-lookup"><span data-stu-id="a0e00-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="a0e00-189">您可以預覽完全 hello 應用程式的行為方式與 hello 目的地位置的組態。</span><span class="sxs-lookup"><span data-stu-id="a0e00-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="a0e00-190">一旦您完成驗證，您會完成在個別步驟中的 hello 交換。</span><span class="sxs-lookup"><span data-stu-id="a0e00-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="a0e00-191">此步驟中具有 hello 好處 hello 來源位置已就緒與 hello 所需的組態，以及用戶端不會經歷任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="a0e00-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="a0e00-192">Hello Azure PowerShell 指令程式可供多階段交換的範例包含在 hello Azure PowerShell cmdlet 的部署位置 區段中。</span><span class="sxs-lookup"><span data-stu-id="a0e00-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="a0e00-193">設定自動交換</span><span class="sxs-lookup"><span data-stu-id="a0e00-193">Configure Auto Swap</span></span>
<span data-ttu-id="a0e00-194">自動交換簡化 DevOps 案例中，您 toocontinuously hello 應用程式的客戶部署應用程式與零冷啟動和零停機時間。</span><span class="sxs-lookup"><span data-stu-id="a0e00-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="a0e00-195">部署位置設定為自動交換到生產環境中，每次推送您的程式碼更新 toothat 位置，當應用程式服務將會自動交換 hello 應用程式至生產環境它有已就緒 hello 插槽中。</span><span class="sxs-lookup"><span data-stu-id="a0e00-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0e00-196">當您啟用自動交換的位置時，請確定 hello 位置組態完全 hello 用於設定 hello 目標位置 （通常 hello 生產位置）。</span><span class="sxs-lookup"><span data-stu-id="a0e00-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="a0e00-197">Linux 上的 Web 應用程式不支援自動交換。</span><span class="sxs-lookup"><span data-stu-id="a0e00-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="a0e00-198">為位置設定自動交換很容易。</span><span class="sxs-lookup"><span data-stu-id="a0e00-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="a0e00-199">請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="a0e00-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="a0e00-200">在**部署位置**中，選取非生產位置，然後在該位置的資源刀鋒視窗中選擇 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="a0e00-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="a0e00-201">選取**上**的**自動交換**，選取中的 hello 想要的目標位置**自動交換位置**，然後按一下**儲存**hello 命令列中。</span><span class="sxs-lookup"><span data-stu-id="a0e00-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="a0e00-202">請確定組態 hello 位置完全 hello 用於設定 hello 目標位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="a0e00-203">hello**通知** 索引標籤將會閃爍綠色**成功**一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="a0e00-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="a0e00-204">tootest 的自動交換，您的應用程式，您可以先選取中的非生產目標位置**自動交換位置**toobecome 熟悉 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="a0e00-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="a0e00-205">執行程式碼推入 toothat 部署位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="a0e00-206">一段時間之後會發生自動交換，而且 hello 更新會反映在目標位置的 URL。</span><span class="sxs-lookup"><span data-stu-id="a0e00-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="a0e00-207">toorollback 交換後在生產應用程式</span><span class="sxs-lookup"><span data-stu-id="a0e00-207">toorollback a production app after swap</span></span>
<span data-ttu-id="a0e00-208">如果發現任何錯誤生產位置交換之後，復原 hello 位置後 tootheir 前交換狀態立即交換 hello 相同的兩個位置。</span><span class="sxs-lookup"><span data-stu-id="a0e00-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="a0e00-209">交換前的自訂準備</span><span class="sxs-lookup"><span data-stu-id="a0e00-209">Custom warm-up before swap</span></span>
<span data-ttu-id="a0e00-210">某些應用程式可能需要自訂的準備動作。</span><span class="sxs-lookup"><span data-stu-id="a0e00-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="a0e00-211">hello `applicationInitialization` web.config 中的組態項目可讓您 toospecify 自訂初始化動作 toobe 執行之前收到要求。</span><span class="sxs-lookup"><span data-stu-id="a0e00-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="a0e00-212">此自訂熱身 toocomplete 將會等到 hello 交換作業。</span><span class="sxs-lookup"><span data-stu-id="a0e00-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="a0e00-213">以下是範例 web.config 片段。</span><span class="sxs-lookup"><span data-stu-id="a0e00-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="a0e00-214">toodelete 部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-214">toodelete a deployment slot</span></span>
<span data-ttu-id="a0e00-215">在 hello 刀鋒視窗中的部署位置，開啟 hello 部署位置的刀鋒視窗中，按一下 **概觀**（hello 預設頁面），然後按一下**刪除**hello 命令列中。</span><span class="sxs-lookup"><span data-stu-id="a0e00-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![刪除部署位置][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="a0e00-217">適用於部署位置的 Azure PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="a0e00-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="a0e00-218">Azure PowerShell 是提供 cmdlet toomanage Azure 透過 Windows PowerShell，包括用於管理 Azure App Service 中的部署位置支援的模組。</span><span class="sxs-lookup"><span data-stu-id="a0e00-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="a0e00-219">如需有關安裝及設定 Azure PowerShell，及其向您的 Azure 訂用帳戶的 Azure PowerShell 的資訊，請參閱[如何 tooinstall 和設定 Microsoft Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="a0e00-220">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="a0e00-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="a0e00-221">建立部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="a0e00-222">起始與檢閱 （多階段交換） 的交換，並套用目的地位置組態 toosource 位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="a0e00-223">取消擱置中的交換 (使用預覽交換)，並還原來源位置組態</span><span class="sxs-lookup"><span data-stu-id="a0e00-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="a0e00-224">交換部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="a0e00-225">刪除部署位置</span><span class="sxs-lookup"><span data-stu-id="a0e00-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="a0e00-226">適用於部署位置的 Azure 命令列介面 (Azure CLI) 命令</span><span class="sxs-lookup"><span data-stu-id="a0e00-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="a0e00-227">hello Azure CLI 提供使用 Azure 中，包括用於管理應用程式服務的部署位置支援跨平台命令。</span><span class="sxs-lookup"><span data-stu-id="a0e00-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="a0e00-228">如需有關安裝和設定指示 hello Azure CLI，包括有關如何 tooconnect Azure CLI tooyour Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a0e00-229">適用於 Azure App Service 中 hello Azure CLI toolist hello 命令呼叫`azure site -h`。</span><span class="sxs-lookup"><span data-stu-id="a0e00-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="a0e00-230">針對適用於部署位置的 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 命令，請參閱 [Azure App Service Web 部署位置](/cli/azure/appservice/web/deployment/slot)。</span><span class="sxs-lookup"><span data-stu-id="a0e00-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="a0e00-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="a0e00-231">azure site list</span></span>
<span data-ttu-id="a0e00-232">如 hello hello 目前訂用帳戶中的應用程式的相關資訊，請呼叫**azure 站台清單**，如下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a0e00-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="a0e00-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="a0e00-233">azure site create</span></span>
<span data-ttu-id="a0e00-234">部署位置，toocreate 呼叫**azure 站台建立**並指定現有的應用程式的 hello 名稱和 hello 插槽 toocreate，如同下列範例中的 hello hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a0e00-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="a0e00-235">hello 新位置，使用 hello tooenable 原始檔控制**-git**選項，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a0e00-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="a0e00-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="a0e00-236">azure site swap</span></span>
<span data-ttu-id="a0e00-237">toomake hello 更新的部署位置 hello 生產環境應用程式，請使用 hello **azure 站台交換**命令 tooperform 交換操作，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a0e00-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="a0e00-238">hello 生產環境應用程式不會經歷任何停機時間，也不會經歷冷啟動。</span><span class="sxs-lookup"><span data-stu-id="a0e00-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="a0e00-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="a0e00-239">azure site delete</span></span>
<span data-ttu-id="a0e00-240">toodelete 部署位置已不再需要請使用 hello **azure 站台刪除**命令，如 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a0e00-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="a0e00-241">請看看作用中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a0e00-241">See a web app in action.</span></span> <span data-ttu-id="a0e00-242">[試用 App Service](https://azure.microsoft.com/try/app-service/) 並建立短期的入門應用程式 — 不需信用卡，不需任何承諾。</span><span class="sxs-lookup"><span data-stu-id="a0e00-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a0e00-243">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0e00-243">Next Steps</span></span>
<span data-ttu-id="a0e00-244">[Azure App Service Web 應用程式 – 封鎖 web 存取 toonon 生產部署位置](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[簡介 tooApp Linux 上的服務](./app-service-linux-intro.md)
[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="a0e00-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
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

