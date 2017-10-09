---
title: "記錄與稽核 aaaAzure |Microsoft 文件"
description: "深入了解如何使用記錄資料 toogain 深入了解有關應用程式。"
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
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Azure 記錄與稽核
## <a name="introduction"></a>簡介
### <a name="overview"></a>概觀
tooassist 目前和預期 Azure 客戶了解與使用 hello 各種安全性相關功能與周圍 hello Azure 平台，Microsoft 開發了一系列的技術白皮書、 安全性概觀、 最佳作法，和檢查清單。 hello 廣度及深度方面的主題範圍，並定期更新。 這份文件摘要 hello 遵循抽象 > 一節中為該系列的一部分。
### <a name="azure-platform"></a>Azure 平台
Azure 是作業系統的開放式且彈性的雲端服務平台支援的程式設計語言、 架構、 工具、 資料庫和裝置 hello 最大範圍的選取範圍。

例如，您可以：
-   透過 Docker 整合執行 Linux 容器。

-   使用 JavaScript、Python、.NET、PHP、Java 和 Node.js 建置應用程式。

-   建置 iOS、Android 和 Windows 裝置的後端。

Azure 公用雲端服務支援相同的技術數百萬的開發人員和 IT 專業人員已經依賴和信任的 hello。

當您建置，或 IT 資產移轉至雲端提供者、 您依賴該組織的能力 tooprotect 應用程式和資料與 hello 服務 」 和 「 hello 」 控制項提供您以雲端為基礎的資產的 toomanage hello 安全性。

從裝載吸引數百萬的客戶同時 hello 設備 tooapplications 設計 azure 的基礎結構，並提供的企業符合安全性需求的可信任基礎。 此外，Azure 為您提供廣泛的可設定的安全性選項和 hello 能力 toocontrol 它們可讓您可以自訂安全性 toomeet hello 獨特需求您的部署。 本文件將協助您符合這些需求。

### <a name="abstract"></a>摘要
安全性相關事件的稽核和記錄及相關警示是有效資料保護策略中的重要元件。 安全性記錄檔和報表提供您的電子記錄的可疑活動，並協助您偵測可能表示嘗試或成功外部滲透 hello 網路與內部攻擊的模式。 您可以使用稽核 toomonitor 使用者活動，文件法規相符性、 執行蒐證分析，等等。 警示會在安全性事件發生時提供即時通知。

Microsoft Azure 服務和產品提供您可設定的安全性稽核和記錄選項 toohelp 找出您的安全性原則和機制，間距，以及解決這些間距 toohelp 避免破壞。 Microsoft 服務提供一些 (在某些情況下，所有) 的下列選項的 hello： 集中化的監視、 記錄和分析系統 tooprovide 連續可見性。即時警示。和報表 toohelp 管理 hello 大量的裝置與服務所產生的資訊。

Microsoft Azure 記錄檔資料可以匯出的 tooSecurity 事件和事件管理 (SIEM) 系統進行分析，並與第三方稽核解決方案整合。

本技術白皮書介紹如何從裝載於 Azure 上的服務產生、收集及分析安全性記錄，並可協助您深入了解 Azure 部署的安全性。 這份技術白皮書 hello 範圍有限的 tooapplications 並建置及部署在 Azure 中的服務。

> [!Note]
> 此處包含的特定建議可能導致資料、網路或計算資源使用量增加，因而提高您的授權或訂用帳戶成本。

## <a name="types-of-logs-in-azure"></a>Azure 中的記錄類型
雲端應用程式相當複雜，且具有許多移動組件。 記錄檔提供您的應用程式保持啟動的資料 tooensure 和狀況良好的狀態中執行。 它也可協助您 toostave 關閉潛在的問題或過去的疑難排解。 此外，您可以使用記錄資料 toogain 深入了解有關應用程式。 該知識可以幫助您 tooimprove 應用程式效能或可維護性，或自動化需要手動介入的動作。

Azure 會為每項 Azure 服務產生大量記錄。 這些記錄檔會分類為這幾種主要類型︰
-   **控制/管理記錄檔**讓 hello 掌握 Azure 資源管理員建立、 更新和刪除作業。 [Azure 活動記錄](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)是這個記錄類型的一個範例。

