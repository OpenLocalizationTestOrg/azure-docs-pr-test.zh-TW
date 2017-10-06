---
title: "Azure AD Connect：無縫單一登入 - 快速入門 | Microsoft Docs"
description: "本文說明如何 tooget 啟動與 Azure Active Directory 無接縫單一登入。"
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory 無縫單一登入：快速入門

## <a name="how-toodeploy-seamless-sso"></a>如何 toodeploy 無縫式 SSO

Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO) 自動簽署時其公司的電腦已連線的 tooyour 公司網路上的使用者。 它提供您的使用者方便存取 tooyour 雲端型應用程式而不需要任何額外的內部部署元件。

>[!IMPORTANT]
>hello 無縫式 SSO 的功能目前為預覽狀態。

您需要 toofollow toodeploy 無縫式 SSO，下列步驟：

## <a name="step-1-check-prerequisites"></a>步驟 1：檢查必要條件

請確定該 hello 下列必要條件已就緒：

1. 設定 Azure AD Connect 伺服器：如果您使用[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)作為登入方法，不需要採取任何動作。 如果您使用[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)作為登入方法，而且 Azure AD Connect 與 Azure AD 之間有防火牆，請確定︰
- 您使用的是 1.1.484.0 版或更新版本的 Azure AD Connect。
- Azure AD Connect 可以與 `*.msappproxy.net` URL 通訊，而且是透過連接埠 443。 只有當您啟用 hello 功能，不會針對實際的使用者登入，是適用於此必要條件。
- Azure AD Connect 可直接 IP 連線 toohello [Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)。 同樣地，此必要條件時，適用於只啟用 hello 功能。
2. 您需要同步處理 tooAzure AD 每個 AD 樹系的網域系統管理員認證 （使用 Azure AD Connect） 和您要為其使用者 tooenable 無縫式 SSO。

## <a name="step-2-enable-hello-feature"></a>步驟 2： 啟用 hello 功能

您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 啟用無縫 SSO。

若您執行全新安裝的 Azure AD Connect，選擇 hello[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。 在 hello 「 使用者登入 」 頁面上，核取 hello 」 啟用單一登入 」 選項。

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso8.png)

如果您已經安裝 Azure AD Connect，請在 Azure AD Connect 上選擇 [變更使用者登入] 頁面，然後按一下 [下一步]。 然後檢查 hello 」 啟用單一登入 」 選項。

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

繼續透過 hello 精靈直到到達 toohello 」 啟用單一登入 」 頁面。 提供每個 AD 樹系同步處理 tooAzure AD 網域系統管理員認證 （使用 Azure AD Connect） 和您要為其使用者 tooenable 無縫式 SSO。 

完成之後 hello 精靈，您的租用戶上已啟用無縫式 SSO。

>[!NOTE]
> hello 網域系統管理員認證不會儲存在 Azure AD Connect，或在 Azure AD 中，但使用的 tooenable hello 功能。

請遵循這些指示 tooverify，您已正確啟用無縫式 SSO:

1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。
2. 選取**Azure Active Directory** hello 左側導覽上。
3. 選取 [Azure AD Connect]。
4. 請確認該 hello**無接縫單一登入**功能就會顯示為**啟用**。

