---
title: "Azure AD Connect：針對傳遞驗證進行疑難排解 | Microsoft Docs"
description: "本文說明如何 tootroubleshoot Azure Active Directory (Azure AD) 的傳遞驗證。"
services: active-directory
keywords: "針對 Azure AD Connect 傳遞驗證進行疑難排解, 安裝 Active Directory, Azure AD, SSO, 單一登入的必要元件"
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
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>針對 Azure Active Directory 傳遞驗證進行疑難排解

這篇文章可協助您尋找有關 Azure AD 傳遞驗證常見問題的疑難排解資訊。

>[!IMPORTANT]
>如果您所面對的使用者登入使用傳遞驗證問題，不會停用 hello 功能，或解除安裝傳遞驗證代理程式，而不需僅限雲端的全域管理員帳戶 toofall 回到上。 了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。 這是確保您不會被租用戶封鎖的關鍵步驟。

## <a name="general-issues"></a>一般問題

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>檢查 hello 功能與驗證代理程式狀態

確定該 hello 傳遞驗證功能仍然**啟用**驗證代理程式的租用戶和 hello 狀態顯示**Active**，而非**非作用中**。 您可以查看狀態移 toohello **Azure AD Connect**刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>使用者看到的登入錯誤訊息

如果無法使用傳遞驗證 toosign hello 使用者，他們可能會看到 hello 下列使用者面向錯誤 hello Azure AD 登入畫面上的其中一個： 

|錯誤|說明|解決方案
| --- | --- | ---
|AADSTS80001|無法 tooconnect tooActive 目錄|請確認代理程式伺服器 hello 相同 AD 樹系的成員以其密碼需要驗證的 toobe hello 使用者都能 tooconnect tooActive 目錄。  
|AADSTS8002|發生連接 tooActive 目錄逾時。|請檢查 Active Directory 可用，而且從 hello 代理程式回應 toorequests tooensure。
|AADSTS80004|hello 傳遞 toohello 代理程式的使用者名稱無效。|請確定 hello 使用者嘗試 toosign 入 hello 正確的使用者名稱。
|AADSTS80005|驗證發生無法預期的 WebException|暫時性錯誤。 重試 hello 要求。 如果持續 toofail，請連絡 Microsoft 支援服務。
|AADSTS80007|和 Active Directory 通訊時發生錯誤|請檢查 hello 代理程式記錄檔，如需詳細資訊，並確認 Active Directory 皆如預期般運作。

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>登入失敗的原因，在 hello Azure Active Directory 系統管理中心

啟動使用者登入問題疑難排解藉由查看 hello[登入活動報表](../active-directory-reporting-activity-sign-ins.md)上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

瀏覽過**Azure Active Directory** -> **登入**上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)，按一下 特定使用者的登入活動。 尋找 hello**登入錯誤碼**欄位。 對應欄位 tooa 失敗的原因和解決使用下表中的 hello 的 hello 的值：

|登入錯誤碼|登入失敗原因|解決方案
| --- | --- | ---
| 50144 | 使用者的 Active Directory 密碼已到期。 | 重設您的內部部署 Active Directory 中的 hello 使用者的密碼。
| 80001 | 沒有可用的驗證代理程式。 | 安裝並註冊驗證代理程式。
| 80002 | 驗證代理程式的密碼驗證要求已逾時。 | 檢查是否可以從 hello 驗證代理程式連線到您的 Active Directory。
| 80003 | 驗證代理程式收到無效的回應。 | 如果 hello 問題一致地重現跨多個使用者，請檢查您的 Active Directory 設定。
| 80004 | 登入要求中使用的使用者主體名稱 (UPN) 不正確。 | 要求 hello 使用者 toosign 入 hello 正確的使用者名稱。
| 80005 | 驗證代理程式：發生錯誤。 | 暫時性錯誤。 請稍後再試。
| 80007 | 驗證代理程式無法 tooconnect tooActive 目錄。 | 檢查是否可以從 hello 驗證代理程式連線到您的 Active Directory。
| 80010 | 驗證代理程式無法 toodecrypt 密碼。 | 如果 hello 問題是一致地重現問題，請安裝並註冊新的驗證代理程式。 然後解除安裝目前的 hello。 
| 80011 | 驗證代理程式無法 tooretrieve 解密金鑰。 | 如果 hello 問題是一致地重現問題，請安裝並註冊新的驗證代理程式。 然後解除安裝目前的 hello。

## <a name="authentication-agent-installation-issues"></a>驗證代理程式安裝問題

### <a name="an-unexpected-error-occurred"></a>發生意外的錯誤

