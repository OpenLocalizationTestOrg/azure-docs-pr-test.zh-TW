---
title: "Azure Active Directory 中的應用程式、權限及同意 | Microsoft Docs"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您與 Azure AD 整合 Office 365、 Azure 和 SaaS 應用程式的通用識別身分的 tooprovide。"
keywords: "什麼是 Azure AD Connect，簡介 tooAzure AD，應用程式，安裝 active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Azure Active Directory 中的應用程式、權限及同意
Azure Active directory，您可以新增應用程式 tooyour 目錄。  hello 應用程式的應用程式的 hello 類型而有所不同。  tooview hello 傳統入口網站中的應用程式選取目錄，然後選擇 [應用程式。

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。

## <a name="types-of-apps"></a>應用程式類型

1. **單一租用戶應用程式** </br>
    - **單一租用戶應用程式**-通常稱為 tooas 的特定業務 (LOB) 應用程式。 這是您組織內其他人開發自己的應用程式，並希望使用者在 toohello 應用程式中的 hello 組織 toobe 無法 toosign hello 情況。
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **應用程式 Proxy 應用程式**-時由內部部署應用程式與 Azure AD 應用程式 Proxy、 公開 （expose） 單一租用戶應用程式會在您的租用戶 （在加法 toohello 應用程式 Proxy 服務) 中註冊。 此應用程式便是代表所有雲端互動 (例如驗證) 之內部部署應用程式的項目  (應用程式 Proxy 需要 Azure AD Basic 或更高版本)。


2. **多租用戶應用程式**
    - **多租用戶應用程式的其他人可以同意**-類似太 「 單一租用戶應用程式，您的組織開發 」。 hello （除了 hello 應用程式本身中的 hello 邏輯） 的主要差異在於來自其他租用戶的使用者也可以同意 tooand toohello 應用程式中的符號。</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **其他人開發、且 Contoso 可同意的多租用戶應用程式**  (或簡稱「已同意的應用程式」)。這是 「 您的組織開發多租用戶應用程式 」 的 hello 缺陷。 另一個組織正在開發多租用戶應用程式時您組織的使用者可同意 toohello 應用程式，然後登入 tooit。
    - **Microsoft 第一方應用程式** - 代表 Microsoft 服務的應用程式。 您申請 hello 服務的 hello 事實有驅動同意。 有時候沒有特殊的 UX 和特定的第一方應用程式通常在建立原則，以存取 toohello 應用程式時所使用的邏輯。</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **預先整合應用程式**-應用程式用於 hello Azure AD App 資源庫，您可以加入 tooyour 目錄 tooprovide 單一登入 （和在某些情況下，佈建） toopopular SaaS 應用程式。
    - **Azure AD 單一登入**：可透過 SAML 2.0 或 OpenID Connect 等受支援登入通訊協定來與 Azure AD 整合之應用程式的「真實」SSO。 hello 精靈將引導您完成設定。
    - **密碼單一登入**: Azure AD 會安全地儲存 hello 應用程式中，hello 使用者的認證和 hello 認證會 「 插入 」 hello 登入表單的 hello Azure AD 應用程式存取瀏覽器延伸模組。 也稱為「密碼儲存庫存」。

## <a name="permissions"></a>權限

應用程式註冊時，執行 hello (也就是 hello developer) 的應用程式註冊的 hello 使用者定義的權限 hello 應用程式需要存取，以及哪些資源。 （hello 資源是，本身定義為其他應用程式）。例如，有人建置 mail 閱讀應用程式中，會說明其應用程式需要 hello 資源 「 Office 365 Exchange Online"hello"hello 登入的使用者身分存取信箱 」 權限：
    
![](media/active-directory-apps-permissions-consent/apps6.png)

為了讓一個應用程式 （hello 用戶端） toorequest 從另一個應用程式 （hello 資源） 的特定權限，hello hello 資源應用程式的開發人員會定義存在的 hello 權限。 在本例中，Microsoft hello hello 「 Office 365 Exchange 連線 」 資源應用程式擁有者已定義名為 「 hello 登入的使用者身分存取信箱 」 權限。

在定義的權限，hello 應用程式開發人員必須定義如果 hello 權限可以同意，或者是否需要獲得管理員同意。 這可讓開發人員 tooallow 使用者 tooconsent 上自己 tooapps 要求只低敏感度權限，但是需要系統管理員 tooconsent toomore 機密權限。 例如，hello"Azure Active Directory"資源應用程式，具有已定義，所以使用者可同意 tooapps，要求的有限的唯讀權限。  不過，行使系統管理員同意則需要完整讀取權限和所有寫入權限。

因為原生用戶端未經過驗證，因此定義為原生用戶端應用程式的應用程式只能要求委派的權限。 這表示在取得權杖時一律必須由實際使用者涉入。 在取得存取權杖時，Web 應用程式和 Web API (機密用戶端) 一律必須向 Azure AD 驗證。 這表示他們也擁有 hello 可能會要求僅限應用程式的權限。 例如，如果一個後端服務需要 tooauthenticate tooanother 後端服務。 要求僅限應用程式權限的應用程式一律需要系統管理員的同意。

摘要︰



