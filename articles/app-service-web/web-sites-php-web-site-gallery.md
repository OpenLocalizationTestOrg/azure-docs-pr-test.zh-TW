---
title: "aaaCreate WordPress web 應用程式在 Azure App Service 中 |Microsoft 文件"
description: "了解如何 toocreate 新的 Azure web 應用程式使用 Azure 入口網站 hello WordPress 部落格。"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="0ed54-103">在 Azure App Service 中建立 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ed54-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="0ed54-104">本教學課程會示範 toodeploy WordPress 部落格 hello Azure Marketplace 中的站台。</span><span class="sxs-lookup"><span data-stu-id="0ed54-104">This tutorial shows how toodeploy a WordPress blog site from hello Azure Marketplace.</span></span>

<span data-ttu-id="0ed54-105">當您完成 hello 教學課程中您必須註冊您的 WordPress 部落格網站和 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="0ed54-105">When you're done with hello tutorial you'll have your own WordPress blog site up and running in hello cloud.</span></span>

![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="0ed54-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="0ed54-107">You'll learn:</span></span>

* <span data-ttu-id="0ed54-108">如何 toofind hello Azure Marketplace 中的應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="0ed54-108">How toofind an application template in hello Azure Marketplace.</span></span>
* <span data-ttu-id="0ed54-109">如何 toocreate Azure 應用程式中的 web 應用程式服務，根據 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="0ed54-109">How toocreate a web app in Azure App Service that is based on hello template.</span></span>
* <span data-ttu-id="0ed54-110">如何 tooconfigure hello 新的 Azure 應用程式服務設定 web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="0ed54-110">How tooconfigure Azure App Service settings for hello new web app and database.</span></span>

<span data-ttu-id="0ed54-111">hello Azure Marketplace 提供各種不同的 Microsoft、 協力廠商和開放原始碼軟體 initiatives 所開發的熱門 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0ed54-111">hello Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="0ed54-112">hello web 應用程式上建立各種不同的受歡迎的架構，例如[PHP](/develop/nodejs/) WordPress 在本例中， [.NET](/develop/net/)， [Node.js](/develop/nodejs/)， [Java](/develop/java/)，和[Python](/develop/python/)，幾 tooname。</span><span class="sxs-lookup"><span data-stu-id="0ed54-112">hello web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), tooname a few.</span></span> <span data-ttu-id="0ed54-113">toocreate hello Azure Marketplace hello 只有您所需要的軟體是您用於 hello hello 瀏覽器從 web 應用程式[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-113">toocreate a web app from hello Azure Marketplace hello only software you need is hello browser that you use for hello [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="0ed54-114">您在本教學課程中部署的 hello WordPress 網站使用 MySQL hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0ed54-114">hello WordPress site that you deploy in this tutorial uses MySQL for hello database.</span></span> <span data-ttu-id="0ed54-115">如果您想 hello 資料庫 tooinstead 使用 SQL Database，請參閱[專案 Nami](http://projectnami.org/)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-115">If you wish tooinstead use SQL Database for hello database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="0ed54-116">**專案 Nami**也會提供透過 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="0ed54-116">**Project Nami** is also available through hello Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="0ed54-117">toocomplete 本教學課程中，您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0ed54-117">toocomplete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="0ed54-118">如果您沒有這類帳戶，可以[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)，或是[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="0ed54-119">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-119">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="0ed54-120">您可以於該處，在 App Service 中立即建立短期的入門 Web app - 不需信用卡，不需任何承諾。</span><span class="sxs-lookup"><span data-stu-id="0ed54-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="0ed54-121">選取 WordPress 和設定 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0ed54-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="0ed54-122">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-122">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0ed54-123">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="0ed54-123">Click **New**.</span></span>
   
    ![建立新的][5]
3. <span data-ttu-id="0ed54-125">搜尋 **WordPress**，然後按一下WordPress。</span><span class="sxs-lookup"><span data-stu-id="0ed54-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="0ed54-126">如果您想 toouse 而不是 MySQL 的 SQL 資料庫時，搜尋**專案 Nami**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-126">If you wish toouse SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress 來源清單][7]
4. <span data-ttu-id="0ed54-128">閱讀 hello 描述 hello WordPress 應用程式之後, 按**建立**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-128">After reading hello description of hello WordPress app, click **Create**.</span></span>
   
    ![建立](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="0ed54-130">輸入 hello web 應用程式的名稱在 hello **Web 應用程式**方塊。</span><span class="sxs-lookup"><span data-stu-id="0ed54-130">Enter a name for hello web app in hello **Web app** box.</span></span>
   
    <span data-ttu-id="0ed54-131">此名稱必須是唯一 hello azurewebsites.net 網域中，因為 hello hello web 應用程式的 URL 將會是 {name}。 名稱是.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="0ed54-131">This name must be unique in hello azurewebsites.net domain because hello URL of hello web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="0ed54-132">如果您輸入的 hello 名稱不是唯一的會出現紅色驚嘆號 hello 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="0ed54-132">If hello name you enter isn't unique, a red exclamation mark appears in hello text box.</span></span>
6. <span data-ttu-id="0ed54-133">如果您有多個訂用帳戶，請選擇 hello 您想 toouse。</span><span class="sxs-lookup"><span data-stu-id="0ed54-133">If you have more than one subscription, choose hello one you want toouse.</span></span> 
7. <span data-ttu-id="0ed54-134">選取 [資源群組]  或建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ed54-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="0ed54-135">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="0ed54-136">選取 [App Service 方案/位置]  ，或建立新的 App Service 方案/位置。</span><span class="sxs-lookup"><span data-stu-id="0ed54-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="0ed54-137">如需 App Service 方案的詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0ed54-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="0ed54-138">按一下**資料庫**，然後在 hello**新的 MySQL 資料庫**刀鋒視窗中提供所需的 hello 值來設定您的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0ed54-138">Click **Database**, and then in hello **New MySQL Database** blade provide hello required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="0ed54-139">a.</span><span class="sxs-lookup"><span data-stu-id="0ed54-139">a.</span></span> <span data-ttu-id="0ed54-140">輸入新名稱，或保留 hello 預設名稱。</span><span class="sxs-lookup"><span data-stu-id="0ed54-140">Enter a new name or leave hello default name.</span></span>
   
    <span data-ttu-id="0ed54-141">b.</span><span class="sxs-lookup"><span data-stu-id="0ed54-141">b.</span></span> <span data-ttu-id="0ed54-142">保留 hello**資料庫類型**設定得**共用**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-142">Leave hello **Database Type** set too**Shared**.</span></span>
   
    <span data-ttu-id="0ed54-143">c.</span><span class="sxs-lookup"><span data-stu-id="0ed54-143">c.</span></span> <span data-ttu-id="0ed54-144">選擇的 hello hello web 應用程式的相同位置中，hello 您選擇。</span><span class="sxs-lookup"><span data-stu-id="0ed54-144">Choose hello same location as hello one you chose for hello web app.</span></span>
   
    <span data-ttu-id="0ed54-145">d.</span><span class="sxs-lookup"><span data-stu-id="0ed54-145">d.</span></span> <span data-ttu-id="0ed54-146">選擇定價層。</span><span class="sxs-lookup"><span data-stu-id="0ed54-146">Choose a pricing tier.</span></span> <span data-ttu-id="0ed54-147">對本教學課程來說，Mercury (允許免費使用的連線數和可用磁碟空間下限) 夠用。</span><span class="sxs-lookup"><span data-stu-id="0ed54-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="0ed54-148">在 hello**新的 MySQL 資料庫**刀鋒視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-148">In hello **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="0ed54-149">在 hello **WordPress**刀鋒視窗中，接受 hello 法律條款，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-149">In hello **WordPress** blade, accept hello legal terms, and then click **Create**.</span></span> 
    
     ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="0ed54-151">Azure App Service 建立 hello web 應用程式，通常會小於一分鐘內。</span><span class="sxs-lookup"><span data-stu-id="0ed54-151">Azure App Service creates hello web app, typically in less than a minute.</span></span> <span data-ttu-id="0ed54-152">您可以在 hello hello 入口網站頁面頂端的 hello 鈴鐺圖示，即可觀賞 hello 進度。</span><span class="sxs-lookup"><span data-stu-id="0ed54-152">You can watch hello progress by clicking hello bell icon at hello top of hello portal page.</span></span>
    
     ![進度指示器](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="0ed54-154">啟動和管理 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0ed54-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="0ed54-155">Hello web 應用程式建立完成時，瀏覽 hello Azure 入口網站 toohello 資源群組中建立 hello 應用程式，您可以看到 hello web 應用程式和 hello 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="0ed54-155">When hello web app creation is finished, navigate in hello Azure Portal toohello resource group in which you created hello application, and you can see hello web app and hello database.</span></span>
   
    <span data-ttu-id="0ed54-156">hello 與 hello 燈泡圖示的額外資源是[Application Insights](/services/application-insights/)，以提供 web 應用程式監視服務。</span><span class="sxs-lookup"><span data-stu-id="0ed54-156">hello extra resource with hello light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="0ed54-157">在 hello**資源群組**刀鋒視窗中，按一下 hello web 應用程式行。</span><span class="sxs-lookup"><span data-stu-id="0ed54-157">In hello **Resource group** blade, click hello web app line.</span></span>
   
    ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="0ed54-159">在 hello Web 應用程式刀鋒視窗中，按一下 **瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-159">In hello Web app blade, click **Browse**.</span></span>
   
    ![網站 URL][browse]
4. <span data-ttu-id="0ed54-161">在 hello WordPress ** 褖畫惎**頁面上，輸入 WordPress、 所需的 hello 組態資訊，然後按一下**安裝 WordPress**。</span><span class="sxs-lookup"><span data-stu-id="0ed54-161">In hello WordPress **Welcome** page, enter hello configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![設定 WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="0ed54-163">使用您在 hello 建立 hello 認證登入** 褖畫惎**頁面。</span><span class="sxs-lookup"><span data-stu-id="0ed54-163">Log in using hello credentials you created on hello **Welcome** page.</span></span>  
6. <span data-ttu-id="0ed54-164">您的網站 [儀表板] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0ed54-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="0ed54-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ed54-166">Next steps</span></span>
<span data-ttu-id="0ed54-167">您已經看到如何 toocreate 和部署 PHP web 應用程式從 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="0ed54-167">You've seen how toocreate and deploy a PHP web app from hello gallery.</span></span> <span data-ttu-id="0ed54-168">如需有關在 Azure 中使用 PHP 的詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-168">For more information about using PHP in Azure, see hello [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="0ed54-169">如需有關如何 toowork 與 App Service Web 應用程式，請參閱 hello hello 頁面 （針對寬的瀏覽器視窗） 的左方 hello 連結或 hello 頁面頂端的 hello （適用於半形的瀏覽器視窗）。</span><span class="sxs-lookup"><span data-stu-id="0ed54-169">For more information about how toowork with App Service Web Apps, see hello links on hello left side of hello page (for wide browser windows) or at hello top of hello page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="0ed54-170">變更的項目</span><span class="sxs-lookup"><span data-stu-id="0ed54-170">What's changed</span></span>
* <span data-ttu-id="0ed54-171">從網站 tooApp 服務指南 toohello 變更，請參閱[Azure App Service 以及它對現有的 Azure 服務影響](http://go.microsoft.com/fwlink/?LinkId=529714)。</span><span class="sxs-lookup"><span data-stu-id="0ed54-171">For a guide toohello change from Websites tooApp Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
