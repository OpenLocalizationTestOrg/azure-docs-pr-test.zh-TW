---
title: "aaaUse Azure Active Directory tooauthenticate 批次管理解決方案 |Microsoft 文件"
description: "使用 Azure 資源管理員所建立的應用程式和 hello 批次資源提供者向 Azure AD。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>使用 Active Directory 驗證 Batch Management 解決方案

呼叫 hello Azure 批次管理服務應用程式向[Azure Active Directory] [ aad_about] (Azure AD)。 Azure AD 是 Microsoft 的多租用戶雲端型目錄和身分識別管理服務。 Azure 本身會使用 Azure AD hello 驗證其客戶、 服務管理員和組織使用者。

hello Batch Management.NET 程式庫會公開使用批次帳戶，帳戶金鑰、 應用程式和應用程式封裝的類型。 hello Batch Management.NET 程式庫是 Azure 資源提供者用戶端，並會搭配[Azure Resource Manager] [ resman_overview] toomanage 這些資源以程式設計的方式。 Azure AD 會透過任何 Azure 資源提供者用戶端，包括 hello Batch Management.NET 程式庫，以及透過需要的 tooauthenticate 要求[Azure Resource Manager][resman_overview]。

在本文中，我們會探討使用 Azure AD tooauthenticate 從使用 hello Batch Management.NET 程式庫的應用程式。 我們會示範如何在 Azure AD toouse tooauthenticate 訂用帳戶管理員或共同管理員，使用整合式驗證。 我們使用 hello [AccountManagment] [ acct_mgmt_sample] GitHub，toowalk 透過使用 Azure AD 與 hello Batch Management.NET 程式庫提供的範例專案。

toolearn 進一步了解使用 hello Batch Management.NET 程式庫和 hello AccountManagement 範例，請參閱[管理批次帳戶與配額與.NET 的 hello 批次管理用戶端程式庫](batch-management-dotnet.md)。

## <a name="register-your-application-with-azure-ad"></a>向 Azure AD 註冊您的應用程式

hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) 提供應用程式中的程式設計介面 tooAzure AD 供使用。 toocall ADAL 從您的應用程式，您必須在 Azure AD 租用戶中註冊您的應用程式。 當您註冊您的應用程式時，您會提供有關您的應用程式，包括其名稱 hello Azure AD 租用戶內資訊與 Azure AD。 然後 azure AD 提供應用程式識別碼，搭配 tooassociate 您的應用程式在執行階段的 Azure AD。 toolearn 深入了解 hello 應用程式識別碼，請參閱[應用程式與 Azure Active Directory 中的服務主體物件](../active-directory/develop/active-directory-application-objects.md)。

tooregister hello AccountManagement 範例應用程式，請遵循 hello 中的 hello 步驟[來新增應用程式](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application)一節中[整合應用程式與 Azure Active Directory] [ aad_integrate]. 指定**原生用戶端應用程式**hello 種應用程式。 hello 業界標準 OAuth 2.0 URI hello**重新導向 URI**是`urn:ietf:wg:oauth:2.0:oob`。 不過，您可以指定任何有效的 URI (例如`http://myaccountmanagementsample`) hello**重新導向 URI**，因為它並不需要 toobe 實際的端點：

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

一旦您完成 hello 註冊程序，您將看到 hello 應用程式識別碼，並 hello 列出您的應用程式的物件 （服務主體） 識別碼。  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>授與 hello Azure 資源管理員 API 存取 tooyour 應用程式

接下來，您將需要 toodelegate 存取 tooyour 應用程式 toohello Azure 資源管理員 API。 hello 資源管理員 API 的 hello Azure AD 識別項是**Windows Azure 服務管理 API**。

請遵循這些步驟 hello Azure 入口網站中：

