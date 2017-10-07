---
title: "快速入門︰Azure AD SSPR | Microsoft Docs"
description: "快速部署 Azure AD 自助式密碼重設"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>快速入門︰Azure AD 自助式密碼重設

> [!IMPORTANT]
> **您來到此處是因為有登入問題嗎？** 若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。

## <a name="rapidly-deploy-self-service-password-reset"></a>快速部署自助式密碼重設

自助式密碼重設 (SSPR) 提供簡單的方法，用於 IT 系統管理員 tooempower 使用者 tooreset 或其密碼或帳戶解除鎖定。 hello 系統包含詳細的報告 tootrack 當使用者使用 hello 系統，以及通知 tooalert 您 toomisuse 或濫用。

本指南假設您已經有有效的試用或經過授權的 Azure AD 租用戶。 如果您需要設定 Azure AD 的說明，請參閱 hello 文章[開始使用 Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/)。

1. 從現有的 Azure AD 租用戶，選取 [密碼重設]

2. 從 hello **「 屬性 」**畫面中的，「 自助密碼重設啟用服務 」 選擇 hello 下列其中一種 hello 選項底下
    * 沒有人-沒有一個是可以 toouse SSPR 功能
    * 您選擇的群組-只有特定的 Azure AD 的成員群組都可以 toouse SSPR 功能
    * 每個人的帳戶在 Azure AD 租用戶中使用的所有使用者都能 toouse SSPR 功能

3. 從 hello **「 驗證方法 」**選擇畫面
    * 所需的方法數目 tooreset-我們支援至少有一個或兩個最大值
    * 方法可用 toousers-我們至少需要一個，但永遠不會損及 toohave 可用的額外選項
        * **電子郵件**會傳送一封電子郵件與程式碼 toohello 使用者所設定的驗證電子郵件地址
        * **行動電話**提供 hello 使用者 hello 選擇 tooreceive 呼叫或使用程式碼 tootheir 文字設定行動電話號碼
        * **辦公室電話**呼叫 hello 使用者與程式碼 tootheir 設定辦公室電話號碼
        * **安全性問題**toochoose 會要求您
            * 所需的問題數目 tooregister-hello 最小值為登錄成功，這表示使用者可以選擇 tooanswer 集區的質疑 toopull 從多個 toocreate。 此選項可設定為 3-5，且必須大於或等於 toohello 問題需要 tooreset 數目。
                * 依序按一下 hello 「 自訂 」 按鈕，僅選擇安全性問題時可以加入自訂的問題
            * 所需的問題 tooreset-可設定為 3-5 問題 toobe 允許解除鎖定或重設使用者密碼 toobe 之前正確解答。

4. 建議使用： **「 自訂 」** toochange hello 「 連絡您的系統管理員 」 連結 toopoint tooa 頁面或電子郵件地址您定義可讓您

5. 選擇性： hello **「 註冊 」**畫面會提供系統管理員的 hello 選項：
    * 在登入時，要求使用者 tooregister
    * 數天之後使用者, 詢問 tooreconfirm 其驗證資訊

6. 選擇性： hello **「 通知 」**畫面會提供系統管理員 hello 選項：
    * 通知使用者密碼重設
    * 當其他系統管理員重設其密碼時通知所有系統管理員

**此時，您已為 Azure AD 租用戶設定 SSPR**。 您可以在此停止或繼續的 tooconfigure 密碼 tooan 的同步處理內部部署 AD 網域。

> [!NOTE]
> 以使用者並非系統管理員測試 SSPR，因為 Microsoft 會強制執行 Azure 系統管理員類型帳戶的強式驗證需求。 如需有關 hello 系統管理員密碼原則的詳細資訊，請參閱我們[密碼原則文章](active-directory-passwords-policy.md#administrator-password-policy-differences)。

## <a name="configure-synchronization-tooexisting-identity-source"></a>設定同步處理 tooexisting 識別來源

tooenable 內部部署身分識別同步處理 tooAzure AD，您需要 tooinstall，以及設定[Azure AD Connect](./connect/active-directory-aadconnect.md)貴組織中的伺服器上。 這個應用程式會同步處理使用者和群組的現有識別來源 tooyour Azure AD 租用戶。

* [從 DirSync 或 Azure AD Sync tooAzure 升級 AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [使用快速設定開始使用 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)
* [設定密碼回寫](active-directory-passwords-writeback.md#configuring-password-writeback)toowrite 從 Azure AD 的密碼回 tooyour 在內部部署目錄。

## <a name="disabling-self-service-password-reset"></a>停用自助式密碼重設

停用自助式密碼重設的很簡單，開啟 Azure AD 租用戶，並將太**密碼重設 > 屬性**> 選擇**無**下**自助密碼重設已啟用**

### <a name="learn-more"></a>詳細資訊
hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 tooconfigure 自助式密碼重設為您的使用者。 toocontinue toohello 遵循這些步驟的 Azure 入口網站 toocomplete hello toohello 入口網站下方的連結。

> [!div class="nextstepaction"]
> [啟用自助密碼重設](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

