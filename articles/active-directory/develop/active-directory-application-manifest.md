---
title: "Azure Active Directory 應用程式資訊清單的 aaaUnderstanding hello |Microsoft 文件"
description: "Hello Azure Active Directory 應用程式資訊清單，代表在 Azure AD 租用戶的應用程式的身分識別設定，並且是使用的 toofacilitate OAuth 授權、 同意體驗，以及更多詳細的涵蓋範圍。"
services: active-directory
documentationcenter: 
author: sureshja
manager: mbaldwin
editor: 
ms.assetid: 4804f3d4-0ff1-4280-b663-f8f10d54d184
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: sureshja
ms.custom: aaddev
ms.reviewer: elisol
ms.openlocfilehash: 096c9d5501edbfc08731fea670cee559d4442ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-azure-active-directory-application-manifest"></a>了解 hello Azure Active Directory 應用程式資訊清單
整合與 Azure Active Directory (AD) 的應用程式必須向 Azure AD 租用戶，提供 hello 應用程式的持續性識別組態。 此組態會參考在執行階段，啟用 允許應用程式 toooutsource 和 broker 驗證/授權透過 Azure AD 的案例。 如需 hello Azure AD 應用程式模型的詳細資訊，請參閱 hello[加入、 更新和移除應用程式][ ADD-UPD-RMV-APP]發行項。

## <a name="updating-an-applications-identity-configuration"></a>更新應用程式的身分識別組態
有可用於更新的功能和程度的困難，包括 hello 下列不同的 hello 屬性在應用程式的身分識別設定中，實際的多個選項：

* hello  **[Azure 入口網站][ AZURE-PORTAL] Web 使用者介面**可讓您的應用程式 tooupdate hello 最常見內容。 這是最快的 hello 和最小錯誤容易出錯方式更新您的應用程式屬性，但並不會讓您完整存取 tooall 屬性，例如 hello 下面兩個方法。
* 對於進階案例中，您需要 tooupdate 屬性未公開在 hello Azure 傳統入口網站中，您可以修改 hello**應用程式資訊清單**。 這是 hello 這篇文章的焦點，且啟動 hello 下一節中詳細討論。
* 此外，也可以太**撰寫的應用程式使用 hello [Graph API] [ GRAPH-API]**  tooupdate 應用程式，這需要 hello 大部分投入時間。 不過，如果您要撰寫管理軟體，或需要定期以自動化方式 tooupdate 應用程式屬性，這可能是一個不錯的選擇。

## <a name="using-hello-application-manifest-tooupdate-an-applications-identity-configuration"></a>使用 hello 應用程式資訊清單 tooupdate 應用程式的身分識別設定
透過 hello [Azure 入口網站][AZURE-PORTAL]，您可以藉由更新 hello 應用程式資訊清單使用 hello 內嵌資訊清單編輯器來管理您的應用程式識別組態。 您也可以下載並上傳 hello 成為 JSON 檔案的應用程式資訊清單。 沒有實際的檔案會儲存在 hello 目錄。 hello 應用程式資訊清單是只是 HTTP GET 作業上 hello Azure AD Graph API 應用程式的實體，而 hello 上載 HTTP PATCH 操作上 hello 應用程式的實體。

如此一來，在順序 toounderstand hello 格式和內容 hello 應用程式資訊清單，您將需要 tooreference hello Graph API[應用程式的實體][ APPLICATION-ENTITY]文件。 可透過應用程式資訊清單上傳執行的更新範例包括：

