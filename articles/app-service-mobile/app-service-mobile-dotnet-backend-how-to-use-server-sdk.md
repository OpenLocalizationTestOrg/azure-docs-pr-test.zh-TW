---
title: "與 hello.NET 後端伺服器的行動應用程式 SDK 的 aaaHow toowork |Microsoft 文件"
description: "了解如何與 toowork hello Azure App Service 行動應用程式的.NET 後端伺服器 SDK。"
keywords: "App Service, Azure App Service, 行動應用程式, 行動服務, 調整, 可調整, 應用程式部署, Azure 應用程式部署"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>可搭配 hello.NET 後端伺服器 SDK 用於 Azure 行動應用程式
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

本主題說明如何 toouse hello Azure App Service 行動應用程式的重要案例中的.NET 後端伺服器 SDK。 hello Azure 行動應用程式 SDK，可協助您使用從您的 ASP.NET 應用程式的行動用戶端。

> [!TIP]
> hello [.NET server 的 Azure 行動應用程式 SDK] [ 2]是開放原始碼 GitHub 上的。 hello 儲存機制] 含有包括 hello 整部伺服器 SDK 的單元測試套件和某些範例專案的所有原始程式碼。
>
>

## <a name="reference-documentation"></a>參考文件
hello hello server SDK 的參考文件集位於此處： [Azure 行動應用程式的.NET 參考][1]。

## <a name="create-app"></a>作法：建立 .NET 行動應用程式後端
如果您要啟動新的專案，您可以建立 App Service 應用程式使用任一 hello [Azure 入口網站]或 Visual Studio。 您可以在本機執行 hello App Service 應用程式，或發行 hello 專案 tooyour 雲端 App Service 行動應用程式。

