---
title: "aaaAzure Active Directory 驗證和資源管理員 |Microsoft 文件"
description: "開發人員指南 tooauthentication hello Azure 資源管理員 API 和 Azure Active Directory 整合應用程式與其他 Azure 訂用帳戶。"
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>使用資源管理員 API 驗證 tooaccess 訂用帳戶
## <a name="introduction"></a>簡介
如果您是軟體開發人員需要 toocreate 管理客戶的 Azure 資源的應用程式，本主題，說明如何使用 tooauthenticate hello Azure 資源管理員 Api，並取得存取 tooresources 其他訂用帳戶中。

您的應用程式可以存取數種方式中的資源管理員 Api hello:

1. **使用者 + 應用程式存取**︰適用於代表登入使用者存取資源的應用程式。 此方式適用於僅處理「互動式管理」Azure 資源的應用程式，例如 Web 應用程式和命令列工具。
2. **僅限應用程式存取**︰適用於執行協助程式服務和已排程之作業的應用程式。 hello 應用程式的身分識別會授與直接存取 toohello 資源。 這個方法適用於需要長期的遠端控制 （自動） 存取 tooAzure 的應用程式。

本主題提供逐步指示 toocreate 採用這兩種授權方法的應用程式。 它會顯示如何 tooperform 每個步驟來搭配 REST API 或 C#。 hello 完整的 ASP.NET MVC 應用程式將會位於[https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)。

## <a name="what-hello-web-app-does"></a>沒有什麼 hello web 應用程式
hello web 應用程式：

1. 登入 Azure 使用者。
2. 會要求使用者 toogrant hello web 應用程式存取 tooResource 管理員。
3. 取得使用者 + 應用程式的存取權杖來存取 Resource Manager。
4. Hello 訂用帳戶，可讓 hello 應用程式長期存取 toohello 訂用帳戶中，會使用語彙基元 （從步驟 3） toocall 資源管理員和指派 hello 應用程式的服務主體 tooa 角色。
5. 取得僅限應用程式存取權杖。
6. Hello 訂用帳戶透過資源管理員中，會使用語彙基元 （來自步驟 5） toomanage 資源。

以下是 hello hello web 應用程式的端對端流程。

