---
title: "aaaAdd Azure Log Analytics 管理解決方案 |Microsoft 文件"
description: "Operations Management Suite (OMS) / Log Analytics 管理解決方案是邏輯、視覺效果和資料擷取規則的集合，可提供針對特定問題領域進行計量的樞紐分析。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>新增 Azure Log Analytics management 解決方案 tooyour 工作區

Log Analytics 管理解決方案是**邏輯**、**視覺效果**和**資料擷取規則**的集合，可提供針對特定問題領域進行計量的樞紐分析。 本文章列出支援的記錄分析的管理解決方案，並顯示 tooadd 和使用工作區移除 hello Azure 入口網站。 您也可以使用 hello 解決方案資源庫 hello OMS 入口網站中新增的解決方案。

管理解決方案可允許更深入的探討，以：

* 協助調查並更快解決操作問題
* 收集並相互關聯各種類型的機器資料
* 協助您主動出擊，hello 解決方案會公開。

> [!NOTE]
> 記錄分析包含記錄搜尋功能，因此您不需要管理方案 tooenable tooinstall 它。 不過，您可以藉由新增管理解決方案 tooyour 工作區取得資料視覺效果、 建議的搜尋和深入資訊。

使用這份文件，您會新增管理解決方案 tooa 工作區中使用 Azure 入口網站 Marketplace hello。 您已新增解決方案之後，會從您的基礎結構中的 hello 伺服器收集資料，並將其傳送 toohello OMS 服務。 依 hello OMS 服務通常只需要幾分鐘的時間 tooan 小時處理。 Hello 服務會處理 hello 資料之後，您可以在 OMS 中檢視它。

當您不再需要管理解決方案時，您可以輕易地將它移除。 當您移除管理解決方案時，其資料不會傳送 tooOMS。 如果您是在 hello 免費定價層，則移除解決方案可以減少 hello 使用的資料量，協助您保持在每日配額的資料。

## <a name="view-available-management-solutions"></a>檢視可用的管理解決方案

hello Azure marketplace 包含 hello 份[供記錄分析的管理解決方案](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions)。

您可以從 Azure marketplace 所提供安裝管理解決方案，依序按一下 hello**立即下載**在每個解決方案的 hello 底部的連結。

