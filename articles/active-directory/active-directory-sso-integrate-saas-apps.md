---
title: "將 Azure Active Directory 單一登入與 SaaS 應用程式整合 | Microsoft Docs"
description: "在 Azure Active Directory 中啟用 SaaS 應用程式的單一登入驗證和使用者佈建集中式存取管理。 如何將 Azure Active Directory 與 SaaS 應用程式整合的概觀。"
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
ms.openlocfilehash: fc0d297598c334ca8f6f8a2bd3ae948c87956342
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="integrate-azure-active-directory-single-sign-on-with-saas-apps"></a>整合 Azure Active Directory 單一登入與 SaaS 應用程式
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-enterprise-apps-manage-sso.md)
> * [Azure 傳統入口網站](active-directory-sso-integrate-saas-apps.md)
>
>

[!INCLUDE [active-directory-sso-use-case-intro](../../includes/active-directory-sso-use-case-intro.md)]

若要開始為將於組織部署的應用程式設定單一登入，您將使用 Azure Active Directory (Azure AD) 中的現有目錄。 您可以使用從 Microsoft Azure、Office 365 或 Windows Intune 取得的 Azure AD 目錄。 如果您有兩個以上的項目，請參閱 [管理 Azure AD 目錄](active-directory-administer.md) 來判斷要使用哪一個。

> [!IMPORTANT]
> Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。 如需如何在 Azure AD 系統管理中心指派系統管理員角色的相關資訊，請參閱[在 Azure Active Directory 中指派系統管理員角色](active-directory-enterprise-apps-manage-sso.md)。

## <a name="authentication"></a>驗證
對於應用程式支援 SAML 2.0、WS-同盟或 OpenID Connect 通訊協定的應用程式，Azure Active Directory 使用簽章憑證來建立信任關係。 如需詳細資訊，請參閱 [管理同盟單一登入的憑證](active-directory-sso-certs.md)。

對於僅支援 HTML 表單型登入的應用程式，Azure Active Directory 使用「密碼儲存庫存」來建立信任關係。 這可讓您組織中的使用者，使用 SaaS 應用程式的使用者帳戶資訊，由 Azure AD 自動登入 SaaS 應用程式。 Azure AD 會收集並安全地儲存使用者帳戶資訊和相關的密碼。 如需詳細資訊，請參閱 [密碼單一登入](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)。

## <a name="authorization"></a>Authorization
佈建的帳戶可授與通過單一登入驗證的使用者使用應用程式的權限。 使用者佈建可以手動方式完成，或是在某些情況下，您可以依據在 Azure Active Directory 中所做的變更來新增和移除 SaaS 應用程式中的使用者資訊。 如需有關使用現有的 Azure AD 連接器來進行自動化佈建的詳細資訊，請參閱[自動執行 SaaS 應用程式的使用者佈建和取消佈建](active-directory-saas-app-provisioning.md)。

否則，您可以手動將使用者資訊新增至應用程式，或使用市集中可用的其他佈建解決方案。

## <a name="access"></a>Access
Azure AD 提供幾種可自訂的方式，來對您組織中的使用者部署應用程式。 您不會受限於任一特定的部署或存取解決方案。 您可以使用 [最符合您需求的解決方案](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)。

## <a name="additional-considerations-for-applications-already-in-use"></a>已使用中的應用程式的其他考量
為組織已使用的應用程式設定單一登入是與為新應用程式建立新帳戶不同的程序。 有幾個基本步驟包括：將應用程式中的使用者身分識別對應到 Azure AD 身分識別，以及了解整合之後使用者如何體驗登入應用程式。

> [!NOTE]
> 若要為現有的應用程式設定 SSO，您必須在 Azure AD 和 SaaS 應用程式同時具有全域系統管理員權限。
>
>

### <a name="mapping-user-accounts"></a>對應使用者帳戶
使用者的身分識別通常有唯一識別碼，可能是電子郵件地址或使用者主體名稱 (UPN)。 您必須將每個使用者的應用程式身分識別連結 (對應) 至其各自的 Azure AD 身分識別。 根據您的應用程式驗證的需求，有好幾種方法可完成這項作業。

如需有關將應用程式身分識別與 Azure AD 身分識別對應的詳細資訊，請參閱[自訂 SAML 權杖中發出的宣告](http://social.technet.microsoft.com/wiki/contents/articles/31257.azure-active-directory-customizing-claims-issued-in-the-saml-token-for-pre-integrated-apps.aspx)和[自訂佈建的屬性對應](active-directory-saas-customizing-attribute-mappings.md)。

### <a name="understanding-the-users-log-in-experience"></a>了解使用者的登入體驗
當您為已在使用中的應用程式整合 SSO 時，請務必了解使用者經驗將會受到影響。 對於所有應用程式，使用者將會開始使用其 Azure AD 認證來登入。 他們也可能需要使用不同的入口網站來存取應用程式。

有些應用程式的 SSO 可在應用程式的登入介面中執行，但對於其他應用程式，使用者則必須透過中央入口網站 (例如[我的應用程式](http://myapps.microsoft.com)或 [Office365](http://portal.office.com/myapps)) 來登入。 請在 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)中深入了解不同類型的 SSO 與其使用者體驗。

另一個有用的資源是[引導開發人員](active-directory-applications-guiding-developers-for-lob-applications.md)一文中的＜隱藏使用者同意＞。

## <a name="next-steps"></a>後續步驟
對於您在應用程式庫中找到的 SaaS 應用程式，Azure AD 提供一些 [有關如何整合 SaaS 應用程式的教學課程](active-directory-saas-tutorial-list.md)。

如果應用程式不在應用程式庫中，您可以 [將應用程式新增至 Azure AD 應用程式庫做為自訂應用程式](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)。

Azure.com 文件庫中還有更多關於這些議題的詳細資料，請先閱讀[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

另外，請勿錯過 [Azure Active Directory 中應用程式管理的文件索引](active-directory-apps-index.md)。
