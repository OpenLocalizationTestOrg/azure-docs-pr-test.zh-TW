---
title: "aaaSingle 登入的 hello Azure Active Directory 中的企業應用程式管理 |Microsoft 文件"
description: "了解如何 toomanage 單一登入企業應用程式使用 hello Azure Active Directory"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: bcc954d3-ddbe-4ec2-96cc-3df996cbc899
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.openlocfilehash: b0a8e622ab10517b7b69f786406b6e9b9f2e7eaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-single-sign-on-for-enterprise-apps"></a>管理企業應用程式的單一登入
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-enterprise-apps-manage-sso.md)
> * [Azure 傳統入口網站](active-directory-sso-integrate-saas-apps.md)
> 

本文說明如何 toouse hello [Azure 入口網站](https://portal.azure.com)toomanage 單一登入企業應用程式的設定。 企業應用程式是您組織內部署和使用的應用程式。 本文件適用於特別 hello 從已加入的 tooapps [Azure Active Directory 應用程式庫](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)。 

## <a name="finding-your-apps-in-hello-portal"></a>在 [hello 入口網站中尋找您的應用程式
您已設定單一登入的所有企業應用程式可以檢視及管理 hello Azure 入口網站中。 hello 應用程式可以在 hello**更服務** &gt; **企業應用程式**hello 入口網站的區段。 

![企業應用程式刀鋒視窗][1]

選取**所有應用程式**tooview 已設定的所有應用程式清單。 選取應用程式載入 hello 資源刀鋒視窗，該應用程式，其中可以檢視報告，該應用程式，且可管理各種不同的設定。

toomanage 單一登入設定，選取**單一登入**。

![應用程式資源刀鋒視窗][2]

## <a name="single-sign-on-modes"></a>單一登入模式
hello**單一登入**刀鋒視窗開頭**模式**功能表上，可讓 hello 單一登入模式 toobe 設定。 hello 可用的選項包括：

* **SAML 型登入**-這個選項才可以使用 hello 應用程式與 Azure Active Directory 使用 hello SAML 2.0 通訊協定支援完整同盟單一登入。
* **密碼型登入** - 如果 Azure AD 支援此應用程式的密碼表單填入，便可使用此選項。
* **連結登入**-稱為 [現有單一登入 」，此選項可讓系統管理員 tooplace 連結 toothis 應用程式中使用者的 Azure AD 存取面板或 Office 365 應用程式的啟動程式。

如需這些模式的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。

## <a name="saml-based-sign-on"></a>SAML 型登入
hello **SAML 型登入**選項會顯示分成四個區段的刀鋒視窗：

### <a name="domains-and-urls"></a>網域和 URL
這是加入 hello 應用程式網域和 Url 的所有詳細 tooyour Azure AD 目錄。 所有輸入所都需 toomake 單一登入工作的應用程式會顯示直接在 hello 畫面上，而選取 hello 也可以檢視所有選擇性輸入**顯示進階的 URL 設定**核取方塊。 支援輸入 hello 完整清單包括：

* **登入 URL** – 其中 hello 使用者進入 toosign 中 toothis 應用程式。 如果當使用者瀏覽 toothis URL，hello 服務提供者未 hello 必要則 hello 應用程式設定的 tooperform 服務提供者起始單一登入，重新導向 tooAzure AD tooauthenticate 並登入 hello 中的使用者。 如果已填入此欄位，Azure AD 會使用 Office 365 和 Azure AD 存取面板 hello 這個 URL toolaunch hello 應用程式。 如果省略此欄位，則 Azure AD 會改為執行身分識別提供者-初始的登入 hello 應用程式啟動時從 Office 365、 Azure AD 存取面板 hello 或 hello Azure AD 單一登入 URL。
* **識別項**-這個 URI 應專門用於識別 hello 應用程式所設定的單一登入。 這是 Azure AD 會傳送後 tooapplication hello hello SAML 權杖中，對象參數時，和 hello 應用程式是預期的 toovalidate hello 值它。 這個值也會顯示為 hello 應用程式所提供的任何 SAML 中繼資料中的實體識別碼 hello。
* **回覆 URL** -hello 回覆 URL 是 hello 應用程式預期 tooreceive hello SAML 權杖中的位置。 這也是參考的 tooas hello 判斷提示取用者服務 (ACS) URL。 這些輸入之後，畫面上，按 [下一步 tooproceed toohello 下一步]。 此畫面會提供哪些需求 toobe 上設定 hello 應用程式端 tooenable 它 tooaccept 來自 Azure AD SAML 權杖的相關資訊。
* **轉送狀態**-hello 轉送狀態是選擇性參數，可協助分辨 hello 應用程式其中 tooredirect hello 使用者驗證完成後。 Hello 值通常是在 hello 應用程式中，有效的 URL，不過有些應用程式以不同的方式使用此欄位 （在文件，如需詳細資訊，請參閱 hello 應用程式的單一登）。 hello 能力 tooset hello 轉送狀態會是唯一的 toohello 新版 Azure 入口網站的新功能。

### <a name="user-attributes"></a>使用者屬性
這是系統管理員可以檢視和編輯 hello 屬性傳送嗨 SAML 權杖中，Azure AD 會發出 toohello 應用程式每次使用者登入位置。

僅支援可編輯的屬性為 hello hello**使用者識別碼**屬性。 hello 這個屬性的值是唯一識別 hello 應用程式中的每個使用者的 Azure AD 中的 hello 欄位。 例如，如果 hello 應用程式已部署為 hello 使用者名稱和唯一識別碼使用 hello 」 電子郵件地址 」，然後 hello 值會設定 toohello"user.mail"欄位在 Azure AD 中。

### <a name="saml-signing-certificate"></a>SAML 簽署憑證
此區段會顯示 hello hello Azure AD 使用 toosign hello SAML 權杖 toohello 應用程式會驗證每個時間 hello 使用者發出的憑證詳細資料。 它可讓 hello hello 目前憑證 toobe 檢查，包括 hello 到期日屬性。

### <a name="application-configuration"></a>應用程式組態
hello 最後一節提供 hello 文件及/或控制項需要的 tooconfigure hello 應用程式本身 toouse Azure Active Directory 身分識別提供者。

hello**設定應用程式**出現的功能表提供新簡潔的內嵌設定指示 hello 應用程式。 這是另一個新功能唯一 toohello 新版 Azure 入口網站。

> [!NOTE]
> 針對內嵌文件的完整範例，請參閱 hello Salesforce.com 應用程式。 將持續新增其他應用程式的文件。
> 
> 

![內嵌的文件][3]

## <a name="password-based-sign-on"></a>密碼型登入
如果支援 hello 應用程式，則選取 hello 密碼型 SSO 模式，然後選取**儲存**立即將它設定 toodo 密碼登入。 如需部署密碼型 SSO 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。

![密碼型登入][4]

## <a name="linked-sign-on"></a>連結型登入
如果支援 hello 應用程式，則選取連結的 hello SSO 模式可讓您 tooenter hello URL 想 hello Azure AD 存取面板或 Office 365 tooredirect toowhen 使用者按一下此應用程式。 如需連結型 SSO (以前稱為「現有 SSO」) 的詳細資訊，請參閱 [單一登入如何搭配 Azure Active Directory 運作](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)。

![連結型單一登入][5]

##<a name="feedback"></a>意見反應

我們希望您希望使用 hello 改善 Azure AD 的體驗。 請保留來自 hello 意見反應 ！ 將張貼到您的意見反應與改進的想法 hello**管理入口**區段我們[意見反應論壇](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal)。  我們正在興奮每一天，建置新很棒的相關指引 tooshape 和使用什麼接下來要建立的定義。

[1]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade.PNG
[2]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-sso-blade.PNG
[3]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-embedded-docs.PNG
[4]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-password-sso.PNG
[5]: ./media/active-directory-enterprise-apps-manage-sso/enterprise-apps-blade-linked-sso.PNG