1. 在 hello 左側導覽窗格中的 hello Azure 入口網站，選擇 **更服務**，按一下**應用程式註冊**，然後按一下**新增**。
2. 搜尋 hello hello 清單中的應用程式註冊您應用程式名稱：

    ![搜尋您的應用程式名稱](./media/batch-aad-auth-management/search-app-registration.png)

3. 顯示 hello**設定**刀鋒視窗。 在 hello **API 存取**區段中，選取**必要的權限**。
4. 按一下**新增**tooadd 新增必要的權限。 
5. 在步驟 1 中，輸入**Windows Azure 服務管理 API**、 從 hello 結果的清單中選取該應用程式開發介面，然後按一下 hello**選取** 按鈕。
6. 在步驟 2 中，選取 hello 核取方塊旁太**做為組織的使用者存取 Azure 傳統部署模型**，然後按一下 hello**選取**按鈕。
7. 按一下 hello**完成** 按鈕。

hello**必要的使用權限**現在顯示 tooyour 應用程式的權限會授與 tooboth hello ADAL 和資源管理員 Api 的 刀鋒視窗。 權限預設會授與 tooADAL 當您第一次使用 Azure AD 註冊您的應用程式。

![委派權限 toohello Azure 資源管理員 API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Azure AD 端點

tooauthenticate 批次管理解決方案與 Azure AD，您將需要兩個已知的端點。

- hello **Azure AD 的一般端點**提供一般認證未提供特定租用戶，如同 hello 案例中整合式驗證時，收集介面：

    `https://login.microsoftonline.com/common`

- hello **Azure 資源管理員端點**是使用的 tooacquire token 來驗證要求 toohello 批次管理服務：

    `https://management.core.windows.net/`

hello AccountManagement 範例應用程式定義這些端點的常數。 將這些常數保留不變︰

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>參考您的應用程式識別碼 

用戶端應用程式會在執行階段使用 hello 應用程式識別碼 （也參考的 tooas hello 用戶端識別碼） tooaccess Azure AD。 一旦您已 hello Azure 入口網站中註冊您的應用程式，更新 Azure AD 註冊應用程式所提供您的程式碼 toouse hello 應用程式識別碼。 Hello AccountManagement 範例應用程式，可以從 hello Azure 入口網站 toohello 適當常數複製應用程式識別碼：

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
也請複製 hello 重新導向 hello 註冊程序期間所指定的 URI。 hello 重新導向 URI 指定在您的程式碼必須符合 hello 重新導向時註冊 hello 應用程式所提供的 URI。

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>取得 Azure AD 驗證權杖

在 hello Azure AD 租用戶中註冊 hello AccountManagement 範例後，當您更新 hello 範例原始程式碼以您的值，hello 範例是使用 Azure AD 準備 tooauthenticate。 當您執行 hello 範例時，hello ADAL 嘗試 tooacquire 驗證權杖。 在此步驟中，它會提示您輸入您的 Microsoft 認證︰ 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

您提供認證之後，hello 範例應用程式可以繼續 tooissue 驗證要求 toohello 批次管理服務。 

## <a name="next-steps"></a>後續步驟

如需有關執行 hello [AccountManagement 範例應用程式][acct_mgmt_sample]，請參閱[管理批次帳戶與配額與 hello 批次管理用戶端程式庫適用於.NET](batch-management-dotnet.md).

toolearn 進一步了解 Azure AD，請參閱 hello [Azure Active Directory 文件](https://docs.microsoft.com/azure/active-directory/)。 深入了解範例來示範如何 toouse ADAL 位於 hello [Azure 程式碼範例](https://azure.microsoft.com/resources/samples/?service=active-directory)程式庫。

tooauthenticate 批次服務應用程式使用 Azure AD，請參閱[與 Active Directory 驗證批次服務解決方案](batch-aad-auth.md)。 


[aad_about]: ../active-directory/active-directory-whatis.md "什麼是 Azure Active Directory？"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD 的驗證案例"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "整合應用程式與 Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