* **宣告您的 Web API 所公開的權限範圍 (oauth2Permissions)** 。 請參閱中的 hello"公開 Web Api tooOther 應用程式 」 主題[整合應用程式與 Azure Active Directory] [ INTEGRATING-APPLICATIONS-AAD]如需實作使用 hello 的使用者模擬資訊oauth2Permissions 委派權限範圍。 如先前所述，應用程式實體屬性都記錄於 hello Graph API[實體和複雜型別][ APPLICATION-ENTITY]參考文件，包括 hello oauth2Permissions 屬性型別的集合[OAuth2Permission][APPLICATION-ENTITY-OAUTH2-PERMISSION]。
* **宣告您的應用程式所公開的應用程式角色 (appRoles)**。 hello 應用程式的實體 appRoles 屬性為集合型別的[AppRole][APPLICATION-ENTITY-APP-ROLE]。 請參閱 hello[角色型存取控制雲端應用程式使用 Azure AD 中的][ RBAC-CLOUD-APPS-AZUREAD]發行項的實作範例。
* **宣告已知的用戶端應用程式 (knownClientApplications)**，可讓您 toologically tie hello 同意的 hello 指定用戶端應用程式 toohello 資源/web API。
* **要求 Azure AD tooissue 群組成員資格宣告**hello 登入的使用者 (groupMembershipClaims)。  這也可以設定的 tooissue hello 使用者的目錄角色成員資格有關的宣告。 請參閱 hello[使用 AD 群組的雲端應用程式中的授權][ AAD-GROUPS-FOR-AUTHORIZATION]發行項的實作範例。
* **允許您的應用程式 toosupport OAuth 2.0 隱含授予**流程 (oauth2AllowImplicitFlow)。 此類型的授權流程可用於內嵌的 JavaScript 網頁或單一頁面應用程式 (SPA)。 如需有關 hello 隱含授權授與的詳細資訊，請參閱[了解 hello OAuth2 隱含授予 Azure Active Directory 中的資料流程][IMPLICIT-GRANT]。
* **啟用使用 X509 憑證 hello 祕密金鑰**(keyCredentials)。 請參閱 hello[建置在 Office 365 中的服務和服務精靈應用程式][ O365-SERVICE-DAEMON-APPS]和[使用 Azure 資源管理員 API 的開發人員指南 tooauth] [ DEV-GUIDE-TO-AUTH-WITH-ARM]如需實作範例的文件。
* 為應用程式**新增應用程式識別碼 URI** (identifierURIs[])。 應用程式識別碼 Uri 可用 toouniquely 識別應用程式在其 Azure AD 租用戶 （或跨多個 Azure AD 租用戶，為多租用戶案例限定透過驗證的自訂網域時）。 要求權限 tooa 資源應用程式時，它們會使用或取得資源的應用程式的存取權杖。 當您更新此項目時，hello 相同的更新是由 toohello 對應服務主體的 servicePrincipalNames [] 集合，其位於 hello 應用程式的主要租用戶。

hello 應用程式資訊清單也會提供很好的方式 tootrack hello 的應用程式註冊狀態。 因為它使用 JSON 格式，hello 檔案表示法可以簽入到您的原始檔控制，以及您的應用程式的原始程式碼。

## <a name="step-by-step-example"></a>逐步執行範例
現在可讓逐步解說 hello 步驟需要 tooupdate 透過 hello 應用程式資訊清單的應用程式的身分識別組態。 我們會反白顯示 hello 前面的範例，其中顯示如何 toodeclare 新權限範圍資源應用程式上：

