---
title: "常見問題集 (FAQ) - Azure AD B2C | Microsoft Docs"
description: "關於 Azure Active Directory B2C 的常見問題集"
services: active-directory-b2c
documentationcenter: 
author: saeeda
manager: krassk
editor: bryanla
ms.assetid: ed33c2ca-76d0-442a-abb1-8b7b7bb92d6a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeeda
ms.openlocfilehash: f7857299bc3cb9d5fbe58e047818ec56741e0740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-frequently-asked-questions-faq"></a>Azure AD B2C：常見問題集 (FAQ) 
此頁面會回答有關 hello Azure Active Directory (Azure AD) B2C 常見問題。 請隨時回來查看最新消息。

### <a name="can-i-use-azure-ad-b2c-features-in-my-existing-employee-based-azure-ad-tenant"></a>我可以在以員工為主的現有 Azure AD 租用戶中使用 Azure AD B2C 功能嗎？
Azure AD 和 Azure AD B2C 為個別產品的供應項目，並不能共存在 hello 相同租用戶。  一個 Azure AD 租用戶代表一個組織。  Azure AD B2C 租用戶代表與信賴憑證者的合作對象應用程式搭配使用的身分識別 toobe 的集合。  （在公開預覽狀態） 的自訂原則，Azure AD B2C 可以同盟組織中員工的 tooAzure AD 允許的驗證。

### <a name="can-i-use-azure-ad-b2c-tooprovide-social-login-facebook-and-google-into-office-365"></a>可以使用 Azure AD B2C tooprovide 社交登入 （Facebook 和 Google +） 到 Office 365 嗎？
Azure AD B2C 不能使用的 tooauthenticate for Microsoft Office 365 的使用者。  Azure AD 是 Microsoft 的解決方案來管理員工存取 tooSaaS 應用程式，它有針對此用途，例如授權和條件式存取所設計的功能。  Azure AD B2C 提供身分識別和存取管理平台來建置 web 和行動應用程式。  Azure AD B2C 時設定的 toofederate tooan Azure AD 租用戶，hello Azure AD 租用戶管理員工存取 tooapplications 依賴 Azure AD B2C。

### <a name="what-are-local-accounts-in-azure-ad-b2c-how-are-they-different-from-work-or-school-accounts-in-azure-ad"></a>Azure AD B2C 中的本機帳戶是什麼？ 與 Azure AD 中的工作或學校帳戶有何不同？
在 Azure AD 租用戶隸屬 toohello 租用戶的使用者登入 hello 表單的電子郵件地址`<xyz>@<tenant domain>`。  hello `<tenant domain>` hello 的其中一個驗證 hello 中的網域的租用戶或 hello 初始`<...>.onmicrosoft.com`網域。 這種類型的帳戶就是工作或學校帳戶。

在 Azure AD B2C 租用戶中大部分的應用程式想要讓 hello 使用者 toosign 中任何的任意的電子郵件地址 (例如， joe@comcast.net， bob@gmail.com， sarah@contoso.com，或jim@live.com)。 這種類型的帳戶就是本機帳戶。  我們也支援使用任意的使用者名稱作為本機帳戶 (例如，joe、bob、sarah 或 jim)。 您可以選擇下列其中一種這些本機帳戶設定 Azure AD B2C hello Azure 入口網站中。

### <a name="which-social-identity-providers-do-you-support-now-which-ones-do-you-plan-toosupport-in-hello-future"></a>你們現在支援哪些社交身分識別提供者？ 哪些執行您計劃在未來的 hello toosupport？
我們目前支援 Facebook、Google+、LinkedIn、Amazon、Twitter (預覽)、WeChat (預覽)、Weibo (預覽) 和 QQ (預覽)。 根據客戶需求，我們將會增加支援其他熱門的社交身分識別提供者。

Azure AD B2C 也新增了[自訂原則](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom)的支援。  這些[自訂原則](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview-custom)自己原則的任何身分識別提供者支援可讓開發人員 toocreate [OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)或 SAML。 

查看我們的[自訂原則入門套件](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack)，開始使用自訂原則。

### <a name="can-i-configure-scopes-toogather-more-information-about-consumers-from-various-social-identity-providers"></a>設定範圍 toogather 各種社交身分識別提供者從取用者的詳細資訊？
否，但這項功能已在我們的規劃中。 使用我們支援的社交身分識別提供者集合的 hello 預設範圍如下：

* Facebook: email
* Google+: email
* Microsoft 帳戶︰openid 電子郵件設定檔
* Amazon: profile
* LinkedIn: r_emailaddress, r_basicprofile

### <a name="does-my-application-have-toobe-run-on-azure-for-it-work-with-azure-ad-b2c"></a>我的應用程式有 toobe 在 Azure 上執行，使用 Azure AD B2C 嗎？
否，您可以主控您的應用程式中任何位置 （hello 雲端或內部部署）。 它只需要與 Azure AD B2C toointeract 是 hello 能力 toosend 和接收 HTTP 要求的可公開存取的端點上。