如果您要加入行動功能 tooan 現有專案，請參閱 hello[下載，並初始化 hello SDK](#install-sdk) > 一節。

### <a name="create-a-net-backend-using-hello-azure-portal"></a>建立.NET 後端使用 hello Azure 入口網站
toocreate App Service 行動後端，請遵循 hello[快速入門教學課程][ 3]或遵循下列步驟：

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

在 [hello*開始*刀鋒視窗底下**建立資料表 API**，選擇**C#**做為您**後端語言**。 按一下**下載**、 擷取壓縮的專案檔案 tooyour 本機電腦，並在 Visual Studio 中開啟 hello 方案。

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>使用 Visual Studio 2013 和 Visual Studio 2015 建立 .NET 後端
安裝 hello [Azure SDK for.NET] [ 4] (2.9.0 版本或更新版本) toocreate Visual Studio 中的 Azure 行動應用程式專案。 一旦您已安裝 hello SDK，建立 ASP.NET 應用程式使用 hello 下列步驟：

1. 開啟 hello**新專案**對話方塊 (從*檔案* > **新增** > **專案...**).
2. 展開 [範本] > [Visual C#]，然後選取 [Web]。
3. 選取 [ASP.NET Web 應用程式] 。
4. 填寫 hello 專案名稱。 然後按一下 [確定] 。
5. 在 [ASP.NET 4.5.2 範本] 底下，選取 [Azure 行動應用程式]。 請檢查**hello 雲端中的主機**toocreate 行動後端中 hello 雲端 toowhich 可以發行這個專案。
6. 按一下 [確定] 。

## <a name="install-sdk"></a>如何： 下載並初始化 hello SDK
hello 是否可以使用 SDK [NuGet.org]。此套件包含 hello 所需的基底功能 tooget 開始使用 hello SDK。 tooinitialize hello SDK，您需要在 hello tooperform 動作**HttpConfiguration**物件。

### <a name="install-hello-sdk"></a>安裝 SDK hello
tooinstall hello SDK，以滑鼠右鍵按一下 hello 伺服器專案，在 Visual Studio 中，選取**管理 NuGet 封裝**，搜尋 hello [Microsoft.Azure.Mobile.Server]封裝，然後按一下 [ **安裝**。

### <a name="server-project-setup"></a>初始化 hello 伺服器專案
.NET 後端伺服器專案是初始化類似 tooother ASP.NET 專案，包括 OWIN 啟動類別。 請確認您擁有參考 hello NuGet 封裝`Microsoft.Owin.Host.SystemWeb`。 tooadd 這個類別，在 Visual Studio 中，以滑鼠右鍵按一下您的伺服器專案並選取**新增** >
**新項目**，然後**Web**  >  **一般** > **OWIN 啟動 「 類別**。  類別會產生以 hello 下列屬性：

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

在 [hello`Configuration()`您 OWIN 啟動類別方法，使用**HttpConfiguration**物件 tooconfigure hello Azure 行動應用程式環境。
下列範例中的 hello 初始化 hello 伺服器專案，沒有新增的功能：

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable 個別功能，您必須呼叫擴充方法 hello **MobileAppConfiguration**物件之前先呼叫**ApplyTo**。 例如，下列程式碼的 hello 加入 hello 預設路由傳送的 hello 屬性 tooall API 控制器`[MobileAppController]`初始化期間：

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

從 hello 伺服器快速入門 hello Azure 入口網站呼叫**UseDefaultConfiguration()**。 安裝此對等 toohello:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

使用的 hello 擴充方法是：

* `AddMobileAppHomeController()`提供 hello 預設 Azure 行動應用程式的首頁。
* `MapApiControllers()`提供自訂 API 功能以 hello 裝飾 WebAPI 控制器`[MobileAppController]`屬性。
* `AddTables()`提供的 hello 對應`/tables`端點 tootable 控制站。
* `AddTablesWithEntityFramework()`是對應 hello 速記`/tables`使用 Entity Framework 的端點基礎控制站。
* `AddPushNotifications()` 提供向通知中樞註冊裝置的簡單方法。
* `MapLegacyCrossDomainController()` 提供用於本機開發的標準 CORS 標頭。

### <a name="sdk-extensions"></a>SDK 延伸模組
下列 NuGet 基礎的擴充功能封裝 hello 提供各種可供您的應用程式的行動裝置功能。 在初始化期間啟用擴充功能使用 hello **MobileAppConfiguration**物件。

* [Microsoft.Azure.Mobile.Server.Quickstart]支援 hello 基本的行動應用程式安裝程式。 組態設定加入的 toohello 呼叫 hello **UseDefaultConfiguration**初始化期間的擴充方法。 此擴充包含下列擴充功能：通知、驗證、實體、資料表、跨網域和首頁封裝。 此套件會使用 hello hello Azure 入口網站上的行動應用程式快速入門。
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/)實作 hello 預設*此行動裝置應用程式已啟動並執行頁面*hello 網站根目錄。 藉由呼叫加入 toohello 組態**AddMobileAppHomeController**擴充方法。
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/)包括資料和設定總 hello 資料管線中的類別。 加入呼叫 hello toohello 組態**AddTables**擴充方法。
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/)啟用 hello SQL Database 中的 hello Entity Framework tooaccess 資料。 加入呼叫 hello toohello 組態**AddTablesWithEntityFramework**擴充方法。
* [Microsoft.Azure.Mobile.Server.Authentication]啟用驗證並設定總 hello OWIN 中介軟體使用 toovalidate 語彙基元。 加入呼叫 hello toohello 組態**AddAppServiceAuthentication**和**IAppBuilder**。**UseAppServiceAuthentication**擴充方法。
* [Microsoft.Azure.Mobile.Server.Notifications] 啟用推播通知，並定義推播註冊端點。 加入呼叫 hello toohello 組態**AddPushNotifications**擴充方法。
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/)會建立可從您的行動裝置應用程式的網頁瀏覽器做資料 toolegacy 控制站。 藉由呼叫加入 toohello 組態**MapLegacyCrossDomainController**擴充方法。
* [Microsoft.Azure.Mobile.Server.Login]提供 hello AppServiceLoginHandler.CreateToken() 方法，這是自訂的驗證案例期間使用的靜態方法。

## <a name="publish-server-project"></a>如何： 將 hello 伺服器專案發行
本節說明如何 toopublish.NET 後端專案從 Visual Studio。 您也可以部署您的後端專案使用 Git 或任一 hello hello 中涵蓋的其他方法[Azure App Service 部署文件](../app-service-web/web-sites-deploy.md)。

1. 在 Visual Studio 中，重建 hello 專案 toorestore NuGet 封裝。
2. 在 [方案總管] 中，以滑鼠右鍵按一下 hello 專案中，按一下 [**發行**。 hello 第一次發行時，您需要 toodefine 發行設定檔。 在定義設定檔後，您可以選取該設定檔，然後按一下 [發佈]。
3. 如果系統詢問 tooselect 發行目標，請按一下**Microsoft Azure App Service** > **下一步**，（如果需要），然後使用您的 Azure 認證登入。
   Visual Studio 會直接從 Azure 下載並安全地儲存您的發佈設定。

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. 選擇您的 [訂用帳戶]，從 [檢視] 中選取 [資源類型]，展開 [行動應用程式]，按一下您的行動應用程式後端，然後按一下 [確定]。

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. 確認 hello 發行設定檔資訊，然後按一下**發行**。

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    當您的行動應用程式後端已成功發佈後，您會看到表示成功的登陸頁面。

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a> 做法：定義資料表控制器
定義資料表控制器 tooexpose SQL 資料表 toomobile 用戶端。  設定資料表控制器需要三個步驟︰

1. 建立資料傳輸物件 (DTO) 類別。
2. Hello 行動 DbContext 類別中設定的資料表參考。
3. 建立資料表控制器。

資料傳輸物件 (DTO) 是繼承自 `EntityData`純 C# 物件。  例如：

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

hello DTO 是使用的 toodefine hello SQL database 中的 hello 資料表。  toocreate hello 資料庫項目，加入`DbSet<>`hello DbContext 您使用的屬性。  在 [hello 預設 Azure 行動應用程式的專案範本，hello DbContext 稱為`Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

如果您擁有的 hello 安裝 Azure SDK，您現在可以建立範本資料表控制器，如下所示：

1. Hello 控制器] 資料夾上按一下滑鼠右鍵，然後選取**新增** > **控制器...**.
2. 選取 hello **Azure 行動應用程式資料表控制器**選項，然後按一下 [**新增**。
3. 在 [hello**加入控制器**對話方塊：
   * 在 [hello**模型類別**下拉式清單中，選取您新 DTO。
   * 在 [hello **DbContext**下拉式清單中，選取 hello 行動服務 DbContext 類別。
   * 為您建立 hello 控制器名稱。
4. 按一下 [新增] 。

hello 快速入門伺服器專案包含簡單的範例**TodoItemController**。

### <a name="adjust-pagesize"></a>如何： 調整 hello 表格分頁大小
根據預設，Azure Mobile Apps 針對每個要求會傳回 50 個記錄。  分頁可確保該 hello 用戶端不會不佔用太久，其 UI 執行緒，也不 hello 伺服器確保良好的使用者經驗。 toochange hello 資料表分頁大小增加 hello 伺服器端 「 允許查詢大小 」 和 hello 「 允許查詢大小 」 的用戶端頁面大小 hello 伺服器端會調整使用 hello`EnableQuery`屬性：

    [EnableQuery(PageSize = 500)]

確定 hello PageSize hello 相同或大於 hello hello 用戶端要求的大小。  如需變更 hello 用戶端頁面大小的詳細資訊，請參閱 toohello 特定用戶端如何文件。

## <a name="how-to-define-a-custom-api-controller"></a>做法：定義自訂 API 控制器
自訂 API 控制器 hello 提供 hello 最基本功能 tooyour 行動裝置應用程式後端所公開的端點。 您可以註冊行動裝置特定 API 控制器會使用 hello [MobileAppController] 屬性。 hello`MobileAppController`屬性註冊 hello 路由、 設定 hello 行動應用程式的 JSON 序列化程式，並開啟[用戶端版本檢查](app-service-mobile-client-and-server-versioning.md)。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello Controllers 資料夾，然後按一下 [**新增** > **控制器**，選取**Web API 2 控制器&mdash;空**和按一下**新增**。
2. 提供 [控制器名稱] \(例如 `CustomController`)，然後按一下 [新增]。
3. 在 [hello 新控制器的類別檔案，加入 [hello 下列 using 陳述式：

        using Microsoft.Azure.Mobile.Server.Config;
4. 套用 hello **[MobileAppController]**屬性 toohello API 控制器類別定義，如 hello 下列範例所示：

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. App_Start/Startup.MobileApp.cs 檔案中加入呼叫 toohello **MapApiControllers**擴充方法，如 hello 下列範例所示：

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

您也可以使用 hello`UseDefaultConfiguration()`擴充方法，而不是`MapApiControllers()`。 用戶端仍然可以存取任何沒有套用 **MobileAppControllerAttribute** 的控制器，但是使用任何行動應用程式用戶端 SDK 的用戶端可能會無法正確取用。

## <a name="how-to-work-with-authentication"></a>做法：使用驗證
Azure 行動應用程式會使用應用程式服務驗證 / 授權 toosecure 行動後端。  這個區段會顯示如何 tooperform hello 下列驗證相關的工作，在.NET 後端伺服器專案中：

* [如何： 加入驗證 tooa 伺服器專案](#add-auth)
* [做法：針對應用程式使用自訂驗證](#custom-auth)
* [做法：取出已驗證的使用者資訊](#user-info)
* [做法︰限制授權使用者的資料存取](#authorize)

### <a name="add-auth"></a>如何： 加入驗證 tooa 伺服器專案
您可以新增驗證 tooyour 伺服器專案延伸 hello **MobileAppConfiguration**物件和設定 OWIN 中介軟體。 當您安裝 hello [Microsoft.Azure.Mobile.Server.Quickstart]封裝並呼叫 hello **UseDefaultConfiguration**擴充方法，您可以略過 toostep 3。

1. 在 Visual Studio 安裝 hello [Microsoft.Azure.Mobile.Server.Authentication]封裝。
2. 在 hello Startup.cs 專案檔案中，加入下列一行程式碼在 hello hello 開頭的 hello**組態**方法：

        app.UseAppServiceAuthentication(config);

    此 OWIN 中介軟體元件驗證相關聯的 hello App Service 閘道所發行的權杖。
3. 新增 hello`[Authorize]`屬性 tooany 控制器或需要驗證的方法。

有關如何 toolearn tooauthenticate 用戶端 tooyour 行動應用程式後端，請參閱[新增 authentication tooyour 應用程式](app-service-mobile-ios-get-started-users.md)。

### <a name="custom-auth"></a>做法：針對應用程式使用自訂驗證
如果您不想 toouse 其中一個 hello 應用程式服務驗證/授權提供者，您可以實作自己的登入系統。 安裝 hello [Microsoft.Azure.Mobile.Server.Login]封裝 tooassist 與驗證權杖產生。  提供您自己的程式碼來驗證使用者認證。 例如，您可以針對資料庫中的 salted 和雜湊密碼進行檢查。 Hello 下列範例中，在 hello `isValidAssertion()` （其他地方定義） 的方法會負責這些檢查。

hello 自訂驗證由建立 ApiController，而且已公開`register`和`login`動作。 hello 用戶端應該使用 hello 使用者自訂 UI toocollect hello 資訊。  hello 資訊是透過標準的 HTTP POST 送出的 toohello API 呼叫。 一旦 hello 伺服器驗證 hello 判斷提示，在核發權杖使用 hello`AppServiceLoginHandler.CreateToken()`方法。  hello ApiController**不應該**使用 hello`[MobileAppController]`屬性。

範例 `login` 動作︰

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

在上述範例中的 hello，LoginResult 和 LoginResultUser 是可序列化的物件公開的必要的屬性。 hello 用戶端必須要有登入回應 toobe 傳回為 hello 表單的 JSON 物件：

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

hello`AppServiceLoginHandler.CreateToken()`方法包含*觀眾*和*簽發者*參數。 這兩個參數會設定 toohello 使用 hello HTTPS 配置的應用程式根目錄 URL。 同樣地，您應該設定*secretKey* toobe hello 值，您的應用程式的簽署金鑰。 不要散發 hello 簽署金鑰，用戶端中的，它可以是使用的 toomint 索引鍵，並模擬使用者。 您可以取得簽署金鑰時所參考 hello 裝載的應用程式服務的 hello*網站\_AUTH\_簽署\_金鑰*環境變數。 如果需要在本機偵錯內容中，請遵循 hello 中的 hello 指示[本機偵錯工具驗證](#local-debug)區段 tooretrieve hello 金鑰並將它儲存為應用程式設定。

其他宣告和到期日，也可能包括 hello 發出權杖。  Hello 發行權杖必須至少包含主旨 (**sub**) 宣告。

您可以支援標準用戶端 hello`loginAsync()`透過 hello 驗證路由的多載的方法。  如果 hello 用戶端呼叫`client.loginAsync('custom');`toolog 中的，您的路由必須`/.auth/login/custom`。  您可以設定 hello 路由 hello 自訂驗證控制器使用`MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> 使用 hello`loginAsync()`方法可確保該 hello 驗證語彙基元會附加 tooevery 後續呼叫 toohello 服務。
>
>

### <a name="user-info"></a>做法：取出已驗證的使用者資訊
當使用者驗證應用程式服務時，您可以存取 hello 分派使用者識別碼和在.NET 後端程式碼中的其他資訊。 hello 使用者資訊可以用於在 hello 後端進行授權決策。 hello 下列程式碼會取得 hello 與要求相關聯的使用者識別碼：

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

hello SID 衍生自 hello 特定提供者使用者識別碼，而且是靜態的給定的使用者和登入提供者。  hello SID 是無效的驗證權杖則為 null。

App Service 也可讓您向登入提供者要求特定宣告。 每個識別提供者均可使用識別提供者 SDK 來提供更多資訊。  例如，您可以使用 hello Facebook 圖形 API 的朋友的資訊。  您可以指定要求的宣告在 hello hello Azure 入口網站中的提供者] 刀鋒視窗。 某些宣告需要 hello 身分識別提供者的其他設定。

hello 下列程式碼呼叫 hello **GetAppServiceIdentityAsync**延伸方法 tooget hello 登入認證，包括對 hello Facebook 圖形 API 的 hello 存取權杖需要的 toomake 要求：

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

加入 using 陳述式`System.Security.Principal`tooprovide hello **GetAppServiceIdentityAsync**擴充方法。

### <a name="authorize"></a>做法︰限制授權使用者的資料存取
Hello 前一節，我們也示範了如何 tooretrieve hello 已驗證使用者的使用者識別碼。 您可以限制存取 toodata 及其他資源，根據此值。 例如，新增使用者識別碼資料行 tootables 和篩選 hello 使用者識別碼 hello 查詢結果是傳回的資料只有 tooauthorized 使用者簡單的方式 toolimit。 hello 下列程式碼時，傳回資料列只 hello SID 符合 hello hello TodoItem 資料表上的使用者識別碼資料行中的值：

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

hello`Query()`方法會傳回`IQueryable`，可由 LINQ toohandle 篩選操作。

## <a name="how-to-add-push-notifications-tooa-server-project"></a>如何： 加入推播通知 tooa 伺服器專案
新增推播通知 tooyour 伺服器專案延伸 hello **MobileAppConfiguration**物件及建立通知中樞的用戶端。

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello 伺服器專案，然後按一下**管理 NuGet 封裝**，搜尋`Microsoft.Azure.Mobile.Server.Notifications`，然後按一下 [**安裝**。
2. 重複此步驟 tooinstall hello`Microsoft.Azure.NotificationHubs`封裝，其中包含 hello 通知中樞的用戶端程式庫。
3. 在 App_Start/Startup.MobileApp.cs，並加入呼叫 toohello **AddPushNotifications()**初始化期間的擴充方法：

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. 加入下列程式碼會建立通知中樞的用戶端 hello:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

您現在可以使用 hello 通知中樞的用戶端 toosend 推播通知 tooregistered 裝置。 如需詳細資訊，請參閱[新增推播通知 tooyour 應用程式](app-service-mobile-ios-get-started-push.md)。 toolearn 深入了解通知中心，請參閱[通知中心概觀](../notification-hubs/notification-hubs-push-notification-overview.md)。

## <a name="tags"></a>作法：使用標籤啟用有目標的推播
通知中樞可讓您透過使用標記 toospecific 註冊傳送目標的通知。 自動建立數個標籤︰

* hello 安裝識別碼會識別特定的裝置。
* hello 使用者 Id 根據已驗證的 hello SID 來識別特定的使用者。

hello 的安裝識別碼可從 hello **installationId**屬性 hello **MobileServiceClient**。  hello 下列範例示範如何使用安裝識別碼 tooadd 標記 tooa 特定安裝在通知中樞：

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Hello 後端建立 hello 安裝時，會忽略任何推播通知登錄期間 hello 用戶端所提供的標記。 用戶端 tooadd tooenable 標記 toohello 安裝，您必須建立自訂 API 中，加入標記使用 hello 前面模式。

請參閱[用戶端新增推播通知標記][ 5]在 hello App Service 行動應用程式已完成的快速入門範例中的範例。

## <a name="push-user"></a>如何： 傳送推播通知 tooan 驗證的使用者
當已驗證的使用者註冊推播通知時，使用者識別碼標籤會自動加入 toohello 註冊。 藉由使用此標記，您可以傳送推播通知 tooall 裝置已註冊該人員。 hello 下列程式碼取得 hello 提出要求的使用者的 SID，並將傳送範本推播通知 tooevery 裝置登錄該人員：

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

在註冊來自已驗證用戶端的推播通知時，請確定驗證已完成，然後再嘗試註冊。 如需詳細資訊，請參閱[推送 toousers] [ 6] hello App Service 行動應用程式已完成的快速入門範例.NET 後端中。

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>如何： 偵錯和疑難排解 hello.NET 伺服器 SDK
Azure App Service 提供了數個適用於 ASP.NET 應用程式的偵錯和疑難排解技術：

* [監視 Azure App Service](../app-service-web/web-sites-monitor.md)
* [在 Azure App Service 中啟用診斷記錄](../app-service-web/web-sites-enable-diagnostic-log.md)
* [在 Visual Studio 中疑難排解 Azure App Service](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>記錄
您可以使用標準 ASP.NET 追蹤寫入 hello 撰寫 tooApp 服務診斷記錄檔。 您可以撰寫 toohello 記錄檔之前，您必須在您的行動裝置應用程式後端啟用診斷。

tooenable 診斷和寫入 toohello 記錄檔：

1. 中的 hello 步驟[如何 tooenable 診斷](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)。
2. 將 hello 面一行加入程式碼檔中使用陳述式：

        using System.Web.Http.Tracing;
3. 建立追蹤寫入器 toowrite hello.NET 後端 toohello 診斷記錄檔，如下所示：

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. 重新發佈您的伺服器專案，而且存取 hello 行動裝置應用程式後端 tooexecute hello 程式碼路徑與 hello 記錄。
5. 下載並評估 hello 記錄中所述[How to： 下載記錄檔](../app-service-web/web-sites-enable-diagnostic-log.md#download)。

### <a name="local-debug"></a>使用驗證進行本機偵錯
您可以執行您的應用程式本機 tootest 變更之前發佈 toohello 雲端。 對於大部分的 Azure Mobile Apps 後端，請在Visual Studio 中時按 F5  。 不過，使用驗證時有一些其他考量。

您必須擁有雲端式行動裝置應用程式與應用程式服務驗證/授權設定，而且您的用戶端必須指定 hello 替代登入主控件以 hello 雲端端點。 請參閱 hello 文件以 hello 所需的特定步驟為您用戶端平台。

確定您的行動後端已安裝 [Microsoft.Azure.Mobile.Server.Authentication] 。 然後，在您的應用程式 OWIN 啟動類別中，加入 hello 下列程式碼之後,`MobileAppConfiguration`已套用的 tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

在上述範例中的 hello，您應該設定 hello *authAudience*和*authIssuer* Web.config 中的應用程式設定檔 tooeach 是應用程式根目錄的 URL 使用 hello HTTPS配置。 同樣地，您應該設定*authSigningKey* toobe hello 值，您的應用程式的簽署金鑰。
tooobtain hello 簽署金鑰：

1. 瀏覽 tooyour 應用程式內 hello [Azure 入口網站]
2. 按一下 [工具]、[Kudu]、[執行]。
3. 在 hello Kudu 管理入口網站中，按一下 [**環境**。
4. 尋找 hello 值*網站\_AUTH\_簽署\_金鑰*。

使用簽署金鑰 hello 的 hello *authSigningKey*本機應用程式組態中的參數。您的行動裝置後端現在已備妥的 toovalidate 語彙基元時，在本機執行 hello 的用戶端會從 hello 以雲端為基礎的端點來取得 hello 語彙基元。

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure 入口網站]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
