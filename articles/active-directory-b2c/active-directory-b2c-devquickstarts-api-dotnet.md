---
title: "aaaAzure AD B2C |Microsoft 文件"
description: "如何使用 Azure Active Directory B2C 的.NET Web 應用程式開發介面 toobuild 保護使用 OAuth 2.0 存取權杖來進行驗證。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C：建置 .NET Web API

透過 Azure Active Directory (Azure AD) B2C，您可以使用 OAuth 2.0 存取權杖來保護 Web API。 這些語彙基元可讓您的用戶端應用程式 tooauthenticate toohello 應用程式開發介面。 本文章將示範如何 toocreate.NET MVC 「 待辦事項清單 」 應用程式開發介面可讓使用者在您的用戶端的應用程式 tooCRUD 工作。 hello web API 使用 Azure AD B2C 保護，並且只允許已驗證的使用者 toomanage 其待辦事項清單。

## <a name="create-an-azure-ad-b2c-directory"></a>建立 Azure AD B2C 目錄

您必須先建立目錄或租用戶，才可使用 Azure AD B2C。 目錄是適用於所有使用者、app、群組等項目的容器。 如果您還沒有此資源，請先 [建立 B2C 目錄](active-directory-b2c-get-started.md) ，再繼續進行本指南。

> [!NOTE]
> hello 用戶端應用程式和 web API 必須使用 hello 相同的 Azure AD B2C 目錄。
>

## <a name="create-a-web-api"></a>建立 Web API

接下來，您需要 toocreate web API 應用程式中 B2C 目錄。 提供 Azure AD，它需要 toosecurely 通訊與您的應用程式的資訊。 toocreate 的應用程式，請遵循[這些指示](active-directory-b2c-app-registration.md)。 請務必：

* 包含**web 應用程式**或**web API** hello 應用程式中。
* 使用 hello**重新導向 URI** `https://localhost:44332/` hello web 應用程式。 這是 hello hello web 應用程式用戶端，此程式碼範例預設位置。
* 複製 hello**應用程式識別碼**也就是指派的 tooyour 應用程式。 稍後您將會用到此資訊。
* 在 [應用程式識別碼 URI] 中輸入應用程式識別碼。
* 新增權限透過 hello**發行領域**功能表。

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>建立您的原則

在 Azure AD B2C 中，每個使用者體驗皆是由某個 [原則](active-directory-b2c-reference-policies.md)所定義。 您必須使用 Azure AD B2C 原則 toocommunicate toocreate。 我們建議使用 hello 結合 sign-up/登入原則 hello 中所述[原則參考文件](active-directory-b2c-reference-policies.md)。 建立原則時，請務必：

* 選擇 [顯示名稱]  和原則中的其他註冊屬性。
* 針對每個原則選擇 [顯示名稱] 和 [物件識別碼] 宣告做為應用程式宣告。 您也可以選擇其他宣告。
* 複製 hello**名稱**的每個原則建立之後。 稍後您將需要 hello 原則名稱。

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

您已成功建立 hello 原則之後，您便準備好 toobuild 您的應用程式。

## <a name="download-hello-code"></a>下載 hello 程式碼

本教學課程中的 hello 程式碼維護在[GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)。 您可以藉由執行複製 hello 範例：

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

下載 hello 範例程式碼之後，開啟 hello Visual Studio.sln 檔案 tooget 啟動。 hello 方案檔包含兩個專案：`TaskWebApp`和`TaskService`。 `TaskWebApp`是 hello 使用者 MVC web 應用程式互動。 `TaskService`是 hello 應用程式後端 web API，儲存每個使用者的待辦事項清單。 本文將只會討論 hello`TaskService`應用程式。 toolearn 如何 toobuild`TaskWebApp`使用 Azure AD B2C，請參閱[我們.NET web 應用程式教學課程](active-directory-b2c-devquickstarts-web-dotnet-susi.md)。

### <a name="update-hello-azure-ad-b2c-configuration"></a>更新 Azure AD B2C hello 組態

我們的範例是設定的 toouse hello 原則和用戶端識別碼我們示範租用戶。 如果您想要 toouse 自己的租用戶，您必須遵循 toodo hello:

