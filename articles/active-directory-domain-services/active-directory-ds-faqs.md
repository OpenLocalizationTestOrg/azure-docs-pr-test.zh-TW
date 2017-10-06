---
title: "aaaFAQs-Azure Active Directory 網域服務 |Microsoft 文件"
description: "關於「Azure Active Directory 網域服務」的常見問題集"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services：常見問題集 (FAQ)
此頁面回答常見問題 hello Azure Active Directory 網域服務。 請隨時回來查看最新消息。

### <a name="troubleshooting-guide"></a>疑難排解指南
請參閱 tooour[疑難排解指南](active-directory-ds-troubleshooting.md)解決方案 toocommon 問題發生時的設定或管理 Azure AD 網域服務。

### <a name="configuration"></a>組態
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>我可以針對單一 Azure AD 目錄建立多個網域嗎？
否。 您只能針對單一 Azure AD 目錄，建立由 Azure AD 網域服務所服務的單一網域服務 。  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>是否可以啟用 Azure Resource Manager 虛擬網路中的 Azure AD 網域服務？
否。 Azure AD 網域服務只可以在傳統 Azure 虛擬網路中啟用。 您可以連接 hello 傳統虛擬網路 tooa 資源管理員虛擬網路使用虛擬網路對等互連 toouse 資源管理員的虛擬網路中受管理的網域。

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>我可以在同盟 Azure AD 目錄中啟用 Azure AD Domain Services 嗎？ 我使用 ADFS tooauthenticate 使用者存取 tooOffice 365。 我可以針對此目錄啟用 Azure AD Domain Services 嗎？
否。 Azure AD 網域服務需要存取使用者帳戶、 tooauthenticate 使用者透過 NTLM 或 Kerberos toohello 密碼雜的湊。 在同盟的目錄中，不會儲存密碼雜湊 hello Azure AD 目錄中。 因此，Azure AD Domain Services 不適用於此類 Azure AD 目錄。

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>我可以在訂用帳戶內的多個虛擬網路中使用 Azure AD 網域服務嗎？
hello 服務本身不直接支援此案例。 Azure AD 網域服務一次只能在一個虛擬網路上使用。 不過，您可能設定多個虛擬網路 tooexpose Azure AD 網域服務 tooother 虛擬網路之間的連線。 此文章說明如何 [在 Azure 中連接虛擬網路](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>我是否可以使用 PowerShell 來啟用「Azure AD 網域服務」？
目前不提供「Azure AD 網域服務」的 PowerShell/自動化部署。

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>是 Azure AD 網域服務中 hello 新版 Azure 入口網站可用？
否。 Azure AD 網域服務可以設定只有在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)。 我們預期 hello tooextend 支援[Azure 入口網站](https://portal.azure.com)hello 未來中。

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>可以加入網域控制站 tooan Azure AD 網域服務受管理的網域嗎？
否。 提供 Azure AD 網域服務的 hello 網域是受管理的網域。 您不需要 tooprovision、 設定或管理此網域中的這些活動由 Microsoft 提供做為服務的管理網域控制站。 因此，您無法新增其他網域控制站 （讀寫或唯讀） 的 hello 受管理的網域。

### <a name="administration-and-operations"></a>管理和作業
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>可以為我的受管理網域使用遠端桌面連接 toohello 網域控制站嗎？
否。 您沒有權限 tooconnect toodomain 網域控制站的 hello 透過遠端桌面的受管理網域。 Hello ' AAD DC Administrators' 群組的成員可以管理使用 AD 系統管理工具，例如 hello Active Directory 管理管理中心 (ADAC) 或 AD PowerShell hello 受管理的網域。 這些工具使用 hello [遠端伺服器管理工具] 會安裝在 Windows server 上的功能加入 toohello 受管理的網域。

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>我已經啟用 Azure AD 網域服務。 哪個使用者帳戶使用 toodomain 加入機器 toothis 網域？
' AAD DC Administrators' hello 系統管理群組的成員可以讓機器加入網域。 此外，此群組的成員會授與遠端桌面存取 toomachines 已聯結的 toohello 網域。

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>是否有 hello Azure AD 網域服務所提供的受管理網域的網域系統管理員權限？
否。 您不會授與管理權限 hello 受管理的網域。 ' 網域管理員 」 和 「 企業管理員 」 權限不適用於 toouse hello 網域內。 現有的網域系統管理員或企業系統管理員群組中您的 Azure AD 目錄也會不授與 hello 網域上的網域/企業系統管理員權限。

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>我可以在受管理的網域上使用 LDAP 或其他 AD 系統管理工具來修改群組成員資格嗎？
不可以。 您無法在 Azure AD 網域服務所服務的網域上修改群組成員資格。 這同樣適用於使用者屬性的 hello。 但是，您可能會在 Azure AD 中或內部部署網域上變更群組成員資格或使用者屬性。 這類變更會自動同步處理的 tooAzure AD 網域服務。

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>多久需要變更我讓 toomy Azure AD 目錄 toobe 顯示我受管理的網域？
在您使用 Azure AD UI hello 或 PowerShell 的 Azure AD 目錄中所做的變更會同步處理的 tooyour 受管理的網域。 Hello 背景中執行此同步處理程序。 完成 hello 一次性的初始同步處理目錄之後，它通常約 20 分鐘讓 Azure AD toobe 中所做的變更會反映在受管理的網域。

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>可以擴充 hello 的 hello 受管理的網域，Azure AD 網域服務所提供的結構描述嗎？
否。 hello 結構描述是由 Microsoft 管理的 hello 受管理的網域。 Azure AD 網域服務不支援結構描述延伸模組。

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>是否可以在受管理的網域中修改或新增 DNS 記錄？
是。 「 DNS 管理員 」 權限，授與 hello ' AAD DC Administrators' 群組的成員 toomodify DNS 記錄 hello 受管理的網域中。 他們可以使用電腦執行 Windows Server 聯結的 toohello 受管理的網域，toomanage DNS hello DNS 管理員主控台。 toouse hello DNS 管理員主控台安裝 [DNS 伺服器工具]，即 hello hello 伺服器上 [遠端伺服器管理工具] 選擇性功能的一部分。 如需 [管理、監視及疑難排解 DNS 的公用程式](https://technet.microsoft.com/library/cc753579.aspx) 詳細資訊，可在 TechNet 上取得。

### <a name="billing-and-availability"></a>計費與可用性
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Azure AD 網域服務是付費服務嗎？
是。 如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/active-directory-ds/)。

#### <a name="is-there-a-free-trial-for-hello-service"></a>有免費的試用版的 hello 服務嗎？
此服務包含在 hello azure 免費試用版。 您可以註冊以 [免費試用 Azure 一個月](https://azure.microsoft.com/pricing/free-trial/)。

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>我可以從 Enterprise Mobility Suite (EMS) 中取得 Azure AD 網域服務嗎？ 是否需要 Azure AD Premium toouse Azure AD 網域服務？
否。 Azure AD 網域服務是隨用隨付的 Azure 服務，並不是 EMS 的一部分。 Azure AD Domain Services 可以與所有 Azure AD 版本 (免費、基本及進階) 搭配使用。 計費方式是每小時依據使用量計費。

#### <a name="what-azure-regions-is-hello-service-available-in"></a>哪些 Azure 區域位於 hello 服務？
請參閱 toohello[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)清單頁面 toosee hello Azure AD 網域服務可使用的 Azure 區域。
