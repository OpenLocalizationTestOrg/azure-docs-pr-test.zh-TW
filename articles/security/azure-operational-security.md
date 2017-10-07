---
title: "aaaAzure 操作安全性 |Microsoft 文件"
description: "了解 Microsoft Operations Management Suite (OMS)、它的服務及運作方式。"
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Azure 作業安全性
## <a name="introduction"></a>簡介

### <a name="overview"></a>概觀
我們知道安全性是 hello 定域機組中的其中一個工作，而且重要，您會看到 Azure 安全性的精確且即時資訊。 Hello 最佳原因 toouse Azure 應用程式與服務的其中一個是 tootake hello 各式各樣的安全性工具和功能的優點。 這些工具和功能協助您更 hello 安全 Azure 平台上可能 toocreate 安全解決方案。 Microsoft Azure 必須提供客戶資料的機密性、完整性和可用性，同時也能釐清責任。

toohelp 客戶深入了解從這兩個 hello 客戶的 Microsoft Azure 內實作的安全性控制項 hello 陣列，並提供寫入 Microsoft 操作檢視方塊，這份技術白皮書，「 Azure 操作安全性 」完整查看適用於 Windows Azure hello 操作安全性的詳細資訊。

### <a name="azure-platform"></a>Azure 平台
Azure 是一個公用雲端服務平台，支援廣泛的作業系統、程式設計語言、架構、工具、資料庫及裝置等選擇。 它可以透過 Docker 整合執行 Linux 容器；使用 JavaScript、Python、.NET、PHP、Java 及 Node.js 建置應用程式；為 iOS、Android 及 Windows 裝置建置後端。 Azure 雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您建置，或移轉到 IT 資產時，您依賴該組織的能力 tooprotect 應用程式和 hello 服務與 hello 控制項資料的公用雲端服務提供者提供 toomanage hello 安全性您雲端架構資產。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂的組織部署的安全性 toomeet hello 獨特需求。 本文件有助於您了解 Azure 安全性功能如何協助您滿足這些需求。

### <a name="abstract"></a>摘要
Azure 操作的安全性是指 toohello 服務、 控制項和功能可用 toousers 保護其資料、 應用程式，以及其他 Microsoft Azure 中的資產。 Azure 操作的安全性是建置在結合 hello 知識透過唯一 tooMicrosoft，包括 hello Microsoft 安全性開發週期 (SDL)，hello Microsoft Security Response Center 各種功能的架構程式及深層 hello 顧慮威脅大環境的認知。

這份技術白皮書說明 Microsoft 的方法 tooAzure 操作安全性內 hello Microsoft Azure 雲端平台和涵蓋下列服務：
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure 網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure 儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) 是 hello hello 混合式雲端 IT 管理解決方案。 單獨使用，或將現有 System Center 部署，OMS，可讓您 tooextend hello 大的彈性和以雲端為基礎的管理基礎結構的控制項。

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

透過 OMS，您就能以低於競爭解決方案的成本來管理任何雲端中的任何執行個體，包括內部部署、Azure、AWS、Windows Server、Linux、VMware 和 OpenStack。 OMS 提供新的方法 toomanaging 建置為 hello 雲端優先世界中，您是 hello 最快速、 最具成本效益的方式 toomeet 新商務面臨的挑戰和配合新的工作負載，應用程式和雲端環境的企業。

### <a name="oms-services"></a>OMS 服務

OMS hello 核心功能是由一組在 Azure 中執行的服務提供。 每個服務提供特定的管理功能，以及您可以結合服務 tooachieve 不同管理案例。

| 服務  | 說明|
| :------------- | :-------------|
| Log Analytics | 監視和分析 hello 可用性和不同的資源，包括實體和虛擬機器的效能。 |
|自動化 | 讓手動程序自動化，並強制設定實體和虛擬機器。 |
| 備份 | 備份及還原重要資料。 |
| Site Recovery | 為重要應用程式提供高可用性。 |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) 藉由將受控資源中的資料收集到中央儲存機制，以提供 OMS 監視服務。 這項資料可能包括事件、 效能資料或透過 hello API 提供的自訂資料。 一旦收集完成，就有一個 hello 資料適用於警示和分析，並匯出。