1. 開啟`web.config`在 hello`TaskService`專案和 hello 值取代
    * `ida:Tenant`：使用您的租用戶名稱
    * `ida:ClientId`：使用您的 Web API 應用程式識別碼
    * `ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱

2. 開啟`web.config`在 hello`TaskWebApp`專案和 hello 值取代
    * `ida:Tenant`：使用您的租用戶名稱
    * `ida:ClientId`：使用您的 Web 應用程式識別碼
    * `ida:ClientSecret`：使用您的 Web 應用程式祕密金鑰
    * `ida:SignUpSignInPolicyId`：使用您的「註冊或登入」原則名稱
    * `ida:EditProfilePolicyId`：使用您的「編輯設定檔」原則名稱
    * `ida:ResetPasswordPolicyId`：使用您的「重設密碼」原則名稱


## <a name="secure-hello-api"></a>安全 hello 應用程式開發介面

當您有可呼叫 API 的用戶端時，您可以使用 OAuth 2.0 持有人權杖來保護 API (例如 `TaskService`)。 這可確保每個要求 tooyour API 才會有效 hello 要求是否持有人權杖。 您的 API 可以使用 Microsoft 的 Open Web Interface for .NET (OWIN) 程式庫來接受並驗證持有人權杖。

### <a name="install-owin"></a>安裝 OWIN

開始使用 Visual Studio Package Manager Console hello 安裝 hello OWIN OAuth 驗證管線。

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

這會安裝 hello OWIN 中介軟體，將接受和驗證持有者權杖。

### <a name="add-an-owin-startup-class"></a>新增 OWIN 啟動類別

新增 OWIN 啟動類別 toohello API 呼叫`Startup.cs`。  以滑鼠右鍵按一下 hello 專案、 選取**新增**和**新項目**，然後搜尋 OWIN。 hello OWIN 中介軟體將會叫用 hello`Configuration(…)`方法，當您啟動應用程式。

在我們的範例中，我們變更 hello 類別宣告太`public partial class Startup`和實作 hello hello 類別中的其他部分`App_Start\Startup.Auth.cs`。 內部 hello`Configuration`方法中，我們加入呼叫太`ConfigureAuth`，定義在`Startup.Auth.cs`。 Hello 修改之後`Startup.cs`看起來像 hello 面：

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>設定 OAuth 2.0 驗證

開啟 hello 檔案`App_Start\Startup.Auth.cs`，並實作 hello`ConfigureAuth(...)`方法。 例如，它可能看起來像 hello 下列：

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>安全 hello 工作控制站

Hello 應用程式設定的 toouse OAuth 2.0 驗證之後，您可以藉由新增保護您的 web API`[Authorize]`標記 toohello 工作控制站。 這是其中所有的待辦事項清單操作發生，因此您應該保護 hello 整個控制器 hello 類別層級的 hello 控制站。 您也可以加入 hello`[Authorize]`標記更細部的掌控 tooindividual 動作。

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Hello 從權杖取得使用者資訊

`TasksController`將工作儲存在資料庫，其中每個工作都有關聯的使用者，「 擁有 」 hello 工作。 hello 擁有者由 hello 使用者**物件識別碼**。 (這就是為什麼需要 tooadd hello 物件識別碼，做為應用程式所有的原則中的宣告。)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>驗證 hello 權杖中的 hello 權限

Web 應用程式開發介面的共通需求是 toovalidate hello 「 範圍 」 hello 權杖中。 這可確保該 hello 使用者同意 toohello 權限需要的 tooaccess hello 待辦事項清單服務。

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>執行 hello 範例應用程式

最後，請建置並執行 `TaskWebApp` 和 `TaskService`。 Hello 使用者待辦事項清單上建立一些工作，並注意如何在保存在 hello API 即使您停止並重新啟動 hello 用戶端。

## <a name="edit-your-policies"></a>編輯您的原則

您已有使用 Azure AD B2C 保護應用程式開發介面之後，您可以試驗您登在 /-註冊原則和檢視 hello 效果上 （或短缺） hello 應用程式開發介面。 您可以操作 hello hello 原則中的應用程式宣告，並變更用於 hello web API 的 hello 使用者資訊。 您新增任何宣告將會是可用 tooyour.NET MVC web 應用程式開發介面中 hello`ClaimsPrincipal`物件，如本文稍早所述。
