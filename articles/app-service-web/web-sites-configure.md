---
title: "aaaConfigure Azure App Service 中的 web 應用程式"
description: "如何 tooconfigure Azure 應用程式服務中的 web 應用程式"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>在 Azure App Service 中設定 Web 應用程式
本主題說明如何使用 web 應用程式的 tooconfigure hello [Azure 入口網站]。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>應用程式設定
1. 在 hello [Azure 入口網站]，開啟 hello web 應用程式的 hello 刀鋒視窗。
2. 按一下 [ **所有設定**]。
3. 按一下 [ **應用程式設定**]。

![應用程式設定][configure01]

hello**應用程式設定**分頁有數種類別在下設為群組的設定。

### <a name="general-settings"></a>一般設定
**Framework 版本**。 如果您的應用程式使用下列任何 Framework，請設定下列選項： 

* **.NET framework**: Set hello.NET framework 版本。 
* **PHP**: Set hello PHP 版本，或**OFF** toodisable PHP。 
* **Java**： 選取 hello Java 版本或**OFF** toodisable Java。 使用 hello**網頁容器**選項 toochoose Tomcat 或 Jetty 版本之間。
* **Python**： 選取 hello Python 版本，或**OFF** toodisable Python。

若是技術原因，針對您的應用程式啟用 Java，將停用 hello.NET、 PHP 以及 Python 選項。

<a name="platform"></a>
**平台**。 選取 Web 應用程式是否會在 32 位元或 64 位元環境中執行。 hello 64 位元環境需要使用基本或標準模式。 [免費] 與 [共用] 模式一律於 32 位元環境中執行。

**Web 通訊端**。 設定**ON** tooenable hello WebSocket 通訊協定; 例如，如果您的 web 應用程式使用[ASP.NET SignalR]或[socket.io]。

<a name="alwayson"></a>
**永遠開啟**。 根據預設，Web 應用程式如果閒置一段時間，就會卸載。 這可讓 hello 系統節省資源。 在基本或標準模式中，您可以啟用**Always On** tookeep hello 應用程式載入所有 hello 時間。 如果您的應用程式執行連續 web 工作或執行 WebJobs 觸發使用 CRON 運算式，您應該啟用**Always On**，或 hello web 工作可能無法可靠地執行。

**受管理的管線版本**。 設定 hello IIS[管線模式]。 保留此設定 tooIntegrated （hello 預設值），除非您有舊版的應用程式需要較舊版本的 IIS。

**自動交換**。 如果您啟用自動交換部署位置時，應用程式服務將會自動交換 hello web 應用程式運行推送更新 toothat 位置時。 如需詳細資訊，請參閱[部署在 Azure App Service web 應用程式的 toostaging 位置](web-sites-staged-publishing.md)。

### <a name="debugging"></a>Debugging
**遠端偵錯**。 啟用遠端偵錯。 啟用時，您可以使用 hello 遠端偵錯工具，在 Visual Studio tooconnect 直接 tooyour web 應用程式即可。 遠端偵錯將保持啟用達 48 小時。 

### <a name="app-settings"></a>應用程式設定
本區段包含您的 Web 應用程式將在啟動時載入的名稱/值組。 

* 如果是 .NET 應用程式，這些設定就會在執行階段插入 .NET 設定 `AppSettings` ，並覆寫現有的設定。 
* PHP、Python、Java 和 Node 應用程式可以在執行階段以環境變數的形式存取這些設定。 每個應用程式設定，會建立兩個環境變數;其中一個 hello hello 應用程式設定項目，和另一個具有 APPSETTING_ 前置詞所指定的名稱。 同時包含 hello 相同的值。

### <a name="connection-strings"></a>連接字串
連結資源的連接字串。 

對於.NET 應用程式，這些連接字串會插入.NET 組態`connectionStrings`覆寫現有 hello 索引鍵相同的項目在執行階段，設定 hello 連結的資料庫名稱。 

PHP、 Python、 Java 和節點的應用程式，會視為環境變數，在執行階段，加上 hello 連接類型使用這些設定。 如下所示為 hello 環境變數的前置詞： 

* SQL Server： `SQLCONNSTR_`
* MySQL： `MYSQLCONNSTR_`
* SQL Database： `SQLAZURECONNSTR_`
* 自訂：`CUSTOMCONNSTR_`

例如，如果已在名為 MySql 連接字串`connectionstring1`，它會透過 hello 環境變數存取`MYSQLCONNSTR_connectionString1`。

### <a name="default-documents"></a>預設文件
hello 預設文件是 hello web 網頁上顯示的 hello 根 URL 的網站。  會使用 hello 第一個相符的檔案 hello 清單中。 

Web 應用程式可能會使用根據 URL 路由傳送的模組，而非處理靜態內容，若是如此，就不會有這類預設文件。    

### <a name="handler-mappings"></a>處理常式對應
使用此區域 tooadd 自訂指令碼處理器 toohandle 要求特定副檔名。 

