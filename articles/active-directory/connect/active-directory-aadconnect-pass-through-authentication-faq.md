---
title: "Azure AD Connect：傳遞驗證 - 常見問題集 | Microsoft Docs"
description: "Azure Active Directory 通過驗證的相關常見問題的解答 toofrequently。"
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Azure Active Directory 傳遞驗證：常見問題集

本文將會解決 Azure Active Directory (Azure AD) 傳遞驗證的常見問題。 請隨時回來查看新內容。

>[!IMPORTANT]
>hello 通過驗證功能目前為預覽狀態。

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>我應該選擇哪一種 hello Azure AD 登入方法傳遞驗證、 密碼雜湊同步處理和 Active Directory Federation Services (AD FS)？

這取決於您的內部部署環境和組織需求。 檢閱本文[比較 hello 各種 Azure AD 登入方法](active-directory-aadconnect-user-signin.md)。

## <a name="is-pass-through-authentication-a-free-feature"></a>傳遞驗證是否為免費功能？

傳遞驗證是可用的功能，您不需要任何付費的版本的 Azure AD toouse 它。 Hello 功能正式運作時，則仍會保持可用。

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>[Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) 和 [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/) 是否有提供傳遞驗證功能？

否，傳遞驗證功能僅適用於 Azure AD hello 全球執行個體。

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>[條件式存取](../active-directory-conditional-access.md)是否能與傳遞驗證搭配運作？

是，所有條件式存取功能 (包括 Azure Multi-Factor Authentication) 都能與傳遞驗證搭配運作。

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>傳遞驗證支援 「 替代識別碼 」 做為 hello 的使用者名稱，而不是"userPrincipalName 」？

是。 傳遞驗證支援`Alternate ID`hello 使用者名稱所示，在 Azure AD Connect 中設定時為[這裡](active-directory-aadconnect-get-started-custom.md)。 並非所有 Office 365 應用程式都支援 `Alternate ID`。 Hello 支援陳述式，請參閱 toohello 特定應用程式的文件。

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>密碼雜湊同步處理是否做為遞補 tooPass 透過驗證中？

否，密碼雜湊同步處理不是泛型後援 tooPass 透過驗證。 它只會作為[目前不支援傳遞驗證的情況下](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios)的遞補。 tooavoid 使用者登入失敗，您應該設定為傳遞驗證[高可用性](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)。

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>我是否可以安裝[Azure AD Application Proxy](../active-directory-application-proxy-get-started.md)接頭 hello 與傳遞驗證代理程式 」 相同的伺服器？

[是]，以 hello 品牌 hello 傳遞驗證代理程式的版本支援此組態 (1.5.193.0 版本或更新版本)。

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>需要哪些版本的 Azure AD Connect 和傳遞驗證代理程式？

您需要 1.1.486.0 版本或更新版本的 Azure AD Connect 和 1.5.58.0 或更新版本的此功能 toowork hello 傳遞驗證代理程式 」。 所有軟體都應該安裝在 Windows Server 2012 R2 或更新版本的伺服器上。

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>如果我的使用者密碼已過期，會發生什麼事，且它們嘗試 toosign 中使用傳遞驗證？

如果您已設定[密碼回寫](../active-directory-passwords-update-your-own-password.md)特定使用者，如果 hello 使用者登入時使用傳遞驗證，也可以變更或重設其密碼。 hello 密碼會回寫 tooon 內部部署 Active Directory 如預期般。

不過，如果未針對特定使用者設定密碼回寫，或如果 hello 使用者不具有有效的 Azure AD 授權指派，hello 使用者無法更新其密碼的 hello 雲端。 即使他們的密碼過期，他們也無法加以更新。 hello 使用者而是會看到此訊息: 「 您的組織不允許您 tooupdate 此站台上的密碼。 請根據您的組織所建議的 toohello 方法進行更新或要求系統管理員尋求協助。 」 hello 使用者或 hello 系統管理員有 tooreset 密碼在內部部署 Active Directory 中。

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>傳遞驗證如何防範暴力密碼破解攻擊？

如需詳細資訊，請閱讀[這篇文章](active-directory-aadconnect-pass-through-authentication-smart-lockout.md)。

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>傳遞驗證代理程式會透過連接埠 80 和 443 進行哪些方面的通訊？

- hello 驗證代理程式會建立功能的所有作業的連接埠 443 上 HTTPS 要求。
- hello 驗證代理程式透過連接埠 80 toodownload SSL 憑證撤銷清單進行 HTTP 要求。

     >[!NOTE]
     >在新的更新我們可以減少 hello hello 功能所需的連接埠的數目。 如果您有舊版的 Azure AD Connect 或 hello 驗證代理程式 」 時，保持這些連接埠也開啟： 5671、 8080、 9090、 9091、 9350、 9352 和 10100 10120。

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>可以透過輸出 web proxy 伺服器 hello 傳遞驗證代理程式通訊嗎？

