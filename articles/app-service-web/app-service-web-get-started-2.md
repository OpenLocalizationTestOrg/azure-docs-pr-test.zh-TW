---
title: "aaaAdd 功能 tooyour 第一個 web 應用程式 |Microsoft 文件"
description: "新增的酷炫功能 tooyour 第一個 web 應用程式在幾分鐘的時間。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 542671c2-22f0-4f20-8b4b-fa477264c492
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2016
ms.author: cephalin
ms.openlocfilehash: 46c9b118c2c188508cb0a369c691a79073b7d7b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-functionality-tooyour-first-web-app"></a>新增功能 tooyour 第一個 web 應用程式
在[5 分鐘內部署您的第一個 web 應用程式 tooAzure](app-service-web-get-started-dotnet.md)，部署範例 web 應用程式以[Azure App Service](../app-service/app-service-value-prop-what-is.md)。 在本文中，您可以快速加入一些很棒的功能 tooyour 部署 web 應用程式。 您將在幾分鐘內︰

* 強制執行使用者驗證
* 自動調整您的應用程式
* 收到 hello 應用程式效能警示

不論您在 hello 前一篇文章中部署的範例應用程式，您可以展開冒險 hello 教學課程中。

hello 中只有幾個範例的 hello 許多有用的功能，您放入應用程式服務的 web 應用程式時，您收到此教學課程都是三個活動。 許多 hello 功能都可在 hello**免費**層 （此為您的第一個 web 應用程式執行的項目），而且您可以使用您的試用信用額度 tootry 需要更高的定價層的功能。 在您 web 應用程式中向前邁進**免費**層，除非您明確地變更它 tooa 不同定價層。

