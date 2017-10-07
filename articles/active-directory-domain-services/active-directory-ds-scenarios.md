---
title: "Azure Active Directory Domain Services：部署案例 | Microsoft Docs"
description: "Azure AD 網域服務的部署案例"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>部署案例和使用案例
在本節中，我們會看一些受益於 Azure Active Directory (AD) 網域服務的部署案例和使用案例。

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>安全、輕鬆管理 Azure 虛擬機器
您可以使用 Azure Active Directory 網域服務 toomanage Azure 虛擬機器，以簡化方式。 Azure 虛擬機器可以加入的 toohello 受管理的網域，因此可讓您 toouse 公司 AD 認證 toolog 中。 這種方法有助於避免認證管理的麻煩，例如維護每個 Azure 虛擬機器上的本機系統管理員帳戶。

也是聯結的 toohello 受管理的網域的伺服器虛擬機器可以受到管理，並且使用群組原則來保護。 您可以套用必要的安全性基準 tooyour Azure 虛擬機器並加以鎖定依據公司的安全性指導方針。 例如，您可以使用群組原則管理功能 toorestrict hello 類型的應用程式可啟動這些虛擬機器上。

![流暢的管理 Azure 虛擬機器](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

當伺服器和其他基礎結構達到生命週期結束，Contoso 移動目前裝載於內部部署 toohello 雲端的許多應用程式。 其目前的 IT 標準會強制代管公司應用程式的伺服器必須加入網域，並使用群組原則進行管理。 Contoso 公司的 IT 系統管理員慣用 toodomain 聯結的虛擬機器部署在 Azure 中，toomake 管理更容易。 這麼一來，系統管理員和使用者可以使用他們的公司認證來登入網域。 在 hello 同時，電腦可以是必要的安全性基準使用群組原則設定的 toocomply。 Contoso 想不 toohave toodeploy 監視和管理 Azure toosecure 中的網域控制站 Azure 虛擬機器。 因此，Azure AD 網域服務十分適合這個使用案例。

**部署注意事項**

請考慮下列重點此部署案例中的 hello:

* Azure AD 網域服務所提供的受管理網域依預設會提供單一個一般組織單位 (OU) 結構。 位於單一一般 OU 中所有加入網域的機器。 您不過可能會選擇 toocreate 自訂的 Ou。
* Azure AD 網域服務中內建 GPO 的每個 hello 使用者及電腦的 hello 表單支援簡單的群組原則容器。 您可以建立自訂的 Gpo，並針對目標 toocustom Ou。
* Azure AD 網域服務支援 hello 基底 AD 電腦物件結構描述。 您無法擴充 hello 電腦物件的結構描述。

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>增益 shift 使用 LDAP 繫結驗證 tooAzure 基礎結構服務的內部部署應用程式
![LDAP 繫結](./media/active-directory-domain-services-scenarios/ldap-bind.png)

Contoso 有多年前購自 ISV 的一個內部部署應用程式。 hello 應用程式目前處於維護模式下，由 hello ISV，且 contoso 極為耗費資源要求的變更 toohello 應用程式。 這個應用程式已收集使用網頁表單的使用者認證，然後執行 LDAP 繫結 toohello 來驗證使用者的 web 架構前端公司 Active Directory。 Contoso 希望 toomigrate 此應用程式 tooAzure 基礎結構服務。 最好 hello 應用程式運作一樣，不需要任何變更。 此外，使用者應該是可以 tooauthenticate 使用其現有的公司認證，而且沒有以不同方式需 tooretrain 使用者 toodo 項目。 換句話說，使用者應該注意 hello 應用程式執行所在的而且 hello 移轉應該是透明的 toothem。

**部署注意事項**

請考慮下列重點此部署案例中的 hello:

* 請確定 hello 應用程式不需要 toomodify/寫入 toohello 目錄。 不支援 Azure AD 網域服務所提供的 LDAP 寫入權限 toomanaged 網域。
* 您無法變更密碼，直接針對 hello 受管理的網域。 使用者可以變更其密碼可能是使用 Azure AD 自助式密碼變更機制或針對 hello 在內部部署目錄。 這些變更會自動同步處理，並可在 hello 受管理的網域中。

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>增益 shift 的內部部署應用程式，使用 LDAP 讀取 tooaccess hello 目錄 tooAzure 基礎結構服務
Contoso 有大約十年前開發的內部部署企業營運 (LOB) 應用程式。 此應用程式感知的目錄，而且已與 Windows Server AD 設計的 toowork。 hello 應用程式會使用 LDAP （輕量型目錄存取通訊協定） tooread 資訊/屬性有關從 Active Directory 的使用者。 hello 應用程式不會修改屬性或否則寫入 toohello 目錄。 Contoso 希望 toomigrate 此應用程式 tooAzure 基礎結構服務和淘汰 hello 過時在內部部署硬體目前裝載此應用程式。 無法重新寫入的 toouse 現代目錄應用程式開發介面，例如 hello 以 REST 為基礎的 Azure AD Graph API hello 應用程式。 因此，增益 shift 選項需要透過 hello 應用程式可以移轉的 toorun hello 雲端，而不需要修改程式碼或重寫 hello 應用程式中。

**部署注意事項**

請考慮下列重點此部署案例中的 hello:

* 請確定 hello 應用程式不需要 toomodify/寫入 toohello 目錄。 不支援 Azure AD 網域服務所提供的 LDAP 寫入權限 toomanaged 網域。
* 請確定 hello 應用程式不需要自訂/擴充的 Active Directory 架構。 Azure AD 網域服務中不支援結構描述延伸模組。

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>移轉內部部署服務或協助程式的應用程式 tooAzure 基礎結構服務
某些應用程式所組成的多層模式，其中一個的 hello 層需要 tooperform 驗證的呼叫 tooa 例如資料庫層的後端層。 Active Directory 服務帳戶通常會用於這些使用案例。 您可以增益 shift 這類應用程式 tooAzure 基礎結構服務和使用 hello 身分識別需求，這些應用程式的 Azure AD 網域服務。 您可以選擇 toouse hello 相同的服務帳戶從您的內部部署目錄 tooAzure AD 同步處理。 或者，您可以先建立自訂的 OU，然後建立個別的服務帳戶在該 OU，toodeploy 這類應用程式。

![使用 WIA 的服務帳戶](./media/active-directory-domain-services-scenarios/wia-service-account.png)

Contoso 有自訂內建的軟體保存庫應用程式，其中包含 Web 前端、SQL 伺服器和後端 FTP 伺服器。 Windows 整合式驗證的服務帳戶是使用的 tooauthenticate hello web 前端 toohello FTP 伺服器。 hello web 前端設定 toorun，做為服務帳戶。 hello 後端伺服器設定 tooauthorize hello 服務帳戶存取的權限 hello web 前端。 Contoso 偏好不 toohave toodeploy 網域控制站中的虛擬機器 hello 雲端 toomove 此應用程式 tooAzure 基礎結構服務。 Contoso 公司的 IT 系統管理員可以部署 hello 伺服器主控 hello web 前端、 SQL server 和 hello FTP 伺服器 tooAzure 虛擬機器。 這些機器是然後聯結的 tooan Azure AD 網域服務受管理的網域。 然後，他們可以使用 hello 相同的服務帳戶，在他們的內部部署目錄進行 hello 應用程式驗證。 此服務帳戶是已同步處理的 toohello Azure AD 網域服務受管理的網域，而且可供使用。

**部署注意事項**

請考慮下列重點此部署案例中的 hello:

* 請確定 hello 應用程式會使用使用者名稱/密碼進行驗證。 Azure AD 網域服務不支援憑證/智慧卡式驗證。
* 您無法變更密碼，直接針對 hello 受管理的網域。 使用者可以變更其密碼可能是使用 Azure AD 自助式密碼變更機制或針對 hello 在內部部署目錄。 這些變更會自動同步處理，並可在 hello 受管理的網域中。

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Azure 中的 Windows Server 遠端桌面服務部署
您可以使用 Azure AD 網域服務 tooprovide 管理 AD 網域服務 tooyour 遠端桌面伺服器部署在 Azure 中。

如需此部署案例的詳細資訊，請參閱如何太[RDS 部署與整合 Azure AD 網域服務](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds)。
