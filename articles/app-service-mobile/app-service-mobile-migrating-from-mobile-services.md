---
title: "aaaMigrate 從行動服務 tooan App Service 行動應用程式"
description: "了解 tooeasily 要如何移轉您的行動服務應用程式 tooan App Service 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="707ec-103"><a name="article-top"></a>移轉您現有的 Azure 行動服務 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="707ec-103"><a name="article-top"></a>Migrate your existing Azure Mobile Service tooAzure App Service</span></span>
<span data-ttu-id="707ec-104">以 hello [Azure 應用程式服務的公開上市]，Azure Mobile Services 站台可以輕鬆地移轉就地 tootake hello Azure App Service 的所有功能的優點。</span><span class="sxs-lookup"><span data-stu-id="707ec-104">With hello [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place tootake advantage of all the features of hello Azure App Service.</span></span>  <span data-ttu-id="707ec-105">本文件說明哪些 tooexpect 時從應用程式服務的 Azure Mobile Services tooAzure 移轉您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-105">This document explains what tooexpect when migrating your site from Azure Mobile Services tooAzure App Service.</span></span>

## <span data-ttu-id="707ec-106"><a name="what-does-migration-do"></a>移轉的作用為何 tooyour 網站</span><span class="sxs-lookup"><span data-stu-id="707ec-106"><a name="what-does-migration-do"></a>What does migration do tooyour site</span></span>
<span data-ttu-id="707ec-107">移轉您的 Azure 行動服務會將行動服務[Azure App Service]應用程式，而不會影響 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="707ec-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting hello code.</span></span>  <span data-ttu-id="707ec-108">您通知中樞、SQL 資料連接、驗證設定、排定的作業和網域名稱都會保持不變。</span><span class="sxs-lookup"><span data-stu-id="707ec-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span></span>  <span data-ttu-id="707ec-109">使用您的 Azure 行動服務的行動用戶端繼續 toooperate 正常運作。</span><span class="sxs-lookup"><span data-stu-id="707ec-109">Mobile clients using your Azure Mobile Service continue toooperate normally.</span></span>  <span data-ttu-id="707ec-110">一旦傳送的 tooAzure 應用程式服務，則移轉會重新啟動您的服務。</span><span class="sxs-lookup"><span data-stu-id="707ec-110">Migration restarts your service once it is transferred tooAzure App Service.</span></span>

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <span data-ttu-id="707ec-111"><a name="why-migrate"></a>為何您應移轉網站</span><span class="sxs-lookup"><span data-stu-id="707ec-111"><a name="why-migrate"></a>Why you should migrate your site</span></span>
<span data-ttu-id="707ec-112">Microsoft 會建議您移轉 hello 功能的 Azure 應用程式服務，包括您 Azure 行動服務 tootake 優點：</span><span class="sxs-lookup"><span data-stu-id="707ec-112">Microsoft is recommending that you migrate your Azure Mobile Service tootake advantage of hello features of Azure App Service, including:</span></span>

* <span data-ttu-id="707ec-113">新的主機功能，包括 [WebJobs] 和[自訂網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="707ec-113">New host features, including [WebJobs] and [custom domain names].</span></span>
* <span data-ttu-id="707ec-114">連線 tooyour 在內部使用的資源[VNet]此外太[混合式連線]。</span><span class="sxs-lookup"><span data-stu-id="707ec-114">Connectivity tooyour on-premises resources using [VNet] in addition too[Hybrid Connections].</span></span>
* <span data-ttu-id="707ec-115">使用 New Relic 或 [Application Insights]進行監視和疑難排解作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-115">Monitoring and troubleshooting with New Relic or [Application Insights].</span></span>
* <span data-ttu-id="707ec-116">內建的 DevOps 工具，包括[預備位置]、回復和生產環境測試。</span><span class="sxs-lookup"><span data-stu-id="707ec-116">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span></span>
* <span data-ttu-id="707ec-117">[自動調整]、負載平衡，以及[效能監視]。</span><span class="sxs-lookup"><span data-stu-id="707ec-117">[Auto-scale], load balancing, and [performance monitoring].</span></span>

<span data-ttu-id="707ec-118">如需 hello 優點 Azure 應用程式服務的詳細資訊，請參閱 hello [vs 行動服務。App Service] 主題。</span><span class="sxs-lookup"><span data-stu-id="707ec-118">For more information on hello benefits of Azure App Service, see hello [Mobile Services vs. App Service] topic.</span></span>

## <span data-ttu-id="707ec-119"><a name="before-you-begin"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="707ec-119"><a name="before-you-begin"></a>Before you begin</span></span>
<span data-ttu-id="707ec-120">網站開始任何主要工作之前，您應該先備份您的行動服務指令碼和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="707ec-120">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span></span>

## <span data-ttu-id="707ec-121"><a name="migrating-site"></a>移轉您的網站</span><span class="sxs-lookup"><span data-stu-id="707ec-121"><a name="migrating-site"></a>Migrating your sites</span></span>
<span data-ttu-id="707ec-122">hello 移轉程序移轉單一 Azure 區域內的所有站台。</span><span class="sxs-lookup"><span data-stu-id="707ec-122">hello migration process migrates all sites within a single Azure Region.</span></span>

<span data-ttu-id="707ec-123">toomigrate 網站：</span><span class="sxs-lookup"><span data-stu-id="707ec-123">toomigrate your site:</span></span>

1. <span data-ttu-id="707ec-124">登入 toohello [Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-124">Log in toohello [Azure Classic Portal].</span></span>
2. <span data-ttu-id="707ec-125">選取行動服務在 hello 區域中，您希望 toomigrate。</span><span class="sxs-lookup"><span data-stu-id="707ec-125">Select a Mobile Service in hello region you wish toomigrate.</span></span>
3. <span data-ttu-id="707ec-126">按一下 hello**移轉 tooApp 服務** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="707ec-126">Click hello **Migrate tooApp Service** button.</span></span>

   ![hello 移轉按鈕][0]
4. <span data-ttu-id="707ec-128">讀取 hello 移轉 tooApp 服務 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="707ec-128">Read hello Migrate tooApp Service dialog.</span></span>
5. <span data-ttu-id="707ec-129">提供的 hello 方塊中輸入您的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-129">Enter hello name of your Mobile Service in hello box provided.</span></span>  <span data-ttu-id="707ec-130">如果您的網域名稱是 contoso.azure mobile.net，比方說，然後輸入*contoso* hello 提供的方塊中。</span><span class="sxs-lookup"><span data-stu-id="707ec-130">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in hello box provided.</span></span>
6. <span data-ttu-id="707ec-131">按一下 hello 刻度 按鈕。</span><span class="sxs-lookup"><span data-stu-id="707ec-131">Click hello tick button.</span></span>

<span data-ttu-id="707ec-132">監視 hello hello 活動監視器 」 中的 hello 移轉狀態。</span><span class="sxs-lookup"><span data-stu-id="707ec-132">Monitor hello status of hello migration in hello activity monitor.</span></span> <span data-ttu-id="707ec-133">您的網站會列為*移轉*hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="707ec-133">Your site is listed as *migrating* in hello Azure Classic Portal.</span></span>

  ![移轉活動監視器][1]

<span data-ttu-id="707ec-135">每個移轉可以需要 3 too15 分鐘每個要移轉的行動服務。</span><span class="sxs-lookup"><span data-stu-id="707ec-135">Each migration can take anywhere from 3 too15 minutes per mobile service being migrated.</span></span>  <span data-ttu-id="707ec-136">Hello 移轉期間，仍可使用您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-136">Your site remains available during hello migration.</span></span>
<span data-ttu-id="707ec-137">您的網站會重新啟動在 hello hello 移轉程序的結尾。</span><span class="sxs-lookup"><span data-stu-id="707ec-137">Your site is restarted at hello end of hello migration process.</span></span>  <span data-ttu-id="707ec-138">hello 重新啟動程序期間，可能會持續幾秒鐘，則無法使用 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="707ec-138">hello site is unavailable during hello restart process, which may last a couple of seconds.</span></span>

## <span data-ttu-id="707ec-139"><a name="finalizing-migration"></a>正在完成 hello 移轉</span><span class="sxs-lookup"><span data-stu-id="707ec-139"><a name="finalizing-migration"></a>Finalizing hello Migration</span></span>
<span data-ttu-id="707ec-140">規劃 tootest 行動用戶端 hello 結論 hello 移轉程序在您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-140">Plan tootest your site from a mobile client at hello conclusion of hello migration process.</span></span>  <span data-ttu-id="707ec-141">請確定您可以執行所有一般不變更 toohello 行動用戶端的用戶端動作。</span><span class="sxs-lookup"><span data-stu-id="707ec-141">Ensure you can perform all common client actions without changes toohello mobile client.</span></span>  

### <span data-ttu-id="707ec-142"><a name="update-app-service-tier"></a>選取適當的 App Service 定價層</span><span class="sxs-lookup"><span data-stu-id="707ec-142"><a name="update-app-service-tier"></a>Select an appropriate App Service pricing tier</span></span>
<span data-ttu-id="707ec-143">您可以更靈活地定價之後移轉 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="707ec-143">You have more flexibility in pricing after you migrate tooAzure App Service.</span></span>

1. <span data-ttu-id="707ec-144">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-144">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-145">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-145">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-146">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-146">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-147">按一下**App Service 方案**hello 設定 功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-147">Click **App Service Plan** in hello Settings menu.</span></span>
5. <span data-ttu-id="707ec-148">按一下 hello**定價層**磚。</span><span class="sxs-lookup"><span data-stu-id="707ec-148">Click hello **Pricing Tier** tile.</span></span>
6. <span data-ttu-id="707ec-149">按一下適當的 tooyour hello 磚的需求，然後按一下 **選取**。</span><span class="sxs-lookup"><span data-stu-id="707ec-149">Click hello tile appropriate tooyour requirements, then Click **Select**.</span></span>  <span data-ttu-id="707ec-150">您可能需要 tooClick**檢視所有**toosee hello 可用的定價層。</span><span class="sxs-lookup"><span data-stu-id="707ec-150">You may need tooClick **View all** toosee hello available pricing tiers.</span></span>

<span data-ttu-id="707ec-151">做為起點，我們建議您遵循層 hello:</span><span class="sxs-lookup"><span data-stu-id="707ec-151">As a starting point, we recommend hello following tiers:</span></span>

| <span data-ttu-id="707ec-152">行動服務定價層</span><span class="sxs-lookup"><span data-stu-id="707ec-152">Mobile Service Pricing Tier</span></span> | <span data-ttu-id="707ec-153">App Service 定價層</span><span class="sxs-lookup"><span data-stu-id="707ec-153">App Service Pricing Tier</span></span> |
|:--- |:--- |
| <span data-ttu-id="707ec-154">免費</span><span class="sxs-lookup"><span data-stu-id="707ec-154">Free</span></span> |<span data-ttu-id="707ec-155">F1 免費</span><span class="sxs-lookup"><span data-stu-id="707ec-155">F1 Free</span></span> |
| <span data-ttu-id="707ec-156">基本</span><span class="sxs-lookup"><span data-stu-id="707ec-156">Basic</span></span> |<span data-ttu-id="707ec-157">B1 基本</span><span class="sxs-lookup"><span data-stu-id="707ec-157">B1 Basic</span></span> |
| <span data-ttu-id="707ec-158">標準</span><span class="sxs-lookup"><span data-stu-id="707ec-158">Standard</span></span> |<span data-ttu-id="707ec-159">S1 標準</span><span class="sxs-lookup"><span data-stu-id="707ec-159">S1 Standard</span></span> |

<span data-ttu-id="707ec-160">選擇 hello 右定價層應用程式中沒有相當大的彈性。</span><span class="sxs-lookup"><span data-stu-id="707ec-160">There is considerable flexibility in choosing hello right pricing tier for your application.</span></span>  <span data-ttu-id="707ec-161">請參閱太[應用程式服務定價]如需新的應用程式服務的定價 hello 的完整詳細資料。</span><span class="sxs-lookup"><span data-stu-id="707ec-161">Refer too[App Service Pricing] for full details on hello pricing of your new App Service.</span></span>

> [!TIP]
> <span data-ttu-id="707ec-162">hello 應用程式服務標準層包含存取 toomany 功能，您可能想 toouse，包括[預備位置]，自動備份，並自動調整。</span><span class="sxs-lookup"><span data-stu-id="707ec-162">hello App Service Standard tier contains access toomany features that you may want toouse, including [staging slots], automatic backups, and auto-scaling.</span></span>  <span data-ttu-id="707ec-163">當您有查看 hello 新功能 ！</span><span class="sxs-lookup"><span data-stu-id="707ec-163">Check out hello new capabilities while you are there!</span></span>
>
>

### <span data-ttu-id="707ec-164"><a name="review-migration-scheduler-jobs"></a>檢閱 hello 移轉排程器作業</span><span class="sxs-lookup"><span data-stu-id="707ec-164"><a name="review-migration-scheduler-jobs"></a>Review hello Migrated Scheduler Jobs</span></span>
<span data-ttu-id="707ec-165">排程器作業在移轉後約 30 分鐘內將不會顯示。</span><span class="sxs-lookup"><span data-stu-id="707ec-165">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span></span>  <span data-ttu-id="707ec-166">排程的工作會繼續 toorun hello 背景。</span><span class="sxs-lookup"><span data-stu-id="707ec-166">Scheduled jobs continue toorun in hello background.</span></span>
<span data-ttu-id="707ec-167">tooview 後才看得見一次排程的工作：</span><span class="sxs-lookup"><span data-stu-id="707ec-167">tooview your scheduled jobs after they are visible again:</span></span>

1. <span data-ttu-id="707ec-168">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-168">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-169">選取**瀏覽 >**，輸入**排程**在 hello*篩選*方塊，然後選取 **排程器集合**。</span><span class="sxs-lookup"><span data-stu-id="707ec-169">Select **Browse>**, enter **Schedule** in hello *Filter* box, then select **Scheduler Collections**.</span></span>

<span data-ttu-id="707ec-170">移轉後可用的排程器作業數量將有所限制。</span><span class="sxs-lookup"><span data-stu-id="707ec-170">There are a limited number of free scheduler jobs available post-migration.</span></span>  <span data-ttu-id="707ec-171">檢閱您的使用量和 hello [Azure 排程器方案]。</span><span class="sxs-lookup"><span data-stu-id="707ec-171">Review your usage and hello [Azure Scheduler Plans].</span></span>

### <span data-ttu-id="707ec-172"><a name="configure-cors"></a>視需要設定 CORS</span><span class="sxs-lookup"><span data-stu-id="707ec-172"><a name="configure-cors"></a>Configure CORS if needed</span></span>
<span data-ttu-id="707ec-173">跨原始資源共用是技術 tooallow 網站 tooaccess Web API 在不同的網域。</span><span class="sxs-lookup"><span data-stu-id="707ec-173">Cross-origin resource sharing is a technique tooallow a website tooaccess a Web API on a different domain.</span></span>  <span data-ttu-id="707ec-174">如果您使用 Azure 行動服務與相關聯的網站，您需要 tooconfigure CORS hello 移轉的一部分。</span><span class="sxs-lookup"><span data-stu-id="707ec-174">If you are using Azure Mobile Services with an associated website, then you need tooconfigure CORS as part of hello migration.</span></span>  <span data-ttu-id="707ec-175">如果您要以獨佔方式從行動裝置存取 Azure 行動服務，CORS 不需要 toobe 設定以外，在少數情況下。</span><span class="sxs-lookup"><span data-stu-id="707ec-175">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need toobe configured except in rare cases.</span></span>

<span data-ttu-id="707ec-176">已移轉的 CORS 設定都像 hello **MS_CrossDomainWhitelist**應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="707ec-176">Your migrated CORS settings are available as hello **MS_CrossDomainWhitelist** App Setting.</span></span>  <span data-ttu-id="707ec-177">toomigrate 您站台 toohello 應用程式服務的 CORS 功能：</span><span class="sxs-lookup"><span data-stu-id="707ec-177">toomigrate your site toohello App Service CORS facility:</span></span>

1. <span data-ttu-id="707ec-178">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-178">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-179">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-179">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-180">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-180">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-181">按一下**CORS** hello API 功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-181">Click **CORS** in hello API menu.</span></span>
5. <span data-ttu-id="707ec-182">任何允許出處 hello 提供方塊中輸入，每個之後按下 Enter。</span><span class="sxs-lookup"><span data-stu-id="707ec-182">Enter any Allowed Origins in hello box provided, pressing Enter after each one.</span></span>
6. <span data-ttu-id="707ec-183">一旦您允許出處的清單正確，請按一下 hello [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="707ec-183">Once your list of Allowed Origins is correct, click hello Save button.</span></span>

> [!TIP]
> <span data-ttu-id="707ec-184">使用 Azure 應用程式服務的 hello 優點的其中一個是，您可以在 hello 上執行您的網站和行動服務相同的站台。</span><span class="sxs-lookup"><span data-stu-id="707ec-184">One of hello advantages of using an Azure App Service is that you can run your web site and mobile service on hello same site.</span></span>  <span data-ttu-id="707ec-185">如需詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。</span><span class="sxs-lookup"><span data-stu-id="707ec-185">For more information, see hello [next steps](#next-steps) section.</span></span>
>
>

### <span data-ttu-id="707ec-186"><a name="download-publish-profile"></a>下載新的發行設定檔</span><span class="sxs-lookup"><span data-stu-id="707ec-186"><a name="download-publish-profile"></a>Download a new Publishing Profile</span></span>
<span data-ttu-id="707ec-187">移轉 tooAzure 應用程式服務時，會變更 hello 網站的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="707ec-187">hello publishing profile of your site is changed when migrating tooAzure App Service.</span></span>  <span data-ttu-id="707ec-188">如果您想 toopublish 您從 Visual Studio 中的網站，您會需要新的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="707ec-188">If you intend toopublish your site from within Visual Studio, you need a new publishing profile.</span></span>  <span data-ttu-id="707ec-189">toodownload hello 新發行設定檔：</span><span class="sxs-lookup"><span data-stu-id="707ec-189">toodownload hello new publishing profile:</span></span>

1. <span data-ttu-id="707ec-190">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-190">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-191">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-191">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-192">按一下 [取得發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="707ec-192">Click **Get publish profile**.</span></span>

<span data-ttu-id="707ec-193">下載的 tooyour 電腦 hello PublishSettings 檔案。</span><span class="sxs-lookup"><span data-stu-id="707ec-193">hello PublishSettings file is downloaded tooyour computer.</span></span>  <span data-ttu-id="707ec-194">此檔案通常名為 *sitename*.PublishSettings。</span><span class="sxs-lookup"><span data-stu-id="707ec-194">It is normally called *sitename*.PublishSettings.</span></span>  <span data-ttu-id="707ec-195">匯入 hello 發行到現有的專案設定：</span><span class="sxs-lookup"><span data-stu-id="707ec-195">Import hello publish settings into your existing project:</span></span>

1. <span data-ttu-id="707ec-196">開啟 Visual Studio 和您的 Azure 行動服務專案。</span><span class="sxs-lookup"><span data-stu-id="707ec-196">Open Visual Studio and your Azure Mobile Service project.</span></span>
2. <span data-ttu-id="707ec-197">以滑鼠右鍵按一下您的專案中 hello**方案總管 中**選取**發行...**</span><span class="sxs-lookup"><span data-stu-id="707ec-197">Right-Click your project in hello **Solution Explorer** and select **Publish...**</span></span>
3. <span data-ttu-id="707ec-198">按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="707ec-198">Click **Import**</span></span>
4. <span data-ttu-id="707ec-199">按一下 [瀏覽]，然後選取已下載的發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="707ec-199">Click **Browse** and select your downloaded publish settings file.</span></span>  <span data-ttu-id="707ec-200">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="707ec-200">Click **OK**</span></span>
5. <span data-ttu-id="707ec-201">按一下**驗證連線**tooensure hello 發行設定的工作。</span><span class="sxs-lookup"><span data-stu-id="707ec-201">Click **Validate Connection** tooensure hello publish settings work.</span></span>
6. <span data-ttu-id="707ec-202">按一下**發行**toopublish 您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-202">Click **Publish** toopublish your site.</span></span>

## <span data-ttu-id="707ec-203"><a name="working-with-your-site"></a>在移轉後使用您的網站</span><span class="sxs-lookup"><span data-stu-id="707ec-203"><a name="working-with-your-site"></a>Working with your site post-migration</span></span>
<span data-ttu-id="707ec-204">開始使用新的應用程式服務在 hello [Azure 入口網站]移轉後。</span><span class="sxs-lookup"><span data-stu-id="707ec-204">Start working with your new App Service in hello [Azure portal] post-migration.</span></span>  <span data-ttu-id="707ec-205">hello 以下是一些附註的特定作業 tooperform 用於 hello [Azure 傳統入口網站]搭配其應用程式服務的對等項目。</span><span class="sxs-lookup"><span data-stu-id="707ec-205">hello following are some notes on specific operations that you used tooperform in hello [Azure Classic Portal], together with their App Service equivalent.</span></span>

### <span data-ttu-id="707ec-206"><a name="publishing-your-site"></a>下載和發佈您已移轉的網站</span><span class="sxs-lookup"><span data-stu-id="707ec-206"><a name="publishing-your-site"></a>Downloading and Publishing your migrated site</span></span>
<span data-ttu-id="707ec-207">您的網站可透過 git 或 ftp 來使用，而且可透過各種不同的機制重新發佈，包括 WebDeploy、TFS、Mercurial、GitHub 及 FTP。</span><span class="sxs-lookup"><span data-stu-id="707ec-207">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span></span>  <span data-ttu-id="707ec-208">hello 的部署認證會以您的站台 hello 其餘部分移轉。</span><span class="sxs-lookup"><span data-stu-id="707ec-208">hello deployment credentials are migrated with hello rest of your site.</span></span>  <span data-ttu-id="707ec-209">如果您未設定部署認證，或您不記得，您可以將其重設：</span><span class="sxs-lookup"><span data-stu-id="707ec-209">If you did not set your deployment credentials or you do not remember them, you can reset them:</span></span>

1. <span data-ttu-id="707ec-210">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-210">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-211">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-211">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-212">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-212">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-213">按一下**部署認證**hello 發行功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-213">Click **Deployment credentials** in hello PUBLISHING menu.</span></span>
5. <span data-ttu-id="707ec-214">Hello 方塊中，請輸入 hello 新的部署認證，然後按一下 [儲存] 按鈕，hello。</span><span class="sxs-lookup"><span data-stu-id="707ec-214">Enter hello new deployment credentials in hello boxes provided, then click hello Save button.</span></span>

<span data-ttu-id="707ec-215">您可以使用這些認證 tooclone hello 站台與 git 或自動部署設定從 GitHub、 TFS 或 Mercurial。</span><span class="sxs-lookup"><span data-stu-id="707ec-215">You can use these credentials tooclone hello site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span></span>  <span data-ttu-id="707ec-216">如需詳細資訊，請參閱 hello [Azure App Service 部署文件]。</span><span class="sxs-lookup"><span data-stu-id="707ec-216">For more information, see hello [Azure App Service deployment documentation].</span></span>

### <span data-ttu-id="707ec-217"><a name="appsettings"></a>應用程式設定</span><span class="sxs-lookup"><span data-stu-id="707ec-217"><a name="appsettings"></a>Application Settings</span></span>
<span data-ttu-id="707ec-218">已移轉的行動服務大部分的設定都可透過 [應用程式設定] 來使用。</span><span class="sxs-lookup"><span data-stu-id="707ec-218">Most settings for a migrated mobile service are available via App Settings.</span></span>  <span data-ttu-id="707ec-219">您可以從 hello 取得一份 hello 應用程式設定[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-219">You can get a list of hello app settings from hello [Azure portal].</span></span>
<span data-ttu-id="707ec-220">tooview 或變更您的應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="707ec-220">tooview or change your app settings:</span></span>

1. <span data-ttu-id="707ec-221">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-221">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-222">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-222">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-223">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-223">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-224">按一下**應用程式設定**hello 一般功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-224">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="707ec-225">捲動 toohello 應用程式設定 區段中，找出您的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="707ec-225">Scroll toohello App Settings section and find your app setting.</span></span>
6. <span data-ttu-id="707ec-226">按一下 hello 應用程式設定 tooedit hello 值 hello 值。</span><span class="sxs-lookup"><span data-stu-id="707ec-226">Click hello value of hello app setting tooedit hello value.</span></span>  <span data-ttu-id="707ec-227">按一下**儲存**toosave hello 值。</span><span class="sxs-lookup"><span data-stu-id="707ec-227">Click **Save** toosave hello value.</span></span>

<span data-ttu-id="707ec-228">您可以更新多個應用程式設定在 hello 相同的時間。</span><span class="sxs-lookup"><span data-stu-id="707ec-228">You can update multiple app settings at hello same time.</span></span>

> [!TIP]
> <span data-ttu-id="707ec-229">有兩個應用程式設定以 hello 相同的值。</span><span class="sxs-lookup"><span data-stu-id="707ec-229">There are two Application Settings with hello same value.</span></span>  <span data-ttu-id="707ec-230">例如，您可能會看到 ApplicationKey 和 MS\_ApplicationKey。</span><span class="sxs-lookup"><span data-stu-id="707ec-230">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span></span>  <span data-ttu-id="707ec-231">更新在 hello 這兩個應用程式設定相同的時間。</span><span class="sxs-lookup"><span data-stu-id="707ec-231">Update both application settings at hello same time.</span></span>
>
>

### <span data-ttu-id="707ec-232"><a name="authentication"></a>驗證</span><span class="sxs-lookup"><span data-stu-id="707ec-232"><a name="authentication"></a>Authentication</span></span>
<span data-ttu-id="707ec-233">所有的驗證設定都可做為已移轉之網站中的 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="707ec-233">All authentication settings are available as App Settings in your migrated site.</span></span>  <span data-ttu-id="707ec-234">tooupdate 您的驗證設定，您必須變更適當的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="707ec-234">tooupdate your authentication settings, you must alter the appropriate app settings.</span></span>  <span data-ttu-id="707ec-235">hello 下表顯示 hello 適當的應用程式設定為驗證提供者：</span><span class="sxs-lookup"><span data-stu-id="707ec-235">hello following table shows hello appropriate app settings for your authentication provider:</span></span>

| <span data-ttu-id="707ec-236">提供者</span><span class="sxs-lookup"><span data-stu-id="707ec-236">Provider</span></span> | <span data-ttu-id="707ec-237">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="707ec-237">Client ID</span></span> | <span data-ttu-id="707ec-238">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="707ec-238">Client Secret</span></span> | <span data-ttu-id="707ec-239">其他設定</span><span class="sxs-lookup"><span data-stu-id="707ec-239">Other Settings</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="707ec-240">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="707ec-240">Microsoft Account</span></span> |<span data-ttu-id="707ec-241">**MS\_MicrosoftClientID**</span><span class="sxs-lookup"><span data-stu-id="707ec-241">**MS\_MicrosoftClientID**</span></span> |<span data-ttu-id="707ec-242">**MS\_MicrosoftClientSecret**</span><span class="sxs-lookup"><span data-stu-id="707ec-242">**MS\_MicrosoftClientSecret**</span></span> |<span data-ttu-id="707ec-243">**MS\_MicrosoftPackageSID**</span><span class="sxs-lookup"><span data-stu-id="707ec-243">**MS\_MicrosoftPackageSID**</span></span> |
| <span data-ttu-id="707ec-244">Facebook</span><span class="sxs-lookup"><span data-stu-id="707ec-244">Facebook</span></span> |<span data-ttu-id="707ec-245">**MS\_FacebookAppID**</span><span class="sxs-lookup"><span data-stu-id="707ec-245">**MS\_FacebookAppID**</span></span> |<span data-ttu-id="707ec-246">**MS\_FacebookAppSecret**</span><span class="sxs-lookup"><span data-stu-id="707ec-246">**MS\_FacebookAppSecret**</span></span> | |
| <span data-ttu-id="707ec-247">Twitter</span><span class="sxs-lookup"><span data-stu-id="707ec-247">Twitter</span></span> |<span data-ttu-id="707ec-248">**MS\_TwitterConsumerKey**</span><span class="sxs-lookup"><span data-stu-id="707ec-248">**MS\_TwitterConsumerKey**</span></span> |<span data-ttu-id="707ec-249">**MS\_TwitterConsumerSecret**</span><span class="sxs-lookup"><span data-stu-id="707ec-249">**MS\_TwitterConsumerSecret**</span></span> | |
| <span data-ttu-id="707ec-250">Google</span><span class="sxs-lookup"><span data-stu-id="707ec-250">Google</span></span> |<span data-ttu-id="707ec-251">**MS\_GoogleClientID**</span><span class="sxs-lookup"><span data-stu-id="707ec-251">**MS\_GoogleClientID**</span></span> |<span data-ttu-id="707ec-252">**MS\_GoogleClientSecret**</span><span class="sxs-lookup"><span data-stu-id="707ec-252">**MS\_GoogleClientSecret**</span></span> | |
| <span data-ttu-id="707ec-253">Azure AD</span><span class="sxs-lookup"><span data-stu-id="707ec-253">Azure AD</span></span> |<span data-ttu-id="707ec-254">**MS\_AadClientID**</span><span class="sxs-lookup"><span data-stu-id="707ec-254">**MS\_AadClientID**</span></span> | |<span data-ttu-id="707ec-255">**MS\_AadTenants**</span><span class="sxs-lookup"><span data-stu-id="707ec-255">**MS\_AadTenants**</span></span> |

<span data-ttu-id="707ec-256">注意： **MS\_AadTenants**儲存為租用戶網域 （hello hello Mobile Services 入口網站中的 「 允許租用戶 」 欄位） 的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="707ec-256">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (hello "Allowed Tenants" fields in hello Mobile Services portal).</span></span>

> [!WARNING]
> <span data-ttu-id="707ec-257">**請勿在 [hello 設定] 功能表中使用 hello 驗證機制**</span><span class="sxs-lookup"><span data-stu-id="707ec-257">**Do not use hello authentication mechanisms in hello Settings menu**</span></span>
>
> <span data-ttu-id="707ec-258">Azure App Service 提供個別 「 沒有程式碼 」 驗證和授權的系統在 hello*驗證 / 授權*設定 功能表和 hello （已過時）*行動驗證*hello 設定 功能表下的選項。</span><span class="sxs-lookup"><span data-stu-id="707ec-258">Azure App Service provides a separate "no-code" Authentication and Authorization system under hello *Authentication / Authorization* Settings menu and hello (deprecated) *Mobile Authentication* option under hello Settings menu.</span></span>  <span data-ttu-id="707ec-259">這些選項與已移轉的 Azure 行動服務不相容。</span><span class="sxs-lookup"><span data-stu-id="707ec-259">These options are incompatible with a migrated Azure Mobile Service.</span></span>  <span data-ttu-id="707ec-260">您可以[升級您的站台](app-service-mobile-net-upgrading-from-mobile-services.md)tootake hello Azure 應用程式服務驗證的優點。</span><span class="sxs-lookup"><span data-stu-id="707ec-260">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) tootake advantage of hello Azure App Service authentication.</span></span>
>
>

### <span data-ttu-id="707ec-261"><a name="easytables"></a>資料</span><span class="sxs-lookup"><span data-stu-id="707ec-261"><a name="easytables"></a>Data</span></span>
<span data-ttu-id="707ec-262">hello*資料*行動服務中的索引標籤已被取代*簡單資料表*hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="707ec-262">hello *Data* tab in Mobile Services has been replaced by *Easy Tables* within hello Azure portal.</span></span>  <span data-ttu-id="707ec-263">tooaccess 簡單的資料表：</span><span class="sxs-lookup"><span data-stu-id="707ec-263">tooaccess Easy Tables:</span></span>

1. <span data-ttu-id="707ec-264">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-264">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-265">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-265">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-266">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-266">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-267">按一下**簡單資料表**hello 行動功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-267">Click **Easy tables** in hello MOBILE menu.</span></span>

<span data-ttu-id="707ec-268">您可以加入資料表，依序按一下 hello**新增**按鈕，或按一下資料表名稱，藉以存取現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="707ec-268">You can add a table by clicking hello **Add** button or access your existing tables by clicking a table name.</span></span>  <span data-ttu-id="707ec-269">在此刀鋒視窗中可以執行各種作業，包括：</span><span class="sxs-lookup"><span data-stu-id="707ec-269">There are various operations you can do from this blade, including:</span></span>

* <span data-ttu-id="707ec-270">變更資料表權限</span><span class="sxs-lookup"><span data-stu-id="707ec-270">Changing table permissions</span></span>
* <span data-ttu-id="707ec-271">編輯 hello 作業指令碼</span><span class="sxs-lookup"><span data-stu-id="707ec-271">Editing hello operational scripts</span></span>
* <span data-ttu-id="707ec-272">管理 hello 資料表結構描述</span><span class="sxs-lookup"><span data-stu-id="707ec-272">Managing hello table schema</span></span>
* <span data-ttu-id="707ec-273">刪除 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="707ec-273">Deleting hello table</span></span>
* <span data-ttu-id="707ec-274">清除 hello 資料表內容</span><span class="sxs-lookup"><span data-stu-id="707ec-274">Clearing hello table contents</span></span>
* <span data-ttu-id="707ec-275">刪除 hello 資料表的特定資料列</span><span class="sxs-lookup"><span data-stu-id="707ec-275">Deleting specific rows of hello table</span></span>

### <span data-ttu-id="707ec-276"><a name="easyapis"></a>API</span><span class="sxs-lookup"><span data-stu-id="707ec-276"><a name="easyapis"></a>API</span></span>
<span data-ttu-id="707ec-277">hello *API*行動服務中的索引標籤已被取代*簡單 Api* hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="707ec-277">hello *API* tab in Mobile Services has been replaced by *Easy APIs* within hello Azure portal.</span></span>  <span data-ttu-id="707ec-278">tooaccess 簡單的 Api:</span><span class="sxs-lookup"><span data-stu-id="707ec-278">tooaccess Easy APIs:</span></span>

1. <span data-ttu-id="707ec-279">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-279">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-280">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-280">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-281">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-281">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-282">按一下**簡單 Api** hello 行動功能表中。</span><span class="sxs-lookup"><span data-stu-id="707ec-282">Click **Easy APIs** in hello MOBILE menu.</span></span>

<span data-ttu-id="707ec-283">您移轉應用程式開發介面已列在 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-283">Your migrated APIs are already listed in hello blade.</span></span>  <span data-ttu-id="707ec-284">您也可以在此刀鋒視窗中新增 API。</span><span class="sxs-lookup"><span data-stu-id="707ec-284">You can also add an API from this blade.</span></span>  <span data-ttu-id="707ec-285">toomanage 特定 API 中，按一下 hello API。</span><span class="sxs-lookup"><span data-stu-id="707ec-285">toomanage a specific API, click hello API.</span></span>
<span data-ttu-id="707ec-286">從 hello 新刀鋒視窗中，您可以調整 hello 權限，並編輯 hello hello API 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="707ec-286">From hello new blade, you can adjust hello permissions and edit hello scripts for hello API.</span></span>

### <span data-ttu-id="707ec-287"><a name="on-demand-jobs"></a>排程器作業</span><span class="sxs-lookup"><span data-stu-id="707ec-287"><a name="on-demand-jobs"></a>Scheduler Jobs</span></span>
<span data-ttu-id="707ec-288">所有排程器工作皆可透過 hello 排程器工作集合 > 一節。</span><span class="sxs-lookup"><span data-stu-id="707ec-288">All scheduler jobs are available through hello Scheduler Job Collections section.</span></span>  <span data-ttu-id="707ec-289">tooaccess 排程器作業：</span><span class="sxs-lookup"><span data-stu-id="707ec-289">tooaccess your scheduler jobs:</span></span>

1. <span data-ttu-id="707ec-290">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-290">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-291">選取**瀏覽 >**，輸入**排程**在 hello*篩選*方塊，然後選取 **排程器集合**。</span><span class="sxs-lookup"><span data-stu-id="707ec-291">Select **Browse>**, enter **Schedule** in hello *Filter* box, then select **Scheduler Collections**.</span></span>
3. <span data-ttu-id="707ec-292">選取您的網站 hello 工作集合。</span><span class="sxs-lookup"><span data-stu-id="707ec-292">Select hello Job Collection for your site.</span></span>  <span data-ttu-id="707ec-293">它的名稱為 *sitename*-Jobs。</span><span class="sxs-lookup"><span data-stu-id="707ec-293">It is named *sitename*-Jobs.</span></span>
4. <span data-ttu-id="707ec-294">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="707ec-294">Click **Settings**.</span></span>
5. <span data-ttu-id="707ec-295">按一下 [管理] 下的 [排程器作業]。</span><span class="sxs-lookup"><span data-stu-id="707ec-295">Click **Scheduler Jobs** under MANAGE.</span></span>

<span data-ttu-id="707ec-296">排程的作業會列出與您指定在移轉前的 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="707ec-296">Scheduled jobs are listed with hello frequency you specified before migration.</span></span>  <span data-ttu-id="707ec-297">隨選作業便已停用。</span><span class="sxs-lookup"><span data-stu-id="707ec-297">On-demand jobs are disabled.</span></span>  <span data-ttu-id="707ec-298">toorun 視作業：</span><span class="sxs-lookup"><span data-stu-id="707ec-298">toorun an on-demand job:</span></span>

1. <span data-ttu-id="707ec-299">選取您想 toorun hello 作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-299">Select hello job you wish toorun.</span></span>
2. <span data-ttu-id="707ec-300">如果有必要，請按一下**啟用**tooenable hello 作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-300">If necessary, click **Enable** tooenable hello job.</span></span>
3. <span data-ttu-id="707ec-301">按一下 [設定]，然後按一下 [排程]。</span><span class="sxs-lookup"><span data-stu-id="707ec-301">Click **Settings**, then **Schedule**.</span></span>
4. <span data-ttu-id="707ec-302">選取 [一次] 的週期性，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="707ec-302">Select a Recurrence of **Once**, then Click **Save**</span></span>

<span data-ttu-id="707ec-303">您的隨需作業會位於 `App_Data/config/scripts/scheduler post-migration`。</span><span class="sxs-lookup"><span data-stu-id="707ec-303">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span></span>  <span data-ttu-id="707ec-304">我們建議您轉換所有隨工作太[WebJobs]或[Functions]。</span><span class="sxs-lookup"><span data-stu-id="707ec-304">We recommend that you convert all on-demand jobs too[WebJobs] or [Functions].</span></span>  <span data-ttu-id="707ec-305">撰寫新的排程器作業，做為 [WebJobs] 或 [Functions]。</span><span class="sxs-lookup"><span data-stu-id="707ec-305">Write new scheduler jobs as [WebJobs] or [Functions].</span></span>

### <span data-ttu-id="707ec-306"><a name="notification-hubs"></a>通知中樞</span><span class="sxs-lookup"><span data-stu-id="707ec-306"><a name="notification-hubs"></a>Notification Hubs</span></span>
<span data-ttu-id="707ec-307">行動服務會使用通知中樞進行推播通知作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-307">Mobile Services uses Notification Hubs for push notifications.</span></span>  <span data-ttu-id="707ec-308">下列應用程式設定的 hello 在移轉之後仍使用的 toolink hello 通知中樞 tooyour 行動服務：</span><span class="sxs-lookup"><span data-stu-id="707ec-308">hello following App Settings are used toolink hello Notification Hub tooyour Mobile Service after migration:</span></span>

| <span data-ttu-id="707ec-309">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="707ec-309">Application Setting</span></span> | <span data-ttu-id="707ec-310">說明</span><span class="sxs-lookup"><span data-stu-id="707ec-310">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="707ec-311">**MS\_PushEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="707ec-311">**MS\_PushEntityNamespace**</span></span> |<span data-ttu-id="707ec-312">hello 通知中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="707ec-312">hello Notification Hub Namespace</span></span> |
| <span data-ttu-id="707ec-313">**MS\_NotificationHubName**</span><span class="sxs-lookup"><span data-stu-id="707ec-313">**MS\_NotificationHubName**</span></span> |<span data-ttu-id="707ec-314">hello 通知中樞名稱</span><span class="sxs-lookup"><span data-stu-id="707ec-314">hello Notification Hub Name</span></span> |
| <span data-ttu-id="707ec-315">**MS\_NotificationHubConnectionString**</span><span class="sxs-lookup"><span data-stu-id="707ec-315">**MS\_NotificationHubConnectionString**</span></span> |<span data-ttu-id="707ec-316">hello 通知中樞連接字串</span><span class="sxs-lookup"><span data-stu-id="707ec-316">hello Notification Hub Connection String</span></span> |
| <span data-ttu-id="707ec-317">**MS\_NamespaceName**</span><span class="sxs-lookup"><span data-stu-id="707ec-317">**MS\_NamespaceName**</span></span> |<span data-ttu-id="707ec-318">MS_PushEntityNamespace 的別名</span><span class="sxs-lookup"><span data-stu-id="707ec-318">An alias for MS_PushEntityNamespace</span></span> |

<span data-ttu-id="707ec-319">透過 hello 管理您的通知中樞[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-319">Your Notification Hub is managed through hello [Azure portal].</span></span>  <span data-ttu-id="707ec-320">請注意 hello 通知中樞名稱 （您可以找到此使用 hello 應用程式設定）：</span><span class="sxs-lookup"><span data-stu-id="707ec-320">Note hello Notification Hub name (you can find this using hello App Settings):</span></span>

1. <span data-ttu-id="707ec-321">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-321">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-322">選取 [瀏覽>]，然後選取 **通知中樞**</span><span class="sxs-lookup"><span data-stu-id="707ec-322">Select **Browse**>, then select **Notification Hubs**</span></span>
3. <span data-ttu-id="707ec-323">按一下 hello 與 hello 行動服務相關聯的通知中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-323">Click hello Notification Hub name associated with hello mobile service.</span></span>

> [!NOTE]
> <span data-ttu-id="707ec-324">如果您的通知中樞是「混合」類型，則不會顯示。</span><span class="sxs-lookup"><span data-stu-id="707ec-324">If your Notification HUb is a "Mixed" type, it is not visible.</span></span>  <span data-ttu-id="707ec-325">「混合」類型的通知中樞會同時使用「通知中樞」和舊版的「服務匯流排」功能。</span><span class="sxs-lookup"><span data-stu-id="707ec-325">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span></span>  <span data-ttu-id="707ec-326">[轉換混合式命名空間]，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-326">[Convert your Mixed namespaces] before continuing.</span></span>  <span data-ttu-id="707ec-327">您的通知中樞 hello 轉換完成之後，會出現在 hello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-327">Once hello conversion is complete, your notification hub appears in hello [Azure portal].</span></span>
>
>

<span data-ttu-id="707ec-328">如需詳細資訊，請檢閱 hello[通知中樞]文件。</span><span class="sxs-lookup"><span data-stu-id="707ec-328">For more information, review hello [Notification Hubs] documentation.</span></span>

> [!TIP]
> <span data-ttu-id="707ec-329">通知中心管理功能，在 hello [Azure 入口網站]是仍在預覽中的。</span><span class="sxs-lookup"><span data-stu-id="707ec-329">Notification Hubs management features in hello [Azure portal] are still in preview.</span></span>  <span data-ttu-id="707ec-330">hello [Azure 傳統入口網站]仍然可供管理所有通知中樞。</span><span class="sxs-lookup"><span data-stu-id="707ec-330">hello [Azure Classic Portal] remains available for managing all your Notification Hubs.</span></span>
>
>

### <span data-ttu-id="707ec-331"><a name="legacy-push"></a>舊版推播設定</span><span class="sxs-lookup"><span data-stu-id="707ec-331"><a name="legacy-push"></a>Legacy Push Settings</span></span>
<span data-ttu-id="707ec-332">如果您配置您之前在通知中樞上的 hello 簡介的行動服務推入，您使用*舊版推播*。</span><span class="sxs-lookup"><span data-stu-id="707ec-332">If you configured Push on your mobile service before hello introduction on Notification Hubs, you are using *legacy push*.</span></span>  <span data-ttu-id="707ec-333">如果您使用推播，組態中卻沒有列出通知中樞，您很可能使用的是「舊版推播」。</span><span class="sxs-lookup"><span data-stu-id="707ec-333">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span></span>  <span data-ttu-id="707ec-334">這項功能會和所有其他功能一起移轉。</span><span class="sxs-lookup"><span data-stu-id="707ec-334">This feature is migrated with all the other features.</span></span>  <span data-ttu-id="707ec-335">不過，建議您升級 tooNotification 集線器後 hello 移轉已完成。</span><span class="sxs-lookup"><span data-stu-id="707ec-335">However, we recommend that you upgrade tooNotification Hubs soon after hello migration is complete.</span></span>

<span data-ttu-id="707ec-336">在 hello 暫時 （與 hello 顯著的例外狀況的 hello APNS 憑證） 的所有 hello 舊版推播設定都可用於應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="707ec-336">In hello interim, all hello legacy push settings (with hello notable exception of hello APNS certificate) are available in App Settings.</span></span>  <span data-ttu-id="707ec-337">透過取代 hello hello 檔案系統上適當的檔案來更新 hello APNS 憑證。</span><span class="sxs-lookup"><span data-stu-id="707ec-337">Update hello APNS certificate by replacing hello appropriate file on hello filesystem.</span></span>

### <span data-ttu-id="707ec-338"><a name="app-settings"></a>其他應用程式設定</span><span class="sxs-lookup"><span data-stu-id="707ec-338"><a name="app-settings"></a>Other App Settings</span></span>
<span data-ttu-id="707ec-339">hello 下列其他應用程式設定會從您的行動服務移轉，可在*設定* > *應用程式設定*:</span><span class="sxs-lookup"><span data-stu-id="707ec-339">hello following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span></span>

| <span data-ttu-id="707ec-340">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="707ec-340">Application Setting</span></span> | <span data-ttu-id="707ec-341">說明</span><span class="sxs-lookup"><span data-stu-id="707ec-341">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="707ec-342">**MS\_MobileServiceName**</span><span class="sxs-lookup"><span data-stu-id="707ec-342">**MS\_MobileServiceName**</span></span> |<span data-ttu-id="707ec-343">hello 應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="707ec-343">hello name of your app</span></span> |
| <span data-ttu-id="707ec-344">**MS\_MobileServiceDomainSuffix**</span><span class="sxs-lookup"><span data-stu-id="707ec-344">**MS\_MobileServiceDomainSuffix**</span></span> |<span data-ttu-id="707ec-345">hello 網域前置詞。</span><span class="sxs-lookup"><span data-stu-id="707ec-345">hello domain prefix.</span></span> <span data-ttu-id="707ec-346">亦即</span><span class="sxs-lookup"><span data-stu-id="707ec-346">i.e</span></span> <span data-ttu-id="707ec-347">azure-mobile.net</span><span class="sxs-lookup"><span data-stu-id="707ec-347">azure-mobile.net</span></span> |
| <span data-ttu-id="707ec-348">**MS\_ApplicationKey**</span><span class="sxs-lookup"><span data-stu-id="707ec-348">**MS\_ApplicationKey**</span></span> |<span data-ttu-id="707ec-349">您的應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="707ec-349">Your application key</span></span> |
| <span data-ttu-id="707ec-350">**MS\_MasterKey**</span><span class="sxs-lookup"><span data-stu-id="707ec-350">**MS\_MasterKey**</span></span> |<span data-ttu-id="707ec-351">您的應用程式主要金鑰</span><span class="sxs-lookup"><span data-stu-id="707ec-351">Your app master key</span></span> |

<span data-ttu-id="707ec-352">hello 應用程式金鑰和主要金鑰都是從原始的行動服務的相同 toohello 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="707ec-352">hello application key and master key are identical toohello Application Keys from your original Mobile Service.</span></span>  <span data-ttu-id="707ec-353">特別是，hello 應用程式金鑰會傳送行動用戶端 toovalidate hello 行動應用程式開發介面使用。</span><span class="sxs-lookup"><span data-stu-id="707ec-353">In particular, hello Application Key is sent by mobile clients toovalidate their use of hello mobile API.</span></span>

### <span data-ttu-id="707ec-354"><a name="cliequivalents"></a>命令列對等項目</span><span class="sxs-lookup"><span data-stu-id="707ec-354"><a name="cliequivalents"></a>Command-Line Equivalents</span></span>
<span data-ttu-id="707ec-355">您可以再使用 hello *azure 行動*命令 toomanage Azure Mobile Services 網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-355">You can longer use hello *azure mobile* command toomanage your Azure Mobile Services site.</span></span>  <span data-ttu-id="707ec-356">相反地，許多函式已取代為 hello *azure 站台*命令。</span><span class="sxs-lookup"><span data-stu-id="707ec-356">Instead, many functions have been replaced with hello *azure site* command.</span></span>  <span data-ttu-id="707ec-357">使用下列資料表 toofind 對等項目的常用命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="707ec-357">Use hello following table toofind equivalents for common commands:</span></span>

| <span data-ttu-id="707ec-358">*Azure Mobile* 命令</span><span class="sxs-lookup"><span data-stu-id="707ec-358">*Azure Mobile* Command</span></span> | <span data-ttu-id="707ec-359">對等的 *Azure site* 命令</span><span class="sxs-lookup"><span data-stu-id="707ec-359">Equivalent *Azure Site* command</span></span> |
|:--- |:--- |
| <span data-ttu-id="707ec-360">mobile locations</span><span class="sxs-lookup"><span data-stu-id="707ec-360">mobile locations</span></span> |<span data-ttu-id="707ec-361">site location list</span><span class="sxs-lookup"><span data-stu-id="707ec-361">site location list</span></span> |
| <span data-ttu-id="707ec-362">mobile list</span><span class="sxs-lookup"><span data-stu-id="707ec-362">mobile list</span></span> |<span data-ttu-id="707ec-363">site list</span><span class="sxs-lookup"><span data-stu-id="707ec-363">site list</span></span> |
| <span data-ttu-id="707ec-364">mobile show *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-364">mobile show *name*</span></span> |<span data-ttu-id="707ec-365">site show *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-365">site show *name*</span></span> |
| <span data-ttu-id="707ec-366">mobile restart *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-366">mobile restart *name*</span></span> |<span data-ttu-id="707ec-367">site restart *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-367">site restart *name*</span></span> |
| <span data-ttu-id="707ec-368">mobile redeploy *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-368">mobile redeploy *name*</span></span> |<span data-ttu-id="707ec-369">site deployment redeploy *commitId* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-369">site deployment redeploy *commitId* *name*</span></span> |
| <span data-ttu-id="707ec-370">mobile key set *name* *type* *value*</span><span class="sxs-lookup"><span data-stu-id="707ec-370">mobile key set *name* *type* *value*</span></span> |<span data-ttu-id="707ec-371">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-371">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="707ec-372">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-372">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="707ec-373">mobile config list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-373">mobile config list *name*</span></span> |<span data-ttu-id="707ec-374">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-374">site appsetting list *name*</span></span> |
| <span data-ttu-id="707ec-375">mobile config get *name* *key*</span><span class="sxs-lookup"><span data-stu-id="707ec-375">mobile config get *name* *key*</span></span> |<span data-ttu-id="707ec-376">site appsetting show *key* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-376">site appsetting show *key* *name*</span></span> |
| <span data-ttu-id="707ec-377">mobile config set *name* *key*</span><span class="sxs-lookup"><span data-stu-id="707ec-377">mobile config set *name* *key*</span></span> |<span data-ttu-id="707ec-378">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-378">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="707ec-379">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-379">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="707ec-380">mobile domain list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-380">mobile domain list *name*</span></span> |<span data-ttu-id="707ec-381">site domain list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-381">site domain list *name*</span></span> |
| <span data-ttu-id="707ec-382">mobile domain add *name* *domain*</span><span class="sxs-lookup"><span data-stu-id="707ec-382">mobile domain add *name* *domain*</span></span> |<span data-ttu-id="707ec-383">site domain add *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-383">site domain add *domain* *name*</span></span> |
| <span data-ttu-id="707ec-384">mobile domain delete *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-384">mobile domain delete *name*</span></span> |<span data-ttu-id="707ec-385">site domain delete *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-385">site domain delete *domain* *name*</span></span> |
| <span data-ttu-id="707ec-386">mobile scale show *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-386">mobile scale show *name*</span></span> |<span data-ttu-id="707ec-387">site show *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-387">site show *name*</span></span> |
| <span data-ttu-id="707ec-388">mobile scale change *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-388">mobile scale change *name*</span></span> |<span data-ttu-id="707ec-389">site scale mode *mode* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-389">site scale mode *mode* *name*</span></span> <br /> <span data-ttu-id="707ec-390">site scale instances *instances* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-390">site scale instances *instances* *name*</span></span> |
| <span data-ttu-id="707ec-391">mobile appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-391">mobile appsetting list *name*</span></span> |<span data-ttu-id="707ec-392">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-392">site appsetting list *name*</span></span> |
| <span data-ttu-id="707ec-393">mobile appsetting add *name* *key* *value*</span><span class="sxs-lookup"><span data-stu-id="707ec-393">mobile appsetting add *name* *key* *value*</span></span> |<span data-ttu-id="707ec-394">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-394">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="707ec-395">mobile appsetting delete *name* *key*</span><span class="sxs-lookup"><span data-stu-id="707ec-395">mobile appsetting delete *name* *key*</span></span> |<span data-ttu-id="707ec-396">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-396">site appsetting delete *key* *name*</span></span> |
| <span data-ttu-id="707ec-397">mobile appsetting show *name* *key*</span><span class="sxs-lookup"><span data-stu-id="707ec-397">mobile appsetting show *name* *key*</span></span> |<span data-ttu-id="707ec-398">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="707ec-398">site appsetting delete *key* *name*</span></span> |

<span data-ttu-id="707ec-399">更新設定，藉由更新 hello 適當的應用程式設定的驗證或推播通知。</span><span class="sxs-lookup"><span data-stu-id="707ec-399">Update authentication or push notification settings by updating hello appropriate Application Setting.</span></span>
<span data-ttu-id="707ec-400">請編輯檔案，並透過 ftp 或 git 發佈您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-400">Edit files and publish your site via ftp or git.</span></span>

### <span data-ttu-id="707ec-401"><a name="diagnostics"></a>診斷和記錄</span><span class="sxs-lookup"><span data-stu-id="707ec-401"><a name="diagnostics"></a>Diagnostics and Logging</span></span>
<span data-ttu-id="707ec-402">Azure App Service 通常會停用 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="707ec-402">Diagnostic Logging is normally disabled in an Azure App Service.</span></span>  <span data-ttu-id="707ec-403">tooenable 診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="707ec-403">tooenable diagnostic logging:</span></span>

1. <span data-ttu-id="707ec-404">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-404">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-405">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-405">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-406">預設會開啟 hello 設定 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-406">hello Settings blade opens by default.</span></span>
4. <span data-ttu-id="707ec-407">選取**診斷記錄檔**hello 功能 功能表底下。</span><span class="sxs-lookup"><span data-stu-id="707ec-407">Select **Diagnostic Logs** under hello FEATURES menu.</span></span>
5. <span data-ttu-id="707ec-408">按一下**ON** hello 下列記錄檔：**的應用程式記錄 （檔案系統）**，**詳細錯誤訊息**，和**追蹤失敗的要求**</span><span class="sxs-lookup"><span data-stu-id="707ec-408">Click **ON** for hello following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span></span>
6. <span data-ttu-id="707ec-409">針對 Web 伺服器記錄，按一下 [檔案系統] </span><span class="sxs-lookup"><span data-stu-id="707ec-409">Click **File System** for Web server logging</span></span>
7. <span data-ttu-id="707ec-410">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="707ec-410">Click **Save**</span></span>

<span data-ttu-id="707ec-411">tooview hello 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="707ec-411">tooview hello logs:</span></span>

1. <span data-ttu-id="707ec-412">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="707ec-412">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="707ec-413">選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="707ec-413">Select **All resources** or **App Services** then click hello name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="707ec-414">按一下 hello**工具**按鈕</span><span class="sxs-lookup"><span data-stu-id="707ec-414">Click hello **Tools** button</span></span>
4. <span data-ttu-id="707ec-415">選取**記錄檔資料流**hello 觀察功能表底下。</span><span class="sxs-lookup"><span data-stu-id="707ec-415">Select **Log Stream** under hello OBSERVE menu.</span></span>

<span data-ttu-id="707ec-416">會產生這些記錄檔會顯示在 [hello] 視窗。</span><span class="sxs-lookup"><span data-stu-id="707ec-416">Logs are displayed in hello window as they are generated.</span></span>  <span data-ttu-id="707ec-417">您也可以下載 hello 記錄供稍後分析，使用您的部署認證。</span><span class="sxs-lookup"><span data-stu-id="707ec-417">You can also download hello logs for later analysis using your deployment credentials.</span></span> <span data-ttu-id="707ec-418">如需詳細資訊，請參閱 hello[記錄]文件。</span><span class="sxs-lookup"><span data-stu-id="707ec-418">For more information, see hello [Logging] documentation.</span></span>

## <span data-ttu-id="707ec-419"><a name="known-issues"></a>已知問題</span><span class="sxs-lookup"><span data-stu-id="707ec-419"><a name="known-issues"></a>Known Issues</span></span>
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a><span data-ttu-id="707ec-420">刪除移轉的行動應用程式複製會導致網站服務中斷</span><span class="sxs-lookup"><span data-stu-id="707ec-420">Deleting a Migrated Mobile App Clone causes a site outage</span></span>
<span data-ttu-id="707ec-421">如果您複製您移轉的行動服務，使用 Azure PowerShell，然後刪除 hello 複製時，會移除 hello 實際執行服務的 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="707ec-421">If you clone your migrated mobile service using Azure PowerShell, then delete hello clone, hello DNS entry for your production service is removed.</span></span>  <span data-ttu-id="707ec-422">您的站台不再是可從 hello 網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="707ec-422">Your site is no longer be accessible from hello Internet.</span></span>  

<span data-ttu-id="707ec-423">解決方式： 如果您想 tooclone 您的網站，這樣透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-423">Resolution: If you wish tooclone your site, do so through hello portal.</span></span>

### <a name="changing-webconfig-does-not-work"></a><span data-ttu-id="707ec-424">變更 Web.config 並未發生作用</span><span class="sxs-lookup"><span data-stu-id="707ec-424">Changing Web.config does not work</span></span>
<span data-ttu-id="707ec-425">如果您的 ASP.NET 網站，變更 toohello`Web.config`檔案並不會套用。</span><span class="sxs-lookup"><span data-stu-id="707ec-425">If you have an ASP.NET site, changes toohello `Web.config` file do not get applied.</span></span>  <span data-ttu-id="707ec-426">hello Azure 應用程式服務建立適合`Web.config`啟動 toosupport hello 行動服務執行階段期間的檔案。</span><span class="sxs-lookup"><span data-stu-id="707ec-426">hello Azure App Service builds a suitable `Web.config` file during startup toosupport hello Mobile Services runtime.</span></span>  <span data-ttu-id="707ec-427">您可以使用 XML 轉換檔案來覆寫特定設定 (例如自訂標頭)。</span><span class="sxs-lookup"><span data-stu-id="707ec-427">You can override certain settings (such as custom headers) by using an XML transform file.</span></span>  <span data-ttu-id="707ec-428">建立檔案在呼叫`applicationHost.xdt`-此檔案必須結束 hello`D:\home\site`目錄 hello Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="707ec-428">Create a file in called `applicationHost.xdt` - this file must end up in hello `D:\home\site` directory on hello Azure Service.</span></span>  <span data-ttu-id="707ec-429">透過自訂部署指令碼或直接使用 Kudu 上傳 `applicationHost.xdt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="707ec-429">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span></span>  <span data-ttu-id="707ec-430">hello 下列範例示範的範例文件：</span><span class="sxs-lookup"><span data-stu-id="707ec-430">hello following shows an example document:</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

<span data-ttu-id="707ec-431">如需詳細資訊，請參閱 hello [XDT 轉換範例]GitHub 上的文件。</span><span class="sxs-lookup"><span data-stu-id="707ec-431">For more information, see hello [XDT Transform Samples] documentation on GitHub.</span></span>

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a><span data-ttu-id="707ec-432">移轉的行動服務無法加入 tooTraffic 管理員</span><span class="sxs-lookup"><span data-stu-id="707ec-432">Migrated Mobile Services cannot be added tooTraffic Manager</span></span>
<span data-ttu-id="707ec-433">當您建立 Traffic Manager 設定檔時，您無法直接選擇遷移行動服務 toohello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="707ec-433">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service toohello profile.</span></span>  <span data-ttu-id="707ec-434">使用「外部端點」。</span><span class="sxs-lookup"><span data-stu-id="707ec-434">Use an "external endpoint."</span></span>  <span data-ttu-id="707ec-435">外部端點只能透過 PowerShell 來新增。</span><span class="sxs-lookup"><span data-stu-id="707ec-435">The external endpoint can only be added through PowerShell.</span></span>  <span data-ttu-id="707ec-436">如需詳細資訊，請參閱[流量管理員教學課程](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="707ec-436">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span></span>

## <span data-ttu-id="707ec-437"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="707ec-437"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="707ec-438">您的應用程式成為移轉的 tooApp 服務之後，有更多的功能，您可以使用：</span><span class="sxs-lookup"><span data-stu-id="707ec-438">Now that your application is migrated tooApp Service, there are even more features you can use:</span></span>

* <span data-ttu-id="707ec-439">部署[預備位置]toostage 變更 tooyour 站台可讓您和執行 A / B 測試。</span><span class="sxs-lookup"><span data-stu-id="707ec-439">Deployment [staging slots] allow you toostage changes tooyour site and perform A/B testing.</span></span>
* <span data-ttu-id="707ec-440">[WebJobs] 可取代隨選排定作業。</span><span class="sxs-lookup"><span data-stu-id="707ec-440">[WebJobs] provide a replacement for On-demand scheduled jobs.</span></span>
* <span data-ttu-id="707ec-441">您可以[持續部署]網站的連結您的站台 tooGitHub、 TFS 或 Mercurial。</span><span class="sxs-lookup"><span data-stu-id="707ec-441">You can [continuously deploy] your site by linking your site tooGitHub, TFS, or Mercurial.</span></span>
* <span data-ttu-id="707ec-442">您可以使用[Application Insights] toomonitor 您的網站。</span><span class="sxs-lookup"><span data-stu-id="707ec-442">You can use [Application Insights] toomonitor your site.</span></span>
* <span data-ttu-id="707ec-443">服務的網站和行動裝置應用程式開發介面從 hello 相同的程式碼。</span><span class="sxs-lookup"><span data-stu-id="707ec-443">Serve a website and a Mobile API from hello same code.</span></span>

### <span data-ttu-id="707ec-444"><a name="upgrading-your-site"></a>升級您的行動服務網站 tooAzure 行動應用程式 SDK</span><span class="sxs-lookup"><span data-stu-id="707ec-444"><a name="upgrading-your-site"></a>Upgrading your Mobile Services site tooAzure Mobile Apps SDK</span></span>
* <span data-ttu-id="707ec-445">Node.js 伺服器專案 hello 新[行動應用程式 Node.js SDK]提供數種新功能。</span><span class="sxs-lookup"><span data-stu-id="707ec-445">For Node.js-based server projects, hello new [Mobile Apps Node.js SDK] provides several new features.</span></span> <span data-ttu-id="707ec-446">例如，您現在可以執行本機開發和偵錯、使用 0.10 以上的任何 Node.js 版本，以及使用任何 Express.js 中介軟體自訂。</span><span class="sxs-lookup"><span data-stu-id="707ec-446">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span></span>
* <span data-ttu-id="707ec-447">。以網路為基礎的伺服器專案中，新 hello[行動應用程式 SDK 的 NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)NuGet 相依性上有更大的彈性。</span><span class="sxs-lookup"><span data-stu-id="707ec-447">For .NET-based server projects, hello new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span></span>  <span data-ttu-id="707ec-448">這些封裝支援 hello 新的應用程式服務驗證，並與任何 ASP.NET 專案撰寫。</span><span class="sxs-lookup"><span data-stu-id="707ec-448">These packages support hello new App Service authentication, and compose with any ASP.NET project.</span></span> <span data-ttu-id="707ec-449">若要深入了解如何升級，請參閱[升級您現有的.NET 行動服務 tooApp 服務](app-service-mobile-net-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="707ec-449">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service tooApp Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[App Service 價格]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[自動調整]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Azure App Service 部署文件]: ../app-service-web/web-sites-deploy.md
[Azure 傳統入口網站]: https://manage.windowsazure.com
[Azure 入口網站]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure 排程器方案]: ../scheduler/scheduler-plans-billing.md
[持續部署]: ../app-service-web/app-service-continuous-deployment.md
[轉換混合式命名空間]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[自訂網域名稱]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[Azure 應用程式服務的公開上市]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[混合式連線]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md
[行動應用程式 Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[vs 行動服務。App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[通知中樞]: ../notification-hubs/notification-hubs-push-notification-overview.md
[效能監視]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[預備位置]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT 轉換範例]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[Functions]: ../azure-functions/functions-overview.md
