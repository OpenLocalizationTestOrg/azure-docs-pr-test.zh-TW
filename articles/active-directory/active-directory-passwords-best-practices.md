---
title: "推出︰Azure AD SSPR | Microsoft Docs"
description: "成功推出 Azure AD 自助式密碼重設的祕訣"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: f8cd7e68-2c8e-4f30-b326-b22b16de9787
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 73d31679b38ff009a767335adaebc49fbc5a75b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="roll-out-password-reset-for-users"></a>為使用者推出密碼重設

大部分的客戶步驟 hello 遵循 tooensure SSPR 功能 smooth 首度發行。

1. [在您的目錄中啟用密碼重設](active-directory-passwords-getting-started.md)
2. [設定密碼回寫的內部部署 AD 權限](active-directory-passwords-how-it-works.md#active-directory-permissions)
3. [設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)toowrite 從 Azure AD 的密碼回 tooyour 在內部部署目錄
4. [指派和驗證所需的授權](active-directory-passwords-licensing.md)
5. 如果您想 tooroll 出逐漸增加，您可以選擇性地限制密碼重設使用者 tooroll 出 hello 功能 tooa 群組緩時變經過一段時間。 這設定 hello toodo**自助密碼重設啟用服務**切換從**可否**太**群組**並選取 密碼重設安全性群組 tooenable。 hello 這個群組的成員都必須擁有指派的授權 toothem 和是很好的方法 tooenable[授權群組](active-directory-passwords-licensing.md#enable-group-or-user-based-licensing)。
6. 填入 hello 最小一組[驗證資料](active-directory-passwords-data.md)，根據您的原則。
7. 告訴使用者如何傳送指示 tooshow toouse SSPR，它們如何 tooregister 以及 tooreset。
    > [!NOTE]
    > 以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。 如需有關 hello 系統管理員密碼原則的詳細資訊，請參閱我們[深入探討文章](active-directory-passwords-how-it-works.md)。

8. 您可以選擇在任何時間點，tooenforce 註冊，並要求使用者 tooreconfirm 一段時間之後其驗證資訊。 如果您不想您使用者 toohave tooregister，您可以[部署密碼重設而不需要使用者註冊](active-directory-passwords-data.md)。
9. 經過一段時間，檢閱 使用者註冊並使用藉由檢視 hello[報告 Azure AD 所提供](active-directory-passwords-reporting.md)。

## <a name="email-based-rollout"></a>以電子郵件為基礎的啟用

許多客戶發現電子郵件宣傳活動中的，簡單 toouse 指示是 hello 最簡單方式 tooget 使用者 toouse SSPR。 [我們已經建立三個簡單的電子郵件，您可以使用為範本 toohelp 中首度發行。](https://onedrive.live.com/?authkey=%21AD5ZP%2D8RyJ2Cc6M&id=A0B59A91C740AB16%2125063&cid=A0B59A91C740AB16)

* **即將登場**電子郵件範本 toobe hello 週數或天數首度發行 toolet 使用者知道他們需要 toodo 項目中使用。
* **現在可用**電子郵件範本使用 toobe hello 啟動 toodrive 使用者 tooregister 天數，並確認其驗證資料，在需要時，他們即可使用 SSPR。
* **登入，以提醒**之後部署 tooremind 使用者 tooregister 電子郵件的幾天 tooweeks 的範本，並確認其驗證資料。

## <a name="creating-your-own-password-portal"></a>建立您自己的密碼入口網站

許多較大客戶選擇 toohost 網頁，並建立 DNS 項目，例如 https://passwords.contoso.com 的根目錄。它們會填入此頁面的連結 toohello Azure AD 密碼重設，密碼重設註冊、 密碼變更入口網站及其他組織特定資訊。 在任何電子郵件通訊或廣告傳單做出，您送出，您可以再包含品牌文數，使用者可以前往 toowhen 它們需要 toouse hello 服務的 URL。

* 密碼重設入口網站 - https://passwordreset.microsoftonline.com/
* 密碼重設註冊入口網站 - http://aka.ms/ssprsetup
* 密碼變更入口網站 - https://account.activedirectory.windowsazure.com/ChangePassword.aspx

## <a name="using-enforced-registration"></a>使用強制註冊

如果您想要使用者 tooregister 密碼重設，您可以強制它們 tooregister 登入使用 Azure AD 時。 您可以啟用此選項，從您的目錄**密碼重設**刀鋒視窗，藉由啟用 hello**需要使用者在登入時的 tooRegister**選項 hello**註冊**索引標籤。

系統管理員可以在一段時間之後使用者 toore 註冊要求設定 hello**數天之後使用者, 詢問 tooreconfirm 其驗證資訊**介於 0-730 天。

啟用此選項之後，簽署的使用者會看到訊息，通知他們管理員要求它們 tooverify 其驗證資訊。

## <a name="populate-authentication-data"></a>填入驗證資料

如果您[設為您的使用者的驗證資料](active-directory-passwords-data.md)，則使用者不需要密碼重設，就能 toouse SSPR tooregister。 只要使用者擁有 hello 驗證定義的資料符合您定義 hello 密碼重設原則，使用者會無法 tooreset 他們的密碼。

## <a name="disabling-self-service-password-reset"></a>停用自助式密碼重設

停用自助式密碼重設的很簡單，開啟 Azure AD 租用戶，並將太**密碼重設**，**屬性**，然後選擇**沒有人**下**自助密碼重設啟用**

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**密碼回寫**](active-directory-passwords-writeback.md) - 密碼回寫如何使用您的內部部署目錄
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR
