---
title: "aaaAzure 安全性管理和監視概觀 |Microsoft 文件"
description: " Azure 提供安全性機制 tooaid hello 管理和監視 Azure 雲端服務和虛擬機器中。  本文概述這些核心安全性功能和服務。 "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Azure 安全性管理和監視概觀
Azure 提供安全性機制 tooaid hello 管理和監視 Azure 雲端服務和虛擬機器中。 本文概述這些核心安全性功能和服務。 提供給每個詳細資料，因此，您可以深入的 tooarticles 時，會提供連結。

您的 Microsoft 雲端服務的 hello 安全性是合作關係與您與 Microsoft 間共用的責任。 共同的責任表示 Microsoft 負責 hello Microsoft Azure 和其資料中心的實體安全性 （透過使用安全性保護，例如鎖定的徽章進入的門、 柵欄和成立條件）。 此外，Azure 會提供強式符合 hello 安全性、 隱私權和相容性需求的客戶嚴苛的 hello 軟體層級的雲端安全性層級。

您擁有您的資料和身分識別、 保護其中的 hello 您在內部部署資源安全性和雲端元件，透過它，您可以控制的安全性，hello hello 責任。 Microsoft 提供您與安全性控制項和功能 toohelp 保護資料和應用程式。 維護安全性的責任的程度為基礎的雲端服務的 hello 型別。

下列圖表中的 hello 摘要說明 Microsoft 和 hello 客戶責任 hello 之間取得平衡。

![共同責任][1]

若要深入了解安全性管理，請參閱 [Azure 的安全性管理](azure-security-management.md)。

以下是本文章涵蓋 hello 核心功能 toobe:

* 角色型存取控制
* 反惡意程式碼
* Multi-Factor Authentication
* ExpressRoute
* 虛擬網路閘道
* Privileged Identity Management
* 身分識別保護
* 資訊安全中心

## <a name="role-based-access-control"></a>角色型存取控制
角色型存取控制 (RBAC) 提供 Azure 資源的更細緻存取權管理。 使用 RBAC 時，您可以授與人員只 hello 少量的所需 tooperform 工作的存取權。  RBAC 也可協助您確保當使用者離開 hello 組織它們會失去存取 tooresources hello 雲端中。

深入了解：

