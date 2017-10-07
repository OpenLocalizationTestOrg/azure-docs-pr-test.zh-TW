---
title: "Azure AD 傳遞驗證 - 快速入門 | Microsoft Docs"
description: "本文說明 tooget 如何開始使用 Azure Active Directory (Azure AD) 的傳遞驗證。"
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
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Azure Active Directory 傳遞驗證：快速入門

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>如何 toodeploy Azure AD 通過驗證

Azure Active Directory (Azure AD) 通過驗證可讓使用者 toosign tooboth 內部和雲端型應用程式使用 hello 相同密碼。 它會直接向內部部署 Active Directory 驗證使用者的密碼，以決定是否讓使用者登入。

>[!IMPORTANT]
>Azure AD 傳遞驗證目前為預覽功能。 如果您已使用預覽透過這項功能，您應該確定您已升級的 hello 驗證代理程式的預覽版本使用所提供的 hello 指示[這裡](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md)。

您需要 toofollow 這些指示 toodeploy 傳遞驗證：

## <a name="step-1-check-prerequisites"></a>步驟 1：檢查必要條件

請確定該 hello 下列必要條件已就緒：

### <a name="on-hello-azure-active-directory-admin-center"></a>在 hello Azure Active Directory 系統管理中心

1. 在 Azure AD 租用戶上建立僅限雲端的「全域管理員」帳戶。 如此一來，您可以管理租用戶 hello 設定應該在內部部署服務失敗或無法使用。 了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。 這個步驟是您不會遭到鎖定您的租用戶的重要 tooensure。
2. 新增一或多個[自訂網域名稱](../active-directory-add-domain.md)tooyour Azure AD 租用戶。 您的使用者會使用其中一個網域名稱登入。

### <a name="in-your-on-premises-environment"></a>在內部部署環境中