* **副檔名**。 hello 檔案副檔名 toobe 處理，例如 *.php 或 handler.fcgi。 
* **指令碼處理器路徑**。 hello 指令碼處理器 hello 絕對路徑。 符合 hello 副檔名的要求 toofiles 會由 hello 指令碼處理器處理。 使用 hello 路徑`D:\home\site\wwwroot`toorefer tooyour 應用程式的根目錄。
* **其他引數**。 Hello 指令碼處理器的選擇性命令列引數 

### <a name="virtual-applications-and-directories"></a>虛擬應用程式與目錄
tooconfigure 虛擬應用程式和目錄，請指定每個虛擬目錄和其對應的實體路徑相對 toohello 網站根目錄。 或者，您可以選取 hello**應用程式**核取方塊 toomark 做為應用程式的虛擬目錄。

## <a name="enabling-diagnostic-logs"></a>啟用診斷記錄
tooenable 診斷記錄檔：

1. 在 hello 刀鋒視窗 web 應用程式中，按一下 **所有設定**。
2. 按一下 [ **診斷記錄**]。 

從支援記錄功能的 Web 應用程式寫入診斷記錄的選項： 

* **應用程式記錄**。 將應用程式記錄檔寫入 toohello 檔案系統。 記錄功能會持續運作 12 小時。 

**層級**。 啟用應用程式記錄時，這個選項會指定 hello 量的資訊，將會錄製 （錯誤、 警告、 資訊或詳細資訊）。

**Web 伺服器記錄**。 記錄檔會儲存在 hello W3C 擴充的記錄檔格式。 

**詳細的錯誤訊息**。 將詳細的錯誤訊息儲存為 .htm 檔案。 hello 檔案會儲存在 /LogFiles/DetailedErrors 下。 

**失敗要求的追蹤**。 記錄檔失敗的要求 tooXML 檔案。 hello 檔案儲存在底下/LogFiles/W3SVC*xxx*，其中 xxx 是唯一的識別項。 此資料夾內含有一個 XSL 檔案和一或多個 XML 檔案。 請確定 toodownload hello XSL 檔案，因為它提供用來格式化和篩選的 hello XML 檔案的 hello 內容的功能。

tooview hello 記錄檔，您必須建立 FTP 認證，如下所示：

1. 在 hello 刀鋒視窗 web 應用程式中，按一下 **所有設定**。
2. 按一下 [ **部署認證**]。
3. 請輸入使用者名稱和密碼。
4. 按一下 [儲存] 。

![設定部署認證][configure03]

hello 完整 FTP 使用者名稱是"app\username"其中*應用程式*hello 您 web 應用程式名稱。 hello 使用者名稱會列在 hello web 應用程式 刀鋒視窗，在**Essentials**。  

![FTP 部署認證][configure02]

## <a name="other-configuration-tasks"></a>其他配置作業
### <a name="ssl"></a>SSL
在 [基本] 或 [標準] 模式中，您可以上傳自訂網域的 SSL 憑證。 如需詳細資訊，請參閱 [為 Web 應用程式啟用 HTTPS]。 

您已上傳的憑證，按一下 tooview**所有設定** > **自訂網域及 SSL**。

### <a name="domain-names"></a>網域名稱
新增 Web 應用程式的自訂網域名稱。 如需詳細資訊，請參閱 [為 Azure App Service 中的 Web 應用程式設定自訂網域名稱]。

您的網域名稱，按一下 tooview**所有設定** > **自訂網域及 SSL**。

### <a name="deployments"></a>部署
* 設定連續部署。 請參閱[使用 Git toodeploy Azure App Service 中的 Web 應用程式](web-sites-deploy.md)。
* 部署位置。 請參閱[Azure App Service 中的 Web 應用程式部署 tooStaging 環境]。

您的部署位置，按一下 tooview**所有設定** > **部署位置**。

### <a name="monitoring"></a>監視
在基本或標準模式中，您可以從測試 HTTP 或 HTTPS 端點的 hello 可用性 toothree 地理位置。 如果 HTTP 回應碼 hello 錯誤 （4xx 或 5xx） 或 hello 回應時間超過 30 秒，則監視測試將會失敗。 端點視為可用 hello 監視測試皆成功從所有 hello 指定位置。 

如需詳細資訊，請參閱 [如何監視 Web 端點狀態]。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務]，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="next-steps"></a>後續步驟
* [在 Azure App Service 中設定自訂網域名稱]
* [針對 Azure App Service 中的 App 啟用 HTTPS]
* [在 Azure App Service 中調整 Web 應用程式規模]
* [在 Azure App Service 中監視 Web 應用程式的基本概念]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure 入口網站]: https://portal.azure.com/
[在 Azure App Service 中設定自訂網域名稱]: ./app-service-web-tutorial-custom-domain.md
[Azure App Service 中的 Web 應用程式部署 tooStaging 環境]: ./web-sites-staged-publishing.md
[針對 Azure App Service 中的 App 啟用 HTTPS]: ./app-service-web-tutorial-custom-ssl.md
[如何監視 Web 端點狀態]: http://go.microsoft.com/fwLink/?LinkID=279906
[在 Azure App Service 中監視 Web 應用程式的基本概念]: ./web-sites-monitor.md
[管線模式]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[在 Azure App Service 中調整 Web 應用程式規模]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[再試一次應用程式服務]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
