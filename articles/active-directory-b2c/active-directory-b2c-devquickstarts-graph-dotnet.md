---
title: "Azure Active Directory B2C： 使用 hello Graph API |Microsoft 文件"
description: "如何 toocall hello Graph API B2C 租用戶使用應用程式識別 tooautomate hello 程序。"
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure AD B2C： 使用 hello Graph API
Azure Active Directory (Azure AD) B2C 租用戶通常 toobe 的非常大。 這表示許多常見的租用戶管理工作需要 toobe 以程式設計方式執行。 使用者管理是主要範例。 您可能需要 toomigrate 現有使用者存放區 tooa B2C 租用戶。 您可能想 toohost 使用者註冊您自己的頁面上，並在您的 Azure AD B2C 目錄 hello 幕後建立使用者帳戶。 這類工作需要 hello 能力 toocreate、 讀取、 更新及刪除使用者帳戶。 您可以利用 hello Azure AD Graph API 來完成這些工作。

B2C 租用戶，有兩個主要模式與 hello Graph API 進行通訊。

* 互動、 執行一次的工作，您應該執行 hello 工作時做為在 hello B2C 租用戶系統管理員帳戶。 這個模式需要使用認證管理員 toosign 系統管理員才能執行任何呼叫 toohello Graph API。
* 自動化、 連續工作，您應該使用某種類型的服務帳戶，您提供 hello 必要的權限 tooperform 管理工作。 在 Azure AD 中，您可以透過登錄應用程式和驗證 tooAzure AD。 這是使用**應用程式識別碼**使用 hello [OAuth 2.0 用戶端認證授與](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)。 在此情況下，hello 應用程式做為本身，不做為使用者，toocall hello Graph API。

在本文中，我們將討論如何 tooperform hello 自動化使用案例。 toodemonstrate，我們會建置.NET 4.5`B2CGraphClient`它不會執行使用者建立、 讀取、 更新和刪除 (CRUD) 作業。 hello 用戶端將會有 Windows 命令列介面 (CLI)，可讓您 tooinvoke 各種方法。 不過，hello 程式碼會以非互動式、 自動化的方式寫入 toobehave。

## <a name="get-an-azure-ad-b2c-tenant"></a>取得 Azure AD B2C 租用戶
您可以建立應用程式或使用者，或完全與 Azure AD 互動之前，您將需要 Azure AD B2C 租用戶和 hello 租用戶中的全域管理員帳戶。 如果您還沒有租用戶，請參閱 [開始使用 Azure AD B2C](active-directory-b2c-get-started.md)。

