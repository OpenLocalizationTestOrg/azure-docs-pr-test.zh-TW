---
title: "Azure AD Connect：針對連線問題進行疑難排解 | Microsoft Docs"
description: "說明如何 tootroubleshoot 連線問題的 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>對 Azure AD Connect 的連線問題進行疑難排解
這篇文章說明 Azure AD Connect 與 Azure AD 之間的連線的運作方式以及如何 tootroubleshoot 連線的問題。 最有可能 toobe 與 proxy 伺服器的環境中所見，這些問題。

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>疑難排解 hello 安裝精靈 中的連線問題
Azure AD Connect 使用新式驗證 （使用 hello ADAL 程式庫） 進行驗證。 hello 安裝精靈和適當的 hello 同步處理引擎都需要正確設定，因為這兩個是.NET 應用程式的 machine.config toobe。

在本文中，我們示範如何 Fabrikam 連接 tooAzure AD 透過其 proxy。 名為 fabrikamproxy 與正在使用連接埠 8080 hello proxy 伺服器。

首先我們需要 toomake 確定[ **machine.config** ](active-directory-aadconnect-prerequisites.md#connectivity)已正確設定。  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> 在某些非 Microsoft 部落格，它會詳細說明，您應該進行變更 toomiiserver.exe.config 改為。 不過，這個檔案是覆寫，因此，即使它的運作方式在初始安裝期間，如果 hello 系統停止運作的第一個升級時每個升級。 基於這個原因，hello 建議改用是 tooupdate machine.config。
>
>

hello proxy 伺服器也必須開啟所需的 hello Url。 hello 官方清單記載於[Office 365 Url 與 IP 位址範圍](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)。

個 Url 下表, 中的 hello 完全是 hello 絕對裸機的最小 toobe 無法 tooconnect tooAzure AD。 這份清單並未包含任何選用的功能，例如密碼回寫或 Azure AD Connect Health。 它是文件的此處 toohelp 疑難排解 hello 初始設定。

| URL | 連接埠 | 說明 |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |列出使用的 toodownload CRL。 |
| \*.verisign.com |HTTP/80 |列出使用的 toodownload CRL。 |
| \*.entrust.com |HTTP/80 |使用的 toodownload CRL 列出 MFA。 |
| \*.windows.net |HTTPS/443 |使用中 tooAzure AD toosign。 |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |用於 MFA。 |
| \*.microsoftonline.com |HTTPS/443 |使用 tooconfigure Azure AD 目錄與匯入/匯出資料。 |

## <a name="errors-in-hello-wizard"></a>Hello 精靈中的錯誤
hello 安裝精靈會使用兩個不同的安全性內容。 在 [hello] 頁面上**連接 tooAzure AD**，它會使用目前登入使用者的 hello。 在 [hello] 頁面上**設定**，它變更 toohello[執行 hello hello 同步處理引擎的服務帳戶](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account)。 如果發生問題時，它會顯示最有可能已經在 hello**連接 tooAzure AD**因為 hello proxy 設定是全域的 hello 精靈中的頁面。

下列問題的 hello 是 hello 在 hello 安裝精靈中遇到最常見的錯誤。

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>hello 安裝精靈設定不正確
Hello 精靈本身無法到達 hello proxy 時，會出現這個錯誤。  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* 如果您看到此錯誤，請確認 hello [machine.config](active-directory-aadconnect-prerequisites.md#connectivity)是否已正確設定。
* 如果這看起來正確，請依照下列中的 hello 步驟[驗證 proxy 的連線](#verify-proxy-connectivity)toosee hello 問題是否有外部 hello 精靈 」。

### <a name="a-microsoft-account-is-used"></a>使用了 Microsoft 帳戶
如果您使用 **Microsoft 帳戶**而不是**學校或組織帳戶**，就會看到一個一般錯誤。  
![使用了 Microsoft 帳戶](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>無法連線到 hello MFA 端點
會出現這個錯誤，如果 hello 端點**https://secure.aadcdn.microsoftonline-p.com**無法連線到您的全域管理員且啟用 MFA。  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* 如果您看到此錯誤，請確認該 hello 端點**secure.aadcdn.microsoftonline p.com** toohello proxy 已加入。

### <a name="hello-password-cannot-be-verified"></a>無法驗證 hello 密碼
如果 hello 安裝精靈已成功連接 tooAzure AD，但無法驗證 hello 密碼本身，您會看到這個錯誤：  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* 受到 hello 密碼暫時密碼，而必須變更嗎？ 是它實際 hello 正確的密碼？ 請嘗試 toosign toohttps://login.microsoftonline.com （在 hello Azure AD Connect 的伺服器以外的另一部電腦） 中，並確認 hello 帳戶可供使用。

### <a name="verify-proxy-connectivity"></a>確認 Proxy 連線
tooverify 如果 hello Azure AD Connect 伺服器具有實際連線 hello Proxy 與網際網路上，使用一些 PowerShell toosee hello proxy 或不允許 web 要求。 在 PowerShell 命令提示字元中，執行 `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`。 （技術上 hello 第一次呼叫是 toohttps://login.microsoftonline.com 而且這個 URI 可以，但是 hello 其他 URI 是更快的 toorespond）。

PowerShell 會使用 machine.config toocontact hello proxy 中的 hello 組態。 在 winhttp/netsh hello 設定應該不會影響這些 cmdlet。

如果 hello proxy 設定正確，您應該取得成功的狀態： ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

如果您收到**toohello 遠端伺服器時，無法 tooconnect**、 然後 PowerShell 正嘗試 toomake 直接呼叫，而不使用 hello proxy 或未正確設定 DNS。 請確定 hello **machine.config**檔案已正確設定。
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

如果 hello proxy 設定不正確，您會收到錯誤： ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| 錯誤 | 錯誤文字 | 註解 |
| --- | --- | --- |
| 403 |禁止 |hello proxy 尚未開啟，hello 要求 URL。 重新檢查 hello proxy 設定，並請確定 hello [Url](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)已經開啟。 |
| 407 |需要 Proxy 驗證 |hello proxy 伺服器需要登入，然後並未提供任何。 如果您的 proxy 伺服器需要驗證，請確定 toohave hello machine.config 中設定此設定。也請確定您使用網域帳戶時，執行 hello 精靈 hello 使用者和 hello 服務帳戶。 |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>hello Azure AD Connect 與 Azure AD 之間的通訊模式
如果您已依照上述這些步驟操作卻仍然無法連接，這時可以開始查看網路記錄檔。 本節說明正常和成功的連線模式。 它也會列出常見的紅色 herrings 可以略過，當您正在閱讀 hello 網路記錄檔。

* 沒有呼叫 toohttps://dc.services.visualstudio.com。不需要的 toohave hello 安裝 toosucceed 及這些呼叫的 hello proxy 中開啟這個 URL 可以忽略。
* 您會看到 dns 解析列出 hello 實際主機 toobe hello DNS 名稱空間 nsatc.net 和 microsoftonline.com 不在其他命名空間中。不過，在 hello 實際伺服器名稱上沒有任何 web 服務要求，您不需要 tooadd 這些 Url toohello proxy。
* hello 端點 adminwebservice provisioningapi 探索端點和使用 toofind hello 實際的端點 toouse。 這些端點會依據您的區域而有所不同。

### <a name="reference-proxy-logs"></a>參考 Proxy 記錄檔
以下是傾印從實際的 proxy 記錄與 hello 安裝精靈頁面，從中拍攝 (相同的端點已經移除重複的項目 toohello)。 本節可以作為您自己 Proxy 和網路記錄檔的參考。 hello 實際的端點可能會不同，您的環境中 (特別是在這些 Url*斜體*)。

**連接 tooAzure AD**

| 時間 | URL |
| --- | --- |
| 1/11/2016 8:31 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**設定**

| 時間 | URL |
| --- | --- |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**初始同步處理**

| 時間 | URL |
| --- | --- |
| 1/11/2016 8:48 |connect://login.windows.net:443 |
| 1/11/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>驗證錯誤
本章節涵蓋可從 ADAL （hello 驗證程式庫使用的 Azure AD Connect） 和 PowerShell 傳回的錯誤。 說明 hello 錯誤應有所幫您在了解您的下一個步驟。

### <a name="invalid-grant"></a>無效的授與
無效的使用者名稱或密碼。 如需詳細資訊，請參閱[無法驗證 hello 密碼](#the-password-cannot-be-verified)。

### <a name="unknown-user-type"></a>不明的使用者類型
Azure AD 目錄找不到或無法解析。 或許您嘗試 toologin 以未經驗證的網域使用者名稱嗎？

### <a name="user-realm-discovery-failed"></a>使用者領域探索失敗
網路或 Proxy 組態問題。 無法連上網路 hello。 請參閱[hello 安裝精靈 中的連線問題進行疑難排解](#troubleshoot-connectivity-issues-in-the-installation-wizard)。

### <a name="user-password-expired"></a>使用者密碼過期
您的認證已過期。 請變更密碼。

### <a name="authorizationfailure"></a>AuthorizationFailure
未知的問題。

### <a name="authentication-cancelled"></a>驗證取消
hello 多因素驗證 (MFA) 要求已取消。

### <a name="connecttomsonline"></a>ConnectToMSOnline
驗證成功，但 Azure AD PowerShell 發生驗證問題。

### <a name="azurerolemissing"></a>AzureRoleMissing
驗證成功。 您不是全域管理員。

### <a name="privilegedidentitymanagement"></a>PrivilegedIdentityManagement
驗證成功。 已啟用 Privileged Identity Management，而且您目前不是全域管理員。 如需詳細資訊，請參閱 [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)。

### <a name="companyinfounavailable"></a>CompanyInfoUnavailable
驗證成功。 無法從 Azure AD 擷取公司資訊。

### <a name="retrievedomains"></a>RetrieveDomains
驗證成功。 無法從 Azure AD 擷取網域資訊。

### <a name="unexpected-exception"></a>未預期的例外狀況
顯示為未預期的錯誤 hello 安裝精靈。 如果您嘗試 toouse 情形**Microsoft 帳戶**而**學校或組織帳戶**。

## <a name="troubleshooting-steps-for-previous-releases"></a>舊版的疑難排解步驟
從組建編號 1.1.105.0 （發行 2016 年 2 月） 的版本，已淘汰 hello 登入小幫手。 此區段和 hello 設定不再是必要項目，但會保持為參考。

Hello 單一-登入小幫手 toowork，必須設定 winhttp。 透過 [**netsh**](active-directory-aadconnect-prerequisites.md#connectivity)，即可完成這項設定。  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>hello 登入小幫手設定不正確
Hello 登入小幫手無法連上 hello proxy 或 hello proxy 不允許 hello 要求時，會出現這個錯誤。
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* 如果您看到此錯誤，請查看中的 hello proxy 組態[netsh](active-directory-aadconnect-prerequisites.md#connectivity)並確認它是否正確。
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* 如果這看起來正確，請依照下列中的 hello 步驟[驗證 proxy 的連線](#verify-proxy-connectivity)toosee hello 問題是否有外部 hello 精靈 」。

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
