---
title: "aaaHow tooprovide 安全遠端存取 tooon 內部部署應用程式"
description: "涵蓋如何 toouse Azure AD Application Proxy tooprovide 安全遠端存取 tooyour 內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式

員工目前想 toobe 產能在任何位置，在任何時間，以及從任何裝置。 不管它們是平板電腦、 電話或膝上型電腦，他們想 toowork 自己的裝置上。 以及他們希望 toobe 無法 tooaccess 其應用程式，內部 hello 雲端中的 SaaS 應用程式和公司應用程式。 提供存取 tooon 內部部署應用程式的傳統上會涉及虛擬私人網路 (Vpn) 或非軍事區域 (Dmz)。 不是安全的這些解決方案複雜且困難 toomake 只他們是昂貴的 tooset 及管理。

還有更好的辦法！

Hello 行動優先 （contract-first） 中的現代員工，雲端優先世界需要現代的遠端存取解決方案。 Azure AD 應用程式 Proxy 是 Azure Active Directory 的一項功能，並提供遠端存取做為服務。 這表示它是簡單 toodeploy、 使用和管理。

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>什麼是 Azure Active Directory 應用程式 Proxy？
Azure AD 應用程式 Proxy 針對 Web 應用程式託管的內部部署，提供單一登入 (SSO) 及安全的遠端存取。 您會想 toopublish 某些應用程式包含 SharePoint 網站、 Outlook Web Access 中或任何其他 LOB web 應用程式必須。 這些應用程式與 Azure AD 整合的內部部署 web hello 相同的識別，並控制由 O365 的平台。 使用者可以存取您在內部部署應用程式 hello 與 Azure AD 整合他們存取 O365 和其他 SaaS 應用程式的方式相同。 您不需要 toochange hello 網路基礎結構，或為您的使用者需要 VPN tooprovide 此解決方案。

## <a name="why-is-application-proxy-a-better-solution"></a>為什麼應用程式 Proxy 是較佳的解決方案？
Azure AD 應用程式 Proxy 提供簡單、 安全且符合成本效益的遠端存取解決方案 tooall 在內部部署應用程式。

Azure AD 應用程式 Proxy：

* **簡單**
   * 您不需要 toochange 或更新您的應用程式 toowork 應用程式 proxy。 
   * 使用者享有一致的驗證體驗。 他們可以使用 hello 雲端和您的應用程式內部部署中的 hello MyApps tooget 入口網站單一登入 tooboth SaaS 應用程式。 
* **安全**
   * 當您發行應用程式使用 Azure AD Application Proxy 時，您可以利用的 hello 豐富的授權控制項和安全性分析在 Azure 中。 您會取得雲端級別安全性和 Azure 安全性功能，例如條件式存取和雙步驟驗證。
   * 您不需要 tooopen 任何輸入的連線透過防火牆 toogive 您使用者的遠端存取。 
* **符合成本效益**
   * 應用程式 Proxy 可 hello 雲端中，因此可以節省時間和金錢。 在內部部署解決方案通常需要您 tooset 組成，而維護 Dmz 中，邊緣的伺服器或其他複雜的基礎結構。  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>哪種應用程式可與應用程式 Proxy 搭配運作？
透過 Azure AD 應用程式 Proxy，您可以存取不同類型的內部應用程式︰

* 使用[整合式 Windows 驗證](active-directory-application-proxy-sso-using-kcd.md)來進行驗證的 Web 應用程式  
* 使用表單架構或[標頭型](application-proxy-ping-access.md)存取的 Web 應用程式  
* Web 應用程式開發介面，您想要在不同裝置上的 tooexpose toorich 應用程式  
* 裝載在[遠端桌面閘道](application-proxy-publish-remote-desktop.md)之後的應用程式  
* 豐富型用戶端應用程式與 hello Active Directory 驗證程式庫 (ADAL) 整合

## <a name="how-does-application-proxy-work"></a>Application Proxy 的運作方式為何？
您需要 tooconfigure toomake 應用程式 Proxy 工作的兩個元件： 連接器和外部端點。 

