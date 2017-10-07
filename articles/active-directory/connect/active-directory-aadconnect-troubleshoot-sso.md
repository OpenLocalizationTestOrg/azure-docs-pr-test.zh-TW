---
title: "Azure AD Connect：針對無縫單一登入進行疑難排解 | Microsoft Docs"
description: "本主題描述如何 tootroubleshoot Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO)。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>針對 Azure Active Directory 無縫單一登入進行疑難排解

這篇文章可協助您尋找有關 Azure AD 無縫單一登入常見問題的疑難排解資訊。

## <a name="known-issues"></a>已知問題

- 如果您正在同步處理 30 個或更多的 AD 樹系，您無法使用 Azure AD Connect 啟用無縫 SSO。 因應措施，您可以[手動啟用](#manual-reset-of-azure-ad-seamless-sso)hello 在租用戶的功能。
- 加入 Azure AD 服務 Url （https://autologon.microsoftazuread-sso.com、 https://aadg.windows.net.nsatc.net） toohello 「 信任的網站 」 區域而不是 hello 「 近端內部網路 」 區域**封鎖使用者登入**。
- 無縫 SSO 無法在 Firefox 和 Edge 的私人瀏覽模式中運作。 此外當「增強保護」模式開啟時，Internet Explorer 也是如此。

>[!IMPORTANT]
>我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。

## <a name="check-status-of-hello-feature"></a>Hello 功能的核取狀態

請確定該 hello 無縫式 SSO 的功能仍然是**啟用**在租用戶。 您可以查看狀態移 toohello **Azure AD Connect**刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>登入失敗的原因，在 hello Azure Active Directory 系統管理中心

使用者登入的問題疑難排解無縫式 SSO 的好地方 toostart 是在 hello toolook[登入活動報表](../active-directory-reporting-activity-sign-ins.md)上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-sso/sso9.png)

瀏覽過**Azure Active Directory** -> **登入**上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)，按一下 特定使用者的登入活動。 尋找 hello**登入錯誤碼**欄位。 對應欄位 tooa 失敗的原因和解決使用下表中的 hello 的 hello 的值：

|登入錯誤碼|登入失敗原因|解決方案
| --- | --- | ---
| 81001 | 使用者的 Kerberos 票證太大。 | 降低使用者的群組成員資格，並再試一次。
| 81002 | 無法 toovalidate 使用者的 Kerberos 票證。 | 請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。
| 81003 | 無法 toovalidate 使用者的 Kerberos 票證。 | 請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。
| 81004 | Kerberos 驗證嘗試失敗。 | 請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。
| 81008 | 無法 toovalidate 使用者的 Kerberos 票證。 | 請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。
| 81009 | 「 無法 toovalidate 使用者的 Kerberos 票證。 | 請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。
| 81010 | 無縫式 SSO 失敗，因為 hello 使用者的 Kerberos 票證已過期或無效。 | 使用者必須從加入網域的裝置，您公司網路內部的 toosign 中。
| 81011 | 無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。 | 使用 Azure AD 到 Azure AD Connect toosynchronize 使用者資訊。
| 81012 | 嘗試 toosign tooAzure AD 中的 hello 使用者所登入 hello 裝置 hello 使用者不同。 | 從不同的裝置登入。
| 81013 | 無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。 |使用 Azure AD 到 Azure AD Connect toosynchronize 使用者資訊。 

## <a name="troubleshooting-checklist"></a>疑難排解檢查清單

使用下列檢查清單 tootroubleshoot 無縫式 SSO 所發出的 hello:

- 請檢查是否已在 Azure AD Connect 啟用 hello 無縫式 SSO 功能。 如果您無法啟用 hello 功能 （例如，由於 tooa 封鎖連接埠），請確定您有所有的 hello[先決條件](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites)備妥。
- 請檢查這兩個 Azure AD Url （https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net） 是否是 hello 使用者的內部網路區域設定的一部分。
- 確認 hello 公司的裝置已加入的 toohello AD 網域。
- 請確定 hello 使用者登入 toohello 裝置使用的 AD 網域帳戶。
- 請確認 hello 使用者帳戶來自已無縫式 SSO 的 AD 樹系設定。
- 確認 hello 裝置 hello 公司網路上連線。
- 請確認 hello 裝置時間的 hello Active Directory 的和 hello 網域控制站的時間同步相差五分鐘內。
- 列出現有的 Kerberos 票證 hello 裝置上使用 hello **klist**命令從命令提示字元。 檢查是否 hello 發出票證`AZUREADSSOACCT`電腦帳戶會出現。 使用者的 Kerberos 票證有效期通常為 12 個小時。 您的 Active Directory 可能有不同的設定。
- 清除現有的 Kerberos 票證 hello 透過從裝置 hello **klist 清除**命令，並再試一次。
- toodetermine 是否有 JavaScript 相關問題，檢閱 hello hello 瀏覽器 （在 [開發人員工具）] 下的主控台記錄檔。
- 檢閱 hello[網域控制站記錄](#domain-controller-logs)以及。

### <a name="domain-controller-logs"></a>網域控制站記錄

如果成功稽核已啟用您的網域控制站上，然後每次使用者登入時使用無縫式 SSO 的安全性項目會記錄在 hello 事件記錄檔。 您可以找到使用下列查詢的 hello 這些安全性事件 (請查看事件**4769** hello 電腦帳戶相關聯**AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>手動重設的 hello 功能

如果疑難排解沒有幫助，可以在租用戶的手動重設 hello 功能。 執行 Azure AD Connect 的情況下遵循 hello 在內部部署伺服器上的下列步驟：

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>步驟 1： 匯入 hello 無縫式 SSO 的 PowerShell 模組

1. 首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。
2. 請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。
3. 瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。
4. 使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>步驟 2： 取得 AD 樹系啟用無縫式 SSO 的 hello 清單

1. 以系統管理員身分執行 PowerShell。 在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。 出現提示時，輸入您租用戶的全域管理員認證。
2. 呼叫 `Get-AzureADSSOStatus`。 這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>步驟3：針對已設定無縫 SSO 的每個 AD 樹系停用該功能

1. 呼叫 `$creds = Get-Credential`。 出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。
2. 呼叫 `Disable-AzureADSSOForest -OnPremCredentials $creds`。 此命令會移除 hello `AZUREADSSOACCT` hello 電腦帳戶在內部部署網域控制站為此特定的 AD 樹系。
3. 重複上述步驟設定好 hello 功能每個 AD 樹系的 hello。

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>步驟 4：為每個 AD 樹系啟用無縫 SSO

1. 呼叫 `Enable-AzureADSSOForest`。 出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。
2. 重複上述步驟，每個 AD 樹系上您想要向上 hello 功能 tooset hello。

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>步驟 5。 啟用在租用戶的 hello 功能

呼叫`Enable-AzureADSSO` 並輸入"true"，在 hello`Enable: `提示 tooturn 租用戶中的 hello 功能。
