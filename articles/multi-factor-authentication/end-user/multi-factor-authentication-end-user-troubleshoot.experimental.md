---
title: "aaaTroubleshoot 雙步驟驗證 |Microsoft 文件"
description: "本文件將提供使用者資訊哪些 toodo 如果作業持續到 Azure Multi-factor Authentication Server 的問題。"
services: multi-factor-authentication
keywords: "多重要素驗證用戶端, 驗證的問題, 相互關聯識別碼"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: end-user
ms.openlocfilehash: 65c25fb70bebeb5eff15ffe63ce11a65f5cdb1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-help-with-two-step-verification"></a>取得雙步驟驗證的說明
本文回答 hello 最常見問題的人員詢問有關雙步驟驗證。 

## <a name="why-do-i-have-tooperform-two-step-verification-can-i-turn-it-off"></a>為什麼必須 tooperform 雙步驟驗證？ 可以將它關閉嗎？

雙步驟驗證是您的組織選擇 toouse tooprotect 您帳戶的安全性功能。 它比只是使用密碼更安全，因為它依賴兩種形式的驗證：您知道和您擁有的東西。 hello 您知道是您的密碼。 您有與您的項目是您通常會有與您的電話或裝置 hello。 當您的帳戶受到雙步驟驗證保護時，有惡意企圖的駭客即使取得您的密碼也無法登入。 因為它們沒有存取 tooyour 電話才能登入。 

Microsoft 提供了雙步驟驗證，但您的組織會選擇 toouse hello 功能。 如果您的 IT 部門需要的就像您無法選擇取消使用密碼 tooprotect 您的帳戶，您無法選擇退出。 

如果您有個人 Microsoft 帳戶開啟雙步驟驗證，並想 toochange 您的設定，請參閱[需兩步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)改為。 

## <a name="i-dont-have-my-phone-with-me-today"></a>我今天沒帶手機

幾天您離開您的電話，但仍需要在工作中的 toosign。 您應該試著 hello 第一件事登入不同的驗證方法。 當您註冊的雙步驟驗證時，未設定多個電話號碼？tootry 登入不同的方法，請遵循下列步驟：

1. 像平常一樣登入。
2. 當 hello 雙步驟驗證] 頁面開啟時，選擇**使用其他驗證選項**。

   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. 選取您想要 toouse hello 驗證選項。 
  - 如果您不需要存取 tooyour 替代方法，請連絡您的 IT 部門 tooget 協助 tooyour 帳戶在登入。
  - 如果您沒有存取 tooyour 替代方法，繼續進行兩步驟驗證。

如果您沒有看見 hello**使用其他驗證選項**連結，則這表示您沒有設定另一種方法時第一次登錄進行兩步驟驗證。 請連絡您 IT 部門 tooget 協助進行登入 tooyour 帳戶。 一旦您已登入，請確定太[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)tooadd 額外的驗證方法下, 一次。 

## <a name="i-lost-my-phone-or-got-a-new-number"></a>我遺失手機，或是有了號碼
有兩種方式 tooget 回 tooyour 帳戶。 hello 第一個是 toosign 中使用替代驗證電話號碼，如果您已設定其中一個。 hello 第二種是您的 IT 部門 tooclear tooask 您的設定。

如果您的手機遺失或遭竊，我們也建議您告訴您的 IT 部門。 其所需 tooreset 應用程式密碼，並清除任何多因素驗證。 

### <a name="use-an-alternate-phone-number"></a>使用備用電話號碼
如果您設定多個驗證選項，例如次要的電話號碼或驗證器應用程式在不同裝置上，使用其中一個 toosign 中。

toosign 中使用 hello 備用電話號碼，請遵循下列步驟：

1. 像平常一樣登入。
2. 當提示的 toofurther 驗證您的帳戶時，請選擇**使用其他驗證選項**。
   
   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. 選取 hello 電話號碼或您具有存取權的裝置。
4. 您會回到您的帳戶之後,[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)toochange 您的驗證電話號碼。

### <a name="clear-your-settings"></a>清除您的設定
如果您未設定次要驗證電話號碼，您必須 toocontact 您 IT 部門以取得協助。 已清除您的設定所以 hello 它們下次您登入，系統會提示您太[註冊進行兩步驟驗證](multi-factor-authentication-end-user-first-time.md)一次。

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>我的手機沒收到簡訊或來電
有幾項原因為什麼您可能 toosign 中，再試一次，但不是會收到 hello 文字或電話。 如果已成功在 hello 過去收到文字或撥打電話 tooyour 電話，然後此問題可能是 hello 電話提供者，不是您的帳戶發生問題。 請確定您的手機收訊良好。 而且，如果您嘗試 tooreceive 文字訊息，請確定您是無法 tooreceive 文字訊息。 您或文字詢問 friend toocall 您為測試。 

如果您已經等待幾分鐘的時間是文字或呼叫時，hello 最快方式 tooget 入您的帳戶是 tootry 不同的選項。

1. 選取**使用其他驗證選項**在 hello] 頁面上，正在等候您的驗證。
   
    ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. 選取 hello 電話號碼或傳遞方法您想要 toouse。
   
    如果您收到多個驗證碼，使用最新 hello。

如果您不需要設定其他方法，請連絡您的 IT 部門，並要求他們 tooclear 您的設定。 hello 下次您登入，系統會提示您太[設定多重要素驗證](multi-factor-authentication-end-user-first-time.md)一次。

如果您經常會有延遲，因為 toobad 儲存格訊號，我們建議使用 hello [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)智慧型手機上。 hello 應用程式會產生您在使用中，toosign 的隨機的安全驗證碼，而這些程式碼不需要任何儲存格訊號或網際網路連線。

## <a name="app-passwords-are-not-working"></a>應用程式密碼無效
首先，請確定您已正確輸入 hello 應用程式密碼。 hello 產生應用程式密碼取代一般密碼，但僅適用於較舊的桌面應用程式不支援雙步驟驗證。 如果仍無法登入，請嘗試登入並[建立新的應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。  如果還是無法登入，請連絡 IT 部門，要求他們[刪除您現有的應用程式密碼](../multi-factor-authentication-manage-users-and-devices.md)，然後建立新的密碼。

## <a name="i-didnt-find-an-answer-toomy-problem"></a>我找不到回應 toomy 問題。
如果您嘗試過這些疑難排解步驟，但仍在遭遇問題，請連絡您的 IT 部門。 它們應該能夠 tooassist 您。

## <a name="related-topics"></a>相關主題
* [管理您的雙步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)  
* [Microsoft Authenticator 應用程式常見問題集](microsoft-authenticator-app-faq.md)

