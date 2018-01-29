---
title: "如何在 Azure MFA 中使用應用程式密碼？ | Microsoft Docs"
description: "本頁面將協助使用者了解什麼是應用程式密碼，以及它們在 Azure MFA 方面的用途。"
services: multi-factor-authentication
documentationcenter: 
author: barlanmsft
manager: mtillman
ms.reviewer: richagi
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: barlan
ms.custom: end-user
ms.openlocfilehash: 55ca5ada0db30440e4599c77b7a6834ef671c7a4
ms.sourcegitcommit: 7d4b3cf1fc9883c945a63270d3af1f86e3bfb22a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>什麼是 Azure Multi-Factor Authentication 中的應用程式密碼？
有些非瀏覽器應用程式 (例如使用 Exchange Active Sync 的 Apple 原生電子郵件用戶端) 目前不支援 Multi-Factor Authentication。 Multi-Factor Authentication 會對每個使用者啟用。 這表示如果使用者已啟用 Multi-Factor Authentication，並嘗試使用非瀏覽器應用程式，他們將無法這麼做。 應用程式密碼允許發生此情形。 如果您透過條件式存取原則強制執行 Multi-Factor Authentication (而不是透過每個使用者的 MFA)，則無法建立應用程式密碼。 使用條件式存取原則來控制存取權的應用程式不需要應用程式密碼。

擁有應用程式密碼後，您可使用此密碼來取代這些非瀏覽器應用程式的原始密碼。 這是因為當您註冊進行雙步驟驗證時，就是告知 Microsoft 如果有人使用您的密碼登入但未執行第二次驗證，則不允許他們登入。 您電話上的 Apple 原生電子郵件用戶端無法以您的身份登入，因為它不能要求進行雙步驟驗證。 這個的解決方法是建立一個您不會每天使用的更安全應用程式密碼，而且它也只針對不支援雙步驟驗證的應用程式。 使用應用程式密碼可讓應用程式略過 Multi-Factor Authentication 並繼續運作。

> [!NOTE]
> Office 2013 用戶端 (包括 Outlook) 支援新式驗證通訊協定，而且可搭配雙步驟驗證。  這表示一旦啟用後，應用程式密碼就不需要使用於 Office 2013 用戶端。  如需詳細資訊，請參閱[發表的 Office 2013 新式驗證公開預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。


## <a name="how-to-use-app-passwords"></a>如何使用應用程式密碼
以下是使用應用程式密碼的一些注意事項。

* 您不用自行建立應用程式密碼。 它們是自動產生的。 因為每個應用程式只需要輸入應用程式密碼一次，所以使用較複雜且自動產生的密碼比您自創一個可記住的密碼更為安全。
* 每位使用者的密碼目前以 40 組為限。 如果您嘗試在達到此限制後建立密碼，系統會提示您刪除其中一個現有的應用程式密碼，然後才能建立新密碼。
* 您應該為每個裝置 (而非每個應用程式) 使用一個應用程式密碼。 例如，您可以為膝上型電腦建立一個應用程式密碼，並將該應用程式密碼使用於該膝上型電腦上的所有應用程式。 接著，建立第二個應用程式密碼用於您桌面上的所有應用程式。
* 您在第一次註冊進行雙步驟驗證時會獲得一個應用程式密碼。  如果您需要其他密碼，您可加以建立。



## <a name="creating-and-deleting-app-passwords"></a>建立和刪除應用程式密碼
在初次登入期間，您會獲得可供使用的應用程式密碼。  此外，您也可以稍後再建立和刪除應用程式密碼。  您執行此動作的方式取決於您使用 Multi-Factor Authentication 的方式。 回答下列問題來判斷您應該到哪裡來管理應用程式密碼：

1. 您的個人 Microsoft 帳戶是否使用雙步驟驗證？ 如果是，您應該參閱[應用程式密碼和雙步驟驗證](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification)一文的說明。 如果不是，繼續回答第二個問題。

2. 好，所以您的工作或學校帳戶使用雙步驟驗證。 您是否用這些帳戶登入 Office 365 應用程式？ 如果是，您應該參閱[建立 Office 365 應用程式密碼](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)的說明。 如果不是，繼續回答第三個問題。

3. 您是否搭配 Microsoft Azure 使用雙步驟驗證？ 如果是，繼續移至本文中[在 Azure 入口網站中管理應用程式密碼](#manage-app-passwords-in-the-Azure-portal)一節。 如果不是，繼續回答第四個問題。

4. 不確定您在哪裡使用雙步驟驗證嗎？ 繼續移至本文中[使用 MyApps 入口網站管理應用程式密碼](#manage-app-passwords-with-the-myapps-portal)一節。


## <a name="manage-app-passwords-in-the-azure-portal"></a>在 Azure 入口網站中管理應用程式密碼
如果您搭配 Azure 使用雙步驟驗證，您會想要透過 Azure 入口網站建立應用程式密碼。



## <a name="manage-app-passwords-with-the-myapps-portal"></a>使用 MyApps 入口網站管理應用程式密碼。
如果您不確定您使用 Multi-Factor Authentication 的方式，一律可以透過 myapps 入口網站建立和刪除應用程式密碼。

### <a name="to-create-an-app-password-using-the-myapps-portal"></a>使用 MyApps 入口網站建立應用程式密碼
1. 登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. 按一下右上方的您的名稱，然後選擇 [設定檔]。
3. 選取 [其他安全性驗證]。
   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. 選取 [應用程式密碼]。
   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. 按一下頁面底部的 [新增] 。
6. 輸入應用程式密碼的名稱，然後按 [下一步] 。
7. 將應用程式密碼複製到剪貼簿，並將它貼到您的應用程式。
   ![建立應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="to-delete-an-app-password-using-the-myapps-portal"></a>使用 MyApps 入口網站刪除應用程式密碼
1. 登入 [https://myapps.microsoft.com](https://myapps.microsoft.com)
2. 在頂端，選取 [設定檔]。
3. 選取 [其他安全性驗證]。

   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. 選取 [應用程式密碼]。

   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. 在您想要刪除的應用程式密碼旁，按一下 [刪除] 。

   ![刪除應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. 按一下 [是] 以確認您要刪除該密碼。
7. 應用程式密碼刪除之後，就可以按一下 [關閉]。

## <a name="next-steps"></a>後續步驟

- [管理雙步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)

- 試用 [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)，透過應用程式通知來驗證您的登入，而不是透過文字訊息或電話。
