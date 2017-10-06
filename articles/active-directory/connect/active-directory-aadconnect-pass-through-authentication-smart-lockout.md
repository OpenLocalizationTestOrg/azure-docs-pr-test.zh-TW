---
title: "Azure AD Connect：傳遞驗證 - 智慧鎖定 | Microsoft Docs"
description: "本文章說明 Azure Active Directory (Azure AD) 的傳遞驗證如何在內部部署帳戶防止暴力密碼破解攻擊 hello 雲端中。"
services: active-directory
keywords: "Azure AD Connect 傳遞驗證, 安裝 Active Directory, Azure AD 的必要元件, SSO, 單一登入"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a>Azure Active Directory 傳遞驗證：智慧鎖定

## <a name="overview"></a>概觀

Azure AD 可防範暴力密碼破解攻擊，並防止正版使用者遭到其 Office 365 和 SaaS 應用程式鎖定而無法使用應用程式。 當您使用傳遞驗證來作為登入方法時，系統便支援這項稱為**智慧鎖定**的功能。 智慧鎖定預設會啟用所有租用戶和要保護所有的 hello 時間; 您的使用者帳戶沒有任何需要 tooturn 其上。

智慧鎖定在運作時，會追蹤失敗的登入嘗試，並在經過一定的**鎖定閾值**後，開始**鎖定期間**。 從 hello 攻擊者在 hello 鎖定持續時間期間的任何登入嘗試會遭到拒絕。 如果仍繼續 hello 攻擊，hello 後續失敗登入嘗試 hello 鎖定持續時間結束導致較長鎖定持續時間。

>[!NOTE]
>hello 預設鎖定閾值為 10 的失敗的嘗試和 hello 預設鎖定持續時間為 60 秒。

智慧鎖定也會區別登入從正版的使用者和攻擊者和出 hello 攻擊者在大部分情況下只鎖定。 這項功能可防止攻擊者惡意地讓使用者遭到鎖定。 我們會使用過去的登入的行為，使用者的裝置和瀏覽器和其他正版的使用者和攻擊者之間的信號 toodistinguish。 我們會持續改善我們的演算法。

傳遞驗證轉送到您在內部部署 Active Directory (AD) 的密碼驗證要求，因為您需要 tooprevent 攻擊者鎖定您的使用者的 AD 帳戶。 由於您自己的 AD 帳戶鎖定原則 (特別是， [**帳戶鎖定閾值**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx)和[**重設帳戶鎖定計數器後原則** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx))，需要 tooconfigure Azure AD 的鎖定閾值，以及鎖定持續時間值適當地 toofilter 出攻擊 hello 雲端中才能到達您內部部署 AD。

>[!NOTE]
>hello 智慧鎖定功能免費而_上_依預設，所有客戶。 不過，修改 Azure AD 的鎖定 」 臨界值和使用 Graph API 的鎖定持續時間值需要您的租用戶 toohave 至少一個 Azure AD Premium P2 授權。 您不需要有 Azure AD Premium P2 授權_每位使用者_tooget hello 智慧鎖定功能，透過通過驗證。

保護 tooensure，您的使用者內部部署 AD 帳戶，您需要 tooensure 的：

1.  Azure AD 的鎖定閾值「小於」AD 的帳戶鎖定閾值。 我們建議您設定 hello 值，使 AD 的帳戶鎖定閾值是至少兩個或三次 Azure AD 的鎖定 」 臨界值。
2.  Azure AD 的鎖定期間 (以秒來表示) 比 AD 的下列時間過後重設帳戶鎖定計數器 (以分鐘來表示)「還久」。

## <a name="verify-your-ad-account-lockout-policies"></a>驗證 AD 帳戶鎖定原則

使用下列指示 tooverify hello AD 帳戶鎖定原則：

1.  開啟 hello 群組原則管理工具。
2.  編輯 hello 的群組原則是套用的 tooall 使用者，例如 hello 預設網域原則。
3.  瀏覽 tooComputer 原則 \windows 設定 \ 安全性帳戶原則 \ 帳戶鎖定原則。
4.  確認 [帳戶鎖定閾值] 和 [下列時間過後重設帳戶鎖定計數器] 的值。

![AD 帳戶鎖定原則](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a>使用您的租用戶智慧鎖定值 hello Graph API toomanage

>[!IMPORTANT]
>使用圖形 API 來修改 Azure AD 的鎖定閾值和鎖定期間值是 Azure AD Premium P2 的功能。 它也需要 toobe 上您的租用戶的全域系統管理員。

您可以使用[圖表總管](https://developer.microsoft.com/graph/graph-explorer)tooread，設定和更新 Azure AD 的智慧鎖定值。 但您也可以透過程式設計的方式進行這些作業。

### <a name="read-smart-lockout-values"></a>讀取智慧鎖定值

請遵循這些步驟 tooread 租用戶的智慧鎖定值：

1. 以租用戶全域管理員的身分登入 Graph 總管。 如果出現提示，hello 授與存取權要求的權限。
2. 按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。
3. 設定 hello Graph API 要求，如下所示： Set 版本太"BETA"，要求類型太 「 取得 」 和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`。
4. 按一下"執行查詢"toosee 租用戶的智慧鎖定值。 如果您之前從未設定過租用戶的值，您會看到空白的設定。

### <a name="set-smart-lockout-values"></a>設定智慧鎖定值

請遵循這些步驟 tooset （適用於 hello 只有第一次) 的租用戶的智慧鎖定值：

1. 以租用戶全域管理員的身分登入 Graph 總管。 如果出現提示，hello 授與存取權要求的權限。
2. 按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。
3. 設定 hello Graph API 要求，如下所示： Set 版本太"BETA"，要求類型太"POST"和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`。
4. 複製並貼上下列 JSON 要求到 hello 「 要求內文 」 欄位的 hello。 變更為適當的 hello 智慧鎖定值，並使用的隨機 GUID `templateId`。
5. 按一下"執行查詢"tooset 租用戶的智慧鎖定值。

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
>如果您不使用它們，您可以將 hello **BannedPasswordList**和**EnableBannedPasswordCheck**值，則為空白 ("") 和"false"分別。

確認您是否已使用[這些步驟](#read-smart-lockout-values)正確地設定租用戶的智慧鎖定值。

### <a name="update-smart-lockout-values"></a>更新智慧鎖定值

遵循這些步驟 tooupdate 租用戶的智慧鎖定值 （如果您已經設定過他們的）：

1. 以租用戶全域管理員的身分登入 Graph 總管。 如果出現提示，hello 授與存取權要求的權限。
2. 按一下 「 修改 」 權限 」，然後選取 hello"Directory.ReadWrite.All 」 權限。
3. [您的租用戶智慧鎖定值，請遵循這些步驟 tooread](#read-smart-lockout-values)。 複製 hello `id` "displayName"為"PasswordRuleSettings"hello 項目的數值 (GUID)。
4. 設定 hello Graph API 要求，如下所示： 將版本設定為太"BETA"，太要求類型 「 修補 」 和 URL 太`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>`-使用 hello GUID，如步驟 3 `<id>`。
5. 複製並貼上下列 JSON 要求到 hello 「 要求內文 」 欄位的 hello。 變更為適當的 hello 智慧鎖定值。
6. 按一下"執行查詢"tooupdate 租用戶的智慧鎖定值。

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

確認您是否已使用[這些步驟](#read-smart-lockout-values)正確地更新租用戶的智慧鎖定值。

## <a name="next-steps"></a>後續步驟
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
