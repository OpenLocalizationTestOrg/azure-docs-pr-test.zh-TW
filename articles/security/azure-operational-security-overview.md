---
title: "aaaAzure 操作安全性概觀 |Microsoft 文件"
description: "本文章提供 hello Azure 操作安全性的概觀。"
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Azure 作業安全性概觀
Azure 操作的安全性是指 toohello 服務、 控制項和功能可用 toousers 保護其資料、 應用程式，以及其他 Microsoft Azure 中的資產。 [Azure 操作安全性](https://docs.microsoft.com/azure/security/azure-operational-security)透過各種不同的功能，包括 Microsoft 安全性開發週期 (SDL)，Microsoft Security hello hello 的唯一 tooMicrosoft 取得結合 hello 知識的架構Response Center 程式和深層感知的 hello 網路安全性威脅架構之下。

Azure 操作安全性概觀本文著重於 hello 下列區域：

- Azure Operations Management Suite
-   Azure 資訊安全中心
-   Azure 監視器
-   Azure 網路監看員
-   Azure 儲存體分析
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
IT 部門負責管理資料中心基礎結構，應用程式和資料，包括 hello 穩定性和這些系統的安全性。 不過，跨通常增加複雜的 IT 環境中取得的安全性深入解析要求組織 toocobble 一起資料從多個安全性與管理系統。

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 是 Microsoft 的雲端式 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。

OMS 是雲端式 IT 管理解決方案，包含許多供應項目，例如 IT 自動化、安全性與合規性、Log Analytics 以及備份與復原。 因此，它是完美的輔助 toomanage 以及保護您的 IT 基礎結構-在內部部署及 hello 雲端中。

OMS hello 核心功能是由一組在 Azure 中執行的服務提供。 每個服務提供特定的管理功能，以及您可以結合服務 tooachieve 不同管理案例。 其中包括：

-   Log Analytics
-   自動化
-   備份
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) 藉由將受控資源中的資料收集到中央儲存機制，以提供 OMS 監視服務。 這項資料可能包括事件、 效能資料或透過 hello API 提供的自訂資料。 一旦收集完成，就有一個 hello 資料適用於警示和分析，並匯出。 這個方法可讓您從各種來源 tooconsolidate 資料讓您可以從您的 Azure 服務結合資料與現有的內部部署環境。 它會從 hello，讓所有動作都都會使用 tooall 種類的資料，該資料上採取的動作也會明確分隔 hello hello 資料集合。

### <a name="automation"></a>自動化
Microsoft [Azure 自動化](https://docs.microsoft.com/azure/automation/automation-intro)對於使用者 tooautomate hello 手動、 長時間執行、 易發生錯誤及經常重複執行工作而經常在雲端和企業環境中提供的方式。 它可以節省時間和可以提升可靠性 hello 的日常管理工作和即使排程這些 toobe 自動定期執行。 您可以使用 Runbook 自動執行程序，或使用「期望狀態設定」自動進行組態管理。

### <a name="backup"></a>備份
[Azure 備份](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup)是 hello Azure 服務，您可以使用最大 tooback （或保護） 和還原您 hello Microsoft 雲端中的資料。 Azure 備份將以一個可靠、安全及具成本競爭力的雲端架構解決方案，取代您現有的內部部署或異地備份解決方案。 Azure 備份提供多個元件，您可以下載並在 hello 適當的電腦上部署伺服器，或在 hello 雲端中。 hello 元件或代理程式，您部署取決於您想要 tooprotect。 Azure 備份的所有元件 （不論是否您要保護資料的內部或 hello 雲端中） 都可以使用的 tooback 資料 tooa 復原服務保存庫在 Azure 中設定。 請參閱 hello [Azure Backup 元件資料表](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use)。

### <a name="site-recovery"></a>站台復原
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)可藉由協調複寫在內部虛擬和實體機器 tooAzure 或 tooa 次要站台提供業務續航力。 如果您主要站台無法使用，您容錯移轉 toohello 次要位置，讓使用者可以繼續工作，並傳回系統傳回 tooworking 順序時，才會失敗。 智慧型和有效的威脅偵測。

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) 是 Microsoft 的全方位「身分識別即服務」(IDaaS) 解決方案，它能夠：

