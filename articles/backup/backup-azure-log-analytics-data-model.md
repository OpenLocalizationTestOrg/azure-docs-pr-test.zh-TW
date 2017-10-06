---
title: "Azure backup aaaLog 分析資料模型"
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
ms.openlocfilehash: 04ac16e38b896851f60b1c4ffbea4343347ae32c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-model-for-azure-backup-data"></a>適用於 Azure 備份資料的 Log Analytics 資料模型
本文說明用來將報表資料 tooLog 分析發送 hello 資料模型。 使用此資料模型，您就可以建立自訂查詢、儀表板，並在 OMS 中加以利用。 

## <a name="using-azure-backup-data-model"></a>使用 Azure 備份資料模型
您可以使用下列欄位的 hello 資料模型 toocreate 視覺效果、 自訂查詢，並根據您的需求的儀表板中提供的 hello。

### <a name="alert"></a>警示
下表提供警示相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| AlertUniqueId_s |文字 |唯一識別碼 hello 產生警示 |
| AlertType_s |文字 |產生警示，例如，備份類型的 hello。 |
| AlertStatus_s |文字 |Hello 警示，例如，作用中的狀態 |
| AlertOccurenceDateTime_s |日期/時間 |建立警示的日期和時間 |
| AlertSeverity_s |文字 |Hello 警示嚴重性，例如，重大 |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| BackupItemUniqueId_s |文字 |此警示所屬太 hello 備份項目 toowhich 的唯一識別碼|
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 警示物件，例如 「 作用中 」、 「 已刪除目前的狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 此警示所屬過的提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業的警示名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |唯一識別碼 hello 保護此警示所屬太 toowhich|
| VaultUniqueId_s |文字 |唯一識別碼 hello 保護此警示所屬太 toowhich|
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="backupitem"></a>BackupItem
下表提供備份項目相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |  
| BackupItemUniqueId_s |文字 |Hello 備份項目的唯一識別碼 |
| BackupItemId_s |文字 |備份項目識別碼 |
| BackupItemName_s |文字 |備份項目名稱 |
| BackupItemFriendlyName_s |文字 |備份項目的易記名稱 |
| BackupItemType_s |文字 |備份項目類型 (例如，VM、FileFolder) |
| ProtectedServerName_s |文字 |太所屬的受保護的伺服器 toowhich 備份項目名稱|
| ProtectionState_s |文字 |目前的 hello 備份項目，例如受保護、 ProtectionStopped 保護狀態 |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 備份項目物件，例如 「 作用中 」、 「 已刪除目前的狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 此備份的項目太所屬的提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業 BackupItem 名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="backupitemassociation"></a>BackupItemAssociation
下表提供與各種實體關聯的備份項目相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |  
| BackupItemUniqueId_s |文字 |Hello 備份項目的唯一識別碼 |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |物件的目前狀態 hello 備份項目關聯，例如 「 作用中 」、 「 已刪除 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 此備份的項目太所屬的提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業 BackupItemAssociation 名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |唯一識別碼 tooidentify hello 原則，也很相關聯的備份的項目|
| ProtectedServerUniqueId_s |文字 |唯一識別碼 hello 受保護伺服器 toowhich 此備份的項目所屬太|
| VaultUniqueId_s |文字 |此備份的項目所屬太 hello 保存庫 toowhich 的唯一識別碼|
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="job"></a>作業
下表提供作業相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| BackupItemUniqueId_s |文字 |此作業所屬太 hello 備份項目 toowhich 的唯一識別碼|
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 工作物件，例如作用中、 已刪除目前的狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 這項作業太所屬的提供者類型|
| OperationName |文字 |此欄位代表 hello 目前作業的名稱的工作 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |唯一識別碼 hello 保護的 toowhich 太所屬這項作業|
| VaultUniqueId_s |文字 |唯一識別碼 hello 保護的 toowhich 太所屬這項作業|
| JobOperation_s |文字 |執行作業的操作 (例如，備份、還原、設定備份) |
| JobStatus_s |文字 |Hello 的狀態已完成作業，例如，已完成、 失敗 |
| JobFailureCode_s |文字 |由於發生作業失敗而產生的失敗碼字串 |
| JobStartDateTime_s |日期/時間 |開始執行作業的日期和時間 |
| BackupStorageDestination_s |文字 |備份儲存體的目的地 (例如，雲端、磁碟)  |
| JobDurationInSecs_s | 數字 |總作業持續時間 (以秒為單位) |
| DataTransferredInMB_s | 數字 |此工作的資料轉送 (以 MB 為單位)|
| JobUniqueId_g |文字 |唯一識別碼 tooidentify hello 工作 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="policy"></a>原則
下表提供原則相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 原則物件，例如 「 作用中 」、 「 已刪除目前的狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 太屬於此原則提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業的原則名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |唯一識別碼 tooidentify hello 原則 |
| PolicyName_s |文字 |Hello 原則定義名稱 |
| BackupFrequency_s |文字 |備份的執行頻率 (例如，每日、每週) |
| BackupTimes_s |文字 |排定要備份的日期和時間 |
| BackupDaysOfTheWeek_s |文字 |當已排程備份的 hello 一周天數 |
| RetentionDuration_s |整數 |所設定備份的保留期間 |
| DailyRetentionDuration_s |整數 |所設定備份的總保留期間 (以天為單位) |
| DailyRetentionTimes_s |文字 |每日保留期的設定日期和時間 |
| WeeklyRetentionDuration_s |十進位數字 |所設定備份的每週保留總期間 (以週為單位) |
| WeeklyRetentionTimes_s |文字 |每週保留期的設定日期和時間 |
| WeeklyRetentionDaysOfTheWeek_s |文字 |選取每週保留期的 hello 週間日 |
| MonthlyRetentionDuration_s |十進位數字 |所設定備份的總保留期間 (以月為單位) |
| MonthlyRetentionTimes_s |文字 |每月保留期的設定日期和時間 |
| MonthlyRetentionFormat_s |文字 |每月保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| MonthlyRetentionDaysOfTheWeek_s |文字 |選取每月保留期的 hello 週間日 |
| MonthlyRetentionWeeksOfTheMonth_s |文字 |週 hello 月份每月保留期設定時，例如，第一個、 最後一個等。 |
| YearlyRetentionDuration_s |十進位數字 |所設定備份的總保留期間 (以年為單位) |
| YearlyRetentionTimes_s |文字 |每年保留期的設定日期和時間 |
| YearlyRetentionMonthsOfTheYear_s |文字 |Hello 年度月份選取每年保留期 |
| YearlyRetentionFormat_s |文字 |每年保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| YearlyRetentionDaysOfTheMonth_s |文字 |選取每年保留期的 hello 月份的日期 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="policyassociation"></a>PolicyAssociation
下表提供與各種實體關聯的原則相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 原則物件，例如 「 作用中 」、 「 已刪除目前的狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM，此原則所屬太 FileFolder toowhich 提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業 PolicyAssociation 名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| PolicyUniqueId_g |文字 |唯一識別碼 tooidentify hello 原則 |
| VaultUniqueId_s |文字 |此原則所屬太 hello 保存庫 toowhich 的唯一識別碼|
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="protectedserver"></a>ProtectedServer
下表提供受保護伺服器相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| ProtectedServerName_s |文字 |受保護伺服器的名稱 |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |目前狀態的 hello 受保護的伺服器物件，例如 「 作用中 」、 「 已刪除 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM，此受保護的伺服器所屬太 FileFolder toowhich 提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業 ProtectedServer 名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |唯一識別碼 hello 受保護伺服器 |
| RegisteredContainerId_s |文字 |已註冊要進行備份的容器識別碼 |
| ProtectedServerType_s |文字 |所備份的受保護伺服器類型 (例如，Windows) |
| ProtectedServerFriendlyName_s |文字 |受保護伺服器的易記名稱 |
| AzureBackupAgentVersion_s |文字 |代理程式備份版本的版本號碼 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="protectedserverassociation"></a>ProtectedServerAssociation
下表提供與其他實體關聯的受保護伺服器相關詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |目前狀態的 hello 受保護伺服器關聯物件，例如 「 作用中 」、 「 已刪除 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 此受保護的伺服器太所屬的提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業 ProtectedServerAssociation 名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |唯一識別碼 hello 受保護伺服器 |
| VaultUniqueId_s |文字 |此受保護的伺服器所屬太 hello 保存庫 toowhich 的唯一識別碼|
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

