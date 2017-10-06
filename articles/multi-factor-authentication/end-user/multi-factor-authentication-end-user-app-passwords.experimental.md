---
title: "aaaHow toouse 中 Azure MFA 的應用程式密碼？ | Microsoft Docs"
description: "此頁面可協助使用者了解何謂應用程式密碼以及什麼是用於具有考慮 tooAzure MFA。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: 3afa2003d8e87576f035bf9440a1dba67bd85f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a>什麼是 Azure Multi-Factor Authentication 中的應用程式密碼？
某些非瀏覽器應用程式，例如 hello Apple 原生電子郵件用戶端會使用 Exchange Active Sync，目前不支援多重要素驗證。 Multi-Factor Authentication 會對每個使用者啟用。  這表示在下列情況下，使用者無法使用多重要素驗證：

- hello 使用者已啟用多重要素驗證
- hello 使用者正嘗試 toouse 非瀏覽器應用程式。

應用程式密碼允許 hello 使用者 toouse hello 應用程式。

擁有應用程式密碼後，您可使用此密碼來取代這些非瀏覽器應用程式的原始密碼。 當您註冊進行兩步驟驗證時，您告訴 Microsoft toolet 任何人登入您的密碼如果他們也不能執行 hello 第二個驗證。 在手機上的 hello Apple 原生電子郵件用戶端無法與您帳戶登入因為它無法進行兩步驟驗證要求。 hello 方案 toothis 問題是 toocreate 更安全的應用程式密碼，您不使用每日。 應用程式密碼僅適用於不支援雙步驟驗證的應用程式。 使用 hello 應用程式密碼，以便可以略過 multi-factor authentication 應用程式，並繼續 toowork。


> [!NOTE]
> Office 2013 用戶端 (包括 Outlook) 支援新式驗證通訊協定，而且可搭配雙步驟驗證。 應用程式密碼就不需要用於 Office 2013 用戶端。  如需詳細資訊，請參閱[發表的 Office 2013 新式驗證公開預覽](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)。


## <a name="how-toouse-app-passwords"></a>如何 toouse 應用程式密碼
以下是一些事項 tooknow，關於應用程式密碼：

* 您不用自行建立應用程式密碼。 它們是自動產生的。
* 每位使用者的密碼目前以 40 組為限。 
* 如果您已達到 hello 限制之後，您可以嘗試 toocreate 應用程式密碼，您必須 toodelete 其中一個現有的應用程式密碼之前建立一個新。
* 為每個裝置 (而非每個應用程式) 使用一個應用程式密碼。 例如，您可以為膝上型電腦建立一個應用程式密碼，並將該應用程式密碼使用於該膝上型電腦上的所有應用程式。 然後，您的桌面上建立第二個應用程式密碼 toouse 所有應用程式。 
* 您會獲得一個應用程式密碼 hello 第一次登錄時進行兩步驟驗證。  如果您需要其他密碼，您可加以建立。



## <a name="creating-and-deleting-app-passwords"></a>建立和刪除應用程式密碼
在初次登入期間，您會獲得可供使用的應用程式密碼。  您也可以稍後再建立和刪除應用程式密碼。 您刪除應用程式密碼的方式取決於您使用多重要素驗證的方式。 下列回應 hello 問題的 toodetermine 您應該在哪裡 toomanage 應用程式密碼： 

1. 您的個人 Microsoft 帳戶是否使用雙步驟驗證？ 如果是，您應該參閱 toohello[應用程式密碼及雙步驟驗證](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification)文件以取得說明。 若為否，繼續 tooquestion 兩個。

2. 好，所以您的工作或學校帳戶使用雙步驟驗證。 您使用它 toosign tooOffice 365 應用程式中？ 如果是，您應該參閱太[for Office 365 中建立應用程式密碼](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183)的說明。 若為否，繼續 tooquestion 三個。 

3. 您是否搭配 Microsoft Azure 使用雙步驟驗證？ 如果是，繼續 toohello[管理 hello Azure 入口網站中的應用程式密碼](#manage-app-passwords-in-the-Azure-portal)本文一節。 若為否，繼續 tooquestion 四個。

4. 不確定您在哪裡使用雙步驟驗證嗎？ 繼續 toohello[管理與 hello MyApps 入口網站應用程式密碼](#manage-app-passwords-with-the-myapps-portal)本文一節。 


## <a name="manage-app-passwords-in-hello-azure-portal"></a>管理 hello Azure 入口網站中的應用程式密碼
如果您搭配 Azure 使用雙步驟驗證，您會想 toocreate 應用程式密碼透過 hello Azure 入口網站。

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a>toocreate hello Azure 入口網站中的應用程式密碼
1. 登入 toohello Azure 傳統入口網站。
2. 在 hello 頂端，以滑鼠右鍵按一下您的使用者名稱並選取 其他安全性驗證。
3. 在 hello proofup 頁面上，在 hello 頂端，選取 應用程式密碼
4. 按一下 [建立] 。
5. 輸入 hello 應用程式密碼的名稱，然後按一下**下一步**
6. 複製 hello 應用程式密碼 toohello 剪貼簿，並將它貼到您的應用程式。
   
   ![雲端](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a>toodelete hello Azure 入口網站中的應用程式密碼
1. 登入 toohello Azure 傳統入口網站。
2. 在 hello 頂端，以滑鼠右鍵按一下您的使用者名稱並選取 其他安全性驗證。
3. 在 hello 頂端下, 一步 tooadditional 安全性驗證，選取**應用程式密碼。**
4. 您想要 toodelete，選取 下一步 toohello 應用程式密碼**刪除**。
5. 按一下確認 hello 刪除**是**。
6. 一旦刪除 hello 應用程式密碼，您可以按一下**關閉**。


## <a name="manage-app-passwords-with-hello-myapps-portal"></a>管理與 hello MyApps 入口網站應用程式密碼。
如果您不確定您使用多重要素驗證的方式，然後您可以一律建立及刪除透過 hello myapps 入口網站應用程式密碼。

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a>應用程式密碼使用 toocreate hello Myapps 入口網站
1. 登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. 按一下您在 hello 右上方，名稱，然後選擇**設定檔**。
3. 選取 [其他安全性驗證]。
   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. 選取 [應用程式密碼]。
   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. 按一下 [建立] 。
6. 輸入 hello 應用程式密碼的名稱，然後按一下**下一步**。
7. 複製 hello 應用程式密碼 toohello 剪貼簿，並將它貼到您的應用程式。
   ![建立應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/create2.png)

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a>應用程式密碼使用 toodelete hello Myapps 入口網站
1. 登入太[https://myapps.microsoft.com](https://myapps.microsoft.com)
2. 在 hello 頂端，選取 設定檔。
3. 選取 [其他安全性驗證]。

   ![選取 [其他安全性驗證] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. 選取 [應用程式密碼]。

   ![選取 [應用程式密碼] - 螢幕擷取畫面](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. 按一下 下一步的 toohello 應用程式密碼，您想要 toodelete，**刪除**。

   ![刪除應用程式密碼](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. 確認您想 toodelete 該密碼即可**是**。
7. 一旦刪除 hello 應用程式密碼，您可以按一下**關閉**。

## <a name="next-steps"></a>後續步驟

- [管理雙步驟驗證設定](multi-factor-authentication-end-user-manage-settings.md)

- 試試看 hello [Microsoft Authenticator 應用程式](microsoft-authenticator-app-how-to.md)tooverify 應用程式通知，而不是文字或呼叫收到與您登入。 
