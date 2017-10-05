---
title: "從行動服務移轉到應用程式服務行動應用程式"
description: "了解如何輕鬆地將您的行動服務應用程式移轉至應用程式服務行動應用程式"
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
ms.openlocfilehash: 16cf05f62602e494affed49e466209b68413e53a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="73e55-103"><a name="article-top"></a>將您現有的 Azure 行動服務移轉至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="73e55-103"><a name="article-top"></a>Migrate your existing Azure Mobile Service to Azure App Service</span></span>
<span data-ttu-id="73e55-104">透過 [Azure App Service 的公開上市版]，Azure 行動服務網站將可輕易地就地移轉，以使用 Azure App Service 的所有功能。</span><span class="sxs-lookup"><span data-stu-id="73e55-104">With the [general availability of Azure App Service], Azure Mobile Services sites can be easily migrated in-place to take advantage of all the features of the Azure App Service.</span></span>  <span data-ttu-id="73e55-105">本文件說明將您的網站從 Azure 行動服務移轉至 Azure App Service 時的情形。</span><span class="sxs-lookup"><span data-stu-id="73e55-105">This document explains what to expect when migrating your site from Azure Mobile Services to Azure App Service.</span></span>

## <span data-ttu-id="73e55-106"><a name="what-does-migration-do"></a>移轉對您的網站有何作用</span><span class="sxs-lookup"><span data-stu-id="73e55-106"><a name="what-does-migration-do"></a>What does migration do to your site</span></span>
<span data-ttu-id="73e55-107">移轉 Azure 行動服務，會使您的行動服務變成 [Azure App Service] 應用程式，而不會對程式碼造成任何影響。</span><span class="sxs-lookup"><span data-stu-id="73e55-107">Migration of your Azure Mobile Service turns your Mobile Service into an [Azure App Service] app without affecting the code.</span></span>  <span data-ttu-id="73e55-108">您通知中樞、SQL 資料連接、驗證設定、排定的作業和網域名稱都會保持不變。</span><span class="sxs-lookup"><span data-stu-id="73e55-108">Your Notification Hubs, SQL data connection, authentication settings, scheduled jobs, and domain name remain unchanged.</span></span>  <span data-ttu-id="73e55-109">使用您的 Azure 行動服務的行動用戶端仍可正常運作。</span><span class="sxs-lookup"><span data-stu-id="73e55-109">Mobile clients using your Azure Mobile Service continue to operate normally.</span></span>  <span data-ttu-id="73e55-110">移轉會在您的服務轉換為 Azure App Service 後加以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="73e55-110">Migration restarts your service once it is transferred to Azure App Service.</span></span>

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <span data-ttu-id="73e55-111"><a name="why-migrate"></a>為何您應移轉網站</span><span class="sxs-lookup"><span data-stu-id="73e55-111"><a name="why-migrate"></a>Why you should migrate your site</span></span>
<span data-ttu-id="73e55-112">Microsoft 建議您移轉 Azure 行動服務，以使用 Azure App Service 的各項功能，其中包括：</span><span class="sxs-lookup"><span data-stu-id="73e55-112">Microsoft is recommending that you migrate your Azure Mobile Service to take advantage of the features of Azure App Service, including:</span></span>

