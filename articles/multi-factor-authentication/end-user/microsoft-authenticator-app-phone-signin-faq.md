---
title: "aaaMicrosoft 驗證器登入-Azure 和 Microsoft 帳戶電話 |Microsoft 文件"
description: "您可以使用電話 toosign 中 tooyour Microsoft 帳戶，而不是輸入您的密碼。 本文回答有關這項功能的常見問題集。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/12/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: a4911ff580b3ffa078299ad706d099330b75a2e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-with-your-phone-not-your-password"></a>使用您的電話而不是您的密碼登入

hello Microsoft 驗證器應用程式可協助您保護您帳戶的安全，方法執行雙步驟驗證之後您輸入密碼。 但是，您知道它可以完全取代 hello 您個人的 Microsoft 帳戶的密碼嗎？ 

這項功能可在 iOS 和 Android 的裝置上提供，並且可用於個人 Microsoft 帳戶。 

## <a name="how-it-works"></a>運作方式

當您登入 Microsoft 帳戶 tooyour，許多您可以使用進行兩步驟驗證的 hello Microsoft 驗證器應用程式。 您輸入密碼，然後移 toohello 應用程式 tooeither 核准的通知，或取得驗證碼。 使用電話登入，則會略過 hello 密碼，並在您的電話上進行所有身分識別驗證。 因為電話登入是一種雙步驟驗證，您仍然需要 tooprovide 您知道的事，您唯一 tooverify 您的身分識別。 hello 電話仍然是 hello 您唯一，而且您的電話 PIN 或生物識別金鑰是您知道的 hello 動作。 

## <a name="how-tooget-started"></a>如何啟動 tooget

toosign tooyour 個人 Microsoft 帳戶與您的電話，請遵循下列步驟： 

1. 啟用電話登入帳戶。 

  - 如果您不需要 hello Microsoft 驗證器應用程式，安裝並新增您個人的 Microsoft 帳戶，根據在 hello toohello 步驟[Microsoft Authenticator 頁面](microsoft-authenticator-app-how-to.md)。 自動啟用新加入的帳戶，讓您準備好 toogo。

  - 如果您已經使用 Microsoft Authenticator 進行兩步驟驗證，hello 應用程式的首頁上，選取您的帳戶，然後選取**電話登入啟用**從 hello 下拉式選單。

  >[!NOTE] 
  >tooprotect 您的帳戶，我們所需的 PIN 或生物識別裝置上的鎖定。 如果您要保留您的電話解除鎖定，hello 應用程式要求，要求您設定鎖定 tooset 啟用電話登入之前出現。 

3. 您會正常輸入 Microsoft 帳戶密碼的大部分頁面都有一個連結，說明**改為使用應用程式**。 選取此連結 toosign，使用您的電話。 

4. Microsoft 會傳送通知 tooyour 電話。 核准 hello 通知 toosign tooyour 帳戶中。   

## <a name="faq"></a>常見問題集 

### <a name="how-is-signing-in-with-my-phone-more-secure-than-typing-a-password"></a>使用我的電話登入會如何比輸入密碼更安全？  

現今的大多數使用者登入 tooweb 站台或應用程式使用使用者名稱和密碼。  不幸的是，密碼通常會遺失、遭竊或遭駭客猜到。 當您設定中的 hello Microsoft 驗證器應用程式 toosign 時，我們會產生您可以解除鎖定您的帳戶的電話上的索引鍵。 我們會保護此機碼以 hello 的 PIN 或生物識別您已使用您的手機上。  當您登入您的電話時，這個金鑰是使用您的身分識別，安全地與兩個因素 – hello 的 tooprove 本身、 電話和能力 toounlock 它。 

使用 hello 金鑰是用 Windows Hello 和 hello FIDO 聯盟 UAF 規格中的類似 toohello 金鑰。 您簡歷資料只會在本機，使用 tooprotect hello 索引鍵和是從未傳送至，或 hello 雲端中儲存。 
 
