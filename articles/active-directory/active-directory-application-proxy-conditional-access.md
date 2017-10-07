---
title: "aaaConditional 存取 tooon 內部部署應用程式的 Azure AD |Microsoft 文件"
description: "涵蓋應用程式的條件式存取 tooset 您如何發行 toobe 從遠端使用存取 Azure AD Application Proxy。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 中的條件式存取

>[!NOTE]
>本文適用於 toohello Azure 傳統入口網站，其已遭到淘汰。 我們建議您改用 hello [Azure 入口網站](https://portal.azure.com)。 Hello Azure 入口網站，在應用程式的應用程式 Proxy hello 相同的條件式存取功能任何其他 SaaS 應用程式。 toolearn 進一步了解條件式存取，請參閱[開始使用 Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal-get-started.md)。

您可以設定存取規則 toogrant 條件式存取 tooapplications 應用程式 Proxy 發行。 這可讓您：

* 要求各應用程式的多重要素驗證
* 只在使用者不在公司時要求多重要素驗證
* 禁止使用者存取不在工作的 hello 應用程式

這些規則可以套用的 tooall 使用者和群組或只 toospecific 使用者和群組。 根據預設 hello 規則適用於 tooall 使用者擁有存取 toohello 應用程式。 不過 hello 規則也可以限制的 toousers 屬於指定之安全性群組的成員。  

當使用者存取使用 OAuth 2.0、OpenID Connect、SAML 或 WS-同盟的同盟應用程式時，就會評估存取規則。 此外，存取規則會評估使用 OAuth 2.0 和 OpenID Connect，重新整理權杖時使用的 tooacquire 存取權杖。

## <a name="conditional-access-prerequisites"></a>條件式存取的先決條件
* 訂用帳戶 tooAzure Active Directory Premium
* 同盟或受管理的 Azure Active Directory 租用戶
* 同盟租用戶需要 Multi-Factor Authentication (MFA)  
    ![設定存取規則 - 要求 Multi-Factor Authentication](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>設定每個應用程式的 Multi-Factor Authentication
1. 登入為系統管理員可以在 hello Azure 傳統入口網站。
2. 請 tooActive 目錄並選取您想在其中 tooenable 應用程式 Proxy 的 hello 目錄。
3. 按一下**應用程式**和捲動 toohello**存取規則**> 一節。 hello 存取規則區段只出現在應用程式 Proxy 發行應用程式，使用同盟的驗證。
4. 選取以啟用 hello 規則**啟用存取規則**太**上**。
5. 指定 hello 使用者和群組 toowhom hello 套用規則。 使用 hello**加入群組**按鈕 tooselect toowhich hello 存取規則套用的一或多個群組。 此對話方塊也可以使用的 tooremove 選取群組。  僅適用於使用者隸屬的 hello 指定 tooone hello 存取規則選取的 tooapply toogroups hello 規則時，會強制執行安全性的群組。  

   * tooexplicitly 排除安全性的群組 hello 規則檢查**除了**並指定一個或多個群組。 Hello，除了清單中成員的使用者不是群組的必要的 tooperform 多重要素驗證。  
   * 如果使用者已設定為使用 hello 每位使用者的多重要素驗證功能，這項設定會優先於 hello 應用程式多因素驗證規則。 已設定的每個使用者的多重要素驗證的使用者是必要的 tooperform 多重要素驗證，即使它們有 hello 應用程式的多因素驗證規則的豁免。 深入了解 [多重要素驗證和每個使用者設定](../multi-factor-authentication/multi-factor-authentication.md)。
6. 選取您想 tooset hello 存取規則：

   * **需要多重要素驗證**: toowhom 存取規則套用的使用者都是必要的 toocomplete 多重要素驗證之前存取 hello 應用 toowhich hello 規則適用於。
   * **需要多重要素驗證，不在工作時**： 嘗試從受信任的 IP 位址的 tooaccess hello 應用程式的使用者並不會需要的 tooperform 多重要素驗證。 hello 受信任的 IP 位址範圍可以設定 hello 多因素驗證設定 頁面上。
   * **封鎖存取不在工作時**： 嘗試 tooaccess hello 應用程式從您的公司網路外部的使用者並不會無法 tooaccess hello 應用程式。

## <a name="configuring-mfa-for-federation-services"></a>設定同盟服務的 MFA
同盟租用戶，multi-factor authentication (MFA) 可能會執行由 Azure Active Directory 或 hello 在內部部署 AD FS 伺服器。 根據預設，MFA 會發生在 Azure Active Directory 所裝載的任何頁面上。 tooconfigure MFA 內部，執行 Windows PowerShell，並使用 hello – SupportsMFA 屬性 tooset hello Azure AD 模組。

hello 下列範例示範如何 tooenable 內部部署 MFA 使用 hello [Set-msoldomainfederationsettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) hello contoso.com 租用戶上：`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

在加法 toosetting 此旗標，hello 同盟租用戶 AD FS 執行個體必須設定 tooperform multi-factor authentication。 請依照指示 hello [Microsoft Azure 多重要素驗證在內部部署](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。

## <a name="see-also"></a>另請參閱
* [使用宣告感知應用程式](active-directory-application-proxy-claims-aware-apps.md)
* [使用應用程式 Proxy 發行應用程式](active-directory-application-proxy-publish.md)
* [啟用單一登入](active-directory-application-proxy-sso-using-kcd.md)
* [使用您自己的網域名稱發行應用程式](active-directory-application-proxy-custom-domains.md)

如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)