是。 如果您在內部部署環境中啟用 WPAD （Web Proxy 自動探索），則驗證代理程式會自動嘗試 toolocate，並 hello 網路上使用 web proxy 伺服器。

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>我可以安裝兩個或更多的傳遞驗證代理程式上 hello 相同的伺服器嗎？

不可以，您只能在單一伺服器上安裝一個傳遞驗證代理程式。 如果想 tooconfigure 通過驗證的高可用性，請依照這個 hello 指示[文章](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)改為。

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>我已經使用 Active Directory 同盟服務 (AD FS) 來進行 Azure AD 登入。 如何切換它 tooPass 透過驗證？

如果您已設定 AD FS 做為登入方法使用 hello Azure AD Connect 精靈，變更 hello 使用者登入方法 tooPass 透過驗證。 這項變更 hello 租用戶上啟用通過驗證，並將轉換_所有_成受管理網域同盟網域。 租用戶所有的後續登入要求都會由傳遞驗證來進行處理。 目前，沒有任何支援的方法，在 Azure AD Connect toouse 跨不同網域的 AD FS 與通過驗證的組合。

如果 AD FS 已設定為 hello 登入方法_外_hello Azure AD Connect 精靈，變更 hello 使用者登入方法 tooPass 透過驗證 （從 hello [不設定] 選項）。 這項變更會啟用 hello 租用戶上通過驗證。 不過，所有同盟網域都繼續 toouse AD FS 登入。 使用 PowerShell toomanually convert 部分或所有這些同盟網域 tooManaged 網域。 完成後，受管理的網域上的所有登入要求便 (只) 會由傳遞驗證來進行處理。

>[!IMPORTANT]
>傳遞驗證不會為僅限雲端的 Azure AD 使用者處理登入要求。

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>是否可以在多樹系 AD 環境中使用傳遞驗證？

是。 如果 AD 樹系之間有樹系信任且名稱尾碼路由已正確設定，就支援多樹系環境。

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>傳遞驗證代理程式是否提供負載平衡功能？

否，安裝多個傳遞驗證代理程式可確保[高可用性](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)，但不會提供負載平衡。 一或兩個 hello 驗證代理程式可能會處理 hello 大量 hello 登入要求。

是輕量型的 hello 驗證代理程式需要 toohandle 的密碼驗證要求。 因此對大多數客戶來說，總共只要兩到三個驗證代理程式就能輕鬆應付尖峰負載和平均負載。

我們建議您安裝驗證代理程式關閉 tooyour 網域控制站 tooimprove 登入延遲。

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>我是否可以安裝 hello 以外 hello 執行 Azure AD Connect 的伺服器上的第一個傳遞驗證代理程式？

不行，「不」支援這種情況。

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>應該安裝幾個傳遞驗證代理程式？

我們的建議如下：

- 總共安裝兩到三個驗證代理程式。 此設定足以應付大部分客戶的需求。
- 您安裝登入延遲 tooimprove 驗證代理程式在您的網域控制站 （或關閉 toothem 越好）。
- 您確定 （驗證代理程式的安裝位置） 的伺服器，會為其密碼需要驗證的 toobe hello 使用者新增 toohello 相同 AD 樹系。

>[!NOTE]
>系統限制每個租用戶只能有 12 個驗證代理程式。

## <a name="how-can-i-disable-pass-through-authentication"></a>如何停用傳遞驗證？

重新執行 hello Azure AD Connect 精靈，並變更傳遞驗證 tooanother 方法 hello 使用者登入方法。 這項變更會通過驗證 hello 租用戶上停用，並會解除安裝 hello 伺服器 hello 驗證代理程式 」。 您必須從其他伺服器的 toomanually 解除安裝 hello 驗證代理程式。

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>解除安裝傳遞驗證代理程式會發生什麼事？

從伺服器解除安裝傳遞驗證代理程式 」 會使它 toostop 接受登入要求。 請確定您有另一個驗證代理程式執行之前執行這項作業，tooavoid 中斷使用者登入您的租用戶。

## <a name="next-steps"></a>後續步驟
- [**目前的限制**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - 此功能目前為預覽狀態。 了解支援的情節和不支援的情節。
- [**快速入門**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - 開始使用 Azure AD 傳遞驗證。
- [**技術性深入探討**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - 了解這項功能的運作方式。
- [**疑難排解**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -了解如何 tooresolve 常見問題與 hello 功能。
- [**Azure AD 無縫 SSO**](active-directory-aadconnect-sso.md) - 深入了解此互補功能。
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。