![Azure 入口網站 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>步驟 3： 轉出 hello 功能

tooroll hello 功能 tooyour 使用者，您必須透過 Active Directory 中的群組原則 tooadd 兩個 Azure AD Url （https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net） toousers' 內部網路區域的設定。

>[!NOTE]
> hello 遵循 Windows 上的指示只適用於 Internet Explorer 和 Google Chrome （如果它與 Internet Explorer 共用一組信任的網站 Url）。 讀取 Mozilla Firefox 和 Google Chrome mac 上的指示 tooset hello 下一節

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>您為什麼需要 toomodify 使用者的內部網路區域的設定？

根據預設，hello 瀏覽器會自動從 URL 計算 hello 區域 （網際網路或內部網路）。 例如，http://contoso/ 都是對應的 toohello 近端內部網路區域，而 http://intranet.contoso.com/ （因為 hello URL 包含句號） 則是對應的 toohello 網際網路區域。 瀏覽器不傳送-像是 hello 兩個 Azure AD Url-Kerberos 票證 tooa 雲端端點，除非其 URL，明確地新增 toohello 瀏覽器的近端內部網路區域。

### <a name="detailed-steps"></a>詳細步驟

1. 開啟 hello 群組原則管理工具。
2. 編輯 hello 套用的 toosome 或所有使用者的群組原則。 在此範例中，我們使用 hello**預設網域原則**。
3. 瀏覽過**使用者設定 \ 系統管理範本 \windows 元件 \internet explorer\ 網際網路控制項 Panel\Security 頁面**選取**站台指派清單 tooZone**。
![單一登入](./media/active-directory-aadconnect-sso/sso6.png)  
4. 啟用 hello 原則，並輸入下列值 (Azure AD Url 會轉送 Kerberos 票證的位置) 的 hello 和資料 (*1*指出近端內部網路區域) hello 對話方塊中。

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> 如果您想要 toodisallow 比方說，使用無縫式 SSO-有些使用者如果這些使用者內部網路上共用 kiosk-登入設定 hello 太前置值*4*。 此動作將 hello Azure AD Url toohello 受限制區域，而且會無縫式 SSO 失敗所有 hello 時間。

5. 按一下 [確定]，然後再按一下 [確定]。

![單一登入](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>瀏覽器考量

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox 不會自動執行 Kerberos 驗證。 每個使用者擁有 toomanually 新增 hello Azure AD Url tootheir Firefox 設定使用 hello 下列步驟：
1. 執行 Firefox，並輸入`about:config`hello 網址列中。 關閉任何您看到的通知。
2. 搜尋 hello **network.negotiate-auth.trusted-uri**喜好設定。 此喜好設定列出 Firefox 進行 Kerberos 驗證的受信任網站。
3. 按一下滑鼠右鍵，然後選取 [修改]。
4. 請輸入"https://autologon.microsoftazuread-sso.com，https://aadg.windows.net.nsatc.net"hello 欄位中。
5. 按一下 [確定]，並重新開啟 hello 瀏覽器。

#### <a name="safari-on-mac-os"></a>Mac OS 上的 Safari

請確認執行 Mac OS 的 hello 機器聯結的 tooAD。 請參閱指示如何 toodo，[這裡](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf)。

#### <a name="google-chrome-on-mac-os"></a>Mac OS 上的 Google Chrome

Mac OS 和其他非 Windows 平台上的 Google chrome，請參閱太[本文](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist)如需有關如何 toowhitelist hello 整合式驗證的 Azure AD Url 資訊。

使用協力廠商架構 Active Directory 群組原則已超出本文的範圍延伸 tooroll 出 hello Azure AD Url tooFirefox 和 Google Chrome Mac 使用者。

#### <a name="known-limitations"></a>已知限制

無縫 SSO 無法在 Firefox 和 Edge 瀏覽器的私人瀏覽模式中運作。 它也不適用於的 Internet Explorer 如果 hello 瀏覽器在增強保護模式中執行。

>[!IMPORTANT]
>我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。

## <a name="step-4-test-hello-feature"></a>步驟 4： 測試 hello 功能

tootest hello 功能特定的使用者，確保_所有_已就位 hello 下列條件：
  - hello 使用者在公司的裝置上登入。
  - hello 裝置已進行先前聯結的 tooyour Active Directory (AD) 網域。
  - hello 裝置有直接連線 tooyour 網域控制站 (DC)，hello 公司有線或無線網路上或是透過遠端存取連線，例如 VPN 連線。
  - 您有[推出 hello 功能](##step-3-roll-out-the-feature)toothis 使用群組原則的使用者。

tootest hello 案例只 hello 使用者名稱，但不是 hello 密碼 hello 使用者會輸入：
- 在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/*。

其中 hello 使用者沒有 tooenter hello 使用者名稱或 hello 密碼 tootest hello 案例： 
- 在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.onmicrosoft.com*。 將 "*contoso*" 取代為您租用戶的名稱。
- 或者，在新的私用瀏覽器工作階段中，登入 *https://myapps.microsoft.com/contoso.com*。 將 "*contoso.com*" 取代為租用戶中的已驗證網域 (非同盟網域)。

## <a name="step-5-roll-over-keys"></a>步驟 5：變換金鑰

在步驟 2 中，Azure AD Connect 會建立電腦帳戶 （代表 Azure AD） 中所有已啟用無縫式 SSO 的 hello AD 樹系。 在[這裡](active-directory-aadconnect-sso-how-it-works.md)詳細了解。 為了提升安全性，建議您經常向前復原透過 hello Kerberos 解密金鑰，這些電腦帳戶。

>[!IMPORTANT]
>您不需要 toodo 這個步驟_立即_啟用 hello 功能之後。 至少每隔 30 天變換 hello Kerberos 解密金鑰。

## <a name="next-steps"></a>後續步驟

- [**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。
- [**常見問題集**](active-directory-aadconnect-sso-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