### <a name="i-have-multiple-azure-ad-b2c-tenants-how-can-i-manage-them-on-hello-azure-portal"></a>我有多個 Azure AD B2C 租用戶。 如何管理它們在 hello Azure 入口網站？
在開啟之前 ' Azure AD B2C' hello 左側功能表中的 hello Azure 入口網站，您必須切換到 hello 目錄中，您想 toomanage。  按一下您的身分識別中 hello 右上角 hello Azure 入口網站，切換目錄，然後選擇 在 hello 下拉式清單，目錄會出現。  如逐步與映像，請參閱[瀏覽 tooAzure AD B2C 設定](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)。

### <a name="how-do-i-customize-verification-emails-hello-content-and-hello-from-field-sent-by-azure-ad-b2c"></a>如何自訂驗證電子郵件 (hello 內容 」 和 「 hello 」 從: 」 欄位) 由 Azure AD B2C 傳送？
您可以使用 hello[公司品牌功能](../active-directory/active-directory-add-company-branding.md)toocustomize hello 內容的驗證電子郵件。 具體來說，您可以自訂 hello 電子郵件的兩個元素：

* **橫幅標誌**： 顯示 hello 右下方。
* **背景色彩**: hello 上方所示。

    ![自訂驗證電子郵件的螢幕擷取畫面](./media/active-directory-b2c-faqs/company-branded-verification-email.png)

hello 電子郵件簽章會包含您提供當您第一次建立 hello B2C 租用戶的 hello B2C 租用戶的名稱。 您可以變更 hello 名稱使用下列指示：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)為 hello 訂用帳戶管理員。
1. 瀏覽 tooyour B2C 租用戶。
1. 按一下 hello**設定** 索引標籤。
1. 變更 hello**名稱**欄位底下 hello**目錄屬性**> 一節。
1. 按一下**儲存**hello hello 頁底端。

目前沒有任何方式 toochange hello 」 從:"hello 電子郵件欄位。 票選[feedback.azure.com](https://feedback.azure.com/forums/169401-azure-active-directory/suggestions/15334335-fully-customizable-verification-emails)您感興趣自訂 hello 主體 hello 驗證電子郵件。

### <a name="how-can-i-migrate-my-existing-user-names-passwords-and-profiles-from-my-database-tooazure-ad-b2c"></a>如何從我的資料庫 tooAzure AD B2C 移轉我現有的使用者名稱、 密碼和設定檔？
您可以使用 hello Azure AD Graph API toowrite 移轉工具。 請參閱 hello [Graph API 範例](active-directory-b2c-devquickstarts-graph-dotnet.md)如需詳細資訊。