## <a name="add-a-management-solution"></a>新增管理解決方案
1. 如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)使用您的 Azure 訂用帳戶。
2. 在 hello**新增**刀鋒視窗底下**Marketplace**，選取**監視 + 管理**。
3. 在 hello**監視 + 管理**刀鋒視窗中，按一下 **查看所有**。  
    ![監視 + 管理刀鋒視窗](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. 右側 toohello**管理解決方案**，按一下 **詳細**。
5. 在 hello**管理解決方案**刀鋒視窗中，選取您想 tooadd tooa 工作區的管理解決方案。  
    ![監視 + 管理刀鋒視窗](./media/log-analytics-add-solutions/management-solutions.png)  
6. 在 hello 管理方案刀鋒視窗中，檢閱有關 hello 管理解決方案，，然後按一下**建立**。
7. 在 hello*管理方案名稱*刀鋒視窗中，選取您想 tooassociate 與 hello 管理解決方案的工作區。
8. （選擇性） 變更 hello Azure 訂用帳戶、 資源群組和位置的工作區設定。 您也可以選擇 [自動化選項]。 按一下 [建立] 。  
    ![解決方案工作區](./media/log-analytics-add-solutions/solution-workspace.png)  
9. toostart 使用 hello 管理解決方案，您已新增的 tooyour 工作區中，瀏覽過**記錄分析** > **訂閱** > ***工作區名稱***  > **概觀**。 隨即會顯示管理解決方案的新圖格。 它並開始使用 hello 解決方案收集資料的 hello 方案之後，請按一下 hello 磚 tooopen。

## <a name="remove-a-management-solution"></a>移除管理解決方案

1. 在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽過**記錄分析** > **訂閱** > ***工作區名稱***然後在 hello***工作區名稱***刀鋒視窗中，按一下 **解決方案**。
2. Hello 清單中的管理解決方案，選取您想 tooremove hello 方案。
3. 在 hello 方案刀鋒視窗中為您工作區，按一下 **刪除**。  
    ![刪除解決方案](./media/log-analytics-add-solutions/solution-delete.png)  
4. 在 hello 確認對話方塊中，按一下 **是**。

## <a name="offers-and-pricing-tiers"></a>優惠和定價層

下表中的 hello 識別哪些管理解決方案隸屬 tooeach Operations Management Suite 提供項目。
hello 資料表也可以識別 hello 定價層所提供的每個管理解決方案。
Hello 下表中的所有方案都是從內部 hello Azure 入口網站與 hello 解決方案資源庫 hello 記錄分析入口網站中使用。

| 管理解決方案                                                                       | 提供項目                                                                     | 定價層<sup>1</sup>                                                 | 注意事項 |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [活動 Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 可免費使用資料 90 天<br>資料不會遵守 toohello 免費層 cap |
| [AD 評估](log-analytics-ad-assessment.md)                                           | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [AD 複寫狀態](log-analytics-ad-replication-status.md)                           | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 無法從 Azure 入口網站/marketplace tooadd。 |
| [代理程式健全狀況](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 資料不會遵守 toohello 免費層 cap<br> 無法從 Azure 入口網站/marketplace tooadd。 |
| [警示管理](log-analytics-solution-alert-management.md)                            | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 無法從 Azure 入口網站/marketplace tooadd。 |
| [Application Insights Connector (預覽)](log-analytics-app-insights-connector.md)                                               | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [自動化混合式背景工作角色](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>自動化和控制</li></ul>                                  | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶 |
| [Azure 應用程式閘道分析](log-analytics-azure-networking-analytics.md)    | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [Azure 網路安全性群組分析](log-analytics-azure-networking-analytics.md)     | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [Azure SQL Analytics (預覽)](log-analytics-azure-sql.md)                                                       | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br>每個&nbsp;節點&nbsp;(OMS)                                                                          | 需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶|
| [Azure Web Apps 分析](log-analytics-azure-web-apps-analytics.md)     | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
|[備份](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>深入解析與分析</li></ul>                                   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)                                                                       | 需要傳統的備份保存庫。<br> 無法從 Azure 入口網站/marketplace tooadd。 |
| [容量與效能 (預覽)](log-analytics-capacity.md)                                                   | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [變更追蹤](log-analytics-change-tracking.md)                                       | <ul><li>自動化和控制</li></ul>                                  | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶 |
| [容器](log-analytics-containers.md)                                                 | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [IT 服務管理連接器 (預覽)](log-analytics-itsmc-overview.md)                                              | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 每個&nbsp;節點&nbsp;(OMS)     | |
| HDInsight HBase 監視 <br>(預覽)                                                  | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [金鑰保存庫分析](log-analytics-azure-key-vault.md)                   | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 無法從 Azure 入口網站/marketplace tooadd。 |
| [惡意程式碼評估](log-analytics-malware.md)                                            | <ul><li>安全性與法規遵循</li></ul>                                 | 免費<br> 獨立<br>每個&nbsp;節點&nbsp;(OMS)                                                                           | 如果您在 2017 年 6 月 19 之後, 加入 hello 安全性與相容性解決方案[帳單為每個節點](https://azure.microsoft.com/pricing/details/security-compliance/)，不論 hello 工作區的定價層。 hello 前 60 天可用。  |
| [網路效能監視器](log-analytics-network-performance-monitor.md) <br>  | <ul><li>深入解析與分析</li></ul>                                   | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | |
| [Office 365 分析 (預覽)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [安全性和稽核](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>安全性&nbsp;和&nbsp;合規性</li></ul>                       | 免費<br> 獨立<br>每個&nbsp;節點&nbsp;(OMS)                                                                           | 收集安全性事件記錄檔需要此解決方案<br>如果您在 2017 年 6 月 19 之後, 加入 hello 安全性與相容性解決方案[帳單為每個節點](https://azure.microsoft.com/pricing/details/security-compliance/)，不論 hello 工作區的定價層。 hello 前 60 天可用。 |
| [Service Fabric Analytics (Service Fabric 分析) (預覽)](log-analytics-service-fabric.md)                     | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [服務對應 (預覽)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>深入解析與分析</li></ul>                      | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 適用於美國東部、西歐和美國中西部    |
| [站台復原](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>深入解析與分析</li></ul>                                   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)                                                                       | 需要傳統的 Site Recovery 保存庫。<br> 無法從 Azure 入口網站/marketplace tooadd。 |
| [SQL 評估](log-analytics-sql-assessment.md)                                         | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| 於下班時間開始/停止 VM<br>(預覽)                                              | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶 |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 無法從 Azure 入口網站/marketplace tooadd。 |
| [System Center Operations Manager 評定 (預覽)](log-analytics-scom-assessment.md)  | <ul><li>深入解析與分析</li><li>Log Analytics</li></ul>        | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [更新管理](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>自動化和控制</li></ul>                                  | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶 |
| [更新合規性 (預覽)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 免費的資料或節點<br>資料不會遵守 toohello 免費層 cap。<br> 無法從 Azure 入口網站/marketplace tooadd。 |
| [升級整備程度](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | 免費的資料或節點<br>資料不會遵守 toohello 免費層 cap。<br> 無法從 Azure 入口網站/marketplace tooadd。 |
| [VMware 監控 (預覽)](log-analytics-vmware.md)                                | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 標準<br> 進階&nbsp;(OMS)<br> 每個&nbsp;GB&nbsp;(獨立)<br> 每個&nbsp;節點&nbsp;(OMS)   | |
| [Wire Data 2.0 (預覽)](log-analytics-wire-data.md)                                                                 | <ul><li>深入解析與分析</li></ul>                                   | 免費<br> 每個&nbsp;節點&nbsp;(OMS)                                                                         | 適用於美國東部、西歐和美國中西部 |

<sup>1</sup> hello*標準*和*Premium (OMS)*定價層才可建立其記錄分析工作區先前 tooSeptember 21 2016年的客戶。

### <a name="community-provided-management-solutions"></a>社群提供的管理解決方案

提供的社群解決方案都是從 hello [Azure 範本庫](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS))並直接從 hello 作者。

| 管理解決方案               | 提供項目                                                                     | 定價層                         | 注意事項 |
| ---                               | ---                                                                       | ---                                   | ---   |
| 所有社群提供的解決方案  | <ul><li>深入解析&nbsp;與&nbsp;分析</li><li>Log Analytics</li></ul>   | 免費<br> 每個&nbsp;節點&nbsp;(OMS)     |   需要您的記錄分析工作區連結的 toobe tooan 自動化帳戶 |




## <a name="data-collection-details"></a>資料收集詳細資料
hello 下表顯示資料收集方法，以及如何記錄分析管理方案和資料來源收集資料的其他詳細資料。 hello 資料表會依分類方案提供等同於太[訂用帳戶的定價層](https://go.microsoft.com/fwlink/?linkid=827926)。 hello 活動記錄分析解決方案是免費的使用 tooall 定價層中。

hello 記錄分析 Windows 代理程式和 System Center Operations Manager 代理程式基本上就是 hello 相同。 hello Windows 代理程式包含其他功能 tooallow 它 tooconnect toohello OMS 工作區，然後透過 proxy 路由。 如果您使用 Operations Manager 代理程式，它必須與 OMS 的 OMS 代理程式 toocommunicate 為目標。 此資料表中的 operations Manager 代理程式會連接的 tooOperations Manager 的 OMS 代理程式。 請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)連接您現有的 Operations Manager 環境 tooOMS 相關資訊。

> [!NOTE]
> 您使用的代理程式的 hello 類型會決定資料如何傳送 tooOMS，以 hello 下列條件：
> - 您使用 hello Windows 代理程式或 Operations Manager 附加的 OMS 代理程式。
> - Operations Manager 需要時，hello 方案的 Operations Manager 代理程式資料會一律傳送 tooOMS 使用 hello Operations Manager 管理群組。 此外，當 Operations Manager 需要時，只有 hello Operations Manager 代理程式會使用 hello 方案。
> - 當 Operations Manager 就不需要與 hello 表顯示 Operations Manager 代理程式資料會傳送 hello 管理群組，則 Operations Manager 代理程式資料使用 tooOMS 一律會傳送 tooOMS 使用管理群組。 Windows 代理程式略過 hello 管理群組，並將其資料傳送直接 tooOMS。
> - 當 Operations Manager 代理程式資料不會傳送使用管理群組時，然後 hello 資料傳送直接 tooOMS — 略過 hello 管理群組。

### <a name="insight--analytics--log-analytics"></a>深入解析與分析 / Log Analytics

| 管理解決方案 | 平台 | Microsoft Monitoring Agent | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 活動 Log Analytics | Azure |   |   |   |   |   | 與通知同時 |
| AD 評估 |Windows |&#8226; |&#8226; |  |  |&#8226; |7 天 |
| AD 複寫狀態 |Windows |&#8226; |&#8226; |  |  |&#8226; |5 天 |
| 代理程式健康狀態 | Windows 和 Linux | &#8226; | &#8226; |   |   | &#8226; | 1 分鐘 |
| 警示管理 (Nagios) |Linux |&#8226; |  |  |  |  |與抵達同時 |
| 警示管理 (Zabbix) |Linux |&#8226; |  |  |  |  |1 分鐘 |
| 警示管理 (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 分鐘 |
| Application Insights 連接器 (預覽) | Azure |   |   |   |   |   | 與通知同時 |
| Azure 應用程式閘道分析 | Azure |   |   |   |   |   | 與通知同時 |
| Azure 網路安全性群組分析 | Azure |   |   |   |   |   | 與通知同時 |
| Azure SQL Analytics (預覽) |Windows |  |  |  |  |  | 10 分鐘 |
| 產能管理 |Windows |&#8226; |&#8226; |  |  |&#8226; |與抵達同時 |
| 容器 | Windows 和 Linux | &#8226; | &#8226; |   |   |   | 3 分鐘 |
| 金鑰保存庫分析 |Windows |  |  |  |  |  |與通知同時 |
| 網路效能監視器 | Windows | &#8226; | &#8226; |   |   |   | TCP 會每 5 秒交握一次，而資料會每 3 分鐘傳送一次 |
| Office 365 分析 (預覽) |Windows |  |  |  |  |  |與通知同時 |
| Service Fabric 分析 |Windows |  |  |&#8226; |  |  |5 分鐘 |
| 服務對應 | Windows 和 Linux | &#8226; | &#8226; |   |   |   | 15 秒 |
| SQL 評估 |Windows |&#8226; |&#8226; |  |  |&#8226; |7 天 |
| Surface Hub |Windows |&#8226; |  |  |  |  |與抵達同時 |
| System Center Operations Manager 評定 (預覽) | Windows | &#8226; | &#8226; |   |   | &#8226; | 7 天 |
| 升級分析 (預覽) | Windows | &#8226; |   |   |   |   | 2 天 |
| VMware 監視 (預覽) | Linux | &#8226; |   |   |   |   | 3 分鐘 |
| 連線資料 |Windows (2012 R2/8.1 或更新版本) |&#8226; |&#8226; |  |  |  | 1 分鐘 |


### <a name="automation--control"></a>自動化與控制

| 管理解決方案 | 平台 | Microsoft Monitoring Agent | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 自動化混合式背景工作角色 | Windows | &#8226; | &#8226; |   |   |   | n/a |
| 變更追蹤 |Windows |&#8226; |&#8226; |  |  |&#8226; |每小時 |
| 變更追蹤 |Linux |&#8226; |  |  |  |  |每小時 |
| 更新管理 | Windows |&#8226; |&#8226; |  |  |&#8226; |安裝更新之後 15 分鐘，至少一天 2 次 |

### <a name="security--compliance"></a>安全性與法規遵循

| 管理解決方案 | 平台 | Microsoft Monitoring Agent | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 反惡意程式碼評估 |Windows |&#8226; |&#8226; |  |  |&#8226; |每小時 |
| 安全性和稽核<sup>1</sup> | Windows 和 Linux | 部分 | 部分 | 部分 |   | 部分 | 各種 |

<sup>1</sup> hello 安全性和稽核解決方案可以從 Windows、 Operations Manager 和 Linux 代理程式收集記錄檔。 請參閱[資料來源](#data-sources)，以取得關於下列各項的資料收集資訊：

- syslog
- Windows 安全性事件記錄檔
- Windows 防火牆記錄檔
- Windows 事件記錄檔



### <a name="protection--recovery"></a>保護和復原

| 管理解決方案 | 平台 | Microsoft Monitoring Agent | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 備份 | Azure |   |   |   |   |   | n/a |
| Azure Site Recovery | Azure |   |   |   |   |   | n/a |


### <a name="data-sources"></a>資料來源


| 資料來源 | 平台 | Microsoft Monitoring Agent | Operations Manager 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Azure 活動記錄檔 |Windows |  |  |  |  |  |與通知同時 |
| Azure 診斷記錄 |Windows |  |  |  |  |  |與通知同時 |
| Azure 診斷計量 |Windows |  |  |  |  |  |與通知同時 |
| ETW |Windows |  |  |&#8226; |  |  |5 分鐘 |
| IIS 記錄檔 |Windows |&#8226; |&#8226; |&#8226; |  |  |5 分鐘 |
| 效能計數器 |Windows |&#8226; |&#8226; |  |  |  |依排程，最少 10 秒 |
| 效能計數器 |Linux |&#8226; |  |  |  |  |依排程，最少 10 秒 |
| syslog |Linux |&#8226; |  |  |  |  |從 Azure 儲存體 ：10 分鐘；從代理程式：與抵達同時 |
| Windows 安全性事件記錄檔 |Windows |&#8226; |&#8226; |&#8226; |  |  |Azure 儲存體： 10 分鐘;hello 代理程式： 到達時 |
| Windows 防火牆記錄檔 |Windows |&#8226; |&#8226; |  |  |  |與抵達同時 |
| Windows 事件記錄檔 |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |Azure 儲存體： 10 分鐘;hello 代理程式： 到達時 |



## <a name="preview-management-solutions-and-features"></a>預覽管理解決方案和功能
執行服務，並遵循 devops 做法，我們目前無法 toopartner 與客戶 toodevelop 功能和方案。

私用在預覽期間，我們會讓客戶存取 tooan 最早實作的 hello 功能或解決方案 toogain 意見的一小群，並進行修改。 此初期實作只有最少的功能和運作能力。

我們的目標快速是 tootry 項目，因此我們可以找到有效的註解，以及功能無法運作。 我們會逐一此程序，直到 hello hello 私人預覽客戶意見反應通知我們，我們已準備好進行公開預覽狀態。

Hello 公用預覽期間，我們會讓 hello 功能或解決方案可供所有使用者 tooget 詳細的意見反應，並驗證我們縮放比例和效率。 在這個階段中：

* 預覽功能會出現在 hello 設定 索引標籤，而且可以由任何使用者啟用。
* 加入預覽解決方案透過 hello 組件庫，或使用指令碼。

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>我對預覽功能和方案應該有何了解？
我們很高興有關新功能和管理解決方案，我們喜歡使用您 toodevelop 它們。

預覽功能和解決方案並不適合每個人。 詢問 toojoin 私人預覽或之前啟用公用預覽，請確定您正常使用正在開發的項目。

當啟用預覽功能，透過 hello 入口網站時，您會看到警告，提醒您 hello 功能處於預覽狀態。

#### <a name="for-both-private-and-public-preview"></a>私人和公開預覽
hello 下列資訊適用於 tooboth 公用和私人預覽：

* 不見得永遠正常運作。
  * 問題範圍從次要令透過 toosomething 完全無法運作。
* 沒有 hello 預覽 toohave 負面的影響，在您的系統上的潛在 / 環境。
  * 我們嘗試 tooavoid 負發生 toohello 系統使用 OMS，但有時非預期的項目就會發生。
* 可能發生資料遺失/損毀。
* 我們可能會要求您 toocollect 診斷記錄檔或其他資料 toohelp 疑難排解問題。
* hello 功能或解決方案可能會移除 （暫時或永久）。
  * 我們可能會依據我們所獲得的經驗，在 hello 預覽期間決定 toonot 發行 hello 功能或解決方案。
* 預覽可能無法運作，或尚未經過所有組態的測試，我們可能會限制︰
  * hello 可用的作業系統 （例如，一項功能可能僅適用於 tooLinux 在預覽中的）。
  * hello 的代理程式 （MMA，Operations Manager） 可以使用的型別 （例如，一項功能可能不適用於在預覽中的 Operations Manager）。  
* Hello 服務等級協定未涵蓋預覽方案和功能。
* 使用預覽功能需要支付使用費用。
* 功能或功能，您需要 hello 功能 / 方案 toobe 有用可能遺失或不完整。
* 並非所有區域都可使用功能/方案。
* 功能/方案可能未完成當地語系化。
* 功能解決方案可能有限制客戶或可以使用它的裝置 hello 數目。
* 您可能需要 toouse 指令碼 tooperform 組態和 tooenable hello 解決方案/功能。
* hello 使用者介面 (UI) 不完整，並從一天 tooday 可能會變更。
* 公開預覽可能不是適用於生產/重要系統。

#### <a name="for-private-preview"></a>私人  預覽
下列資訊的 hello 加法 toohello 以上項目，是特定 tooprivate 預覽：

* 我們預期 tooprovide 隨您的體驗的意見反應給我們，讓我們可以 hello/方案功能更好。
* 我們可能會利用意見調查、電話或電子郵件，請您提供意見反應。
* 情況不見得一帆風順。
* 我們可能在您加入之前要求簽署保密合約 (NDA)，也可能含有機密內容。
  * 部落格、 tweeting，或之前否則與第三方進行通訊，請洽詢 hello 經理負責 hello 預覽 toounderstand 公開的任何限制。
* 請勿在生產/重要系統上執行。

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>如何取得存取 tooprivate 預覽功能和方案？
我們邀請客戶 tooprivate 預覽透過幾種不同的方法，根據 hello 預覽。

* 接聽 hello 每月客戶調查並放棄我們權限 toofollow 與您可改善受邀的 tooa 私人預覽中的次數。
* 您的 Microsoft 帳戶小組可以提名您。
* 您可以根據 twitter [msopsmgmt](https://twitter.com/msopsmgmt)。
* 您可以根據社群活動分享的詳細資料來註冊 – 請在會面場合、會議和線上社群與我們接觸。

## <a name="next-steps"></a>後續步驟
* [搜尋記錄](log-analytics-log-searches.md)tooview 詳細管理解決方案所收集的資訊。
