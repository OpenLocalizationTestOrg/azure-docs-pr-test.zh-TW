---
title: "aaaSingle 登入應用程式 proxy |Microsoft 文件"
description: "涵蓋 tooprovide 的單一登入使用 Azure AD Application Proxy。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Kerberos 限制委派針對單一登入 tooyour 應用程式與應用程式 Proxy

您可以針對透過應用程式 Proxy 發佈並使用整合式 Windows 驗證保護的內部部署應用程式，提供單一登入。 這些應用程式需要 Kerberos 票證以進行存取。 應用程式 Proxy 會使用 Kerberos 限制委派 (KCD) toosupport 這些應用程式。 

您可以啟用單一登入 tooyour 應用程式使用整合式 Windows 驗證 (IWA) 在 Active Directory tooimpersonate 使用者，提供應用程式 Proxy 連接器權限。 hello 連接器會使用此權限 toosend，並接收代表語彙基元。

## <a name="how-single-sign-on-with-kcd-works"></a>使用 KCD 單一登入的運作方式
使用者嘗試 tooaccess 使用 IWA 的內部應用程式時，此圖表會說明 hello 流程。

![Microsoft AAD 驗證流程圖](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. hello 使用者輸入 hello URL tooaccess hello 內部應用程式透過應用程式 Proxy。
2. 應用程式 Proxy 會重新導向 hello 要求 tooAzure AD 驗證服務 toopreauthenticate。 此時，Azure AD 會套用任何適用的驗證和授權原則，例如多重要素驗證。 如果 hello 使用者已經驗證，Azure AD 建立語彙基元，並將它傳送 toohello 使用者。
3. hello 使用者通過 hello 語彙基元 tooApplication Proxy。
4. 應用程式 Proxy 驗證 hello 語彙基元，和擷取 hello 使用者主體名稱 (UPN)，並傳送 hello 要求、 hello UPN，然後 hello 透過經雙重驗證安全通道的服務主要名稱 (SPN) toohello 連接器。
5. hello 連接器執行與 hello 內部的 Kerberos 限制委派 (KCD) 交涉 AD，模擬 hello 使用者 tooget Kerberos 權杖 toohello 應用程式。
6. Active Directory 會傳送 hello 應用程式 toohello 連接器的 hello Kerberos 權杖。
7. hello 連接器會傳送 hello 原始要求 toohello 使用應用程式伺服器，它收到來自 AD hello Kerberos 權杖。
8. hello 應用程式會傳送 hello 回應 toohello 連接器，然後傳回 toohello 應用程式 Proxy 服務和最後 toohello 使用者。

## <a name="prerequisites"></a>必要條件
您開始使用單一登入 IWA 應用程式之前，請確定您的環境是否準備好以 hello 之後設定和設定：

* 您的應用程式，例如 SharePoint Web 應用程式，設定 toouse 整合式 Windows 驗證。 如需詳細資訊，請參閱[啟用支援 Kerberos 驗證](https://technet.microsoft.com/library/dd759186.aspx)，或者若是使用 SharePoint，請參閱[為 SharePoint 2013 中的 Kerberos 驗證做規劃](https://technet.microsoft.com/library/ee806870.aspx)。
* 您的所有應用程式都有[服務主體名稱](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)。
* hello 伺服器執行 hello 連接器和執行 hello 應用程式的 hello 伺服器是已加入網域且 hello 的相同網域或信任網域。 如需有關加入網域的詳細資訊，請參閱[加入網域的電腦 tooa](https://technet.microsoft.com/library/dd807102.aspx)。
* 執行 hello 連接器 hello 伺服器具有使用者存取 tooread hello TokenGroupsGlobalAndUniversal 屬性。 此預設設定可能會影響安全性強化 hello 環境。

### <a name="configure-active-directory"></a>設定 Active Directory
hello Active Directory 組態會有所不同，取決於您的應用程式 Proxy 連接器和 hello 應用程式伺服器是否在 hello 或不相同的網域。

#### <a name="connector-and-application-server-in-hello-same-domain"></a>連接器和 hello 中的應用程式伺服器相同的網域
1. 在 Active Directory 中，移過**工具** > **使用者和電腦**。
2. 選取 hello 執行 hello 連接器的伺服器。
3. 按一下滑鼠右鍵，然後選取 [屬性] > [委派]。
4. 選取**信任這台電腦所委派 toospecified 服務只**。 
5. 在下**服務 toowhich 此帳戶可以呈送委派的認證**加入 hello hello hello 應用程式伺服器的 SPN 身分識別值。 這可在 AD 中讓 hello 應用程式 Proxy 連接器 tooimpersonate 使用者對 hello hello 清單中所定義的應用程式。

   ![[連接器 SVR 屬性] 視窗螢幕擷取畫面](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>連接器和應用程式伺服器位於不同網域
1. 如需跨網域使用 KCD 的先決條件清單，請參閱 [跨網域的 Kerberos 限制委派](https://technet.microsoft.com/library/hh831477.aspx)。
2. 使用 hello `principalsallowedtodelegateto` hello 連接器伺服器 tooenable hello 應用程式 Proxy toodelegate hello 連接器的伺服器上的屬性。 hello 應用程式伺服器是`sharepointserviceaccount`而且委派伺服器 hello `connectormachineaccount`。 在 Windows 2012 R2 中，以此程式碼作為範例：

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount 可以 hello SPS 電腦帳戶或服務帳戶的 hello 預存程序下執行應用程式集區。

## <a name="configure-single-sign-on"></a>設定單一登入 
1. 將根據 toohello 指示中所述的應用程式發行[發行應用程式 Proxy](application-proxy-publish-azure-portal.md)。 請確定 tooselect **Azure Active Directory**為 hello**預先驗證方法**。
2. Hello 企業應用程式清單中出現您的應用程式之後，請選取它，然後按一下**單一登入**。
3. Hello 單一登入模式設定太**整合式 Windows 驗證**。  
4. 輸入 hello**內部應用程式 SPN** hello 應用程式伺服器。 在此範例中，我們已發行的應用程式的 hello SPN 是 http/www.contoso.com。此服務 toowhich hello 連接器 hello 清單中的 SPN 需求 toobe 可以呈送委派的認證。 
5. 選擇 hello**委派登入身分識別**的 hello 連接器 toouse 代表您的使用者。 如需詳細資訊，請參閱[使用不同的內部部署和雲端身分識別](#Working-with-different-on-premises-and-cloud-identities)

   ![進階應用程式組態](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>非 Windows 應用程式的 SSO
Azure AD 會驗證 hello 雲端中的 hello 使用者時，就會啟動 hello Kerberos 委派流程在 Azure AD Application Proxy。 一旦 hello 要求抵達在內部部署，Azure AD 應用程式 Proxy 連接器發出 Kerberos 票證代表 hello 使用者互動的 hello hello 本機 Active Directory。 此程序是參照的 tooas Kerberos 限制委派 (KCD)。 Hello 中下一個階段中，會將要求傳送 toohello 後端應用程式與這個 Kerberos 票證。 有數個定義如何 toosend 這類要求的通訊協定。 大部分的非 Windows 伺服器會預期 Azure AD 應用程式 Proxy 現在支援的交涉/SPNego。

如需有關 Kerberos 的詳細資訊，請參閱[所有您想要關於 Kerberos 限制委派 (KCD) tooknow](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)。

非 Windows 應用程式通常會使用使用者名稱或 SAM 帳戶名稱，而不是網域的電子郵件地址。 如果這種情況下套用 tooyour 應用程式，您需要 tooconfigure 委派 hello 登入身分識別欄位 tooconnect 雲端身分識別 tooyour 應用程式識別。 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>使用不同的內部部署和雲端身分識別
應用程式 Proxy 會假設使用者是否具有剛好 hello hello 雲端和內部部署中的相同身分識別。 如果不是 hello 情況下，您可以仍然可以使用 KCD 的單一登入。 設定**委派登入身分識別**的單一登入執行時，應該使用哪些身分識別的每個應用程式 toospecify。  

這項功能可讓許多組織可以有不同的內部部署和雲端識別 toohave SSO 從 hello 雲端 tooon 內部部署應用程式而不需要 hello 使用者 tooenter 不同使用者名稱和密碼。 這包括下列組織：

* 就內部而言有多個網域 (joe@us.contoso.com， joe@eu.contoso.com) hello 雲端中的單一定義域 (joe@contoso.com)。
* 在內部有路由的內部網域名稱 (joe@contoso.usa) 和一個法律 hello 雲端中的。
* 請勿在內部使用網域名稱 (joe)
* 使用不同別名由內部部署和 hello 雲端中。 例如：joe-johns@contoso.com 對上 joej@contoso.com  

應用程式 proxy，您可以選取的身分識別 toouse tooobtain hello Kerberos 票證。 這項設定會因應用程式而異。 其中的一些選項適合不接受電子郵件地址格式的系統，另外的選項則設計用於替代登入。

![[委派的登入身分識別] 參數螢幕擷取畫面](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

如果使用委派的登入身分識別，則 hello 值可能不是唯一跨所有 hello 網域或組織中的樹系。 您可以藉由使用兩個不同的連接器群組發佈這些應用程式兩次來避免此問題。 因為每個應用程式都有不同的使用者對象，您可以加入其連接器 tooa 不同的網域。

### <a name="configure-sso-for-different-identities"></a>設定不同身分識別的 SSO
1. 設定 Azure AD Connect 的設定，讓 hello 主要識別是 hello 電子郵件地址 （郵件）。 這是屬於 hello 自訂程序，藉由變更 hello**使用者主體名稱**hello 同步處理設定中的欄位。 這些設定也會決定使用者如何登入 tooOffice365、 Windows10 裝置，以及其他 Azure AD 做為其身分識別存放區的應用程式。  
   ![識別使用者螢幕擷取畫面 - [使用者主體名稱] 下拉式清單](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. 在 hello hello 應用程式的應用程式組態設定您想要 toomodify，選取 hello**委派登入身分識別**toobe 使用：

   * 使用者主體名稱 (例如 joe@contoso.com)
   * 替代使用者主體名稱 (例如 joed@contoso.local)
   * 使用者主體名稱的使用者名稱部分 (例如 joe)
   * 替代使用者主體名稱的使用者名稱部分 (例如 joed)
   * 在內部部署 SAM 帳戶名稱 （取決於 hello 網域控制站設定）

### <a name="troubleshooting-sso-for-different-identities"></a>疑難排解不同身分識別的 SSO
如果 hello SSO 程序中有錯誤，則會出現在 hello 連接器電腦事件記錄檔中所述[疑難排解](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)。
但是，在某些情況下，hello 要求成功傳送 toohello 後端應用程式時，此應用程式回覆中的各種其他 HTTP 回應。 疑難排解這些情況下，應該藉由檢查事件編號 24029 hello 應用程式 Proxy 的工作階段事件記錄檔中的 hello 連接器電腦上啟動。 hello 用於委派的使用者識別會出現在 hello hello 事件詳細資料中的 「 使用者 」 欄位。 對工作階段記錄 tooturn 選取**顯示分析與偵錯記錄檔**hello 事件檢視器檢視 功能表中。

## <a name="next-steps"></a>後續步驟

* [如何 tooconfigure 應用程式 Proxy 應用程式 toouse Kerberos 限制委派](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [使用應用程式 Proxy 疑難排解您遇到的問題](active-directory-application-proxy-troubleshoot.md)


如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)

