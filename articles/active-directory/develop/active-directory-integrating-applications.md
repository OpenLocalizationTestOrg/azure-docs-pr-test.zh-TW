---
title: "應用程式與 Azure Active Directory aaaIntegrating |Microsoft 文件"
description: "Tooadd，如何更新或移除 Azure Active Directory (Azure AD) 中的應用程式詳細資料。"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: mbaldwin
ms.assetid: ae637be5-0b71-4b1e-b1fe-b83df3eb4845
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: lenalepa
ms.custom: aaddev
ms.reviewer: luleon
ms.openlocfilehash: c6bf1123bb3a4d78b55c1c55558e684fb844e687
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-applications-with-azure-active-directory"></a>整合應用程式與 Azure Active Directory
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

企業開發人員和軟體做為服務 (SaaS) 提供者可以開發商業雲端服務或企業營運應用程式可以整合 Azure Active Directory (Azure AD) tooprovide 安全登入和授權其服務。 toointegrate 應用程式或服務與 Azure AD，開發人員必須先向 Azure AD 透過 hello Azure 傳統入口網站 hello 他們的應用程式的詳細資料。

本文章將示範如何 tooadd、 更新或移除應用程式在 Azure AD 中。 您將了解 hello 不同類型的應用程式可以如何整合 Azure ad 的 tooconfigure 應用程式 tooaccess 其他資源，例如 web Api，等等。

toolearn hello 兩個 Azure AD 物件代表已註冊的應用程式和 hello 它們之間的關聯性的詳細資料請參閱[應用程式與服務主體物件](active-directory-application-objects.md); toolearn 更多關於 hello 的商標指導您應該使用開發與 Azure Active Directory 的應用程式時，請參閱[整合的應用程式的商標指導](active-directory-branding-guidelines.md)。

## <a name="adding-an-application"></a>新增應用程式
任何想 toouse hello 功能的 Azure AD 的應用程式必須先註冊 Azure AD 租用戶中。 此登錄程序牽涉到讓 Azure AD 應用程式，例如其所在的 hello URL 的詳細資料，請驗證使用者之後 hello URL toosend 回覆、 hello 識別 hello 應用程式，以及其他 URI。

