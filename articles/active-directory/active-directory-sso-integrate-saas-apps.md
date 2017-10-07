---
title: "Azure Active Directory 單一登入具有 SaaS 應用程式的 aaaIntegrate |Microsoft 文件"
description: "在 Azure Active Directory 中啟用 SaaS 應用程式的單一登入驗證和使用者佈建集中式存取管理。 概觀 toointegrate Azure Active Directory tooSaaS 應用程式。"
services: active-directory
keywords: "將 Azure AD 與 SaaS 應用程式整合在一起"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 53b9d341-d1fc-4bbb-ac7c-3f4c68fcf00a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: aaronsm
ms.openlocfilehash: fe621a30429c81c32470635d105ae3e95184efa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>整合 Azure Active Directory 單一登入與 SaaS 應用程式
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-enterprise-apps-manage-sso.md)
> * [Azure 傳統入口網站](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

tooget 啟動 設定單一登入帶入您的組織的應用程式，您將使用現有的目錄中 Azure Active Directory (Azure AD)。 您可以使用從 Microsoft Azure、Office 365 或 Windows Intune 取得的 Azure AD 目錄。 如果您有兩個或多個，請參閱[管理您的 Azure AD 目錄](active-directory-administer.md)toodetermine 哪一個 toouse。

> [!IMPORTANT]
> Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。 如何置 tooassign hello Azure AD 系統管理員中的系統管理員角色，請參閱[指派 Azure Active Directory 中的系統管理員角色](active-directory-enterprise-apps-manage-sso.md)。

## <a name="authentication"></a>驗證
應用程式支援 hello SAML 2.0 WS-同盟或 OpenID Connect 的通訊協定，Azure Active Directory 使用簽署憑證 tooestablish 信任關係。 如需詳細資訊，請參閱 [管理同盟單一登入的憑證](active-directory-sso-certs.md)。

對於支援僅 HTML 表單型登入的應用程式，Azure Active Directory 使用 '密碼儲存庫存' tooestablish 信任關係。 這可讓 hello 中的使用者組織 toobe 自動登入 tooa hello SaaS 應用程式中的 hello 使用者帳戶資訊，使用 Azure AD SaaS 應用程式。 Azure AD 會收集並安全地儲存 hello 使用者帳戶資訊和 hello 相關的密碼。 如需詳細資訊，請參閱 [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。

## <a name="authorization"></a>Authorization
佈建的帳戶它們透過單一登入已驗證之後，可讓使用者獲得授權的 toobe toouse 應用程式。 使用者佈建即可手動方式或在某些情況下，您可以新增和移除 Azure Active Directory 中所做的變更所根據的 hello SaaS 應用程式的使用者資訊。 如需有關使用現有的 Azure AD 連接器來進行自動化佈建的詳細資訊，請參閱[自動執行 SaaS 應用程式的使用者佈建和取消佈建](active-directory-saas-app-provisioning.md)。

否則，您可以手動新增使用者資訊 tooan 應用程式，或使用其他佈建的解決方案，可在 hello marketplace 中。

## <a name="access"></a>Access
Azure AD 提供數個可自訂的方式 toodeploy 您組織中的應用程式 tooend 使用者。 您不會受限於任一特定的部署或存取解決方案。 您可以使用[hello 最適合您需求的解決方案](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。

## <a name="additional-considerations-for-applications-already-in-use"></a>已使用中的應用程式的其他考量
設定單一登入您的組織已使用的應用程式是從建立新應用程式的新帳戶的 hello 程序在不同處理序。 有幾個基本步驟包括： 對應中 hello 應用程式 tooAzure AD 身分識別的使用者識別，以及了解使用者如何體驗之後整合 tooan 應用程式中的記錄。

> [!NOTE]
> tooset 上現有的應用程式的 SSO，這兩個 Azure AD 中需要 toohave 全域系統管理員權限和 hello SaaS 應用程式。
>
>

### <a name="mapping-user-accounts"></a>對應使用者帳戶
使用者的身分識別通常有唯一識別碼，可能是電子郵件地址或使用者主體名稱 (UPN)。 您將需要 toolink (map) 每個使用者的應用程式識別 tootheir 各自的 Azure AD 身分識別。 有幾個方式 tooaccomplish 這如何根據 hello 需求的應用程式驗證。

如需對應應用程式識別與 Azure AD 識別身分的詳細資訊，請參閱[自訂 hello SAML 權杖中發出的宣告](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx)和[自訂屬性對應的佈建](active-directory-saas-customizing-attribute-mappings.md)。

### <a name="understanding-hello-users-log-in-experience"></a>了解 hello 使用者的登入體驗
當您將 SSO 整合的應用程式已在使用時，務必 toorealize hello 使用者體驗，將會受到影響。 所有應用程式，使用者將使用在其 Azure AD 認證 toosign 來開始。 它也可能是它們必須使用不同的入口網站 tooaccess hello 應用程式。

SSO 對於某些應用程式可以對 hello 應用程式的登入介面，但其他應用程式，hello 使用者會有 toogo 透過中央入口網站例如 ([我的應用程式](http://myapps.microsoft.com)或[Office365](http://portal.office.com/myapps)) toosign 中的。 深入了解 hello 不同類型的 SSO 和使用者經驗[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。

另一個重要的資源是*隱藏使用者同意*在 hello [Guiding 開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)發行項。

## <a name="next-steps"></a>後續步驟
針對您在 hello 應用程式庫中找到的 SaaS 應用程式，Azure AD 提供數個[教學課程有關 toointegrate SaaS 應用程式](active-directory-saas-tutorial-list.md)。

如果應用程式不會在應用程式庫中，您可以[將它做為自訂應用程式加入 Azure AD App 資源庫 toohello](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。

沒有更多詳細資料，從這些問題 hello Azure.com 文件庫中的所有[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。

此外，不會錯過 hello [Azure Active Directory 中的應用程式管理的文件索引](active-directory-apps-index.md)。
