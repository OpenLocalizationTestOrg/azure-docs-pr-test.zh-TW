---
title: "常見問題集 - Azure Active Directory Domain Services | Microsoft Docs"
description: "關於「Azure Active Directory 網域服務」的常見問題集"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: maheshu
ms.openlocfilehash: 1963931f30808e861445c9555a04f933514239c3
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2018
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services：常見問題集 (FAQ)
此頁面會回答有關 Azure Active Directory Domain Services 的常見問題。 請隨時回來查看最新消息。

## <a name="troubleshooting-guide"></a>疑難排解指南
如需設定或管理「Azure AD 網域服務」時會發生之常見問題的解決方式，請參閱[疑難排解指南](active-directory-ds-troubleshooting.md) 。

## <a name="configuration"></a>組態
### <a name="can-i-create-multiple-managed-domains-for-a-single-azure-ad-directory"></a>我可以針對單一 Azure AD 目錄建立多個受控網域嗎？
編號 您只能針對單一 Azure AD 目錄，建立由 Azure AD Domain Services 所服務的單一受控網域服務。  

### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>是否可以啟用 Azure Resource Manager 虛擬網路中的 Azure AD 網域服務？
是。 可以啟用 Azure Resource Manager 虛擬網路中的 Azure AD Domain Services。 不再支援傳統 Azure 虛擬網路建立新的受控網域。

### <a name="can-i-migrate-my-existing-managed-domain-from-a-classic-virtual-network-to-a-resource-manager-virtual-network"></a>是否可以將我現有的受控網域從傳統虛擬網路移轉到 Resource Manager 虛擬網路？
目前不支援。 Microsoft 在未來會提供一個機制，將現有的受控網域從傳統虛擬網路移轉到 Resource Manager 虛擬網路。

### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-csp-cloud-solution-provider-subscription"></a>是否可以在 Azure CSP (雲端方案提供者) 訂用帳戶中啟用 Azure AD Domain Services？
是。 了解如何啟用 [Azure CSP 訂用帳戶中的 Azure AD 網域服務](active-directory-ds-csp.md)。

### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-to-authenticate-users-for-access-to-office-365-and-do-not-synchronize-password-hashes-to-azure-ad-can-i-enable-azure-ad-domain-services-for-this-directory"></a>我可以在同盟 Azure AD 目錄中啟用 Azure AD Domain Services 嗎？ 我使用 ADFS 來驗證使用者存取 Office 365，且不會將密碼雜湊同步至 Azure AD。 我可以針對此目錄啟用 Azure AD Domain Services 嗎？
編號 Azure AD Domain Services 需要存取使用者帳戶的密碼雜湊，以透過 NTLM 或 Kerberos 驗證使用者。 在同盟目錄中，密碼雜湊不是儲存在 Azure AD 目錄中。 因此，Azure AD Domain Services 不適用於此類 Azure AD 目錄。

### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>我可以在訂用帳戶內的多個虛擬網路中使用 Azure AD 網域服務嗎？
服務本身並不直接支援這種情況。 受控網域一次只能在一個虛擬網路上使用。 不過，您可以在多個虛擬網路之間設定連線，以將 Azure AD 網域服務公開至其他虛擬網路。 了解如何[在 Azure 中連線虛擬網路](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。

### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>我是否可以使用 PowerShell 來啟用「Azure AD 網域服務」？
是。 了解[如何使用 PowerShell 啟用 Azure AD 網域服務](active-directory-ds-enable-using-powershell.md)。

### <a name="can-i-enable-azure-ad-domain-services-using-a-resource-manager-template"></a>是否可以使用 Resource Manager 範本啟用 Azure AD Domain Services？
是。 了解[如何使用 PowerShell 啟用 Azure AD 網域服務](active-directory-ds-enable-using-powershell.md)。

### <a name="can-i-add-domain-controllers-to-an-azure-ad-domain-services-managed-domain"></a>可以將網域控制站新增至 Azure AD 網域服務的受控網域嗎？
編號 Azure Active Directory Domain Services 所提供的網域是受控網域。 您不需要佈建、設定或管理此網域的網域控制站 - Microsoft 會以服務形式提供這些管理活動。 因此，您無法為受控網域新增其他網域控制站 (讀寫或唯讀)。

## <a name="administration-and-operations"></a>管理和作業
### <a name="can-i-connect-to-the-domain-controller-for-my-managed-domain-using-remote-desktop"></a>我可以使用遠端桌面連線到我的受控網域的網域控制站嗎？
編號 您沒有權限透過遠端桌面連接至受控網域上的網域控制站。 「AAD DC 系統管理員」群組的成員可以使用 AD 系統管理工具，例如 Active Directory 管理中心 (ADAC) 或 AD PowerShell 來管理受控網域。 這些工具會在加入受控網域的 Windows 伺服器上，使用「遠端伺服器管理工具」功能安裝。

### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-to-domain-join-machines-to-this-domain"></a>我已經啟用 Azure AD 網域服務。 我應該使用哪一個使用者帳戶來將電腦加入此網域？
系統管理群組「AAD DC 系統管理員」的成員都能將電腦加入網域。 此外，此群組的成員會被授與已加入網域之電腦的遠端桌面存取權限。

### <a name="do-i-have-domain-administrator-privileges-for-the-managed-domain-provided-by-azure-ad-domain-services"></a>我有 Azure AD Domain Services 所提供的受控網域的網域系統管理員權限嗎？
編號 您不會取得受控網域的系統管理權限。 您無法在網域內使用「網域系統管理員」和「企業系統管理員」權限。 Azure AD 目錄內現有的網域系統管理員或企業系統管理員群組也不會被授與該網域的網域/企業系統管理員權限。

### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>我可以在受控網域上使用 LDAP 或其他 AD 系統管理工具來修改群組成員資格嗎？
編號 您無法在 Azure AD 網域服務所服務的網域上修改群組成員資格。 這同樣適用於使用者屬性。 但是，您可能會在 Azure AD 中或內部部署網域上變更群組成員資格或使用者屬性。 這類變更會自動同步處理到 Azure AD 網域服務。

### <a name="how-long-does-it-take-for-changes-i-make-to-my-azure-ad-directory-to-be-visible-in-my-managed-domain"></a>我對 Azure AD 目錄所做的變更要多久才會反映在我的受控網域中？
使用 Azure AD UI 或 PowerShell 在您 Azure AD 目錄中進行的變更會同步至您的受控網域。 這個同步處理程序會在背景執行。 在您目錄的單次初始同步處理完成之後，通常需要 20 分鐘的時間，在 Azure AD 中所做的變更才會反映在您的受控網域中。

### <a name="can-i-extend-the-schema-of-the-managed-domain-provided-by-azure-ad-domain-services"></a>可以擴充 Azure AD Domain Services 所提供之受控網域的結構描述嗎？
編號 結構描述是由 Microsoft 針對受控網域進行管理。 Azure AD 網域服務不支援結構描述延伸模組。

### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>是否可以在受控網域中修改或新增 DNS 記錄？
是。 「AAD DC 系統管理員」群組的成員會被授與「DNS 系統管理」權限，以在受控網域中修改 DNS 記錄。 他們可以在加入受控網域且執行 Windows Server 的電腦上，使用 DNS 管理員主控台管理 DNS。 若要使用 DNS 管理員主控台，請安裝 DNS 伺服器工具，這是伺服器上的「遠端伺服器管理工具」選擇性功能的一部分。 如需 [管理、監視及疑難排解 DNS 的公用程式](https://technet.microsoft.com/library/cc753579.aspx) 詳細資訊，可在 TechNet 上取得。

## <a name="billing-and-availability"></a>計費與可用性
### <a name="is-azure-ad-domain-services-a-paid-service"></a>Azure AD 網域服務是付費服務嗎？
是。 如需詳細資訊，請參閱[價格頁面](https://azure.microsoft.com/pricing/details/active-directory-ds/)。

### <a name="is-there-a-free-trial-for-the-service"></a>是否可以免費試用服務？
此服務隨附於 Azure 的免費試用版。 您可以註冊以 [免費試用 Azure 一個月](https://azure.microsoft.com/pricing/free-trial/)。

### <a name="can-i-pause-an-azure-ad-domain-services-managed-domain"></a>我能否暫停 Azure AD Domain Services 受控網域？ 
編號 啟用 Azure AD Domain Services 受控網域後，您選取的虛擬網路中即有該服務可供使用，直到您停用/刪除受控網域為止。 無法暫停服務。 除非您刪除受控網域，否則會以每小時計費。

### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-to-use-azure-ad-domain-services"></a>我可以從 Enterprise Mobility Suite (EMS) 中取得 Azure AD 網域服務嗎？ 我是否需要 Azure AD Premium 才能使用 Azure AD 網域服務？
編號 Azure AD 網域服務是隨用隨付的 Azure 服務，並不是 EMS 的一部分。 Azure AD Domain Services 可以與所有 Azure AD 版本 (免費、基本及進階) 搭配使用。 計費方式是每小時依據使用量計費。

### <a name="what-azure-regions-is-the-service-available-in"></a>哪些 Azure 區域提供此服務？
請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services/)頁面，以查看可使用 Azure AD 網域服務的 Azure 區域清單。
