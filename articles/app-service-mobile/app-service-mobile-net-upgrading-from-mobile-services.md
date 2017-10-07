---
title: "aaaUpgrade 從行動服務 tooAzure 應用程式服務"
description: "了解如何 tooeasily 升級您的行動服務應用程式 tooan App Service 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>升級您現有的.NET 的 Azure 行動服務 tooApp 服務
App Service Mobile 是新的方式 toobuild 行動應用程式使用 Microsoft Azure。 詳細資訊，請參閱 toolearn[行動應用程式是什麼？]。

本主題描述如何 tooupgrade 現有的.NET 後端應用程式從 Azure Mobile Services tooa 新應用程式服務的行動應用程式。 當您執行此升級時，現有的行動服務應用程式可以繼續 toooperate。   如果您需要 tooupgrade Node.js 後端應用程式，請參閱太[升級您的 Node.js 行動服務](app-service-mobile-node-backend-upgrading-from-mobile-services.md)。

升級的 tooAzure App Service 行動後端時，它有 App Service 功能且計費太根據存取 tooall[應用程式服務定價]、 定價不行動服務。

## <a name="migrate-vs-upgrade"></a>移轉與升級
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> 建議您在升級之前，先 [執行移轉](app-service-mobile-migrating-from-mobile-services.md) 。 如此一來，您可以將您的應用程式的兩個版本上 hello 相同 App Service 方案，並會產生任何額外的成本。
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Mobile Apps .NET 伺服器 SDK 中的增強功能
升級新 toohello[行動應用程式 SDK](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)提供下列優點 hello:

* NuGet 相依性有更多彈性。 不再裝載環境的 hello 提供它自己版本的 NuGet 封裝，因此您可以使用替代的相容版本。 不過，如果有新的重大 bugfixes 或安全性更新 toohello Mobile 伺服器 SDK 的相依性，您必須手動更新您的服務。
* 更具彈性的 hello 行動 SDK。 您可以明確地控制哪些功能，和路由設定，例如驗證時，資料表的 Api，且會 hello 推播註冊端點。 詳細資訊，請參閱 toolearn[如何 toouse hello Azure 行動應用程式的.NET 伺服器 SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md)。
* 支援其他 ASP.NET 專案類型和路由。 您現在可以為您的行動裝置的後端專案裝載 MVC 和 Web API 控制器 hello 相同專案中。
* 支援新的應用程式服務驗證功能，可讓您的 web 和行動裝置應用程式之間的 toouse 常見的驗證設定。

## <a name="overview"></a>基本升級概觀
在許多情況下，升級將會做為切換 toohello 新行動裝置應用程式伺服器 SDK，並重新發行到新的行動裝置應用程式執行個體上的程式碼一樣簡單。 但在某些情況下則需要一些額外的設定，例如進階驗證案例和使用排程工作。 每一種涵蓋 hello 中稍後的章節。

> [!TIP]
> 建議您閱讀，並在開始升級之前完全了解本主題的 hello rest。 請記下您使用的下列任何功能。
>
>

hello 行動服務用戶端 Sdk 是**不**與新行動裝置應用程式伺服器 hello SDK 相容。 在順序 tooprovide 服務連續性的應用程式，您不應該發行變更 tooa 站台目前正在服務已發佈的用戶端。 而是應該建立新的行動應用程式做為重複項目。 您可以將此應用程式相同的應用程式服務計劃在 hello tooavoid 產生額外的財務成本。

您將會讓 hello 應用程式的兩個版本： 一哪些保持 hello 相同，並提供 wild，hello 和 hello 中已發行的應用程式另一個您可以接著升級和目標服務以新的用戶端版本。 您可以移動，或您的程式碼測試您的速度，但您應該確定您所做的任何 bug 修正取得套用的 tooboth。 在您覺得 hello wild 中的用戶端應用程式所需的數目有更新 toohello 最新版本，如果您想要您可以刪除 hello 原始移轉應用程式。

hello 完整大綱 hello 升級程序如下所示：

1. 建立新的行動 App
2. 更新 hello 專案 toouse hello 新伺服器 Sdk
3. 發行新版的用戶端應用程式
4. (選擇性) 刪除原始已移轉的執行個體

## <a name="mobile-app-version"></a>建立第二個應用程式執行個體
hello 升級的第一個步驟是應用的將主控新版本程式中的 hello toocreate hello 行動裝置應用程式資源。 如果您已移轉現有的行動服務，您會想 toocreate hello 上的這個版本相同的主控方案。 開啟 hello [Azure 入口網站]並瀏覽 tooyour 移轉應用程式。 記下 hello App Service 方案上執行。