這個方法可讓您從各種來源 tooconsolidate 資料，因此您可以結合資料從您的 Azure 服務與現有內部部署環境。 它會從 hello，讓所有動作都都會使用 tooall 種類的資料，該資料上採取的動作也會明確分隔 hello hello 資料集合。


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

hello 記錄分析服務會管理雲端架構資料安全地使用下列方法的 hello:
-   資料隔離
-   資料保留
-   實體安全性
-   事件管理
-   法規遵循
-   安全性標準認證

### <a name="azure-backup"></a>Azure 備份

[Azure 備份](http://azure.microsoft.com/documentation/services/backup)提供備份和還原服務與屬於 hello OMS 套件的產品和服務的資料。
它可保護您的應用程式資料並保留數年，而您完全不必投入資本投資，並且只需要最少的營運成本。 它可以將資料從備份實體和虛擬 Windows 伺服器除了 tooapplication 工作負載，例如 SQL Server 和 SharePoint。 它也可由[System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate 受保護資料 tooAzure 為了備援及長期儲存。


Azure 備份中受保護的資料會儲存在位於特定地理區域的備份保存庫中。 hello 資料會複寫在 hello 相同的區域，並根據 hello 保存庫類型，也可能是複寫的 tooanother 區域進一步提供恢復功能。

### <a name="management-solutions"></a>管理解決方案
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) 是 Microsoft 的雲端式 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。


[管理解決方案](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions)是預先封裝的邏輯集合，可使用一或多項 OMS 服務實作特定管理案例。 從 Microsoft 和協力廠商，您可以在 OMS 中輕鬆地加入您的投資 tooyour Azure 訂用帳戶 tooincrease hello 值可使用不同的解決方案。 身為合作夥伴，您可以建立您自己的解決方案 toosupport 應用程式和服務，並提供給他們 toousers 透過 hello Azure Marketplace 或快速啟動範本。


![管理解決方案](./media/azure-operational-security/azure-operational-security-fig4.png)

使用多個服務 tooprovide 其他功能的解決方案的理想範例為 hello[更新管理解決方案](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management)。 這個解決方案會使用 hello[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)有關 Windows 和 Linux toocollect 必要更新每個代理程式上的代理程式。 它會寫入此資料 toohello 記錄分析儲存機制，包含儀表板與分析它。

當您建立的部署中的 runbook [Azure 自動化](https://docs.microsoft.com/azure/automation/automation-intro)使用的 tooinstall 所需的更新。 您管理整個 hello 入口網站中的程序，而不需 tooworry 關於 hello 基礎詳細資料。

## <a name="azure-security-center"></a>Azure 資訊安全中心

Azure 資訊安全中心可協助保護您的 Azure 資源。 它提供您 Azure 訂用帳戶之間的整合式安全性監視和原則管理。 Hello 在服務內，您就可以 toodefine 原則不只是針對您 Azure 訂用帳戶，同時也針對[資源群組](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)，使您能夠更細微。

### <a name="security-policies-and-recommendations"></a>安全性原則和建議

安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。

資訊安全中心，您定義原則根據 tooyour 公司的安全性需求與 hello 類型的應用程式或 hello 資料的機密性。

![安全性原則和建議](./media/azure-operational-security/azure-operational-security-fig5.png)


會自動啟用 hello 訂用帳戶層級中的原則傳播 tooall hello 訂用帳戶內的資源群組中在 hello 右邊 hello 圖表所示：


### <a name="data-collection"></a>資料收集

資訊安全中心會收集從虛擬機器 (Vm) tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。 當您第一次存取資訊安全中心時，訂用帳戶中的所有 VM 都會啟用資料收集。 建議使用資料收集，但您也可以退出關閉 hello 資訊安全中心原則中的資料收集。

### <a name="data-sources"></a>資料來源

- Azure 資訊安全中心會分析資料，從下列來源 tooprovide 可見性為您的安全性狀態的 hello、 識別的弱點可能會建議防護功能，以及偵測到作用中威脅：

-   Azure 服務： 使用您已部署藉由與該服務的資源提供者通訊 hello Azure 服務組態相關資訊。

- 網路流量︰使用從 Microsoft 的基礎結構取樣的網路流量中繼資料，例如來源/目的地 IP/連接埠、封包大小和網路通訊協定。

-   合作夥伴解決方案：使用整合式合作夥伴解決方案 (例如防火牆和反惡意程式碼解決方案) 的安全性警示。

-   您的虛擬機器：使用組態資訊以及安全性事件的相關資訊，例如來自您虛擬機器的 Windows 事件和稽核記錄檔、IIS 記錄檔、syslog 訊息和損毀傾印檔。

### <a name="data-protection"></a>資料保護

toohelp 客戶防止、 偵測及回應 toothreats，Azure 資訊安全中心會收集並處理安全性相關的資料，包括組態資訊、 中繼資料、 事件記錄檔、 損毀傾印檔案，等等。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。

-   **資料隔離**: hello 服務在每個元件上，資料以邏輯方式分開。 每個組織加上標記的所有資料。 這項標記作業在整個 hello 資料生命週期持續發生，它會強制執行各種層級的 hello 服務。

-   **資料存取**: tooprovide 安全性建議和調查潛在的安全性威脅，Microsoft 人員可能存取收集的資訊，或由 Azure 服務，包括損毀傾印檔案，分析處理建立事件，VM 磁碟快照集，可能會不小心包含客戶資料或個人資料與您的虛擬機器的成品。 我們將遵守 toohello [Microsoft Online Services 條款及隱私權聲明](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)的狀態下，Microsoft 不會使用客戶資料，或衍生自它的資訊進行任何廣告或類似的商業用途。

-   **資料使用**： 使用模式，Microsoft 威脅情報看到跨多個租用戶 tooenhance 我們預防和偵測功能之後，我們這樣中所述的 hello 隱私權承諾根據我們[隱私權陳述式](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx)。

### <a name="data-location"></a>資料位置

Azure 資訊安全中心會收集損毀傾印檔案的暫時複本並加以分析，以取得惡意探索嘗試和成功入侵的證明。 Azure 資訊安全中心會執行這項分析內 hello 同一地區，因為 hello 工作區中，並刪除 hello 的暫時副本，當分析完成。 機器成品都會儲存在集中為 hello VM hello 相同的區域。

-   **儲存體帳戶**︰針對執行虛擬機器的每個區域指定儲存體帳戶。 這個控制項可讓您 toostore 資料在 hello 與 hello 虛擬機器收集資料的 hello 相同區域中。

-   **Azure 資訊安全中心儲存體**： 安全性警示，包括夥伴警示、 建議和安全性健全狀況狀態的相關資訊會儲存集中，目前在 hello 美國。 這項資訊可能包括相關的設定資訊及安全性事件收集從您的虛擬機器所需的 tooprovide 您 hello 安全性警示、 建議或安全性健全狀況狀態。


## <a name="azure-monitor"></a>Azure 監視器

hello [OMS 安全性](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources)和稽核解決方案可讓 IT tooactively 監視所有的資源，可協助安全性事件的 hello 影響降到最低。 OMS 安全性和稽核具備可用來監視資源的安全性網域。 hello 安全性網域提供快速存取 toooptions、 更多詳細資料進行安全性監視 hello 涵蓋下列網域：

-   惡意程式碼評估
-   更新評估
-   身分識別與存取。

Azure 監視指標 tooinformation 提供特定類型的資源。 它提供視覺效果、 查詢、 路由、 警示、 自動調整規模及自動化 hello Azure 基礎結構 （活動記錄檔） 從資料和每個個別的 Azure 資源 （診斷記錄檔）。

![Azure 監視器](./media/azure-operational-security/azure-operational-security-fig6.png)


雲端應用程式相當複雜，且具有許多移動組件。 監視提供您的應用程式保持啟動的資料 tooensure 和狀況良好的狀態中執行。 它也可協助您 toostave 關閉潛在的問題或過去的疑難排解。

此外，您可以使用監視資料 toogain 深入了解有關應用程式。 該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。

### <a name="azure-activity-log"></a>Azure 活動記錄檔


它是提供深入了解您的訂用帳戶中的資源執行的 hello 作業記錄。 hello 活動記錄檔先前稱為 「 稽核記錄檔 」 或 「 操作記錄檔 」，因為它會報告您的訂用帳戶的控制平面事件。

![Azure 活動記錄檔](./media/azure-operational-security/azure-operational-security-fig7.png)

使用 hello 活動記錄檔，您可以決定 hello '功能，對象、 及何時' 的任何寫入作業 (PUT、 POST、 DELETE) 在您的訂用帳戶中的 hello 資源。 您也可以了解 hello 狀態 hello 作業以及其他相關的屬性。 hello 活動記錄檔不包括讀取 (GET) 作業或作業，以使用 hello 傳統模式的資源。

### <a name="azure-diagnostic-logs"></a>Azure 診斷記錄

這些記錄檔所發出的資源，並提供豐富、 且經常 hello 該資源的作業有關的資料。 這些記錄檔的 hello 內容會因資源類型。

例如，Windows 事件系統記錄是適用於 VM、Blob 和資料表的一個診斷記錄類別，而佇列記錄則是適用於儲存體帳戶的診斷記錄類別。

診斷記錄檔不同 hello [（之前稱為稽核記錄檔或作業記錄檔） 的活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)。 hello 活動記錄檔提供深入了解您的訂用帳戶中的資源執行的 hello 操作。 診斷記錄能讓您了解資源自行執行的作業。

### <a name="metrics"></a>度量

Azure 監視器可讓您 tooconsume 遙測 toogain 掌握 hello 效能和您的工作負載在 Azure 上的健全狀況。 hello Azure 的遙測資料的最重要型別是 hello 度量 （也稱為效能計數器） 發出的大部分的 Azure 資源。 Azure 監視提供數種方式 tooconfigure 和取用這些[度量](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics)監視和疑難排解。 度量是重要的遙測資料來源，並啟用您 toodo hello 下列工作：

-   **追蹤 hello 效能**之資源 （例如 VM、 網站或邏輯應用程式） 繪製其入口網站的圖表上的度量，釘選圖表 tooa 儀表板。

-   **取得問題的通知**影響 hello 之資源的效能，當度量超出某個臨界值時。

-   **設定自動化動作**，例如自動調整資源，或在計量超出特定閾值時觸發 Runbook。

-   **執行進階分析**或報告您資源的效能或使用量趨勢。

-   **封存**hello 效能或健全狀況歷程記錄之資源的相容性或稽核用途。

### <a name="azure-diagnostics"></a>Azure 診斷

它是在啟用 hello 集合上部署的應用程式的診斷資料的 Azure 中的 hello 功能。 您可以使用 hello 診斷延伸模組，從各種不同的來源。 目前支援 [Azure 雲端服務 Web 和背景工作角色](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service)、執行 Microsoft Windows 的 [Azure 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/windows/overview)，以及 [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics)。 其他 Azure 服務都有自己個別的診斷。

## <a name="azure-network-watcher"></a>Azure 網路監看員

在偵測網路漏洞，並確認您的 IT 安全性和法規治理模型的合規性時，稽核您的網路安全性非常重要。 安全性群組 檢視中，您可以擷取 hello 設定網路安全性群組與安全性規則，且 hello 有效的安全性規則。 Hello 要套用的規則清單中，您可以決定 hello 連接埠已開啟，並評估網路的弱點可能會。

[網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher)是地區和服務，可讓您 toomonitor 診斷在網路層級中，並從 Azure 的情況。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。 這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。 案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。

![Azure 網路監看員](./media/azure-operational-security/azure-operational-security-fig8.png)

網路監看員目前具有下列功能的 hello:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">稽核記錄檔</a>**-hello 的網路組態的一部分執行的作業記錄。 這些記錄檔可以在 hello Azure 入口網站中檢視，或使用 Microsoft 工具，例如 Power BI 或協力廠商工具來擷取。 稽核記錄檔皆可透過 hello 入口網站、 PowerShell、 CLI 和 Rest API。 如需稽核記錄的詳細資訊，請參閱＜使用 Resource Manager 來稽核作業＞。 針對所有網路資源所進行的作業都會有稽核記錄。


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">IP 流程驗證</a>**：根據流程資訊 5 個 Tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 檢查是否允許或拒絕封包。 如果 hello 封包被拒絕的網路安全性群組，會傳回 hello 規則，並拒絕 hello 封包的網路安全性群組。

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">下一個躍點</a>** -決定 hello 封包路由傳送 hello Azure 網路網狀架構，讓您 toodiagnose 任何設定錯誤的使用者定義的路由中下一個躍點。

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">安全性的群組檢視</a>** -取得 hello 有效且套用安全性規則，可在 VM 上套用。

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">NSG 流程記錄</a>** -網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。 hello 流程是由 5-tuple 資訊 – 來源 IP、 目的地 IP、 來源連接埠，目的地連接埠和通訊協定定義。

## <a name="azure-storage-analytics"></a>Azure 儲存體分析

[儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)可以儲存有關要求 tooa 儲存體服務的彙總的交易統計資料和容量資料的度量。 在這兩個 hello 應用程式開發介面作業層級和 hello 儲存體服務層級報告交易和容量會報告在 hello 儲存體服務層級。 度量資料可使用的 tooanalyze 儲存體服務使用量，要求的 hello 儲存體服務，與使用服務的應用程式的 tooimprove hello 效能診斷問題。

[Azure 儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)會執行記錄，並提供儲存體帳戶的計量資料。 您可以使用此資料 tootrace 要求、 分析使用趨勢，以及診斷儲存體帳戶的問題。 儲存體分析記錄是供 hello [Blob、 佇列和表格服務](https://docs.microsoft.com/azure/storage/storage-introduction)。 儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。

這項資訊可以使用的 toomonitor 個別要求和 toodiagnose 與儲存體服務的問題。 系統會以最佳方式來記錄要求。 只有在沒有對 hello 服務端點所提出的要求，會建立記錄項目。 如範例的儲存體帳戶有活動，其 Blob 端點中，但不是在資料表或佇列端點，如果只會記錄有關 toohello Blob 服務會建立。

toouse 儲存體分析，您必須先啟用個別針對每個服務要 toomonitor。 您可以啟用它 hello [Azure 入口網站](https://portal.azure.com/); 如需詳細資訊，請參閱[監視 hello Azure 入口網站的儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account)。 您也可以啟用儲存體分析，以程式設計方式透過 hello REST API 或 hello 用戶端程式庫。 每個服務使用個別 hello 設定服務屬性作業 tooenable 儲存體分析。

hello 彙總的資料儲存在已知的 blob （用於記錄） 和已知資料表 （用於度量），可能會使用 hello Blob 服務和表格服務 Api 存取。

儲存體分析會將 20 TB 限制對 hello 儲存的資料量 hello 儲存體帳戶總限制無關。 所有記錄都會儲存在名為 $logs 之容器內的[區塊 Blob](https://docs.microsoft.com/azure/storage/storage-analytics) 中，該容器是在針對儲存體帳戶啟用儲存體分析時自動建立的。

hello 下列儲存體分析所執行的動作會列入計費：

-   記錄的要求 toocreate blob
-   要求 toocreate 資料表實體的度量。

> [!Note]
> 如需計費和資料保留原則的詳細資訊，請參閱[儲存體分析和計費](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)。
> 為了達到最佳效能，您會想 toolimit hello 數目高過低的磁碟附加 toohello 虛擬機器 tooavoid 可能節流設定。 如果所有磁碟都正在都使用率不高 hello 在同一時間，hello 儲存體帳戶可支援較大的數字磁碟。

> [!Note]
> 如需儲存體帳戶限制的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](https://docs.microsoft.com/azure/storage/storage-scalability-targets)。


會記錄下列類型的已驗證和匿名要求的 hello。

| 已驗證  | 匿名|
| :------------- | :-------------|
| 成功的要求 | 成功的要求 |
|失敗的要求，包括逾時、節流、網路、授權和其他錯誤 | 使用共用存取簽章 (SAS) 的要求，包括失敗和成功的要求 |
| 使用共用存取簽章 (SAS) 的要求，包括失敗和成功的要求 |用戶端與伺服器的逾時錯誤 |
|   要求 tooanalytics 資料 |    失敗的 GET 要求，錯誤碼為 304 (未修改) |
| 系統不會記錄儲存體分析本身所提出的要求 (例如，記錄檔的建立或刪除)。 Hello 記錄資料的完整清單會記載在 hello[儲存體分析記錄作業和狀態訊息](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages)和[儲存體分析記錄格式](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format)主題。 | 系統不會記錄所有其他失敗的匿名要求。 Hello 記錄資料的完整清單會記載在 hello[儲存體分析記錄作業和狀態訊息](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages)和[儲存體分析記錄格式](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format)。 |
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 也包含一組完整的身分識別管理功能，包括多重要素驗證、裝置註冊、自助式密碼管理、自助式群組管理、特殊權限的帳戶管理、角色型存取控制、應用程式使用量監視、豐富的稽核，以及安全性監視和警示。

-   利用 Azure AD 多重要素驗證和條件式存取，改善應用程式的安全性。

-   利用安全性報告和監視，監視應用程式使用量並保護您的企業免於受到嚴重的威脅。

Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。 [hello Azure Active Directory 稽核報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide)可以協助客戶其 Azure Active Directory 中發生的 tooidentify 特殊權限動作。 特殊權限的動作包括提高權限變更 （例如，建立角色或密碼重設），變更原則設定 （例如密碼原則） 或變更 toodirectory 設定 （例如，變更 toodomain 同盟設定）。

hello 報表提供 hello 事件名稱，執行 hello 動作，hello 受到 hello 變更及 hello 日期和時間 （以 utc 格式） 的目標資源的 hello 執行者 hello 稽核記錄。 客戶有 hello 透過其 Azure Active Directory 的稽核事件可以 tooretrieve hello 清單[Azure 入口網站](https://portal.azure.com/)中所述，[檢視稽核記錄](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)。 以下是一份包含 hello 報表：

| 安全性報告  | 活動報告| 稽核報告 |
| :------------- | :-------------| :-------------|
|從不明來源登入 | 應用程式使用情況：摘要 | 目錄稽核報告 |
|在多次失敗後登入 | 應用程式使用情況：詳細 |   |
|從多個地理區域登入 | 應用程式儀表板 |  |
|從具有可疑活動的 IP 位址登入 |帳戶佈建錯誤 |  |
|異常的登入活動 |個別使用者裝置 |  |
|從可能受感染的裝置登入 |個別使用者活動 |   |
|具有異常登入活動的使用者 |群組活動報告 |   |
| |密碼重設登錄活動報告 |   |
| |密碼重設活動 |   | |



這些報告的 hello 資料可以是很有用的 tooyour 應用程式，例如 SIEM 系統、 稽核及商業智慧工具。 hello Azure AD reporting [Api](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started)提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。 您可以從各種程式設計語言和工具呼叫這些 API。

180 天會保留在 hello Azure AD 稽核報告事件。

> [!Note]
> 如需保留報告的詳細資訊，請參閱 [Azure Active Directory 報告保留原則](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)。

客戶想儲存其[稽核事件](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events)較長的保留時間 hello 報告應用程式開發介面可以是使用的 tooregularly 提取稽核事件到另一個資料存放區。

## <a name="summary"></a>摘要

此發行項摘要，保護您的隱私權和保護您的資料，同時提供軟體和服務，可協助您管理 hello 貴組織的 IT 基礎結構。 Microsoft 認為當它們委託其資料 tooothers，該信任需要嚴格的安全性。 Microsoft 遵守 toostrict 相容性與安全性指導方針 — 從 toooperating 服務撰寫程式碼。 保全和保護資料在 Microsoft 是第一要務。

本文說明

-   如何收集、 處理及資料保護 hello Operations Management Suite (OMS) 中。

-   快速分析多個資料來源中的事件。 找出安全性風險，並了解安全性缺口的潛在威脅和攻擊 toomitigate hello 損壞的 hello 範圍和影響。

-   藉由將輸出的惡意 IP 流量和惡意威脅類型視覺化，進而識別攻擊模式。 了解整個無論平台環境的 hello 安全性狀態。

-   擷取所有 hello 記錄檔和事件的資料所需的安全性或相容性的稽核。 斜線 hello 時間和資源所需的 toosupply 安全性稽核以完整、 可搜尋，且可匯出記錄檔和事件的資料集。

<ul>
<li>收集安全性相關事件、 稽核及 tookeep 關閉 eye 您資產的漏洞分析：</li>
<ul>
<li>安全性狀態</li>
<li>值得注意的問題</li>
<li>摘要說明威脅</li>
</ul>
</ul>

## <a name="next-steps"></a>後續步驟

- [設計與作業安全性 (英文)](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft 設計其服務，並且注意 toohelp 中具有安全性軟體確保其雲端基礎結構有彈性且防守遭受攻擊。

- [Operations Management Suite | 安全性與合規性](https://www.microsoft.com/cloud-platform/security-and-compliance)

使用 Microsoft 安全性資料和分析 tooperform 更加智慧型而有效威脅偵測。

- [規劃 azure 資訊安全中心及作業](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)一組步驟和工作，您可以遵循它們的 toooptimize 貴用戶資訊安全中心使用根據組織的安全性需求和雲端管理模型。