![Resource Manager 驗證流程](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

身為使用者，您可以提供 hello 訂用帳戶 id 想 toouse hello 訂用帳戶：

![提供訂用帳戶識別碼](./media/resource-manager-api-authentication/sample-ux-1.png)

選取 hello 帳戶 toouse 進行登入。

![選取帳戶](./media/resource-manager-api-authentication/sample-ux-2.png)

提供您的認證。

![提供認證](./media/resource-manager-api-authentication/sample-ux-3.png)

授與 hello 應用程式存取 tooyour Azure 訂用帳戶：

![授與存取權](./media/resource-manager-api-authentication/sample-ux-4.png)

管理連接的訂用帳戶：

![連線訂用帳戶](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>註冊應用程式
在開始撰寫程式碼之前，請先使用 Azure Active Directory (AD) 註冊 Web 應用程式。 hello 應用程式註冊在 Azure AD 中建立應用程式的中央識別身分。 它會保留應用程式使用 tooauthenticate 和存取 Azure 資源管理員 Api 應用程式，例如 OAuth 用戶端識別碼、 回覆 Url 和認證的相關基本資訊。 hello 應用程式登錄也會記錄的 hello 各種委派代表 hello 使用者存取 Microsoft 應用程式開發介面時，需要您的應用程式的權限。

由於應用程式會存取其他訂用帳戶，您必須將它設定為多租用戶應用程式。 toopass 驗證提供與 Azure Active Directory 相關聯的網域。 Azure Active Directory，登入 toohello 與相關聯的 toosee hello 網域[傳統入口網站](https://manage.windowsazure.com)。 選取您的 Azure Active Directory，然後選取 [網域]。

hello 下列範例顯示如何 tooregister hello 使用 Azure PowerShell 的應用程式。 您必須擁有 hello 最新版本 (年 8 月 2016) 的 Azure PowerShell 這個命令 toowork。

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog 中的為 hello AD 應用程式，您需要 hello 應用程式識別碼和密碼。 傳回從 hello 前一個命令，使用 toosee hello 應用程式識別碼：

    $app.ApplicationId

下列範例中的 hello 顯示 tooregister 如何使用 Azure CLI hello 應用程式。

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

hello 結果包含 hello hello 應用程式以進行驗證時，您需要的 AppId。

### <a name="optional-configuration---certificate-credential"></a>選擇性組態 - 憑證認證
Azure AD 也支援憑證認證的應用程式： 您建立自我簽署的憑證、 保留 hello 私用金鑰，以及新增 hello 公用金鑰 tooyour Azure AD 應用程式註冊。 進行驗證，您的應用程式會傳送小裝載 tooAzure 使用您的私密金鑰來簽署 AD 與 Azure AD 會驗證使用 hello 註冊，讓您的公用金鑰 hello 簽章。

使用憑證建立 AD 應用程式的詳細資訊，請參閱[使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)或[使用 Azure CLI toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>從訂用帳戶識別碼取得租用戶識別碼
toorequest 語彙基元可能是使用的 toocall 資源管理員，您的應用程式必須裝載 hello Azure 訂用帳戶的 hello Azure AD 租用戶 tooknow hello 租用戶識別碼。 使用者很可能知道其訂用帳戶識別碼，但他們可能不知道其用於 Azure Active Directory 的租用戶識別碼。 tooget hello 使用者的租用戶識別碼，hello 使用者尋求 hello 訂用帳戶 id。傳送嗨訂用帳戶的相關要求時，請提供該訂用帳戶 id:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

hello 要求失敗是因為 hello 使用者尚未登入，但您可以擷取 hello 回應 hello 租用戶識別碼。 在該例外狀況，請從 hello 回應標頭值中擷取 hello 租用戶識別碼**Www-authenticate**。 您會看到此實作中 hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20)方法。

## <a name="get-user--app-access-token"></a>取得使用者 + 應用程式的存取權杖
您的應用程式重新導向 hello 使用者 tooAzure AD 的 OAuth 2.0 授權要求-tooauthenticate hello 使用者的認證，並取得授權碼。 您的應用程式會使用資源管理員的 hello 授權程式碼 tooget 存取權杖。 hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42)方法會建立 hello 授權要求。

本主題顯示 hello REST API 要求 tooauthenticate hello 使用者。 您也可以使用協助程式程式庫 tooperform 驗證程式碼中。 如需這些程式庫的詳細資訊，請參閱 [Azure Active Directory 驗證程式庫](../active-directory/active-directory-authentication-libraries.md)。 如需在應用程式中整合身分識別管理的指引，請參閱 [Azure Active Directory 開發人員指南](../active-directory/active-directory-developers-guide.md)。

### <a name="auth-request-oauth-20"></a>驗證要求 (OAuth 2.0)
發出開啟識別碼連接/OAuth2.0 授權要求 toohello Azure AD 授權端點：

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

hello 查詢字串參數可用於此要求所述 hello[要求授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code)主題。

下列範例會示範如何 hello toorequest OAuth2.0 授權：

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD 驗證 hello 使用者，並視需要要求 hello 使用者 toogrant 權限 toohello 應用程式。 它會傳回 hello 授權程式碼 toohello 應用程式的回覆 URL。 根據 hello 要求 response_mode，任一個傳送回 hello 資料查詢字串或張貼資料的 Azure AD。

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>驗證要求 (Open ID Connect)
如果您不只想 tooaccess Azure 資源管理員代表 hello 使用者，但也允許 hello 使用者 toosign tooyour 使用其 Azure AD 帳戶的應用程式中，發出開啟識別碼連線授權要求。 開啟連接識別碼，與您的應用程式也會收到 id_token 從您的應用程式，可以使用 toosign hello 使用者在 Azure AD。

hello 查詢字串參數可用於此要求所述 hello[登入要求傳送嗨](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request)主題。

Open ID Connect 的要求範例是︰

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD 驗證 hello 使用者，並視需要要求 hello 使用者 toogrant 權限 toohello 應用程式。 它會傳回 hello 授權程式碼 toohello 應用程式的回覆 URL。 根據 hello 要求 response_mode，任一個傳送回 hello 資料查詢字串或張貼資料的 Azure AD。

Open ID Connect 回應的範例是︰

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>權杖要求 (OAuth2.0 程式碼授與流程)
現在，您的應用程式已收到來自 Azure AD 的 hello 授權碼，它會是時間 tooget hello 存取語彙基元的 Azure 資源管理員。  張貼 OAuth2.0 程式碼授與權杖要求 toohello Azure AD 權杖端點：

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

hello 查詢字串參數可用於此要求所述 hello[使用 hello 授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token)主題。

hello 下列範例顯示使用密碼認證的程式碼授與權杖的要求：

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

當使用憑證認證，建立 JSON Web Token (JWT) 並登入 (RSA SHA256) 使用的應用程式的憑證認證 hello 私密金鑰。 hello hello 語彙基元的宣告型別如下所示[JWT 權杖宣告](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)。 如需參考，請參閱 hello [Active Directory 驗證程式庫 (.NET) 程式碼](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs)toosign 用戶端判斷提示的 JWT 語彙基元。

請參閱 hello[開啟連接的識別碼規格](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication)如用戶端驗證的詳細資訊。

hello 下列範例顯示使用憑證認證的程式碼授與權杖的要求：

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

程式碼授與權杖回應的範例︰

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>處理程式碼授與權杖回應
成功的語彙基元回應包含 hello （使用者 + 應用程式） 存取權杖的 Azure 資源管理員。 您的應用程式會使用代表 hello 使用者此存取權杖 tooaccess 資源管理員。 Azure AD 所簽發存取語彙基元的 hello 存留期為一小時。 不太 web 應用程式需要 toorenew hello （使用者 + 應用程式） 存取權杖。 如果它需要 toorenew hello 存取權杖時，使用您的應用程式收到 hello 權杖回應中的 hello 重新整理權杖。 張貼 OAuth2.0 語彙基元要求 toohello Azure AD 權杖端點：

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

hello 參數 toouse 與 hello 重新整理要求中有描述[重新整理 hello 存取權杖](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)。

hello 下列範例顯示如何 toouse hello 重新整理權杖：

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

雖然重新整理語彙基元可以用的 tooget 新存取權杖的 Azure 資源管理員，他們並不適合您的應用程式的離線存取。 hello 重新整理權杖存留期受到限制，而且重新整理權杖是繫結的 toohello 使用者。 如果 hello 使用者離開組織 hello，hello 應用程式使用 hello 重新整理權杖會失去存取權。 這個方法不是適用於應用程式供小組 toomanage 他們的 Azure 資源。

## <a name="check-if-user-can-assign-access-toosubscription"></a>請檢查使用者可指派給存取 toosubscription
您的應用程式現在具有代表 hello 使用者語彙基元 tooaccess Azure 資源管理員。 hello 下一個步驟是 tooconnect 應用程式 toohello 訂用帳戶。 連接之後，您的應用程式可以管理這些訂閱 hello 使用者不存在，即使 （長期離線存取）。

每個訂用帳戶 tooconnect，來呼叫 hello[資源管理員清單權限](https://docs.microsoft.com/rest/api/authorization/permissions)API toodetermine hello 使用者是否擁有存取 hello 訂用帳戶的管理權限。

hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44)的 hello ASP.NET MVC 範例應用程式的方法會實作此呼叫。

下列範例會示範如何 hello toorequest 訂用帳戶的使用者的權限。 83cfe939-2402-4581-b761-4f59b0a041e4 是 hello hello 訂用帳戶識別碼。

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

訂用帳戶的 hello 回應 tooget 使用者的權限的範例是：

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

hello 權限應用程式開發介面會傳回多個權限。 每個權限包含允許的動作 (actions) 和不允許的動作 (notactions)。 如果動作是否存在於 hello 允許的任何權限的動作清單以及 hello notactions 該權限清單中不存在，hello 使用者是否允許 tooperform 該動作。 **microsoft.authorization/roleassignments/write** hello 動作，授與存取管理權利。 您的應用程式必須剖析 hello 權限結果 toolook regex 相符項目在 hello 動作和每個權限的 notactions 中此動作字串。

## <a name="get-app-only-access-token"></a>取得僅限應用程式存取權杖
現在，您知道如果 hello 使用者可以指派存取 toohello Azure 訂用帳戶。 hello 後續的步驟如下：

1. 指派 hello 訂用帳戶的 hello 適當 RBAC 角色 tooyour 應用程式的識別碼。
2. 藉由查詢 hello 訂用帳戶上的 hello 應用程式的權限，或藉由存取資源管理員使用僅限應用程式的權杖驗證 hello 存取指派。
3. 您的應用程式 「 已連線的訂閱 」 資料結構-保存 hello 識別碼 hello 訂用帳戶中的記錄 hello 連接。

讓我們來看靠近 hello 第一個步驟。 tooassign hello 適當 RBAC 角色 toohello 應用程式的身分識別，您必須決定：

* hello hello 使用者的 Azure Active Directory 中的應用程式的身分識別的物件識別碼
* hello hello RBAC 角色應用程式所需 hello 訂用帳戶識別碼

當您的應用程式驗證來自 Azure AD 的使用者時，它會在該 Azure AD 中建立應用程式的服務主體物件。 Azure 可讓 RBAC 角色 toobe 指派 tooservice 主體 toogrant 直接存取 toocorresponding 應用程式上的 Azure 資源。 我們希望 toodo 此動作即完全相同。 查詢 hello Azure AD Graph API toodetermine hello hello 服務主體識別碼 hello 登入的使用者在應用程式的 Azure AD。

您只需要存取權杖的 Azure 資源管理員-您需要新的存取語彙基元 toocall hello Azure AD Graph API。 在 Azure AD 中的每個應用程式有權限 tooquery 它自己的服務主體物件，因此僅限應用程式的存取權杖已足夠。

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>取得 Azure AD Graph API 的僅限應用程式存取權杖
tooauthenticate 應用程式，並取得語彙基元 tooAzure AD Graph API，發出的用戶端認證授與 OAuth2.0 流程語彙基元要求 tooAzure AD 權杖端點 (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/語彙基元**).

hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs)方法的 ASP.net MVC 範例應用程式取得僅限應用程式的存取權杖以供使用 Graph API 的 hello hello Active Directory Authentication Library for.NET。

hello 查詢字串參數可用於此要求所述 hello[要求存取權杖](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token)主題。

用戶端認證授與權杖要求範例︰

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

用戶端認證授與權杖回應範例︰

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>取得使用者 Azure AD 中的應用程式服務主體的 ObjectId
現在，使用 hello 僅限應用程式的存取語彙基元 tooquery hello [Azure AD Graph 服務主體](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)API toodetermine hello hello 目錄中的 hello 應用程式的服務主體的物件識別碼。

hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。

下列範例會示範如何 hello toorequest 應用程式的服務主體。 a0448380-c346-4f9f-b897-c18733de9394 是 hello 用戶端識別碼 hello 應用程式。

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

hello 下列範例顯示的應用程式服務的回應 toohello 要求主體

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>取得 Azure RBAC 角色識別碼
tooassign hello 適當 RBAC 角色 tooyour 服務主體，您必須決定 hello hello Azure rbac 進行角色識別碼。

hello 右 RBAC 角色應用程式：

* 如果您的應用程式只會監視 hello 訂用帳戶，而不進行任何變更，則需要只有 hello 訂用帳戶的讀取器權限。 指派 hello**讀取器**角色。
* 如果您的應用程式為您管理 Azure 的 hello 訂用帳戶，建立/修改/刪除實體，它需要下列其中一個 hello 參與者權限。
  * toomanage 特定類型的資源，指派 hello 特定資源參與者角色 （虛擬機器參與者、 虛擬網路參與者、 儲存體帳戶參與者等）
  * toomanage 任何資源類型、 指派 hello**參與者**角色。

hello 應用程式的角色指派是可見的 toousers，因此選取 hello 最低所需的權限。

呼叫 hello[資源管理員角色定義 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist 所有 Azure rbac 進行角色和搜尋然後都逐一 hello 結果 toofind hello 預期角色定義的名稱。

hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。

hello 下列要求的範例會示範如何 tooget Azure rbac 進行角色識別碼。 09cbd307-aa71-4aca-b346-5f253e6e3ebb 是 hello hello 訂用帳戶識別碼。

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

hello 回應 hello 遵循格式為：

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

您不需要 toocall 持續不斷上的這個 API。 一旦您判定 hello hello 角色定義的已知 GUID，您可以建構 hello 角色定義 id 為：

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

以下是常用的內建角色的 hello 已知 guid:

| 角色 | Guid |
| --- | --- |
| 讀取器 |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| 參與者 |b24988ac-6180-42a0-ab88-20f7382dd24c |
| 虛擬機器參與者 |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| 虛擬網路參與者 |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| 儲存體帳戶參與者 |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| 網站參與者 |de139f84-1756-47ae-9be6-808fbbe84772 |
| Web 方案參與者 |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| SQL Server 參與者 |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| SQL DB 參與者 |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>指派 RBAC 角色 tooapplication
您擁有所需的所有 tooassign hello 適當 RBAC 角色 tooyour 服務主體使用 hello[資源管理員 建立角色指派](https://docs.microsoft.com/rest/api/authorization/roleassignments)應用程式開發介面。

hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。

範例要求 tooassign RBAC 角色 tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

在 hello 要求中，會使用下列值的 hello:

| Guid | 說明 |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |hello hello 訂閱識別碼 |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |hello hello hello 應用程式的服務主體的物件識別碼 |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |hello hello 讀取器角色識別碼 |
| 4f87261d-2816-465d-8311-70a27558df4c |新的 guid 建立 hello 新角色指派 |

hello 回應 hello 遵循格式為：

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>取得 Azure Resource Manager 的僅限應用程式存取權杖
toovalidate 該應用程式所需的 hello 存取 hello 訂用帳戶，請使用僅限應用程式的權杖 hello 訂用帳戶上執行的測試工作。

tooget 僅限應用程式的存取權杖，請依照指示執行區段[取得 Azure AD Graph api 的僅限應用程式的存取權杖](#app-azure-ad-graph)，具有不同的值為 hello resource 參數：

    https://management.core.windows.net/

hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) hello ASP.NET MVC 範例應用程式取得僅限應用程式的存取語彙基元的 Azure 資源管理員使用的方法 hello Active Directory Authentication Library for.net。

#### <a name="get-applications-permissions-on-subscription"></a>取得訂用帳戶上的應用程式權限
您的應用程式具有 hello 的 toocheck 想要針對 Azure 訂用帳戶的存取，您可能也會呼叫 hello[資源管理員 」 權限](https://docs.microsoft.com/rest/api/authorization/permissions)應用程式開發介面。 這個方法很類似 toohow 您決定 hello 使用者是否具有 hello 訂用帳戶的管理存取權限。 不過，這次呼叫 hello 權限應用程式開發介面使用 hello 上一個步驟中收到 hello 僅限應用程式的存取權杖。

hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110)的 hello ASP.NET MVC 範例應用程式的方法會實作此呼叫。

## <a name="manage-connected-subscriptions"></a>管理連接的訂用帳戶
當 hello 適當 RBAC 的角色指派 tooyour 應用程式的服務主體 hello 訂用帳戶時，您的應用程式可以保留監視/管理 Azure 資源管理員的使用僅限應用程式的存取權杖。

如果訂用帳戶擁有者移除您的應用程式使用 hello 傳統入口網站或命令列工具，您的應用程式的角色指派是不再能 tooaccess 該訂用帳戶。 在此情況下，您應通知 hello 使用者 hello 與 hello 訂用帳戶的連接已嚴重損毀來自外部的 hello 應用程式授與他們選項太 「 修復 」 hello 連線。 「 修復 」 只會重新建立 hello 離線已刪除的角色指派。

就如同您啟用 hello 使用者 tooconnect 訂閱 tooyour 應用程式，您必須太允許 hello 使用者 toodisconnect 訂用帳戶。 從存取管理的觀點，中斷連線移除 hello hello 應用程式的服務主體具有 hello 訂用帳戶的角色指派的方式。 （選擇性） 可能太移除 hello hello 訂用帳戶的應用程式中的任何狀態。
只有具有存取 hello 訂用帳戶的管理權限的使用者都能 toodisconnect hello 訂用帳戶。

hello [RevokeRoleFromServicePrincipalOnSubscription 方法](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200)hello ASP.net MVC 的範例應用程式會實作此呼叫。

大功告成，使用者現在能使用您的應用程式來輕鬆連接及管理其 Azure 訂用帳戶。
