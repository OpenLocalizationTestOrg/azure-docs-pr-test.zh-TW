---
title: "aaaGet 啟動 Azure Multi-factor Auth 提供者 |Microsoft 文件"
description: "深入了解如何 toocreate Azure Multi-factor Auth 提供者。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>開始使用 Azure Multi-Factor Auth Provider
依預設，擁有 Azure Active Directory 和 Office 365 使用者的全域管理員可以使用雙步驟驗證。 不過，如果您想利用 tootake[進階功能](multi-factor-authentication-whats-next.md)則您應該購買 hello 完整版本的 Azure Multi-factor Authentication (MFA)。

使用 Azure Multi-factor Auth 提供者 tootake 利用 hello 完整版本的 Azure MFA 所提供的功能。 它的適用對象是**未透過 Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 取得授權**的使用者。  Azure MFA、 Azure AD Premium 和 EMS 包括 hello 完整版的 Azure MFA 的預設值。 如果您有授權，則不需要 Azure Multi-Factor Auth Provider。

Azure 多因素驗證提供者為必要的 toodownload hello SDK。

> [!IMPORTANT]
> toodownload hello SDK，您需要 toocreate Azure Multi-factor Auth 提供者，即使您的 Azure MFA、 AAD Premium 或 EMS 授權數量。  如果您針對此用途建立 Azure Multi-factor Auth 提供者，且已授權，可確定 toocreate hello 提供者以 hello**每個已啟用的使用者**模型。 然後，連結 hello 包含 hello Azure MFA、 Azure AD Premium 或 EMS 授權提供者 toohello 目錄。 此組態可確保，您才需要付費如果您有多個唯一的使用者執行雙步驟驗證比 hello 您所擁有的授權數目。

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>什麼是 Azure Multi-Factor Auth Provider？

如果您沒有授權的 Azure Multi-factor Authentication，您可以建立 auth 提供者 toorequire 雙步驟驗證為您的使用者。 如果您正在開發自訂應用程式，而且想 tooenable Azure MFA 時，會建立驗證提供者和[下載 hello SDK](multi-factor-authentication-sdk.md)。

有兩種類型的驗證提供者，且 hello 區別是解決您的 Azure 訂用帳戶收費的方式。 hello 驗證每個選項會計算 hello 驗證您的租用戶對執行中之月數。 如果您有許多使用者偶爾才會進行驗證，像是如果您要求 MFA 進行自訂應用程式，最好使用此選項。 hello 每位使用者選項計算執行中之月的雙步驟驗證您的租用戶中個人的 hello 的數目。 如果您已經擁有授權的某些使用者，但是需要 tooextend MFA toomore 使用者超出您的授權限制，最好使用此選項。

## <a name="create-a-multi-factor-auth-provider"></a>建立 Multi-Factor Auth Provider
使用下列步驟 toocreate Azure Multi-factor Auth 提供者的 hello。 只能在 hello Azure 傳統入口網站中建立 azure 的 Multi-factor Auth 提供者。 如果您無法登入 toohello Azure 傳統入口網站，檢查確定您的 Azure AD 租用戶是 toomake[與 Azure 訂用帳戶相關聯](../active-directory/active-directory-how-subscriptions-associated-directory.md)。 

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)身為系統管理員。
2. Hello 左側選取**Active Directory**。
3. 在 [hello Active Directory] 頁面上，在 hello 頂端，選取**Multi-factor Authentication 提供者**。
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. 在 hello 下方，按一下 **新增**。
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. 在 [應用程式服務] 之下，選取 [Multi-Factor Auth Provider]
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. 選取 [快速建立] 。
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. 填寫下列欄位的 hello，選取**建立**。
   1. **名稱**– hello hello Multi-factor Auth 提供者的名稱。
   2. **使用量模型** – 選擇兩個選項其中之一：
      * 每次驗證 – 購買依每次驗證付費的模式。 通常用於在取用者導向應用程式中使用 Azure Multi-factor Authentication 的案例。
      * 每個啟用的使用者 – 購買依每個啟用使用者付費的模式。 通常用於例如 Office 365 的員工存取 tooapplications。 如果某些使用者已擁有 Azure MFA 的授權，請選擇這個選項。
   3. **目錄**– hello Azure Active Directory 租用戶的多因素驗證提供者是與相關聯的 hello。 請注意下列 hello:
      * 您不需要 Azure AD 目錄 toocreate Multi-factor Auth 提供者。 這個方塊保留空白，如果您計劃只 toodownload hello Azure Multi-factor Authentication Server 或 SDK。
      * hello Multi-factor Auth 提供者必須是 hello 的 Azure AD 目錄 tootake 優點的進階功能與相關聯。
      * 只有一個 Multi-Factor Auth Provider 可以與任何一個 Azure AD 目錄相關聯。  
      ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. 一旦您按一下 建立，請建立多因素驗證提供者的 hello 和您應該會看到訊息指出：**已成功建立 Multi-factor Authentication 提供者**。 按一下 [確定] 。  
   
   ![建立 MFA Provider](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>管理 Multi-Factor Auth Provider

您無法變更 hello 使用量的 MFA 提供者建立之後，模型 （每個已啟用的使用者或驗證）。 不過，您可以刪除 hello MFA 提供者，然後建立一個具有不同的使用方式模型。

如果 hello 目前 Multi-factor Auth 提供者與相關聯的 Azure AD 目錄 （也稱為 Azure AD 租用戶），您就可以安全地刪除 hello MFA 提供者，並建立一個是連結的 toohello 相同的 Azure AD 租用戶。 或者，如果您購買足夠 MFA、 Azure AD Premium，或企業行動力 + 安全性 (EMS) 授權 toocover 所有使用者啟用 MFA，您可以完全刪除 hello MFA 提供者。

如果您的 MFA 提供者不是連結的 tooan Azure AD 租用戶，或連結 hello 新 MFA 提供者 tooa 不同的 Azure AD 租用戶、 使用者設定和組態選項不會傳送。 此外，現有的 Azure MFA 伺服器需要重新啟動使用透過產生啟用認證 toobe hello 新的 MFA 提供者。 重新啟動 hello MFA Server toolink 它們 toohello 新的 MFA 提供者不會影響通話和簡訊驗證，但通知將會停止運作的所有使用者，直到它們重新啟用 hello 行動應用程式的行動裝置應用程式。

## <a name="next-steps"></a>後續步驟

[下載多因素驗證 SDK hello](multi-factor-authentication-sdk.md)

[進行 Multi-Factor Authentication 設定](multi-factor-authentication-whats-next.md)