### <a name="where-can-i-use-my-phone-tooreplace-my-password-and-where-would-i-still-need-hello-password"></a>其中可以使用我的電話 tooreplace 我的密碼，以及其中仍然需要 hello 密碼嗎？  

現在，hello 電話登入功能僅適用於 web 應用程式和由個人 Microsoft 帳戶、 iOS 或 Android 應用程式，使用個人 Microsoft 帳戶，以及在 Windows 10 上使用個人 Microsoft 帳戶的應用程式的服務。 當您登入 tooone 網站或應用程式時，在 hello 通常輸入您的密碼 頁面上沒有連結**改用應用程式**。 

電話登入不能使用的 toounlock Windows 電腦、 XBOX 或任何桌面版本的 Microsoft 應用程式，例如 Office 應用程式在此階段。 
 
### <a name="does-this-replace-two-step-verification-should-i-turn-it-off"></a>這會取代雙步驟驗證嗎？ 應該將它關機嗎？   

有時是。 我們正努力展開 hello 範圍電話登入，但是現在依然有 hello Microsoft 生態系統中不支援它的地方。 在這些位置中，我們仍會使用兩步驟驗證進行安全登入。 基於這個理由，不可以，您不應該關閉您帳戶的雙步驟驗證。 
 
### <a name="okay-if-i-keep-two-step-verification-turned-on-for-my-account-do-i-have-tooapprove-two-notifications"></a>好了，如果我保留為 我的帳戶開啟雙步驟驗證，必須 tooapprove 兩個通知？

否，您不會。 登入 Microsoft 帳戶與您的電話 tooyour 也算是雙步驟驗證。 而不是輸入您的密碼，然後核准通知您，證明您的身分識別的知道如何 toounlock 您的電話，然後核准通知。 我們不會傳送第二個通知 tooapprove。

### <a name="what-if-i-lose-my-phone-or-dont-have-it-with-me-how-can-i-access-my-account"></a>如果我遺失電話或沒有攜帶電話，要如何存取我的帳號？  

您隨時可以按一下**改為使用密碼**上 hello 登入頁面 tooswitch 回 toousing 您的密碼。 請記住，如果您使用兩步驟驗證，您仍需要第二個方法 tooverify 登入。 這就是為什麼我們強烈建議您 toomake 確定您在您的帳戶上有額外、 最新的安全性資訊。 您可以在 https://account.live.com/proofs/manage 管理您的安全性資訊。 
 
### <a name="how-do-i-stop-using-this-feature-and-go-back-tooentering-my-password"></a>如何停止使用此功能及返回 tooentering 我的密碼？

當您登入時，按一下 [改為使用密碼]。 我們請記住您最近的選擇，並提供的預設 hello 下次您登入。 如果您想要 toogo 後 toosigning 入您的手機，請按一下**改用應用程式**。 
 
### <a name="can-i-use-hello-app-toosign-in-tooall-my-accounts-with-microsoft"></a>我可以使用在 tooall hello 應用程式 toosign 我的帳戶與 Microsoft？   
這項功能只適用於個人 Microsoft 帳戶。 
 
### <a name="can-i-sign-into-my-pc-with-my-phone"></a>可以使用我的電話登入我的電腦嗎？  
針對您的電腦，我們建議您使用臉部、指紋或 PIN 碼，以 Windows 10 上的 Windows Hello 登入。   
 
### <a name="can-i-sign-in-with-my-windows-phone"></a>我可以使用 Windows Phone 登入嗎？  
在這個階段中，我們不在開發這項功能的 hello Microsoft Windows Phone 上的驗證器。 

## <a name="next-steps"></a>後續步驟
如果您尚未下載 hello Microsoft 驗證器應用程式，請將它簽出。hello 應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)，電話登入位於 hello Microsoft Authenticator 應用程式和[Android](http://go.microsoft.com/fwlink/?Linkid=825072)和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。

如果您在一般情況下有疑問 hello 應用程式，看看 hello [Microsoft 驗證器常見問題集](microsoft-authenticator-app-faq.md)