接下來，建立下列 hello hello 第二個應用程式執行個體[.NET 後端建立指示](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app)。 當您的應用程式服務方案或 「 主機計劃 」 選擇提示的 tooselect hello 計劃已移轉的應用程式。

您可能會想 toouse hello 相同的資料庫與通知中樞為您未在行動服務中。 您可以複製這些值開啟[Azure 入口網站]巡覽 toohello 原始應用程式，然後按一下**設定** > **應用程式設定**。 在 [連接字串] 下，複製 `MS_NotificationHubConnectionString` 和 `MS_TableConnectionString`。 瀏覽 tooyour 新升級的站台，然後將它們貼在中，覆寫任何現有的值。 針對您的應用程式需要的任何其他應用程式設定重複執行此程序。 如果未使用移轉的服務，您可以將連接字串和應用程式設定讀取 hello**設定**] 索引標籤的 hello 行動服務 > 一節的 hello [Azure 傳統入口網站]。

製作的應用程式的 hello ASP.NET 專案，並將它發行 tooyour 新站台。 使用一份 hello 新的 URL 以更新的用戶端應用程式，驗證確認一切如預期運作。

## <a name="updating-hello-server-project"></a>更新 hello 伺服器專案
行動應用程式提供了新[行動應用程式伺服器 SDK]其中提供許多的 hello 與 hello 行動服務執行階段相同的功能。 首先，您應該移除所有參考 toohello 行動服務封裝。 在 [hello NuGet 封裝管理員] 中，搜尋`WindowsAzure.MobileServices.Backend`。 大部分的 app 將會在此處看見數個封裝，包括 `WindowsAzure.MobileServices.Backend.Tables` 和 `WindowsAzure.MobileServices.Backend.Entity`。 在這種情況下，啟動與 hello 最低套件 hello 相依性樹狀目錄中，例如`Entity`，並將它移除。 出現提示時，請勿移除所有相依的封裝。 重複執行此程序，直到您移除了 `WindowsAzure.MobileServices.Backend` 本身為止。

此時，您的專案將不再參考行動服務 SDK。

接下來您將會新增參考 hello 行動應用程式 SDK。 針對這個升級中，大部分的開發人員會想 toodownload 並安裝 hello`Microsoft.Azure.Mobile.Server.Quickstart`封裝，因為這會在 hello 必要整組中提取。

會有極多的編譯器錯誤造成 hello Sdk 之間的差異，但這些是簡單 tooaddress，涵蓋在 hello 本節其餘部分。

### <a name="base-configuration"></a>基本組態
然後，在 WebApiConfig.cs 中，您可以取代：

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

取代為

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> 如果您想要 toolearn 新.NET 伺服器 hello SDK 與 tooadd/移除功能從您的應用程式的方式的詳細資訊，請參閱 hello [toouse 如何 hello.NET 伺服器 SDK]主題。
>
>

如果您的應用程式會使用 hello 驗證功能，您也需要 tooregister OWIN 中介軟體。 在此情況下，您應該將 hello 上述組態程式碼移到新的 OWIN 啟動 「 類別。

1. 將 hello NuGet 套件加入`Microsoft.Owin.Host.SystemWeb`如果它已不包含在專案中。
2. 在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [新增] -> [新項目]。 依序選取 [Web] -> [一般] -> [OWIN 啟動類別]。
3. 移動程式碼上方 hello MobileAppConfiguration 從`WebApiConfig.Register()`toohello`Configuration()`新啟動類別的方法。

請確定 hello`Configuration()`方法的結尾：

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

有其他變更的相關的 tooauthentication 涵蓋的 hello 完整驗證一節。

### <a name="working-with-data"></a>使用資料
行動服務中 hello 行動裝置應用程式名稱會當作 hello Entity Framework 安裝程式中的 hello 預設結構描述名稱。

您擁有的 tooensure hello 相同結構描述所參考的如往常一般，之後在您的應用程式的 hello DbContext tooset hello 結構描述使用 hello:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

請確定您有 MS_MobileServiceName 如果您不要 hello 上述設定。 如果您的應用程式先前已自訂這個結構描述，您也可以提供另一個結構描述名稱。