### <a name="what-password-policy-is-used-for-local-accounts-in-azure-ad-b2c"></a>Azure AD B2C 中用於本機帳戶的密碼原則為何？
hello Azure AD B2C 本機帳戶的密碼原則根據 Azure AD hello 原則。 Azure AD B2C 的註冊，註冊或登入和密碼重設原則使用 hello 「 強式 」 密碼強度，並不會過期的任何密碼。 讀取 hello [Azure AD 密碼原則](https://msdn.microsoft.com/library/azure/jj943764.aspx)如需詳細資訊。

### <a name="can-i-use-azure-ad-connect-toomigrate-consumer-identities-that-are-stored-on-my-on-premises-active-directory-tooazure-ad-b2c"></a>可以使用 Azure AD Connect toomigrate 消費者身分識別儲存在我的內部部署 Active Directory tooAzure AD B2C 上嗎？
否，Azure AD Connect 不是設計與 Azure AD B2C toowork。 請考慮使用 hello [Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md)使用者移轉。

### <a name="can-my-app-open-up-azure-ad-b2c-pages-within-an-iframe"></a>我的應用程式是否能在 iFrame 內開啟 Azure AD B2C 頁面？
否，基於安全性考量，無法在 iFrame 內開啟 Azure AD B2C 頁面。  我們的服務會與 hello 瀏覽器 tooprohibit Iframe 通訊。  一般情況下 hello 安全性社群 hello OAUTH2 規格，建議您不要使用 Iframe toohello 風險按一下 jacking 因為身分識別的使用體驗。

### <a name="does-azure-ad-b2c-work-with-crm-systems-such-as-microsoft-dynamics"></a>Azure AD B2C 可以搭配 Microsoft Dynamics 之類的 CRM 系統一起使用嗎？
與 Microsoft Dynamics 365 入口網站的整合已可供使用。  請參閱[設定 Dynamics 365 入口網站 toouse 驗證 Azure AD B2C](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/portals/azure-ad-b2c)。

### <a name="does-azure-ad-b2c-work-with-sharepoint-on-premises-2016-or-earlier"></a>Azure AD B2C 可以搭配 SharePoint 內部部署的 2016 或更舊版本一起使用嗎？
Azure AD B2C 不適用於 hello SharePoint 外部夥伴共用的案例。請參閱[Azure AD B2B](http://blogs.technet.com/b/ad/archive/2015/09/15/learn-all-about-the-azure-ad-b2b-collaboration-preview.aspx)改為。

### <a name="should-i-use-azure-ad-b2c-or-b2b-toomanage-external-identities"></a>應該使用 Azure AD B2C 或 B2B toomanage 外部識別？
閱讀這篇文章[外部識別](../active-directory/active-directory-b2b-compare-external-identities.md)toolearn 更多有關套用 hello 適當功能 tooyour 外部識別案例。

### <a name="what-reporting-and-auditing-features-does-azure-ad-b2c-provide-are-they-hello-same-as-in-azure-ad-premium"></a>Azure AD B2C 提供哪些報告和稽核功能？ 會在 Azure AD Premium 與 hello 相同嗎？
否，Azure AD B2C 不支援相同的報表設定為 Azure AD Premium 的 hello。 不過有許多共同點：

* hello 登入報表提供每個登入以降低的詳細資訊的記錄。
* Hello Azure 入口網站的 Azure Active Directory 中的稽核報告可用 > 活動稽核記錄檔 > 選擇 B2C 及套用篩選所需。 管理活動以及應用程式活動都包括在內。 
* 您可以在[使用報告 API](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-usage-reporting-api)中取得使用報告，裡面記載了使用者人數、登入次數及 MFA 數量

### <a name="can-i-localize-hello-ui-of-pages-served-by-azure-ad-b2c-what-languages-are-supported"></a>可以當地語系化 hello UI 頁面由 Azure AD B2C 嗎？ 支援哪些語言？
可以！  請參閱[語言自訂](active-directory-b2c-reference-language-customization.md) (處於公開預覽狀態)。  我們提供翻譯 36 種語言，並可以覆寫任何字串 toosuit 您的需求。

### <a name="can-i-use-my-own-urls-on-my-sign-up-and-sign-in-pages-that-are-served-by-azure-ad-b2c-for-instance-can-i-change-hello-url-from-loginmicrosoftonlinecom-toologincontosocom"></a>我可以在 Azure AD B2C 提供的註冊與登入頁面上使用自己的 URL 嗎？ 例如，可以變更 hello URL 從 login.microsoftonline.com toologin.contoso.com 嗎？
目前不支援。 但這項功能已在我們的規劃中。 正在驗證您的網域中 hello**網域**hello Azure 傳統入口網站上的索引標籤不達成此目標。

### <a name="how-do-i-delete-my-azure-ad-b2c-tenant"></a>如何刪除 Azure AD B2C 租用戶？
請遵循這些步驟 toodelete 您的 Azure AD B2C 租用戶：

1. 請遵循下列步驟太[瀏覽 tooAzure AD B2C 設定](active-directory-b2c-app-registration.md#navigate-to-b2c-settings)hello Azure 入口網站上。
1. 瀏覽 toohello**應用程式**，**身分識別提供者**，和**所有原則**並刪除所有的 hello 中每個項目。
1. 立即登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)為 hello 訂用帳戶管理員。 （使用的 hello 相同工作或學校帳戶或 hello 註冊 Azure toosign 有使用相同的 Microsoft 帳戶）。
1. 瀏覽 toohello hello 左邊的 Active Directory 延伸模組，然後按一下您 B2C 租用戶。
1. 按一下 hello**使用者** 索引標籤。
1. 選取每個使用者在開啟 （排除 hello 訂用帳戶管理員使用者您目前登入為）。 按一下**刪除**底端 hello hello 頁面按一下**是**出現提示時。
1. 按一下 hello**應用程式** 索引標籤。
1. 選取**我公司所擁有的應用程式**在 hello**顯示**下拉式清單欄位，然後按一下 hello 核取記號。
1. 名稱為 **b2c-extensions-app** 的應用程式。 按一下**刪除**底端 hello hello 頁面按一下**是**出現提示時。
1. 再次瀏覽 toohello Active Directory 延伸模組，然後選取您 B2C 租用戶。
1. 按一下**刪除**hello hello 頁底端。 toocomplete hello 程序，遵循 hello 囉 」 畫面上的指示。

### <a name="can-i-get-azure-ad-b2c-as-part-of-enterprise-mobility-suite"></a>我可以從 Enterprise Mobility Suite 中取得 Azure AD B2C 嗎？
否，Azure AD B2C 是隨用隨付的 Azure 服務，並不是 Enterprise Mobility Suite 的一部分。

### <a name="how-do-i-report-issues-with-azure-ad-b2c"></a>如何報告有關 Azure AD B2C 的問題？
請參閱 [提出 Azure Active Directory B2C 的支援要求](active-directory-b2c-support.md)。
