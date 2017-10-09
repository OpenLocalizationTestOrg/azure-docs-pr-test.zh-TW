---
title: "aaaCreate 和連接 tooa 在 Azure 中的 MySQL 資料庫"
description: "了解如何 toouse hello Azure 入口網站 toocreate MySQL 資料庫，然後從在 Azure 中的 PHP web 應用程式連接 tooit。"
documentationcenter: php
services: app-service\web
author: cephalin
manager: erikre
editor: 
tags: mysql
ms.assetid: 55465a9a-7e65-4fd9-8a65-dd83ee41f3e5
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm;cephalin
ms.openlocfilehash: 3abc02f8887432625666afd847e9dc0c0a4db2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a><span data-ttu-id="86c4b-103">建立及連接 tooa 在 Azure 中的 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="86c4b-103">Create and connect tooa MySQL database in Azure</span></span>
<span data-ttu-id="86c4b-104">本教學課程告訴您如何 toocreate MySQL 資料庫在 hello [Azure 入口網站](https://portal.azure.com)(提供者是[ClearDB](http://www.cleardb.com/)) 以及 tooconnect tooit 來自 PHP web 應用程式中執行[Azure App Service](app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="86c4b-104">This tutorial shows you how toocreate a MySQL database in hello [Azure portal](https://portal.azure.com) (provider is [ClearDB](http://www.cleardb.com/)) and how tooconnect tooit from a PHP web app running in [Azure App Service](app-service/app-service-value-prop-what-is.md).</span></span>

> [!NOTE]
> <span data-ttu-id="86c4b-105">您也可以建立 MySQL 資料庫做為 [Marketplace 應用程式範本](app-service-web/app-service-web-create-web-app-from-marketplace.md)的一部分。</span><span class="sxs-lookup"><span data-stu-id="86c4b-105">You can also create a MySQL database as part of a [Marketplace app template](app-service-web/app-service-web-create-web-app-from-marketplace.md).</span></span>
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a><span data-ttu-id="86c4b-106">在 Azure 入口網站中建立 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="86c4b-106">Create a MySQL database in Azure portal</span></span>
<span data-ttu-id="86c4b-107">toocreate hello Azure 入口網站中的 MySQL 資料庫沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="86c4b-107">toocreate a MySQL database in hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="86c4b-108">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="86c4b-108">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="86c4b-109">從 hello 左窗格中，按一下 **新增** > **資料 + 儲存體** > **MySQL 資料庫**。</span><span class="sxs-lookup"><span data-stu-id="86c4b-109">From hello left menu, click **New** > **Data + Storage** > **MySQL Database**.</span></span>

    ![在 Azure 中建立 MySQL 資料庫 - 開始](./media/store-php-create-mysql-database/create-db-1-start.png)
3. <span data-ttu-id="86c4b-111">在新的 MySQL 資料庫 hello[刀鋒視窗](azure-portal-overview.md)，設定新的 MySQL 資料庫，如下所示 (*刀鋒視窗*： 水平開啟入口網站頁面):</span><span class="sxs-lookup"><span data-stu-id="86c4b-111">In hello New MySQL Database [blade](azure-portal-overview.md), configure your new MySQL database as follows (*blade*: a portal page that opens horizontally):</span></span>

   * <span data-ttu-id="86c4b-112">**資料庫名稱**︰輸入可唯一識別的名稱</span><span class="sxs-lookup"><span data-stu-id="86c4b-112">**Database Name**: Type a uniquely identifiable name</span></span>
   * <span data-ttu-id="86c4b-113">**訂用帳戶**： 選擇 hello 訂用帳戶 toouse</span><span class="sxs-lookup"><span data-stu-id="86c4b-113">**Subscription**: Choose hello subscription toouse</span></span>
   * <span data-ttu-id="86c4b-114">**資料庫類型**： 選取**共用**低成本或免費層或**專用**tooget 專用資源。</span><span class="sxs-lookup"><span data-stu-id="86c4b-114">**Database Type**: Select **Shared** for low-cost or free tiers, or **Dedicated** tooget dedicated resources.</span></span>
   * <span data-ttu-id="86c4b-115">**資源群組**： 新增 hello MySQL 資料庫 tooan 現有[資源群組](azure-resource-manager/resource-group-overview.md)或將它放在新的。</span><span class="sxs-lookup"><span data-stu-id="86c4b-115">**Resource group**: Add hello MySQL database tooan existing [resource group](azure-resource-manager/resource-group-overview.md) or put it in a new one.</span></span> <span data-ttu-id="86c4b-116">在同一個群組可以輕鬆地管理一起 hello 的資源。</span><span class="sxs-lookup"><span data-stu-id="86c4b-116">Resources in hello same group can be easily managed together.</span></span>
   * <span data-ttu-id="86c4b-117">**位置**： 選取位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="86c4b-117">**Location**: Select a location close tooyou.</span></span> <span data-ttu-id="86c4b-118">加入現有的資源群組的 tooan，當您鎖定的 toohello 資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="86c4b-118">When adding tooan existing resource group, you're locked toohello resource group's location.</span></span>
   * <span data-ttu-id="86c4b-119">**定價層**︰按一下 定價層，然後選取定價選項 (水星 層是免費的)，然後按一下選取。</span><span class="sxs-lookup"><span data-stu-id="86c4b-119">**Pricing Tier**: Click **Pricing Tier**, then select a pricing option (**Mercury** tier is free), and then click **Select**.</span></span>
   * <span data-ttu-id="86c4b-120">**法律條款**： 按一下**法律條款**，檢閱 hello 採購單詳細資料，然後按一下**購買**。</span><span class="sxs-lookup"><span data-stu-id="86c4b-120">**Legal Terms**: Click **Legal Terms**, review hello purchase details, and click **Purchase**.</span></span>
   * <span data-ttu-id="86c4b-121">**Pin toodashboard**： 如果您想 tooaccess 選取它，直接從 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="86c4b-121">**Pin toodashboard**: Select if you want tooaccess it directly from hello dashboard.</span></span> <span data-ttu-id="86c4b-122">如果您還不熟悉入口網站瀏覽方式，這會特別有用。</span><span class="sxs-lookup"><span data-stu-id="86c4b-122">This is especially helpful if you aren't familiar with portal navigation yet.</span></span>

     <span data-ttu-id="86c4b-123">下列螢幕擷取畫面的 hello 只是一個範例的方式，您可以設定您的 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="86c4b-123">hello following screenshot is just an example of how you can configure your MySQL database.</span></span>  
     ![在 Azure 中建立 MySQL 資料庫 - 設定](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. <span data-ttu-id="86c4b-125">完成設定之後，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="86c4b-125">When you're done configuring, click **Create**.</span></span>

    ![在 Azure 中建立 MySQL 資料庫 - 建立](./media/store-php-create-mysql-database/create-db-3-create.png)

    <span data-ttu-id="86c4b-127">您會看到一則告訴您已開始部署的快顯通知。</span><span class="sxs-lookup"><span data-stu-id="86c4b-127">You will see a pop-up notification letting you know that deployment has started.</span></span>

    ![在 Azure 中建立 MySQL 資料庫 - 進行中](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    <span data-ttu-id="86c4b-129">部署成功之後，您會看到另一則快顯通知。</span><span class="sxs-lookup"><span data-stu-id="86c4b-129">You will get another pop-up once deployment has succeeded.</span></span> <span data-ttu-id="86c4b-130">hello 入口網站也會自動開啟您的 MySQL 資料庫刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86c4b-130">hello portal will also open your MySQL database blade automatically.</span></span>

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a><span data-ttu-id="86c4b-131">連接 tooyour MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="86c4b-131">Connect tooyour MySQL database</span></span>
<span data-ttu-id="86c4b-132">toosee hello 連接資訊，為您新的 MySQL 資料庫，只要按一下**屬性**在您的 web 應用程式 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="86c4b-132">toosee hello connection information for your new MySQL database, just click **Properties** in your web app's blade.</span></span>

![在 Azure 中建立 MySQL 資料庫 - MySQL 資料庫刀鋒視窗](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

<span data-ttu-id="86c4b-134">您現在已可以在任何 Web 應用程式中使用該連接資訊。</span><span class="sxs-lookup"><span data-stu-id="86c4b-134">You can now use that connection information in any web app.</span></span> <span data-ttu-id="86c4b-135">顯示 toouse hello 連接資訊，從簡單的 PHP 應用程式可以使用範例[這裡](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)。</span><span class="sxs-lookup"><span data-stu-id="86c4b-135">A sample that shows how toouse hello connection information from a simple PHP app is available [here](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql).</span></span>

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a><span data-ttu-id="86c4b-136">連接 Laravel web 應用程式 （從 hello PHP get 入門教學課程）</span><span class="sxs-lookup"><span data-stu-id="86c4b-136">Connect a Laravel web app (from hello PHP get started tutorial)</span></span>
<span data-ttu-id="86c4b-137">假設您剛完成的 hello 教學課程[建立、 設定和部署 PHP web 應用程式 tooAzure](app-service-web/app-service-web-php-get-started.md) ，而且有[Laravel](https://www.laravel.com/)在 Azure 中執行的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86c4b-137">Suppose you just finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md) and have a [Laravel](https://www.laravel.com/) web app running in Azure.</span></span> <span data-ttu-id="86c4b-138">您可以輕鬆地新增資料庫功能 tooyour Laravel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86c4b-138">You can easily add database capabilities tooyour Laravel app.</span></span> <span data-ttu-id="86c4b-139">只要遵循 hello 執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="86c4b-139">Just follow hello steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="86c4b-140">hello 下列步驟假設您已完成 hello 教學課程[建立、 設定和部署 PHP web 應用程式 tooAzure](app-service-web/app-service-web-php-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="86c4b-140">hello following steps assume that you have finished hello tutorial [Create, configure, and deploy a PHP web app tooAzure](app-service-web/app-service-web-php-get-started.md).</span></span>
>
>

1. <span data-ttu-id="86c4b-141">設定在本機開發環境 toopoint toohello MySQL 資料庫中的 hello Laravel 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86c4b-141">Configure hello Laravel app in your local development environment toopoint toohello MySQL database.</span></span> <span data-ttu-id="86c4b-142">toodo，開啟`.env`從 Laravel 應用程式的根目錄，並設定 hello MySQL 資料庫選項。</span><span class="sxs-lookup"><span data-stu-id="86c4b-142">toodo this, open `.env` from your Laravel app's root directory and configure hello MySQL database options.</span></span>

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > <span data-ttu-id="86c4b-143">在 hello**屬性**刀鋒視窗中，您的 MySQL 資料庫 hello 名稱可能或中可能不其中一個 hello 顯示 hello**資料庫名稱**欄位。</span><span class="sxs-lookup"><span data-stu-id="86c4b-143">In hello **Properties** blade, hello name of your MySQL database may or may not be hello one shown in hello **DATABASE NAME** field.</span></span> <span data-ttu-id="86c4b-144">這是較佳 toocheck hello 資料庫參數，在 hello**連接字串**欄位。</span><span class="sxs-lookup"><span data-stu-id="86c4b-144">It's better toocheck hello Database parameter in hello **CONNECTION STRING** field.</span></span>    
   >
   > ![在 Azure 中建立 MySQL 資料庫 - 進行中](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. <span data-ttu-id="86c4b-146">hello 您現在可以 MySQL 存取的最快速方式 tooverify 是 toouse [Laravel 的預設驗證 scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart)。</span><span class="sxs-lookup"><span data-stu-id="86c4b-146">hello quickest way tooverify that you have MySQL access now is toouse [Laravel's default authentication scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart).</span></span>
   <span data-ttu-id="86c4b-147">在命令列終端機 hello，執行 hello Laravel 應用程式的根目錄中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="86c4b-147">In hello command-line terminal, run hello following commands from your Laravel app's root directory:</span></span>

         php artisan migrate
         php artisan make:auth

    <span data-ttu-id="86c4b-148">hello 第一個命令會根據預先定義的移轉中 hello Azure 中建立 hello 資料表`database/migrations`目錄和 hello scaffold hello 基本的檢視和使用者註冊和驗證路由的第二個命令。</span><span class="sxs-lookup"><span data-stu-id="86c4b-148">hello first command creates hello tables in Azure based on predefined migrations in hello `database/migrations` directory, and hello second  command scaffolds hello basic views and routes for user registration and authentication.</span></span>
3. <span data-ttu-id="86c4b-149">現在就執行 hello 程式開發伺服器：</span><span class="sxs-lookup"><span data-stu-id="86c4b-149">Run hello development server now:</span></span>

        php artisan serve
4. <span data-ttu-id="86c4b-150">在 hello 瀏覽器瀏覽 toohttp://localhost:8000 並註冊新的使用者，如所示：</span><span class="sxs-lookup"><span data-stu-id="86c4b-150">In hello browser, navigate toohttp://localhost:8000 and register a new user as shown:</span></span>

    ![連接 Azure 中的 tooMySQL 資料庫-註冊使用者](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    <span data-ttu-id="86c4b-152">請遵循 hello UI 提示完成 hello 註冊。</span><span class="sxs-lookup"><span data-stu-id="86c4b-152">Follow hello UI prompt complete hello registration.</span></span> <span data-ttu-id="86c4b-153">完成註冊之後，系統會您將登入。</span><span class="sxs-lookup"><span data-stu-id="86c4b-153">Once registration completes, you will be logged in.</span></span>

    ![連接 Azure 中的 tooMySQL 資料庫-註冊使用者](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    <span data-ttu-id="86c4b-155">您現在正在開發您的應用程式，針對在 Azure 中的 hello MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="86c4b-155">You are now developing your app against hello MySQL database in Azure.</span></span>
5. <span data-ttu-id="86c4b-156">現在，您只需要 tooreplicate 您`.env`設定 tooyour Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86c4b-156">Now, you just need tooreplicate your `.env` settings tooyour Azure web app.</span></span> <span data-ttu-id="86c4b-157">執行下列 Azure CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="86c4b-157">Run hello following Azure CLI commands:</span></span>

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. <span data-ttu-id="86c4b-158">接下來，認可並推送 tooAzure hello 本機變更先前執行時進行`php artisan make:auth`。</span><span class="sxs-lookup"><span data-stu-id="86c4b-158">Next, commit and push tooAzure hello local changes made earlier while running `php artisan make:auth`.</span></span>

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. <span data-ttu-id="86c4b-159">瀏覽 toohello Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="86c4b-159">Browse toohello Azure web app.</span></span>

        azure site browse
8. <span data-ttu-id="86c4b-160">使用您稍早建立的 hello 使用者認證登入。</span><span class="sxs-lookup"><span data-stu-id="86c4b-160">Log in using hello user credentials you created earlier.</span></span>

    ![連接 Azure 中的 tooMySQL 資料庫-瀏覽 tooAzure web 應用程式](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    <span data-ttu-id="86c4b-162">登入之後，您應該會看到 hello 易記後的登入畫面。</span><span class="sxs-lookup"><span data-stu-id="86c4b-162">After you log in, you should see hello friendly post-login screen.</span></span>

    ![連接 Azure-記錄在 tooMySQL 資料庫](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    <span data-ttu-id="86c4b-164">恭喜您，您在 Azure 中的 PHP Web 應用程式現在已在從 MySQL 資料庫存取資料。</span><span class="sxs-lookup"><span data-stu-id="86c4b-164">Congratulations, your PHP web app in Azure is now accessing data from your MySQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c4b-165">後續步驟</span><span class="sxs-lookup"><span data-stu-id="86c4b-165">Next steps</span></span>
<span data-ttu-id="86c4b-166">如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。</span><span class="sxs-lookup"><span data-stu-id="86c4b-166">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>
