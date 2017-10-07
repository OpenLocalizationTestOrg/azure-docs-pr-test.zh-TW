---
title: "從行動服務 tooAzure 應用程式服務-Node.js aaaUpgrade"
description: "了解如何 tooeasily 升級您的行動服務應用程式 tooan App Service 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>升級您現有的 Node.js 的 Azure 行動服務 tooApp 服務
App Service Mobile 是新的方式 toobuild 行動應用程式使用 Microsoft Azure。 詳細資訊，請參閱 toolearn[行動應用程式是什麼？]。

本主題描述如何將現有 Node.js 後端應用程式從 Azure Mobile Services tooa tooupgrade 新的 App Service Mobile App。 當您執行此升級時，現有的行動服務應用程式可以繼續 toooperate。  如果您需要 tooupgrade Node.js 後端應用程式，請參閱太[升級您的.NET 行動服務](app-service-mobile-net-upgrading-from-mobile-services.md)。

升級的 tooAzure App Service 行動後端時，它有 App Service 功能且計費太根據存取 tooall[應用程式服務定價]、 定價不行動服務。

## <a name="migrate-vs-upgrade"></a>移轉與升級
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> 建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。 如此一來，您可以將您的應用程式的兩個版本上 hello 相同 App Service 方案，並會產生任何額外的成本。
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Mobile Apps Node.js 伺服器 SDK 中的改進功能
升級新 toohello[行動應用程式 SDK](https://www.npmjs.com/package/azure-mobile-apps)提供許多增強功能，包括：

* 根據 hello [Express framework](http://expressjs.com/en/index.html)，hello 新節點 SDK 是輕量且設計 tookeep 總，以新節點的版本為送。您可以自訂 hello Express 中介軟體的應用程式行為。
* 大幅改良效能比較 toohello 行動服務 SDK。
* 您現在可以在行動裝置的後端; 以及裝載網站同樣地，它是簡單 tooadd hello Azure Mobile SDK tooany 現有 express.v4 應用程式。
* 建置跨平台和本機程式開發，hello 行動應用程式 SDK 開發和本機 Windows、 Linux 及 OSX 平台上執行。 現在很容易 toouse 常見節點開發技術，如執行[Mocha](https://mochajs.org/)測試先前 toodeployment。

## <a name="overview"></a>基本升級概觀
tooaid 升級 Node.js 後端 Azure App Service 中的提供的相容性封裝。  升級之後，您必須使用 niew 站台，可以部署的 tooa 新應用程式服務的站台。

hello 行動服務用戶端 Sdk 是**不**與新行動裝置應用程式伺服器 hello SDK 相容。 在順序 tooprovide 服務連續性的應用程式，您不應該發行變更 tooa 站台目前正在服務已發佈的用戶端。 而是應該建立新的行動應用程式做為重複項目。 您可以將此應用程式相同的應用程式服務計劃在 hello tooavoid 產生額外的財務成本。

您將會讓 hello 應用程式的兩個版本： 一個維持相同 hello 和中 hello 普遍可已發佈的應用程式的另一個您可以接著升級和使用新的用戶端的目標版本。 您可以移動，或您的程式碼測試您的速度，但您應該確定您所做的任何 bug 修正取得套用的 tooboth。 一旦您認為不應在用戶端應用程式所需的數目有更新 toohello 最新版本，如果您想要您可以刪除 hello 原始移轉應用程式。 如果裝載於相同應用程式服務計劃做為您的行動裝置應用程式的 hello，它不會產生任何額外的金錢費用。

hello 完整大綱 hello 升級程序如下所示：

1. 下載您現有的 (已移轉) Azure 行動服務。
2. 轉換 hello 專案 tooan Azure 行動應用程式使用 hello 相容性封裝。
3. 更正任何差異 (例如驗證設定)。
4. 部署您已轉換的 Azure 行動應用程式專案 tooa 新應用程式服務。
5. 發行新版本的用戶端應用程式使用 hello 新的行動裝置應用程式。
6. (可省略) 刪除您已移轉的原始行動服務應用程式。

當已移轉的原始行動服務沒有任何流量時，就能加以刪除。

## <a name="install-npm-package"></a>安裝 hello 的必要元件
您應該在本機電腦上安裝 [節點]。  您也應該安裝 hello 相容性封裝。  節點安裝之後，您可以執行下列命令，從新的 cmd 或 PowerShell 命令提示字元的 hello:

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> 取得 Azure 行動服務指令碼
* 登入 toohello [Azure 入口網站]。
* 使用 [所有資源] 或 [應用程式服務]，尋找您的行動服務網站。
* 在 hello 網站中，按一下**工具** -> **Kudu** -> **移**tooopen hello Kudu 站台。
* 按一下**偵錯主控台** -> **PowerShell** tooopen hello 偵錯主控台。
* 瀏覽過`site/wwwroot/App_Data/config`依次按一下每個目錄
* 按一下 hello 下載圖示下一步 toohello`scripts`目錄。

這會下載 ZIP 格式中的 hello 指令碼。  在本機電腦上建立新的目錄，並解壓縮 hello `scripts.ZIP` hello 目錄內的檔案。  這會建立 `scripts` 目錄。

## <a name="scaffold-app"></a>Scaffold hello 新的 Azure 行動應用程式後端
執行下列命令，從包含 hello 指令碼目錄 hello 目錄 hello:

```scaffold-mobile-app scripts out```

這會建立 scaffold 的 Azure 行動應用程式後端中 hello`out`目錄。  雖然並非必要，是個不錯的主意 toocheck hello`out`到來源的程式碼儲存機制，您所選擇的目錄。

## <a name="deploy-ama-app"></a> 部署 Azure Mobile Apps 後端
在部署期間，您將需要 toodo hello 下列：

1. 建立新的行動裝置應用程式在 hello [Azure 入口網站]。
2. 執行 hello`createViews.sql`連接的資料庫上的指令碼。
3. 連結 hello 資料庫連結的 tooyour 行動服務 tooyour 新應用程式服務。
4. 連結任何其他資源 （例如通知中樞） toohello 新應用程式服務。
5. 部署 hello 產生程式碼 tooyour 新站台。

### <a name="create-a-new-mobile-app"></a>建立新的行動 App
1. 在 hello 登入[Azure 入口網站]。
2. 按一下 [+ 新增]  >  [Web + 行動]  >  [行動應用程式]，然後為您的行動應用程式後端提供名稱。
3. Hello**資源群組**，選取現有的資源群組，或建立新的 (使用 hello 與您的應用程式同名)。

    您可以選取另一個 App Service 方案或建立新方案。 如需詳細資訊，應用程式服務計劃和如何 toocreate 新計劃中不同的定價層，然後在您想要的位置，請參閱[Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。
4. Hello **App Service 方案**，hello 預設計劃 (在 hello[標準層](https://azure.microsoft.com/pricing/details/app-service/)) 已選取。 您也可以選取不同的方案，或[建立新的方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan)。 hello 應用程式服務方案設定會決定 hello[位置、 功能、 成本及計算資源](https://azure.microsoft.com/pricing/details/app-service/)與您的應用程式相關聯。

    當您決定 hello 計劃之後，請按一下**建立**。 這會建立 hello 行動裝置應用程式後端。

### <a name="run-createviewssql"></a>執行 CreateViews.SQL
hello scaffold 應用程式包含檔案，稱為`createViews.sql`。  您必須對目標資料庫執行這個指令碼。  hello hello 目標資料庫的連接字串可以取自您移轉的行動服務，從 hello**設定**刀鋒視窗底下**連接字串**。  其名稱為 `MS_TableConnectionString`。

您可以從 SQL Server Management Studio 或 Visual Studio 內執行這個指令碼。

### <a name="link-hello-database-tooyour-app-service"></a>連結 hello 資料庫 tooyour 應用程式服務
連結現有資料庫 tooyour hello 應用程式服務：

* 在 hello [Azure 入口網站]，開啟您的應用程式服務。
* 選取 [所有設定] -> [資料連接]。
* 按一下 [+ 新增] 。
* 在 hello 下拉式清單中，選取  **SQL 資料庫**
* 在 [SQL Database] 底下選取現有資料庫，然後按一下 [選取]。
* 在下**連接字串**、 輸入 hello 資料庫 hello 使用者名稱和密碼，然後按一下**確定**。
* 在 hello**加入資料連接**刀鋒視窗中，按一下 **確定**。

可以藉由檢視移轉的行動服務中的 hello 目標資料庫的連接字串 hello 找到 hello 使用者名稱和密碼。

### <a name="set-up-authentication"></a>設定驗證
Azure 行動應用程式可讓您 tooconfigure hello 服務內的 Azure Active Directory、 Facebook、 Google、 Microsoft 及 Twitter 驗證。  Toobe 個別開發時，就需要自訂的驗證。  請參閱 hello[驗證概念]文件和[驗證快速入門]文件的詳細資訊。  

## <a name="updating-clients"></a>更新行動用戶端
在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。 行動應用程式也包含新版 hello client Sdk，以及類似的 toohello server 升級上方，您將需要的 tooremove toohello 行動服務 Sdk 之前的所有參照安裝行動應用程式版本。

其中一個 hello hello 版本之間的主要變更是 hello 建構函式不再需要應用程式金鑰。
您現在只需傳入 hello 行動應用程式的 URL。 例如，在 hello.NET 用戶端，hello`MobileServiceClient`建構函式現在是：

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

您可以閱讀安裝 hello 新 Sdk，並使用 hello 透過以下的 hello 連結新的結構：

* [Android 2.2 版或更新版本](app-service-mobile-android-how-to-use-client-library.md)
* [iOS 3.0.0 版或更新版本](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) 2.0.0 版或更新版本](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova 2.0 版或更新版本](app-service-mobile-cordova-how-to-use-client-library.md)

如果您的應用程式更能使用推播通知，請記下 hello 特定註冊指示每個平台，已有一些變更有以及。

當您擁有 hello 新用戶端版本準備好時，現在就試試看對您已升級的伺服器專案。 驗證它運作之後，您可以釋放您的應用程式 toocustomers 的新版本。 最後，一旦您的客戶有機會 tooreceive 這些更新，您可以刪除 hello 行動服務應用程式版本。 此時，您完全升級 tooan App Service 行動應用程式使用最新版行動應用程式伺服器 hello SDK。

<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[行動應用程式是什麼？]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[應用程式服務定價]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[驗證概念]: ../app-service/app-service-authentication-overview.md
[驗證快速入門]: app-service-mobile-auth.md

[Azure 入口網站]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
