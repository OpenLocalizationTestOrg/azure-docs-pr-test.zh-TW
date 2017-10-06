---
title: "Azure AD 網域服務： 比較 Azure AD 網域服務 tooDIY 網域控制站 |Microsoft 文件"
description: "比較 Azure Active Directory 網域服務 tooDIY 網域控制站"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 165249d5-e0e7-4ed1-aa26-91a05a87bdc9
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: maheshu
ms.openlocfilehash: 5e384f6a676e76e4f22ff62d4aeb578bc8481ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodecide-if-azure-ad-domain-services-is-right-for-your-use-case"></a>如何 toodecide 如果 Azure AD 網域服務是最適合您的使用案例
與 Azure AD 網域服務中，您可以部署您的工作負載在 Azure 基礎結構服務中，而不需要維護 Azure 中的身分識別基礎結構的相關 tooworry。 此受管理的服務不同於您自行部署及管理的典型 Windows Server Active Directory 部署。 hello 服務是簡單 toodeploy，並提供自動化的健全狀況監視和修復。 我們會持續演變常見部署案例的 hello 服務 tooadd 的支援。

toodecide toouse Azure AD 網域服務是否我們建議您遵循讀取資料的 hello:

* 請參閱 hello 清單[Azure AD 網域服務 」 所提供的功能](active-directory-ds-features.md)。
* 檢閱常見 [Azure AD 網域服務的部署案例](active-directory-ds-scenarios.md)。
* 最後，[比較 Azure AD 網域服務 tooa 自助式 AD 選項](active-directory-ds-comparison.md#compare-azure-ad-domain-services-to-diy-ad-domain-in-azure)。

## <a name="compare-azure-ad-domain-services-toodiy-ad-domain-in-azure"></a>比較在 Azure 中的 Azure AD 網域服務 tooDIY AD 網域
hello 表可協助您使用 Azure AD 網域服務與管理您自己在 Azure 中的 AD 基礎結構之間做決定。

| **功能** | **Azure AD 網域服務** | **Azure VM 中的「自己動手做」AD** |
| --- |:---:|:---:|
| [**受管理的服務**](active-directory-ds-comparison.md#managed-service) |**&#x2713;** |**&#x2715;** |
| [**安全的部署**](active-directory-ds-comparison.md#secure-deployments) |**&#x2713;** |系統管理員必須 toosecure hello 部署。 |
| [**DNS 伺服器**](active-directory-ds-comparison.md#dns-server) |**&#x2713;** (受管理的服務) |**&#x2713;** |
| [**Domain or Enterprise administrator privileges**](active-directory-ds-comparison.md#domain-or-enterprise-administrator-privileges) |**&#x2715;** |**&#x2713;** |
| [**加入網域**](active-directory-ds-comparison.md#domain-join) |**&#x2713;** |**&#x2713;** |
| [**使用 NTLM 和 Kerberos 的網域驗證**](active-directory-ds-comparison.md#domain-authentication-using-ntlm-and-kerberos) |**&#x2713;** |**&#x2713;** |
| [**Kerberos 限制委派**](active-directory-ds-comparison.md#kerberos-constrained-delegation)|資源型|資源型與帳戶型|
| [**自訂 OU 結構**](active-directory-ds-comparison.md#custom-ou-structure) |**&#x2713;** |**&#x2713;** |
| [**結構描述延伸模組**](active-directory-ds-comparison.md#schema-extensions) |**&#x2715;** |**&#x2713;** |
| [**AD 網域/樹系信任**](active-directory-ds-comparison.md#ad-domain-or-forest-trusts) |**&#x2715;** |**&#x2713;** |
| [**LDAP read**](active-directory-ds-comparison.md#ldap-read) |**&#x2713;** |**&#x2713;** |
| [**安全的 LDAP (LDAPS)**](active-directory-ds-comparison.md#secure-ldap) |**&#x2713;** |**&#x2713;** |
| [**LDAP write**](active-directory-ds-comparison.md#ldap-write) |**&#x2715;** |**&#x2713;** |
| [**Group Policy**](active-directory-ds-comparison.md#group-policy) |**&#x2713;** |**&#x2713;** |
| [**地理位置分散部署**](active-directory-ds-comparison.md#geo-dispersed-deployments) |**&#x2715;** |**&#x2713;** |

#### <a name="managed-service"></a>受管理的服務
Azure AD 網域服務網域是由 Microsoft 管理。 您沒有 tooworry 有關修補程式更新、 監視、 備份，以及確保可用性，您的網域。 這些管理工作是 Microsoft Azure 針對受管理網域提供的服務。

#### <a name="secure-deployments"></a>安全的部署
hello 受管理的網域安全地鎖定根據 Microsoft 的 AD 部署的安全性建議。 這些建議源自 hello AD 產品小組的數十年的經驗，工程及支援部署 AD。 自助式部署中，您需要 tootake 特定部署步驟 toolock 清單/安全部署。

#### <a name="dns-server"></a>DNS 伺服器
Azure AD 網域服務管理的網域包含受管理的 DNS 服務。 Hello ' AAD DC Administrators' 群組的成員可以管理受管理的 hello 網域上的 DNS。 此群組的成員會將 DNS 管理的完整權限給 hello 受管理的網域。 可以使用 hello DNS 管理主控台 hello 遠端伺服器管理工具 (RSAT) 封裝中包含執行 DNS 管理。
[詳細資訊](active-directory-ds-admin-guide-administer-dns.md)

#### <a name="domain-or-enterprise-administrator-privileges"></a>網域或企業系統管理員權限
AAD DS 受管理網域上不提供這些提高的權限。 無法對 AAD-DS 受管理的網域部署需要這些提高權限的應用程式。 較小的系統管理權限的子集是名為 ' AAD DC Administrators' hello 委派的系統管理群組的可用 toomembers。 這些權限包含權限 tooconfigure DNS、 設定群組原則，取得已加入網域的機器等上的系統管理員權限。

#### <a name="domain-join"></a>加入網域
您可以將虛擬機器加入 toohello 管理網域的類似 toohow 加入電腦 tooan AD 網域。

#### <a name="domain-authentication-using-ntlm-and-kerberos"></a>使用 NTLM 和 Kerberos 的網域驗證
與 Azure AD 網域服務，您可以使用您的公司認證 tooauthenticate 與 hello 受管理的網域。 憑證會與您的 Azure AD 租用戶保持同步。 同步處理的租用戶，Azure AD Connect 可確保變更 toocredentials 進行內部部署同步的 tooAzure AD。 自助式網域安裝程式中，您可能需要 tooset AD 網域與您內部部署信任的 AD 使用者 tooauthenticate 利用其公司認證。 或者，您可能需要 tooset AD 複寫 tooensure 使用者密碼同步處理 tooyour Azure 網域控制站虛擬機器上。

#### <a name="kerberos-constrained-delegation"></a>Kerberos 限制委派
在 Active Directory Domain Services 的受管理網域上，您沒有「網域系統管理員」權限。 因此，您無法設定帳戶型 (傳統) Kerberos 限制委派。 不過，您可以設定更安全的 hello 資源型限制委派。
[詳細資訊](active-directory-ds-enable-kcd.md)

#### <a name="custom-ou-structure"></a>自訂 OU 結構
Hello ' AAD DC Administrators' 群組的成員可以建立自訂受管理的 hello 網域內的 Ou。 建立自訂的 Ou 的使用者授與完整系統管理權限透過 hello OU。
[詳細資訊](active-directory-ds-admin-guide-create-ou.md)

#### <a name="schema-extensions"></a>結構描述延伸模組
您無法擴充 hello Azure AD 網域服務受管理網域的基底結構描述。 因此，依賴 tooAD 結構描述擴充功能 （例如，新屬性 hello 使用者物件下） 的應用程式無法提高，而且移位 tooAAD DS 網域。

#### <a name="ad-domain-or-forest-trusts"></a>AD 網域或樹系信任
受管理的網域不能設定的 tooset 向上 （輸入/輸出） 與其他網域的信任關係。 因此，資源樹系部署案例無法使用 Azure AD Domain Services。 同樣地，您希望不 toosynchronize 密碼 tooAzure AD 位置的部署無法使用 Azure AD 網域服務。

#### <a name="ldap-read"></a>LDAP 讀取
hello 管理網域支援 LDAP 讀取工作負載。 因此，您可以部署執行 LDAP hello 受管理的網域的讀取作業的應用程式。

#### <a name="secure-ldap"></a>安全的 LDAP
您可以設定 Azure AD 網域服務 tooprovide 安全 LDAP 存取 tooyour 受管理網域，包括透過 hello 網際網路。
[詳細資訊](active-directory-ds-admin-guide-configure-secure-ldap.md)

#### <a name="ldap-write"></a>LDAP 寫入
hello 受管理的網域僅供唯讀之使用者物件。 因此，執行對屬性 hello 使用者物件的 LDAP 寫入作業的應用程式不適用於受管理的網域。 此外，使用者無法變更密碼從 hello 受管理的網域內。 另一個範例會修改群組成員資格或群組內 hello 受管理的網域，但不允許這樣的屬性。 不過，任何變更 toouser 屬性或在 Azure AD （透過 PowerShell/Azure 入口網站） 中所做的密碼或在內部部署 AD 同步處理 toohello AAD DS 受管理的網域。

#### <a name="group-policy"></a>群組原則
沒有內建每個所需的 GPO hello 「 AADDC 電腦 」 和 「 AADDC 使用者 」 容器。 您可以自訂這些內建的 Gpo tooconfigure 群組原則。 Hello ' AAD DC Administrators' 群組的成員也可以建立自訂的 Gpo，並將其連結 tooexisting Ou （包括自訂的 Ou）。
[詳細資訊](active-directory-ds-admin-guide-administer-group-policy.md)

#### <a name="geo-dispersed-deployments"></a>分散各地的部署
Azure AD 網域服務受管理網域可以在Azure 的單一虛擬網路中使用。 需要網域控制站 toobe 可用在多個 Azure 區域 hello 世界各地的情況下，設定在 Azure IaaS Vm 中的網域控制站可能 hello 佳替代方式。


## <a name="do-it-yourself-diy-ad-deployment-options"></a>「自己動手做」(DIY) AD 部署選項
您可能需要部署使用案例，您需要的一些 hello 所安裝的 Windows Server AD 提供的功能。 在這些情況下，請考慮下列自助式 (DIY) 選項的 hello:

* **獨立雲端網域︰** 您可以使用已設定為網域控制站的 Azure 虛擬機器來設定獨立「雲端網域」。 此基礎結構不會與內部部署 AD 環境整合。 此選項需要一組不同的 「 雲端認證 」 toologin/管理 hello 雲端中的 Vm。
* **資源樹系部署：**您可以設定的網域在 hello 資源樹系拓撲中，使用 Azure 虛擬機器設定為網域控制站。 接下來，您可以設定與內部部署 AD 環境的 AD 信任關係。 您可以加入網域的電腦 (Azure Vm) toothis 資源樹系 hello 雲端中。 使用者驗證發生在 [VPN/ExpressRoute 連線 tooyour 在內部部署目錄。
* **延伸您在內部部署網域 tooAzure:**您可以使用 VPN/ExpressRoute 連接 Azure 虛擬網路 tooyour 在內部部署網路連線。 此安裝程式可讓 Azure Vm toobe 聯結的 tooyour 內部部署 AD。 另一個替代方式是 toopromote 複本網域控制站，您的內部部署網域在 Azure 中作為 VM。 您可以再設定它 tooreplicate 透過 VPN/ExpressRoute 連線 tooyour 在內部部署目錄。 這個部署模式中有效地擴充您的內部部署網域 tooAzure。

> [!NOTE]
> 您可能認為 DIY 選項比較適合您的部署使用案例。 請考慮[分享意見反應](active-directory-ds-contact-us.md)toohelp 我們了解功能可協助您選擇在 hello 未來的 Azure AD 網域服務。 此意見反應可協助我們持續改進您的部署需要 hello 服務 toobetter 花色與使用案例。
>
>

我們已經發行[部署 Windows Server Active Directory 在 Azure 虛擬機器的指導方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)toohelp 簡化 DIY 安裝。

## <a name="related-content"></a>相關內容
* [功能 - Azure AD 網域服務](active-directory-ds-features.md)
* [部署案例 - Azure AD 網域服務](active-directory-ds-scenarios.md)
* [在 Azure 虛擬機器上部署 Windows Server Active Directory 的指導方針](https://msdn.microsoft.com/library/azure/jj156090.aspx)
