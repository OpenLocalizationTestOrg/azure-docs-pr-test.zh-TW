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
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>在 Azure App Service 中建立 WordPress Web 應用程式
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

本教學課程會示範 toodeploy WordPress 部落格 hello Azure Marketplace 中的站台。

當您完成 hello 教學課程中您必須註冊您的 WordPress 部落格網站和 hello 雲端中執行。

![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

您將了解：

* 如何 toofind hello Azure Marketplace 中的應用程式範本。
* 如何 toocreate Azure 應用程式中的 web 應用程式服務，根據 hello 範本。
* 如何 tooconfigure hello 新的 Azure 應用程式服務設定 web 應用程式和資料庫。

hello Azure Marketplace 提供各種不同的 Microsoft、 協力廠商和開放原始碼軟體 initiatives 所開發的熱門 web 應用程式。 hello web 應用程式上建立各種不同的受歡迎的架構，例如[PHP](/develop/nodejs/) WordPress 在本例中， [.NET](/develop/net/)， [Node.js](/develop/nodejs/)， [Java](/develop/java/)，和[Python](/develop/python/)，幾 tooname。 toocreate hello Azure Marketplace hello 只有您所需要的軟體是您用於 hello hello 瀏覽器從 web 應用程式[Azure 入口網站](https://portal.azure.com/)。 

您在本教學課程中部署的 hello WordPress 網站使用 MySQL hello 資料庫。 如果您想 hello 資料庫 tooinstead 使用 SQL Database，請參閱[專案 Nami](http://projectnami.org/)。 **專案 Nami**也會提供透過 hello Marketplace。

> [!NOTE]
> toocomplete 本教學課程中，您需要 Microsoft Azure 帳戶。 如果您沒有這類帳戶，可以[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)，或是[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。
> 
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)。 您可以於該處，在 App Service 中立即建立短期的入門 Web app - 不需信用卡，不需任何承諾。
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>選取 WordPress 和設定 Azure App Service
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 [新增] 。
   
    ![建立新的][5]
3. 搜尋 **WordPress**，然後按一下WordPress。 如果您想 toouse 而不是 MySQL 的 SQL 資料庫時，搜尋**專案 Nami**。
   
    ![WordPress 來源清單][7]
4. 閱讀 hello 描述 hello WordPress 應用程式之後, 按**建立**。
   
    ![建立](./media/web-sites-php-web-site-gallery/create.png)
5. 輸入 hello web 應用程式的名稱在 hello **Web 應用程式**方塊。
   
    此名稱必須是唯一 hello azurewebsites.net 網域中，因為 hello hello web 應用程式的 URL 將會是 {name}。 名稱是.azurewebsites.net。 如果您輸入的 hello 名稱不是唯一的會出現紅色驚嘆號 hello 文字方塊中。
6. 如果您有多個訂用帳戶，請選擇 hello 您想 toouse。 
7. 選取 [資源群組]  或建立新的資源群組。
   
    如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。
8. 選取 [App Service 方案/位置]  ，或建立新的 App Service 方案/位置。
   
    如需 App Service 方案的詳細資訊，請參閱 [Azure App Service 方案概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)    
9. 按一下**資料庫**，然後在 hello**新的 MySQL 資料庫**刀鋒視窗中提供所需的 hello 值來設定您的 MySQL 資料庫。
   
    a. 輸入新名稱，或保留 hello 預設名稱。
   
    b. 保留 hello**資料庫類型**設定得**共用**。
   
    c. 選擇的 hello hello web 應用程式的相同位置中，hello 您選擇。
   
    d. 選擇定價層。 對本教學課程來說，Mercury (允許免費使用的連線數和可用磁碟空間下限) 夠用。
10. 在 hello**新的 MySQL 資料庫**刀鋒視窗中，按一下 **確定**。 
11. 在 hello **WordPress**刀鋒視窗中，接受 hello 法律條款，然後再按一下**建立**。 
    
     ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/configure.png)
    
     Azure App Service 建立 hello web 應用程式，通常會小於一分鐘內。 您可以在 hello hello 入口網站頁面頂端的 hello 鈴鐺圖示，即可觀賞 hello 進度。
    
     ![進度指示器](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>啟動和管理 WordPress Web 應用程式
1. Hello web 應用程式建立完成時，瀏覽 hello Azure 入口網站 toohello 資源群組中建立 hello 應用程式，您可以看到 hello web 應用程式和 hello 資料庫中。
   
    hello 與 hello 燈泡圖示的額外資源是[Application Insights](/services/application-insights/)，以提供 web 應用程式監視服務。
2. 在 hello**資源群組**刀鋒視窗中，按一下 hello web 應用程式行。
   
    ![設定 Web 應用程式](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. 在 hello Web 應用程式刀鋒視窗中，按一下 **瀏覽**。
   
    ![網站 URL][browse]
4. 在 hello WordPress ** 褖畫惎**頁面上，輸入 WordPress、 所需的 hello 組態資訊，然後按一下**安裝 WordPress**。
   
    ![設定 WordPress](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. 使用您在 hello 建立 hello 認證登入** 褖畫惎**頁面。  
6. 您的網站 [儀表板] 頁面隨即開啟。    
   
    ![WordPress 網站](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>後續步驟
您已經看到如何 toocreate 和部署 PHP web 應用程式從 hello 組件庫。 如需有關在 Azure 中使用 PHP 的詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

如需有關如何 toowork 與 App Service Web 應用程式，請參閱 hello hello 頁面 （針對寬的瀏覽器視窗） 的左方 hello 連結或 hello 頁面頂端的 hello （適用於半形的瀏覽器視窗）。 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務指南 toohello 變更，請參閱[Azure App Service 以及它對現有的 Azure 服務影響](http://go.microsoft.com/fwlink/?LinkId=529714)。

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png
