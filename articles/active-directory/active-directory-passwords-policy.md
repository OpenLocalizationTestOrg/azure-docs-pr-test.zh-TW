---
title: "原則︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設原則選項"
services: active-directory
keywords: "Active directory 密碼管理, 密碼管理, Azure AD 自助式密碼重設"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a>密碼原則和 Azure Active Directory 中的限制

本文說明 hello 密碼原則和儲存在 Azure AD 租用戶的使用者帳戶相關聯的複雜性需求。

## <a name="administrator-password-policy-differences"></a>系統管理員密碼原則差異

Microsoft 會對任何系統管理員角色 (全域管理員、技術支援系統管理員、密碼管理員等) 強制執行強式預設「雙閘道」密碼重設原則

這會停用系統管理員使用安全性問題，並強制執行 hello 下列。

兩個控制原則，需要這兩項驗證資料 (電子郵件地址**和**電話號碼)，適用於下列情況下的 hello

* 所有的 Azure 系統管理員角色
  * 服務台系統管理員
  * 服務支援管理員
  * 計費管理員
  * 合作夥伴第 1 層支援
  * 合作夥伴第 2 層支援
  * Exchange 服務管理員
  * Lync 服務管理員
  * 使用者帳戶管理員
  * 目錄撰寫者
  * 全域管理員/公司系統管理員
  * SharePoint 服務管理員
  * 規範管理員
  * 應用程式系統管理員
  * 安全性系統管理員
  * 特殊權限角色管理員
  * Intune 服務管理員
  * 應用程式 Proxy 服務管理員
  * CRM 服務管理員
  * Power BI 服務管理員
  
* 試用已經過 30 天**或**
* 虛名網域存在於 (contoso.com) **或**
* Azure AD Connect 正在同步處理內部部署目錄中的身分識別

### <a name="exceptions"></a>例外狀況
單一閘道原則，需要一段驗證資料 (電子郵件地址**或**電話號碼)，適用於下列情況下的 hello

* 試用的前 30 天**或**
* 虛名網域不存在 (*.onmicrosoft.com) **且** Azure AD Connect 並未同步處理身分識別


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a>適用於 tooall 使用者帳戶的 UserPrincipalName 原則

需要 toosign tooAzure AD 中的每個使用者帳戶必須具有與帳戶相關聯的唯一使用者主要名稱 (UPN) 屬性值。 hello 表概述 hello 原則適用於 tooboth 內部部署 Active Directory 使用者帳戶同步處理 toohello 雲端和 toocloud 僅限使用者帳戶。

| 屬性 | UserPrincipalName 需求 |
| --- | --- |
| 允許的字元 |<ul> <li>A – Z</li> <li>a - z</li><li>0 – 9</li> <li> 。 - \_ ! \# ^ \~</li></ul> |
| 不允許的字元 |<ul> <li>任何 ' @' 不區隔 hello hello 網域的使用者名稱的字元。</li> <li>不能包含句號字元 '。 '正前面的 hello' @' 符號</li></ul> |
| 長度限制 |<ul> <li>總長度不得超過 113 個字元</li><li>hello 前的 64 個字元 ' @' 符號</li><li>在 hello 後的 48 個字元 ' @' 符號</li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a>適用於 toocloud 使用者帳戶的密碼原則

hello 下表描述可為套用的 toouser 帳戶所建立及管理 Azure AD 中的 hello 密碼原則設定。