-   讓 IAM 做為雲端服務
-   提供集中式存取管理、單一登入 (SSO) 及報告功能
-   支援的整合式的存取管理[數千個應用程式](https://azure.microsoft.com/marketplace/active-directory/)在 hello 應用程式庫，包括 Salesforce、 Google Apps、 Box、 Concur、 和多個。

Azure AD 也包含一組完整的[身分識別管理功能](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports)，包括[多重要素驗證](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)、[裝置註冊]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview)、[自助式密碼管理](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/)、[自助式群組管理](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password)、[特殊權限的帳戶管理](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure)、[角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)、[應用程式使用量監視](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health)、[豐富的稽核](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs)，以及[安全性監視和警示](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts)。

與 Azure Active Directory，所有應用程式發行您的合作夥伴，且 （商務或取用者） 的客戶有 hello 相同的身分識別和存取管理功能。 這樣做可讓您 toosignificantly 縮減營運成本。

## <a name="azure-security-center"></a>Azure 資訊安全中心
[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-get-started)幫助您防止、 偵測，並以進一步掌握回應 toothreats 及控制 hello 您的 Azure 資源的安全性。 它提供您訂用帳戶之間的整合式安全性監視和原則管理，協助您偵測可能會忽略的威脅，且適用於廣泛的安全性解決方案生態系統。

[資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine)可協助您保護 Azure 中的虛擬機器資料，方法為提供虛擬機器的安全性設定可見性，並監視威脅。 資訊安全中心可以監視虛擬機器以取得︰

-   作業系統 (OS) 安全性設定以 hello 建議組態規則
-   系統安全性和重大更新遺失
-   端點保護建議
-   磁碟加密驗證
-   網路型攻擊

使用 azure 資訊安全中心[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)，這樣會提供[內建角色](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles)toousers、 群組和服務在 Azure 中的可獲指派。

資訊安全中心會評估 hello 和組態都資源 tooidentify 安全性問題的弱點。 資訊安全中心，因此您只看到資訊相關 tooa 資源時指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色。