## <a name="register-your-application-in-your-tenant"></a>在您的租用戶中註冊您的應用程式
B2C 租用戶之後，您需要 tooregister 應用程式透過 hello [Azure 入口網站](https://portal.azure.com)。

> [!IMPORTANT]
> toouse hello 與 B2C 租用戶的 Graph API，您將需要 tooregister 專用的應用程式使用 hello 泛型*應用程式註冊*hello Azure 入口網站中，在刀鋒視窗**不**Azure AD B2C 的*應用程式*刀鋒視窗。 您無法重複使用 hello 現有 B2C 的應用程式註冊，讓您在 Azure AD B2C 的 hello*應用程式*刀鋒視窗。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD B2C 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 左側導覽窗格中，選擇 **更服務**，按一下**應用程式註冊**，然後按一下**新增**。
4. 依照 hello 提示，並建立新的應用程式。 
    1. 選取**Web 應用程式 / 應用程式開發介面**為 hello 應用程式類型。    
    2. 提供**任何重新導向 URI** (例如 https://B2CGraphAPI)，因為它在此範例中不重要。  
5. hello 應用程式會立即顯示在 hello 應用程式清單，按一下它 tooobtain hello**應用程式識別碼**（也稱為用戶端識別碼）。 將它複製下來，稍後一節需要用到。
6. 在 hello 設定刀鋒視窗中，按一下**金鑰**並加入新的金鑰 （也稱為用戶端密碼）。 也將它複製下來，稍後一節會用到。

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>設定應用程式的建立、讀取和更新權限
現在您需要 tooconfigure 所有 hello 您應用程式 tooget 所需的權限 toocreate、 讀取、 更新和刪除使用者。

1. 繼續在 hello Azure 入口網站應用程式註冊 刀鋒視窗中，選取您的應用程式。
2. 在 hello 設定刀鋒視窗中，按一下**必要的權限**。
3. 在 hello 必要的權限刀鋒視窗中，按一下**Windows Azure Active Directory**。
4. 在 hello 啟用存取刀鋒視窗中，選取 hello**讀取和寫入目錄資料**權限從**應用程式權限**按一下**儲存**。
5. 最後，在 [hello 必要的權限刀鋒視窗中，按一下 hello**授與權限**] 按鈕。

現在您已經有具有從 B2C 租用戶的權限 toocreate、 讀取和更新使用者的應用程式。

## <a name="configure-delete-permissions-for-your-application"></a>設定應用程式的刪除權限
目前，hello*讀取和寫入目錄資料*權限未**不**包含 hello 能力 toodo 任何刪除動作，例如刪除使用者。 如果您想 toogive 您 hello 能力 toodelete 應用程式的使用者，，您還需要 toodo 這些額外的步驟牽涉到 PowerShell 否則您可以略過 toohello 下一節。

首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。 請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。

安裝 hello PowerShell 模組之後，請開啟 PowerShell，並連接 tooyour B2C 租用戶。 當您執行`Get-Credential`，系統將提示您的使用者名稱和密碼、 輸入 hello 使用者名稱和 B2C 租用戶系統管理員帳戶的密碼。

> [!IMPORTANT]
> 您必須是 toouse B2C 租用戶系統管理員帳戶**本機**toohello B2C 租用戶。 這些帳戶看起來像這樣︰myusername@myb2ctenant.onmicrosoft.com。

```powershell
Connect-MsolService
```

現在我們將使用 hello**應用程式識別碼**hello tooassign hello 應用程式 hello 使用者帳戶系統管理員角色，讓它 toodelete 使用者指令碼中。 這些角色具有已知的識別項，因此您只需要 toodo 輸入您**應用程式識別碼**hello 以下的指令碼中。

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

您的應用程式現在也有 toodelete 使用者權限從 B2C 租用戶。

## <a name="download-configure-and-build-hello-sample-code"></a>下載、 設定和建置 hello 範例程式碼
首先，下載 hello 範例程式碼，並加以執行。 然後我們會仔細查看。  您可以[下載 hello 範例程式碼的.zip 檔](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip)。 您可以將此檔案複製到您選擇的目錄中：

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

開啟 hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio 中的 Visual Studio 方案。 在 hello`B2CGraphClient`專案、 開啟 hello 檔案`App.config`。 取代您自己的值為 hello 三個應用程式設定：

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

接下來，以滑鼠右鍵按一下 hello`B2CGraphClient`方案並重建 hello 範例。 如果成功，您現在應該有一個 `B2C.exe` 可執行檔位於 `B2CGraphClient\bin\Debug`。

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>利用 hello Graph API 來建立使用者 CRUD 作業
toouse hello B2CGraphClient，開啟`cmd`Windows 命令提示字元並變更目錄 toohello`Debug`目錄。 然後執行 hello`B2C Help`命令。

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

這會顯示每個命令的簡短描述。 您可以叫用其中一個命令，每次`B2CGraphClient`讓要求 toohello Azure AD Graph API。

### <a name="get-an-access-token"></a>取得存取權杖
任何要求 toohello Graph API 要求存取權杖進行驗證。 `B2CGraphClient`使用 hello 開放原始碼 Active Directory 驗證程式庫 (ADAL) toohelp 取得存取權杖。 ADAL 提供簡單的 API 並處理一些重要的細節，例如快取存取權杖，可讓您輕鬆取得權杖。 雖然您不需要 toouse ADAL tooget 語彙基元。 您也可以藉由製作 HTTP 要求來取得權杖。

> [!NOTE]
> 此程式碼範例會使用 ADAL v2 順序 toocommunicate 以 hello Graph API 中。  您必須使用 ADAL v2 或 v3，就可以使用 Azure AD Graph API hello 順序 tooget 存取權杖中。
> 
> 

當`B2CGraphClient`執行時，它會建立執行個體的 hello`B2CGraphClient`類別。 這個類別的 hello 建構函式上設定 ADAL 驗證 scaffolding:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

我們將使用 hello`B2C Get-User`命令做為範例。 當`B2C Get-User`叫用不含任何其他輸入 hello CLI 呼叫 hello`B2CGraphClient.GetAllUsers(...)`方法。 這個方法會呼叫`B2CGraphClient.SendGraphGetRequest(...)`，其中送出 HTTP GET 要求 toohello Graph API。 之前`B2CGraphClient.SendGraphGetRequest(...)`傳送 hello GET 要求，它會先取得存取權杖使用 ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

您可以取得存取權杖的 hello Graph API 的呼叫 hello ADAL`AuthenticationContext.AcquireToken(...)`方法。 然後傳回 ADAL`access_token`表示 hello 應用程式的身分識別。

### <a name="read-users"></a>讀取使用者
當您想 tooget 的使用者清單，或從 hello Graph API 取得特定的使用者時，您可以傳送 HTTP`GET`要求 toohello`/users`端點。 所有租用戶中的 hello 使用者的要求看起來像這樣：

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee 這項要求，執行：

 ```
 > B2C Get-User
 ```

有兩個重要事項 toonote:

* hello 透過 ADAL 取得存取權杖加入 toohello`Authorization`標頭使用 hello`Bearer`配置。
* B2C 租用戶，您必須使用 hello 查詢參數`api-version=1.6`。

這兩個這些詳細資料會在 hello 處理`B2CGraphClient.SendGraphGetRequest(...)`方法：

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>建立取用者的使用者帳戶
當您 B2C 租用戶中建立使用者帳戶時，您可以傳送 HTTP`POST`要求 toohello`/users`端點：

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

這個要求中的這些屬性大部分都是必要的 toocreate 取用者的使用者。 詳細資訊，按一下 toolearn[這裡](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)。 請注意該 hello`//`註解已包含如圖例。 請不要放入實際的要求中。

toosee hello 要求，執行下列命令的 hello 的其中一個：

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

hello`Create-User`命令會使用做為輸入參數的.json 檔案。 這包含使用者物件的 JSON 表示法。 Hello 範例程式碼中有兩個範例.json 檔案：`usertemplate-email.json`和`usertemplate-username.json`。 您可以修改這些檔案 toosuit 您的需求。 此外 toohello 需要上述欄位，這些檔案中包含數個您可以使用的選擇性欄位。 Hello 選擇性欄位的詳細資訊，請參閱 hello [Azure AD Graph API 實體參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity)。

您可以看到 hello POST 要求中的建構方式`B2CGraphClient.SendGraphPostRequest(...)`。

* 它會將附加存取語彙基元 toohello `Authorization` hello 要求標頭。
* 它會設定 `api-version=1.6`。
* 在 hello hello 要求主體包含 hello JSON 使用者物件。

> [!NOTE]
> Hello 帳戶如果您想從現有的使用者存放區 toomigrate 具有比 hello 的密碼強度較低[由 Azure AD B2C 強制執行強式密碼強度](https://msdn.microsoft.com/library/azure/jj943764.aspx)，您可以停用使用 hello hello強式密碼需求`DisableStrongPassword`中 hello 值`passwordPolicies`屬性。 比方說，您可以修改 hello 建立，如下所示以上所提供的使用者要求： `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`。
> 
> 

### <a name="update-consumer-user-accounts"></a>更新取用者的使用者帳戶
當您更新使用者物件時，hello 程序是類似 toohello 使用 toocreate 使用者物件。 但此程序使用 hello HTTP`PATCH`方法：

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

嘗試 tooupdate 使用者藉由更新您的 JSON 檔案使用新的資料。 然後您可以使用`B2CGraphClient`toorun 其中一個命令：

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

檢查 hello`B2CGraphClient.SendGraphPatchRequest(...)`方法的詳細資料 toosend 此要求。

### <a name="search-users"></a>搜尋使用者
您可以透過數種方式在 B2C 租用戶中搜尋使用者。 一個使用 hello 使用者的物件識別碼或兩個，使用登入識別碼 hello 使用者 (亦即，hello`signInNames`屬性)。

執行下列命令 toosearch 特定使用者的 hello 任一個：

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

以下是一些範例︰

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>刪除使用者
刪除使用者 hello 程序很簡單。 使用 hello HTTP`DELETE`方法和建構 hello URL 以 hello 更正物件識別碼：

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee 範例中，輸入這個命令並檢視 hello 刪除要求所列印的 toohello 主控台：

```
> B2C Delete-User <object-id-of-user>
```

檢查 hello`B2CGraphClient.SendGraphDeleteRequest(...)`方法的詳細資料 toosend 此要求。

您可以執行許多其他動作以 hello Azure AD Graph API 在加法 toouser 管理。 [Azure AD 圖形 API 參考](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 會提供每個動作的詳細資訊以及範例要求。

## <a name="use-custom-attributes"></a>使用自訂屬性
大部分的取用者應用程式需要 toostore 某種類型的自訂使用者設定檔資訊。 執行這項操作的一個方式是 toodefine B2C 租用戶中的自訂屬性。 然後，您可以將該屬性 hello 相同的方式，您將使用者物件上的任何其他內容。 您可以更新 hello 屬性刪除 hello 屬性查詢 hello 屬性，在登入語彙基元和多個宣告的形式傳送 hello 屬性。

toodefine B2C 租用戶中的自訂屬性，請參閱 「 hello [B2C 自訂屬性參考](active-directory-b2c-reference-custom-attr.md)。

您可以檢視 hello 使用 B2C 租用戶中定義的自訂屬性`B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

這些函式的 hello 輸出會顯示 hello 詳細資料的每個自訂屬性，例如：

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

您可以使用完整名稱，例如 hello `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`，為您的使用者物件的屬性。  更新您的.json 檔案 hello 新屬性和 hello 屬性的值，然後執行：

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

使用 `B2CGraphClient`，您會有一個服務應用程式可利用程式設計方式來管理 B2C 租用戶使用者。 `B2CGraphClient`會使用它自己的應用程式識別 tooauthenticate toohello Azure AD Graph API。 它也會使用用戶端密碼來取得權杖。 將這項功能納入您的應用程式時，請記住 B2C 應用程式的幾個重點：

* 您需要 toogrant hello 應用程式 hello 適當的權限 hello 租用戶中。
* 現在，您需要將 toouse ADAL (不 MSAL) tooget 存取語彙基元。 (也可以直接傳送通訊協定訊息，而不使用程式庫)。
* 當您呼叫 hello Graph API 時，使用`api-version=1.6`。
* 當建立和更新取用者使用者，有幾個必要的屬性，如上所述。

如果您有任何問題或您想要 tooperform hello Graph API，透過動作的要求您 B2C 租用戶上這篇文章留下註解或 hello GitHub 的程式碼範例儲存機制中提出問題。

