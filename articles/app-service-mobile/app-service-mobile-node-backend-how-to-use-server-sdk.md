---
title: "與 hello Node.js 後端伺服器的行動應用程式 SDK 的 aaaHow toowork |Microsoft 文件"
description: "了解如何與 toowork hello Node.js 後端伺服器 SDK Azure App Service 行動應用程式。"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a>如何 toouse hello Azure 行動應用程式 Node.js SDK
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

本文章提供詳細的資訊和範例顯示如何 toowork Node.js 後端 Azure App Service 行動應用程式中使用。

## <a name="Introduction"></a>簡介
Azure App Service 行動應用程式提供 hello 功能 tooadd 行動最佳化資料存取 Web API tooa web 應用程式。  ASP.NET 和 Node.js web 應用程式提供 hello Azure App Service 行動應用程式 SDK。  hello SDK 提供 hello 下列作業：

* 資料存取的資料表作業 (讀取、插入、更新、刪除)
* 自訂 API 作業

這兩種作業都可用於 Azure App Service 所允許的所有識別提供者 (包括 Facebook、Twitter、Google 和 Microsoft 等社交識別提供者，以及用於企業身分識別的 Azure Active Directory) 之間的驗證。

您可以找到每個範例使用案例中 hello [GitHub 上的範例目錄]。

## <a name="supported-platforms"></a>支援的平台
hello Azure 行動應用程式節點 SDK 支援的 hello LTS 目前版本的節點及更新版本。  撰寫、 hello 新版 LTS 為節點 v4.5.0。  其他版本的 Node 可能可以運作，但不受支援。

hello Azure 行動應用程式節點 SDK 支援兩個資料庫驅動程式-hello 節點 mssql 驅動程式支援 SQL Azure 和本機 SQL Server 執行個體。  hello sqlite3 驅動程式的單一執行個體只支援 SQLite 資料庫。

### <a name="howto-cmdline-basicapp"></a>如何： 建立基本的 Node.js 後端使用 hello 命令列
每個 Azure App Service Mobile App Node.js 後端都會以 ExpressJS 應用程式的形式啟動。  ExpressJS 是 hello 熱門 web 服務架構，適用於 Node.js。  您可以依照下列方式建立基本的 [Express] 應用程式：

1. 在命令或 PowerShell 視窗中，為您的專案建立目錄。

        mkdir basicapp
2. 請執行 npm init tooinitialize hello 封裝結構。

        cd basicapp
        npm init

    hello npm init 命令會要求一組問題 tooinitialize hello 專案。  請參閱 hello 範例輸出：

    ![hello npm init 輸出][0]
3. Hello npm 儲存機制安裝 hello 快速和 azure 行動應用程式程式庫。

        npm install --save express azure-mobile-apps
4. 建立 app.js 檔案 tooimplement hello 基本行動伺服器。

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

此應用程式建立行動裝置最佳化的 WebAPI 與單一端點 (`/tables/TodoItem`) 提供未驗證的存取 tooan 基礎 SQL 資料存放區中使用動態結構描述。  它適用於下列用戶端程式庫快速入門：

* [Android 用戶端快速入門]
* [Apache Cordova 用戶端快速入門]
* [iOS 用戶端快速入門]
* [Windows 市集用戶端快速入門]
* [Xamarin.iOS 用戶端快速入門]
* [Xamarin.Android 用戶端快速入門]
* [Xamarin.Forms 用戶端快速入門]

您可以在 hello 這個基本應用程式找到 hello 程式碼[GitHub 上的 basicapp 範例]。

### <a name="howto-vs2015-basicapp"></a>作法：使用 Visual Studio 2015 建立 Node 後端
Visual Studio 2015 需要 hello IDE 內延伸 toodevelop Node.js 應用程式。  toostart，安裝 hello [Node.js Tools 1.1 for Visual Studio]。  一旦安裝 hello Node.js Tools for Visual Studio，建立 Express 4.x 應用程式：

1. 開啟 hello**新專案**對話方塊 (從**檔案** > **新增** > **專案...**).
2. 展開**範本** > **JavaScript** > **Node.js**。
3. 選取 hello**基本 Azure Node.js Express 4 應用程式**。
4. 填寫 hello 專案名稱。  按一下 [確定] 。

    ![Visual Studio 2015 新專案][1]
5. 以滑鼠右鍵按一下 hello **npm**節點，然後選取**安裝新的 npm 封裝...**.
6. 您可能需要 toorefresh hello npm 目錄上建立第一個 Node.js 應用程式。  如有必要，請按一下 [重新整理]  。
7. 輸入*azure 行動應用程式*hello [搜尋] 方塊中。  按一下 hello **azure 行動-應用程式 2.0.0**封裝，然後按一下 **安裝套件**。

    ![安裝新的 npm 封裝][2]