* <span data-ttu-id="73e55-113">新的主機功能，包括 [WebJobs] 和[自訂網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="73e55-113">New host features, including [WebJobs] and [custom domain names].</span></span>
* <span data-ttu-id="73e55-114">除了[混合式連線]以外，使用 [VNet] 連線到您的內部部署資源。</span><span class="sxs-lookup"><span data-stu-id="73e55-114">Connectivity to your on-premises resources using [VNet] in addition to [Hybrid Connections].</span></span>
* <span data-ttu-id="73e55-115">使用 New Relic 或 [Application Insights]進行監視和疑難排解作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-115">Monitoring and troubleshooting with New Relic or [Application Insights].</span></span>
* <span data-ttu-id="73e55-116">內建的 DevOps 工具，包括[預備位置]、回復和生產環境測試。</span><span class="sxs-lookup"><span data-stu-id="73e55-116">Built-in DevOps tooling, including [staging slots], roll-back, and in-production testing.</span></span>
* <span data-ttu-id="73e55-117">[自動調整]、負載平衡，以及[效能監視]。</span><span class="sxs-lookup"><span data-stu-id="73e55-117">[Auto-scale], load balancing, and [performance monitoring].</span></span>

<span data-ttu-id="73e55-118">若想進一步了解 Azure App Service 的優點，請參閱[比較行動服務與App Service] 主題。</span><span class="sxs-lookup"><span data-stu-id="73e55-118">For more information on the benefits of Azure App Service, see the [Mobile Services vs. App Service] topic.</span></span>

## <span data-ttu-id="73e55-119"><a name="before-you-begin"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="73e55-119"><a name="before-you-begin"></a>Before you begin</span></span>
<span data-ttu-id="73e55-120">網站開始任何主要工作之前，您應該先備份您的行動服務指令碼和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="73e55-120">Before beginning any major work on your site, you should back up your Mobile Service scripts and SQL database.</span></span>

## <span data-ttu-id="73e55-121"><a name="migrating-site"></a>移轉您的網站</span><span class="sxs-lookup"><span data-stu-id="73e55-121"><a name="migrating-site"></a>Migrating your sites</span></span>
<span data-ttu-id="73e55-122">移轉程序會移轉單一 Azure 區域內的所有網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-122">The migration process migrates all sites within a single Azure Region.</span></span>

<span data-ttu-id="73e55-123">若要移轉您的網站：</span><span class="sxs-lookup"><span data-stu-id="73e55-123">To migrate your site:</span></span>

1. <span data-ttu-id="73e55-124">登入 [Azure 傳統入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-124">Log in to the [Azure Classic Portal].</span></span>
2. <span data-ttu-id="73e55-125">選取區域中您想要移轉的行動服務。</span><span class="sxs-lookup"><span data-stu-id="73e55-125">Select a Mobile Service in the region you wish to migrate.</span></span>
3. <span data-ttu-id="73e55-126">按一下 [移轉至 App Service]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e55-126">Click the **Migrate to App Service** button.</span></span>

   ![移轉按鈕][0]
4. <span data-ttu-id="73e55-128">閱讀 [移轉至 App Service] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="73e55-128">Read the Migrate to App Service dialog.</span></span>
5. <span data-ttu-id="73e55-129">在提供的方塊中輸入您的行動服務名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-129">Enter the name of your Mobile Service in the box provided.</span></span>  <span data-ttu-id="73e55-130">例如，如果您的網域名稱是 contoso.azure-mobile.net，請在提供的方塊中輸入 *contoso*。</span><span class="sxs-lookup"><span data-stu-id="73e55-130">For example, if your domain name is contoso.azure-mobile.net, then enter *contoso* in the box provided.</span></span>
6. <span data-ttu-id="73e55-131">按一下勾號按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e55-131">Click the tick button.</span></span>

<span data-ttu-id="73e55-132">在活動監視器中監視移轉的狀態。</span><span class="sxs-lookup"><span data-stu-id="73e55-132">Monitor the status of the migration in the activity monitor.</span></span> <span data-ttu-id="73e55-133">您的網站會在 Azure 傳統入口網站中列為*移轉中*。</span><span class="sxs-lookup"><span data-stu-id="73e55-133">Your site is listed as *migrating* in the Azure Classic Portal.</span></span>

  ![移轉活動監視器][1]

<span data-ttu-id="73e55-135">每個移轉的行動服務在每次移轉時可能需要 3 到 15 分鐘不等。</span><span class="sxs-lookup"><span data-stu-id="73e55-135">Each migration can take anywhere from 3 to 15 minutes per mobile service being migrated.</span></span>  <span data-ttu-id="73e55-136">移轉期間仍可使用您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-136">Your site remains available during the migration.</span></span>
<span data-ttu-id="73e55-137">您的網站會在移轉程序結束時重新啟動。</span><span class="sxs-lookup"><span data-stu-id="73e55-137">Your site is restarted at the end of the migration process.</span></span>  <span data-ttu-id="73e55-138">在重新啟動程序期間無法使用網站，此狀況可能會持續幾秒鐘。</span><span class="sxs-lookup"><span data-stu-id="73e55-138">The site is unavailable during the restart process, which may last a couple of seconds.</span></span>

## <span data-ttu-id="73e55-139"><a name="finalizing-migration"></a>完成移轉</span><span class="sxs-lookup"><span data-stu-id="73e55-139"><a name="finalizing-migration"></a>Finalizing the Migration</span></span>
<span data-ttu-id="73e55-140">規劃在移轉程序結束後從行動用戶端測試您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-140">Plan to test your site from a mobile client at the conclusion of the migration process.</span></span>  <span data-ttu-id="73e55-141">請確定您可以執行所有的一般用戶端動作，而不會變更行動用戶端。</span><span class="sxs-lookup"><span data-stu-id="73e55-141">Ensure you can perform all common client actions without changes to the mobile client.</span></span>  

### <span data-ttu-id="73e55-142"><a name="update-app-service-tier"></a>選取適當的 App Service 定價層</span><span class="sxs-lookup"><span data-stu-id="73e55-142"><a name="update-app-service-tier"></a>Select an appropriate App Service pricing tier</span></span>
<span data-ttu-id="73e55-143">在移轉至 Azure App Service 之後，您在價格方面將會有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="73e55-143">You have more flexibility in pricing after you migrate to Azure App Service.</span></span>

1. <span data-ttu-id="73e55-144">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-144">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-145">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-145">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-146">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-146">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-147">按一下 [設定] 功能表中的 [App Service 方案] 。</span><span class="sxs-lookup"><span data-stu-id="73e55-147">Click **App Service Plan** in the Settings menu.</span></span>
5. <span data-ttu-id="73e55-148">按一下 [定價層] 圖格。</span><span class="sxs-lookup"><span data-stu-id="73e55-148">Click the **Pricing Tier** tile.</span></span>
6. <span data-ttu-id="73e55-149">按一下您的需求適用的圖格，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="73e55-149">Click the tile appropriate to your requirements, then Click **Select**.</span></span>  <span data-ttu-id="73e55-150">您可能需要按一下 [檢視全部]，才能查看可用的定價層。</span><span class="sxs-lookup"><span data-stu-id="73e55-150">You may need to Click **View all** to see the available pricing tiers.</span></span>

<span data-ttu-id="73e55-151">建議您以下列各層做為起點：</span><span class="sxs-lookup"><span data-stu-id="73e55-151">As a starting point, we recommend the following tiers:</span></span>

| <span data-ttu-id="73e55-152">行動服務定價層</span><span class="sxs-lookup"><span data-stu-id="73e55-152">Mobile Service Pricing Tier</span></span> | <span data-ttu-id="73e55-153">App Service 定價層</span><span class="sxs-lookup"><span data-stu-id="73e55-153">App Service Pricing Tier</span></span> |
|:--- |:--- |
| <span data-ttu-id="73e55-154">免費</span><span class="sxs-lookup"><span data-stu-id="73e55-154">Free</span></span> |<span data-ttu-id="73e55-155">F1 免費</span><span class="sxs-lookup"><span data-stu-id="73e55-155">F1 Free</span></span> |
| <span data-ttu-id="73e55-156">基本</span><span class="sxs-lookup"><span data-stu-id="73e55-156">Basic</span></span> |<span data-ttu-id="73e55-157">B1 基本</span><span class="sxs-lookup"><span data-stu-id="73e55-157">B1 Basic</span></span> |
| <span data-ttu-id="73e55-158">標準</span><span class="sxs-lookup"><span data-stu-id="73e55-158">Standard</span></span> |<span data-ttu-id="73e55-159">S1 標準</span><span class="sxs-lookup"><span data-stu-id="73e55-159">S1 Standard</span></span> |

<span data-ttu-id="73e55-160">您有相當大的彈性可為應用程式選擇適當的定價層。</span><span class="sxs-lookup"><span data-stu-id="73e55-160">There is considerable flexibility in choosing the right pricing tier for your application.</span></span>  <span data-ttu-id="73e55-161">請參閱 [App Service 價格] ，以充分了解新的 App Service 的價格。</span><span class="sxs-lookup"><span data-stu-id="73e55-161">Refer to [App Service Pricing] for full details on the pricing of your new App Service.</span></span>

> [!TIP]
> <span data-ttu-id="73e55-162">App Service 標準層包含您可能想要使用之多種功能的存取權，包括[預備位置]、自動備份和自動調整。</span><span class="sxs-lookup"><span data-stu-id="73e55-162">The App Service Standard tier contains access to many features that you may want to use, including [staging slots], automatic backups, and auto-scaling.</span></span>  <span data-ttu-id="73e55-163">您可以在相關位置查看新功能。</span><span class="sxs-lookup"><span data-stu-id="73e55-163">Check out the new capabilities while you are there!</span></span>
>
>

### <span data-ttu-id="73e55-164"><a name="review-migration-scheduler-jobs"></a>檢閱已移轉的排程器作業</span><span class="sxs-lookup"><span data-stu-id="73e55-164"><a name="review-migration-scheduler-jobs"></a>Review the Migrated Scheduler Jobs</span></span>
<span data-ttu-id="73e55-165">排程器作業在移轉後約 30 分鐘內將不會顯示。</span><span class="sxs-lookup"><span data-stu-id="73e55-165">Scheduler Jobs will not be visible until approximately 30 minutes after migration.</span></span>  <span data-ttu-id="73e55-166">排程的作業會持續在背景中執行。</span><span class="sxs-lookup"><span data-stu-id="73e55-166">Scheduled jobs continue to run in the background.</span></span>
<span data-ttu-id="73e55-167">若要在排程的作業再度顯現後加以檢視︰</span><span class="sxs-lookup"><span data-stu-id="73e55-167">To view your scheduled jobs after they are visible again:</span></span>

1. <span data-ttu-id="73e55-168">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-168">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-169">選取 [瀏覽 >]、在 [篩選] 方塊中輸入 **Schedule**，然後選取 [排程器集合]。</span><span class="sxs-lookup"><span data-stu-id="73e55-169">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>

<span data-ttu-id="73e55-170">移轉後可用的排程器作業數量將有所限制。</span><span class="sxs-lookup"><span data-stu-id="73e55-170">There are a limited number of free scheduler jobs available post-migration.</span></span>  <span data-ttu-id="73e55-171">檢閱您的使用量和 [Azure 排程器方案]。</span><span class="sxs-lookup"><span data-stu-id="73e55-171">Review your usage and the [Azure Scheduler Plans].</span></span>

### <span data-ttu-id="73e55-172"><a name="configure-cors"></a>視需要設定 CORS</span><span class="sxs-lookup"><span data-stu-id="73e55-172"><a name="configure-cors"></a>Configure CORS if needed</span></span>
<span data-ttu-id="73e55-173">跨原始資源共用是一項可讓網站存取不同網域之 Web API 的技術。</span><span class="sxs-lookup"><span data-stu-id="73e55-173">Cross-origin resource sharing is a technique to allow a website to access a Web API on a different domain.</span></span>  <span data-ttu-id="73e55-174">如果您使用的 Azure 行動服務具有相關聯的網站，您就必須在移轉中設定 CORS。</span><span class="sxs-lookup"><span data-stu-id="73e55-174">If you are using Azure Mobile Services with an associated website, then you need to configure CORS as part of the migration.</span></span>  <span data-ttu-id="73e55-175">如果您從行動裝置以獨佔方式存取 Azure 行動服務，則在絕大多數的情況下都不需要設定 CORS。</span><span class="sxs-lookup"><span data-stu-id="73e55-175">If you are accessing Azure Mobile Services exclusively from mobile devices, then CORS does not need to be configured except in rare cases.</span></span>

<span data-ttu-id="73e55-176">已移轉的 CORS 設定可做為 **MS_CrossDomainWhitelist** 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-176">Your migrated CORS settings are available as the **MS_CrossDomainWhitelist** App Setting.</span></span>  <span data-ttu-id="73e55-177">若要將您的網站移轉至 App Service CORS 工具：</span><span class="sxs-lookup"><span data-stu-id="73e55-177">To migrate your site to the App Service CORS facility:</span></span>

1. <span data-ttu-id="73e55-178">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-178">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-179">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-179">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-180">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-180">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-181">按一下 [API] 功能表中的 [CORS]。</span><span class="sxs-lookup"><span data-stu-id="73e55-181">Click **CORS** in the API menu.</span></span>
5. <span data-ttu-id="73e55-182">在提供的方塊中輸入任何 [允許的原點]，每輸入一個就按一下 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="73e55-182">Enter any Allowed Origins in the box provided, pressing Enter after each one.</span></span>
6. <span data-ttu-id="73e55-183">如果 [允許的原點] 清單正確無誤，請按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e55-183">Once your list of Allowed Origins is correct, click the Save button.</span></span>

> [!TIP]
> <span data-ttu-id="73e55-184">使用 Azure App Service 的優點之一，是您可以在相同網站上執行您的網站和行動服務。</span><span class="sxs-lookup"><span data-stu-id="73e55-184">One of the advantages of using an Azure App Service is that you can run your web site and mobile service on the same site.</span></span>  <span data-ttu-id="73e55-185">如需詳細資訊，請參閱[後續步驟](#next-steps)一節。</span><span class="sxs-lookup"><span data-stu-id="73e55-185">For more information, see the [next steps](#next-steps) section.</span></span>
>
>

### <span data-ttu-id="73e55-186"><a name="download-publish-profile"></a>下載新的發行設定檔</span><span class="sxs-lookup"><span data-stu-id="73e55-186"><a name="download-publish-profile"></a>Download a new Publishing Profile</span></span>
<span data-ttu-id="73e55-187">網站的發行設定檔移轉至 Azure App Service 後，會進行變更。</span><span class="sxs-lookup"><span data-stu-id="73e55-187">The publishing profile of your site is changed when migrating to Azure App Service.</span></span>  <span data-ttu-id="73e55-188">如果您想要從 Visual Studio 發佈您的網站，您需要新的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="73e55-188">If you intend to publish your site from within Visual Studio, you need a new publishing profile.</span></span>  <span data-ttu-id="73e55-189">若要下載新的發行設定檔：</span><span class="sxs-lookup"><span data-stu-id="73e55-189">To download the new publishing profile:</span></span>

1. <span data-ttu-id="73e55-190">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-190">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-191">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-191">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-192">按一下 [取得發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="73e55-192">Click **Get publish profile**.</span></span>

<span data-ttu-id="73e55-193">PublishSettings 檔案會下載至您的電腦。</span><span class="sxs-lookup"><span data-stu-id="73e55-193">The PublishSettings file is downloaded to your computer.</span></span>  <span data-ttu-id="73e55-194">此檔案通常名為 *sitename*.PublishSettings。</span><span class="sxs-lookup"><span data-stu-id="73e55-194">It is normally called *sitename*.PublishSettings.</span></span>  <span data-ttu-id="73e55-195">將發佈設定匯入現有的專案中：</span><span class="sxs-lookup"><span data-stu-id="73e55-195">Import the publish settings into your existing project:</span></span>

1. <span data-ttu-id="73e55-196">開啟 Visual Studio 和您的 Azure 行動服務專案。</span><span class="sxs-lookup"><span data-stu-id="73e55-196">Open Visual Studio and your Azure Mobile Service project.</span></span>
2. <span data-ttu-id="73e55-197">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [發佈...]。</span><span class="sxs-lookup"><span data-stu-id="73e55-197">Right-Click your project in the **Solution Explorer** and select **Publish...**</span></span>
3. <span data-ttu-id="73e55-198">按一下 [匯入]。</span><span class="sxs-lookup"><span data-stu-id="73e55-198">Click **Import**</span></span>
4. <span data-ttu-id="73e55-199">按一下 [瀏覽]，然後選取已下載的發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="73e55-199">Click **Browse** and select your downloaded publish settings file.</span></span>  <span data-ttu-id="73e55-200">按一下 [檔案] &gt; [新增] &gt; [專案] </span><span class="sxs-lookup"><span data-stu-id="73e55-200">Click **OK**</span></span>
5. <span data-ttu-id="73e55-201">按一下 [驗證連接]，確保發佈設定可運作。</span><span class="sxs-lookup"><span data-stu-id="73e55-201">Click **Validate Connection** to ensure the publish settings work.</span></span>
6. <span data-ttu-id="73e55-202">選擇 [發佈] 來發佈您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-202">Click **Publish** to publish your site.</span></span>

## <span data-ttu-id="73e55-203"><a name="working-with-your-site"></a>在移轉後使用您的網站</span><span class="sxs-lookup"><span data-stu-id="73e55-203"><a name="working-with-your-site"></a>Working with your site post-migration</span></span>
<span data-ttu-id="73e55-204">移轉之後，在 [Azure 入口網站]中開始使用新的 App Service。</span><span class="sxs-lookup"><span data-stu-id="73e55-204">Start working with your new App Service in the [Azure portal] post-migration.</span></span>  <span data-ttu-id="73e55-205">以下是您過去在 [Azure 傳統入口網站]中執行之特定作業的某些注意事項，及其 App Service 的對等項目。</span><span class="sxs-lookup"><span data-stu-id="73e55-205">The following are some notes on specific operations that you used to perform in the [Azure Classic Portal], together with their App Service equivalent.</span></span>

### <span data-ttu-id="73e55-206"><a name="publishing-your-site"></a>下載和發佈您已移轉的網站</span><span class="sxs-lookup"><span data-stu-id="73e55-206"><a name="publishing-your-site"></a>Downloading and Publishing your migrated site</span></span>
<span data-ttu-id="73e55-207">您的網站可透過 git 或 ftp 來使用，而且可透過各種不同的機制重新發佈，包括 WebDeploy、TFS、Mercurial、GitHub 及 FTP。</span><span class="sxs-lookup"><span data-stu-id="73e55-207">Your site is available via git or ftp and can be republished with various different mechanisms, including WebDeploy, TFS, Mercurial, GitHub, and FTP.</span></span>  <span data-ttu-id="73e55-208">部署認證會隨著網站的其餘部分移轉。</span><span class="sxs-lookup"><span data-stu-id="73e55-208">The deployment credentials are migrated with the rest of your site.</span></span>  <span data-ttu-id="73e55-209">如果您未設定部署認證，或您不記得，您可以將其重設：</span><span class="sxs-lookup"><span data-stu-id="73e55-209">If you did not set your deployment credentials or you do not remember them, you can reset them:</span></span>

1. <span data-ttu-id="73e55-210">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-210">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-211">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-211">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-212">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-212">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-213">按一下 [發佈] 功能表中的 [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="73e55-213">Click **Deployment credentials** in the PUBLISHING menu.</span></span>
5. <span data-ttu-id="73e55-214">在提供的方塊中輸入新的部署認證，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="73e55-214">Enter the new deployment credentials in the boxes provided, then click the Save button.</span></span>

<span data-ttu-id="73e55-215">您可以使用這些認證透過 git 複製網站，或從 GitHub、TFS 或 Mercurial 設定自動化部署。</span><span class="sxs-lookup"><span data-stu-id="73e55-215">You can use these credentials to clone the site with git or set up automated deployments from GitHub, TFS, or Mercurial.</span></span>  <span data-ttu-id="73e55-216">如需詳細資訊，請參閱 [Azure App Service 部署文件]。</span><span class="sxs-lookup"><span data-stu-id="73e55-216">For more information, see the [Azure App Service deployment documentation].</span></span>

### <span data-ttu-id="73e55-217"><a name="appsettings"></a>應用程式設定</span><span class="sxs-lookup"><span data-stu-id="73e55-217"><a name="appsettings"></a>Application Settings</span></span>
<span data-ttu-id="73e55-218">已移轉的行動服務大部分的設定都可透過 [應用程式設定] 來使用。</span><span class="sxs-lookup"><span data-stu-id="73e55-218">Most settings for a migrated mobile service are available via App Settings.</span></span>  <span data-ttu-id="73e55-219">您可以從 [Azure 入口網站]取得應用程式設定清單。</span><span class="sxs-lookup"><span data-stu-id="73e55-219">You can get a list of the app settings from the [Azure portal].</span></span>
<span data-ttu-id="73e55-220">若要檢視或變更您的應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="73e55-220">To view or change your app settings:</span></span>

1. <span data-ttu-id="73e55-221">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-221">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-222">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-222">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-223">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-223">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-224">按一下 [一般] 功能表中的 [應用程式設定]  。</span><span class="sxs-lookup"><span data-stu-id="73e55-224">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="73e55-225">捲動至 [應用程式設定] 區段，並尋找您的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-225">Scroll to the App Settings section and find your app setting.</span></span>
6. <span data-ttu-id="73e55-226">按一下應用程式設定的值，以編輯該值。</span><span class="sxs-lookup"><span data-stu-id="73e55-226">Click the value of the app setting to edit the value.</span></span>  <span data-ttu-id="73e55-227">按一下 [儲存] 以儲存該值。</span><span class="sxs-lookup"><span data-stu-id="73e55-227">Click **Save** to save the value.</span></span>

<span data-ttu-id="73e55-228">您可以同時更新多個應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-228">You can update multiple app settings at the same time.</span></span>

> [!TIP]
> <span data-ttu-id="73e55-229">有兩個 [應用程式設定] 具有相同的值。</span><span class="sxs-lookup"><span data-stu-id="73e55-229">There are two Application Settings with the same value.</span></span>  <span data-ttu-id="73e55-230">例如，您可能會看到 ApplicationKey 和 MS\_ApplicationKey。</span><span class="sxs-lookup"><span data-stu-id="73e55-230">For example, you may see *ApplicationKey* and *MS\_ApplicationKey*.</span></span>  <span data-ttu-id="73e55-231">同時更新這兩個應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-231">Update both application settings at the same time.</span></span>
>
>

### <span data-ttu-id="73e55-232"><a name="authentication"></a>驗證</span><span class="sxs-lookup"><span data-stu-id="73e55-232"><a name="authentication"></a>Authentication</span></span>
<span data-ttu-id="73e55-233">所有的驗證設定都可做為已移轉之網站中的 [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="73e55-233">All authentication settings are available as App Settings in your migrated site.</span></span>  <span data-ttu-id="73e55-234">若要更新您的驗證設定，您必須變更適當的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-234">To update your authentication settings, you must alter the appropriate app settings.</span></span>  <span data-ttu-id="73e55-235">下表列出您的驗證提供者所適用的應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="73e55-235">The following table shows the appropriate app settings for your authentication provider:</span></span>

| <span data-ttu-id="73e55-236">提供者</span><span class="sxs-lookup"><span data-stu-id="73e55-236">Provider</span></span> | <span data-ttu-id="73e55-237">用戶端識別碼</span><span class="sxs-lookup"><span data-stu-id="73e55-237">Client ID</span></span> | <span data-ttu-id="73e55-238">用戶端密碼</span><span class="sxs-lookup"><span data-stu-id="73e55-238">Client Secret</span></span> | <span data-ttu-id="73e55-239">其他設定</span><span class="sxs-lookup"><span data-stu-id="73e55-239">Other Settings</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="73e55-240">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="73e55-240">Microsoft Account</span></span> |<span data-ttu-id="73e55-241">**MS\_MicrosoftClientID**</span><span class="sxs-lookup"><span data-stu-id="73e55-241">**MS\_MicrosoftClientID**</span></span> |<span data-ttu-id="73e55-242">**MS\_MicrosoftClientSecret**</span><span class="sxs-lookup"><span data-stu-id="73e55-242">**MS\_MicrosoftClientSecret**</span></span> |<span data-ttu-id="73e55-243">**MS\_MicrosoftPackageSID**</span><span class="sxs-lookup"><span data-stu-id="73e55-243">**MS\_MicrosoftPackageSID**</span></span> |
| <span data-ttu-id="73e55-244">Facebook</span><span class="sxs-lookup"><span data-stu-id="73e55-244">Facebook</span></span> |<span data-ttu-id="73e55-245">**MS\_FacebookAppID**</span><span class="sxs-lookup"><span data-stu-id="73e55-245">**MS\_FacebookAppID**</span></span> |<span data-ttu-id="73e55-246">**MS\_FacebookAppSecret**</span><span class="sxs-lookup"><span data-stu-id="73e55-246">**MS\_FacebookAppSecret**</span></span> | |
| <span data-ttu-id="73e55-247">Twitter</span><span class="sxs-lookup"><span data-stu-id="73e55-247">Twitter</span></span> |<span data-ttu-id="73e55-248">**MS\_TwitterConsumerKey**</span><span class="sxs-lookup"><span data-stu-id="73e55-248">**MS\_TwitterConsumerKey**</span></span> |<span data-ttu-id="73e55-249">**MS\_TwitterConsumerSecret**</span><span class="sxs-lookup"><span data-stu-id="73e55-249">**MS\_TwitterConsumerSecret**</span></span> | |
| <span data-ttu-id="73e55-250">Google</span><span class="sxs-lookup"><span data-stu-id="73e55-250">Google</span></span> |<span data-ttu-id="73e55-251">**MS\_GoogleClientID**</span><span class="sxs-lookup"><span data-stu-id="73e55-251">**MS\_GoogleClientID**</span></span> |<span data-ttu-id="73e55-252">**MS\_GoogleClientSecret**</span><span class="sxs-lookup"><span data-stu-id="73e55-252">**MS\_GoogleClientSecret**</span></span> | |
| <span data-ttu-id="73e55-253">Azure AD</span><span class="sxs-lookup"><span data-stu-id="73e55-253">Azure AD</span></span> |<span data-ttu-id="73e55-254">**MS\_AadClientID**</span><span class="sxs-lookup"><span data-stu-id="73e55-254">**MS\_AadClientID**</span></span> | |<span data-ttu-id="73e55-255">**MS\_AadTenants**</span><span class="sxs-lookup"><span data-stu-id="73e55-255">**MS\_AadTenants**</span></span> |

<span data-ttu-id="73e55-256">注意：**MS\_AadTenants** 會儲存為租用戶網域 ([行動服務入口網站] 中的 [允許的租用戶] 欄位) 的逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="73e55-256">Note: **MS\_AadTenants** is stored as a comma-separated list of tenant domains (the "Allowed Tenants" fields in the Mobile Services portal).</span></span>

> [!WARNING]
> <span data-ttu-id="73e55-257">**請不要使用 [設定] 功能表中的驗證機制**</span><span class="sxs-lookup"><span data-stu-id="73e55-257">**Do not use the authentication mechanisms in the Settings menu**</span></span>
>
> <span data-ttu-id="73e55-258">Azure App Service 分別在 [驗證/授權設定] 功能表下提供「無程式碼」驗證和授權系統，以及在 [設定] 功能表下提供已被取代的 [行動驗證] 選項。</span><span class="sxs-lookup"><span data-stu-id="73e55-258">Azure App Service provides a separate "no-code" Authentication and Authorization system under the *Authentication / Authorization* Settings menu and the (deprecated) *Mobile Authentication* option under the Settings menu.</span></span>  <span data-ttu-id="73e55-259">這些選項與已移轉的 Azure 行動服務不相容。</span><span class="sxs-lookup"><span data-stu-id="73e55-259">These options are incompatible with a migrated Azure Mobile Service.</span></span>  <span data-ttu-id="73e55-260">您可以 [升級您的網站](app-service-mobile-net-upgrading-from-mobile-services.md) ，以利用 Azure App Service 驗證功能。</span><span class="sxs-lookup"><span data-stu-id="73e55-260">You can [upgrade your site](app-service-mobile-net-upgrading-from-mobile-services.md) to take advantage of the Azure App Service authentication.</span></span>
>
>

### <span data-ttu-id="73e55-261"><a name="easytables"></a>資料</span><span class="sxs-lookup"><span data-stu-id="73e55-261"><a name="easytables"></a>Data</span></span>
<span data-ttu-id="73e55-262">行動服務中的 [資料] 索引標籤在 Azure 入口網站中已替換為 [簡單資料表]。</span><span class="sxs-lookup"><span data-stu-id="73e55-262">The *Data* tab in Mobile Services has been replaced by *Easy Tables* within the Azure portal.</span></span>  <span data-ttu-id="73e55-263">若要存取簡單資料表：</span><span class="sxs-lookup"><span data-stu-id="73e55-263">To access Easy Tables:</span></span>

1. <span data-ttu-id="73e55-264">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-264">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-265">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-265">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-266">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-266">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-267">按一下 [行動] 功能表中的 [簡單資料表]。</span><span class="sxs-lookup"><span data-stu-id="73e55-267">Click **Easy tables** in the MOBILE menu.</span></span>

<span data-ttu-id="73e55-268">您可以按一下 [新增] 按鈕以新增資料表，或按一下資料表名稱以存取現有的資料表。</span><span class="sxs-lookup"><span data-stu-id="73e55-268">You can add a table by clicking the **Add** button or access your existing tables by clicking a table name.</span></span>  <span data-ttu-id="73e55-269">在此刀鋒視窗中可以執行各種作業，包括：</span><span class="sxs-lookup"><span data-stu-id="73e55-269">There are various operations you can do from this blade, including:</span></span>

* <span data-ttu-id="73e55-270">變更資料表權限</span><span class="sxs-lookup"><span data-stu-id="73e55-270">Changing table permissions</span></span>
* <span data-ttu-id="73e55-271">編輯作業指令碼</span><span class="sxs-lookup"><span data-stu-id="73e55-271">Editing the operational scripts</span></span>
* <span data-ttu-id="73e55-272">管理資料表結構描述</span><span class="sxs-lookup"><span data-stu-id="73e55-272">Managing the table schema</span></span>
* <span data-ttu-id="73e55-273">刪除資料表</span><span class="sxs-lookup"><span data-stu-id="73e55-273">Deleting the table</span></span>
* <span data-ttu-id="73e55-274">清除資料表內容</span><span class="sxs-lookup"><span data-stu-id="73e55-274">Clearing the table contents</span></span>
* <span data-ttu-id="73e55-275">刪除資料表的特定資料列</span><span class="sxs-lookup"><span data-stu-id="73e55-275">Deleting specific rows of the table</span></span>

### <span data-ttu-id="73e55-276"><a name="easyapis"></a>API</span><span class="sxs-lookup"><span data-stu-id="73e55-276"><a name="easyapis"></a>API</span></span>
<span data-ttu-id="73e55-277">行動服務中的 [API] 索引標籤在 Azure 入口網站中已替換為 [簡單 API]。</span><span class="sxs-lookup"><span data-stu-id="73e55-277">The *API* tab in Mobile Services has been replaced by *Easy APIs* within the Azure portal.</span></span>  <span data-ttu-id="73e55-278">若要存取簡單 API：</span><span class="sxs-lookup"><span data-stu-id="73e55-278">To access Easy APIs:</span></span>

1. <span data-ttu-id="73e55-279">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-279">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-280">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-280">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-281">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-281">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-282">按一下 [行動] 功能表中的 [簡單 API]。</span><span class="sxs-lookup"><span data-stu-id="73e55-282">Click **Easy APIs** in the MOBILE menu.</span></span>

<span data-ttu-id="73e55-283">移轉的 API 已經列在刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="73e55-283">Your migrated APIs are already listed in the blade.</span></span>  <span data-ttu-id="73e55-284">您也可以在此刀鋒視窗中新增 API。</span><span class="sxs-lookup"><span data-stu-id="73e55-284">You can also add an API from this blade.</span></span>  <span data-ttu-id="73e55-285">若要管理特定 API，請按一下該 API。</span><span class="sxs-lookup"><span data-stu-id="73e55-285">To manage a specific API, click the API.</span></span>
<span data-ttu-id="73e55-286">從新的刀鋒視窗中，您可以調整權限，以及編輯 API 的指令碼。</span><span class="sxs-lookup"><span data-stu-id="73e55-286">From the new blade, you can adjust the permissions and edit the scripts for the API.</span></span>

### <span data-ttu-id="73e55-287"><a name="on-demand-jobs"></a>排程器作業</span><span class="sxs-lookup"><span data-stu-id="73e55-287"><a name="on-demand-jobs"></a>Scheduler Jobs</span></span>
<span data-ttu-id="73e55-288">所有的排程器作業都可透過 [排程器作業集合] 區段來使用。</span><span class="sxs-lookup"><span data-stu-id="73e55-288">All scheduler jobs are available through the Scheduler Job Collections section.</span></span>  <span data-ttu-id="73e55-289">若要存取您的排程器作業：</span><span class="sxs-lookup"><span data-stu-id="73e55-289">To access your scheduler jobs:</span></span>

1. <span data-ttu-id="73e55-290">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-290">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-291">選取 [瀏覽 >]、在 [篩選] 方塊中輸入 **Schedule**，然後選取 [排程器集合]。</span><span class="sxs-lookup"><span data-stu-id="73e55-291">Select **Browse>**, enter **Schedule** in the *Filter* box, then select **Scheduler Collections**.</span></span>
3. <span data-ttu-id="73e55-292">選取網站的作業集合。</span><span class="sxs-lookup"><span data-stu-id="73e55-292">Select the Job Collection for your site.</span></span>  <span data-ttu-id="73e55-293">它的名稱為 *sitename*-Jobs。</span><span class="sxs-lookup"><span data-stu-id="73e55-293">It is named *sitename*-Jobs.</span></span>
4. <span data-ttu-id="73e55-294">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="73e55-294">Click **Settings**.</span></span>
5. <span data-ttu-id="73e55-295">按一下 [管理] 下的 [排程器作業]。</span><span class="sxs-lookup"><span data-stu-id="73e55-295">Click **Scheduler Jobs** under MANAGE.</span></span>

<span data-ttu-id="73e55-296">排程的工作會以您在移轉之前所指定的頻率列出。</span><span class="sxs-lookup"><span data-stu-id="73e55-296">Scheduled jobs are listed with the frequency you specified before migration.</span></span>  <span data-ttu-id="73e55-297">隨選作業便已停用。</span><span class="sxs-lookup"><span data-stu-id="73e55-297">On-demand jobs are disabled.</span></span>  <span data-ttu-id="73e55-298">若要執行隨選作業：</span><span class="sxs-lookup"><span data-stu-id="73e55-298">To run an on-demand job:</span></span>

1. <span data-ttu-id="73e55-299">選取您想要執行的作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-299">Select the job you wish to run.</span></span>
2. <span data-ttu-id="73e55-300">如有必要，請按一下 [啟用] 以啟用作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-300">If necessary, click **Enable** to enable the job.</span></span>
3. <span data-ttu-id="73e55-301">按一下 [設定]，然後按一下 [排程]。</span><span class="sxs-lookup"><span data-stu-id="73e55-301">Click **Settings**, then **Schedule**.</span></span>
4. <span data-ttu-id="73e55-302">選取 [一次] 的週期性，然後按一下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="73e55-302">Select a Recurrence of **Once**, then Click **Save**</span></span>

<span data-ttu-id="73e55-303">您的隨需作業會位於 `App_Data/config/scripts/scheduler post-migration`。</span><span class="sxs-lookup"><span data-stu-id="73e55-303">Your on-demand jobs are located in `App_Data/config/scripts/scheduler post-migration`.</span></span>  <span data-ttu-id="73e55-304">建議您將所有隨選作業轉換為 [WebJobs] 或 [Functions]。</span><span class="sxs-lookup"><span data-stu-id="73e55-304">We recommend that you convert all on-demand jobs to [WebJobs] or [Functions].</span></span>  <span data-ttu-id="73e55-305">撰寫新的排程器作業，做為 [WebJobs] 或 [Functions]。</span><span class="sxs-lookup"><span data-stu-id="73e55-305">Write new scheduler jobs as [WebJobs] or [Functions].</span></span>

### <span data-ttu-id="73e55-306"><a name="notification-hubs"></a>通知中樞</span><span class="sxs-lookup"><span data-stu-id="73e55-306"><a name="notification-hubs"></a>Notification Hubs</span></span>
<span data-ttu-id="73e55-307">行動服務會使用通知中樞進行推播通知作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-307">Mobile Services uses Notification Hubs for push notifications.</span></span>  <span data-ttu-id="73e55-308">在移轉之後，會使用下列應用程式設定將通知中樞連結至您的行動服務：</span><span class="sxs-lookup"><span data-stu-id="73e55-308">The following App Settings are used to link the Notification Hub to your Mobile Service after migration:</span></span>

| <span data-ttu-id="73e55-309">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="73e55-309">Application Setting</span></span> | <span data-ttu-id="73e55-310">說明</span><span class="sxs-lookup"><span data-stu-id="73e55-310">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73e55-311">**MS\_PushEntityNamespace**</span><span class="sxs-lookup"><span data-stu-id="73e55-311">**MS\_PushEntityNamespace**</span></span> |<span data-ttu-id="73e55-312">通知中樞命名空間</span><span class="sxs-lookup"><span data-stu-id="73e55-312">The Notification Hub Namespace</span></span> |
| <span data-ttu-id="73e55-313">**MS\_NotificationHubName**</span><span class="sxs-lookup"><span data-stu-id="73e55-313">**MS\_NotificationHubName**</span></span> |<span data-ttu-id="73e55-314">通知中樞名稱</span><span class="sxs-lookup"><span data-stu-id="73e55-314">The Notification Hub Name</span></span> |
| <span data-ttu-id="73e55-315">**MS\_NotificationHubConnectionString**</span><span class="sxs-lookup"><span data-stu-id="73e55-315">**MS\_NotificationHubConnectionString**</span></span> |<span data-ttu-id="73e55-316">通知中樞連接字串</span><span class="sxs-lookup"><span data-stu-id="73e55-316">The Notification Hub Connection String</span></span> |
| <span data-ttu-id="73e55-317">**MS\_NamespaceName**</span><span class="sxs-lookup"><span data-stu-id="73e55-317">**MS\_NamespaceName**</span></span> |<span data-ttu-id="73e55-318">MS_PushEntityNamespace 的別名</span><span class="sxs-lookup"><span data-stu-id="73e55-318">An alias for MS_PushEntityNamespace</span></span> |

<span data-ttu-id="73e55-319">您的通知中樞會透過 [Azure 入口網站]管理。</span><span class="sxs-lookup"><span data-stu-id="73e55-319">Your Notification Hub is managed through the [Azure portal].</span></span>  <span data-ttu-id="73e55-320">請記下通知中樞名稱 (您可以使用 [應用程式設定] 找到此項目)：</span><span class="sxs-lookup"><span data-stu-id="73e55-320">Note the Notification Hub name (you can find this using the App Settings):</span></span>

1. <span data-ttu-id="73e55-321">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-321">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-322">選取 [瀏覽>]，然後選取 **通知中樞**</span><span class="sxs-lookup"><span data-stu-id="73e55-322">Select **Browse**>, then select **Notification Hubs**</span></span>
3. <span data-ttu-id="73e55-323">按一下與行動服務相關聯的通知中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-323">Click the Notification Hub name associated with the mobile service.</span></span>

> [!NOTE]
> <span data-ttu-id="73e55-324">如果您的通知中樞是「混合」類型，則不會顯示。</span><span class="sxs-lookup"><span data-stu-id="73e55-324">If your Notification HUb is a "Mixed" type, it is not visible.</span></span>  <span data-ttu-id="73e55-325">「混合」類型的通知中樞會同時使用「通知中樞」和舊版的「服務匯流排」功能。</span><span class="sxs-lookup"><span data-stu-id="73e55-325">"Mixed" type notification hubs utilize both Notification Hubs and legacy Service Bus features.</span></span>  <span data-ttu-id="73e55-326">[轉換混合式命名空間]，再繼續作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-326">[Convert your Mixed namespaces] before continuing.</span></span>  <span data-ttu-id="73e55-327">轉換完成後，您的通知中樞會出現在 [Azure 入口網站]中。</span><span class="sxs-lookup"><span data-stu-id="73e55-327">Once the conversion is complete, your notification hub appears in the [Azure portal].</span></span>
>
>

<span data-ttu-id="73e55-328">如需詳細資訊，請檢閱 [通知中樞] 文件。</span><span class="sxs-lookup"><span data-stu-id="73e55-328">For more information, review the [Notification Hubs] documentation.</span></span>

> [!TIP]
> <span data-ttu-id="73e55-329">[Azure 入口網站]中的通知中樞管理功能仍處於預覽階段。</span><span class="sxs-lookup"><span data-stu-id="73e55-329">Notification Hubs management features in the [Azure portal] are still in preview.</span></span>  <span data-ttu-id="73e55-330">[Azure 傳統入口網站] 仍可用來管理您所有的通知中樞。</span><span class="sxs-lookup"><span data-stu-id="73e55-330">The [Azure Classic Portal] remains available for managing all your Notification Hubs.</span></span>
>
>

### <span data-ttu-id="73e55-331"><a name="legacy-push"></a>舊版推播設定</span><span class="sxs-lookup"><span data-stu-id="73e55-331"><a name="legacy-push"></a>Legacy Push Settings</span></span>
<span data-ttu-id="73e55-332">如果您在通知中樞引入前，即已設定行動服務的推播，您使用的就是「舊版推播」。</span><span class="sxs-lookup"><span data-stu-id="73e55-332">If you configured Push on your mobile service before the introduction on Notification Hubs, you are using *legacy push*.</span></span>  <span data-ttu-id="73e55-333">如果您使用推播，組態中卻沒有列出通知中樞，您很可能使用的是「舊版推播」。</span><span class="sxs-lookup"><span data-stu-id="73e55-333">If you are using Push and you do not see a Notification Hub listed in your configuration, then it is likely you are using *legacy push*.</span></span>  <span data-ttu-id="73e55-334">這項功能會和所有其他功能一起移轉。</span><span class="sxs-lookup"><span data-stu-id="73e55-334">This feature is migrated with all the other features.</span></span>  <span data-ttu-id="73e55-335">不過，建議您完成移轉後盡快升級至通知中樞。</span><span class="sxs-lookup"><span data-stu-id="73e55-335">However, we recommend that you upgrade to Notification Hubs soon after the migration is complete.</span></span>

<span data-ttu-id="73e55-336">在過渡時期，所有舊版推播設定 (APNS 憑證除外) 都可以在應用程式設定中取得。</span><span class="sxs-lookup"><span data-stu-id="73e55-336">In the interim, all the legacy push settings (with the notable exception of the APNS certificate) are available in App Settings.</span></span>  <span data-ttu-id="73e55-337">將檔案系統上適當的檔案替換掉，以更新 APNS 憑證。</span><span class="sxs-lookup"><span data-stu-id="73e55-337">Update the APNS certificate by replacing the appropriate file on the filesystem.</span></span>

### <span data-ttu-id="73e55-338"><a name="app-settings"></a>其他應用程式設定</span><span class="sxs-lookup"><span data-stu-id="73e55-338"><a name="app-settings"></a>Other App Settings</span></span>
<span data-ttu-id="73e55-339">以下是從您的行動服務移轉的其他應用程式設定，可從 [設定] > [應用程式設定]：</span><span class="sxs-lookup"><span data-stu-id="73e55-339">The following additional app settings are migrated from your Mobile Service and available under *Settings* > *App Settings*:</span></span>

| <span data-ttu-id="73e55-340">應用程式設定</span><span class="sxs-lookup"><span data-stu-id="73e55-340">Application Setting</span></span> | <span data-ttu-id="73e55-341">說明</span><span class="sxs-lookup"><span data-stu-id="73e55-341">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="73e55-342">**MS\_MobileServiceName**</span><span class="sxs-lookup"><span data-stu-id="73e55-342">**MS\_MobileServiceName**</span></span> |<span data-ttu-id="73e55-343">您的應用程式名稱</span><span class="sxs-lookup"><span data-stu-id="73e55-343">The name of your app</span></span> |
| <span data-ttu-id="73e55-344">**MS\_MobileServiceDomainSuffix**</span><span class="sxs-lookup"><span data-stu-id="73e55-344">**MS\_MobileServiceDomainSuffix**</span></span> |<span data-ttu-id="73e55-345">網域前置詞。</span><span class="sxs-lookup"><span data-stu-id="73e55-345">The domain prefix.</span></span> <span data-ttu-id="73e55-346">亦即</span><span class="sxs-lookup"><span data-stu-id="73e55-346">i.e</span></span> <span data-ttu-id="73e55-347">azure-mobile.net</span><span class="sxs-lookup"><span data-stu-id="73e55-347">azure-mobile.net</span></span> |
| <span data-ttu-id="73e55-348">**MS\_ApplicationKey**</span><span class="sxs-lookup"><span data-stu-id="73e55-348">**MS\_ApplicationKey**</span></span> |<span data-ttu-id="73e55-349">您的應用程式金鑰</span><span class="sxs-lookup"><span data-stu-id="73e55-349">Your application key</span></span> |
| <span data-ttu-id="73e55-350">**MS\_MasterKey**</span><span class="sxs-lookup"><span data-stu-id="73e55-350">**MS\_MasterKey**</span></span> |<span data-ttu-id="73e55-351">您的應用程式主要金鑰</span><span class="sxs-lookup"><span data-stu-id="73e55-351">Your app master key</span></span> |

<span data-ttu-id="73e55-352">應用程式金鑰和主要金鑰會與原始行動服務中的應用程式金鑰完全相同。</span><span class="sxs-lookup"><span data-stu-id="73e55-352">The application key and master key are identical to the Application Keys from your original Mobile Service.</span></span>  <span data-ttu-id="73e55-353">特別是，行動用戶端會傳送應用程式金鑰，以驗證他們對行動 API 的使用。</span><span class="sxs-lookup"><span data-stu-id="73e55-353">In particular, the Application Key is sent by mobile clients to validate their use of the mobile API.</span></span>

### <span data-ttu-id="73e55-354"><a name="cliequivalents"></a>命令列對等項目</span><span class="sxs-lookup"><span data-stu-id="73e55-354"><a name="cliequivalents"></a>Command-Line Equivalents</span></span>
<span data-ttu-id="73e55-355">您將無法再使用 *azure mobile* 命令來管理您的 Azure 行動服務網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-355">You can longer use the *azure mobile* command to manage your Azure Mobile Services site.</span></span>  <span data-ttu-id="73e55-356">有許多函式已替換為 *azure site* 命令。</span><span class="sxs-lookup"><span data-stu-id="73e55-356">Instead, many functions have been replaced with the *azure site* command.</span></span>  <span data-ttu-id="73e55-357">使用下表來尋找常用命令的對等項目：</span><span class="sxs-lookup"><span data-stu-id="73e55-357">Use the following table to find equivalents for common commands:</span></span>

| <span data-ttu-id="73e55-358">*Azure Mobile* 命令</span><span class="sxs-lookup"><span data-stu-id="73e55-358">*Azure Mobile* Command</span></span> | <span data-ttu-id="73e55-359">對等的 *Azure site* 命令</span><span class="sxs-lookup"><span data-stu-id="73e55-359">Equivalent *Azure Site* command</span></span> |
|:--- |:--- |
| <span data-ttu-id="73e55-360">mobile locations</span><span class="sxs-lookup"><span data-stu-id="73e55-360">mobile locations</span></span> |<span data-ttu-id="73e55-361">site location list</span><span class="sxs-lookup"><span data-stu-id="73e55-361">site location list</span></span> |
| <span data-ttu-id="73e55-362">mobile list</span><span class="sxs-lookup"><span data-stu-id="73e55-362">mobile list</span></span> |<span data-ttu-id="73e55-363">site list</span><span class="sxs-lookup"><span data-stu-id="73e55-363">site list</span></span> |
| <span data-ttu-id="73e55-364">mobile show *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-364">mobile show *name*</span></span> |<span data-ttu-id="73e55-365">site show *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-365">site show *name*</span></span> |
| <span data-ttu-id="73e55-366">mobile restart *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-366">mobile restart *name*</span></span> |<span data-ttu-id="73e55-367">site restart *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-367">site restart *name*</span></span> |
| <span data-ttu-id="73e55-368">mobile redeploy *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-368">mobile redeploy *name*</span></span> |<span data-ttu-id="73e55-369">site deployment redeploy *commitId* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-369">site deployment redeploy *commitId* *name*</span></span> |
| <span data-ttu-id="73e55-370">mobile key set *name* *type* *value*</span><span class="sxs-lookup"><span data-stu-id="73e55-370">mobile key set *name* *type* *value*</span></span> |<span data-ttu-id="73e55-371">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-371">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="73e55-372">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-372">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="73e55-373">mobile config list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-373">mobile config list *name*</span></span> |<span data-ttu-id="73e55-374">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-374">site appsetting list *name*</span></span> |
| <span data-ttu-id="73e55-375">mobile config get *name* *key*</span><span class="sxs-lookup"><span data-stu-id="73e55-375">mobile config get *name* *key*</span></span> |<span data-ttu-id="73e55-376">site appsetting show *key* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-376">site appsetting show *key* *name*</span></span> |
| <span data-ttu-id="73e55-377">mobile config set *name* *key*</span><span class="sxs-lookup"><span data-stu-id="73e55-377">mobile config set *name* *key*</span></span> |<span data-ttu-id="73e55-378">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-378">site appsetting delete *key* *name*</span></span> <br/> <span data-ttu-id="73e55-379">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-379">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="73e55-380">mobile domain list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-380">mobile domain list *name*</span></span> |<span data-ttu-id="73e55-381">site domain list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-381">site domain list *name*</span></span> |
| <span data-ttu-id="73e55-382">mobile domain add *name* *domain*</span><span class="sxs-lookup"><span data-stu-id="73e55-382">mobile domain add *name* *domain*</span></span> |<span data-ttu-id="73e55-383">site domain add *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-383">site domain add *domain* *name*</span></span> |
| <span data-ttu-id="73e55-384">mobile domain delete *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-384">mobile domain delete *name*</span></span> |<span data-ttu-id="73e55-385">site domain delete *domain* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-385">site domain delete *domain* *name*</span></span> |
| <span data-ttu-id="73e55-386">mobile scale show *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-386">mobile scale show *name*</span></span> |<span data-ttu-id="73e55-387">site show *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-387">site show *name*</span></span> |
| <span data-ttu-id="73e55-388">mobile scale change *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-388">mobile scale change *name*</span></span> |<span data-ttu-id="73e55-389">site scale mode *mode* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-389">site scale mode *mode* *name*</span></span> <br /> <span data-ttu-id="73e55-390">site scale instances *instances* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-390">site scale instances *instances* *name*</span></span> |
| <span data-ttu-id="73e55-391">mobile appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-391">mobile appsetting list *name*</span></span> |<span data-ttu-id="73e55-392">site appsetting list *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-392">site appsetting list *name*</span></span> |
| <span data-ttu-id="73e55-393">mobile appsetting add *name* *key* *value*</span><span class="sxs-lookup"><span data-stu-id="73e55-393">mobile appsetting add *name* *key* *value*</span></span> |<span data-ttu-id="73e55-394">site appsetting add *key*=*value* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-394">site appsetting add *key*=*value* *name*</span></span> |
| <span data-ttu-id="73e55-395">mobile appsetting delete *name* *key*</span><span class="sxs-lookup"><span data-stu-id="73e55-395">mobile appsetting delete *name* *key*</span></span> |<span data-ttu-id="73e55-396">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-396">site appsetting delete *key* *name*</span></span> |
| <span data-ttu-id="73e55-397">mobile appsetting show *name* *key*</span><span class="sxs-lookup"><span data-stu-id="73e55-397">mobile appsetting show *name* *key*</span></span> |<span data-ttu-id="73e55-398">site appsetting delete *key* *name*</span><span class="sxs-lookup"><span data-stu-id="73e55-398">site appsetting delete *key* *name*</span></span> |

<span data-ttu-id="73e55-399">藉由更新適當的應用程式設定，可更新驗證或推播通知設定。</span><span class="sxs-lookup"><span data-stu-id="73e55-399">Update authentication or push notification settings by updating the appropriate Application Setting.</span></span>
<span data-ttu-id="73e55-400">請編輯檔案，並透過 ftp 或 git 發佈您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-400">Edit files and publish your site via ftp or git.</span></span>

### <span data-ttu-id="73e55-401"><a name="diagnostics"></a>診斷和記錄</span><span class="sxs-lookup"><span data-stu-id="73e55-401"><a name="diagnostics"></a>Diagnostics and Logging</span></span>
<span data-ttu-id="73e55-402">Azure App Service 通常會停用 [診斷記錄]。</span><span class="sxs-lookup"><span data-stu-id="73e55-402">Diagnostic Logging is normally disabled in an Azure App Service.</span></span>  <span data-ttu-id="73e55-403">若要啟用診斷記錄：</span><span class="sxs-lookup"><span data-stu-id="73e55-403">To enable diagnostic logging:</span></span>

1. <span data-ttu-id="73e55-404">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-404">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-405">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-405">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-406">根據預設，[設定] 刀鋒視窗隨即會開啟。</span><span class="sxs-lookup"><span data-stu-id="73e55-406">The Settings blade opens by default.</span></span>
4. <span data-ttu-id="73e55-407">選取 [功能] 功能表下的 [診斷記錄]  。</span><span class="sxs-lookup"><span data-stu-id="73e55-407">Select **Diagnostic Logs** under the FEATURES menu.</span></span>
5. <span data-ttu-id="73e55-408">對下列記錄檔按一下 [開啟]：[應用程式記錄 (檔案系統)]、[詳細錯誤訊息] 和 [失敗要求的追蹤]</span><span class="sxs-lookup"><span data-stu-id="73e55-408">Click **ON** for the following logs: **Application Logging (Filesystem)**, **Detailed error messages**, and **Failed request tracing**</span></span>
6. <span data-ttu-id="73e55-409">針對 Web 伺服器記錄，按一下 [檔案系統] </span><span class="sxs-lookup"><span data-stu-id="73e55-409">Click **File System** for Web server logging</span></span>
7. <span data-ttu-id="73e55-410">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="73e55-410">Click **Save**</span></span>

<span data-ttu-id="73e55-411">若要檢視記錄檔：</span><span class="sxs-lookup"><span data-stu-id="73e55-411">To view the logs:</span></span>

1. <span data-ttu-id="73e55-412">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="73e55-412">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="73e55-413">選取 [所有資源] 或 [應用程式服務]，然後按一下已移轉的行動應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="73e55-413">Select **All resources** or **App Services** then click the name of your migrated Mobile Service.</span></span>
3. <span data-ttu-id="73e55-414">按一下 [工具] 按鈕</span><span class="sxs-lookup"><span data-stu-id="73e55-414">Click the **Tools** button</span></span>
4. <span data-ttu-id="73e55-415">選取 [觀察] 功能表下的 [記錄資料流]  。</span><span class="sxs-lookup"><span data-stu-id="73e55-415">Select **Log Stream** under the OBSERVE menu.</span></span>

<span data-ttu-id="73e55-416">產生的記錄檔會顯示在視窗中。</span><span class="sxs-lookup"><span data-stu-id="73e55-416">Logs are displayed in the window as they are generated.</span></span>  <span data-ttu-id="73e55-417">您也可以下載的記錄檔，以便後續使用您的部署認證加以分析。</span><span class="sxs-lookup"><span data-stu-id="73e55-417">You can also download the logs for later analysis using your deployment credentials.</span></span> <span data-ttu-id="73e55-418">如需詳細資訊，請參閱[記錄]文件。</span><span class="sxs-lookup"><span data-stu-id="73e55-418">For more information, see the [Logging] documentation.</span></span>

## <span data-ttu-id="73e55-419"><a name="known-issues"></a>已知問題</span><span class="sxs-lookup"><span data-stu-id="73e55-419"><a name="known-issues"></a>Known Issues</span></span>
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a><span data-ttu-id="73e55-420">刪除移轉的行動應用程式複製會導致網站服務中斷</span><span class="sxs-lookup"><span data-stu-id="73e55-420">Deleting a Migrated Mobile App Clone causes a site outage</span></span>
<span data-ttu-id="73e55-421">如果您使用 Azure PowerShell 複製移轉的行動服務，然後又刪除此複製，則會移除生產服務的 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="73e55-421">If you clone your migrated mobile service using Azure PowerShell, then delete the clone, the DNS entry for your production service is removed.</span></span>  <span data-ttu-id="73e55-422">無法再從網際網路存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-422">Your site is no longer be accessible from the Internet.</span></span>  

<span data-ttu-id="73e55-423">解決方法︰如果您想要複製網站，請透過入口網站進行。</span><span class="sxs-lookup"><span data-stu-id="73e55-423">Resolution: If you wish to clone your site, do so through the portal.</span></span>

### <a name="changing-webconfig-does-not-work"></a><span data-ttu-id="73e55-424">變更 Web.config 並未發生作用</span><span class="sxs-lookup"><span data-stu-id="73e55-424">Changing Web.config does not work</span></span>
<span data-ttu-id="73e55-425">如果您有 ASP.NET 網站，不會套用 `Web.config` 檔案的變更。</span><span class="sxs-lookup"><span data-stu-id="73e55-425">If you have an ASP.NET site, changes to the `Web.config` file do not get applied.</span></span>  <span data-ttu-id="73e55-426">Azure App Service 會在啟動期間建置適合的 `Web.config` 檔案，以支援行動服務執行階段。</span><span class="sxs-lookup"><span data-stu-id="73e55-426">The Azure App Service builds a suitable `Web.config` file during startup to support the Mobile Services runtime.</span></span>  <span data-ttu-id="73e55-427">您可以使用 XML 轉換檔案來覆寫特定設定 (例如自訂標頭)。</span><span class="sxs-lookup"><span data-stu-id="73e55-427">You can override certain settings (such as custom headers) by using an XML transform file.</span></span>  <span data-ttu-id="73e55-428">建立名稱為 `applicationHost.xdt` 的檔案 - 這個檔案必須在 Azure 服務上的 `D:\home\site` 目錄中結束。</span><span class="sxs-lookup"><span data-stu-id="73e55-428">Create a file in called `applicationHost.xdt` - this file must end up in the `D:\home\site` directory on the Azure Service.</span></span>  <span data-ttu-id="73e55-429">透過自訂部署指令碼或直接使用 Kudu 上傳 `applicationHost.xdt` 檔案。</span><span class="sxs-lookup"><span data-stu-id="73e55-429">Upload the `applicationHost.xdt` file via a custom deployment script or directly using Kudu.</span></span>  <span data-ttu-id="73e55-430">下圖顯示範例文件：</span><span class="sxs-lookup"><span data-stu-id="73e55-430">The following shows an example document:</span></span>

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

<span data-ttu-id="73e55-431">如需詳細資訊，請參閱 GitHub 上的 [XDT 轉換範例]文件。</span><span class="sxs-lookup"><span data-stu-id="73e55-431">For more information, see the [XDT Transform Samples] documentation on GitHub.</span></span>

### <a name="migrated-mobile-services-cannot-be-added-to-traffic-manager"></a><span data-ttu-id="73e55-432">移轉的行動服務無法新增至流量管理員</span><span class="sxs-lookup"><span data-stu-id="73e55-432">Migrated Mobile Services cannot be added to Traffic Manager</span></span>
<span data-ttu-id="73e55-433">當您建立流量管理員設定檔時，無法直接選擇設定檔的移轉行動服務。</span><span class="sxs-lookup"><span data-stu-id="73e55-433">When you create a Traffic Manager profile, you cannot directly choose a migrated mobile service to the profile.</span></span>  <span data-ttu-id="73e55-434">使用「外部端點」。</span><span class="sxs-lookup"><span data-stu-id="73e55-434">Use an "external endpoint."</span></span>  <span data-ttu-id="73e55-435">外部端點只能透過 PowerShell 來新增。</span><span class="sxs-lookup"><span data-stu-id="73e55-435">The external endpoint can only be added through PowerShell.</span></span>  <span data-ttu-id="73e55-436">如需詳細資訊，請參閱[流量管理員教學課程](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="73e55-436">For more information, see the [Traffic Manager tutorial](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).</span></span>

## <span data-ttu-id="73e55-437"><a name="next-steps"></a>後續步驟</span><span class="sxs-lookup"><span data-stu-id="73e55-437"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="73e55-438">您的應用程式現在已移轉至 App Service，有更多功能可供您使用：</span><span class="sxs-lookup"><span data-stu-id="73e55-438">Now that your application is migrated to App Service, there are even more features you can use:</span></span>

* <span data-ttu-id="73e55-439">部署 [預備位置] 可讓您預備網站的變更，並執行 A/B 測試。</span><span class="sxs-lookup"><span data-stu-id="73e55-439">Deployment [staging slots] allow you to stage changes to your site and perform A/B testing.</span></span>
* <span data-ttu-id="73e55-440">[WebJobs] 可取代隨選排定作業。</span><span class="sxs-lookup"><span data-stu-id="73e55-440">[WebJobs] provide a replacement for On-demand scheduled jobs.</span></span>
* <span data-ttu-id="73e55-441">將網站連結至 GitHub、TFS 或 Mercurial，即可[連續部署]網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-441">You can [continuously deploy] your site by linking your site to GitHub, TFS, or Mercurial.</span></span>
* <span data-ttu-id="73e55-442">您可以使用 [Application Insights] 監視您的網站。</span><span class="sxs-lookup"><span data-stu-id="73e55-442">You can use [Application Insights] to monitor your site.</span></span>
* <span data-ttu-id="73e55-443">以相同的程式碼為網站和行動 API 提供服務。</span><span class="sxs-lookup"><span data-stu-id="73e55-443">Serve a website and a Mobile API from the same code.</span></span>

### <span data-ttu-id="73e55-444"><a name="upgrading-your-site"></a>將您的行動服務網站升級至 Azure Mobile Apps SDK</span><span class="sxs-lookup"><span data-stu-id="73e55-444"><a name="upgrading-your-site"></a>Upgrading your Mobile Services site to Azure Mobile Apps SDK</span></span>
* <span data-ttu-id="73e55-445">對於以 Node.js 為基礎的伺服器專案，新的 [Mobile Apps Node.js SDK] 提供多項新功能。</span><span class="sxs-lookup"><span data-stu-id="73e55-445">For Node.js-based server projects, the new [Mobile Apps Node.js SDK] provides several new features.</span></span> <span data-ttu-id="73e55-446">例如，您現在可以執行本機開發和偵錯、使用 0.10 以上的任何 Node.js 版本，以及使用任何 Express.js 中介軟體自訂。</span><span class="sxs-lookup"><span data-stu-id="73e55-446">For instance, you can now do local development and debugging, use any Node.js version above 0.10, and customize with any Express.js middleware.</span></span>
* <span data-ttu-id="73e55-447">對於以 .NET 為基礎的伺服器專案，新的 [Mobile Apps SDK NuGet 套件](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)對 NuGet 相依性有更多彈性。</span><span class="sxs-lookup"><span data-stu-id="73e55-447">For .NET-based server projects, the new [Mobile Apps SDK NuGet packages](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) have more flexibility on NuGet dependencies.</span></span>  <span data-ttu-id="73e55-448">這些套件支援新的 App Service 驗證，並以任何 ASP.NET 專案撰寫。</span><span class="sxs-lookup"><span data-stu-id="73e55-448">These packages support the new App Service authentication, and compose with any ASP.NET project.</span></span> <span data-ttu-id="73e55-449">若要深入了解升級，請參閱 [將您現有的 .NET 行動服務升級為 App Service](app-service-mobile-net-upgrading-from-mobile-services.md)。</span><span class="sxs-lookup"><span data-stu-id="73e55-449">To learn more about upgrading, see [Upgrade your existing .NET Mobile Service to App Service](app-service-mobile-net-upgrading-from-mobile-services.md).</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
<span data-ttu-id="73e55-450">[App Service 價格]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span><span class="sxs-lookup"><span data-stu-id="73e55-450">[App Service pricing]: https://azure.microsoft.com/en-us/pricing/details/app-service/</span></span>
<span data-ttu-id="73e55-451">[Application Insights]: ../application-insights/app-insights-overview.md</span><span class="sxs-lookup"><span data-stu-id="73e55-451">[Application Insights]: ../application-insights/app-insights-overview.md</span></span>
<span data-ttu-id="73e55-452">[自動調整]: ../app-service-web/web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="73e55-452">[Auto-scale]: ../app-service-web/web-sites-scale.md</span></span>
<span data-ttu-id="73e55-453">[Azure App Service]: ../app-service/app-service-value-prop-what-is.md</span><span class="sxs-lookup"><span data-stu-id="73e55-453">[Azure App Service]: ../app-service/app-service-value-prop-what-is.md</span></span>
<span data-ttu-id="73e55-454">[Azure App Service 部署文件]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="73e55-454">[Azure App Service deployment documentation]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="73e55-455">[Azure 傳統入口網站]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="73e55-455">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
<span data-ttu-id="73e55-456">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="73e55-456">[Azure portal]: https://portal.azure.com</span></span>
[Azure Region]: https://azure.microsoft.com/en-us/regions/
<span data-ttu-id="73e55-457">[Azure 排程器方案]: ../scheduler/scheduler-plans-billing.md</span><span class="sxs-lookup"><span data-stu-id="73e55-457">[Azure Scheduler Plans]: ../scheduler/scheduler-plans-billing.md</span></span>
<span data-ttu-id="73e55-458">[連續部署]: ../app-service-web/app-service-continuous-deployment.md</span><span class="sxs-lookup"><span data-stu-id="73e55-458">[continuously deploy]: ../app-service-web/app-service-continuous-deployment.md</span></span>
<span data-ttu-id="73e55-459">[轉換混合式命名空間]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/</span><span class="sxs-lookup"><span data-stu-id="73e55-459">[Convert your Mixed namespaces]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/</span></span>
[curl]: http://curl.haxx.se/
<span data-ttu-id="73e55-460">[自訂網域名稱]: ../app-service-web/web-sites-custom-domain-name.md</span><span class="sxs-lookup"><span data-stu-id="73e55-460">[custom domain names]: ../app-service-web/web-sites-custom-domain-name.md</span></span>
[Fiddler]: http://www.telerik.com/fiddler
<span data-ttu-id="73e55-461">[Azure App Service 的公開上市版]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/</span><span class="sxs-lookup"><span data-stu-id="73e55-461">[general availability of Azure App Service]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/</span></span>
<span data-ttu-id="73e55-462">[混合式連線]: ../app-service-web/web-sites-hybrid-connection-get-started.md</span><span class="sxs-lookup"><span data-stu-id="73e55-462">[Hybrid Connections]: ../app-service-web/web-sites-hybrid-connection-get-started.md</span></span>
<span data-ttu-id="73e55-463">[記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="73e55-463">[Logging]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="73e55-464">[Mobile Apps Node.js SDK]: https://github.com/azure/azure-mobile-apps-node</span><span class="sxs-lookup"><span data-stu-id="73e55-464">[Mobile Apps Node.js SDK]: https://github.com/azure/azure-mobile-apps-node</span></span>
<span data-ttu-id="73e55-465">[比較行動服務與App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="73e55-465">[Mobile Services vs. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md</span></span>
<span data-ttu-id="73e55-466">[通知中樞]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="73e55-466">[Notification Hubs]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="73e55-467">[效能監視]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="73e55-467">[performance monitoring]: ../app-service-web/web-sites-monitor.md</span></span>
[Postman]: http://www.getpostman.com/
<span data-ttu-id="73e55-468">[預備位置]: ../app-service-web/web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="73e55-468">[staging slots]: ../app-service-web/web-sites-staged-publishing.md</span></span>
<span data-ttu-id="73e55-469">[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md</span><span class="sxs-lookup"><span data-stu-id="73e55-469">[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md</span></span>
<span data-ttu-id="73e55-470">[WebJobs]: ../app-service-web/websites-webjobs-resources.md</span><span class="sxs-lookup"><span data-stu-id="73e55-470">[WebJobs]: ../app-service-web/websites-webjobs-resources.md</span></span>
<span data-ttu-id="73e55-471">[XDT 轉換範例]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples</span><span class="sxs-lookup"><span data-stu-id="73e55-471">[XDT Transform Samples]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples</span></span>
<span data-ttu-id="73e55-472">[Functions]: ../azure-functions/functions-overview.md</span><span class="sxs-lookup"><span data-stu-id="73e55-472">[Functions]: ../azure-functions/functions-overview.md</span></span>