-   **資料平面記錄**讓掌握 hello hello 的 Azure 資源的使用方式的一部分引發的事件。 這種類型的記錄檔的範例包括 hello Windows 事件系統、 安全性，和應用程式記錄檔中的虛擬機器和 hello[診斷記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)透過 Azure 監視器設定


-   **已處理的事件**提供分析已代替您處理之事件/警示的相關資訊。 這個類型的範例是 [Azure 資訊安全中心警示](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)，[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)已在其中處理和分析您的訂用帳戶，並提供簡要的安全性警示。

hello 下列表格會提供在 Azure 中的記錄檔的清單最重要型別。

| 記錄分類 | 記錄類型 | 使用方式 | 整合 |
| ------------ | -------- | ------ | ----------- |
|[活動記錄](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Azure Resource Manager 資源上控制層面的事件| 深入瞭解您的訂用帳戶中的資源執行的 hello 操作。|   REST API 與 [Azure 監視器](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Azure 診斷記錄](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|頻繁的訂用帳戶中的 Azure 資源管理員資源的 hello 作業的相關資料| 讓您了解資源自行執行的作業| Azure 監視器、[資料流](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[AAD 報告](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|記錄和報告|使用者登入活動，以及使用者和群組管理相關的系統活動資訊|[Graph API](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[雲端服務與虛擬機器](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Windows 事件記錄與 Linux Syslog|  擷取系統資料和 hello 虛擬機器上的記錄資料，並將該資料傳送到您選擇的儲存體帳戶。| 使用 [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (Windows Azure 診斷儲存體) 的 Windows 和 Azure 監視器上的 Linux|
|[Storage Analytics](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|儲存體記錄，並提供儲存體帳戶的計量資料|讓您了解追蹤要求、分析使用趨勢，以及診斷儲存體帳戶的問題。|  REST API 或 hello[用戶端程式庫](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[NSG (網路安全性群組) 流程記錄](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|JSON 格式，並顯示每個規則的輸出和輸入流程|檢視透過網路安全性群組輸入和輸出 IP 流量的相關資訊|[網路監看員](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application Insight](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|記錄、例外狀況及自訂診斷|  多個平台上的 Web 開發人員所適用的應用程式效能管理 (APM) 服務。| REST API、[Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|處理資料/安全性警示| Azure 資訊安全中心警示，OMS 警示| 資訊安全資訊與警示。|   REST API、JSON|

### <a name="activity-log"></a>活動記錄檔
hello [Azure 活動記錄檔](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)，提供深入了解您的訂用帳戶中的資源執行的 hello 操作。 hello 活動記錄檔先前稱為 「 稽核記錄檔 」 或 「 操作記錄檔 」，因為它會報告[控制平面事件](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/)訂用帳戶。 使用 hello 活動記錄檔，您可以決定 hello 」 功能，對象、 及何時"的任何寫入作業 (PUT、 POST、 DELETE) 在您的訂用帳戶中的 hello 資源。 您也可以了解 hello 狀態 hello 作業以及其他相關的屬性。 hello 活動記錄檔不包括讀取 (GET) 作業。

這裡 PUT、 POST、 DELETE 指的是活動記錄檔包含 hello 資源 tooall hello 寫入作業。 例如，您可以使用 hello 活動記錄檔 toofind 錯誤進行疑難排解時或 toomonitor 您組織中的使用者如何修改資源。

![活動記錄檔](./media/azure-log-audit/azure-log-audit-fig1.png)


您可以從您使用 hello Azure 入口網站的活動記錄檔擷取事件[CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli)，PowerShell cmdlet 和[Azure 監視 REST API](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough)。 活動記錄的資料保留期限為 19 天。

整合案例
-   [建立電子郵件或可觸發關閉活動記錄檔事件的 webhook 警示。](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [串流 tooan 事件中心](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs)來擷取第三方服務或自訂的分析解決方案，例如 power Bi。

-   分析中使用 hello PowerBI [power Bi 內容套件。](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [將它儲存 tooa 儲存體帳戶進行保存或手動檢查。](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) 您可以指定 hello 保留時間 （以天為單位） 記錄檔的設定檔使用。

-   查詢，並在 hello Azure 入口網站中檢視它。

-   透過 PowerShell Cmdlet、CLI 或 REST API 查詢活動記錄。

-   匯出 hello 與記錄檔的設定檔的活動記錄檔太[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)。

您可以使用儲存體帳戶或[事件中樞命名空間](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive)不在 hello 相同訂用帳戶，因為 hello 一個發出記錄檔。 將設定 hello 設定的 hello 使用者必須擁有適當的 hello [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)存取 tooboth 訂閱
### <a name="azure-diagnostic-logs"></a>Azure 診斷記錄
Azure 診斷的記錄檔會發出由資源提供豐富、 且經常 hello 該資源的作業有關的資料。 hello 這些記錄檔的內容會因資源類型 (比方說， [Windows 事件系統記錄檔](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)vm 是一個診斷記錄檔的分類和[blob、 資料表和佇列記錄](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account)診斷記錄檔的類別儲存體帳戶） 而不同 hello 活動記錄檔，可提供深入了解您的訂用帳戶中的資源執行的 hello 操作。

![Azure 診斷記錄](./media/azure-log-audit/azure-log-audit-fig2.png)

Azure 診斷記錄提供多個組態選項，亦即 Azure 入口網站、使用 PowerShell、命令列介面 (CLI) 和 REST API。

**整合案例**
-   將它們儲存 tooa[儲存體帳戶](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs)稽核或手動檢查。 您可以指定 hello 保留時間 （以天為單位） 使用 hello 診斷設定。

-   [對它們進行串流 tooEvent 集線器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs)來擷取第三方服務或自訂的分析解決方案，例如[PowerBI。](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   以 [OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) 分析記錄。

**支援的服務、診斷記錄的結構描述，以及每個資源類型支援的記錄分類**


| 服務 | 結構描述與文件 | 資源類型 | 類別 |
| ------- | ------------- | ------------- | -------- |
|負載平衡器| [Azure 負載平衡器的記錄檔分析 (預覽)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|網路安全性群組|[網路安全性群組 (NSG) 的記錄檔分析](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|應用程式閘道|[應用程式閘道的診斷記錄功能](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|金鑰保存庫|[Azure 金鑰保存庫記錄](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Azure 搜尋服務|[啟用和使用搜尋流量分析](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Data Lake Store|[存取 Azure Data Lake Store 的診斷記錄](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|稽核|
|Data Lake Analytics|[存取 Azure Data Lake Analytics 的診斷記錄](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|稽核|
|||Microsoft.DataLakeAnalytics/accounts|要求|
|||Microsoft.DataLakeStore/accounts|要求|
|Logic Apps|[Logic Apps B2B 自訂追蹤結構描述](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Azure Batch 診斷記錄](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Azure 自動化|[Azure 自動化的記錄檔分析](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|事件中樞|[Azure 事件中樞診斷記錄](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|串流分析|[作業診斷記錄](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|執行|
|||Microsoft.StreamAnalytics/streamingjobs|編寫|
|服務匯流排|[Azure 服務匯流排診斷記錄](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Azure Active Directory 報告
Azure Active Directory (Azure AD) 包括您的目錄的安全性、活動和稽核報告。 hello [Azure Active Directory 稽核報告](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide)可以協助客戶其 Azure Active Directory 中發生的 tooidentify 特殊權限動作。 特殊權限的動作包括提高權限變更 （例如，建立角色或密碼重設），變更原則設定 （例如密碼原則） 或變更 toodirectory 設定 （例如，變更 toodomain 同盟設定）。

hello 報表提供 hello 事件名稱，執行 hello 動作，hello 受到 hello 變更及 hello 日期和時間 （以 utc 格式） 的目標資源的 hello 執行者 hello 稽核記錄。 客戶有 hello 透過其 Azure Active Directory 的稽核事件可以 tooretrieve hello 清單[Azure 入口網站](https://portal.azure.com/)中所述，[檢視稽核記錄](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)。 以下是一份包含 hello 報表：

| 安全性報告 | 活動報告 | 稽核報告 |
| :--------------- | :--------------- | :------------ |
|從不明來源登入| 應用程式使用情況：摘要| 目錄稽核報告|
|在多次失敗後登入|  應用程式使用情況：詳細||
|從多個地理區域登入|    應用程式儀表板||
|從具有可疑活動的 IP 位址登入|   帳戶佈建錯誤||
|異常的登入活動|    個別使用者裝置||
|從可能受感染的裝置登入|   個別使用者活動||
|具有異常登入活動的使用者| 群組活動報告||
||密碼重設登錄活動報告||
||密碼重設活動|||

這些報告的 hello 資料可以是很有用的 tooyour 應用程式，例如 SIEM 系統、 稽核及商業智慧工具。 hello Azure AD 報告 Api 提供以程式設計方式存取 toohello 資料透過一組 REST 架構應用程式開發介面。 您可以從各種程式設計語言和工具呼叫這些 [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started)。

180 天會保留在 hello Azure AD 稽核報告事件。

> [!Note]
> 如需保留報告的詳細資訊，請參閱 [Azure Active Directory 報告保留原則](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention)。

對於較長的保留時間儲存其稽核事件有興趣的客戶，hello Reporting API 可以用 tooregularly 提取[稽核事件](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events)到個別的資料存放區。

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>使用 Azure 診斷的虛擬機器記錄
[Azure 診斷](https://docs.microsoft.com/azure/azure-diagnostics)是在啟用 hello 集合上部署的應用程式的診斷資料的 Azure 中的 hello 功能。 您可以從數個不同的來源使用 hello 診斷延伸模組。 目前支援 [Azure 雲端服務的 Web 和背景工作角色](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me)。

![使用 Azure 診斷的虛擬機器記錄](./media/azure-log-audit/azure-log-audit-fig3.png)

執行 Microsoft Windows 和[Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview) 的 [Azure 虛擬機器](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)。

您可以使用下列方式，在虛擬機器上啟用 Azure 診斷：

-   使用 Visual Studio，請參閱[使用 Visual Studio tootrace Azure 虛擬機器](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [從遠端在 Azure 虛擬機器上設定 Azure 診斷](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Azure 虛擬機器上使用 PowerShell tooset 診斷](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [使用 Azure Resource Manager 範本建立具有監視和診斷的 Windows 虛擬機器](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>儲存體分析
[Azure 儲存體分析](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)會執行記錄，並提供儲存體帳戶的計量資料。 您可以使用此資料 tootrace 要求、 分析使用趨勢，以及診斷儲存體帳戶的問題。 儲存體分析記錄是供 hello [Blob、 佇列和表格服務。](https://docs.microsoft.com/azure/storage/storage-introduction) 儲存體分析記錄成功和失敗的要求 tooa 儲存體服務的詳細的資訊。

這項資訊可以使用的 toomonitor 個別要求和 toodiagnose 與儲存體服務的問題。 系統會以最佳方式來記錄要求。 只有在沒有對 hello 服務端點所提出的要求，會建立記錄項目。 例如，如果儲存體帳戶其 Blob 端點中有活動，但不是在資料表或佇列端點，只會記錄有關 toohello Blob 服務會建立。

toouse 儲存體分析，您必須先啟用個別針對每個服務要 toomonitor。 您可以啟用它 hello [Azure 入口網站](https://portal.azure.com/); 如需詳細資訊，請參閱[監視 hello Azure 入口網站的儲存體帳戶。](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) 您也可以啟用儲存體分析，以程式設計方式透過 hello REST API 或 hello 用戶端程式庫。 每個服務使用個別 hello 設定服務屬性作業 tooenable 儲存體分析。

hello 彙總的資料儲存在已知的 blob （用於記錄） 和已知資料表 （用於度量），可能會使用 hello Blob 服務和表格服務 Api 存取。

儲存體分析會將 20 TB 限制對 hello 儲存的資料量 hello 儲存體帳戶總限制無關。 所有記錄都會儲存在名為 $logs 之容器內的[區塊 Blob](https://docs.microsoft.com/azure/storage/storage-analytics) 中，該容器是在針對儲存體帳戶啟用儲存體分析時自動建立的。

> [!Note]
> 如需計費和資料保留原則的詳細資訊，請參閱[儲存體分析和計費](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing)。
>
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

### <a name="azure-networking-logs"></a>Azure 網路記錄
Azure 中的網路記錄和監視功能相當完善，主要涵蓋分類有二種：

-   [網路監看員](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher)-使用網路監看員中的 hello 功能提供以案例為基礎的網路監視。 這項服務包括封包擷取、下一個躍點、IP 流量驗證、安全性群組檢視、NSG 流量記錄。 案例層級監視提供結束 tooend 檢視中對比 tooindividual 網路資源監視的網路資源。

-   [資源監視](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring)：資源層級監視由診斷記錄、計量、疑難排解和資源健康狀態這四個功能所組成。 所有這些功能是建置在 hello 網路資源層級。

![Azure 網路記錄](./media/azure-log-audit/azure-log-audit-fig4.png)

網路監看員是地區和服務，可讓您 toomonitor 診斷層級網路案例中，，然後從 Azure 的情況。 網路診斷和使用網路監看員的視覺化工具，可協助您了解、 診斷，以及取得 Azure insights tooyour 網路。

**NSG 流程記錄**-網路安全性群組的流程記錄可讓您 toocapture 記錄相關的 tootraffic 允許或拒絕 hello 群組中的 hello 安全性規則。 這些流程記錄檔會寫入以 JSON 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。

### <a name="network-security-group-flow-logging"></a>網路安全性群組流程記錄

[網路安全性小組流程記錄](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview)是 tooview ingress 和 egress IP 流量，透過網路安全性群組相關的資訊可讓您的網路監看員的功能。 這些流程記錄檔會寫入以 JSON 格式，並顯示輸出和輸入每個規則為基礎的流量，hello NIC hello 流程適用於，5 個 tuple hello 流程 （來源/目的地 IP，來源/目的地連接埠通訊協定） 的資訊，並允許流量，如果 hello 或被拒絕。

流程記錄目標網路安全性群組，而不會顯示 hello 相同 hello 做其他記錄檔。 流程記錄只會儲存於儲存體帳戶內。

hello 相同套用 tooflow 記錄的其他記錄檔所見的保留原則。 記錄檔具有可設定為 1 天 too365 天的保留原則。 如果未設定保留原則，就會永遠保留 hello 記錄檔。

**診斷記錄**

定期和即時事件建立的網路資源，登入傳送 tooan 事件中心 」 或 「 記錄分析的儲存體帳戶。 這些記錄檔提供深入了解資源的 hello 健全狀況。 您可以在 Power BI 和 Log Analytics 等工具中檢視這些記錄。 toolearn tooview 診斷記錄檔的瀏覽[記錄分析。](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![診斷記錄檔](./media/azure-log-audit/azure-log-audit-fig5.png)

診斷記錄適用於[負載平衡器](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log)、[網路安全性群組](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log)、路由和[應用程式閘道](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics)。

網路監看員提供診斷記錄檢視。 此檢視包含所有支援診斷記錄的網路資源。 從這個檢視中，您可以方便且快速地啟用和停用網路資源。


在加法 toopreceding 記錄功能，網路監看員目前具有下列功能的 hello:
- [拓樸](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview)-提供網路層級檢視顯示 hello 各種 connect 和資源群組中的網路資源之間的關聯。

- [變數封包擷取](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview)：擷取進出虛擬機器的封包資料。 進階篩選選項，例如位於無法 tooset 微調的控制項提供 versatility.hello 封包資料可以儲存在 blob 存放區或 hello.cap 格式的本機磁碟上的時間，而且大小限制。

-   [IP 流程驗證](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview)：根據流程資訊 5 個 Tuple 封包參數 (目的地 IP、來源 IP、目的地連接埠、來源連接埠和通訊協定) 檢查是否允許或拒絕封包。 如果安全性群組遭拒絕 hello 封包，hello 規則，並拒絕 hello 封包的群組會傳回。

-   [下一個躍點](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview)-決定 hello 封包路由傳送 hello Azure 網路網狀架構，讓您 toodiagnose 任何設定錯誤的使用者定義的路由中下一個躍點。

-   [安全性的群組檢視](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview)-取得 hello 有效且套用安全性規則，可在 VM 上套用。

-   [虛擬網路閘道與連接疑難排解](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest)-提供 hello 能力 tootroubleshoot 虛擬網路閘道與連線。

-   [訂用帳戶限制的網路](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits)-可讓您限制對 tooview 網路資源使用狀況。

### <a name="application-insight"></a>Application Insight

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) 是多個平台上的 Web 開發人員所適用的可延伸應用程式效能管理 (APM) 服務。 它使用 toomonitor 即時 web 應用程式。 它會自動偵測效能異常。 它包括強大的分析工具 toohelp 您診斷問題和 toounderstand 哪些使用者實際執行應用程式。

 其設計目的是 toohelp 持續改善效能和可用性。

 這也適用於應用程式上各種不同的平台包括.NET、 Node.js 和 J2EE，裝載在內部部署或 hello 雲端中。 它與您的 devOps 程序整合，並具有連接點 toovarious 開發工具。

![Application Insight](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights 旨在 hello 開發團隊，toohelp 您了解如何執行您的應用程式，以及如何被使用。 它可監視︰

-   **要求率、回應時間和失敗率** - 找出哪些頁面在每天哪些時段最受歡迎，以及使用者位於何處。 查看哪些頁面的表現最好。 如果您的回應時間和失敗率隨著要求增加而提高，您或許有資源配置問題。

-   **相依比率、回應時間和失敗率** - 找出外部服務是否會使您降低效能。

-   **例外狀況**-分析 hello 彙總統計資料，或選擇特定執行個體和下鑽研至 hello 堆疊追蹤和相關的要求。 伺服器和瀏覽器例外狀況都會報告。

-   **頁面檢視和載入效能** - 由使用者的瀏覽器報告。

-   來自網頁的 **AJAX 呼叫** - 比率、回應時間和失敗率。

-   **使用者和工作階段計數**。

-   Windows 或 Linux 伺服器電腦中的**效能計數器**，例如 CPU、記憶體和網路使用量。

-   來自 Docker 或 Azure 的**主機診斷**。

-   來自您應用程式的**診斷追蹤記錄檔** - 讓您使追蹤事件與要求相互關聯。

-   **自訂事件和度量**，您自行撰寫 hello 用戶端或伺服器程式碼中，tootrack 商務事件，例如項目已售出或遊戲成交。

**整合案例及描述清單：**

| 整合案例 | 說明 |
| --------------------- | :---------- |
|[應用程式對應](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|您的應用程式，警示的關鍵計量與 hello 元件。||
|[執行個體資料的診斷搜尋](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| 搜尋和篩選事件，例如要求、例外狀況、相依性呼叫、記錄追蹤，以及頁面檢視。||
|[彙總資料的計量瀏覽器](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|瀏覽、篩選和分割彙總的資料，例如，要求、錯誤和例外狀況的比率；回應時間、頁面載入時間。||
|[儀表板](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|來自多個資源的交互式資料並與其他人員共用。 多元件的應用程式，然後連續顯示 hello 小組室中很棒。||
|[即時計量串流](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|當您部署新組建時，觀賞這些接近即時的效能指標 toomake 確定一切如預期運作。||
|[分析](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|使用這個功能強大的查詢語言，回答有關您應用程式效能和使用方式的艱難問題。||
|[自動和手動警示](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|警示自動調整 tooyour 應用程式的遙測和觸發程序的一般模式有任務在身時外 hello 一般模式。 您也可以在自訂或標準計量的特定層級上設定警示。||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|請參閱 hello 程式碼中的效能資料。 移 toocode 從堆疊追蹤。||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|整合使用量計量和其他商業智慧。||
|[REST API](https://dev.applicationinsights.io/)|撰寫程式碼 toorun 查詢透過您的度量和原始資料。||
|[連續匯出](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|大量的未經處理資料 toostorage 送達時予以匯出。||

### <a name="azure-security-center-alerts"></a>Azure 資訊安全中心警示
[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-intro)自動收集、 分析和整合記錄資料從 Azure 資源、 hello 網路和連線的協力廠商解決方案，例如防火牆和 endpoint protection 解決方案，toodetect 威脅並降低誤判。 優先順序的安全性警示的清單會顯示在資訊安全中心，以及 hello 資訊需要 tooquickly 調查 hello 問題，並建議如何 tooremediate 攻擊。

資訊安全中心威脅偵測的運作方式自動收集您的 Azure 資源、 hello 網路和連線的交易夥伴方案中的 安全性資訊。 它會分析這項資訊通常相互關聯多個來源，tooidentify 威脅的資訊。 安全性警示的優先順序資訊安全中心以及如何 tooremediate hello 威脅的建議。

![Azure 資訊安全中心](./media/azure-log-audit/azure-log-audit-fig7.png)

資訊安全中心會運用進階安全性分析，其遠勝於以簽章為基礎的方法。 在大型資料突破和[機器學習](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/)技術跨 hello 整個雲端網狀架構 – 偵測會是不可能 tooidentify 使用手動方法，並預測 hello 的威脅是套用的 tooevaluate 事件演進而來的攻擊。 這些安全性分析包括︰

-   **整合威脅情報：**尋找 Microsoft 產品和服務，從套用全域威脅情報已知的不良執行者 hello Microsoft 數位犯罪單元 (DCU)，如 hello Microsoft Security Response Center (MSRC) 和外部摘要。

-   **行為分析：**已知的模式 toodiscover 惡意行為套用。

-   **異常偵測：**統計分析 toobuild 歷程基準使用。 它會提醒上偏離已建立符合 tooa 潛在的攻擊誘因的基準。


許多安全性作業和事件回應小組依賴安全性資訊和事件管理 (SIEM) 方案作為 hello 分級和調查安全性警示的起點。 利用 Azure 記錄整合，客戶可以將資訊安全中心警示，以及 Azure 診斷和 Azure 稽核記錄檔所收集的虛擬機器安全性事件，與其 Log Analytics 或 SIEM 方案以接近即時的方式進行同步處理。


## <a name="log-analytics"></a>Log Analytics

Log Analytics 是 [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) 中的一項服務，可協助您收集和分析雲端和內部部署環境中的資源所產生的資料。 它可讓您使用整合式的搜尋的即時深入資訊和自訂儀表板 tooreadily 地分析數百萬筆記錄在所有工作負載和伺服器，無論其實體位置為何。

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Hello 中心記錄分析是 hello OMS 儲存機制裝載在 hello Azure 雲端。 到 hello 儲存機制從所設定的資料來源和加入解決方案 tooyour 訂用帳戶連線來源收集資料。 資料來源和解決方案將每個建立自己的屬性集，但可能仍然會分析一起查詢 toohello 儲存機制中不同的記錄類型。 這可讓您 toouse hello 與不同類型的資料相同的工具和方法 toowork 收集不同的來源。

已連線的來源為 hello 電腦及其他資源，產生記錄分析所收集的資料。 這可包括安裝在直接連接之 [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) 和 [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) 電腦的代理程式，或[已連接的 System Center Operations Manager 管理群組](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents)中的代理程式。 Log Analytics 也可以從 [Azure 儲存體](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)收集資料。

[資料來源](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources)hello 不同的每個連接的來源收集資料。 這包括事件和[效能資料](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters)從[Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)和 Linux 代理程式，例如加法 toosources 中的[IIS 記錄檔](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)，和[自訂文字記錄檔。](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) 您設定您想要 toocollect，，和 hello 組態會自動傳遞的 tooeach 已連接的來源的每個資料來源。

有四種不同的方式可[收集 Azure 服務的記錄和計量](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage)：
1.  Azure 診斷直接 tooLog 分析 （hello 下表中的診斷）

2.  Azure 診斷 tooAzure 儲存體 tooLog 分析 （hello 下表中的儲存體）

3.  Azure 服務 （hello 下表中的連接器） 連接器

4.  和編寫指令碼 toocollect 然後張貼資料到記錄分析 （空白下表中的 hello 和未列出的服務）

| 服務 | 資源類型 | 記錄檔 | 度量 | 方案 |
| :------ | :------------ | :--- | :------ | :------- |
|應用程式閘道|  Microsoft.Network/<br>applicationGateways|  診斷|診斷|    [Azure 應用程式](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)[閘道分析](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application insights||     連接器|  連接器|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/) [ 連接器 (預覽) (英文)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|自動化帳戶|   Microsoft.Automation/<br>AutomationAccounts|    診斷||       [詳細資訊](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Batch 帳戶|    Microsoft.Batch/<br>batchAccounts|  診斷|    診斷||
|傳統雲端服務||       儲存體||       [詳細資訊](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|辨識服務|    Microsoft.CognitiveServices/<br>accounts|       診斷|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>accounts|   診斷|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>accounts|   診斷|||
|事件中樞命名空間|   Microsoft.EventHub/<br>namespaces|  診斷|    診斷||
|IoT 中樞|  Microsoft.Devices/<br>IotHubs||     診斷||
|金鑰保存庫| Microsoft.KeyVault/<br>vaults|  診斷  || [金鑰保存庫分析](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|負載平衡器|    Microsoft.Network/<br>loadBalancers|    診斷|||
|Logic Apps|    Microsoft.Logic/<br>workflows|  診斷|    診斷||
||Microsoft.Logic/<br>integrationAccounts||||
|網路安全性群組|   Microsoft.Network/<br>networksecuritygroups|診斷||   [Azure 網路安全性群組分析](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|復原保存庫|   Microsoft.RecoveryServices/<br>vaults|||[Azure 復原服務分析 (預覽)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|搜尋服務|   Microsoft.Search/<br>searchServices|    診斷|    診斷||
|服務匯流排命名空間| Microsoft.ServiceBus/<br>namespaces|    診斷|診斷|    [服務匯流排分析 (預覽)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       儲存體||    [Service Fabric Analytics (Service Fabric 分析) (預覽)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (v12)| Microsoft.Sql/<br>servers/<br>資料庫||       診斷||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|儲存體|||         指令碼| [Azure 儲存體分析 (預覽)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|虛擬機器|  Microsoft.Compute/<br>virtualMachines|  擴充功能|  分機||
||||診斷||
|虛擬機器擴展集|   Microsoft.Compute/<br>virtualMachines    ||診斷||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Web 伺服器陣列|Microsoft.Web/<br>serverfarms||   診斷
|網站| Microsoft.Web/<br>sites ||      診斷|    [詳細資訊](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slots|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>與內部部署之 SIEM 系統整合的記錄
[Azure 記錄檔整合](https://www.microsoft.com/download/details.aspx?id=53324)可讓您從您的 Azure 資源在 tooyour 內部 toointegrate 未經處理的記錄檔**安全性資訊和事件管理 (SIEM) 系統**。

![記錄整合](./media/azure-log-audit/azure-log-audit-fig9.png)

Azure 記錄整合會從您的 Windows (WAD) 虛擬機器、Azure 活動記錄，Azure 資訊安全中心警示和 Azure 資源提供者記錄收集 Azure 診斷。 這項整合提供統一的儀表板的所有資產，在內部部署或在 hello 雲端中，以便您可以彙總、 相互關聯、 分析及安全性事件的警示。



Azure 記錄整合目前支援整合 Azure 活動記錄、您 Azure 訂用帳戶中 Windows 虛擬機器的 Windows 事件記錄檔、Azure 資訊安全中心警示、Azure 診斷記錄及 Azure Active Directory 稽核記錄。

| 記錄類型 | 支援 JSON 的記錄分析 (Splunk、ArcSight、Qradar) |
| :------- | :-------------------------------------------------------- |
|AAD 稽核記錄|    yes|
|活動記錄檔| 是|
|ASC 警示 |是|
|診斷記錄 (資源記錄)|  是|
|VM 記錄|   是，透過轉送的事件，而非透過 JSON|


hello 下表說明 hello 記錄類別目錄和 SIEM 整合的詳細資料。

[開始使用 Azure 記錄整合](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started)：這個教學課程會逐步引導您安裝 Azure 記錄整合，以及整合來自 Azure WAD 儲存體的記錄、Azure 活動記錄、Azure 資訊安全中心警示以及 Azure Active Directory 稽核記錄。

整合案例

-   [夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)– 此部落格文章會示範 tooconfigure Azure 與協力廠商解決方案 Splunk、 HP 討論 ArcSight 和 IBM QRadar 所記錄的整合 toowork。

-   [Azure 記錄整合常見問題集 (FAQ)](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) - 此常見問題集會回答有關 Azure 記錄整合的問題。

-   [整合的資訊安全中心與 Azure 的警示記錄 Integration](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) – 本文件說明如何 toosync 資訊安全中心發出警示通知，以及虛擬機器的安全性事件記錄分析收集 Azure 診斷和 Azure 稽核記錄檔，或SIEM 解決方案。

## <a name="next-steps"></a>後續步驟

- [稽核和記錄](https://www.microsoft.com/trustcenter/security/auditingandlogging)

保護資料維護可見性，並快速回應 tootimely 安全性警示

- [Azure 中的安全性記錄和稽核記錄收集 (英文)](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

您需要確定您的 Azure 執行個體收集 tooenforce toomake 哪些設定 hello 正確的安全性和稽核記錄。

- [設定網站集合的稽核設定](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

為網站集合管理員，一個就可以 hello 特定使用者所採取的動作記錄和擷取也可以擷取 hello 歷程記錄，在特定日期範圍期間所採取的動作。 

- [搜尋在 hello Office 365 安全性與相容性中心 hello 稽核記錄檔](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Office 365 組織中可以使用 hello Office 365 安全性與相容性中心 toosearch hello 統一的稽核記錄 tooview 使用者和系統管理員的活動。


