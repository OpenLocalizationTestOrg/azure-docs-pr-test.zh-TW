---
title: "aaaDeploy hello Azure 入口網站在五分鐘 Umbraco web 應用程式 |Microsoft 文件"
description: "了解如何輕鬆 toorun App Service 中的 web 應用程式部署範例 ASP.NET 應用程式。 立即看到結果。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Umbraco web 應用程式在 hello Azure 入口網站部署在五分鐘

本教學課程可幫助您部署 n [Umbraco](https://our.umbraco.org/) web 應用程式太[Azure App Service](../app-service/app-service-value-prop-what-is.md)以分鐘為單位。

![Umbraco 應用程式](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>必要條件
您需要 Microsoft Azure 帳戶。 如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。

> [!NOTE]
> 您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。 建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。
> 
> 

## <a name="deploy-hello-aspnet-app"></a>部署 hello ASP.NET 應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。

2. 開啟 [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS)。

    此連結是快顯 tooimmediately hello Azure 入口網站中設定新的 Umbraco 應用程式。

3. 在 [應用程式名稱] 中，輸入 Web 應用程式名稱。 您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`azurewebsites.net`網域。
   
5. 在**資源群組**，按一下 **建立新**新 toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)，然後為它命名。

7. 按一下 [App Service 方案/位置] > [新建]。 設定 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)所示：

    - 在**App Service 方案**，型別 hello 所需的名稱。
    - 在**位置**，選擇位置 toohost 您計劃。
    - 按一下 定價層，然後選取 F1 免費 或另一個適合您的層級，然後按一下選取。
    - 按一下 [確定] 。

    Umbraco CMS 設定現在看起來應該像下列螢幕擷取畫面的 hello:

    ![設定進行中 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. 按一下 [SQL Database] > [建立新的資料庫]。 設定 hello SQL 資料庫，如下所示：

    - 在 [名稱] 中輸入名稱，例如 **myDB**。
    - 按一下 定價層，然後選取 F 免費 或另一個適合您的層級，然後按一下選取。
    - 按一下 [目標伺服器] > [建立新的伺服器]。 Hello 資料庫伺服器設定，如下所示：

        - 在 [伺服器名稱] 中，輸入伺服器名稱。 您會看到綠色的核取記號，在 [hello] 方塊中，如果 hello 名稱是唯一在 hello`.database.windows.net`網域。
        - 在**Server 系統管理員登入**，型別 hello 需要系統管理員外的使用者名稱。
        - 在**密碼**和**確認密碼**，型別 hello 想要的密碼。
        - 在位置中，選取 hello 您 hello web 應用程式所使用的相同位置。
        - 請確定**允許 azure 服務 tooaccess 伺服器**已選取。
        - 按一下 [選取] 。
    
    - 按一下 [選取] 。

13. 按一下**Web 應用程式設定**，指定 hello 資料庫使用者名稱和密碼，然後按一下**確定**。

    Umbraco CMS 設定現在看起來應該像下列螢幕擷取畫面的 hello:

    ![設定完成 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. 按一下 [建立] 。
    
    Azure 現在會根據您的設定建立 Umbraco 應用程式。 您應該會看到 [部署已開始...] 通知。

    ![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>啟動及管理您的 Umrbaco Web 應用程式

當 Azure 完成應用程式部署時，您會看到另一個通知。

![部署成功 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. 按一下 hello 通知。 如果您遺漏了，您永遠可以存取它，即可 hello 通知鈴鐺 (![通知方-Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/notification.png))。

    您現在應該會看到 Web 應用程式的管理[刀鋒視窗](../azure-resource-manager/resource-group-portal.md#manage-resources) (*刀鋒視窗*︰水平開啟的入口網站頁面)。

3. 在 hello hello 概觀 頁面頂端，按一下 **瀏覽**。
   
    ![瀏覽 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/browse.png)

    現在您會看到 hello Umbraco ** 褖畫惎**頁面。 設定 hello Umbraco 安裝和開始玩玩看 ！

    ![Umbraco 設定 - Azure App Service 中的第一個 Umbraco](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>後續步驟
* [部署 ASP.NET web 應用程式 tooAzure 應用程式服務，使用 Visual Studio](app-service-web-get-started-dotnet.md) -了解如何 toocreate 新的 Azure web 應用程式，從 Visual Studio 中，使用 hello 其中包含應用程式範本。
* [部署您的應用程式服務的程式碼 tooAzure](web-sites-deploy.md)-了解如何 toodeploy 從 FTP 或從原始檔控制儲存機制。
* [新增功能 tooyour 第一個 web 應用程式](app-service-web-get-started-2.md)-採用 Azure 應用程式 toohello 下一個層級。 驗證您的使用者。 根據需求加以調整。 設定一些效能警示。 都只要點幾下滑鼠就能完成。
