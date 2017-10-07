---
title: "aaaAzure Active Directory B2B 共同作業應用程式開發介面和自訂 |Microsoft 文件"
description: "Azure Active Directory B2B 共同作業支援跨公司關聯性，方式是讓商務夥伴 tooselectively 存取公司的應用程式"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Azure Active Directory B2B 共同作業 API 和自訂

我們發現許多客戶，告訴他們想 toocustomize hello 邀請程序，最適合組織的方式。 使用我們的 API，您可以進行自訂。 [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Hello 邀請應用程式開發介面的功能
hello API 提供下列功能的 hello:

1. 使用*任何*電子郵件地址來邀請外部使用者。

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. 自訂您想之後他們接受的邀請使用者 tooland。

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. 選擇透過我們的 toosend hello 標準邀請 mail

    ```
    "sendInvitationMessage": true
    ```

  您可以自訂訊息 toohello 收件者

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. 選擇 toocc： 您想要在 hello tookeep 人員迴圈關於邀請這個共同作業者。

5. 或完全選擇不 toosend 透過 Azure AD 的通知，以自訂您的邀請和入門訓練工作流程。

    ```
    "sendInvitationMessage": false
    ```

  在此情況下，您會回到兌換 URL 從 hello API，您可以內嵌在電子郵件範本、 IM 或您選擇的其他發佈方法。

6. 最後，如果您是系統管理員，您可以選擇 tooinvite hello 使用者為成員。

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>授權模型
hello API 可以執行下列授權模式的 hello:

### <a name="app--user-mode"></a>應用程式 + 使用者模式
在此模式中，所有人員都使用 hello API 需求 toohave hello 權限 toobe 建立 B2B 邀請。

### <a name="app-only-mode"></a>僅應用程式模式
應用程式只有在內容中，必須 hello User.ReadWrite.All 或 Directory.ReadWrite.All 範圍 hello 邀請 toosucceed hello 應用程式。

如需詳細資訊，請參閱︰ https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
它是現在可能 toouse PowerShell tooadd 和邀請外部使用者 tooan 組織輕鬆。 建立邀請使用 hello cmdlet:

```
New-AzureADMSInvitation
```

您可以使用下列選項的 hello:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

您也可以查看中的 hello 邀請應用程式開發介面參考[https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>後續步驟

請瀏覽有關 Azure AD B2B 共同作業的其他文章：

* [何謂 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者？](active-directory-b2b-admin-add-users.md)
* [資訊工作者如何新增 B2B 共同作業使用者？](active-directory-b2b-iw-add-users.md)
* [hello hello B2B 共同作業邀請電子郵件項目](active-directory-b2b-invitation-email.md)
* [B2B 共同作業邀請兌換](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B 共同作業授權](active-directory-b2b-licensing.md)
* [針對 Azure Active Directory B2B 共同作業問題進行疑難排解](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B 共同作業常見問題 (FAQ)](active-directory-b2b-faq.md)
* [適用於 B2B 共同作業使用者的多重要素驗證](active-directory-b2b-mfa-instructions.md)
* [在沒有邀請的情況下新增 B2B 共同作業使用者](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory 中應用程式管理的文章索引](active-directory-apps-index.md)