1. 登入 toohello [Azure 入口網站][AZURE-PORTAL]。
2. 已通過驗證之後，選擇您的 Azure AD 租用戶從 hello 右上角的 hello 頁面中選取它。
3. 選取**Azure Active Directory** hello 剩餘的導覽面板，然後按一下延伸**應用程式註冊**。
4. 尋找您想要在清單中的 hello tooupdate 並加以點選 「 hello 」 應用程式。
5. 從 hello 應用程式] 頁面上，按一下 [**資訊清單**tooopen hello 內嵌資訊清單編輯器。 
6. 您可以直接編輯使用此編輯器的 hello 資訊清單。 請注意該 hello 資訊清單會遵循 hello hello 結構描述[應用程式的實體][ APPLICATION-ENTITY]如前所述： 例如，假設我們想要 tooimplement 公開新的權限呼叫 「 Employees.Read.All"在我們資源的應用程式 (API)，您只可以 ie 加入秒新項目 toohello oauth2Permissions 集合：
   
        "oauth2Permissions": [
        {
        "adminConsentDescription": "Allow hello application tooaccess MyWebApplication on behalf of hello signed-in user.",
        "adminConsentDisplayName": "Access MyWebApplication",
        "id": "aade5b35-ea3e-481c-b38d-cba4c78682a0",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application tooaccess MyWebApplication on your behalf.",
        "userConsentDisplayName": "Access MyWebApplication",
        "value": "user_impersonation"
        },
        {
        "adminConsentDescription": "Allow hello application toohave read-only access tooall Employee data.",
        "adminConsentDisplayName": "Read-only access tooEmployee records",
        "id": "2b351394-d7a7-4a84-841e-08a6a17e4cb8",
        "isEnabled": true,
        "type": "User",
        "userConsentDescription": "Allow hello application toohave read-only access tooyour Employee data.",
        "userConsentDisplayName": "Read-only access tooyour Employee records",
        "value": "Employees.Read.All"
        }
        ],
   
    hello 項目必須是唯一的並因此，您必須產生新全域唯一識別碼 (GUID) hello`"id"`屬性。 在此情況下，因為我們指定`"type": "User"`，此權限可以是已獲得同意的 tooby hello Azure AD 租用戶中的 hello 註冊資源/API 應用程式的任何帳戶驗證。 此授與 hello 用戶端應用程式的權限 tooaccess hello 帳戶代表它。 決定同意期間和 hello Azure 入口網站中顯示的資料，會使用 hello 描述和顯示名稱的字串。
6. 當您完成更新 hello 資訊清單時，按一下 **儲存**toosave hello 資訊清單。  
   
既然 hello 資訊清單會儲存，您可以提供已註冊的用戶端應用程式存取 toohello 新權限上述我們新增。 您可以使用這個時間 hello Azure 入口網站 Web UI，而不是編輯 hello 用戶端應用程式的資訊清單：  

1. 先前往 toohello**設定**刀鋒視窗中的 hello 按一下您想 tooadd 存取 toohello 新 API，用戶端應用程式 toowhich**必要的使用權限**選擇**選取應用程式開發介面**.
2. 然後您會有 hello hello 租用戶中登錄的資源應用程式 (Api) 清單。 它，或型別 hello 名稱 hello 應用程式 hello 搜尋] 方塊中，按一下 [hello 資源應用程式 tooselect。 當您發現 hello 應用程式時，按一下**選取**。  
3. 這會帶您 toohello**選取權限**頁面上，將會顯示 hello 的應用程式權限和委派權限，可用於 hello 資源應用程式的清單。 選取 hello tooadd 順序中的新權限它 toohello 用戶端的要求的權限清單。 這個新權限會儲存在 hello"requiredResourceAccess 」 集合屬性中的 hello 用戶端應用程式的身分識別組態。


就這麼簡單。 現在，您的應用程式將會使用其新的身分識別組態來執行。

## <a name="next-steps"></a>後續步驟
* 如需有關 hello 應用程式的應用程式和服務主體物件之間的關聯性的詳細資訊，請參閱[應用程式和服務主體物件，在 Azure AD 中的][AAD-APP-OBJECTS]。
* 請參閱 hello [Azure AD 開發人員詞彙][ AAD-DEVELOPER-GLOSSARY]一些 hello 核心 Azure Active Directory (AD) 開發人員概念的定義。

請使用以下 tooprovide 意見反應 hello 註解區段，然後幫助我們改善並圖形內容。

<!--article references -->
[AAD-APP-OBJECTS]: active-directory-application-objects.md
[AAD-DEVELOPER-GLOSSARY]: active-directory-dev-glossary.md
[AAD-GROUPS-FOR-AUTHORIZATION]: http://www.dushyantgill.com/blog/2014/12/10/authorization-cloud-applications-using-ad-groups/
[ADD-UPD-RMV-APP]: active-directory-integrating-applications.md
[APPLICATION-ENTITY]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[APPLICATION-ENTITY-APP-ROLE]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#approle-type
[APPLICATION-ENTITY-OAUTH2-PERMISSION]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#oauth2permission-type
[AZURE-PORTAL]: https://portal.azure.com
[DEV-GUIDE-TO-AUTH-WITH-ARM]: http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/
[GRAPH-API]: active-directory-graph-api.md
[IMPLICIT-GRANT]: active-directory-dev-understanding-oauth2-implicit-grant.md
[INTEGRATING-APPLICATIONS-AAD]: https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
[O365-PERM-DETAILS]: https://msdn.microsoft.com/office/office365/HowTo/application-manifest
[O365-SERVICE-DAEMON-APPS]: https://msdn.microsoft.com/office/office365/howto/building-service-apps-in-office-365
[RBAC-CLOUD-APPS-AZUREAD]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/