如果您正在建置 web 應用程式只需要 toosupport 登入的使用者在 Azure AD 中，您只可以依照下列 hello 指示。 如果您的應用程式需要認證或權限 tooaccess tooa web API，或需要 tooallow 使用者從其他 Azure AD 租用戶 tooaccess，請參閱[更新應用程式](#updating-an-application)區段 toocontinue 設定您的應用程式。

### <a name="tooregister-a-new-application-in-hello-azure-portal"></a>tooregister hello Azure 入口網站中的新應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 左側導覽窗格中，選擇 **更服務**，按一下**應用程式註冊**，然後按一下**新增**。
4. 依照 hello 提示，並建立新的應用程式。 如果您想要 Web 應用程式或原生應用程式的特定範例，請查看我們的[快速入門](active-directory-developers-guide.md)。
  * Web 應用程式，提供 hello**登入 URL**，這是應用程式的 hello 基底 URL，使用者可以登入在例如`http://localhost:12345`。
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * 原生應用程式，提供**重新導向 URI**，哪些 Azure AD 使用 tooreturn 權杖回應。 輸入值特定 tooyour 應用程式。 例如`http://MyFirstAADApp`
5. 當您完成註冊之後時，Azure AD 會指派給您的應用程式的唯一用戶端識別碼，hello 應用程式識別碼。 已加入您的應用程式，而且您會針對您的應用程式採取 toohello 快速入門 頁面。 根據您的應用程式是 web 或原生應用程式，您會看到不同的選項如何 tooadd 額外的功能 tooyour 應用程式。 一旦新增您的應用程式，您可以開始更新中存取 web Api 中其他應用程式，您的應用程式 tooenable 使用者 toosign 或設定多租用戶應用程式 （可讓您的應用程式的其他組織 tooaccess）。

> [!NOTE]
> 根據預設，hello 新建立的應用程式註冊是從您的目錄 toosign tooyour 應用程式中設定的 tooallow 使用者。
> 
> 

## <a name="updating-an-application"></a>更新應用程式
一旦向 Azure AD 註冊您的應用程式之後，就可能需要更新 toobe tooprovide 存取 tooweb 應用程式開發介面，可供其他組織使用，等等。 本節說明您可能需要 tooconfigure 進一步應用程式的各種方式。 首先我們會啟動概觀 hello 同意架構，這是重要的 toounderstand，如果您要建立可供用戶端應用程式由您的組織或另一個組織中的開發人員所建立的資源/API 應用程式。

如需有關 hello Azure AD 中的運作方式驗證，請參閱[Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

### <a name="overview-of-hello-consent-framework"></a>Hello 同意架構的概觀
Azure AD 的同意架構讓您輕鬆 toodevelop 多租用戶 web 及原生用戶端應用程式需要 tooaccess web Api 受到 Azure AD 租用戶，不同於 hello hello 用戶端應用程式註冊的其中一個。 這些 web Api 還包括 hello Microsoft Graph API （tooaccess Azure Active Directory、 Intune 和 Office 365 中的服務） 和其他 Microsoft 服務 Api，此外 tooyour 擁有 web 應用程式開發介面。 hello 架構根據使用者或系統管理員身分詢問 toobe 註冊在他們的目錄，可能會存取目錄資料的同意 tooan 應用程式中，提供。

例如，如果 web 用戶端應用程式需要從 Office 365 的 hello 使用者 tooread 行事曆資訊，該使用者會需要的 tooconsent toohello 用戶端應用程式。 同意之後，hello 用戶端應用程式會代表 hello 使用者能 toocall hello Microsoft Graph API 並使用 hello 行事曆資訊所需。 hello [Microsoft Graph API](https://graph.microsoft.io)提供 Office 365 中的存取 toodata （例如行事曆和訊息從 Exchange、 網站和從 SharePoint 文件從 OneDrive、 OneNote、 Planner 活頁簿中的工作從筆記型電腦的清單Excel、 等） 以及使用者和群組從 Azure AD 與其他資料物件之多個 Microsoft 雲端服務。 

hello 同意架構建置在 OAuth 2.0 和各種不同的流程，例如授權碼授與和用戶端認證授與，採用公用或機密的用戶端。 藉由使用 OAuth 2.0，Azure AD 可讓可能 toobuild 許多不同類型的用戶端應用程式，例如，在電話、 tablet 伺服器或 web 應用程式，並存取 toohello 所需的資源。

如需詳細 hello 同意架構的相關資訊，請參閱[Azure AD 的 OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx)， [Azure AD 的驗證案例](active-directory-authentication-scenarios.md)，以及如需取得授權的存取 tooOffice 365 透過資訊Microsoft Graph，請參閱[Microsoft Graph 應用程式驗證](https://graph.microsoft.io/docs/authorization/auth_overview)。

#### <a name="example-of-hello-consent-experience"></a>Hello 同意體驗的範例
hello 下列步驟將說明 hello 應用程式開發人員和使用者的 hello 同意體驗運作方式。

1. 在 hello Azure 入口網站中的 web 用戶端應用程式的組態頁面上，設定您的應用程式需要使用 hello 功能表 hello 所需的權限 區段中的 hello 權限。
   
    ![權限 tooother 應用程式](./media/active-directory-integrating-applications/requiredpermissions.png)
2. 請考慮，已更新您的應用程式的權限、 hello 應用程式正在執行，而使用者是關於 toouse hello 第一次。 如果 hello 應用程式尚未取得存取或重新整理語彙基元，hello 應用程式需要 toogo tooAzure AD 的授權端點 tooobtain 授權碼可以使用的 tooacquire，新的存取和重新整理權杖。
3. 如果 hello 使用者不已通過驗證，則會要求他們 toosign tooAzure AD 中。
   
    ![使用者或系統管理員身分登入 tooAzure AD](./media/active-directory-integrating-applications/usersignin.png)
4. Hello 使用者登入之後，Azure AD 會決定是否 hello 使用者需要 toobe 顯示同意頁面。 這項決定根據是否 hello 使用者 （或其組織的系統管理員） 已授與 hello 應用程式同意。 如果尚未獲得同意，Azure AD 會提示使用者同意 hello，並會顯示它需要 toofunction hello 所需權限。 顯示在 hello 同意對話方塊中的 hello 集的權限是 hello 與 hello 委派的權限在 hello Azure 入口網站中選取的項目相同。
   
    ![使用者同意體驗](./media/active-directory-integrating-applications/consent.png)
5. Hello 使用者授與同意之後，授權碼會傳回 tooyour 應用程式，它可以兌換 tooacquire 存取權杖和重新整理權杖。 如需有關此流程的詳細資訊，請參閱 hello [web 應用程式 tooweb API 區段](active-directory-authentication-scenarios.md#web-application-to-web-api)一節中[Azure AD 的驗證案例](active-directory-authentication-scenarios.md)。

6. 身為管理員，您也可以在您的租用戶同意 tooan 應用程式代表所有 hello 使用者委派權限。 這將導致 hello 同意對話方塊中出現的 hello 租用戶中的每個使用者。 您可以從 hello [Azure 入口網站](https://portal.azure.com)從您的應用程式頁面。 從 hello**設定**刀鋒視窗，您的應用程式中，按一下**必要的使用權限**，然後按一下 [hello**授與權限**] 按鈕。 

    ![授與明確的系統管理員同意權限](./media/active-directory-integrating-applications/grantpermissions.png)
    
> [!NOTE]
> 授與明確同意使用 hello**授與權限**按鈕目前是否需要單一網頁應用程式 (SPA) 使用 ADAL.js，hello 存取權杖要求不同意提示，如果不同意將會失敗已經授與。   

### <a name="configuring-a-client-application-tooaccess-web-apis"></a>設定用戶端應用程式 tooaccess web 應用程式開發介面
為了讓 web/機密用戶端應用程式 toobe 無法 tooparticipate 需要驗證 （並取得存取權杖） 授權授與流程中，它必須建立安全的憑證。 hello hello Azure 入口網站所支援的預設驗證方法是用戶端識別碼 + 對稱金鑰。 本節將討論您的用戶端認證的 hello 組態步驟需要的 tooprovide hello 秘密金鑰。

此外，用戶端可以之前存取 web API 所公開資源的應用程式 (亦即： Microsoft Graph API)，hello 同意架構，可確保 hello 用戶端取得 hello 權限授與必要的、 根據 hello 要求的權限。 根據預設，所有的應用程式可以選擇權限從 Azure Active Directory (Graph API) 和 Azure 服務管理 API，與 hello Azure AD"啟用登入並讀取的使用者設定檔 」 權限預設已選取。 如果您的用戶端應用程式已在 Office 365 Azure AD 租用戶中註冊，則也可選取 SharePoint 與 Exchange Online 的 Web API 和權限。 您可以從選取[兩種類型的權限](active-directory-dev-glossary.md#permissions)hello 中下一個 toohello 預期的下拉式功能表 web API:

* 應用程式權限： 用戶端應用程式需要 tooaccess hello web API，直接以本身 （沒有使用者內容）。 這種類型的權限需要系統管理員的同意，而且無法供原生用戶端應用程式使用。
* 委派的權限： 用戶端應用程式需要 tooaccess hello web API 以 hello 登入的使用者，但受到 hello 選取權限的存取權。 這種類型的權限可以授與使用者，除非 hello 權限已設定為需要系統管理員的同意。 

> [!NOTE]
> 新增委派權限 tooan 應用程式不會自動授與內 hello 租用戶的同意 toohello 使用者 hello Azure 傳統入口網站中所顯示的一樣。 hello 使用者必須仍然可以手動同意的 hello 加入委派權限，在執行階段，除非 hello 系統管理員會按一下 hello**授與權限**按鈕 hello**必要的使用權限**區段hello Azure 入口網站中的 hello 應用程式頁面。 

#### <a name="tooadd-credentials-or-permissions-tooaccess-web-apis"></a>tooadd 認證或權限 tooaccess web 應用程式開發介面
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. tooadd 秘密金鑰對於 web 應用程式的認證，請按一下 hello hello 設定 刀鋒視窗中的 「 金鑰 」 一節。  
   
   * 新增金鑰的描述，然後選取 1 或 2 年的持續時間。 
   * hello 最右側資料行會包含 hello 金鑰值，儲存 hello 組態變更之後。 上一步是確定 toocome toothis 區段並複製它您叫用後儲存，因此您將需要為使用中用戶端應用程式在執行階段驗證期間。
5. tooadd 使用權限 tooaccess 資源應用程式開發介面從用戶端，按一下 [從 hello 設定] 刀鋒視窗的 hello 」 所需的權限 > 一節。 
   
   * 首先，請按一下 hello [新增] 按鈕。
   * 按一下您想從 toopick 資源 」 選取 [API] tooselect hello 類型。
   * 瀏覽可用的應用程式開發介面的 hello 清單，或使用 hello 搜尋方塊 tooselect 從 hello 可用資源的應用程式目錄中公開 web API。 按一下您感興趣，然後按一下 hello 資源**選取**。
   * 選取之後，您可以移動 toohello**選取權限**功能表上，您可以選取 hello"應用程式權限 」 和 「 委派的權限 」 應用程式。
   
6. 完成後，請按一下 hello**完成** 按鈕。

> [!NOTE]
> 按一下 hello**完成**按鈕也會自動設定 hello 權限，在您的目錄中的應用程式根據 hello 權限 tooother 應用程式在您的設定。  您可以藉由查看 hello 應用程式中檢視這些應用程式權限**設定**刀鋒視窗。
> 
> 

### <a name="configuring-a-resource-application-tooexpose-web-apis"></a>設定資源應用程式 tooexpose web 應用程式開發介面
您可以開發 web 應用程式開發介面，並藉由將存取權公開可用 tooclient 應用程式讓它[範圍](active-directory-dev-glossary.md#scopes)和[角色](active-directory-dev-glossary.md#roles)。 Hello 其他 Microsoft 的 web Api，包括 Graph API hello 和 hello Office 365 Api 時，一樣，都可以提供正確設定的 web API。 存取範圍和角色會透過[應用程式的資訊清單](active-directory-dev-glossary.md#application-manifest) (此為代表應用程式身分識別組態的 JSON 檔案) 公開。  

hello 之後 > 一節將說明如何 tooexpose 存取範圍限制，藉由修改 hello 資源應用程式的資訊清單。

#### <a name="adding-access-scopes-tooyour-resource-application"></a>新增存取領域 tooyour 資源應用程式
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. 按一下**資訊清單**從 hello 應用程式頁面 tooopen hello 內嵌資訊清單編輯器。 
5. 取代下列 JSON 片段 hello"oauth2Permissions"節點。 這個程式碼片段是一種稱為 「 使用者模擬 」，可讓用戶端應用程式的資源擁有者 toogive 範圍 tooexpose 委派存取 tooa 資源的方式範例。 請確定您的應用程式變更的 hello 文字和值：
   
        "oauth2Permissions": [
        {
            "adminConsentDescription": "Allow hello application full access toohello Todo List service on behalf of hello signed-in     user",
            "adminConsentDisplayName": "Have full access toohello Todo List service",
            "id": "b69ee3c9-c40d-4f2a-ac80-961cd1534e40",
            "isEnabled": true,
            "type": "User",
            "userConsentDescription": "Allow hello application full access toohello todo service on your behalf",
            "userConsentDisplayName": "Have full access toohello todo service",
            "value": "user_impersonation"
            }
        ],
   
    hello 識別碼值必須是使用您建立新產生的 GUID [GUID 產生工具](https://msdn.microsoft.com/library/ms241442%28v=vs.80%29.aspx)或以程式設計的方式。 它代表 hello hello web API 所公開的權限的唯一識別碼。 一旦您的用戶端已適當地設定 toorequest 存取 tooyour web API 並呼叫 hello web API，它將會顯示具有 hello 範圍 (scp) 宣告集 toohello 值以上版本，在此情況下為 user_impersonation 的 OAuth 2.0 JWT 權杖。
   
   > [!NOTE]
   > 稍後您可以視需要公開其他範圍。 請考慮您的 Web API 可能會公開多個與各種不同功能相關聯的範圍。 現在您可以控制在收到 hello OAuth 2.0 JWT 權杖中的存取 toohello web 應用程式開發介面使用 hello 範圍 (scp) 宣告。
   > 
   > 
6. 按一下**儲存**toosave hello 資訊清單。 您的 web api 現在設定 toobe 目錄中的其他應用程式使用。

#### <a name="tooverify-hello-web-api-is-exposed-tooother-applications-in-your-directory"></a>tooverify hello web API 是您目錄中的公開的 tooother 應用程式
1. 在 hello 上方功能表中，按一下 [**應用程式註冊**，選取 hello 預期想 tooconfigure 存取 toohello web API 和瀏覽 toohello 設定] 刀鋒視窗的用戶端應用程式。
2. 從 hello**必要的使用權限**區段中，選取剛才公開權限的 hello web API。 從 hello 委派的權限下拉式功能表，選取 hello 新權限。

![顯示待辦事項清單權限](./media/active-directory-integrating-applications/todolistpermissions.png)

#### <a name="more-on-hello-application-manifest"></a>需 hello 應用程式資訊清單的詳細資訊
hello 應用程式資訊清單實際上做為更新 hello 應用程式實體定義的所有屬性的 Azure AD 應用程式的身分識別設定，包括我們討論 hello API 的存取範圍機制。 如需有關 hello 應用程式的實體的詳細資訊，請參閱 hello [Graph API 的應用程式實體文件](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity)。 中，您會找到 hello 應用程式的實體成員使用 toospecify 您 API 權限的完整參考有關：  

* hello appRoles 成員，也就是集合的[AppRole](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type)可使用的 toodefine hello 實體**應用程式權限**web API  
* hello oauth2Permissions 成員，也就是集合的[OAuth2Permission](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type)可使用的 toodefine hello 實體**委派的權限**web API

如需有關應用程式資訊清單的概念一般情況下，請參閱太[了解 hello Azure Active Directory 應用程式資訊清單](active-directory-application-manifest.md)。

### <a name="accessing-hello-azure-ad-graph-and-office-365-via-microsoft-graph-apis"></a>Hello Azure AD Graph 和 Microsoft Graph Api 透過 Office 365 存取  
提到更早版本，除了 tooexposing/存取 Api 對資源應用程式，您也可以更新您的用戶端應用程式 tooaccess Microsoft 資源所公開的 Api。  hello 稱為 「 Microsoft Graph"hello 清單中的權限 tooother 應用程式，可用的 「 Microsoft Graph API 或使用 Azure AD 註冊的所有應用程式。 如果您在 Office 365 所佈建的 Azure AD 租用戶中註冊用戶端應用程式，您也可以存取所有 hello hello Microsoft Graph API toovarious Office 365 資源所公開的權限。

Microsoft Graph API 所公開的存取領域的完整討論，請參閱 hello[權限範圍 |Microsoft Graph API 概念](https://graph.microsoft.io/docs/authorization/permission_scopes)發行項。

> [!NOTE]
> Tooa 目前的限制，因為原生用戶端應用程式，才能呼叫 hello Azure AD Graph API 使用 hello 「 存取貴組織的目錄 」 權限。  這項限制不適用於 web 應用程式。
> 
> 

### <a name="configuring-multi-tenant-applications"></a>設定多租用戶應用程式
新增應用程式 tooAzure AD，您可以只由您組織中的使用者存取您的應用程式 toobe。 或者，您可以由外部組織的使用者存取您的應用程式 toobe。 這兩個應用程式類型稱為單一租用戶和多租用戶應用程式。 您可以修改單一租用戶應用程式 toomake hello 設定它的多租用戶應用程式，本節將討論如下。

它是單一租用戶與多租用戶應用程式之間的重要 toonote hello 差異：  

* 單一租用戶應用程式適合在一個組織中使用。 它們通常是由企業開發人員撰寫的企業營運 (LoB) 應用程式。 單一租用戶應用程式只需要一個目錄中的使用者存取 toobe，如此一來，它只需要 toobe 佈建一個目錄中。
* 多租用戶應用程式適合在許多組織中使用。 它們是通常由獨立軟體廠商 (ISV) 撰寫的軟體即服務 (SaaS) Web 應用程式。 多租用戶應用程式需要在每個目錄中會使用這些，需要使用者或系統管理員同意 tooregister 中佈建 toobe 它們透過 hello Azure AD 的同意架構支援。 請注意，所有的原生用戶端應用程式預設的多租用戶 hello 資源擁有者的裝置上安裝。 Hello 同意架構，請參閱 hello hello 同意架構前一節，如需詳細資訊的概觀。

#### <a name="enabling-external-users-toogrant-your-application-access-tootheir-resources"></a>啟用外部使用者 toogrant 應用程式存取 tootheir 資源
如果您撰寫的應用程式的 toomake 可用 tooyour 客戶或合作夥伴組織外，您必須在 hello Azure 入口網站中的 tooupdate hello 應用程式定義。

> [!NOTE]
> 啟用多租用戶時，您必須確定應用程式的應用程式識別碼 URI 屬於已驗證的網域。 此外，hello 傳回 URL 必須以 https:// 開頭。 如需詳細資訊，請參閱 [應用程式物件和服務主體物件](active-directory-application-objects.md)。
> 
> 

tooenable 外部使用者的存取 tooyour 應用程式： 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. 從 hello 設定刀鋒視窗中，按一下 **屬性**和翻轉的 hello**多重 tenanted**太切換**是**。

您所做變更上述使用者和系統管理員在其他組織中的 hello 才能夠 toogrant 您應用程式存取 tootheir 目錄及其他資料。

#### <a name="triggering-hello-azure-ad-consent-framework-at-runtime"></a>觸發 hello Azure AD 的同意架構在執行階段
toouse hello 同意架構，多租用戶的用戶端應用程式必須使用 OAuth 2.0 授權要求。 [程式碼範例](https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multi-tenant)是您如何 web 應用程式、 原生應用程式或伺服器/精靈應用程式要求授權碼和存取權杖 toocall 可用 tooshow web 應用程式開發介面。

Web 應用程式也可提供使用者的註冊體驗。 如果您提供註冊體驗，預期 hello 使用者會按一下註冊按鈕，將會重新導向 hello 瀏覽器 toohello Azure AD OAuth2.0 授權端點或 OpenID Connect 使用者資訊端點。 這些端點可讓藉由檢查 hello id_token hello 應用程式 tooget hello 新使用者資訊。 下列 hello 註冊階段 hello 使用者會看到同意提示類似 toohello hello 概觀 hello 同意架構 > 一節中，如上所示的其中一個。

或者，您的 web 應用程式可能還會提供可讓系統管理員太 「 註冊我的公司 」 的體驗。 此體驗也會重新導向 hello 使用者 toohello Azure AD OAuth 2.0 授權端點。 在此情況下，您傳遞提示 = admin_consent 參數 toohello 授權端點 tooforce hello 系統管理員同意體驗，hello 系統管理員會授與同意，代表其組織。 只有屬於 toohello 全域管理員角色的帳戶進行驗證的使用者可以提供同意。其他人會收到錯誤。 成功同意時，hello 回應將包含 admin_consent = true。 當兌換存取權杖，您也會收到 hello 組織會提供相關資訊的 id_token 和 hello 註冊您的應用程式的系統管理員。

### <a name="enabling-oauth-20-implicit-grant-for-single-page-applications"></a>啟用單一頁面應用程式的 OAuth 2.0 隱含授權
單一頁面應用程式的 (SPAs) 的結構通常與 hello 瀏覽器，它會呼叫 hello 應用程式的 web API 後端 tooperform 其商務邏輯中執行的 JavaScript 繁重前端。 SPAs 裝載在 Azure AD 中，為方法，您可以使用 Azure AD 的 OAuth 2.0 隱含授予 tooauthenticate hello 使用者，並取得語彙基元，您可以使用 toosecure hello 應用程式的 JavaScript 用戶端 tooits 從回撥結束 web API。 Hello 使用者已授與同意之後，這個相同的驗證通訊協定可以使用的 tooobtain 語彙基元 toosecure 呼叫 hello 用戶端和其他設定 hello 應用程式的 web API 資源之間。 toolearn 進一步了解 hello 隱含授權授與，並協助您決定是否適合您應用程式的案例，請參閱[了解 hello OAuth2 隱含授予 Azure Active Directory 中的資料流程](active-directory-dev-understanding-oauth2-implicit-grant.md)。

根據預設，應用程式的 OAuth 2.0 隱含授權會停用。 您可以啟用 OAuth 2.0 隱含授予您的應用程式的設定 hello`oauth2AllowImplicitFlow`值在其[應用程式資訊清單](active-directory-application-manifest.md)，即表示您的應用程式識別設定的 JSON 檔案。

#### <a name="tooenable-oauth-20-implicit-grant"></a>tooenable OAuth 2.0 隱含授予
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. 從 hello 應用程式] 頁面上，按一下 [**資訊清單**tooopen hello 內嵌資訊清單編輯器。
   找出並設定太"true 的"hello"oauth2AllowImplicitFlow"值。 根據預設，它是 “false”。
   
    `"oauth2AllowImplicitFlow": true,`
5. 儲存更新的 hello 資訊清單。 儲存之後，您的 web api 現在設定 toouse OAuth 2.0 隱含授予 tooauthenticate 使用者。


## <a name="removing-an-application"></a>移除應用程式
本章節描述如何 tooremove 應用程式從您的 Azure AD 租用戶。

### <a name="removing-an-application-authored-by-your-organization"></a>移除您的組織所編寫的應用程式
這些是 Azure AD 租用戶的顯示 hello 主要的 [應用程式] 頁面上的 hello"應用程式我的公司擁有 」 篩選器下的 hello 應用程式。 在技術詞彙中，這些應用程式註冊，讓您以手動方式透過 hello Azure 傳統入口網站，或是以程式設計方式透過 PowerShell 或 hello Graph API。 更具體來說，它們會由您租用戶中的應用程式與服務主體物件所表示。 如需詳細資訊，請參閱 [應用程式物件和服務主體物件](active-directory-application-objects.md) 。

#### <a name="tooremove-a-single-tenant-application-from-your-directory"></a>tooremove 單一租用戶應用程式，從您的目錄
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. 從 hello 應用程式] 頁面上，按一下 [**刪除**。
5. 按一下**是**hello 確認訊息中。

#### <a name="tooremove-a-multi-tenant-application-from-your-directory"></a>tooremove 的多租用戶應用程式，從您的目錄
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 選擇您的 Azure AD 租用戶 hello 右上角的 hello 頁面中選取您的帳戶。
3. 在 hello 上方的功能表上選擇  **Azure Active Directory**，按一下**應用程式註冊**，然後按一下您想要 tooconfigure hello 應用程式。 這會帶您 toohello 應用程式的快速入門 頁面上，以及開啟 hello hello 應用程式的設定 刀鋒視窗。
4. 從 hello 設定刀鋒視窗中，選擇 **屬性**和翻轉的 hello**多重 tenanted**太切換**否**。 這會將轉換您的應用程式 toobe 單一租用戶，但 hello 應用程式仍會保留在組織內已同意 tooit。
5. 按一下 hello**刪除**從 hello 應用程式頁面上的按鈕。
6. 按一下**是**hello 確認訊息中。

### <a name="removing-a-multi-tenant-application-authorized-by-another-organization"></a>移除其他組織授權的多租用戶應用程式
這些是 Azure AD 租用戶，特別是 hello hello"應用程式我的公司擁有 」 清單下未列出的項目顯示 hello 主要的 [應用程式] 頁面上的 hello"應用程式我的公司會使用"篩選器下的 hello 應用程式的子集。 在技術詞彙中，這些是多租用戶應用程式註冊期間 hello 同意程序。 更具體來說，它們僅由您租用戶中的服務主體物件表示。 如需詳細資訊，請參閱 [應用程式物件和服務主體物件](active-directory-application-objects.md) 。

若要 tooremove tooyour directory 的多租用戶應用程式的存取權 （在同意之後），hello 公司系統管理員必須擁有 Azure 訂用帳戶 tooremove 存取透過 hello Azure 入口網站。 或者，hello 公司系統管理員可以使用 hello [Azure AD PowerShell Cmdlet](http://go.microsoft.com/fwlink/?LinkId=294151) tooremove 存取。

## <a name="next-steps"></a>後續步驟
* 請參閱 hello[整合的應用程式的商標指導](active-directory-branding-guidelines.md)如需有關您的應用程式的視覺化導引秘訣。
* 如需有關 hello 應用程式的應用程式和服務主體物件之間的關聯性的詳細資訊，請參閱[應用程式與服務主體物件](active-directory-application-objects.md)。
* toolearn 深入了解 hello 角色 hello 應用程式資訊清單播放，請參閱[了解 hello Azure Active Directory 應用程式資訊清單](active-directory-application-manifest.md)
* 請參閱 hello [Azure AD 開發人員詞彙](active-directory-dev-glossary.md)一些 hello 核心 Azure Active Directory (AD) 開發人員概念的定義。
* 請瀏覽 hello [Active Directory 開發人員手冊 》](active-directory-developers-guide.md)所有開發人員的概觀與相關內容。

