---
title: "aaaMicrosoft Authenticator 應用程式說明及支援 |Microsoft 文件"
description: "提供的常見問題集清單，以及解答相關的 toohello Microsoft 驗證應用程式與 Azure Multi-factor Authentication。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f04d5bce-e99e-4f75-82d1-ef6369be3402
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: afba9b59ccaac60d022e8516fcf573dcfbf68af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-authenticator-app-faq"></a>Microsoft Authenticator 應用程式常見問題集

本文回答的問題，我們收到 hello Microsoft Authenticator 應用程式。 如果您沒有看到回應 tooyour 問題，請移至 toohello [Microsoft 驗證器應用程式論壇](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp)。 我們也有 hello 應用程式，另一個特定功能的相關的常見問題集[登入您的電話常見問題集](microsoft-authenticator-app-phone-signin-faq.md)。

hello Microsoft 驗證器應用程式取代 hello Azure Authenticator 應用程式，並 hello 時，建議應用程式使用 Azure Multi-factor Authentication。 hello Microsoft 驗證器應用程式是供[Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071)， [Android](http://go.microsoft.com/fwlink/?Linkid=825072)，和[IOS](http://go.microsoft.com/fwlink/?Linkid=825073)。

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="what-are-hello-codes-in-hello-app-for-why-does-hello-number-keep-counting-down"></a>Hello 代碼 hello 應用程式中的有哪些？ 為什麼沒有 hello 數保留計算向下？

當您開啟 hello Microsoft 驗證器應用程式時，您看到您新增的 hello 帳戶和六個或八位元數字的每個。 您可能會看到三十秒倒數。

當您登入 tooyour 帳戶，則會使用這些代碼。 輸入您的使用者名稱和密碼之後，您可能會要求您 tooenter 驗證碼。 開啟 hello Microsoft 驗證器應用程式，並複製 hello 程式碼，表示目前顯示。 Hello 登入頁面 toofinish 中輸入該程式碼。

hello hello 碼每隔 30 秒的變更是，讓您永遠不會使用 hello 兩次相同的程式碼的原因。 不像是密碼一樣，您應該 tooremember。 hello 概念是只有具備存取 tooyour 電話的人知道您的驗證碼。

hello 碼不需要網際網路或資料，所以您不需要讓電話服務 toosign tooworry。 當您關閉 hello 應用程式時，它不在 hello 背景繼續執行，並不會使得電池電力耗盡。 您可以關閉 hello 應用程式，並忽略直到 hello 登入的下一次。  

### <a name="i-only-get-notifications-when-i-have-hello-app-open-if-hello-app-isnt-open-i-dont-get-any-notifications"></a>我只收到通知，當有開啟的 hello 應用程式時。 如果 hello 應用程式未開啟，我無法取得任何通知。

如果您收到通知，但未進行雜訊，或者震動儘管您在上的響鈴，先檢查 hello 應用程式設定。 啟用 hello 應用程式 toouse 聲音，或使用其通知進行震動。

如果您沒有收到通知，請檢查下列情況下的 hello:

- 您的電話處於「請勿打擾」還是無訊息模式？ 此模式可以讓應用程式傳送通知。
- 您可以接收來自其他應用程式的通知嗎？ 如果沒有，則可能會在您的電話或從 Android 或 Apple 的 hello 通知通道的 hello 網路連線發生問題。 您可以在您的電話設定，來解決 hello 第一個選項，但您可能需要 tootalk tooyour 服務提供者與 hello 第二個選項的說明。
- 您可以收到 hello 應用程式，在某些帳戶而非其他電腦的通知？ 如果是，從您的應用程式移除 hello 有問題的帳戶，並將它重新加入 tooenable 推播通知。 

如果嘗試了上述疑難排解的建議但仍有問題，請將您的記錄傳送給我們以供診斷。 開啟 toohello 應用程式設定，然後選取**說明與意見反應**和**傳送記錄檔**。 接著，前往 toohello [Microsoft 驗證器應用程式論壇](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp)，讓我們知道什麼問題，您看見與步驟嘗試過為止。 

### <a name="im-already-using-hello-microsoft-authenticator-application-for-verification-codes-how-do-i-switch-tooone-click-push-notifications"></a>我已經在使用 hello Microsoft 驗證器應用程式的驗證碼。 我要如何切換 tooone 按一下推播通知？
透過推播通知核准登入僅適用於個人的 Microsoft 帳戶或是工作和學校 Microsoft 帳戶，而不適用於 Google 或 Facebook 這類協力廠商帳戶。 如果您有工作或學校的 Microsoft 帳戶，您的組織可以選擇 toodisable 此選項。

如果您使用 Microsoft 帳戶為您個人的帳戶，並想 tooswitch 透過 toopush 通知，您需要 tooadd 您的帳戶一次。 重新註冊 hello 裝置與您的帳戶，並設定推播通知。  

如果您使用 Microsoft Authenticator 工作或學校帳戶，則您的組織決定是否 tooallow 單鍵通知。

### <a name="do-one-click-push-notifications-work-for-non-microsoft-accounts"></a>單鍵推播通知適用於非 Microsoft 帳戶嗎？
不適用，推播通知只適用於 Microsoft 帳戶與 Azure Active Directory 帳戶。 如果您的工作或學校使用 Azure AD 帳戶，它們可能會停用這項功能。  

### <a name="i-restored-my-device-from-a-backup-and-my-account-codes-are-missing-or-not-working-what-happened"></a>我從備份還原了我的裝置，但我的帳戶代碼遺漏或無法運作。 發生什麼情形？
基於安全考量，我們不會從應用程式的備份還原帳戶。  還原 hello 應用程式之後，刪除您的帳戶，然後再次新增。

### <a name="i-got-a-new-device-how-do-i-remove-hello-microsoft-authenticator-app-from-my-old-device-and-move-toohello-new-one"></a>我收到新的裝置。 如何從我的舊裝置中移除 hello Microsoft 驗證器應用程式和移動 toohello 新？
新增 hello Microsoft 驗證器應用程式 tooa 新裝置不會自動移除它的其他裝置。 toomanage 哪些裝置已針對您的帳戶，請瀏覽 hello toomanage 雙步驟驗證，並選擇 tooremove 舊的應用程式相同的網站。

針對個人 Microsoft 帳戶，這個網站是您的[帳戶安全性](https://account.microsoft.com/security)頁面。 針對工作或學校 Microsoft 帳戶，這個網站可能是 [MyApps](https://myapps.microsoft.com) 或您的組織已設定的自訂入口網站。

### <a name="how-do-i-remove-an-account-from-hello-app"></a>如何移除從 hello 應用程式的帳戶？
* iOS: hello 主畫面上，從帳戶磚往左撥動。 選取 [刪除] 。
* Windows Phone： 從 hello 主畫面上，選取 [hello] 功能表按鈕，然後**編輯帳戶**。 點選 hello **X**下一個 toohello 帳戶名稱。
* Android： 從 hello 主畫面上，選取 [hello] 功能表按鈕，然後**編輯帳戶**。 點選 hello **X**下一個 toohello 帳戶名稱。

如果您有向您的組織註冊的裝置，您可能需要額外的步驟 tooremove toocomplete 您的帳戶。 在這些裝置上 hello Microsoft 驗證器應用程式會自動註冊為裝置系統管理員。 如果您想 toocompletely 解除安裝 hello 應用程式，您需要 toofirst hello hello 應用程式設定的應用程式取消註冊。

### <a name="why-does-hello-app-request-so-many-permissions"></a>為什麼 hello 應用程式會要求這麼多的權限？
以下是我們可能會要求，權限的完整清單，並在 hello 應用程式中的使用方式。 hello 特定權限，您會看到取決於您的電話 hello 類型。

* **相機**： 加入工作、 學校或非 Microsoft 帳戶時，我們會使用您的相機 tooscan QR 代碼。
* **連絡人和 phone**： 當您使用您個人的 Microsoft 帳戶登入時，我們會嘗試 toosimplify hello 處理程序藉由尋找您在手機使用的現有帳戶。
* **SMS**： 當您登入您個人的 Microsoft 帳戶 hello 第一次時，我們有 toomake 確定電話號碼相符項目 hello 我們可以記錄上。 我們會傳送文字訊息 toohello 電話 hello 應用程式的下載位置。 hello 訊息包含 6-8 位數驗證碼。 而不是要求您 toofind 此程式碼，並將其輸入在 hello 應用程式中，我們發現它在 hello 文字訊息為您。
* **其他應用程式上繪製**： 當您收到通知 tooverify 您的身分識別時，我們可能會執行任何其他應用程式透過顯示該通知。
* **接收資料，從 hello 網際網路**： 此權限，需要在傳送通知。
* **防止手機進入休眠**：如果您向組織註冊裝置，則他們可以在您的手機上變更這個原則。
* **控制震動**： 您可以選擇是否希望震動時接收通知 tooverify 您的身分識別。
* **使用指紋硬體**︰確認身分識別時，部分工作和學校帳戶需要額外的 PIN。 toomake hello 程序更輕鬆，我們讓您 toouse 指紋而不是輸入 hello 的 PIN。
* **檢視網路連線**： 當您新增 Microsoft 帳戶時，hello 應用程式需要的網路/網際網路連線。
* **讀取您的儲存體的 hello 內容**： 報表透過 hello 應用程式設定的技術問題時，才會使用此權限。 收集您的儲存體的部分資訊 toodiagnose hello 問題。
* **完整網路存取**： 此權限，需要在傳送通知 tooverify 您的身分識別。
* **在啟動時執行**： 如果您重新啟動您的電話，此權限可確保您繼續收到通知 tooverify 您的身分識別。

### <a name="why-does-hello-microsoft-authenticator-app-allow-you-tooapprove-a-request-without-unlocking-hello-device"></a>為什麼確實 hello Microsoft 驗證器應用程式可讓您的要求，而不解除鎖定 hello 裝置 tooapprove？

您不需要您的裝置 tooapprove 驗證要求，因為您只需要 tooprove 是，您會需要您的電話與您的 toounlock。 雙步驟驗證需要證明兩件事 - 一件是您知道的，另一件則是您擁有的。 hello，就是您的密碼。 您擁有的 hello 件事就是您的電話 （hello Microsoft Authenticator 應用程式設定和註冊 MFA 證明為）。因此，擁有 hello 電話並核准 hello 要求符合 hello hello 第二個驗證因素的準則。 

### <a name="what-does-hello-lock-icon-in-hello-account-list-mean"></a>Hello 帳戶清單中的 hello 鎖定圖示代表什麼意思？

hello 掛鎖圖示表示該 hello 裝置會在 Azure AD 中註冊且 toohello 帳戶註冊。 iOS 的裝置註冊是在 Microsoft Intune 註冊期間進行。

## <a name="next-steps"></a>後續步驟

### <a name="contact-us"></a>與我們連絡
如果您的問題未在此處找到答案，我們想要從您的 toohear。 移 toohello [Microsoft 驗證器應用程式論壇](https://social.technet.microsoft.com/Forums/en-US/home?forum=MicrosoftAuthenticatorApp)toopost 問題和 get hello 社群協助或離開此頁面上的註解。


### <a name="related-topics"></a>相關主題
* Microsoft 帳戶的[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)
* 針對您的工作或學校帳戶[使用雙步驟驗證遇到困難](multi-factor-authentication-end-user-troubleshoot.md)？
* [使用中 」 從您的電話中的 hello Microsoft Authenticator toosign](microsoft-authenticator-app-phone-signin-faq.md)