- （用戶端） 的應用程式狀態 （資源） 的其他應用程式所需要的 hello 權限。
- （資源） 的應用程式狀態時公開的 tooother 應用程式 （用戶端） 的權限。
- 權限可以是僅限應用程式權限或委派的權限。
- 委派的權限可以標示為「允許使用者同意」或「需要系統管理員同意」。
- 應用程式的行為會為用戶端 （藉由宣告它需要權限 tooa 資源），做為資源 （藉由宣告它所公開的權限），或兩者。

## <a name="controls"></a>控制

hello 以下是不同的系統管理員 hello 控制項，可供所有這種行為的清單。 控制項可以存取 hello 從傳統入口網站中的 hello 系統管理員設定 hello 目錄下。

![](media/active-directory-apps-permissions-consent/apps7.png)

在 [hello Azure 入口網站中，在**管理**，**使用者設定**。

![](media/active-directory-apps-permissions-consent/apps11.png)



- 您可以控制使用者是否可以同意 tooapps:

在 [hello 傳統入口網站，選取 [**使用者可以給予應用程式的權限 tooaccess 其資料。**
![](media/active-directory-apps-permissions-consent/apps8.png)

在 [hello Azure 入口網站，選取 [**使用者可以允許其資料應用程式 tooaccess**。
![](media/active-directory-apps-permissions-consent/apps12.png)



- 您可以控制使用者是否可以註冊他們自己的單一租用戶 LOB 應用程式： 在 hello 傳統入口網站選取**使用者可以新增整合的應用程式。**
![](media/active-directory-apps-permissions-consent/apps9.png)

在 [hello Azure 入口網站，選取 [**使用者可以允許其資料應用程式 tooaccess**。
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>即使您允許使用者 tooregister 單一租用戶 LOB 應用程式，會有 toowhat 可以註冊的限制。  
>例如，不是目錄管理員的開發人員。
>
>- 使用者無法讓單一租用戶應用程式變成多租用戶應用程式。
>- 當登錄單一租用戶的 LOB 應用程式，使用者無法要求僅限應用程式的權限 tooother 應用程式。
>- 當登錄單一租用戶的 LOB 應用程式，使用者無法要求委派的權限 tooother 應用程式，如果這些權限需要系統管理員同意。
>- 使用者無法進行變更 tooapps，它們不是擁有者。



- 您可以控制使用者是否可以自行新增使用密碼 SSO 的預先整合應用程式 (也稱為「密碼儲存庫存」) ![](media/active-directory-apps-permissions-consent/apps10.png)



- 您可以控制在哪些情況下可以存取應用程式 (也就是條件式存取)。 請注意這適用於 toohello 用戶端應用程式和 toohello 資源應用程式。 因此，假設您設定條件式存取原則，指出該 hello 「 Office 365 Exchange Online"的應用程式只能存取從相容的電腦。  使用者嘗試 toouse 會要求權限 tooExchange 線上的用戶端應用程式時，此原則也會啟動。



- 您必須在其中應用程式已獲得同意的 tooand 正在使用哪些的可見性。

1.  當使用者同意時 tooan 應用程式時，ServicePrincipal 物件會建立 hello 租用戶中。 Hello 稽核報表中包含 ServicePrincipal 建立。
2.  使用者登入活動報表會告訴您哪些應用程式 hello 使用者登入。 

## <a name="example"></a>範例

例如，讓我們來看 hello"FabrikamMail 適用於 Office 365 」 應用程式，您已注意到您的租用戶中的使用者所登入至其中。 「FabrikamMail」是 Android 版的郵件讀取程式應用程式，由「Fabrikam, Inc.」所發行。 這屬於 hello"多租用戶應用程式其他開發，Contoso 同意 」。

如果使用者允許 tooconsent，他們取得同意提示 hello 第一次登入：![](media/active-directory-apps-permissions-consent/apps14.png)

「 存取您的信箱 」 為 「 Office 365 Exchange 連線 」 （也就是交換） 所公開的 hello"hello 登入的使用者身分存取信箱 」 權限的 hello 面對使用者的同意字串。

您可以看見 hello 權限適用於 Exchange （hello 資源），已加入您註冊 Office 365 時查閱 hello ServicePrincipal 物件。 在您的租用戶，以用於記錄不同的選項和組態中，您可以將 hello ServicePrincipal 物件的 hello 應用程式 」 執行個體 」。  您可以看到此使用 hello`Get-AzureADServicePrincipal`在 PowerShell 中。

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Hello 使用者按一下 [接受] 時，就會起始同意。 首先，「 FabrikamMail 適用於 Office 365 」 的 ServicePrincipal 物件就會建立 hello 租用戶中。 hello ServicePrincipal 看起來像這樣：

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

同意 tooan 應用程式 Oauth2PermissionGrant 之間建立連結 hello 下列：
  
- hello 使用者物件
- hello 用戶端應用程式 ServicePrincipalName (SPN)
- hello 資源應用程式 ServicePrincipalName (SPN)
- 在 [hello 資源應用程式的權限。  

FabrikamMail hello 案例，它看起來像這樣：

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** FabrikamMail 的服務主體的物件識別碼 (hello 取得剛建立的其中一個)， **PrincipalId** hello 使用者物件識別碼 （hello 使用者同意）， **ResourceId**是交換的服務主體的物件識別碼，範圍是已同意的交換中的 hello 權限)。

如果使用者不允許 tooconsent，就會看到指出該權限的螢幕為必要。

