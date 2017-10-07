---
title: "Azure Active Directory 中預先整合應用程式的 hello SAML 權杖中發出的 aaaCustomizing 宣告 |Microsoft 文件"
description: "了解 toocustomize hello 發出宣告的方式在 hello Azure Active Directory 中預先整合應用程式的 SAML 權杖"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: f1daad62-ac8a-44cd-ac76-e97455e47803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.custom: aaddev
ms.openlocfilehash: a376318929472403e799f02fdd3fbddc91d0a70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-claims-issued-in-hello-saml-token-for-pre-integrated-apps-in-azure-active-directory"></a>Azure Active Directory 中預先整合應用程式的 SAML 權杖在 hello 自訂宣告發出
Azure Active Directory 現在支援數千種預先整合的應用程式中 hello Azure AD 應用程式庫，包括超過支援單一登入的 360 使用 hello SAML 2.0 通訊協定。 當使用者透過 Azure AD 使用 SAML tooan 應用程式，Azure AD 會傳送權杖 toohello 應用程式 （透過 HTTP POST)。 與然後 hello 應用程式會驗證使用中的 hello 語彙基元 toolog hello 使用者而不是提示輸入使用者名稱和密碼。 這些 SAML 權杖包含 hello 使用者稱為 「 宣告 」 的相關資訊。

在識別說，「 宣告 」 內 hello 語彙基元所發出該使用者的使用者身分識別提供者指出資訊。 在[SAML 權杖](http://en.wikipedia.org/wiki/SAML_2.0)，此資料通常會包含在 hello SAML 屬性陳述式。 hello 使用者的唯一識別碼通常都會在 hello SAML 主體也稱為名稱識別項。

根據預設，Azure Active Directory 發出 SAML 權杖 tooyour 應用程式，其中包含 NameIdentifier 宣告，以在 Azure AD 中的 hello 使用者的使用者名稱 （也稱為使用者主體名稱） 的值。 這個值可以唯一識別 hello 使用者。 hello SAML 語彙基元也會包含額外的宣告包含 hello 使用者的電子郵件地址、 名字和姓氏。

tooview 或編輯 hello 宣告 hello 發出 SAML 權杖 toohello 應用程式，開啟 hello Azure 入口網站中的應用程式。 然後選取 hello**檢視和編輯所有其他使用者屬性**核取方塊在 hello**使用者屬性**hello 應用程式 > 一節。

![使用者屬性區段][1]

有兩個可能的原因為何，您可能需要在 hello SAML 權杖中發出的 tooedit hello 宣告：
* hello 應用程式已寫入的 toorequire 用不同的宣告的 Uri 設定，或宣告值。
* hello 應用程式已部署需要 hello NameIdentifier 宣告 toobe 以外的項目 hello 使用者名稱 （也稱為使用者主體名稱） 儲存在 Azure Active Directory 中的方式。

您可以編輯任何 hello 預設宣告值。 選取 hello SAML token 屬性資料表中的 hello 宣告資料列。 這會開啟 hello**編輯屬性**區段，然後您可以編輯宣告名稱、 值和命名空間與 hello 宣告相關聯。

![編輯使用者屬性][2]

您也可以移除使用 hello 操作功能表，按一下在 hello 所開啟的 （非 NameIdentifier) 宣告**...**圖示。  您也可以加入新的宣告，使用 hello**加入屬性** 按鈕。

![編輯使用者屬性][3]

## <a name="editing-hello-nameidentifier-claim"></a>編輯 hello NameIdentifier 宣告
toosolve hello 問題已部署 hello 應用程式使用不同的使用者名稱，按一下 hello**使用者識別碼**下拉式清單中 hello**使用者屬性**> 一節。 這個動作會提供包含數個不同選項的對話方塊：

![編輯使用者屬性][4]

在 hello 下拉式清單中，選取  **user.mail** tooset hello NameIdentifier 宣告 toobe hello 使用者的電子郵件地址 hello 目錄中。 或者，選取**user.onpremisessamaccountname** tooset toohello 使用者 SAM 帳戶名稱，從同步處理內部部署 Azure AD。

您也可以使用特殊的 hello **ExtractMailPrefix()**函式 tooremove hello 從 hello 電子郵件地址、 SAM 帳戶名稱或 hello 使用者主體名稱的網域尾碼。 這會擷取僅 hello 第一部分 hello 使用者名稱傳遞出去 (例如，"joe_smith"而不是joe_smith@contoso.com)。