| 屬性 | 需求 |
| --- | --- |
| 允許的字元 |<ul><li>A – Z</li><li>a - z</li><li>0 – 9</li> <li>@ # $ % ^ & * - _ ! + = [ ] { } &#124; \ : ‘ , . ? / ` ~ “ ( ) ;</li></ul> |
| 不允許的字元 |<ul><li>Unicode 字元</li><li>空格</li><li> **強式密碼只**： 不能包含點字元 '。 '正前面的 hello' @' 符號</li></ul> |
| 密碼限制 |<ul><li>最少 8 個字元，最多 16 個字元</li><li>**強式密碼只**： 需要 3，4 hello 以下的：<ul><li>小寫字元</li><li>大寫字元</li><li>數字 (0-9)</li><li>符號 (請參閱上面的密碼限制)</li></ul></li></ul> |
| 密碼到期時間 |<ul><li>預設值：**90** 天 </li><li>值為可使用 hello Set-msolpasswordpolicy cmdlet 從 hello Azure Active Directory 的 Windows PowerShell 模組設定。</li></ul> |
| 密碼到期通知 |<ul><li>預設值：**14** 天 (密碼到期之前)</li><li>值為可使用 hello Set-msolpasswordpolicy cmdlet 設定。</li></ul> |
| 密碼到期 |<ul><li>預設值︰**false** 天 (表示已啟用密碼到期) </li><li>值可以設定為使用 hello Set-msoluser 指令程式的個別使用者帳戶。 </li></ul> |
| 密碼**變更**歷程記錄 |**變更**密碼時，**無法**再次使用上次的密碼。 |
| 密碼**重設**歷程記錄 | **重設**遺忘的密碼時，**可以**再次使用上次的密碼。 |
| 帳戶鎖定 |10 失敗登入嘗試之後 （錯誤密碼），請花一分鐘鎖定 hello 使用者。 不正確的登入嘗試鎖定 hello 使用者增加持續時間。 |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a>在 Azure Active Directory 中設定密碼到期原則

Microsoft 雲端服務的全域系統管理員可以使用使用者密碼不 tooexpire hello Microsoft Azure Active Directory 的 Windows PowerShell 模組 tooset。 您也可以使用 Windows PowerShell cmdlet tooremove hello 永不過期的設定或 toosee 不 tooexpire 設定哪些使用者密碼。 本指南適用於 tooother 提供者，例如 Microsoft Intune 和 Office 365 也依賴 Microsoft Azure Active Directory 身分識別和目錄服務。

> [!NOTE]
> 只有密碼 toonot 可以設定未透過目錄同步作業同步處理的使用者帳戶到期。 如需有關目錄同步作業，請參閱 [Connect AD 與 Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。
>
>

## <a name="set-or-check-password-policies-using-powershell"></a>使用 PowerShell 設定或檢查密碼原則

tooget 開始，您需要太[下載並安裝 hello Azure AD PowerShell 模組](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)。 一旦您已經安裝，您可以依照下列 tooconfigure hello 步驟是每個欄位。

### <a name="how-toocheck-expiration-policy-for-a-password"></a>如何 toocheck 密碼到期原則
1. 連接 tooWindows PowerShell 中使用您的公司系統管理員認證。
2. 執行下列其中一個 hello 下列命令：

   * toosee 單一使用者的密碼是否設定 toonever 過期，請執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello (例如， aprilr@contoso.onmicrosoft.com) 或 hello 使用者識別碼的 hello 使用者想要 toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`
   * toosee hello 所有使用者的 [密碼永久有效] 設定，請執行下列 cmdlet 的 hello:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`

### <a name="set-a-password-tooexpire"></a>設定密碼 tooexpire

1. 連接 tooWindows PowerShell 中使用您的公司系統管理員認證。
2. 執行下列其中一個 hello 下列命令：

   * 某位使用者的 tooset hello 密碼，以便讓 hello 密碼已過期，執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello 或 hello hello 使用者的使用者識別碼：`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`
   * hello 組織中所有使用者的 tooset hello 密碼，讓它們過期時，使用下列 cmdlet 的 hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`

### <a name="set-a-password-toonever-expire"></a>將密碼 toonever 過期

1. 連接 tooWindows PowerShell 中使用您的公司系統管理員認證。
2. 執行下列其中一個 hello 下列命令：

   * 一位使用者 toonever tooset hello 密碼過期，執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello 或 hello hello 使用者的使用者識別碼：`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`
   * 所有 hello 中的使用者組織 toonever tooset hello 密碼過期，請執行下列 cmdlet 的 hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR
