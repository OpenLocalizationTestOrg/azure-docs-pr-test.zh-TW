---
title: "適用於 Azure 備份的 Log Analytics 資料模型"
description: "本文將討論 Azure 備份資料的 Log Analytics 資料模型詳細資料。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: dfd5c73d-0d34-4d48-959e-1936986f9fc0
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 041a8835a1dd185739b23d4073fd5811bb4490b5
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>適用於 Azure 備份資料的 Log Analytics 資料模型
本文描述將報告資料推送到 Log Analytics 所使用的資料模型。 使用此資料模型，您就可以建立自訂查詢、儀表板，並在 OMS 中加以利用。 

## <a name="using-azure-backup-data-model"></a>使用 Azure 備份資料模型
若要根據您的需求建立視覺效果、自訂查詢及儀表板，您可以使用下列提供作為資料模型一部分的欄位。

### <a name="alert"></a>警示
下表提供警示相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| AlertUniqueId_s |文字 |所產生警示的唯一識別碼 |
| AlertType_s |文字 |所產生的警示類型 (例如，備份) |
| AlertStatus_s |文字 |警示狀態 (例如，作用中) |
| AlertOccurenceDateTime_s |日期/時間 |建立警示的日期和時間 |
| AlertSeverity_s |文字 |警示嚴重性 (例如，重大) |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| BackupItemUniqueId_s |文字 |此警示所屬之備份項目的唯一 ID |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |警示物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本警示所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - Alert |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |此警示所屬之受保護項目的唯一 ID |
| VaultUniqueId_s |文字 |此警示所屬之受保護項目的唯一 ID |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="backupitem"></a>BackupItem
下表提供備份項目相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |  
| BackupItemUniqueId_s |文字 |備份項目的唯一 ID |
| BackupItemId_s |文字 |備份項目識別碼 |
| BackupItemName_s |文字 |備份項目名稱 |
| BackupItemFriendlyName_s |文字 |備份項目的易記名稱 |
| BackupItemType_s |文字 |備份項目類型 (例如，VM、FileFolder) |
| ProtectedServerName_s |文字 |備份項目所屬之受保護伺服器的名稱 |
| ProtectionState_s |文字 |備份項目的目前保護狀態 (例如，受保護、ProtectionStopped) |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |備份項目物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本備份項目所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - BackupItem |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="backupitemassociation"></a>BackupItemAssociation
下表提供與各種實體關聯的備份項目相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |  
| BackupItemUniqueId_s |文字 |備份項目的唯一 ID |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |備份項目關聯物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本備份項目所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - BackupItemAssociation |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |可識別備份項目與其相關聯之原則的唯一 ID |
| ProtectedServerUniqueId_s |文字 |此備份項目所屬之受保護伺服器的唯一 ID |
| VaultUniqueId_s |文字 |此備份項目所屬之保存庫的唯一 ID |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="job"></a>作業
下表提供作業相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| BackupItemUniqueId_s |文字 |此作業所屬之備份項目的唯一 ID |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |作業物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本作業所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - Job |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |此作業所屬之受保護項目的唯一 ID |
| VaultUniqueId_s |文字 |此作業所屬之受保護項目的唯一 ID |
| JobOperation_s |文字 |執行作業的操作 (例如，備份、還原、設定備份) |
| JobStatus_s |文字 |已完成之作業的狀態 (例如，已完成、失敗) |
| JobFailureCode_s |文字 |由於發生作業失敗而產生的失敗碼字串 |
| JobStartDateTime_s |日期/時間 |開始執行作業的日期和時間 |
| BackupStorageDestination_s |文字 |備份儲存體的目的地 (例如，雲端、磁碟)  |
| JobDurationInSecs_s | 數字 |總作業持續時間 (以秒為單位) |
| DataTransferredInMB_s | 數字 |此工作的資料轉送 (以 MB 為單位)|
| JobUniqueId_g |文字 |用來識別作業的唯一識別碼 |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="policy"></a>原則
下表提供原則相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |原則物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本原則所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - Policy |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |用來識別原則的唯一識別碼 |
| PolicyName_s |文字 |所定義原則的名稱 |
| BackupFrequency_s |文字 |備份的執行頻率 (例如，每日、每週) |
| BackupTimes_s |文字 |排定要備份的日期和時間 |
| BackupDaysOfTheWeek_s |文字 |一週中已排定要備份的日期 |
| RetentionDuration_s |整數 |所設定備份的保留期間 |
| DailyRetentionDuration_s |整數 |所設定備份的總保留期間 (以天為單位) |
| DailyRetentionTimes_s |文字 |每日保留期的設定日期和時間 |
| WeeklyRetentionDuration_s |十進位數字 |所設定備份的每週保留總期間 (以週為單位) |
| WeeklyRetentionTimes_s |文字 |每週保留期的設定日期和時間 |
| WeeklyRetentionDaysOfTheWeek_s |文字 |一週中所選用於每週保留期的日期 |
| MonthlyRetentionDuration_s |十進位數字 |所設定備份的總保留期間 (以月為單位) |
| MonthlyRetentionTimes_s |文字 |每月保留期的設定日期和時間 |
| MonthlyRetentionFormat_s |文字 |每月保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| MonthlyRetentionDaysOfTheWeek_s |文字 |一週中所選用於每月保留期的日期 |
| MonthlyRetentionWeeksOfTheMonth_s |文字 |一個月中每月保留期的設定週數 (例如，第一週、最後一週等等)。 |
| YearlyRetentionDuration_s |十進位數字 |所設定備份的總保留期間 (以年為單位) |
| YearlyRetentionTimes_s |文字 |每年保留期的設定日期和時間 |
| YearlyRetentionMonthsOfTheYear_s |文字 |一年中所選用於每年保留期的月數 |
| YearlyRetentionFormat_s |文字 |每年保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| YearlyRetentionDaysOfTheMonth_s |文字 |一個月中所選用於每年保留期的日期 |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="policyassociation"></a>PolicyAssociation
下表提供與各種實體關聯的原則相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |原則物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本原則所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - PolicyAssociation |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |用來識別原則的唯一識別碼 |
| VaultUniqueId_s |文字 |此原則所屬之保存庫的唯一 ID |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="protectedserver"></a>ProtectedServer
下表提供受保護伺服器相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| ProtectedServerName_s |文字 |受保護伺服器的名稱 |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |受保護伺服器物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本受保護伺服器所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - ProtectedServer |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |受保護伺服器的唯一 ID |
| RegisteredContainerId_s |文字 |已註冊要進行備份的容器識別碼 |
| ProtectedServerType_s |文字 |所備份的受保護伺服器類型 (例如，Windows) |
| ProtectedServerFriendlyName_s |文字 |受保護伺服器的易記名稱 |
| AzureBackupAgentVersion_s |文字 |代理程式備份版本的版本號碼 |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
下表提供與其他實體關聯的受保護伺服器相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |受保護伺服器關聯物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本受保護伺服器所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - ProtectedServerAssociation |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |受保護伺服器的唯一 ID |
| VaultUniqueId_s |文字 |此受保護伺服器所屬之保存庫的唯一 ID |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="storage"></a>儲存體
下表提供儲存體相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| CloudStorageInBytes_s |十進位數字 |備份所使用的雲端備份儲存體，在計算時會以最後的值為依據 |
| ProtectedInstances_s |十進位數字 |用於在帳單中計算前端儲存體的受保護執行個體數目，在計算時會以最後的值為依據 |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |儲存體物件的目前狀態 (例如，作用中、已刪除) |
| BackupManagementType_s |文字 |用於執行本儲存體所屬之備份的提供者類型 (例如，IaaSVM、FileFolder) |
| OperationName |文字 |此欄位代表目前作業的名稱 - Storage |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |所計算儲存體之受保護伺服器的唯一 ID |
| VaultUniqueId_s |文字 |會計算儲存體保存庫的唯一 ID |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

### <a name="vault"></a>保存庫
下表提供保存庫相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表目前版本的結構描述，它是 **V1** |
| State_s |文字 |保存庫物件的目前狀態 (例如，作用中、已刪除) |
| OperationName |文字 |此欄位代表目前作業的名稱 - Vault |
| 類別 |文字 |此欄位代表推送到 Log Analytics 的診斷資料類別，則是 AzureBackupReport |
| 資源 |文字 |這是所收集資料的資源，會顯示復原服務保存庫名稱 |
| VaultUniqueId_s |文字 |保存庫的唯一 ID |
| VaultName_s |文字 |保存庫名稱 |
| AzureDataCenter_s |文字 |保存庫所在的資料中心 |
| StorageReplicationType_s |文字 |保存庫的儲存體複寫類型 (例如，GeoRedundant) |
| SourceSystem |文字 |目前資料的來源系統 - Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之訂用帳戶 ID |
| ResourceGroup |文字 |此欄位代表所收集資料的資源 (RS 保存庫) 之資源群組 |
| ResourceProvider |文字 |此欄位代表所收集資料的資源提供者 - Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位代表所收集資料的資源類型 - Vaults |

## <a name="next-steps"></a>後續步驟
一旦您檢閱建立 Azure 備份報告的資料模型後，就可以開始在 Log Analytics 和 OMS 中[建立儀表板](../log-analytics/log-analytics-dashboards.md)。