> [!NOTE]
> 您使用 Azure CLI 建立 hello web 應用程式中執行**免費**層，只允許一個共用的 VM 執行個體使用的資源配額。 如需可在 **免費** 層獲得之資源的詳細資訊，請參閱 [App Service 限制](../azure-subscription-service-limits.md#app-service-limits)。
> 
> 

## <a name="authenticate-your-users"></a>驗證您的使用者
現在，讓我們來看看是多麼的輕鬆 tooadd authentication tooyour 應用程式 (在進一步閱讀[應用程式服務驗證/授權](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/))。

1. 在 hello 入口網站應用程式的刀鋒視窗，其中您剛開啟中，按一下**設定** > **驗證 / 授權**。  
    ![Authenticate - settings blade](./media/app-service-web-get-started/aad-login-settings.png)
2. 按一下**上**tooturn 驗證。  
3. 在 [驗證提供者] 中，按一下 [Azure Active Directory]。  
    ![Authenticate - select Azure AD](./media/app-service-web-get-started/aad-login-config.png)
4. 在 hello **Azure Active Directory 設定**刀鋒視窗中，按一下  **Express**，然後按一下 **確定**。 hello 預設設定建立新的預設目錄中的 Azure AD 應用程式。  
    ![Authenticate - express configuration](./media/app-service-web-get-started/aad-login-express.png)
5. 按一下 [儲存] 。  
    ![Authenticate - save configuration](./media/app-service-web-get-started/aad-login-save.png)
   
    一旦 hello 變更成功，您會看見 hello 通知鈴鐺變成綠色，以及一個易記訊息。
6. 在 hello 入口網站應用程式的刀鋒視窗，按一下 hello **URL**連結 (或**瀏覽**hello 功能表列中)。 hello 連結是 HTTP 位址。  
    ![驗證-瀏覽 tooURL](./media/app-service-web-get-started/aad-login-browse-click.png)  
    但會 hello 應用程式開啟新索引標籤中，一旦 hello URL 方塊中重新導向數次，並完成您的應用程式上的 HTTPS 位址。 您所看到您已登入 tooyour Azure 訂用帳戶，而且您自動驗證 hello 應用程式中。  
    ![Authenticate - logged in](./media/app-service-web-get-started/aad-login-browse-http-postclick.png)  
    如果您現在會在不同的瀏覽器中開啟未驗證的工作階段，您將看到登入畫面，當您巡覽 toohello 相同的 URL。  
    <!-- ![Authenticate - login page](./media/app-service-web-get-started/aad-login-browse.png)  -->
    如果您從未使用 Azure Active Directory 執行任何作業，預設目錄可能沒有任何 Azure AD 使用者。 在此情況下，可能 hello 中那里唯一的帳戶是 hello 與您 Azure 訂用帳戶的 Microsoft 帳戶。 已自動登入 toohello 應用程式中的原因 hello 相同稍早的瀏覽器。
    您可以使用在該同一個 Microsoft 帳戶 toolog 此登入頁面上。

恭喜，您要將所有流量 tooyour web 應用程式進行都驗證。

您可能已注意到在 hello**驗證 / 授權**刀鋒視窗，您可以包含許多功能，例如：

* 啟用社交登入
* 啟用多個登入選項
* 變更 hello 預設行為，當使用者第一次瀏覽 tooyour 應用程式

應用程式服務提供周全需求的解決方案的 hello 通用驗證某些因此您不自己需要 tooprovide hello 驗證邏輯。
如需詳細資訊，請參閱 [App Service 驗證/授權](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/)。

## <a name="scale-your-app-automatically-based-on-demand"></a>自動根據需求調整您的應用程式
下一步] 讓我們來自動調整您的應用程式，它會自動調整其容量 toorespond toouser 需求 (進一步閱讀 [在[向上擴充您的應用程式在 Azure 中](web-sites-scale.md)和[手動或自動調整執行個體計數](../monitoring-and-diagnostics/insights-how-to-scale.md)).

簡單地說，Web 應用程式有兩種調整方法︰

* [相應增加](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)︰取得更多的 CPU、記憶體、磁碟空間和額外的功能，例如專用 VM、自訂網域和憑證、預備位置，以及自動調整等等。 向上擴充藉由變更定價層的應用程式所屬的應用程式服務方案的 hello。
* [向外延展](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling)： 增加 hello 執行您的應用程式的 VM 執行個體數目。
  您可以向外延展 tooas 許多為 50 個執行個體，視您的定價層而定。

我們就不再贅言，馬上來設定自動調整。

1. 首先，讓我們來向上擴充 tooenable 自動調整。 在 hello 入口網站應用程式的刀鋒視窗，按一下 **設定** > **向上延展 （App Service 方案）**。  
    ![Scale up - settings blade](./media/app-service-web-get-started/scale-up-settings.png)
2. 捲動並選取 hello **S1 標準**層，hello 最低層支援自動調整 （中所圈出螢幕擷取畫面），然後按一下 **選取**。  
    ![Scale up - choose tier](./media/app-service-web-get-started/scale-up-select.png)
   
    您已完成相應增加。
   
   > [!IMPORTANT]
   > 這一層會耗用您的免費試用額度。 如果您有每次使用付費帳戶，它會產生費用 tooyour 帳戶。
   > 
   > 
3. 接下來，設定自動調整。 在 hello 入口網站應用程式的刀鋒視窗，按一下 **設定** > **向外 （App Service 方案）**。  
    ![Scale out - settings blade](./media/app-service-web-get-started/scale-out-settings.png)
4. 變更**縮放**太**CPU 百分比**。 hello hello 下拉式清單下方的滑桿會隨之更新。 然後，定義介於 **1** 與 **2** 之間的 [執行個體] 範圍，以及介於 **40** 與 **80** 之間的 [目標範圍]。 在 [hello] 方塊中輸入或移動 hello 滑桿，請進行它。  
    ![Scale out - configure autoscaling](./media/app-service-web-get-started/scale-out-configure.png)
   
    根據此設定，當 CPU 使用率高於 80% 時，您的應用程式會自動相應放大，而當 CPU 使用率低於 40% 時則會相應縮小。
5. 按一下**儲存**hello 功能表列中。

恭喜，您的應用程式已在自動調整。

您可能已注意到在 hello**調整規模設定**刀鋒視窗，您可以包含許多功能，例如：

* 手動調整 tooa 特定執行個體數目
* 依其他效能計量 (例如記憶體百分比或磁碟佇列) 調整
* 自訂觸發效能規則時的調整行為
* 根據排程自動調整
* 設定未來事件的自動調整行為

如需有關相應增加應用程式的詳細資訊，請參閱 [在 Azure 中相應增加您的應用程式](web-sites-scale.md)。 如需有關相應放大的詳細資訊，請參閱[手動或自動調整執行個體計數](../monitoring-and-diagnostics/insights-how-to-scale.md)。

## <a name="receive-alerts-for-your-app"></a>接收應用程式的警示
既然您的應用程式會自動調整，到達 hello 執行個體計數上限 (2) 時，會發生什麼事，且 CPU 高於所需的使用率 （80%)？
您可以設定警示 (在進一步閱讀[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)) tooinform 您這種情況，因此您可以進一步調整向上/出您的應用程式，例如。 為此案例迅速設定警示。