1. 識別執行 Windows Server 2012 R2 或更新版本上的 toorun Azure AD Connect 的伺服器。 新增 hello 伺服器 toohello 相同 AD 樹系做為其密碼需要驗證的 toobe hello 使用者。
2. 安裝 hello[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) hello 上一個步驟中所識別的伺服器上。 如果您已經有 Azure AD Connect 執行，請確定該 hello 版本 1.1.557.0 或更新版本。
3. 找出額外的伺服器執行 Windows Server 2012 R2 或稍後哪些 toorun 的獨立驗證代理程式 」。 必須 toobe 1.5.193.0 的 hello 驗證代理程式版本或更新版本。 此伺服器是需要的 tooensure 的登入要求的高可用性。 新增 hello 伺服器 toohello 相同 AD 樹系做為其密碼需要驗證的 toobe hello 使用者。
4. 如果您的伺服器和 Azure AD 之間的防火牆，您需要下列項目 tooconfigure hello:
   - 請驗證代理程式可以做出**輸出**要求 tooAzure AD 透過下列連接埠的 hello:
   
   | 連接埠號碼 | 使用方式 |
   | --- | --- |
   | **80** | 下載憑證撤銷清單 (Crl) 時驗證 hello SSL 憑證 |
   | **443** | 所有與我們服務之間的輸出通訊 |
   
   如果您的防火牆，強制執行規則，根據 toooriginating 使用者，開啟這些連接埠的流量從做為網路服務執行的 Windows 服務。
   - 如果您的防火牆或 proxy 可讓 DNS 允許清單，白名單連線太**\*。 msappproxy.net**和 **\*。.servicebus.windows.net**。 如果沒有，請允許存取太[Azure 資料中心 IP 範圍](https://www.microsoft.com/download/details.aspx?id=41653)，這每週更新。
   - 驗證代理程式需要存取太**login.windows.net**和**login.microsoftonline.com**的初始註冊時，開啟您的防火牆，以及這些 url。
   - 憑證驗證解除封鎖 hello 下列 Url: **mscrl.microsoft.com:80**， **crl.microsoft.com:80**， **ocsp.msocsp.com:80**和**www.microsoft.com:80**。 這些 URL 會用於其他 Microsoft 產品的憑證驗證，因此您可能已將這些 URL 解除封鎖。

## <a name="step-2-enable-exchange-activesync-support-optional"></a>步驟 2：啟用 Exchange ActiveSync 支援 (選擇性)

請遵循這些指示 tooenable Exchange ActiveSync 的支援：

1. 使用[Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) toorun hello 下列命令：
```
Get-OrganizationConfig | fl per*
```

2. 檢查 hello hello 值`PerTenantSwitchToESTSEnabled`設定。 如果 hello 值**true**、 您的租用戶已正確設定-通常是對大多數客戶來說 hello 案例。 如果 hello 值**false**，請執行 hello 下列命令：
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. 請確認 hello 值的 hello`PerTenantSwitchToESTSEnabled`現在設定為太**true**。 等候一小時前移動 toohello 下一個步驟。

如果進行此步驟時碰到任何問題，請查閱我們的[疑難排解指南](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues)以取得更多資訊。

## <a name="step-3-enable-hello-feature"></a>步驟 3： 啟用 hello 功能

您可以使用 [Azure AD Connect](active-directory-aadconnect.md) 來啟用傳遞驗證。

>[!IMPORTANT]
>Hello Azure AD Connect 的主要或暫存伺服器上，可以啟用傳遞驗證。 強烈建議您啟用從 hello 主要伺服器。

如果您第一次安裝 Azure AD Connect hello，選擇 hello[自訂安裝路徑](active-directory-aadconnect-get-started-custom.md)。 在 hello**使用者登入**頁面上，選擇**傳遞驗證**為 hello 登入方法。 成功完成時，傳遞驗證代理程式安裝在 hello 與 Azure AD Connect 相同的伺服器。 此外，您的租用戶上啟用 hello 傳遞驗證功能。

![Azure AD Connect - 使用者登入](./media/active-directory-aadconnect-sso/sso3.png)

如果您已安裝 Azure AD Connect (使用 hello[快速安裝](active-directory-aadconnect-get-started-express.md)或 hello[自訂安裝](active-directory-aadconnect-get-started-custom.md)路徑)，請選取**變更使用者的登入頁面**上 Azure AD連接，然後按一下**下一步**。 然後選取**傳遞驗證**為 hello 登入方法。 成功完成時，傳遞驗證代理程式安裝在 hello 與 Azure AD Connect 和 hello 功能相同的伺服器已啟用您的租用戶上。

![Azure AD Connect - 變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>傳遞驗證是租用戶層級的功能。 開啟此功能會影響的跨使用者登入_所有_hello 管理您的租用戶中的網域。 如果您要從 AD FS tooPass 透過驗證切換，我們建議您等待至少 12 小時，關閉您的 AD FS 基礎結構之前，-這個等候時間是使用者可以保持登入 tooExchange ActiveSync 轉換期間的 tooensure。

## <a name="step-4-test-hello-feature"></a>步驟 4： 測試 hello 功能

請遵循這些指示 tooverify，您已正確啟用傳遞驗證：

1. 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)hello 租用戶的全域管理員認證。
2. 選取**Azure Active Directory** hello 左側導覽上。
3. 選取 [Azure AD Connect]。
4. 請確認該 hello**傳遞驗證**功能就會顯示為**啟用**。
5. 選取 [傳遞驗證]。 此刀鋒視窗會列出 hello 伺服器驗證代理程式的安裝位置。

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

在此階段，租用戶中所有受管理網域的使用者都可以使用傳遞驗證來登入。 不過，同盟網域的使用者會繼續 toosign 中使用 Active Directory Federation Services (AD FS) 或您先前設定的另一個同盟提供者。 如果您從同盟 toomanaged 轉換網域，請從該網域的所有使用者會自動都啟動使用傳遞驗證登入。 僅限雲端的使用者不會受到 hello 通過驗證功能。

## <a name="step-5-ensure-high-availability"></a>步驟 5：確保高可用性

如果您計劃 toodeploy 傳遞驗證實際執行環境中的，您應該安裝在獨立驗證代理程式 」。 在伺服器上安裝此第二個驗證代理程式_其他_比 hello 一個執行 Azure AD Connect 與 hello 第一個驗證代理程式。 此設定可提供高可用性來滿足登入要求。 請遵循這些指示 toodeploy 獨立驗證代理程式：

1. **下載 hello hello 驗證代理程式最新版本 (版本 1.5.193.0 或更新版本)**： 登入 toohello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com)與您的租用戶全域管理員認證。
2. 選取**Azure Active Directory** hello 左側導覽上。
3. 依序選取 [Azure AD Connect] 和 [傳遞驗證]。 然後選取 [下載代理程式]。
4. 按一下 hello**接受條款 （& s) 下載** 按鈕。
5. **Hello 最新版本的 hello 驗證代理程式安裝**: hello 前面步驟中所下載的可執行檔執行 hello。 出現提示時，提供您租用戶的全域管理員認證。

![Azure Active Directory 管理中心 - 下載驗證代理程式按鈕](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory 管理中心 - 下載代理程式刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>您也可以下載 hello 驗證代理程式 」 從[這裡](https://aka.ms/getauthagent)。 請確定您檢閱並接受 hello 驗證代理程式的[服務條款](https://aka.ms/authagenteula)_之前_安裝它。

## <a name="next-steps"></a>後續步驟
- [**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。 了解支援的情節和不支援的情節。
- [**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。
- [**常見問題集**](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently 常見問題的答案。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