8. 按一下 [關閉] 。
9. 開啟 hello *app.js*檔案 hello Azure 行動應用程式 SDK 的 tooadd 支援。  底端列 6 at hello hello 程式庫需要陳述式，加入下列程式碼的 hello:

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    在大約列 27 之後 hello 其他 app.use 陳述式中，加入下列程式碼的 hello:

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    儲存 hello 檔案。
10. 請執行 hello 應用程式在本機 (hello http://localhost:3000 提供應用程式開發介面)，或發行 tooAzure。

### <a name="create-node-backend-portal"></a>如何： 建立 Node.js 後端使用 hello Azure 入口網站
您可以建立行動裝置應用程式後端從右 hello [Azure 入口網站]。 您可以依照下列步驟，或建立下列 hello 一起用戶端和伺服器 hello[建立行動應用程式](app-service-mobile-ios-get-started.md)教學課程。 hello 教學課程包含這些指示的簡化的版本，而且是最適合的專案概念證明。

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

在 hello*開始*刀鋒視窗底下**建立資料表 API**，選擇**Node.js**做為您**後端語言**。
核取方塊 hello"**我了解此將覆寫所有網站內容。**"，然後按一下 **建立 TodoItem 資料表**。

### <a name="download-quickstart"></a>如何： 下載 hello Node.js 後端快速入門的程式碼專案使用 Git
當您建立 Node.js 行動裝置應用程式後端使用 hello 網站**快速入門**刀鋒視窗中，您與已部署的 tooyour 網站建立 Node.js 專案。 您可以加入資料表和應用程式開發介面，並編輯 hello 入口網站中的 hello Node.js 後端的程式碼檔案。 您也可以使用各種部署工具 toodownload hello 後端專案，讓您可以新增或修改的資料表和應用程式開發介面，然後重新發行 hello 專案。 如需詳細資訊，請參閱 [Azure App Service 部署指南]。 hello 下列程序使用 Git 儲存機制 toodownload hello 快速入門專案代碼。

1. 如果尚未安裝 Git，請先安裝。 hello 步驟需要的 tooinstall Git 因作業系統不同。 如需作業系統特定的發佈和安裝指引，請參閱 [安裝 Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) 。
2. 中的 hello 步驟[啟用 hello App Service 應用程式儲存機制](../app-service-web/app-service-deploy-local-git.md#Step3)tooenable hello Git 儲存機制，為您記下 hello 部署使用者名稱和密碼的後端網站。
3. 在您的行動裝置應用程式後端 hello 刀鋒視窗，記下的 hello **Git 複製 URL**設定。
4. 執行 hello`git clone`命令使用 hello Git 複製 URL，輸入您的密碼時所需，如下列範例所示：

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. 瀏覽 toolocal 目錄，即在上述範例中的 hello /todolist，並請注意，專案檔已下載。 找出 hello`todoitem.json`檔案在 hello`/tables`目錄。  該檔案定義了資料表上的權限。  也可以找到 hello`todoitem.js`相同檔案中 hello 定義 CRUD 作業 hello 資料表編寫指令碼的目錄。
6. 您所做的變更 tooproject 檔案之後，執行下列命令 tooadd，認可，則上傳變更 toohello 站台的 hello:

        $ git commit -m "updated hello table script"
        $ git push origin master

    當您新增新檔案 toohello 專案時，您必須先 tooexecute hello`git add .`命令。

每次一組新的認可已推送 toohello 站台重新發行 hello 站台。

### <a name="howto-publish-to-azure"></a>如何： 發行您的 Node.js 後端 tooAzure
Microsoft Azure 提供許多發行您的 Azure App Service 行動應用程式 Node.js 後端，hello Azure 服務的機制。  其中包括使用整合至 Visual Studio 中的部署工具、命令列工具，和以原始檔控制為基礎的連續部署選項。  如需有關本主題的詳細資訊，請參閱 [Azure App Service 部署指南]。

Azure App Service 提供 Node.js 應用程式方面的具體建議，您應該在部署之前先檢閱：

* 如何太[指定 hello 節點版本]
* 如何太[使用節點模組]

### <a name="howto-enable-homepage"></a>作法：啟用應用程式的首頁
許多應用程式是 web 和行動裝置應用程式的組合，hello ExpressJS 架構可讓您 toocombine 兩個 facet。  有時候，不過，您可能希望 tooonly 實作行動裝置的介面。  有用的 tooprovide 登陸頁面 tooensure hello 應用程式服務已啟動並執行它。  您可以提供您自己的首頁，或啟用暫時的首頁。  tooenable 暫存的首頁上，使用下列 tooinstantiate Azure 行動應用程式的 hello:

    var mobile = azureMobileApps({ homePage: true });

如果您只想使用此選項，在本機開發時，您可以加入此設定 tooyour`azureMobile.js`檔案。

## <a name="TableOperations"></a>資料表作業
hello azure 行動應用程式 Node.js 伺服器 SDK 提供機制 tooexpose 資料儲存為 WebAPI Azure SQL Database 中的資料表。  提供的作業有五種。

| 作業 | 說明 |
| --- | --- |
| GET /tables/*tablename* |取得 hello 資料表中的所有記錄 |
| GET /tables/*tablename*/:id |取得 hello 資料表中的特定記錄 |
| POST /tables/*tablename* |建立 hello 資料表中的記錄 |
| PATCH /tables/*tablename*/:id |更新 hello 資料表中的記錄 |
| DELETE /tables/*tablename*/:id |刪除 hello 資料表中的記錄 |

支援這個 WebAPI [OData]並擴充 hello 資料表結構描述 toosupport[離線的資料同步]。

### <a name="howto-dynamicschema"></a>作法：使用動態結構描述定義資料表
資料表必須先經過定義才能使用。  資料表可以定義，使用靜態結構描述 （hello 開發人員定義 hello hello 結構描述內的資料行） 或動態 （hello SDK 控制項 hello 根據連入要求的結構描述）。 此外，hello 開發人員可以藉由新增 Javascript 程式碼 toohello 定義控制 hello WebAPI 的特定層面。

最佳做法，您應該在 hello 資料表目錄中，Javascript 檔案中定義的每個資料表，然後使用 tables.import() 方法 tooimport hello 資料表。  擴充 hello basic 應用程式，會調整 hello app.js 檔案：

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

中的 hello 資料表定義。 / tables/TodoItem.js:

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

資料表依預設會使用動態結構描述。  關閉動態結構描述的 tooturn 全域設定 hello 應用程式設定**MS_DynamicSchema** toofalse hello Azure 入口網站中的。

您可以在 hello 找到完整的範例[GitHub 上的 todo 範例]。

### <a name="howto-staticschema"></a>作法：使用靜態結構描述定義資料表
您可以明確定義透過 hello WebAPI hello 資料行 tooexpose。  hello azure 行動應用程式 Node.js SDK 會自動將您提供的離線資料同步處理 toohello 清單所需的任何其他資料行。  例如，快速入門用戶端應用程式需要具有兩個資料行的資料表：文字 (字串) 和完整 (布林值)。  
hello 資料表可以定義 hello 資料表定義 JavaScript 檔案中 （位於 hello 資料表目錄），如下所示：

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

如果您以靜態方式定義的資料表，然後您必須也 hello tables.initialize() 方法 toocreate hello 資料庫結構描述上呼叫啟動。  hello tables.initialize() 方法會傳回[承諾]以便 hello web 服務不會服務正在初始化 hello 資料庫之前，要求。

### <a name="howto-sqlexpress-setup"></a>作法：以 SQL Express 作為本機電腦上的開發資料存放區
hello Azure 行動應用程式 hello AzureMobile 應用程式節點 SDK 提供三個選項來服務資料 hello 現成： SDK 提供 hello 現成提供資料的三個選項：

* 使用 hello**記憶體**驅動程式 tooprovide 非持續性範例存放區
* 使用 hello **mssql**驅動程式 tooprovide 開發 SQL Express 資料存放區
* 使用 hello **mssql**驅動程式 tooprovide 生產環境的 Azure SQL Database 資料存放區

hello Azure 行動應用程式 Node.js SDK 會使用 hello [mssql Node.js 封裝]tooestablish 及使用連線 tooboth SQL Express 和 SQL Database。  要使用此封裝，您必須在 SQL Express 執行個體上啟用 TCP 連線。

> [!TIP]
> hello 記憶體驅動程式不提供一組完整的測試。  如果您想 tootest 後端在本機，我們會建議 hello 使用 SQL Express 的資料存放區，且 hello mssql 驅動程式。
>
>

1. 下載並安裝 [Microsoft SQL Server 2014 Express]。  請確定您安裝 hello SQL Server 2014 Express with Tools 版本。  除非您明確需要 64 位元支援，hello 32 位元版本執行時，就會耗用較少的記憶體。
2. 執行 SQL Server 2014 組態管理員 hello。

   1. 展開 hello **SQL Server 網路組態**hello 左側的樹狀結構功能表中的節點。
   2. 按一下 [SQLEXPRESS 的通訊協定] 。
   3. 以滑鼠右鍵按一下 [TCP/IP]，然後選取 [啟用]。  按一下**確定**hello 快顯對話方塊中。
   4. 以滑鼠右鍵按一下 [TCP/IP]，然後選取 [屬性]。
   5. 按一下 hello **IP 位址** 索引標籤。
   6. 尋找 hello **IPAll**節點。  在 hello **TCP 連接埠**欄位中，輸入**1433年**。

          ![Configure SQL Express for TCP/IP][3]
   7. 按一下 [確定] 。  按一下**確定**hello 快顯對話方塊中。
   8. 按一下**SQL Server 服務**hello 左側的樹狀結構功能表中。
   9. 以滑鼠右鍵按一下 [SQL Server (SQLEXPRESS)]，然後選取 [重新啟動]
   10. 關閉 hello SQL Server 2014 組態管理員。
3. 執行 hello SQL Server 2014 Management Studio 並連接 tooyour 本機 SQL Express 執行個體

   1. 以滑鼠右鍵按一下您在 hello 物件總管 中的執行個體，然後選取**屬性**
   2. 選取 hello**安全性**頁面。
   3. 請確定 hello **SQL Server 及 Windows 驗證模式**選取
   4. 按一下 [檔案] &gt; [新增] &gt; [專案] 

          ![Configure SQL Express Authentication][4]
   5. 展開**安全性** > **登入**hello 物件總管 中
   6. 以滑鼠右鍵按一下 [登入]，然後選取 [新增登入...]
   7. 輸入登入名稱。  選取 [SQL Server 驗證] 。  輸入密碼，然後輸入 hello 相同密碼**確認密碼**。  hello 密碼必須符合 Windows 複雜性需求。
   8. 按一下 [檔案] &gt; [新增] &gt; [專案] 

          ![Add a new user tooSQL Express][5]
   9. 以滑鼠右鍵按一下新的登入，然後選取 [屬性] 
   10. 選取 hello**伺服器角色**頁面
   11. 檢查 hello 方塊的下一個 toohello **dbcreator**伺服器角色
   12. 按一下 [檔案] &gt; [新增] &gt; [專案] 
   13. 關閉 hello SQL Server 2015 Management Studio

請確定您記錄 hello 使用者名稱和您選取的密碼。  根據您特定資料庫的需求，您可能需要 tooassign 其他伺服器角色或權限。

hello Node.js 應用程式讀取 hello **SQLCONNSTR_MS_TableConnectionString** hello 這個資料庫的連接字串的環境變數。  您可以將該變數設定在環境中。  例如，您可以使用 PowerShell tooset 這個環境變數：

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

透過 TCP/IP 連接來存取 hello 資料庫和 hello 連線提供使用者名稱和密碼。

### <a name="howto-config-localdev"></a>作法：設定專案以在本機上進行開發
Azure 行動應用程式會讀取名為的 JavaScript 檔案*azureMobile.js*從 hello 本機檔案系統。  不使用在生產環境中的此檔案 tooconfigure hello Azure 行動應用程式 SDK-hello 內使用應用程式設定[Azure 入口網站]改為。  hello *azureMobile.js*檔案應該匯出的組態物件。  hello 最常見的設定如下：

* 資料庫設定
* 診斷記錄設定
* 替代 CORS 設定

範例*azureMobile.js*檔案實作 hello 前面資料庫設定如下所示：

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

我們建議您新增*azureMobile.js* tooyour *.gitignore*檔案 （或其他忽略檔案原始程式碼控制） tooprevent hello 雲端中儲存的密碼。  永遠設定實際執行應用程式設定內 hello [Azure 入口網站]。

### <a name="howto-appsettings"></a>作法：設定行動應用程式的應用程式設定
大部分的設定，在 hello *azureMobile.js*檔案具有對等的應用程式設定在 hello [Azure 入口網站]。  在應用程式設定中使用下列清單 tooconfigure hello 您的應用程式：

| 應用程式設定 | *azureMobile.js* 設定 | 說明 | 有效值 |
|:--- |:--- |:--- |:--- |
| **MS_MobileAppName** |名稱 |hello hello 應用程式名稱 |字串 |
| **MS_MobileLoggingLevel** |logging.level |最小的記錄層級的訊息 toolog |error、warning、info、verbose、debug、silly |
| **MS_DebugMode** |debug |啟用或停用偵錯模式 |true、false |
| **MS_TableSchema** |data.schema |SQL 資料表的預設結構描述名稱 |字串 (預設值：dbo) |
| **MS_DynamicSchema** |data.dynamicSchema |啟用或停用偵錯模式 |true、false |
| **MS_DisableVersionHeader** |版本 (組 tooundefined) |停用 hello X ZUMO-伺服器版本標頭 |true、false |
| **MS_SkipVersionCheck** |skipversioncheck |停用 hello 用戶端應用程式開發介面版本檢查 |true、false |

tooset 應用程式設定：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 hello 行動應用程式名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。 如果沒有，請按一下 [設定] 。
4. 按一下**應用程式設定**hello 一般功能表中。
5. 捲動 toohello 應用程式設定 區段。
6. 如果您的應用程式設定已存在，請按一下 hello 應用程式設定 tooedit hello 值 hello 值。
7. 如果您的應用程式設定不存在，請 hello 金鑰 方塊和 hello 值方塊中的 hello 值中輸入 hello 應用程式設定。
8. 完成後，按一下 [儲存] 。

變更大部分的應用程式設定都需要重新啟動服務。

### <a name="howto-use-sqlazure"></a>做法：使用 SQL Database 做為您的實際執行資料存放區
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

無論是何種 Azure App Service 應用程式類型，以 SQL Database 作為資料存放區的程序都是相同的。 如果您尚未執行此動作，請遵循這些步驟 toocreate 行動裝置應用程式後端。

1. 登入 toohello [Azure 入口網站]。
2. 在 [hello 左上方的 hello] 視窗中按一下 hello **+ 新增**按鈕 > **Web + 行動** > **行動裝置應用程式**，然後提供您的行動裝置應用程式後端的名稱。
3. 在 hello**資源群組**方塊中，輸入您的應用程式的名稱相同的 hello。
4. 選取 hello 預設應用程式服務計劃。  如果您想 toochange 您 App Service 方案，您可以按一下應用程式服務方案 hello > **+ 建立新**。  提供 hello 新的 App Service 方案的名稱，然後選取適當的位置。  按一下 hello 定價層，然後選取適當的定價層 hello 服務。 選取**檢視所有**tooview 多定價選項，例如**免費**和**共用**。  一旦您選取的定價層，按一下 hello**選取** 按鈕。  在 hello **App Service 方案**刀鋒視窗中，按一下 **確定**。
5. 按一下 [建立] 。 佈建行動應用程式後端可能需要幾分鐘。  Hello 入口網站 hello 行動裝置應用程式後端會佈建之後，開啟 hello**設定**hello 行動裝置應用程式後端的刀鋒視窗。

一旦建立 hello 行動裝置應用程式後端時，您可以選擇 tooeither 連接現有 SQL 資料庫 tooyour 行動裝置應用程式後端，或建立新的 SQL 資料庫。  在這一節中，您將建立 SQL Database。

> [!NOTE]
> 如果您已經有資料庫在 hello 與 hello 行動裝置應用程式後端相同的位置，您可以改為選擇**使用現有的資料庫**，然後選取該資料庫。 hello 使用不同的位置中的資料庫不會建議因為更高的延遲。
>
>

1. 在 hello 新行動裝置應用程式後端中，按一下 **設定** > **行動裝置應用程式** > **資料** > **+ 加**.
2. 在 hello**加入資料連接**刀鋒視窗中，按一下**SQL Database-必要的設定** > **建立新的資料庫**。  輸入 hello hello 新資料庫名稱在 hello**名稱**欄位。
3. 按一下 [伺服器] 。  在 hello**新的伺服器**刀鋒視窗中，在 hello 中輸入唯一的伺服器名稱**伺服器名稱**欄位，並提供適合**Server 系統管理員登入**和**密碼**.  請確定**允許 azure 服務 tooaccess 伺服器**已核取。  按一下 [確定] 。

    ![建立 Azure SQL Database][6]
4. 在 hello**新資料庫**刀鋒視窗中，按一下 **確定**。
5. 在 hello**加入資料連接**刀鋒視窗中，選取**連接字串**，輸入 hello 登入和建立 hello 資料庫時，您所提供的密碼。  如果您使用現有的資料庫時，提供該資料庫 hello 登入認證。  輸入完成後，按一下 [確定] 。
6. 在 hello**加入資料連接**刀鋒視窗中，按一下**確定**toocreate hello 資料庫。

<!--- END OF ALTERNATE INCLUDE -->

建立 hello 資料庫可能需要幾分鐘的時間。  使用 hello**通知**hello 部署的區域 toomonitor hello 進度。  不進行直到 hello 資料庫已成功部署。  已成功部署之後，為行動後端應用程式設定中的 hello SQL Database 執行個體建立連接字串。  您可以看到這個應用程式中的設定 hello**設定** > **應用程式設定** > **連接字串**。

### <a name="howto-tables-auth"></a>如何： 存取 tootables 要求進行驗證
如果您想與 hello 資料表端點 toouse 應用程式服務驗證，您必須設定應用程式服務驗證中 hello [Azure 入口網站]第一次。  在 Azure 應用程式服務中設定驗證的詳細檢閱 hello 身分識別提供者的設定指南 hello 想 toouse:

* [如何 tooconfigure Azure Active Directory 驗證]
* [如何 tooconfigure Facebook 驗證]
* [如何 tooconfigure Google 驗證]
* [如何 tooconfigure Microsoft 驗證]
* [如何 tooconfigure Twitter 驗證]

每個資料表都可以使用的 toocontrol 存取 toohello 資料表存取屬性。  hello 下列範例會顯示為需要驗證的靜態定義的資料表。

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

hello 存取屬性可以接受三個值的其中一個

* *匿名*表示 hello 用戶端應用程式允許未經驗證的 tooread 資料
* *驗證*指示 hello 用戶端應用程式必須傳送有效的驗證 token 與 hello 要求
* *disabled* 表示此資料表目前已停用

如果未定義 hello 存取屬性，則允許未驗證的存取。

### <a name="howto-tables-getidentity"></a>作法：透過資料表使用驗證宣告
您可以設定驗證設定時所要求的各種宣告。  這些宣告不是通常可透過 hello`context.user`物件。  不過，他們可以使用擷取 hello`context.user.getIdentity()`方法。  hello`getIdentity()`方法傳回的承諾，解析 tooan 物件。  hello 物件，做為驗證方法 （facebook、 google、 twitter、 microsoftaccount 或 aad） 索引鍵。

例如，如果您設定 Microsoft 帳戶驗證與要求 hello 電子郵件地址宣告時，您可以加入 hello 電子郵件地址 toohello 記錄以下列資料表控制器的 hello:

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

toosee 哪些宣告可供使用，使用 web 瀏覽器 tooview hello`/.auth/me`網站的端點。

### <a name="howto-tables-disabled"></a>如何： 停用存取 toospecific 資料表作業
加法 tooappearing hello 資料表上，在 hello 存取屬性可以使用的 toocontrol 個別作業。  共有四種作業：

* *讀取*hello RESTful 取得作業 hello 資料表
* *插入*hello 資料表 hello RESTful POST 作業
* *更新*hello RESTful 修補作業 hello 資料表
* *刪除*hello 資料表上的 hello RESTful 刪除作業

例如，您可能希望 tooprovide 唯讀未經驗證的資料表：

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <a name="howto-tables-query"></a>如何： 調整資料表作業所使用的 hello 查詢
資料表作業的共通需求是 tooprovide hello 資料的限制檢視。  例如，您可能會提供的資料表，則會標記為 hello 驗證使用者識別碼，使您可以只讀取或更新自己的記錄。  下列資料表定義的 hello 提供下列功能：

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

正常執行的查詢作業，擁有供您使用 Where 子句來調整的查詢屬性。 hello 查詢屬性是[QueryJS]物件，這個物件可以處理使用的 tooconvert hello 資料後端 OData 查詢 toosomething。  針對簡單的等號比較 （例如 hello 之前) 的情況下，可以使用對應。 您也可以新增特定的 SQL 子句︰

    context.query.where('myfield eq ?', 'value');

### <a name="howto-tables-softdelete"></a>作法：設定資料表上的虛刪除
虛刪除並不會實際刪除記錄。  而是它將其標記為藉由設定 hello 刪除資料行 tootrue hello 資料庫中刪除。  除非 hello 行動用戶端 SDK 使用 IncludeDeleted() hello Azure 行動應用程式 SDK 會自動從結果移除虛刪除的記錄。  tooconfigure 軟體的資料表刪除，請設定 hello `softDelete` hello 資料表定義檔中的屬性：

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

您應建立清除記錄的機制：從用戶端應用程式、透過 WebJob、Azure Function 或透過自訂 API。

### <a name="howto-tables-seeding"></a>做法：在您的資料庫中植入資料
當建立新的應用程式，您可能會想 tooseed 具有資料的資料表。  作法是在 hello 資料表定義 JavaScript 檔案，如下所示：

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

只有執行植入的資料，當 hello 資料表由 hello Azure 行動應用程式 SDK。  Hello 資料表已經存在 hello 資料庫內，如果沒有資料會插入 hello 資料表中。  如果已開啟動態結構描述，結構描述會推斷 hello 植入資料。

我們建議您明確地呼叫 hello`tables.initialize()`方法 toocreate hello 資料表 hello 服務開始執行時。

### <a name="Swagger"></a>作法：啟用 Swagger 支援
Azure App Service Mobile Apps 隨附內建 [Swagger] 支援。  tooenable Swagger 支援，請先安裝 hello swagger ui 做為相依性：

    npm install --save swagger-ui

安裝之後，您可以啟用 Swagger hello Azure 行動應用程式建構函式中的支援：

    var mobile = azureMobileApps({ swagger: true });

您可能只想 tooenable Swagger 版本所支援之開發。  您可以使用 `NODE_ENV` 應用程式設定來執行這項工作：

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

hello swagger 端點位於 http://*您的站台*.azurewebsites.net/swagger。  您可以存取透過 hello hello Swagger UI`/swagger/ui`端點。  如果您選擇 toorequire 驗證整個應用程式之間，Swagger 會產生錯誤。  為獲得最佳結果，選擇透過 tooallow 未經驗證的要求在 hello Azure 應用程式服務驗證 / 授權設定，然後控制驗證使用 hello`table.access`屬性。

您也可以加入 hello Swagger 選項 tooyour`azureMobile.js`檔案，如果您只想 Swagger 支援在本機開發時。

## <a name="a-namepushpush-notifications"></a><a name="push">推播通知
行動應用程式整合了 Azure 通知中樞 tooenable 您的裝置為目標的 toosend 推播通知 toomillions 跨所有主要平台。 藉由使用通知中樞，您可以傳送推播通知 tooiOS、 Android 和 Windows 裝置。 詳細資訊，您可以使用執行的 toolearn 通知中心，請參閱[通知中心概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。

### </a><a name="send-push"></a>作法：傳送推播通知
hello，下列程式碼顯示如何 toouse hello 推播物件 toosend 廣播推播通知 tooregistered iOS 裝置：

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

藉由建立範本的推播登錄從 hello 用戶端，您可以改為傳送所有支援的平台上的範本推播訊息 toodevices。 hello 下列程式碼會示範如何 toosend 範本通知：

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <a name="push-user"></a>如何： 傳送推播通知 tooan 驗證使用標記的使用者
當已驗證的使用者註冊推播通知時，使用者識別碼標籤會自動加入 toohello 註冊。 藉由使用此標記，您可以傳送推播通知 tooall 裝置已註冊的特定使用者。 hello 下列程式碼取得 hello 發出 hello 要求使用者的 SID，並將傳送範本推播通知 tooevery 裝置登錄該使用者：

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。

## <a name="CustomAPI"></a> 自訂 API
### <a name="howto-customapi-basic"></a>作法：定義自訂 API
此外 toohello 資料存取應用程式開發介面透過 hello /tables 端點，Azure 行動應用程式可以提供自訂應用程式開發介面的涵蓋範圍。  自訂 Api 類似的方式 toohello 資料表定義中所定義，而且可以存取所有 hello 相同的功能，包括驗證。

如果您想 toouse 具有自訂 API 的應用程式服務驗證，您必須設定應用程式服務驗證中 hello [Azure 入口網站]第一次。  在 Azure 應用程式服務中設定驗證的詳細檢閱 hello 身分識別提供者的設定指南 hello 想 toouse:

* [如何 tooconfigure Azure Active Directory 驗證]
* [如何 tooconfigure Facebook 驗證]
* [如何 tooconfigure Google 驗證]
* [如何 tooconfigure Microsoft 驗證]
* [如何 tooconfigure Twitter 驗證]

自訂 Api 會定義大致相同方式與 hello 資料表 API hello。

1. 建立 [api]  目錄。
2. 建立應用程式開發介面定義 JavaScript 檔案在 hello **api**目錄。
3. 使用 hello 匯入方法 tooimport hello **api**目錄。

以下是我們先前使用的 hello basic 應用程式範例為基礎的 hello 原型 api 定義。

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

我們以範例應用程式開發介面中傳回 hello 伺服器的日期使用 hello *Date.now()*方法。  以下是 hello api/date.js 檔案：

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

每一個參數的其中一個 hello 標準 RESTful 指令動詞為 GET、 POST、 PATCH 或 DELETE。  hello 方法是一種標準[ExpressJS 中介軟體]傳送 hello 所需的輸出函式。

### <a name="howto-customapi-auth"></a>如何： 存取 tooa 自訂 API 要求進行驗證
Azure 行動應用程式 SDK 實作驗證中 hello hello 表格端點和自訂應用程式開發介面的方式相同。  若要加入驗證 toohello API 開發 hello 前一節中，加入**存取**屬性：

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

您也可以指定特定作業的驗證：

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

hello 用於 hello 資料表端點的相同語彙基元必須用於需要驗證的自訂 Api。

### <a name="howto-customapi-auth"></a>作法：處理大型檔案上傳
Azure 行動應用程式 SDK 會使用 hello[主體剖析器中介軟體](https://github.com/expressjs/body-parser)tooaccept 及解碼您上傳的本文內容。  您可以預先設定的內文剖析器 tooaccept 較大的檔案上傳：

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

base 64 編碼傳輸之前 hello 檔案。  這會增加 hello hello 實際的上傳大小 （並因此 hello 必須負責的大小）。

### <a name="howto-customapi-sql"></a>作法：執行自訂 SQL 陳述式
hello Azure 行動應用程式 SDK 可讓存取 toohello hello 要求物件，透過整個內容 tooexecute 可讓您輕鬆地參數化 SQL 陳述式 toohello 定義的資料提供者：

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <a name="Debugging"></a>偵錯、簡單資料表及簡單的 API
### <a name="howto-diagnostic-logs"></a>作法：為 Azure Mobile Apps 偵錯、診斷和進行疑難排解
hello Azure 應用程式服務提供數個偵錯和疑難排解 Node.js 應用程式的技術。
請參閱下列文章 tooget 疑難排解 Node.js 行動後端啟動 toohello:

* [監視 Azure App Service]
* [在 Azure App Service 中啟用診斷記錄]
* [在 Visual Studio 中疑難排解 Azure App Service]

Node.js 應用程式可存取 tooa 各種不同的診斷記錄檔工具。  就內部而言，使用 Azure 行動應用程式 Node.js SDK 的 hello[邱吉爾]的診斷記錄。  記錄會自動啟用啟用偵錯模式，或設定 hello **MS_DebugMode** hello 中的應用程式設定 tootrue [Azure 入口網站]。 產生的記錄檔會出現在 hello 診斷記錄檔上 hello [Azure 入口網站]。

### <a name="in-portal-editing"></a><a name="work-easy-tables"></a>如何： 在 hello Azure 入口網站中使用簡單的資料表
Hello 入口網站中的簡單資料表可讓您建立和使用 hello 入口網站中的資料表權限。 您甚至可以編輯資料表作業使用 hello 應用程式服務的編輯器。

當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除資料表。 您也可以查看 hello 資料表中的資料。

![使用簡單資料表](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

hello 下列命令可在資料表的 hello 命令列上：

* **變更權限**-修改 hello 權限讀取、 插入、 更新及刪除 hello 資料表上的作業。
  選項為 tooallow 匿名存取、 toorequire 驗證或 toodisable 所有存取 toohello 作業。
* **編輯指令碼**-hello hello 資料表的指令碼檔案會在 hello 應用程式服務編輯器中開啟。
* **管理結構描述**-新增或刪除資料行或變更 hello 資料表索引。
* **清除資料表**-截斷現有的資料表不會刪除所有資料列，但又 hello 結構描述變更。
* **刪除資料列** - 刪除個別的資料列。
* **檢視資料流記錄**-將您連線 toohello 串流您的站台的記錄檔服務。

### <a name="work-easy-apis"></a>如何： 在 hello Azure 入口網站中使用簡單的應用程式開發介面
Hello 入口網站中的簡單 Api 可讓您建立和使用 hello 入口網站中的自訂 Api 權限。 您可以編輯應用程式開發介面使用 hello 應用程式服務編輯器的指令碼。

當您按一下後端網站設定中的 [簡單資料表]  時，可以新增、修改或刪除自訂 API 端點。

![使用簡單 API](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

在 hello 入口網站，您可以變更 hello 給定 HTTP 動作的存取權限、 編輯 hello API 指令碼檔案中的應用程式服務編輯器中，或是檢視 hello 串流記錄。

### <a name="online-editor"></a>如何： hello 應用程式服務編輯器中編輯程式碼
hello Azure 入口網站可讓您編輯 hello 應用程式服務編輯器中的 Node.js 後端指令碼檔案，而不必下載 hello 專案 tooyour 本機電腦。 tooedit hello 線上編輯器中的指令碼檔案：

1. 在您的「行動應用程式」後端刀鋒視窗中，按一下 [所有設定] > [簡單資料表] 或 [簡單 API]，按一下資料表或 API，然後按一下 [編輯指令碼]。 hello 應用程式服務編輯器中開啟 hello 指令碼檔案。

    ![App Service 編輯器](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. Hello 線上編輯器中，讓您變更 toohello 的程式碼檔案。 當您輸入資料時，會自動儲存變更。

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Android 用戶端快速入門]: app-service-mobile-android-get-started.md
[Apache Cordova 用戶端快速入門]: app-service-mobile-cordova-get-started.md
[iOS 用戶端快速入門]: app-service-mobile-ios-get-started.md
[Xamarin.iOS 用戶端快速入門]: app-service-mobile-xamarin-ios-get-started.md
[Xamarin.Android 用戶端快速入門]: app-service-mobile-xamarin-android-get-started.md
[Xamarin.Forms 用戶端快速入門]: app-service-mobile-xamarin-forms-get-started.md
[Windows 市集用戶端快速入門]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[離線的資料同步]: app-service-mobile-offline-data-sync.md
[如何 tooconfigure Azure Active Directory 驗證]: app-service-mobile-how-to-configure-active-directory-authentication.md
[如何 tooconfigure Facebook 驗證]: app-service-mobile-how-to-configure-facebook-authentication.md
[如何 tooconfigure Google 驗證]: app-service-mobile-how-to-configure-google-authentication.md
[如何 tooconfigure Microsoft 驗證]: app-service-mobile-how-to-configure-microsoft-authentication.md
[如何 tooconfigure Twitter 驗證]: app-service-mobile-how-to-configure-twitter-authentication.md
[Azure App Service 部署指南]: ../app-service-web/web-sites-deploy.md
[監視 Azure App Service]: ../app-service-web/web-sites-monitor.md
[在 Azure App Service 中啟用診斷記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md
[在 Visual Studio 中疑難排解 Azure App Service]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[指定 hello 節點版本]: ../nodejs-specify-node-version-azure-apps.md
[使用節點模組]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[Azure 入口網站]: https://portal.azure.com/
[OData]: http://www.odata.org
[承諾]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[GitHub 上的 basicapp 範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[GitHub 上的 todo 範例]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[GitHub 上的範例目錄]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js 封裝]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS 中介軟體]: http://expressjs.com/guide/using-middleware.html
[邱吉爾]: https://github.com/winstonjs/winston
