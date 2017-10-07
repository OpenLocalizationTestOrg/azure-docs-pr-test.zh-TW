---
title: "Azure AD：SSPR 註冊 | Microsoft Docs"
description: "註冊 Azure AD 自助式密碼重設的驗證資料"
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: end-user
ms.openlocfilehash: dfcd0106616218c84d23920b124bed5b202cdd6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="register-for-self-service-password-reset"></a>註冊自助式密碼重設

> [!IMPORTANT]
> **您來到此處是因為有登入問題嗎？** 若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md)。

以一般使用者，您可以重設密碼或解除鎖定帳戶而不需要使用自助式密碼重設 (SSPR) toospeak tooa 人員。 您可以使用這項功能之前，您尚未 tooregister 驗證方法，或確認已填入您的系統管理員的 hello 預先定義的驗證方法。

## <a name="register-or-confirm-authentication-data-with-sspr"></a>使用 SSPR 註冊或確認驗證資料

1. 在您的裝置，然後移至 toohello hello 開啟網頁瀏覽器[密碼重設註冊頁面](http://aka.ms/ssprsetup)
2. 輸入您的使用者名稱和您系統管理員所提供的密碼
3. 根據您的 IT 人員如何設定項目、 一個或多個 hello 下列選項可供您 tooconfigure，並確認。 您的系統管理員可能會填入這一點為您他們有權限 toouse hello 資訊。
    * 辦公室電話是只能夠 toobe 管理員所設定
    * 驗證電話應設定 tooanother，您必須存取 toolike 行動電話可以接收簡訊或電話的電話號碼。
    * 驗證電子郵件應該設定 tooan 替代電子郵件地址，您可以存取 hello 密碼的情況下，您需要 tooreset。
    * 安全性問題，可讓您的問題，您的系統管理員已核准您 tooanswer 的清單。 您不可能使用的 hello 相同問題或回答一次以上。
4. 提供並確認您的系統管理員所需的 hello 資訊。 如果使用多個選項，則我們建議您註冊多個方法 tooprovide 彈性，無法使用另一種方法時 (範例： 出差而無法 tooaccess 您的辦公室電話)

    ![註冊驗證方法，並按一下 [完成]][Register]

5. 當完成步驟 4 時選擇**完成**，而且您現在可以 toouse 自助式密碼重設時需要 tooin hello 未來。

如果您輸入 hello 驗證電話或驗證電子郵件中的資料，它是不可見 hello 全域目錄中。 hello 的人才可以看到此資料包括您和您的系統管理員。 只有您可以看到 hello 回答 tooyour 安全性問題。

系統管理員可能需要您 tooconfirm 驗證方法在一段時間 toomake 確定仍有 hello 註冊適當的方法。

## <a name="common-problems-and-their-solutions"></a>常見問題及其解決方案

 以下提供一些常見的錯誤案例及其解決方案：

| 錯誤案例| 您看到什麼錯誤訊息？| 方案 |
| --- | --- | --- |
| 在輸入我的使用者 ID 後，出現了「請連絡您的系統管理員」頁面 | 請連絡您的系統管理員 <br> <br> 我們偵測到您的使用者帳戶密碼未受到 Microsoft 管理。 如此一來，我們目前無法 tooautomatically 重設密碼。 <br> <br> 您需要 toocontact 您的 IT 人員尋求進一步的協助。 | 您會看到此訊息，因為您的 IT 人員管理您的密碼在內部部署環境中並不允許您 tooreset 的密碼，無法存取您帳戶的連結。 <br> <br> tooreset 您的密碼，請連絡您的 IT 人員直接的說明，以及讓他們知道您想 tooreset 您的密碼，因此它們可以讓您啟用此功能。|
| 在輸入我的使用者 ID 後，出現了「您的帳戶未啟用密碼重設」錯誤 | 您的帳戶未啟用密碼重設功能 <br> <br> 很抱歉，IT 人員還沒將您的帳戶設定用於此服務。 <br> <br> 如果您想要的話，我們可以請連絡系統管理員可以在您的組織 tooreset 您的密碼。 | 您會看到此訊息，因為您的 IT 人員尚未啟用密碼重設為從您的組織無法存取您帳戶的連結，或未授權您 toouse hello 功能。 <br> <br> tooreset 您的密碼，按一下連絡人管理員連結 toosend 電子郵件 tooyour 公司的 IT 人員，並且讓他們知道您將 tooreset 希望您的密碼，因此，它們可以讓您啟用此功能。 |
| 在輸入我的使用者 ID 後，出現了「我們無法驗證您的帳戶」錯誤 | 我們無法驗證您的帳戶 <br> <br> 如果您想要的話，我們可以請連絡系統管理員可以在您的組織 tooreset 您的密碼。 | 您會看到此訊息，因為您已啟用密碼重設，但您沒有註冊 toouse hello 服務。 tooregister 密碼重設，您已重新取得存取 tooyour 帳戶之後，請移 toohttp://aka.ms/ssprsetup。 <br> <br> tooreset 您的密碼，按一下連絡人管理員連結 toosend 電子郵件 tooyour 公司的 IT 人員。 |

## <a name="next-steps"></a>後續步驟

* [如何 toochange 您使用自助式密碼重設密碼](active-directory-passwords-update-your-own-password.md)
* [密碼重設註冊頁面](http://aka.ms/ssprsetup)
* [密碼重設入口網站](https://passwordreset.microsoftonline.com/)
* [無法登入 tooyour Microsoft 帳戶](https://support.microsoft.com/help/12429/microsoft-account-sign-in-cant)

[Register]: ./media/active-directory-passwords-reset-register/register-2-methods.png "顯示已註冊方法及完成按鈕的密碼重設註冊頁面"