1. 在 hello 入口網站應用程式的刀鋒視窗，按一下 **工具** > **警示**。  
    ![Alerts - settings blade](./media/app-service-web-get-started/alert-settings.png)
2. 按一下 [新增警示] 。 然後，在 hello**資源**方塊中，選取 hello 資源以結束的**（上限）**。 這就是您的 App Service 方案。  
    ![警示 - 新增 App Service 方案的警示](./media/app-service-web-get-started/alert-add.png)
3. 將 [名稱] 指定為 `CPU Maxed`、[計量] 指定為 [CPU 百分比]，以及 [臨界值] 指定為 `90`，然後選取 [電子郵件擁有者、參與者和讀者]，再按一下 [確定]。   
    ![Alerts - configure alert](./media/app-service-web-get-started/alert-configure.png)
   
    當 Azure 完成建立 hello 警示時，會看到在 hello**警示**刀鋒視窗。  
    ![Alerts - finished view](./media/app-service-web-get-started/alert-done.png)

恭喜，您現已接收警示。

此警示設定會每隔 5 分鐘檢查一次 CPU 使用率。 如果該數字高於 90%，您以及獲得授權的人員都會收到電子郵件警示。 toosee 是授權的 tooreceive hello 警示所有人移回您的應用程式的 toohello 入口網站的刀鋒視窗，然後按一下 [hello**存取**] 按鈕。  
![查看有誰收到警示](./media/app-service-web-get-started/alert-rbac.png)

您應該會看到**訂閱管理員**已 hello**擁有者**hello 應用程式。 這個群組會包含您，如果您的 Azure 訂用帳戶 （例如您試用的訂閱） 的 hello 帳戶系統管理員。 如需 Azure 角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。

> [!NOTE]
> 警示規則是一項 Azure 功能。 如需詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)。
> 
> 

## <a name="next-steps"></a>後續步驟
在您的方式 tooconfigure hello 警示，您可能已注意到一組豐富的工具在 hello**工具**刀鋒視窗。 在這裡，您可以疑難排解問題，監視效能測試弱點，管理資源、 互動 hello VM 主控台中，並加入實用的擴充功能。 我們邀請您針對每一個這些工具 toodiscover hello 簡單但功能強大工具在您的手指秘訣 tooclick。

了解如何 toodo 多個已部署應用程式。 以下只是部分清單︰

* [購買並設定自訂網域名稱](custom-dns-web-site-buydomains-web-app.md) - 為您的 Web 應用程式購買引人注意的網域，而非 *.azurewebsites.net 網域。 或使用既有網域。
* [設定預備環境](web-sites-staged-publishing.md)-部署您的應用程式 tooa 暫存之前將它放置到實際執行環境的 URL。 放心地更新執行中的 Web 應用程式。 為精心規劃的 DevOps 方案設定多個部署位置。
* [設定連續部署](app-service-continuous-deployment.md) - 將應用程式部署整合至原始檔控制系統。 使用每個認可部署到 Azure。
* [存取內部部署資源](web-sites-hybrid-connection-get-started.md) - 存取現有的內部部署資料庫或 CRM 系統。
* [備份您的應用程式](web-sites-backup.md) - 為 Web 應用程式設定備份與還原。 為非預期的失敗做好準備，並從中復原。
* [啟用診斷記錄檔](web-sites-enable-diagnostic-log.md)-讀取 hello IIS 記錄來自 Azure 或應用程式的追蹤。 在串流中讀取記錄檔、下載記錄檔，或將記錄檔移植到 [Application Insights](../application-insights/app-insights-overview.md) 來進行周全分析。
* [掃描應用程式中的弱點](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)-
  使用 [Tinfoil Security](https://www.tinfoilsecurity.com/) 所提供的服務，掃描 Web 應用程式中是否有新型威脅。
* [執行背景工作](../azure-functions/functions-overview.md) - 執行資料處理、報告等工作。
* [了解 App Service 的運作方式](../app-service/app-service-how-works-readme.md)