![編輯使用者屬性][5]

我們現在還新增了 hello **join （)**函式 toojoin hello 驗證網域與 hello 使用者識別碼值。 當您選取 hello join （） 函式在 hello**使用者識別碼**第一次選取類似電子郵件地址或使用者主體名稱為 hello 使用者識別碼，然後 hello 第二個下拉式清單中選取 已驗證的網域。 如果您選取 hello 電子郵件地址與 hello 已驗證網域，則 Azure AD 擷取從 hello 第一個值 joe_smith hello username joe_smith@contoso.com ，並將它附加與 contoso.onmicrosoft.com。請參閱下列範例中的 hello:

![編輯使用者屬性][6]

## <a name="adding-claims"></a>新增宣告
當新增宣告，您可以指定 hello 屬性名稱 （不嚴格需要 toofollow 根據 hello SAML 規格的 URI 模式）。 設定 hello 值 tooany 使用者屬性儲存在 hello 目錄中。

![新增使用者屬性][7]

例如，您需要 toosend hello 使用者的 hello 部門所屬 tooin 組織 （例如，Sales) 宣告的形式。 如預期般 hello 應用程式中，輸入 hello 宣告名稱，然後選取**user.department** hello 值。

> [!NOTE]
> 如果沒有針對選取的屬性儲存的值指定使用者，然後該宣告無法發行 hello 權杖中。

> [!TIP]
> hello **user.onpremisesecurityidentifier**和**user.onpremisesamaccountname**時同步處理使用者資料，從內部部署 Active Directory 使用 hello，才支援[AzureAD Connect 工具](../active-directory-aadconnect.md)。

## <a name="restricted-claims"></a>受限制的宣告

SAML 有一些受限制的宣告。 如果您新增這些宣告，則 Azure AD 不會傳送這些宣告。 以下是 hello SAML 限制宣告集：

    | 宣告類型 (URI) |
    | ------------------- |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expiration |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/expired |
    | http://schemas.microsoft.com/identity/claims/accesstoken |
    | http://schemas.microsoft.com/identity/claims/openid2_id |
    | http://schemas.microsoft.com/identity/claims/identityprovider |
    | http://schemas.microsoft.com/identity/claims/objectidentifier |
    | http://schemas.microsoft.com/identity/claims/puid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier[MR1] |
    | http://schemas.microsoft.com/identity/claims/tenantid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod |
    | http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groups |
    | http://schemas.microsoft.com/claims/groups.link |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/role |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/wids |
    | http://schemas.microsoft.com/2014/09/devicecontext/claims/iscompliant |
    | http://schemas.microsoft.com/2014/02/devicecontext/claims/isknown |
    | http://schemas.microsoft.com/2012/01/devicecontext/claims/ismanaged |
    | http://schemas.microsoft.com/2014/03/psso |
    | http://schemas.microsoft.com/claims/authnmethodsreferences |
    | http://schemas.xmlsoap.org/ws/2009/09/identity/claims/actor |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authorizationdecision |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/authentication |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/sid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarygroupsid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlyprimarysid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/denyonlysid |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/denyonlywindowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdeviceclaim |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsdevicegroup |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsfqbnversion |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowssubauthority |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsuserclaim |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/x500distinguishedname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn |
    | http://schemas.microsoft.com/ws/2008/06/identity/claims/ispersistent |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier |
    | http://schemas.microsoft.com/identity/claims/scope |

## <a name="next-steps"></a>後續步驟
* [Article Index for Application Management in Azure Active Directory (Azure Active Directory 中應用程式管理的文件索引)](../active-directory-apps-index.md)
* [設定單一登入 tooapplications 不在 hello Azure Active Directory 應用程式庫](../active-directory-saas-custom-apps.md)
* [SAML 型單一登入疑難排解](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saml-claims-customization/user-attribute-section.png
[2]: ./media/active-directory-saml-claims-customization/edit-claim-name-value.png
[3]: ./media/active-directory-saml-claims-customization/delete-claim.png
[4]: ./media/active-directory-saml-claims-customization/user-identifier.png
[5]: ./media/active-directory-saml-claims-customization/extractemailprefix-function.png
[6]: ./media/active-directory-saml-claims-customization/join-function.png
[7]: ./media/active-directory-saml-claims-customization/add-attribute.png