[收集代理程式記錄檔](#collecting-pass-through-authentication-agent-logs)從 hello 伺服器以及與您的問題，請連絡 Microsoft 支援服務。

## <a name="authentication-agent-registration-issues"></a>驗證代理程式註冊問題

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Hello 驗證代理程式註冊失敗，因為 tooblocked 連接埠

請驗證代理程式已安裝哪些 hello 該 hello 伺服器可與我們的服務 Url 和連接埠的列通訊[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)。

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Hello 驗證代理程式註冊失敗，因為 tootoken 或帳戶授權錯誤

請確定您在所有 Azure AD Connect 或獨立驗證代理程式安裝和註冊作業中，使用僅限雲端的全域管理員帳戶。 沒有啟用 MFA 的全域管理員帳戶; 的已知的問題因應措施關閉暫時 MFA （只有 toocomplete hello 作業）。

### <a name="an-unexpected-error-occurred"></a>發生意外的錯誤

[收集代理程式記錄檔](#collecting-pass-through-authentication-agent-logs)從 hello 伺服器以及與您的問題，請連絡 Microsoft 支援服務。

## <a name="authentication-agent-uninstallation-issues"></a>驗證代理程式解除安裝問題

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>解除安裝 Azure AD Connect 時出現的警告訊息

如果您有在租用戶啟用傳遞驗證，而且您嘗試 toouninstall Azure AD Connect，它就會顯示您 hello 下列警告訊息: 「 使用者並不會無法 toosign 中 tooAzure AD 除非有其他的傳遞驗證代理程式其他伺服器上安裝。 」

請確定您的設定不[高可用](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)才能解除安裝 Azure AD Connect tooavoid 中斷使用者登入。

## <a name="issues-with-enabling-hello-feature"></a>啟用 「 hello 」 功能的問題

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>啟用 「 hello 」 功能失敗，因為沒有任何驗證代理程式

您需要 toohave 至少一個作用中驗證代理程式 」 tooenable 傳遞驗證您的租用戶上。 您可以安裝 Azure AD Connect 或獨立的驗證代理程式，來安裝驗證代理程式。

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>啟用 「 hello 」 功能失敗，因為 tooblocked 連接埠

確認已安裝的 Azure AD Connect 該 hello 伺服器能與我們的服務 Url 和連接埠的列通訊[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)。

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>啟用 「 hello 」 功能失敗，因為 tootoken 或帳戶授權錯誤

請啟用 「 hello 」 功能時，使用僅限雲端的全域管理員帳戶。 使用 multi-factor authentication (MFA) 的已知問題-啟用全域系統管理員帳戶。因應措施關閉暫時 MFA （只有 toocomplete hello 作業）。

## <a name="exchange-activesync-configuration-issues"></a>Exchange ActiveSync 設定問題

當您設定 Exchange ActiveSync 支援通過驗證時，這些是 hello 常見的問題。

### <a name="exchange-powershell-issue"></a>Exchange PowerShell 問題

如果您看到 hello"**參數找不到符合的參數名稱 'PerTenantSwitchToESTSEnabled'\.**" 當您執行 hello 錯誤`Set-OrganizationConfig`Exchange PowerShell 命令，請連絡 Microsoft 支援。

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync 未運作

hello 設定生效，某些時間 tootake-hello 取決於您環境的時間週期。 如果 hello 情況持續發生一段時間，請連絡 Microsoft 支援服務。

## <a name="collecting-pass-through-authentication-agent-logs"></a>收集傳遞驗證代理程式記錄

根據 hello 類型您可能有的問題，您會需要在不同的地方 toolook 傳遞驗證代理程式記錄檔。

### <a name="authentication-agent-event-logs"></a>驗證代理程式事件記錄檔

是否有錯誤相關 toohello 驗證代理程式，開啟 hello hello 伺服器上事件檢視器應用程式，並檢查下**應用程式和服務 Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**。

進行詳細分析，啟用 hello 「 工作階段 」 記錄檔。 不正常的作業; 期間啟用此記錄檔以執行 hello 驗證代理程式使用此選項只有在進行疑難排解。 已再次停用 hello 記錄之後，才會顯示 hello 記錄內容。

### <a name="detailed-trace-logs"></a>詳細的追蹤記錄檔

追蹤記錄檔，尋找 tootroubleshoot 使用者登入失敗， **%programdata%\Microsoft\Azure AD 連線驗證 Agent\Trace\\**。 這些記錄檔包含在特定使用者登入失敗的原因使用 hello 傳遞驗證功能的原因。 這些錯誤也會顯示 hello 上述對應的 toohello 登入失敗原因[資料表](#sign-in-failure-reasons-on-the-Azure-portal)。 以下是記錄項目範例：

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

您可以藉由開啟 hello 命令提示字元並執行下列命令的 hello 取得 hello 錯誤 (hello 前面範例中為 ' 1328') 的敘述性的詳細資料 (附註: '1328' 取代為您在記錄中看到的 hello 實際的錯誤號碼):

`Net helpmsg 1328`

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>網域控制站記錄

如果已啟用稽核記錄，其他資訊可以找到網域控制站的 hello 安全性記錄檔中。 簡單的方式 tooquery 登入傳送的要求傳遞驗證代理程式如下所示：

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>效能監視器計數器

另一個方式 toomonitor 驗證代理程式是 tootrack 特定的效能監視器計數器 hello 驗證代理程式安裝所在的每個伺服器上。 下列全域計數器使用 hello (**# PTA 驗證**， **#PTA 失敗驗證**和**#PTA 成功驗證**) 和錯誤計數器 (**# PTA 驗證錯誤**):

![傳遞驗證效能監視器計數器](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>傳遞驗證使用多個驗證代理程式，且_不_進行負載平衡，而提供了高可用性。 視您的設定而定，_並非_所有的驗證代理程式都會收到數目大約_相同_的要求。 特定的驗證代理程式可能完全不會收到流量。
