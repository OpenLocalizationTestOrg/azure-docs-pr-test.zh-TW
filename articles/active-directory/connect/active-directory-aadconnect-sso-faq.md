---
title: "Azure AD Connect：無縫單一登入 - 常見問題集 | Microsoft Docs"
description: "關於 Azure Active Directory 無縫式單一登入的常見問題的解答 toofrequently。"
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory 無縫單一登入：常見問題集

本文將會解決 Azure Active Directory 無縫單一登入 (無縫 SSO) 的常見問題。 請隨時回來查看新內容。

>[!IMPORTANT]
>hello 無縫式 SSO 的功能目前為預覽狀態。

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>無縫 SSO 與哪些登入方法搭配運作？

無縫式 SSO 可以結合其中一個 hello[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法。 然而，此功能無法搭配 Active Directory Federation Services (ADFS) 使用。

## <a name="is-seamless-sso-a-free-feature"></a>無縫 SSO 是免費功能嗎？

無縫式 SSO 是可用的功能，您不需要任何付費的版本的 Azure AD toouse 它。 Hello 功能正式運作時，則仍會保持可用。

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>哪些應用程式利用無縫 SSO 的 `domain_hint` 或 `login_hint` 參數功能？

我們很 hello 處理序編譯的應用程式傳送這些參數與 hello 的不 hello 清單中。 如果您有興趣的應用程式，讓我們知道 hello 註解區段中。

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>並無縫式 SSO 支援`Alternate ID`hello 使用者名稱，而不是因為`userPrincipalName`嗎？

是。 無縫式 SSO 支援`Alternate ID`hello 使用者名稱所示，在 Azure AD Connect 中設定時為[這裡](active-directory-aadconnect-get-started-custom.md)。 並非所有 Office 365 應用程式都支援 `Alternate ID`。 Hello 支援陳述式，請參閱 toohello 特定應用程式的文件。

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>我想 tooregister 非 Windows 10 裝置與 Azure AD，而不需要使用 AD FS。 我可以改為使用無縫 SSO 嗎？

是，這種情況下需要版本 2.1 或更新版本的 hello[工作地方聯結用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>如何可以我變換 hello Kerberos 解密金鑰的 hello`AZUREADSSOACCT`電腦帳戶？

請務必 toofrequently 變換 hello Kerberos 解密金鑰的 hello`AZUREADSSOACCT`電腦帳戶 （這表示 Azure AD） 建立在您內部部署 AD 樹系。

>[!IMPORTANT]
>我們強烈建議您，您會彙總 hello Kerberos 解密金鑰至少每隔 30 天。

執行 Azure AD Connect 的情況下遵循 hello 在內部部署伺服器上的下列步驟：

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>步驟 1. 取得已啟用無縫 SSO 的 AD 樹系清單

1. 首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。
2. 請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。
3. 瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。
4. 使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。
5. 以系統管理員身分執行 PowerShell。 在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。 此命令應該提供快顯 tooenter 租用戶的全域管理員認證。
6. 呼叫 `Get-AzureADSSOStatus`。 這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>步驟 2. 更新上設定它在每個 AD 樹系的 hello Kerberos 解密金鑰

1. 呼叫 `$creds = Get-Credential`。 出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。
2. 呼叫 `Update-AzureADSSOForest -OnPremCredentials $creds`。 此命令更新 hello hello Kerberos 的解密金鑰`AZUREADSSOACCT`這個特定的 AD 樹系中的電腦帳戶在 Azure AD 中更新它。
3. 重複上述步驟設定好 hello 功能每個 AD 樹系的 hello。

>[!IMPORTANT]
>請確定您_不_執行 hello`Update-AzureADSSOForest`命令一次以上。 否則，hello 功能會停止運作，直到 hello 時間過期，而且會重新發出您在內部部署 Active directory 使用者的 Kerberos 票證。

## <a name="how-can-i-disable-seamless-sso"></a>如何停用無縫 SSO？

您可以使用 Azure AD Connect 停用無縫 SSO。

執行 Azure AD Connect，選擇 [變更使用者登入頁面]，然後按一下 [下一步]。 然後取消核取 hello 」 啟用單一登入 」 選項。 繼續完成 hello 精靈。 完成之後 hello 精靈，無縫式 SSO 會停用您的租用戶。

但是，您會在畫面上看到一個包含以下內容的訊息：

「 單一登入現已停用，但有額外的手動步驟 tooperform 順序 toocomplete 清除中。 深入了解」

toocomplete hello 程序，請執行下列手動步驟 hello 在內部部署伺服器上的執行 Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>步驟 1. 取得已啟用無縫 SSO 的 AD 樹系清單

1. 首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。
2. 請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。
3. 瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。
4. 使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。
5. 以系統管理員身分執行 PowerShell。 在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。 此命令應該提供快顯 tooenter 租用戶的全域管理員認證。
6. 呼叫 `Get-AzureADSSOStatus`。 這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>步驟 2. 手動刪除 hello`AZUREADSSOACCT`從您看到列出每個 AD 樹系的電腦帳戶。

## <a name="next-steps"></a>後續步驟

- [**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。
- [**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
