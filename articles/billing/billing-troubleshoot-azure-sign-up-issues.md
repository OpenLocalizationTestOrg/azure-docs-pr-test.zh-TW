---
title: "aaaTroubleshoot Azure 註冊問題 |Microsoft 文件"
description: "描述如何 tootroubleshoot 某些常見的 Azure 註冊問題。"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>針對 Azure 的註冊問題進行疑難排解
如果您無法註冊 Azure，請在此發行項 tootroubleshoot 常見的問題使用 hello 秘訣。 如果在註冊期間遇到信用卡的問題，請參閱[在 Azure 註冊時信用卡或金融卡遭到拒絕](billing-credit-card-fails-during-azure-sign-up.md)。 如果您有 Azure 帳戶，但無法登入，請參閱[無法登入 toomanage 我 Azure 訂用帳戶](billing-cannot-login-subscription.md)。

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>[依據卡片進行身分識別驗證] 區段中的進度列停止回應

卡 toocomplete hello 身分識別驗證，您的瀏覽器必須允許第三方 cookie。

![Hello 卡區段在註冊期間溢出的身分識別驗證的螢幕擷取畫面](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

使用下列步驟 tooupdate hello 瀏覽器的 cookie 設定。

1. 如果您使用 Chrome，請移至太**設定** > **顯示進階設定** > **隱私權** > **內容設定**。 取消選取 [封鎖第三方 Cookie 和網站資料]。
2. 如果您使用邊緣，請移至太**設定** > **檢視進階設定** > **Cookie**。 選取 [不要封鎖 Cookie]。
3. 重新整理 hello Azure 註冊頁面上，並檢查是否已解決 hello 問題。
4. 如果 hello 重新整理後仍無法解決 hello 問題，請結束並重新啟動瀏覽器然後再試一次。

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>信用卡表單不支援我的帳單地址
帳單地址必須在您選取在 hello hello 國家/地區的 toobe**關於您**> 一節。 請確定您選取 hello 正確的國家/地區。

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>註冊帳戶驗證期間沒有文字訊息或呼叫
雖然通常會更快，就會在傳送驗證碼 toobe toofour 分鐘。 您輸入驗證 hello 電話號碼不儲存為 hello 帳號的連絡電話號碼。

以下是一些其他的祕訣：
* VOIP 電話號碼不能用於 hello 電話驗證程序。
* 檢查輸入，包括您在 [hello] 下拉式功能表中選取的 hello 國碼 hello 電話號碼。
* 如果您的電話未收到簡訊 (SMS)，再試一次 hello**撥號給我**選項。
* 請確定您的電話可以接收來自美國電話號碼的來電或簡訊。

當您取得 hello 簡訊或電話時，輸入程式碼，您會收到 hello 文字方塊中。

## <a name="credit-card-declined-or-not-accepted"></a>信用卡被拒絕或不被接受
虛擬卡、預付信用卡或金融卡不被視為 Azure 訂用帳戶的付款方式。 toosee 還發生了什麼可能會造成您的卡片 toobe 拒絕，請參閱[您的信用卡或扣款卡被拒絕，以註冊 Azure](billing-credit-card-fails-during-azure-sign-up.md)。

## <a name="free-trial-is-not-available"></a>「無法使用免費試用版」
您使用 Azure 訂用帳戶中的 hello 過去嗎？hello Azure 使用規定限制僅針對該使用者是新 tooAzure 免費試用啟用。 如果您有任何其他類型的 Azure 訂用帳戶，會無法啟用免費試用。 請考慮註冊[隨用隨付訂用帳戶](https://azure.microsoft.com/offers/ms-azr-0003p/)。

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>我的免費試用帳戶收到一筆費用
您可能會看到一個小型您登入設定，這會移除 3 too5 天內後保留在您的信用卡帳戶驗證。 如果您擔心管理成本，請深入了解[如何避免非預期的成本](https://docs.microsoft.com/azure/billing/billing-getting-started)。

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>無法啟用 MSDN、BizSpark、BizSparkPlus 或 MPN 之類的 Azure 權益方案
請確定您使用 hello 右登入認證。 然後檢查 hello 權益程式 toomake 確定您符合資格。 

* MSDN
  * 請在您的 [MSDN 帳戶頁面](https://msdn.microsoft.com/subscriptions/manage/default.aspx)驗證自己的資格狀態。
  * 如果您無法驗證您的狀態，請連絡 hello [MSDN 訂用帳戶客戶服務中心](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * 登入 toohello [BizSpark 入口網站](https://www.microsoft.com/bizspark/default.aspx#start-two)和 BizSpark 和 BizSpark 加號確認資格狀態。
  * 如果您無法驗證您的狀態，您可以[在 hello BizSpark 論壇取得說明](http://aka.ms/bzforums)。
* MPN
  * 登入 toohello [MPN 入口網站](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx)並驗證資格狀態。 如果您有適當的 hello[雲端平台能力](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx)，您可進行額外的好處。
  * 如果您無法驗證自己的狀態，請連絡 [MPN 支援](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx)。

## <a name="cant-activate-new-azure-in-open-subscription"></a>無法啟用新的 Azure in Open 訂用帳戶
toocreate 開啟中 Azure 訂用帳戶，您必須至少一個 「 開啟 Azure 中的語彙基元相關聯 tooit 與有效的線上服務啟用 (OSA) 金鑰。 如果您沒有 OSA 金鑰，請連絡 [Microsoft Pinpoint](http://pinpoint.microsoft.com/) 中列出的其中一個 Microsoft 合作夥伴。

## <a name="need-help-contact-support"></a>需要協助嗎？ 請連絡支援人員。
如果您仍需要協助，[連絡支援人員](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)tooget 快速解決您的問題。
