---
title: "在 Azure App Service 中建立 WordPress Web 應用程式 | Microsoft Docs"
description: "了解如何使用 Azure 入口網站為 WordPress 部落格建立新的 Azure Web 應用程式。"
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
ms.openlocfilehash: 460afdabed947fb4018a9ea8a7a5bc7dc5bc89c7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a><span data-ttu-id="c4268-103">在 Azure App Service 中建立 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4268-103">Create a WordPress web app in Azure App Service</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="c4268-104">本教學課程示範如何從 Azure Marketplace 部署 WordPress 部落格網站。</span><span class="sxs-lookup"><span data-stu-id="c4268-104">This tutorial shows how to deploy a WordPress blog site from the Azure Marketplace.</span></span>

<span data-ttu-id="c4268-105">當您完成本教學課程時，您的專屬 WordPress 部落格網站將在雲端中啟動並執行中。</span><span class="sxs-lookup"><span data-stu-id="c4268-105">When you're done with the tutorial you'll have your own WordPress blog site up and running in the cloud.</span></span>

![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

<span data-ttu-id="c4268-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="c4268-107">You'll learn:</span></span>

* <span data-ttu-id="c4268-108">如何在 Azure Marketplace 尋找應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="c4268-108">How to find an application template in the Azure Marketplace.</span></span>
* <span data-ttu-id="c4268-109">如何在 Azure App Service 建立以範本為基礎的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4268-109">How to create a web app in Azure App Service that is based on the template.</span></span>
* <span data-ttu-id="c4268-110">如何為新的 Web 應用程式和資料庫設定 Azure App Service 設定。</span><span class="sxs-lookup"><span data-stu-id="c4268-110">How to configure Azure App Service settings for the new web app and database.</span></span>

<span data-ttu-id="c4268-111">Azure Marketplace 提供由 Microsoft、協力廠商公司及開放原始碼軟體計劃所開發的各種熱門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4268-111">The Azure Marketplace makes available a wide range of popular web apps developed by Microsoft, third party companies, and open source software initiatives.</span></span> <span data-ttu-id="c4268-112">Web 應用程式組建在廣泛的熱門架構上，例如本 WordPress 範例中的 [PHP](/develop/nodejs/)、[.NET](/develop/net/)、[Node.js](/develop/nodejs/)、[Java](/develop/java/) 和 [Python](/develop/python/) 等等。</span><span class="sxs-lookup"><span data-stu-id="c4268-112">The web apps are built on a wide range of popular frameworks, such as [PHP](/develop/nodejs/) in this WordPress example, [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), and [Python](/develop/python/), to name a few.</span></span> <span data-ttu-id="c4268-113">若要從 Azure Marketplace 建立 Web 應用程式，您唯一需要的軟體就是用於 [Azure 入口網站](https://portal.azure.com/)的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c4268-113">To create a web app from the Azure Marketplace the only software you need is the browser that you use for the [Azure Portal](https://portal.azure.com/).</span></span> 

<span data-ttu-id="c4268-114">您在本教學課程中部署的 WordPress 網站將 MySQL 用於資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4268-114">The WordPress site that you deploy in this tutorial uses MySQL for the database.</span></span> <span data-ttu-id="c4268-115">如果您想要改為將 SQL Database 用於資料庫，請參閱 [專案 Nami](http://projectnami.org/)。</span><span class="sxs-lookup"><span data-stu-id="c4268-115">If you wish to instead use SQL Database for the database, see [Project Nami](http://projectnami.org/).</span></span> <span data-ttu-id="c4268-116">**專案 Nami** 也可透過 Marketplace 使用。</span><span class="sxs-lookup"><span data-stu-id="c4268-116">**Project Nami** is also available through the Marketplace.</span></span>

> [!NOTE]
> <span data-ttu-id="c4268-117">若要完成此教學課程，您需要 Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4268-117">To complete this tutorial, you need a Microsoft Azure account.</span></span> <span data-ttu-id="c4268-118">如果您沒有這類帳戶，可以[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)，或是[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="c4268-118">If you don't have an account, you can [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="c4268-119">如果您想要在註冊 Azure 帳戶之前先開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="c4268-119">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="c4268-120">您可以於該處，在 App Service 中立即建立短期的入門 Web app - 不需信用卡，不需任何承諾。</span><span class="sxs-lookup"><span data-stu-id="c4268-120">There, you can immediately create a short-lived starter web app in App Service—no credit card required, and no commitments.</span></span>
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a><span data-ttu-id="c4268-121">選取 WordPress 和設定 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c4268-121">Select WordPress and configure for Azure App Service</span></span>
1. <span data-ttu-id="c4268-122">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c4268-122">Log in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4268-123">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="c4268-123">Click **New**.</span></span>
   
    ![建立新的][5]
3. <span data-ttu-id="c4268-125">搜尋 **WordPress**，然後按一下 [WordPress]。</span><span class="sxs-lookup"><span data-stu-id="c4268-125">Search for **WordPress**, and then click **WordPress**.</span></span> <span data-ttu-id="c4268-126">如果您想要使用 SQL Database，而不是 MySQL，請搜尋**專案 Nami**。</span><span class="sxs-lookup"><span data-stu-id="c4268-126">If you wish to use SQL Database instead of MySQL, search for **Project Nami**.</span></span>
   
    ![WordPress 來源清單][7]
4. <span data-ttu-id="c4268-128">在閱讀 WordPress 應用程式的描述之後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c4268-128">After reading the description of the WordPress app, click **Create**.</span></span>
   
    ![建立](./media/web-sites-php-web-site-gallery/create.png)
5. <span data-ttu-id="c4268-130">在 [Web 應用程式]  方塊中，輸入 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="c4268-130">Enter a name for the web app in the **Web app** box.</span></span>
   
    <span data-ttu-id="c4268-131">此名稱在 azurewebsites.net 網域中必須是唯一的，因為 Web 應用程式的 URL 將是 {name}.azurewebsites.net。</span><span class="sxs-lookup"><span data-stu-id="c4268-131">This name must be unique in the azurewebsites.net domain because the URL of the web app will be {name}.azurewebsites.net.</span></span> <span data-ttu-id="c4268-132">如果您輸入的名稱不是唯一的，紅色驚嘆號會出現在文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="c4268-132">If the name you enter isn't unique, a red exclamation mark appears in the text box.</span></span>
6. <span data-ttu-id="c4268-133">如果您有多個訂用帳戶，請選擇您想要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4268-133">If you have more than one subscription, choose the one you want to use.</span></span> 
7. <span data-ttu-id="c4268-134">選取 [資源群組]  或建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c4268-134">Select a **Resource Group** or create a new one.</span></span>
   
    <span data-ttu-id="c4268-135">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c4268-135">For more information about resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="c4268-136">選取 [App Service 方案/位置]  ，或建立新的 App Service 方案/位置。</span><span class="sxs-lookup"><span data-stu-id="c4268-136">Select an **App Service plan/Location** or create a new one.</span></span>
   
    <span data-ttu-id="c4268-137">如需 App Service 方案的詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="c4268-137">For more information about App Service plans, see [Azure App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span></span>    
9. <span data-ttu-id="c4268-138">按一下 [資料庫]，然後在 [新增 MySQL 資料庫] 刀鋒視窗中，提供設定 MySQL 資料庫所需的值。</span><span class="sxs-lookup"><span data-stu-id="c4268-138">Click **Database**, and then in the **New MySQL Database** blade provide the required values for configuring your MySQL database.</span></span>
   
    <span data-ttu-id="c4268-139">a.</span><span class="sxs-lookup"><span data-stu-id="c4268-139">a.</span></span> <span data-ttu-id="c4268-140">輸入新名稱或保留預設名稱。</span><span class="sxs-lookup"><span data-stu-id="c4268-140">Enter a new name or leave the default name.</span></span>
   
    <span data-ttu-id="c4268-141">b.</span><span class="sxs-lookup"><span data-stu-id="c4268-141">b.</span></span> <span data-ttu-id="c4268-142">保留設為 [共用] 的 [資料庫類型]。</span><span class="sxs-lookup"><span data-stu-id="c4268-142">Leave the **Database Type** set to **Shared**.</span></span>
   
    <span data-ttu-id="c4268-143">c.</span><span class="sxs-lookup"><span data-stu-id="c4268-143">c.</span></span> <span data-ttu-id="c4268-144">選擇與您選擇 Web 應用程式的同一位置。</span><span class="sxs-lookup"><span data-stu-id="c4268-144">Choose the same location as the one you chose for the web app.</span></span>
   
    <span data-ttu-id="c4268-145">d.</span><span class="sxs-lookup"><span data-stu-id="c4268-145">d.</span></span> <span data-ttu-id="c4268-146">選擇定價層。</span><span class="sxs-lookup"><span data-stu-id="c4268-146">Choose a pricing tier.</span></span> <span data-ttu-id="c4268-147">對本教學課程來說，Mercury (允許免費使用的連線數和可用磁碟空間下限) 夠用。</span><span class="sxs-lookup"><span data-stu-id="c4268-147">Mercury (free with minimal allowed connections and disk space) is fine for this tutorial.</span></span>
10. <span data-ttu-id="c4268-148">在 [新增 MySQL 資料庫] 刀鋒視窗中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c4268-148">In the **New MySQL Database** blade, click **OK**.</span></span> 
11. <span data-ttu-id="c4268-149">在 [WordPress] 刀鋒視窗中，接受法律條款，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="c4268-149">In the **WordPress** blade, accept the legal terms, and then click **Create**.</span></span> 
    
     ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/configure.png)
    
     <span data-ttu-id="c4268-151">Azure App Service 即會建立 Web 應用程式，通常不到一分鐘。</span><span class="sxs-lookup"><span data-stu-id="c4268-151">Azure App Service creates the web app, typically in less than a minute.</span></span> <span data-ttu-id="c4268-152">您可以按一下入口網站頁面頂端的鐘圖示查看進度。</span><span class="sxs-lookup"><span data-stu-id="c4268-152">You can watch the progress by clicking the bell icon at the top of the portal page.</span></span>
    
     ![進度指示器](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a><span data-ttu-id="c4268-154">啟動和管理 WordPress Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="c4268-154">Launch and manage your WordPress web app</span></span>
1. <span data-ttu-id="c4268-155">當您完成建立 Web 應用程式時，請在 Azure 入口網站中瀏覽至您在其中建立應用程式的資源群組，然後您就能看到 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4268-155">When the web app creation is finished, navigate in the Azure Portal to the resource group in which you created the application, and you can see the web app and the database.</span></span>
   
    <span data-ttu-id="c4268-156">具有燈泡圖示的額外資源是 [Application Insights](/services/application-insights/)，它會提供 Web 應用程式的監視服務。</span><span class="sxs-lookup"><span data-stu-id="c4268-156">The extra resource with the light bulb icon is [Application Insights](/services/application-insights/), which provides monitoring services for your web app.</span></span>
2. <span data-ttu-id="c4268-157">在 [資源群組]  刀鋒視窗中，按一下 Web 應用程式列。</span><span class="sxs-lookup"><span data-stu-id="c4268-157">In the **Resource group** blade, click the web app line.</span></span>
   
    ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. <span data-ttu-id="c4268-159">在 [Web 應用程式] 刀鋒視窗中，按一下 [瀏覽] 。</span><span class="sxs-lookup"><span data-stu-id="c4268-159">In the Web app blade, click **Browse**.</span></span>
   
    ![網站 URL][browse]
4. <span data-ttu-id="c4268-161">在 WordPress 的 [歡迎使用] 頁面中，輸入 WordPress 所需的組態資訊，然後按一下 [安裝 WordPress]。</span><span class="sxs-lookup"><span data-stu-id="c4268-161">In the WordPress **Welcome** page, enter the configuration information required by WordPress, and then click **Install WordPress**.</span></span>
   
    ![設定 WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. <span data-ttu-id="c4268-163">使用您已在 [歡迎使用]  頁面上建立的認證登入。</span><span class="sxs-lookup"><span data-stu-id="c4268-163">Log in using the credentials you created on the **Welcome** page.</span></span>  
6. <span data-ttu-id="c4268-164">您的網站 [儀表板] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c4268-164">Your site Dashboard page opens.</span></span>    
   
    ![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a><span data-ttu-id="c4268-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4268-166">Next steps</span></span>
<span data-ttu-id="c4268-167">您已了解如何從資源庫建立及部署 PHP Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c4268-167">You've seen how to create and deploy a PHP web app from the gallery.</span></span> <span data-ttu-id="c4268-168">如需在 Azure 中使用 PHP 的詳細資訊，請參閱 [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="c4268-168">For more information about using PHP in Azure, see the [PHP Developer Center](/develop/php/).</span></span>

<span data-ttu-id="c4268-169">如需如何使用 App Service Web Apps 的詳細資訊，請參閱頁面左邊上的連結 (適用於寬瀏覽器視窗) 或頁面頂端的連結 (適用於窄瀏覽器視窗)。</span><span class="sxs-lookup"><span data-stu-id="c4268-169">For more information about how to work with App Service Web Apps, see the links on the left side of the page (for wide browser windows) or at the top of the page (for narrow browser windows).</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="c4268-170">變更的項目</span><span class="sxs-lookup"><span data-stu-id="c4268-170">What's changed</span></span>
* <span data-ttu-id="c4268-171">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c4268-171">For a guide to the change from Websites to App Service, see [Azure App Service and its impact on existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