* [有關 RBAC 的 Active Directory 小組部落格](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>反惡意程式碼
有了 Azure，您可以使用反惡意程式碼軟體，例如 Microsoft、 Symantec、 趨勢科技、 McAfee，主要的安全性廠商和 Kaspersky toohelp 來自惡意檔案、 廣告軟體和其他威脅保護您的虛擬機器。

Microsoft 反惡意程式碼提供 hello 能力 tooinstall PaaS 角色和虛擬機器的反惡意程式碼代理程式。 根據 System Center Endpoint Protection，這項功能會使經過證實的內部部署安全性技術 toohello 雲端。

我們也提供深層整合趨勢的[Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ 和[SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ hello Azure 平台的產品。 DeepSecurity 是一種防毒解決方案，SecureCloud 則是一種加密解決方案。 DeepSecurity 會使用擴充功能模型部署在 VM 內。 使用 hello 入口網站 UI 和 PowerShell，您可以選擇 toouse DeepSecurity 新的 Vm 會被調整大小或已部署的現有 Vm 內。

Azure 也支援 Symantec End Point Protection (SEP)。 透過入口網站整合，客戶可以指定其想 toouse 年 9 月，在 VM 內。 9 月可以透過 hello Azure 入口網站的新 VM 上安裝，或可以使用 PowerShell 將現有 VM 上安裝。

深入了解：

* [在 Azure 虛擬機器上部署反惡意程式碼解決方案](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [適用於 Azure 雲端服務和虛擬機器的 Microsoft Antimalware](azure-security-antimalware.md)
* [如何 tooinstall 和設定 Trend Micro Deep Security 作為 Windows VM 上的服務](../virtual-machines/windows/classic/install-trend.md)
* [如何 tooinstall 及 Windows VM 上設定 Symantec Endpoint Protection](../virtual-machines/windows/classic/install-symantec.md)
* [保護 Azure 虛擬機器的新反惡意程式碼選項 - McAfee Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure multi-factor authentication (MFA) 是驗證的程式需要 hello 使用一個以上的驗證方法，並將重要的第二層的安全性 toouser 登入和交易方法。 MFA 有助於保護存取 toodata 和應用程式，同時滿足簡單登入程序的使用者需求。 它可以透過一些驗證選項 (例如電話、文字訊息，或行動應用程式通知或驗證代碼，以及第三方 OATH 權杖) 來提供強大的驗證功能。

深入了解：

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [什麼是 Azure Multi-Factor Authentication？](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure Multi-Factor Authentication 的作用](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的專用私人連接。 透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 CRM Online。 從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。 ExpressRoute 連線不會經過 hello 公用網際網路。 這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。

深入了解：

* [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>虛擬網路閘道
使用 VPN 閘道，也稱為 Azure 虛擬網路閘道，toosend 虛擬網路與內部部署位置之間的網路流量。 它們也是使用的 toosend Azure (VNet 對 VNet) 內的多個虛擬網路之間的流量。  VPN 閘道提供 Azure 與基礎結構之間的跨單位安全連線。

深入了解：

* [關於 VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Azure 網路安全性概觀](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
有時候使用者需要 toocarry 特殊權限的 Azure 資源或其他 SaaS 應用程式中的作業。 這通常表示的組織有 toogive 它們的永久特殊權限存取 Azure Active Directory (Azure AD) 中。 這會提高雲端資源的安全性風險，因為組織無法滴水不漏地監視這些使用者利用其特殊存取權限的所作所為。
此外，如果擁有特殊存取權限的使用者帳戶遭到入侵，這個缺口可能會影響您的整體雲端安全性。 Azure AD Privileged Identity Management 的十分有助於 tooresolve 這項風險降低的權限的 hello 曝光時間並增加可見性使用方式。  

Privileged 的 Identity Management 引進了暫時的系統管理員角色或 「 及時 」 系統管理員存取權，也就是需要的 toocomplete 的啟用程序指派給角色的使用者 hello 概念。 hello 啟動處理程序變更 hello 非作用中 tooactive，從指定的時間週期，例如八個小時的 Azure AD 中的 hello 使用者 tooa 角色指派。

深入了解：

* [Azure AD 特殊權限身分識別管理](../active-directory/active-directory-privileged-identity-management-configure.md)
* [開始使用 Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>身分識別保護
Azure Active Directory (AD) 的識別身分保護，提供合併的檢視可疑的登入活動和潛在弱點 toohelp 保護您的業務。 Identity Protection 會依據跡象偵測使用者和特權 (系統管理員) 身分識別的可疑活動，例如暴力密碼破解攻擊、認證外洩，以及從不明位置或受感染裝置的登入。

藉由提供通知，並建議的補救，識別項保護有助於即時 toomitigate 風險。 它會計算使用者風險嚴重性，並且可以設定風險原則 tooautomatically 保護應用程式存取說明從未來的威脅。

深入了解：

* [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md)
* [第 9 頻道：Azure AD 和身分識別展示：Identity Protection 預覽](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>資訊安全中心
Azure 資訊安全中心可協助您防止、 偵測，並回應 toothreats，，並提供您增加可見性，並控制、 hello 安全性的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

資訊安全中心可協助您最佳化及監視您的 Azure 資源的 hello 安全性：

* 讓您針對您的 Azure 訂用帳戶資源，根據 tooyour toodefine 原則公司的安全性需要而且 hello 的應用程式類型或大小寫的每個訂用帳戶中的 hello 資料。
* 監視 Azure 虛擬機器、 網路功能和應用程式的 hello 狀態。
* 提供一份排列安全性警示，包括從整合式的解決方案，以及您需要 tooquickly hello 資訊調查的夥伴和建議的警示 tooremediate 攻擊。

深入了解：

* [簡介 tooAzure 資訊安全中心](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
