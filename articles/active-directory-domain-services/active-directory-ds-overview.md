---
title: "Azure Active Directory 網域服務的 aaaOverview |Microsoft 文件"
description: "Azure Active Directory Domain Services 概觀"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 0d47178f-773e-45f9-9ff4-9e8cffa4ffa2
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 2b4884b3b8b639fcca438ddbab0bd3361aac53c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services"></a>Azure AD 網域服務
## <a name="overview"></a>概觀
Azure 基礎結構服務可讓您 toodeploy 各種不同的運算解決方案以敏捷的方式。 使用 Azure 虛擬機器中，您可以在幾乎立即部署，而且您必須支付只能由 hello 分鐘。 利用對 Windows、Linux、SQL Server、Oracle、IBM、SAP 和 BizTalk 的支援性，您幾乎可以在所有作業系統上使用任何語言部署所有工作負載。 這些優點可讓您 toomigrate 舊版應用程式部署在內部部署 tooAzure，toosave 上操作費用。

移轉的重要層面內部應用程式 tooAzure 正在處理這些應用程式的 hello 的識別身分需求。 目錄感知應用程式可能依賴 LDAP 讀取或寫入存取 toohello 企業目錄，或依賴 Windows 整合式驗證 （Kerberos 或 NTLM 驗證） tooauthenticate 終端使用者。 在 Windows Server 執行的企業營運 (LOB) 應用程式通常都會部署在已加入網域的電腦，因此只要使用群組原則就能安全地加以管理。 too'lift shift' toohello 在內部部署應用程式的雲端，這些相依性 hello 公司身分識別基礎結構需要 toobe 解析。

系統管理員通常會開啟 tooone 的下列方案 toosatisfy hello 的識別身分需求的應用程式部署在 Azure 中的 hello:

* 部署在 Azure 基礎結構服務和 hello 公司 directory 內部部署中執行的工作負載之間的站對站 VPN 連線。
* 設定使用 Azure 虛擬機器的複本網域控制站來擴充 hello 公司 AD 網域/樹系基礎結構。
* 使用已部署為 Azure 虛擬機器的網域控制站來部署 Azure 中的獨立網域。

這些方法都面臨高成本和管理負擔。 系統管理員是在 Azure 中使用虛擬機器的必要的 toodeploy 網域控制站。 此外，它們需要安全 toomanage、 修補程式、 監視、 備份，且這些虛擬機器進行疑難排解。 VPN 連線 toohello 的 hello 依賴內部部署目錄，導致部署在 Azure toobe 容易遭受 tootransient 網路問題或中斷的工作負載。 這些網路中斷會導致執行時間降低，並減損這些應用程式的可靠性。

我們設計 Azure AD 網域服務 tooprovide 更容易的替代方式。

## <a name="introducing-azure-ad-domain-services"></a>Azure AD 網域服務簡介
Azure AD 網域服務提供受管理的網域服務，例如：加入網域、群組原則、LDAP、Kerberos/NTLM 驗證，與 Windows Server Active Directory 完全相容。 您可以使用這些網域服務，而您 toodeploy hello 需要、 管理及修補程式 hello 雲端中的網域控制站。 Azure AD 網域服務整合與您現有的 Azure AD 租用戶，因此讓使用者 toolog 中使用其公司認證。 此外，您可以使用現有的群組和使用者帳戶 toosecure 存取 tooresources，以確保較平滑 '增益和-右移' 的內部部署資源 tooAzure 基礎結構服務。

Azure AD 網域服務的功能運作順暢，不論您的 Azure AD 租用戶是僅限雲端或與您的內部部署 Active Directory 同步。

### <a name="azure-ad-domain-services-for-cloud-only-organizations"></a>僅限雲端的組織的 Azure AD 網域服務
僅限雲端的 Azure AD 租用戶 （通常參照的 tooas 管理的租用戶 」） 並沒有任何內部部署身分識別磁碟使用量。 換句話說，使用者帳戶、 密碼和群組成員資格的所有原生 toohello 雲端-也就是建立和管理 Azure AD 中。 考慮一下 Contoso 是僅限雲端的 Azure AD 租用戶。 Hello 下列圖例所示，Contoso 的系統管理員設定虛擬網路在 Azure 基礎結構服務中。 應用程式和伺服器工作負載會部署在 Azure 虛擬機器的此虛擬網路中。 由於 Contoso 是僅限雲端的租用戶，所有的使用者身分識別、其認證和群組成員資格都是在 Azure AD 中建立和管理。

![Azure AD 網域服務概觀](./media/active-directory-domain-services-overview/aadds-overview.png)

Contoso 公司的 IT 系統管理員可以啟用其 Azure AD 租用戶的 Azure AD 網域服務，並選擇 toomake 此虛擬網路中可用的網域服務。 此後，Azure AD 網域服務佈建新的受管理的網域，而使其可 hello 虛擬網路中。 Contoso 的 Azure AD 租用戶中可使用的所有使用者帳戶、群組成員資格和使用者認證，也會在此新建立的網域中可供使用。 這項功能可讓使用者使用其公司認證-例如，當遠端 toodomain 加入機器透過遠端桌面連接的 toohello 網域中的 hello 組織 toosign 中。 系統管理員可以佈建存取 tooresources 使用現有的群組成員資格的 hello 網域中。 Hello 虛擬網路上的虛擬機器中部署的應用程式可以使用功能，例如加入網域、 LDAP 讀取、 LDAP 繫結、 NTLM 和 Kerberos 驗證，以及群組原則。

