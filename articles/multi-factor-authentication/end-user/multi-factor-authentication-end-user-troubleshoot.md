---
title: "針對雙步驟驗證進行疑難排解 | Microsoft Docs"
description: "本文件將提供如果使用者使用 Azure Multi-Factor Authentication 遇到問題時，該怎麼辦的資訊。"
services: multi-factor-authentication
keywords: "多重要素驗證用戶端, 驗證的問題, 相互關聯識別碼"
documentationcenter: 
author: barlanmsft
manager: mtillman
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: barlan
ms.reviewer: richagi
ms.custom: end-user
ms.openlocfilehash: 840f4f9e3616f5a60ebbbb0ad33cee9a67958989
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="get-help-with-two-step-verification"></a>取得雙步驟驗證的說明
本文回答人們最常詢問有關雙步驟驗證的問題。

## <a name="why-do-i-have-to-perform-two-step-verification-can-i-turn-it-off"></a>為什麼必須執行雙步驟驗證？ 可以將它關閉嗎？

雙步驟驗證是貴組織選擇用來保護您帳戶的安全性功能。 它比只是使用密碼更安全，因為它依賴兩種形式的驗證：您知道和您擁有的東西。 您知道的就是密碼。 您擁有的是您通常帶在身邊的手機或裝置。 當您的帳戶受到雙步驟驗證時，這表示惡意駭客如果以某種方式取得您的密碼，也無法以您的身分登入，因為他們無法存取您的手機。

Microsoft 提供了雙步驟驗證，但您的組織選擇使用該功能。 如果您的公司支援人員要求您，您無法選擇取消使用，就像是您無法選擇取消使用密碼來保護您的帳戶。

如果您已為您的個人 Microsoft 帳戶開啟雙步驟驗證，而且想要變更設定，請改為閱讀[關於雙步驟驗證](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification)。

## <a name="i-dont-have-my-phone-with-me-today"></a>我今天沒帶手機

有些天您會將手機留在家裡，但仍需要登入工作。 您首先應該嘗試使用不同的驗證方法登入。 當您註冊雙步驟驗證時，是否有設定多個手機號碼？ 若要嘗試以不同的方法登入，請遵循下列步驟：

1. 像平常一樣登入。
2. 當雙步驟驗證頁面開啟時，選擇 [使用其他驗證選項]。

   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. 選取您想要使用的驗證選項。
4. 繼續雙步驟驗證。

如果您沒有看到 [使用其他驗證選項] 連結，則表示您在第一次登錄雙步驟驗證時並未設定另一種方法。 請連絡您的公司支援人員，以協助登入您的帳戶。 一旦您登入，請務必[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)，為下次新增額外的驗證方法。

如果您看到 [使用其他驗證選項] 連結，但也無法存取您的替代方法，請連絡您的公司支援人員以取得協助，登入您的帳戶。

## <a name="i-lost-my-phone-or-got-a-new-number"></a>我遺失手機，或是有了號碼
有兩種方式可以取回您的帳戶。 第一種是使用備用驗證電話號碼登入 (如果已設定)。 第二種是要求您的公司支援人員清除您的設定。

如果您的手機遺失或遭竊，也建議告知您的公司支援人員，讓他們能重設您的應用程式密碼，並清除任何已記住的裝置。

### <a name="use-an-alternate-phone-number"></a>使用備用電話號碼
如果您已設定多個驗證選項 (包含不同裝置上的次要電話號碼或驗證器應用程式)，則可以使用其中一個選項來登入。

若要使用備用電話號碼登入，請遵循下列步驟︰

1. 像平常一樣登入。
2. 系統提示進一步驗證您的帳戶時，請選擇 [使用不同的驗證選項]。

   ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)

3. 選取您具有存取權的手機號碼或裝置。
4. 取回您的帳戶之後，請[管理您的設定](multi-factor-authentication-end-user-manage-settings.md)以變更您的驗證電話號碼。

### <a name="clear-your-settings"></a>清除您的設定
如果您尚未設定次要驗證手機號碼，則需要連絡公司支援人員來尋求協助。 請他們清除您的帳戶，因此，在下次登入時，系統會提示您重新[註冊雙步驟驗證](multi-factor-authentication-end-user-first-time.md)。

## <a name="i-am-not-receiving-a-text-or-call-on-my-phone"></a>我的手機沒收到簡訊或來電
有幾個原因您可能會嘗試登入，而不是收到簡訊或來電。 如果您的手機過去成功收到過簡訊或來電，則這可能是電話提供者問題，而非帳戶問題。 請確定您的手機收訊良好，而且，如果您嘗試接收文字訊息，請確定您能夠接收文字訊息。 要求朋友打電話給您，或是傳送簡訊作為測試。

如果您已經等待幾分鐘的時間還沒收到文字或通話，則進入您帳戶的最快速方法是嘗試不同的選項。

1. 在等候您驗證的頁面上，選取 [使用不同的驗證選項]。

    ![不同的驗證方式](./media/multi-factor-authentication-end-user-troubleshoot/diff_option.png)
2. 選取您想要使用的電話號碼或傳遞方法。

    如果收到多個驗證碼，請使用最新的驗證碼。

如果您未設定其他方法，請連絡公司支援人員並要求他們清除您的設定。 下次登入時，系統會提示您再次[設定多重要素驗證](multi-factor-authentication-end-user-first-time.md)。

如果您經常因手機收訊不良而延遲，則建議在智慧型手機上使用 [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)。 應用程式可以產生您用來登入的隨機安全驗證碼，而且這些代碼不需要任何手機訊號或網際網路連接。

## <a name="app-passwords-are-not-working"></a>應用程式密碼無效
首先，請確定您輸入的是正確的應用程式密碼。 產生的應用程式密碼會取代您的一般密碼，但僅適用於不支援雙步驟驗證的較舊桌面應用程式。 如果仍無法登入，請嘗試登入並[建立新的應用程式密碼](multi-factor-authentication-end-user-app-passwords.md)。  如果還是無法登入，請連絡公司支援人員，要求他們[刪除您現有的應用程式密碼](../multi-factor-authentication-manage-users-and-devices.md)，然後建立新的密碼。

## <a name="i-didnt-find-an-answer-to-my-problem"></a>我找不到我問題的解答。
如果您嘗試過這些疑難排解步驟，但仍遭遇問題，請連絡您的公司支援人員。 他們應該可以協助您。

## <a name="related-topics"></a>相關主題
* [管理您的雙步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)  
* [Microsoft Authenticator 應用程式常見問題集](microsoft-authenticator-app-faq.md)
