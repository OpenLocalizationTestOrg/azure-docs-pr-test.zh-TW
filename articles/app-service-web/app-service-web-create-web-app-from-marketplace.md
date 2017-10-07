---
title: "aaaCreate web 應用程式從 hello Azure Marketplace |Microsoft 文件"
description: "了解如何從 hello Azure Marketplace 使用的新 WordPress web 應用程式 toocreate hello Azure 入口網站。"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>建立 web 應用程式從 hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

hello Azure Marketplace 提供各種不同的開放原始碼軟體社群，例如 WordPress 和 Umbraco CMS 所開發的熱門 web 應用程式。 在此教學課程中，您學會如何從 Azure marketplace 所提供的 toocreate WordPress 應用程式。
這會建立 Azure Web 應用程式和 MySQL 資料庫。 

![WordPress Web 應用程式儀表板範例](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>開始之前 

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

## <a name="deploy-from-azure-marketplace"></a>從 Azure Marketplace 進行部署
從 Azure Marketplace，請遵循以下 toodeploy WordPress 的 hello 步驟。

### <a name="sign-in-tooazure"></a>登入 tooAzure
登入 toohello [Azure 入口網站](https://portal.azure.com)。

### <a name="deploy-wordpress-template"></a>部署 WordPress 範本
hello Azure Marketplace 提供的範本設定資源，安裝程式 hello [WordPress](https://portal.azure.com/#create/WordPress.WordPress)範本 tooget 啟動。
   
輸入 hello 下列資訊 toodeploy hello WordPress 應用程式和其資源。

  ![WordPress 建立流程](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| 欄位         | 建議的值           | 說明  |
| ------------- |-------------------------|-------------|
| 應用程式名稱      | mywordpressapp          | 為您的 **Web 應用程式名稱**輸入唯一的應用程式名稱。 這個名稱會當做 hello 預設應用程式的 DNS 名稱的一部分`<app_name>.azurewebsites.net`，所以它需要 toobe 唯一跨 Azure 中的所有應用程式。 公開 tooyour 使用者之前，您可以稍後對應的自訂網域名稱 tooyour 應用程式 |
| 訂用帳戶  | Pay-As-You-Go             | 選取 [訂用帳戶] 。 如果您有多個訂閱，請選擇 hello 適當的訂用帳戶。 |
| 資源群組| mywordpressappgroup                 |    輸入**資源群組**。 資源群組是一個邏輯容器，可在其中部署與管理 Azure 資源 (例如 Web Apps、資料庫)。 您可以建立資源群組，或使用現有的資源群組 |
| App Service 方案 | myappplan          | 應用程式服務計劃代表 hello 集合，其使用的實體資源 toohost 的應用程式。 選取 hello**位置**和 hello**定價層**。 如需價格的詳細資訊，請參閱 [App Service 定價層](https://azure.microsoft.com/pricing/details/app-service/) |
| 資料庫      | mywordpressapp          | 選取用於 MySQL 的 hello 適當的資料庫提供者。 Web Apps 支援 **ClearDB**、**適用於 MySQL 的 Azure 資料庫**和**應用程式內 MySQL**。 如需詳細資料，請參閱下列的[資料庫設定](#database-config)一節。 |
| Application Insights | ON 或 OFF          | 這是選擇性。 請按一下 [ON]，[Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) 即可為您的 Web 應用程式提供監視服務。|

<a name="database-config"></a>

### <a name="database-configuration"></a>資料庫設定
請遵循下列 hello 步驟根據您所選擇的 MySQL 資料庫提供者。  建議在 hello 為該 Web 應用程式和 MySQL 資料庫相同的位置。

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) 是第三方解決方案，適用於 Azure 上完全整合的 MySQL 服務。 在訂單 toouse ClearDB 資料庫，您將需要 tooassociate 信用卡 tooyour [Azure 帳戶](http://account.windowsazure.com/subscriptions)。 如果您選取 ClearDB 資料庫提供者，您可以檢視從現有的資料庫 toochoose 的清單，或按一下**建立新**按鈕 toocreate 資料庫。

![ClearDB 建立](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>適用於 MySQL 的 Azure 資料庫 (預覽)
[Azure 的 MySQL 資料庫](https://azure.microsoft.com/en-us/services/mysql)應用程式開發和部署，可讓您在分鐘和 hello 上的小數位數的 MySQL 資料庫 toostand 飛您信任最 hello 雲端上提供的受管理的資料庫服務。 透過內含的計價模型，您可以取得所有 hello 功能，例如高可用性、 安全性及復原 – 在沒有內建的您想要額外成本。 按一下**定價層**toochoose 不同[定價層](https://azure.microsoft.com/pricing/details/mysql)。 toouse 的現有資料庫或現有的 MySQL server，使用現有的資源群組中的 hello 所在伺服器。 

![設定 hello hello web 應用程式的資料庫設定](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  並非所有的區域都提供適用於 MySQL 的 Azure 資料庫 (預覽) 和 Linux 上的 Web 應用程式 (預覽)。 深入了解 toolearn [MySQL （預覽） 的 Azure 資料庫](https://docs.microsoft.com/en-us/azure/mysql)和[Linux 上的 Web 應用程式](./app-service-linux-intro.md)限制。 

#### <a name="mysql-in-app"></a>應用程式內 MySQL
[MySQL 應用程式內](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)是應用程式服務可讓 hello 平台上原生執行 MySql 的功能。 hello hello hello 功能版本支援的核心功能：

- 在 hello 相同的執行個體並存裝載 hello 站台 web 伺服器上執行的 MySQL 伺服器。 這可提升您應用程式的效能。
- 可在 MySQL 和您的 web 應用程式檔案之間共用儲存體。 請注意，免費和共用計劃，您可能會達到中執行時使用 hello 網站根據 hello 動作您我們配額限制。 請查看[配額限制](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/)，了解免費與共用方案。
- 您可以開啟緩慢查詢記錄和適用於 MySQL 的一般記錄。 請注意，這可能會影響 hello 站台效能就不永遠開啟。 hello 記錄功能可協助您調查任何應用程式的問題。 

如需詳細資料，請查看這篇[文章](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![應用程式內 MySQL 管理](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

您可以按一下上方的 hello 入口網站頁面時 WordPress 應用程式正在部署的 hello hello hello 鈴鐺圖示觀賞 hello 進度。    
![進度指示器](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>管理新的 Azure Web 應用程式

移 toohello Azure 入口網站 tootake 查看您剛才建立的 hello web 應用程式。

toodo，登入太[https://portal.azure.com](https://portal.azure.com)。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


您已進入 Web 應用程式的_刀鋒視窗_ (水平開啟的入口網站頁面)。

根據預設，您的 web 應用程式 刀鋒視窗會顯示 hello**概觀**頁面。 此頁面可讓您檢視應用程式的執行方式。 您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 hello hello 左邊算起的 hello 刀鋒視窗上的索引標籤會顯示您可以開啟 hello 不同的組態頁面。

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

在 [hello] 刀鋒視窗中的這些索引標籤會顯示 hello 許多很棒的功能，您可以加入 tooyour web 應用程式。 下列清單中的 hello 可讓您幾個 hello 可能性：

* 對應自訂 DNS 名稱
* 繫結自訂 SSL 憑證
* 設定連續部署
* 相應增加和相應放大
* 新增使用者驗證

完成 hello 5 分鐘 WordPress 安裝精靈 toohave WordPress 應用程式啟動並執行。 簽出[Wordpress 文件](https://codex.WordPress.org/)toodevelop 您 web 應用程式。

![Wordpress 安裝精靈](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>設定您的應用程式 
在準備好將 WordPress 應用程式用於生產環境之前，需要進行多個步驟來管理 WordPress 應用程式。 請依照這些步驟 tooconfigure，並管理您的 WordPress 應用程式：

| toodo 這... | 目的... |
| --- | --- |
| **上傳或儲存大型檔案** |[使用 Blob 儲存體的 WordPress 外掛程式](https://wordpress.org/plugins/windows-azure-storage/)|
| **傳送電子郵件** |購買[SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview)電子郵件服務，並使用 hello [WordPress 外掛程式使用 SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure 它|
| **自訂網域名稱** |[在 Azure App Service 中設定自訂網域名稱](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[針對 Azure App Service 中的 Web 應用程式啟用 HTTPS](app-service-web-tutorial-custom-ssl.md) |
| **生產前驗證** |[針對 Azure App Service 中的 Web Apps 設定預備環境和開發環境](web-sites-staged-publishing.md)|
| **監視與疑難排解** |[針對 Azure App Service 中的 Web Apps 啟用診斷記錄功能](web-sites-enable-diagnostic-log.md)及[監視 Azure App Service 中的 Web Apps](app-service-web-tutorial-monitoring.md) |
| **部署您的網站** |[在 Azure App Service 中部署 Web 應用程式](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>保護您的應用程式 
在準備好將 WordPress 應用程式用於生產環境之前，需要進行多個步驟來管理 WordPress 應用程式。 請依照這些步驟 tooconfigure，並管理您的 WordPress 應用程式：

| toodo 這... | 目的... |
| --- | --- |
| **強式使用者名稱和密碼**|  經常變更密碼。 請勿使用常用的使用者名稱，例如 admin 或 wordpress 等。強制所有 WordPress 使用者 toouse 唯一使用者名稱和強式密碼。 |
| **隨時掌握最新資訊** | 將您的 WordPress 核心、 佈景主題、 向上 toodate 外掛程式。 使用 hello 最新版 PHP 執行階段可在 Azure 應用程式服務 |
| **更新 WordPress 安全性金鑰** | 更新[WordPress 安全性金鑰](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys)tooimprove 加密儲存在 cookie 中|

## <a name="improve-performance"></a>提升效能
Hello 雲端中的效能是主要是透過快取和向外延展來達成。不過，應該考慮 hello 記憶體、 頻寬和其他屬性的 Web 應用程式裝載。

| toodo 這... | 目的... |
| --- | --- |
| **了解 App Service 執行個體功能** |[定價詳細資料，包括 App Service 層的功能](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **快取資源** |使用[Azure Redis 快取](https://azure.microsoft.com/en-us/services/cache/)，或其中一個 hello hello 中的其他快取提供項目[Azure 市集](https://azuremarketplace.microsoft.com) |
| **調整您的應用程式** |您需要 tooscale [hello Azure App Service 中的 web 應用程式](web-sites-scale.md)及/或 MySQL 資料庫。 應用程式內 MySQL 不支援相應放大，因此請選擇適用於 MySQL 的 ClearDB 或 Azure 資料庫 (預覽)。 [調整 Azure 資料庫的 MySQL （預覽）](https://azure.microsoft.com/en-us/pricing/details/mysql/) ，或者使用[ClearDB 高可用性路由](http://w2.cleardb.net/faqs/)tooscale 註冊您的資料庫 |

## <a name="availability-and-disaster-recovery"></a>可用性和災難復原
高可用性包含災害復原 toomaintain 業務續航力的 hello 層面。 規劃失敗和嚴重損壞 hello 雲端中的快速需要 toorecognize hello 失敗。 這些解決方案可協助實作高可用性的策略。

| toodo 這... | 目的... |
| --- | --- |
| **負載平衡網站**或**異地發佈網站** |[使用 Azure 流量管理員將流量路由傳送](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **備份與還原** |[備份 Azure App Service 中的 Web 應用程式](web-sites-backup.md)及[還原 Azure App Service 中的 Web 應用程式](web-sites-restore.md) |

## <a name="next-steps"></a>後續步驟
深入了解各項功能[App Service toodevelop 和小數位數](/app-service-web/)。