hello 連接器是輕量型的代理程式位於內部網路的 Windows 伺服器上。 hello 連接器有助於 hello 流量從 hello hello 雲端 tooyour 應用程式在內部部署中的應用程式 Proxy 服務。 它只會使用輸出連線，因此您尚未 tooopen 任何輸入連接埠，或將任何項目放在 hello 周邊網路。 hello 連接器是無狀態，並視 hello 雲端提取資訊。 如需連接器的詳細資訊，例如如何負載平衡和驗證，請參閱[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)。 

hello 外部端點會是您的使用者如何到達您的應用程式網路外部。 它們可以是瀏覽直接 tooan 外部 URL，以決定時，或它們可以透過 hello MyApps 入口網站存取 hello 應用程式。 當使用者前往 tooone 這些端點時，它們在 Azure AD 進行驗證，然後透過進行路由傳送嗨連接器 toohello 在內部部署應用程式。

 ![Azure AD 應用程式 Proxy 圖表](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. hello 使用者存取透過 hello 應用程式 Proxy 服務的 hello 應用程式，並會導向的 toohello Azure AD 登入頁面 tooauthenticate。
2. 在成功登入之後，會產生語彙基元，並將其傳送 toohello 用戶端裝置中。
3. hello 用戶端會傳送 hello 語彙基元 toohello 應用程式 Proxy 服務，擷取 hello 使用者主要名稱 (UPN) 和安全性主體名稱 (SPN)，從 hello 權杖，然後會引導 hello 要求 toohello 應用程式 Proxy 連接器。
4. 如果您已設定單一登入，hello 連接器執行代表 hello 使用者所需的任何其他驗證。
5. hello 連接器會傳送 hello 要求 toohello 在內部部署應用程式。  
6. 透過應用程式 Proxy 服務和連接器 toohello 使用者會傳送 hello 回應。

### <a name="single-sign-on"></a>單一登入
Azure AD 應用程式 Proxy 提供單一登入 (SSO) tooapplications 使用整合式 Windows 驗證 (IWA) 」 或 「 宣告感知應用程式。 如果您的應用程式使用 IWA，應用程式 Proxy 會模擬使用 Kerberos 限制委派 tooprovide SSO hello 使用者。 如果您有 Azure Active Directory 的信任的宣告感知應用程式時，SSO 運作，因為已由 Azure AD 驗證 hello 使用者。

如需有關 Kerberos 的詳細資訊，請參閱[所有您想要關於 Kerberos 限制委派 (KCD) tooknow](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd)。

### <a name="managing-apps"></a>管理應用程式
其中一個應用程式發佈應用程式 proxy 時，您可以像是其他任何企業應用程式在 hello Azure 入口網站中加以管理。 您可以使用 Azure Active Directory 安全性功能，例如條件式存取和兩步驟驗證、 控制使用者的權限，以及自訂應用程式的商標 hello。 

## <a name="get-started"></a>開始使用

設定 Application Proxy 之前，確定您有支援的 [Azure Active Directory 版本](https://azure.microsoft.com/pricing/details/active-directory/)，以及您是全域管理員的 Azure AD 目錄。

開始使用 Application Proxy 有兩個步驟：

1. [啟用應用程式 Proxy 及設定 hello 連接器](active-directory-application-proxy-enable.md)。    
2. [發行應用程式](active-directory-application-proxy-publish.md)-使用 hello 快速、 簡易的精靈 tooget 已發行，而且可存取您在內部部署應用程式從遠端。

## <a name="whats-next"></a>後續步驟
您發佈第一個應用程式後，應用程式 Proxy 還有其他更多用途：

* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [使用您自己的網域名稱發行應用程式](active-directory-application-proxy-custom-domains.md)
* [了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)
* [使用現有的內部部署 Proxy 伺服器](application-proxy-working-with-proxy-servers.md) 
* [設定自訂首頁](application-proxy-office365-app-launcher.md)

如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)