### <a name="system-properties"></a>系統屬性
#### <a name="naming"></a>命名
在 [hello Azure Mobile Services 伺服器 SDK 系統屬性永遠包含雙底線 (`__`) hello 屬性的前置詞：

* __createdAt
* __updatedAt
* __deleted
* __version

hello 行動服務用戶端 Sdk 有特殊邏輯，來剖析下列格式的系統屬性。

Azure 行動應用程式，在系統內容不會再有特殊格式，並具有下列名稱的 hello:

* 建立時間
* 更新時間
* 已刪除
* 版本

hello 行動應用程式用戶端 Sdk 使用 hello 新系統屬性的名稱，因此不必變更需要 tooclient 程式碼。 不過，如果您直接進行 REST 呼叫 tooyour 服務，則您應該據以變更您的查詢。

#### <a name="local-store"></a>本機存放區
系統屬性 hello 變更 toohello 名稱表示行動服務的離線同步處理本機資料庫不是與行動應用程式相容。 可能的話，您應該避免從應用程式直到之後暫止的變更尚未傳送 toohello server 的行動服務 tooMobile 升級用戶端應用程式。 然後，hello 升級應用程式應該使用新的資料庫檔案名稱。

如果有暫止的離線變更 hello 作業佇列中時，用戶端應用程式已升級從行動服務 tooMobile 應用程式，則 hello 系統資料庫必須是更新的 toouse hello 新資料行名稱。 在 iOS 上，這可以使用輕量型移轉 toochange hello 資料行名稱。 Android 和 hello.NET 受管理用戶端上，您應該撰寫自訂的 SQL toorename hello 資料行的資料物件資料表。

在 iOS 上，您可以變更您的核心資料結構描述資料實體 toomatch hello 下列。 請注意，hello 屬性`createdAt`，`updatedAt`和`version`不再有`ms_`前置詞：

| 屬性 | 類型 | 注意 |
| --- | --- | --- |
| id |字串 (標示為必要) |遠端存放區中的主索引鍵 |
| 建立時間 |Date |（選擇性） 對應 toocreatedAt 系統屬性 |
| 更新時間 |Date |（選擇性） 對應 tooupdatedAt 系統屬性 |
| 版本 |String |（選擇性） 使用的 toodetect 衝突，對應 tooversion |

#### <a name="querying-system-properties"></a>查詢系統屬性
在 Azure Mobile Services 中，系統屬性不會傳送預設情況下，但要求使用 hello 查詢字串時，只`__systemProperties`。 相反地，在 Azure 行動應用程式系統屬性是**一律選取**因為它們是 hello 伺服器 SDK 物件模型的一部分。

這項變更主要會影響網域管理員的自訂實作，例如 `MappedEntityDomainManager`的延伸模組。 在行動服務，如果用戶端永遠不會要求任何系統屬性，就可能 toouse`MappedEntityDomainManager`實際上未對應的所有屬性。 不過，在 Azure Mobile Apps 中，這些未對應的屬性將導致 GET 查詢發生錯誤。

hello 最簡單的方式 tooresolve hello 問題，使其繼承從是 toomodify 您 DTOs`ITableData`而不是`EntityData`。 接著，新增 hello`[NotMapped]`屬性應省略 toohello 欄位。

例如，下列 hello 定義`TodoItem`與任何系統屬性：

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

注意： 如果您收到錯誤訊息`NotMapped`，加入組件參考 toohello `System.ComponentModel.DataAnnotations`。

### <a name="cors"></a>CORS
行動服務藉由包裝 hello ASP.NET CORS 方案包含一些適用於 CORS 支援。 此文繞圖圖層移除的 toogive hello 開發人員已更大的控制權，因此您可以直接利用[ASP.NET CORS 支援](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api)。

hello 的問題，如果使用 CORS 的主要區域是該 hello`eTag`和`Location`標頭必須允許 hello 用戶端 Sdk toowork 順序正確。

### <a name="push-notifications"></a>推播通知
推入，您可能會發現遺漏 hello Server SDK hello 主要項目是 hello PushRegistrationHandler 類別。 註冊在行動應用程式中處理方式稍有不同，依預設會啟用不具標籤的註冊。 管理標籤可使用自訂 API 來完成。 請參閱 hello[標記註冊](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags)如需詳細資訊的指示。

### <a name="scheduled-jobs"></a>排程的工作
排程的工作不建行動裝置應用程式，因此您在.NET 後端中有任何現有的作業將需要 toobe 個別升級。 其中一個選項是排程的 toocreate [Web 工作]hello 行動裝置應用程式程式碼的站台上。 您無法同時設定了控制器保存您的作業程式碼，並設定 hello [Azure 排程器]toohit hello 預期排程該端點。

### <a name="miscellaneous-changes"></a>其他變更
這會由行動用戶端的所有 ApiControllers 現在必須都具有 hello`[MobileAppController]`屬性。 這已不再包含根據預設，讓其他不受影響的 ApiControllers toogo hello 行動格式器。

hello`ApiServices`物件不再是 hello SDK 的一部分。 tooaccess 行動裝置應用程式設定，您可以使用下列 hello:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

同樣地，記錄現在即可完成使用標準 ASP.NET 追蹤寫入 hello:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>驗證考量
行動服務的 hello 驗證元件現在已移到 hello 應用程式服務驗證和授權功能。 您可以了解啟用此站台所讀取的 hello[新增驗證 tooyour 行動裝置應用程式](app-service-mobile-ios-get-started-users.md)主題。

對於某些提供者，例如 AAD、 Facebook 和 Google，您應該能夠 tooleverage hello 現有註冊從您複製的應用程式。 您只需要 toonavigate toohello 身分識別提供者的入口網站，並加入新的重新導向 URL toohello 註冊。 接著設定應用程式服務驗證/授權與 hello 用戶端識別碼和密碼。

### <a name="controller-action-authorization"></a>控制器動作授權
任何執行個體的 hello`[AuthorizeLevel(AuthorizationLevel.User)]`屬性現在必須變更的 toouse hello 標準 ASP.NET`[Authorize]`屬性。 此外，根據預設，控制器現在是匿名的，就如同在其他 ASP.NET 應用程式中。
如果您使用其中一個 hello 其他 AuthorizeLevel 選項，例如系統管理員或應用程式，請注意，這些是消失。 相反地，您可以為共用密碼設定 AuthorizationFilters 或安全地設定 AAD 服務主體 tooenable 服務對服務呼叫。

### <a name="getting-additional-user-information"></a>取得其他使用者資訊
您可以取得額外的使用者資訊，包括存取權杖透過 hello`GetAppServiceIdentityAsync()`方法：

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

此外，如果您的應用程式使用者識別碼上, 使用相依性，例如將它們儲存在資料庫中，務必 hello 行動服務與應用程式服務的行動應用程式之間的使用者識別碼的 toonote 會不同。 您還可以透過取得 hello 行動服務使用者識別碼。 Hello ProviderCredentials 子類別的所有有使用者識別碼屬性。 因此從 hello 範例，然後再繼續：

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

如果您的應用程式採用任何相依項目上的使用者 Id，很重要，運用盡可能 hello 與身分識別提供者相同的登錄。 使用者識別碼會是通常已設定領域的 toohello 應用程式登錄，因此導入新的註冊，則可以建立比對使用者 tootheir 資料的問題。

### <a name="custom-authentication"></a>自訂驗證
如果您的應用程式使用的自訂驗證解決方案，您會想 toomake 確定該 hello 升級站台具有存取 toohello 系統。 遵循 hello 新的自訂驗證 hello [.NET 伺服器 SDK 概觀]toointegrate 您的方案。 請注意，hello 自訂驗證元件仍在預覽中。

## <a name="updating-clients"></a>更新用戶端
在您擁有可運作的行動 App 後端之後，就能在取用它的新版用戶端應用程式上運作。 行動應用程式也包含新版 hello client Sdk，以及類似的 toohello server 升級上方，您將需要的 tooremove toohello 行動服務 Sdk 之前的所有參照安裝 hello 行動應用程式版本。

其中一個 hello hello 版本之間的主要變更是 hello 建構函式不再需要應用程式金鑰。 您現在只需傳入 hello 行動應用程式的 URL。 例如，在 hello.NET 用戶端，hello`MobileServiceClient`建構函式現在是：

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

您可以閱讀安裝 hello 新 Sdk，並使用 hello 透過以下的 hello 連結新的結構：

* [iOS 3.0.0 版或更新版本](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) 2.0.0 版或更新版本](app-service-mobile-dotnet-how-to-use-client-library.md)

如果您的應用程式更能使用推播通知，請記下 hello 特定註冊指示每個平台，已有一些變更有以及。

當您擁有 hello 新用戶端版本準備好時，現在就試試看對您已升級的伺服器專案。 驗證它運作之後，您可以釋放您的應用程式 toocustomers 的新版本。 最後，一旦您的客戶有機會 tooreceive 這些更新，您可以刪除 hello 行動服務應用程式版本。 此時，您完全升級 tooan App Service 行動應用程式使用最新版行動應用程式伺服器 hello SDK。

<!-- URLs. -->

[Azure 入口網站]: https://portal.azure.com/
[Azure 傳統入口網站]: https://manage.windowsazure.com/
[什麼是 Mobile Apps？]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[行動應用程式伺服器 SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure 排程器]: /en-us/documentation/services/scheduler/
[Web 工作]: ../app-service-web/websites-webjobs-resources.md
[如何 toouse hello.NET 伺服器 SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[App Service 價格]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET 伺服器 SDK 概觀]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
