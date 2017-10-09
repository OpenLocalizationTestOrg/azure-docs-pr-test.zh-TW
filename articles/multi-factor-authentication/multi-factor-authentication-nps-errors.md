---
title: "hello Azure MFA NPS 擴充 aaaTroubleshoot 錯誤碼 |Microsoft 文件"
description: "如需協助解決問題的 hello NPS 擴充功能的 Azure Multi-factor Authentication，與特定解決方案的常見錯誤訊息"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>針對 Azure Multi-factor Authentication 解決 hello NPS 擴充功能中的錯誤訊息

如果您遇到錯誤 hello NPS 擴充功能的 Azure Multi-factor authentication 時，使用此發行項 tooreach 解析度更快。 

## <a name="troubleshooting-steps-for-common-errors"></a>為常見錯誤而設的疑難排解步驟

| 錯誤碼 | 疑難排解步驟 |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [請連絡支援人員](#contact-microsoft-support)，並提供 hello 收集記錄檔的步驟清單。 提供詳細資訊，您可能需 hello 發生錯誤，包括租用戶識別碼，以及使用者主要名稱 (UPN) 之前發生什麼事。 |
| **CLIENT_CERT_INSTALL_ERROR** | 可能有如何 hello 用戶端憑證已安裝，或與您的租用戶相關聯的問題。 請依照下列中的 hello 指示[疑難排解 hello MFA NPS 擴充](multi-factor-authentication-nps-extension.md#troubleshooting)tooinvestigate 用戶端憑證問題。 |
| **ESTS_TOKEN_ERROR** | 請依照下列中的 hello 指示[疑難排解 hello MFA NPS 擴充](multi-factor-authentication-nps-extension.md#troubleshooting)tooinvestigate 用戶端憑證，ADAL 權杖的問題。 |
| **HTTPS_COMMUNICATION_ERROR** | 從 Azure MFA 無法 tooreceive 回應 hello NPS 伺服器。 確認您的防火牆的流量 tooand 從 https://adnotifications.windowsazure.com 開啟之間雙向 |
| **HTTP_CONNECT_ERROR** | 在 hello 執行 hello NPS 擴充功能的伺服器，確認 https://adnotifications.windowsazure.com 而 https://login.microsoftonline.com/ 可以到達。 如果無法載入這些站台，請針對該伺服器上的連線進行移難排解。 |
| **REGISTRY_CONFIG_ERROR** | 遺漏金鑰 hello hello 應用程式，這可能是因為登錄中 hello [PowerShell 指令碼](multi-factor-authentication-nps-extension.md#install-the-nps-extension)未在安裝後執行。 hello 錯誤訊息應該包含 hello 遺失索引鍵。 請確定您擁有 hello 金鑰 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa 底下。 |
| **REQUEST_FORMAT_ERROR** <br> RADIUS 要求中遺失必要的 RADIUS 使用者名稱\識別碼。請確定 NPS 會收到 RADIUS 要求 | 此錯誤通常反映的是安裝問題。 hello NPS 擴充功能必須安裝在 NPS 伺服器可以接收 RADIUS 要求。 NPS 伺服器若是作為 RDG 和 RRAS 等服務的相依項目安裝，則不會收到 RADIUS 要求。 NPS 擴充功能無法運作時安裝透過這種安裝和錯誤，因為它無法讀取 hello 驗證要求中的 hello 詳細資料。 |
| **REQUEST_MISSING_CODE** | 請確定 hello NPS 與 NAS 伺服器之間的 hello 密碼加密通訊協定支援您所使用的 hello 次要驗證方法。 **PAP** hello 定域機組中支援的 Azure MFA 的所有 hello 驗證方法： 通話、 單向簡訊、 行動裝置應用程式通知和行動裝置應用程式的驗證碼。 **CHAPV2** 和 **EAP** 支援通話和行動裝置應用程式通知。 |
| **USERNAME_CANONICALIZATION_ERROR** | 確認 hello 使用者存在於您在內部部署 Active Directory 執行個體，且該 hello NPS 服務權限 tooaccess hello 目錄。 如果您使用跨樹系信任，請[連絡支援人員](#contact-microsoft-support)以取得進一步協助。 |


   

### <a name="alternate-login-id-errors"></a>替代登入識別碼錯誤

| 錯誤碼 | 錯誤訊息 | 疑難排解步驟 |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | 錯誤：userObjectSid 查閱失敗 | 請確認該 hello 使用者存在於您的內部部署 Active Directory 執行個體。 如果您使用跨樹系信任，請[連絡支援人員](#contact-microsoft-support)以取得進一步協助。 |
| **ALTERNATE_LOGIN_ID_ERROR** | 錯誤：替代 LoginId 查閱失敗 | 確認 LDAP_ALTERNATE_LOGINID_ATTRIBUTE 設定 tooa[有效的 active directory 屬性](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx)。 <br><br> 如果 LDAP_FORCE_GLOBAL_CATALOG 設定 tooTrue，或 LDAP_LOOKUP_FORESTS 設定具有非空白值，請確認您已設定為通用類別目錄，和該 hello AlternateLoginId 屬性會加入 tooit。 <br><br> 如果 LDAP_LOOKUP_FORESTS 設定具有非空白值，請確認 hello 值是否正確。 如果有多個樹系名稱，hello 名稱必須以分號分隔，不可包含空格。 <br><br> 如果上述步驟未能解決 hello 問題[連絡支援人員](#contact-microsoft-support)更多協助。 |
| **ALTERNATE_LOGIN_ID_ERROR** | 錯誤：替代 LoginId 值是空的 | 請確認該 hello AlternateLoginId 屬性設定為 hello 使用者。 |


## <a name="errors-your-users-may-encounter"></a>您的使用者可能會遇到下列錯誤

| 錯誤碼 | 錯誤訊息 | 疑難排解步驟 |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | 沒有 hello 使用者的存取權限 toodo 驗證呼叫者的租用戶。 | 請檢查是否 hello 租用戶網域和 hello 使用者主體名稱 (UPN) 的 hello 網域是 hello 相同。 例如，請確定user@contoso.com正嘗試 tooauthenticate toohello Contoso 租用戶。 hello UPN 代表有效的使用者在 Azure 中的 hello 租用戶。 |
| **AuthenticationMethodNotConfigured** | hello 指定 hello 使用者未設定驗證方法 | 已新增或驗證其驗證方法，根據 toohello 指示中的 hello 使用者[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md)。 |
| **AuthenticationMethodNotSupported** | 不支援指定的驗證方法。 | 請收集所有包含此錯誤的記錄，並[連絡支援人員](#contact-microsoft-support)。 當您連絡支援人員時，提供 hello 使用者名稱和 hello 觸發 hello 錯誤的次要驗證方法。 |
| **BecAccessDenied** | MSODS Bec 呼叫傳回存取遭拒，可能 hello 未定義 username hello 租用戶中 | hello 使用者存在於 Active Directory 內部部署中，但未同步處理至 Azure AD 的 AD Connect。 或者，hello 使用者遺漏 hello 租用戶。 加入 hello 使用者 tooAzure AD，並將它們加入其驗證方法，根據 toohello 指示[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md)。 |
| **InvalidFormat** 或 **StrongAuthenticationServiceInvalidParameter** | hello 電話號碼的格式無法辨識 | 有 hello 使用者修正其驗證電話號碼。 |
| **InvalidSession** | hello 指定工作階段無效或已過期 | hello 工作階段已使用超過三分鐘 toocomplete。 請確認該 hello 使用者輸入 hello 驗證程式碼，或者回應 toohello 應用程式通知，在初始化 hello 驗證要求的三分鐘內。 如果這樣未修正 hello 問題，請檢查有沒有用戶端、 NAS 伺服器、 NPS 伺服器與 hello Azure MFA 端點之間的網路延遲。  |
| **NoDefaultAuthenticationMethodIsConfigured** | Hello 使用者已不設定任何預設驗證方法 | 已新增或驗證其驗證方法，根據 toohello 指示中的 hello 使用者[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md)。 請確認該 hello 使用者已選擇預設驗證方法，並設定該帳戶的方法。 |
| **OathCodePinIncorrect** | 輸入的代碼和 Pin 碼錯誤。 | 此錯誤不應該在 hello NPS 擴充功能。 如果您的使用者遇到此錯誤，請[連絡支援人員](#contact-microsoft-support)以取得疑難排解說明。 |
| **ProofDataNotFound** | 證明資料未設定為指定的 hello 驗證方法。 | 請嘗試不同的驗證方法，或加入新的驗證方法，根據 toohello 指示中的 hello 使用者[管理您的設定進行兩步驟驗證](./end-user/multi-factor-authentication-end-user-manage-settings.md)。 如果 hello 使用者持續發生此錯誤之後，確認其驗證方法設定正確，toosee[連絡支援人員](#contact-microsoft-support)。 |
| **SMSAuthFailedWrongCodePinEntered** | 輸入的代碼和 Pin 碼錯誤。 (OneWaySMS) | 此錯誤不應該在 hello NPS 擴充功能。 如果您的使用者遇到此錯誤，請[連絡支援人員](#contact-microsoft-support)以取得疑難排解說明。 |
| **TenantIsBlocked** | 租用戶已遭封鎖 | [請連絡支援人員](#contact-microsoft-support)目錄識別碼從 hello Azure 入口網站中的 hello Azure AD 屬性頁面。 |
| **UserNotFound** | 找不到 hello 指定的使用者 | 不會再為使用 Azure AD 中看見 hello 租用戶。 檢查您的訂閱為作用中，且您擁有 hello 必要的第一個合作對象應用程式。 也請確定 hello 憑證主體中的 hello 租用戶如預期般，而 hello 憑證仍然有效，且已註冊在 hello 服務主體。 |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>使用者收到的訊息可能不是錯誤訊息

有時候，由於您使用者的驗證要求失敗，他們可能會收到來自 Multi-Factor Authentication 的訊息。 這些不是錯誤的設定，hello 產品中，但是會刻意警告解釋為什麼拒絕驗證要求。

| 錯誤碼 | 錯誤訊息 | 建議的步驟 | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | 輸入的代碼錯誤\OATH 代碼錯誤 | 這不是錯誤，是使用者輸入的代碼有誤。 | hello 使用者輸入 hello 錯誤的程式碼。 請要求新代碼並讓他們再試一次，或請他們重新登入。 | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | 已達重試代碼次數的上限 | hello 使用者 hello 驗證挑戰失敗太多次。 根據您的設定，它們可能需要 toobe 現在解除封鎖管理員。  |
| **SMSAuthFailedWrongCodeEntered** | 輸入的代碼錯誤/文字訊息 OTP 不正確 | hello 使用者輸入 hello 錯誤的程式碼。 請要求新代碼並讓他們再試一次，或請他們重新登入。 |

## <a name="errors-that-require-support"></a>需要支援的錯誤

如果您遇到以下其中一種錯誤，我們建議您[連絡支援人員](#contact-microsoft-support)以取得診斷協助。 這些錯誤並沒有標準的解決步驟。 當您執行連絡支援人員時，是確定 tooinclude 太多越好 hello 步驟造成 tooan 錯誤的例外狀況相關的資訊與您的租用戶資訊。

| 錯誤碼 | 錯誤訊息 |
| ---------- | ------------- |
| **InvalidParameter** | 要求不能是 Null |
| **InvalidParameter** | 對 ReplicationScope:{0} 而言，ObjectId 不能是 Null 或空白 |
| **InvalidParameter** | hello 的 CompanyName 長度\{0} \ 超過 hello 最大允許的長度 {1} |
| **InvalidParameter** | UserPrincipalName 不能是 Null 或空白 |
| **InvalidParameter** | hello 提供 TenantId 不是正確的格式 |
| **InvalidParameter** | SessionId 不能是 Null 或空白 |
| **InvalidParameter** | 無法解析任何來自要求或 Msods 的 ProofData。 hello ProofData 不明 |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>後續步驟

### <a name="troubleshoot-user-accounts"></a>針對使用者帳戶進行移難排解

如果您的使用者[進行雙步驟驗證時發生問題](./end-user/multi-factor-authentication-end-user-troubleshoot.md)，請協助助他們自行診斷問題。 

### <a name="contact-microsoft-support"></a>連絡 Microsoft 支援

如需其他協助，請透過 [Azure Multi-Factor Authentication Server 支援](https://support.microsoft.com/oas/default.aspx?prid=14947)連絡支援專業人員。 連絡我們時，請盡量包含有關問題的最多資訊，這樣會十分有幫助。 您可以提供的資訊包括您已看到 hello 錯誤，hello hello 使用者特定的錯誤代碼，hello 特定的工作階段識別碼，hello 識別碼 hello 頁面看到 hello 錯誤，以及偵錯記錄檔。

toocollect 偵錯記錄檔，以支援的診斷資訊，請使用 hello 下列步驟： 

1. 開啟系統管理員命令提示字元並執行下列命令︰

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. 重現 hello 問題

3. 停止使用這些命令的 hello 追蹤：

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. 壓縮 hello hello C:\NPS 資料夾內容，並附加 hello 壓縮檔案 toohello 支援案例。


