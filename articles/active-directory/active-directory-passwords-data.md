---
title: "Azure AD SSPR 資料需求 | Microsoft Docs"
description: "資料需求的 Azure AD 自助式密碼重設以及 toosatisfy 它們"
services: active-directory
keywords: 
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a>部署密碼重設而不需要使用者註冊

部署自助密碼重設 (SSPR) 需要驗證資料 toobe 存在。 某些組織有使用者輸入他們的驗證資料本身，但許多組織都希望 toosynchronize 與 Active Directory 中的現有資料。 如果您已正確地格式化資料在內部部署目錄中，並設定[使用快速設定的 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)，資料由可用 tooAzure AD 和 SSPR 與不需要使用者互動。

任何電話號碼必須是在 hello 格式 + CountryCode PhoneNumber 範例: + 1 4255551234 toowork 正確。

> [!NOTE]
> 密碼重設不支援電話分機。 即使在 hello + 1 4255551234 X 12345 格式 hello 呼叫開始之前，會移除延伸模組。

## <a name="fields-populated"></a>填入的欄位

如果您使用下列 Azure AD Connect hello 中的 hello 預設設定建立對應。

| 內部部署 AD | Azure AD | Azure AD 驗證的連絡資訊 |
| --- | --- | --- |
| telephoneNumber | 辦公室電話 | 備用手機 |
| mobile | 行動電話 | 電話 |


## <a name="security-questions-and-answers"></a>安全性問題和答案

安全性問題和答案會安全地儲存在 Azure AD 租用戶和是透過 hello 只存取 toousers [SSPR 註冊入口網站](https://aka.ms/ssprsetup)。 系統管理員無法看到或修改其他使用者的問題和答案 hello 內容。

### <a name="what-happens-when-a-user-registers"></a>使用者註冊時的情況

當使用者註冊時，hello 註冊] 頁面上設定下列欄位的 hello:

* 驗證電話
* 驗證電子郵件
* 安全性問題和答案

如果您提供的值**行動電話**或**備用電子郵件**，使用者可以立即使用這些值 tooreset 他們的密碼，即使它們尚未註冊 hello 服務。 此外，使用者 hello 註冊第一次，請參閱這些值，而且如果他們想加以修改。 成功註冊之後，這些值將會保存在 hello**驗證電話**和**驗證電子郵件**分別欄位。

## <a name="set-and-read-authentication-data-using-powershell"></a>使用 PowerShell 設定和讀取驗證資料

可以使用 PowerShell 來設定下列欄位的 hello

* 替代電子郵件
* 行動電話
* 辦公室電話 - 只有在未與內部部署目錄同步處理時才能設定

### <a name="using-powershell-v1"></a>使用 PowerShell V1

tooget 開始，您需要太[下載並安裝 hello Azure AD PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)。 一旦您已經安裝，您可以依照每個欄位，請遵循 tooconfigure 的 hello 步驟。

#### <a name="set-authentication-data-with-powershell-v1"></a>使用 PowerShell V1 設定驗證資料

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a>使用 PowerShellPowerShell V1 讀取驗證資料

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a>驗證電話驗證電子郵件可以只讀取和使用 Powershell V1 使用 hello 命令後面

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a>使用 PowerShell V2

tooget 開始，您需要太[下載並安裝 Azure AD V2 hello PowerShell 模組](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)。 一旦您已經安裝，您可以依照每個欄位，請遵循 tooconfigure 的 hello 步驟。

快速從最新版本的 PowerShell 支援 Find-module、 install-module tooinstall 執行這些命令 （hello 第一行只檢查 toosee 如果安裝的話）：

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a>使用 PowerShell V2 設定驗證資料

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a>使用 PowerShell V2 讀取驗證資料

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a>後續步驟

hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊

* [**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理 
* [**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權
* [**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱
* [**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。
* [**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則
* [**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能
* [**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式
* [**常見問題集**](active-directory-passwords-faq.md) - 如何？ 原因為何？ 何事？ 何地？ 何人？ 何時？ -回答您總是想 tooask tooquestions
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR
