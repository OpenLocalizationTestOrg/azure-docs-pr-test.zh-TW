---
title: "aaaDeploy hello 在五分鐘的 Azure 入口網站中的 WordPress 應用程式 |Microsoft 文件"
description: "了解如何輕鬆 toorun App Service 中的 web 應用程式部署的 WordPress 應用程式。 立即看到結果。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>WordPress 中部署應用程式 hello Azure 入口網站在五分鐘

本教學課程示範如何 toodeploy 您第一次[WordPress](https://wordpress.org/) web 應用程式太[Azure App Service](../app-service/app-service-value-prop-what-is.md)以分鐘為單位。

![WordPress 網站](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>必要條件
您需要 Microsoft Azure 帳戶。 如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。

> [!NOTE]
> 您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。 建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。
> 
> 

## <a name="deploy-hello-wordpress-app"></a>部署 hello WordPress 應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 開啟 [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress)。

    此連結是快顯 tooimmediately hello Azure 入口網站中設定的新 WordPress 應用程式。

3. 在 [應用程式名稱] 中，輸入 Web 應用程式名稱。 您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`azurewebsites.net`網域。
   
5. 在**資源群組**，按一下 [**建立新**新 toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。

6. 在 [資料庫提供者] 中，選取 [CleaDB]。

7. 按一下 [App Service 方案/位置] > [新建]。 設定 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)所示：

    - 在**App Service 方案**，型別 hello 所需的名稱。
    - 在**位置**，選擇位置 toohost 您計劃。
    - 按一下 [定價層]，然後選取 [F1 免費] 或另一個適合您的層級，然後按一下 [選取]。
    - 按一下 [確定] 。

8. 按一下 [資料庫] > [新建]。 設定 hello SQL 資料庫，如下所示：

    - 在 [資料庫名稱] 中，輸入資料庫名稱。 
    - 在**位置**，選擇 hello hello 應用程式服務計劃與相同的位置。
    - 按一下 [定價層]，然後選取 [Mercury] 或另一個適合您的層級，然後按一下 [選取]。
    - 按一下 [法律條款]，然後按一下 [購買]。
    - 按一下 [確定] 。

9. 按一下 [建立] 。

    Azure 現在會根據您的設定建立 WordPress 應用程式。 您應該會看到 [部署已開始...] 通知。

    ![已開始部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>啟動和管理 WordPress Web 應用程式

當 Azure 完成應用程式部署時，您會看到另一個通知。

![已成功部署 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. 按一下 hello 通知。 如果您遺漏了，您永遠可以存取它，即可 hello 通知鈴鐺 (![通知方-Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-dotnet-portal/notification.png))。

    您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。

3. 在 [hello hello 概觀] 頁面頂端，按一下 [**瀏覽**。
   
    ![瀏覽 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/browse.png)

    現在您會看到 hello WordPress ** 褖畫惎**頁面。 設定 hello WordPress 安裝和開始玩玩看 ！

    ![WordPress 設定 - Azure App Service 中的第一個 WordPress](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>後續步驟
* [建立、 設定及部署 Laravel web 應用程式 tooAzure](app-service-web-php-get-started.md) -了解您需要 toorun 任何 PHP web 應用程式在 Azure 中，例如 hello 基本技巧：

    * 從 PowerShell/Bash 在 Azure 中建立及設定 App。
    * 設定 PHP 版本。
    * 使用不是 hello 應用程式根目錄中啟動檔案。
    * 啟用編寫器自動化。
    * 存取環境特有的變數。
    * 針對常見錯誤進行疑難排解。

* [部署您的應用程式服務的程式碼 tooAzure](web-sites-deploy.md)-了解如何 toodeploy 從 FTP 或從原始檔控制儲存機制。
* [新增功能 tooyour 第一個 web 應用程式](app-service-web-get-started-2.md)-採用 Azure 應用程式 toohello 下一個層級。 驗證您的使用者。 根據需求加以調整。 設定一些效能警示。 都只要點幾下滑鼠就能完成。