>[!Note]
>請參閱[Azure 資訊安全中心中的權限](https://docs.microsoft.com/azure/security-center/security-center-permissions)toolearn 深入了解角色與資訊安全中心所允許的動作。

資訊安全中心使用 hello Microsoft Monitoring Agent – 這是的 hello hello Operations Management Suite，記錄分析服務使用相同的代理程式。 從這個代理程式收集的資料會儲存在現有記錄分析[工作區](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access)納入的 hello VM 帳戶 hello 地理位置與您 Azure 訂用帳戶或新 workspace(s)，相關聯。

## <a name="azure-monitor"></a>Azure 監視器
您雲端應用程式中的效能問題可能會對企業產生影響。 透過多個互連的元件和頻繁的發行，隨時都可能導致效能降低。 此外，如果您正在開發應用程式，您的使用者通常會探索到您在測試時未發現的問題。 您應該立即，這些問題的相關資訊，並已進行診斷與修正 hello 問題的工具。

[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor)是用以監視 Azure 上執行之服務的基本工具。 它會提供您相關的服務，且周圍環境的 hello hello 輸送量的基礎結構層級資料。 如果您要管理您的應用程式在 Azure 中，決定是否 tooscale 向上或向下的資源，然後 Azure 監視器可讓您使用什麼 toostart。

此外，您可以使用監視資料 toogain 深入了解有關應用程式。 該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。 其中包括：

-   Azure 活動記錄檔
-   Azure 診斷記錄
-   度量
-   Azure 診斷

### <a name="azure-activity-log"></a>Azure 活動記錄檔
它是提供深入了解您的訂用帳戶中的資源執行的 hello 作業記錄。 hello[活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)先前稱為 「 稽核記錄檔 」 或 「 操作記錄檔 」，因為它會報告您的訂用帳戶的控制平面事件。

### <a name="azure-diagnostic-logs"></a>Azure 診斷記錄
[Azure 診斷的記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)所發出的資源，並提供豐富、 且經常 hello 該資源的作業有關的資料。 這些記錄檔的 hello 內容會因資源類型。

例如，Windows 事件系統記錄是適用於 VM、Blob 和資料表的一個診斷記錄類別，而佇列記錄則是適用於儲存體帳戶的診斷記錄類別。

診斷記錄檔不同 hello [（之前稱為稽核記錄檔或作業記錄檔） 的活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)。 hello 活動記錄檔提供深入了解您的訂用帳戶中的資源執行的 hello 操作。 診斷記錄能讓您了解資源自行執行的作業。

### <a name="metrics"></a>度量
Azure 監視器可讓您 tooconsume 遙測 toogain 掌握 hello 效能和您的工作負載在 Azure 上的健全狀況。 hello Azure 的遙測資料的最重要型別是 hello 度量 （也稱為效能計數器） 發出的大部分的 Azure 資源。 Azure 監視提供數種方式 tooconfigure 和取用這些[度量](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics)監視和疑難排解。

### <a name="azure-diagnostics"></a>Azure 診斷
它是在啟用 hello 集合上部署的應用程式的診斷資料的 Azure 中的 hello 功能。 您可以使用 hello 診斷延伸模組，從各種不同的來源。 目前支援 [Azure 雲端服務 Web 和背景工作角色](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service)、執行 Microsoft Windows 的 [Azure 虛擬機器](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service)，以及 [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics)。


## <a name="network-watcher"></a>網路監看員
客戶可藉由安排和組合各種個別的網路資源 (例如 VNet、ExpressRoute、應用程式閘道、負載平衡器等等)，在 Azure 中建置端對端網路。 使用每個 hello 網路資源的監視。

hello 結束 tooend 網路可具有複雜的組態和資源，建立複雜的案例需要的案例為基礎的監視透過網路監看員之間的互動。

[網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)會簡化 Azure 網路的監視和診斷。 適用於您 tootake 遠端擷取封包在 Azure 虛擬機器上，網路監看員啟用的診斷和視覺效果工具深入了解您的網路流量使用流程記錄和診斷 VPN 閘道與連線。

網路監看員目前具有下列功能的 hello:

- [拓樸](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview)-提供網路層級檢視顯示 hello 各種 connect 和資源群組中的網路資源之間的關聯。
-   [變數封包擷取](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview)：擷取進出虛擬機器的封包資料。 進階篩選選項和微調的控制項，例如無法 tooset 加上時間和大小限制會提供彈性。 hello 封包資料可以儲存在 blob 存放區或 hello.cap 格式的本機磁碟上。
-   [IP 流量驗證](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - 以流量資訊 5-tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 作為基礎，檢查是否允許或拒絕封包。 如果安全性群組遭拒絕 hello 封包，hello 規則，並拒絕 hello 封包的群組會傳回。
-   [下一個躍點](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview)-決定 hello 封包路由傳送 hello Azure 網路網狀架構，讓您 toodiagnose 任何設定錯誤的使用者定義的路由中下一個躍點。
-   [安全性的群組檢視](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview)-取得 hello 有效且套用安全性規則，可在 VM 上套用。
-   [NSG 流程記錄](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview)-網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。 hello 流程是由 5-tuple 資訊 – 來源 IP、 目的地 IP、 來源連接埠，目的地連接埠和通訊協定定義。
-   [虛擬網路閘道與連接疑難排解](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)-提供 hello 能力 tootroubleshoot 虛擬網路閘道與連線。
-   [訂用帳戶限制的網路](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)-可讓您限制對 tooview 網路資源使用狀況。
-   [設定診斷記錄](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)– 提供單一窗格 tooenable 或停用網路資源的資源群組中的診斷記錄檔。

更多如何查看 tooconfigure 網路監看員，toolearn[設定網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-create)。

## <a name="developer-operations-devops"></a>開發人員作業 (DevOps)
先前 tooDevOps 應用程式開發，小組所負責收集軟體程式的商務需求，並撰寫程式碼。 然後個別的 QA 小組測試 hello 程式在隔離式的開發環境中，如果已符合需求，並釋放 hello 作業 toodeploy 的程式碼。 hello 部署團隊進一步片段化成類似網路功能與資料庫筒倉式群組。 每次軟體程式"擲回透過 hello 牆"tooan 獨立的小組，它會新增瓶頸。

[DevOps](https://www.visualstudio.com/learn/what-is-devops/)可讓小組 toodeliver 更安全、 更高品質的解決方案更快速，且成本較低。 使用軟體與服務時，客戶預期能獲得動態且可靠的經驗。  小組在軟體更新必須快速地逐一查看測量 hello 影響 hello 更新並迅速開發新的反覆項目 tooaddress 問題或提供更多的值。  諸如 Microsoft Azure 的雲端平台已移除傳統的瓶頸，並協助基礎結構獲得更高價值。 軟體 reigns 中每一項業務為 hello 主要區分在於與業務的結果中的因數。 沒有組織、 developer 或 IT 工作者可以或應該避免 hello DevOps 移動。

成熟的 DevOps 從業採用下列做法 hello 數。 這些做法[涉及人員](https://www.visualstudio.com/learn/what-is-devops-culture/)tooform 策略根據 hello 的商務案例。  工具可以協助自動 hello 各種作法：

-   [Agile 計劃和專案管理](https://www.visualstudio.com/learn/what-is-agile/)技術會使用的 tooplan 和隔離進入短期衝刺的工作、 管理小組的產能，以及協助小組快速地適應 toochanging 商務需求。
-   [版本控制，通常會有 Git](https://www.visualstudio.com/learn/what-is-git/)，可讓小組 hello world tooshare 來源中任何位置，並與軟體開發工具 tooautomate hello 發行管線整合。
-   [持續整合](https://www.visualstudio.com/learn/what-is-continuous-integration/)磁碟機 hello 進行中的合併和程式碼，而導致 toofinding 缺失早期測試。  其他優點包括減少對抗合併問題的時間，以及開發小組的快速意見反應。
-   [持續傳遞](https://www.visualstudio.com/learn/what-is-continuous-delivery/)軟體解決方案 tooproduction 和測試環境協助組織快速修正的 bug 及回應 tooever 變更商務需求。
-   執行中應用程式的[監視](https://www.visualstudio.com/learn/what-is-monitoring/)包括應用程式健康情況的生產環境以及客戶的使用方式，能協助組織產生假設並快速驗證或反駁策略。  擷取豐富的資料並以各種記錄格式加以儲存。
-   [基礎結構程式碼 (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/)是可啟用 hello 自動化和驗證的建立和清除作業，以提供安全且穩定裝載平台的應用程式的網路和虛擬機器 toohelp 作法。
-   [Microservices](https://www.visualstudio.com/learn/what-are-microservices/)架構會運用 tooisolate 商務使用案例，為小可重複使用的服務。  此架構能提升延展性和效率。

## <a name="next-steps"></a>後續步驟
toolearn 深入了解 OMS 安全性和稽核解決方案，請參閱下列文章 hello:

- [Operations Management Suite | 安全性與合規性](https://www.microsoft.com/cloud-platform/security-and-compliance)。
- [Operations Management Suite 安全性和稽核解決方案中的監視和回應 tooSecurity 警示](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts)。
- [在 Operations Management Suite 安全性和稽核解決方案內監視資源](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources)。
