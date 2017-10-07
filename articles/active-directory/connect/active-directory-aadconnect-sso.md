---
title: "Azure AD Connect：無縫單一登入 | Microsoft Docs"
description: "本主題說明 Azure Active Directory (Azure AD) 無接縫單一登入，並且如何允許您 tooprovide true 單一登入您公司網路內部的企業桌面使用者。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Azure Active Directory 無縫單一登入

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>何謂 Azure Active Directory 無縫單一登入？

Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO) 自動簽署時其公司的裝置連線的 tooyour 公司網路上的使用者。 啟用時，使用者就不需要在 tooAzure AD 中, 其密碼 toosign tootype，並通常，即使輸入其使用者名稱。 這項功能提供您的使用者方便存取 tooyour 雲端型應用程式而不需要任何額外的內部部署元件。

無縫式 SSO 可以結合其中一個 hello[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法。

![無縫單一登入](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>無縫 SSO 目前為預覽狀態。 這項功能_不_適用 tooActive Directory Federation Services (ADFS)。

## <a name="key-benefits"></a>主要權益

- 良好的使用者體驗
  - 使用者會自動登入內部部署和雲端式應用程式。
  - 使用者沒有 tooenter 密碼重複。
- *輕鬆 toodeploy （& s) 管理*
  - 沒有其他元件所需內部 toomake 這項工作。
  - 與任何雲端驗證方法搭配運作：[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)。
  - 可以推出 toosome 或您使用群組原則的所有使用者。
  - 非 Windows 10 裝置註冊而 hello 需要在任何 AD FS 基礎結構的 Azure AD。 這項功能需要您 toouse 版本 2.1 或更新版本的 hello[工作地方聯結用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。

## <a name="feature-highlights"></a>功能要點

- 登入使用者名稱可以是任一個 hello 內部預設使用者名稱 (`userPrincipalName`) 或在 Azure AD Connect 中設定的另一個屬性 (`Alternate ID`)。 同時使用的情況下工作，因為無縫式 SSO 使用 hello `securityIdentifier` hello Kerberos 票證 toolook hello 對應使用者物件在 Azure AD 中的宣告。
- 無縫 SSO 是一種靈活變換的功能。 如果因為任何原因失敗，hello 使用者登入經驗會回到 tooits 一般行為-也就是，hello 使用者需要 tooenter hello 登入頁面上的密碼。
- 如果應用程式會將轉送`domain_hint`(OpenID Connect) 或`whr`(SAML) 參數-識別您的租用戶或`login_hint`參數-識別 hello 使用者在其 Azure AD 登入要求中，使用者會自動登入未加上輸入使用者名稱或密碼。
- 您可以透過 Azure AD Connect 啟用它。
- 這是可用的功能，而且不需要任何付費的版本的 Azure AD toouse 它。
- 它是在能夠使用 Kerberos 驗證的平台和瀏覽器上，支援[新式驗證](https://aka.ms/modernauthga)的網頁瀏覽器型用戶端和 Office 用戶端來支援：

| 作業系統\瀏覽器 |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|是|否|是|是\*|N/A
|Windows 8.1|是|N/A|是|是\*|N/A
|Windows 8|是|N/A|是|是\*|N/A
|Windows 7|是|N/A|是|是\*|N/A
|Mac OS X|N/A|N/A|是\*|是\*|是\*

\*需要[其他設定](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。

>[!NOTE]
>Windows 10 hello 建議的做法是 toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) hello 最佳單一登入體驗與 Azure AD。

## <a name="next-steps"></a>後續步驟

- [**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。
- [**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。
- [**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
