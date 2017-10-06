---
title: "aaaThe hello Azure Active Directory B2B 共同作業邀請電子郵件項目 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業邀請電子郵件範本"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>hello hello B2B 共同作業邀請電子郵件項目

邀請電子郵件都是重要的元件 toobring 夥伴上做為 B2B 共同作業的使用者在 Azure AD 中。 您可以使用它們 tooincrease hello 收件者的信任。 您可以加入合法性和社交證明 toohello 電子郵件、 toomake 確定 hello 收件者都想要選取 hello**開始**按鈕 tooaccept hello 邀請。 此信任是索引鍵表示 tooreduce 共用摩擦。 而且也想 toomake hello 電子郵件尋找很棒 ！

![Azure AD B2b 邀請電子郵件](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>說明 hello 電子郵件
因此您知道如何最佳 toouse 其功能，讓我們看看 hello 電子郵件的幾個項目。

### <a name="subject"></a>主旨
hello hello 電子郵件主旨會遵循下列模式的 hello： 邀請您 toohello &lt;tenantname&gt;組織

### <a name="from-address"></a>寄件者地址
針對從位址 hello 使用 LinkedIn 類似的模式。  您應該很清楚 hello 邀請者並從公司，以及也釐清該 hello 電子郵件來自 Microsoft 的電子郵件地址。 hello 格式：&lt;邀請者顯示名稱&gt;從&lt;tenantname&gt; （透過 Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>回覆地址
hello 回覆 tooemail 設定 toohello 邀請者電子郵件時使用，以便回覆 toohello 電子郵件會傳送電子郵件後 toohello 邀請者。

### <a name="branding"></a>商標
hello 邀請電子郵件，從您的租用戶使用 hello 公司品牌，您可能已設定為您的租用戶。 如果您想要利用這項功能，tootake[這裡](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)hello 詳細資料，如何 tooconfigure 它。 hello 橫幅標誌會出現在 hello 電子郵件。 請遵循 hello 映像大小和品質指示[這裡](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal)為了獲得最佳結果。 此外，hello 公司名稱也會顯示 hello 呼叫 tooaction 中。

### <a name="call-tooaction"></a>呼叫 tooaction
hello 呼叫 tooaction 是由兩個部分所組成： 說明為什麼 hello 收件者已收到 hello 郵件，以及哪些 hello 收件者會 toodo 要求資訊，請參閱。
- hello 可以使用下列模式的 hello 處理 「 原因 」 一節： 已受邀的 tooaccess 應用程式在 hello &lt;tenantname&gt;組織

- 和 「 什麼詢問您是否正在 toodo 」 一節以 hello 與否 hello hello**開始**] 按鈕。 當 hello 收件者已加入而 hello 需要在邀請時，這個按鈕不會顯示。

### <a name="inviters-information"></a>邀請者的資訊
hello 邀請者顯示名稱會包含在 hello 電子郵件。 而且此外，如果您已設定為您的 Azure AD 帳戶的設定檔圖片，hello 邀請電子郵件將包含也該圖片。 這兩個是預定的 tooincrease hello 電子郵件收件者的信心。

如果您尚未尚未設定設定檔圖片，與 hello 邀請者縮寫取代 hello 圖片圖示所示：

  ![顯示 hello 邀請者縮寫](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>內文
hello 主體會包含 hello 訊息該 hello 邀請者撰寫或透過 hello 邀請 API 傳遞。 因為它是文字區域，所以不會基於安全考量處理 HTML 標記。

### <a name="footer-section"></a>頁尾區段
hello 頁尾包含 hello Microsoft 公司品牌，並可讓 hello 收件者知道如果 hello 電子郵件已傳送未受監視的別名。 特殊案例：

- hello 邀請者不在 hello 邀請租用戶的電子郵件地址

  ![邀請者的圖片不在 hello 邀請租用戶的電子郵件地址](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- hello 收件者不需要 tooredeem hello 邀請

  ![當收件者不需要 tooredeem 邀請](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [什麼是 Azure AD B2B 共同作業](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B 共同作業 API 和自訂](active-directory-b2b-api.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