### <a name="storage"></a>儲存體
下表提供儲存體相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| CloudStorageInBytes_s |十進位數字 |備份所使用的雲端備份儲存體，在計算時會以最後的值為依據 |
| ProtectedInstances_s |十進位數字 |用於在帳單中計算前端儲存體的受保護執行個體數目，在計算時會以最後的值為依據 |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 儲存物件，例如 「 作用中 」、 「 已刪除的目前狀態 |
| BackupManagementType_s |文字 |執行備份，例如 IaaSVM FileFolder toowhich 太所屬此存放裝置提供者類型|
| OperationName |文字 |此欄位會顯示 hello 目前作業存放區的名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| ProtectedServerUniqueId_s |文字 |計算儲存體的伺服器來保護 hello 的唯一識別碼 |
| VaultUniqueId_s |文字 |計算儲存體的 hello 保存庫的唯一識別碼 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位 representse 類型 hello 資源為其收集的資料-保存庫 |

### <a name="vault"></a>保存庫
下表提供保存庫相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| EventName_s |文字 |此欄位代表這個事件的名稱，它一律為 AzureBackupCentralReport |
| SchemaVersion_s |文字 |此欄位代表 hello 結構描述的目前版本，它是**V1** |
| State_s |文字 |Hello 保存庫物件，例如 「 作用中 」、 「 已刪除目前的狀態 |
| OperationName |文字 |此欄位會顯示 hello 目前作業保存庫的名稱 |
| 類別 |文字 |此欄位代表推入 tooLog 分析的診斷資料的類別目錄，則是 AzureBackupReport |
| 資源 |文字 |這是為其收集資料的 hello 資源，它會顯示復原服務保存庫名稱 |
| VaultUniqueId_s |文字 |Hello 保存庫的唯一識別碼 |
| VaultName_s |文字 |Hello 保存庫的名稱 |
| AzureDataCenter_s |文字 |保存庫所在的資料中心 |
| StorageReplicationType_s |文字 |Hello 保存庫，例如 GeoRedundant 的儲存體複寫類型 |
| SourceSystem |文字 |來源系統的 hello 目前的資料-Azure |
| ResourceId |文字 |此欄位代表所收集資料的資源 ID，會顯示復原服務保存庫資源 ID |
| SubscriptionId |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的訂用帳戶 id |
| ResourceGroup |文字 |此欄位會顯示為其收集資料的 hello 資源 （RS 保存庫） 的資源群組 |
| ResourceProvider |文字 |此欄位會顯示 hello 資源提供者為其收集的資料-Microsoft.RecoveryServices |
| ResourceType |文字 |此欄位會顯示 hello 資源為其收集的資料-保存庫的類型 |

## <a name="next-steps"></a>後續步驟
一旦您檢閱 hello 資料模型來建立 Azure Backup 報表時，就可以開始[建立儀表板](../log-analytics/log-analytics-dashboards.md)記錄分析和 OMS 中。
