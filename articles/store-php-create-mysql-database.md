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
# <a name="create-and-connect-tooa-mysql-database-in-azure"></a>建立及連接 tooa 在 Azure 中的 MySQL 資料庫
本教學課程告訴您如何 toocreate MySQL 資料庫在 hello [Azure 入口網站](https://portal.azure.com)(提供者是[ClearDB](http://www.cleardb.com/)) 以及 tooconnect tooit 來自 PHP web 應用程式中執行[Azure App Service](app-service/app-service-value-prop-what-is.md).

> [!NOTE]
> 您也可以建立 MySQL 資料庫做為 [Marketplace 應用程式範本](app-service-web/app-service-web-create-web-app-from-marketplace.md)的一部分。
>
>

## <a name="create-a-mysql-database-in-azure-portal"></a>在 Azure 入口網站中建立 MySQL 資料庫
toocreate hello Azure 入口網站中的 MySQL 資料庫沒有 hello 遵循：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 從 hello 左窗格中，按一下 **新增** > **資料 + 儲存體** > **MySQL 資料庫**。

    ![在 Azure 中建立 MySQL 資料庫 - 開始](./media/store-php-create-mysql-database/create-db-1-start.png)
3. 在新的 MySQL 資料庫 hello[刀鋒視窗](azure-portal-overview.md)，設定新的 MySQL 資料庫，如下所示 (*刀鋒視窗*： 水平開啟入口網站頁面):

   * **資料庫名稱**︰輸入可唯一識別的名稱
   * **訂用帳戶**： 選擇 hello 訂用帳戶 toouse
   * **資料庫類型**： 選取**共用**低成本或免費層或**專用**tooget 專用資源。
   * **資源群組**： 新增 hello MySQL 資料庫 tooan 現有[資源群組](azure-resource-manager/resource-group-overview.md)或將它放在新的。 在同一個群組可以輕鬆地管理一起 hello 的資源。
   * **位置**： 選取位置關閉 tooyou。 加入現有的資源群組的 tooan，當您鎖定的 toohello 資源群組的位置。
   * **定價層**︰按一下 定價層，然後選取定價選項 (水星 層是免費的)，然後按一下選取。
   * **法律條款**： 按一下**法律條款**，檢閱 hello 採購單詳細資料，然後按一下**購買**。
   * **Pin toodashboard**： 如果您想 tooaccess 選取它，直接從 hello 儀表板。 如果您還不熟悉入口網站瀏覽方式，這會特別有用。

     下列螢幕擷取畫面的 hello 只是一個範例的方式，您可以設定您的 MySQL 資料庫。  
     ![在 Azure 中建立 MySQL 資料庫 - 設定](./media/store-php-create-mysql-database/create-db-2-configure.png)
4. 完成設定之後，按一下 [建立] 。

    ![在 Azure 中建立 MySQL 資料庫 - 建立](./media/store-php-create-mysql-database/create-db-3-create.png)

    您會看到一則告訴您已開始部署的快顯通知。

    ![在 Azure 中建立 MySQL 資料庫 - 進行中](./media/store-php-create-mysql-database/create-db-4-started-status.png)

    部署成功之後，您會看到另一則快顯通知。 hello 入口網站也會自動開啟您的 MySQL 資料庫刀鋒視窗。

<a name="connect"></a>

## <a name="connect-tooyour-mysql-database"></a>連接 tooyour MySQL 資料庫
toosee hello 連接資訊，為您新的 MySQL 資料庫，只要按一下**屬性**在您的 web 應用程式 刀鋒視窗。

![在 Azure 中建立 MySQL 資料庫 - MySQL 資料庫刀鋒視窗](./media/store-php-create-mysql-database/create-db-5-finished-db-blade.png)

您現在已可以在任何 Web 應用程式中使用該連接資訊。 顯示 toouse hello 連接資訊，從簡單的 PHP 應用程式可以使用範例[這裡](https://github.com/WindowsAzure/azure-sdk-for-php-samples/tree/master/tasklist-mysql)。

## <a name="connect-a-laravel-web-app-from-hello-php-get-started-tutorial"></a>連接 Laravel web 應用程式 （從 hello PHP get 入門教學課程）
假設您剛完成的 hello 教學課程[建立、 設定和部署 PHP web 應用程式 tooAzure](app-service-web/app-service-web-php-get-started.md) ，而且有[Laravel](https://www.laravel.com/)在 Azure 中執行的 web 應用程式。 您可以輕鬆地新增資料庫功能 tooyour Laravel 應用程式。 只要遵循 hello 執行下列步驟：

> [!NOTE]
> hello 下列步驟假設您已完成 hello 教學課程[建立、 設定和部署 PHP web 應用程式 tooAzure](app-service-web/app-service-web-php-get-started.md)。
>
>

1. 設定在本機開發環境 toopoint toohello MySQL 資料庫中的 hello Laravel 應用程式。 toodo，開啟`.env`從 Laravel 應用程式的根目錄，並設定 hello MySQL 資料庫選項。

        DB_CONNECTION=mysql
        DB_HOST=<HOSTNAME_from_properties_blade>
        DB_PORT=<PORT_from_properties_blade>
        DB_DATABASE=<see_note_below>
        DB_USERNAME=<USERNAME_from_properties_blade>
        DB_PASSWORD=<PASSWORD_from_properties_blade>

   > [!NOTE]
   > 在 hello**屬性**刀鋒視窗中，您的 MySQL 資料庫 hello 名稱可能或中可能不其中一個 hello 顯示 hello**資料庫名稱**欄位。 這是較佳 toocheck hello 資料庫參數，在 hello**連接字串**欄位。    
   >
   > ![在 Azure 中建立 MySQL 資料庫 - 進行中](./media/store-php-create-mysql-database/connect-db-1-database-name.png)
   >
   >
2. hello 您現在可以 MySQL 存取的最快速方式 tooverify 是 toouse [Laravel 的預設驗證 scaffolding](https://laravel.com/docs/5.2/authentication#authentication-quickstart)。
   在命令列終端機 hello，執行 hello Laravel 應用程式的根目錄中的下列命令：

         php artisan migrate
         php artisan make:auth

    hello 第一個命令會根據預先定義的移轉中 hello Azure 中建立 hello 資料表`database/migrations`目錄和 hello scaffold hello 基本的檢視和使用者註冊和驗證路由的第二個命令。
3. 現在就執行 hello 程式開發伺服器：

        php artisan serve
4. 在 hello 瀏覽器瀏覽 toohttp://localhost:8000 並註冊新的使用者，如所示：

    ![連接 Azure 中的 tooMySQL 資料庫-註冊使用者](./media/store-php-create-mysql-database/connect-db-2-development-server.png)

    請遵循 hello UI 提示完成 hello 註冊。 完成註冊之後，系統會您將登入。

    ![連接 Azure 中的 tooMySQL 資料庫-註冊使用者](./media/store-php-create-mysql-database/connect-db-3-registered-user.png)

    您現在正在開發您的應用程式，針對在 Azure 中的 hello MySQL 資料庫。
5. 現在，您只需要 tooreplicate 您`.env`設定 tooyour Azure web 應用程式。 執行下列 Azure CLI 命令的 hello:

        azure site appsetting add DB_CONNECTION=mysql
        azure site appsetting add DB_HOST=<HOSTNAME_from_properties_blade>
        azure site appsetting add DB_PORT=<PORT_from_properties_blade>
        azure site appsetting add DB_DATABASE=<Database_param_from_CONNECTION_INFO_from_properties_blade>
        azure site appsetting add DB_USERNAME=<USERNAME_from_properties_blade>
        azure site appsetting add DB_PASSWORD=<PASSWORD_from_properties_blade>

6. 接下來，認可並推送 tooAzure hello 本機變更先前執行時進行`php artisan make:auth`。

        git add .
        git commit -m "scaffold auth views and routes"
        git push azure master
7. 瀏覽 toohello Azure web 應用程式。

        azure site browse
8. 使用您稍早建立的 hello 使用者認證登入。

    ![連接 Azure 中的 tooMySQL 資料庫-瀏覽 tooAzure web 應用程式](./media/store-php-create-mysql-database/connect-db-4-browse-azure-webapp.png)

    登入之後，您應該會看到 hello 易記後的登入畫面。

    ![連接 Azure-記錄在 tooMySQL 資料庫](./media/store-php-create-mysql-database/connect-db-5-logged-in.png)

    恭喜您，您在 Azure 中的 PHP Web 應用程式現在已在從 MySQL 資料庫存取資料。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。