Hello 所佈建的 Azure AD 網域服務的受管理網域的幾個要點如下所示：

* Contoso 公司的 IT 系統管理員不需要 toomanage，修補程式，或監視此網域或受管理的網域的任何網域控制站。
* 沒有為此網域需要 toomanage AD 複寫。 使用者帳戶、群組成員資格和來自 Contoso 的 Azure AD 租用戶認證會自動在此受管理的網域中提供。
* 因為 hello 網域受 Azure AD 網域服務中，contoso 公司的 IT 系統管理員沒有這個網域的網域系統管理員或企業系統管理員權限。

### <a name="azure-ad-domain-services-for-hybrid-organizations"></a>混合式組織的 Azure AD 網域服務
具有混合式 IT 基礎結構的組織會混合取用雲端資源和內部部署資源。 這類組織同步處理其在內部部署目錄 tootheir Azure AD 租用戶的身分識別資訊。 混合式組織尋找更多的 toomigrate，其在內部部署應用程式 toohello 雲端，特別是舊版目錄感知應用程式，Azure AD 網域服務是極為有用 toothem。

Litware 的公司已部署[Azure AD Connect](../active-directory/active-directory-aadconnect.md)，toosynchronize 身分識別資訊從其內部部署目錄 tootheir Azure AD 租用戶。 同步處理的 hello 身分識別資訊會包括使用者帳戶、 其認證雜湊，用於驗證 （密碼同步） 與群組成員資格。

> [!NOTE]
> **密碼同步化是必要的 Azure AD 網域服務的混合式組織 toouse**。 這是因為在受管理的 hello 需要使用者的認證提供的 Azure AD 網域服務、 tooauthenticate 透過 NTLM 或 Kerberos 驗證方法，這些使用者的網域。
>
>

![Litware Corporation 的 Azure AD 網域服務](./media/active-directory-domain-services-overview/aadds-overview-synced-tenant.png)

hello 前面的圖例中顯示的混合式 IT 基礎結構，例如 Litware 的公司，組織可以如何使用 Azure AD 網域服務。 Litware 需要網域服務的應用程式和伺服器工作負載會部署在 Azure 基礎結構服務的虛擬網路中。 Litware 的 IT 系統管理員可以啟用其 Azure AD 租用戶的 Azure AD 網域服務，並選擇 toomake 可用在此虛擬網路中受管理的網域。 因為 Litware 是具有混合式 IT 基礎結構的組織，使用者帳戶、 群組和認證會從其內部部署目錄同步處理的 tootheir Azure AD 租用戶。 此功能可讓使用者使用其公司認證 toohello 網域中的 toosign-例如，從遠端連線時 toomachines 聯結 toohello 網域透過遠端桌面。 系統管理員可以佈建存取 tooresources 使用現有的群組成員資格的 hello 網域中。 Hello 虛擬網路上的虛擬機器中部署的應用程式可以使用功能，例如加入網域、 LDAP 讀取、 LDAP 繫結、 NTLM 和 Kerberos 驗證，以及群組原則。

Hello 所佈建的 Azure AD 網域服務的受管理網域的幾個要點如下所示：

* hello 受管理的網域是一個獨立的網域。 它不是 Litware 的內部部署網域的延伸。
* Litware 的 IT 系統管理員不需要 toomanage、 patch 或監視網域控制站的受管理的網域。
* 沒有任何需要 toomanage AD 複寫 toothis 網域。 使用者帳戶、 群組成員資格，以及從 Litware 的內部部署目錄的認證是透過 Azure AD Connect 同步處理的 tooAzure AD。 這些使用者帳戶、 群組成員資格，以及認證會自動提供 hello 受管理的網域內。
* 因為 hello 網域由 Azure AD 網域服務，Litware 的管理的 IT 系統管理員沒有這個網域的網域系統管理員或企業系統管理員權限。

## <a name="benefits"></a>優點
與 Azure AD 網域服務，您可以享用 hello 下列優點：

* **簡單**– 您可以滿足 hello 的識別身分需求的虛擬機器部署簡單按幾下的 tooAzure 基礎結構服務。 請勿需要 toodeploy 和管理 Azure 或安裝程式的連線後 tooyour 在內部部署識別基礎結構中的身分識別基礎結構。
* **整合** - Azure AD 網域服務與 Azure AD 租用戶密切整合。 您現在可以使用 Azure AD 皆代表 toohello 需求您的現代化應用程式和傳統目錄感知應用程式的整合式雲端企業目錄。
* **相容**– 建立 Azure AD 網域服務基礎結構 hello 經過證實的企業等級的 Windows Server Active Directory。 因此，您的應用程式可仰賴相容性更高的 Windows Server Active Directory 功能。 並非 Windows Server AD 中的所有功能目前都可在 Azure AD 網域服務中使用。 不過，可用的功能都與 hello 您需要在您的內部部署基礎結構對應 Windows Server AD 功能相容。 hello LDAP、 Kerberos、 NTLM、 群組原則和網域聯結功能會構成成熟的供應項目測試和精簡透過多種不同的 Windows Server 版本。
* **符合成本效益**– 利用 Azure AD 網域服務，您可以避免與管理身分識別基礎結構 toosupport 傳統目錄感知應用程式相關聯的 hello 基礎結構和管理負擔。 您可以將這些應用程式 tooAzure 基礎結構服務，並受益於能節省更多的營運費用。
