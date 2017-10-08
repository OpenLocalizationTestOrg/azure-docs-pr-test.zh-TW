---
title: "Azure backup aaaData 模型"
description: "本文將討論 Azure 備份報告的 Power BI 資料模型詳細資料。"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 0767c330-690d-474d-85a6-aa8ddc410bb2
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/26/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e3e7ca13c7a3f007c206bd56b8753166a2c264b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-model-for-azure-backup-reports"></a>Azure 備份報告的資料模型
本文說明用來建立 Azure Backup 報表 hello Power BI 資料模型。 使用此資料模型，您可以篩選相關的欄位為基礎的現有報表和多個重要的是，透過使用資料表和欄位 hello 模型中的建立您自己的報表。 

## <a name="creating-new-reports-in-power-bi"></a>在 Power BI 中建立新的報告
Power BI 提供自訂功能，您便可以使用[使用 hello 資料模型建立報表](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)。

## <a name="using-azure-backup-data-model"></a>使用 Azure 備份資料模型
您可以使用下列欄位當成模型 toocreate 報表 hello 資料的一部分，並自訂現有的報表提供 hello。

### <a name="alert"></a>警示
下表提供基本欄位和各種警示相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #AlertsCreatedInPeriod |整數 |所選時段內建立的警示數目 |
| %ActiveAlertsCreatedInPeriod |百分比 |所選時段內作用中警示的百分比 |
| %CriticalAlertsCreatedInPeriod |百分比 |所選時段內重大警示的百分比 |
| AlertOccurenceDate |日期 |警示的建立日期 |
| AlertSeverity |文字 |例如，重大 hello 警示嚴重性 |
| AlertStatus |文字 |例如，作用中的 hello 警示的狀態 |
| AlertType |文字 |例如，備份 hello 產生的警示類型 |
| AlertUniqueId |文字 |唯一識別碼 hello 產生警示 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| AvgResolutionTimeInMinsForAlertsCreatedInPeriod |十進位數字 |選取的時間間隔的平均時間 （以分鐘為單位） tooresolve 警示 |
| EntityState |文字 |例如，作用中、 已刪除的 hello 警示物件的目前狀態 |

### <a name="backup-item"></a>備份項目
下表提供基本欄位和各種備份項目相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #BackupItems |整數 |備份項目數目 |
| #UnprotectedBackupItems |整數 |已停止保護或已設定要備份卻未開始備份的備份項目數目|
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| BackupItemFriendlyName |文字 |備份項目的易記名稱 |
| BackupItemId |文字 |備份項目識別碼 |
| BackupItemName |文字 |備份項目名稱 |
| BackupItemType |文字 |備份項目類型 (例如，VM、FileFolder) |
| EntityState |文字 |例如，作用中、 已刪除的 hello 備份項目物件的目前狀態 |
| LastBackupDateTime |日期/時間 |所選備份項目的最後一次備份時間 |
| LastBackupState |文字 |所選備份項目的最後一次備份狀態 (例如，成功、失敗) |
| LastSuccessfulBackupDateTime |日期/時間 |所選備份項目最後一次成功備份的時間 |
| ProtectionState |文字 |例如，受保護、 ProtectionStopped hello 備份的項目目前保護狀態 |

### <a name="calendar"></a>行事曆
下表提供行事曆相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| 日期 |日期 |所選用於篩選資料的日期 |
| DateKey |文字 |每個日期項目的唯一索引鍵 |
| DayDiff |十進位數字 |用於篩選資料的日期差異，例如，0 代表當天的資料，-1 代表前一天的資料、0 和 -1 代表當天和前一天的資料  |
| 月 |文字 |月份的所選用於篩選資料的 hello 年、 月從第一天，結束第 31 天 |
| MonthDate | Date |當月結束，hello 月份中的日期所選用於篩選資料 |
| MonthDiff |十進位數字 |用於篩選資料的月份差異，例如，0 代表當月的資料，-1 代表上個月的資料、0 和 -1 代表當月和上個月的資料 |
| 週 |文字 |所選用於篩選資料的週別，一週的計算會從星期日開始，到星期六結束 |
| WeekDate |Date |日期 hello 一週的當週結束時，所選用於篩選資料 |
| WeekDiff |十進位數字 |用於篩選資料的週別差異，例如，0 代表當週的資料，-1 代表上週的資料、0 和 -1 代表當週和上週的資料 |
| Year |文字 |所選用於篩選資料的日曆年度 |
| YearDate |Date |日期 hello 年度當年度結束時，所選用於篩選資料 |

### <a name="job"></a>作業
下表提供基本欄位和各種作業相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #JobsCreatedInPeriod |整數 |在選取的時間週期的 hello 中建立的作業數目 |
| %FailuresForJobsCreatedInPeriod |百分比 |百分比整體工作失敗，在選取的時間週期的 hello |
| 80thPercentileDataTransferredInMBForBackupJobsCreatedInPeriod |十進位數字 |80th 百分位數值的資料傳輸以 mb 為單位**備份**hello 選取的時間週期中建立的工作 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| AvgBackupDurationInMinsForJobsCreatedInPeriod |十進位數字 |所選時段內建立之**備份作業已完成者**的平均完成時間 (以分鐘為單位) |
| AvgRestoreDurationInMinsForJobsCreatedInPeriod |十進位數字 |所選時段內建立之**還原作業已完成者**的平均完成時間 (以分鐘為單位) |
| BackupStorageDestination |文字 |備份儲存體的目的地 (例如，雲端、磁碟)  |
| EntityState |文字 |例如，作用中、 已刪除的 hello 工作物件的目前狀態 |
| JobFailureCode |文字 |由於發生作業失敗而產生的失敗碼字串 |
| JobOperation |文字 |執行作業的操作 (例如，備份、還原、設定備份) |
| JobStartDate |日期 |開始執行作業的日期 |
| JobStartTime |時間 |開始執行作業的時間 |
| JobStatus |文字 |狀態的 hello 完成作業，例如已完成、 失敗 |
| JobUniqueId |文字 |唯一識別碼 tooidentify hello 工作 |

### <a name="policy"></a>原則
下表提供基本欄位和各種原則相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #Policies |整數 |許多 hello 系統中存在的備份原則 |
| #PoliciesInUse |整數 |目前正用於設定備份的原則數目 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| BackupDaysOfTheWeek |文字 |當已排程備份的 hello 一周天數 |
| BackupFrequency |文字 |備份的執行頻率 (例如，每日、每週) |
| BackupTimes |文字 |排定要備份的日期和時間 |
| DailyRetentionDuration |整數 |所設定備份的總保留期間 (以天為單位) |
| DailyRetentionTimes |文字 |每日保留期的設定日期和時間 |
| EntityState |文字 |例如，作用中、 已刪除的 hello 原則物件的目前狀態 |
| MonthlyRetentionDaysOfTheMonth |文字 |選取每月保留期的 hello 月份的日期 |
| MonthlyRetentionDaysOfTheWeek |文字 |選取每月保留期的 hello 週間日 |
| MonthlyRetentionDuration |十進位數字 |所設定備份的總保留期間 (以月為單位) |
| MonthlyRetentionFormat |文字 |每月保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| MonthlyRetentionTimes |文字 |每月保留期的設定日期和時間 |
| MonthlyRetentionWeeksOfTheMonth |文字 |每月保留期時的 hello 月份的週數，例如設定第一個、 最後一個等。 |
| PolicyName |文字 |Hello 原則定義名稱 |
| PolicyUniqueId |文字 |唯一識別碼 tooidentify hello 原則 |
| RetentionType |文字 |保留原則類型 (例如，每天、每週、每月、每年) |
| WeeklyRetentionDaysOfTheWeek |文字 |選取每週保留期的 hello 週間日 |
| WeeklyRetentionDuration |十進位數字 |所設定備份的每週保留總期間 (以週為單位) |
| WeeklyRetentionTimes |文字 |每週保留期的設定日期和時間 |
| YearlyRetentionDaysOfTheMonth |文字 |選取每年保留期的 hello 月份的日期 |
| YearlyRetentionDaysOfTheWeek |文字 |每年保留期選取 hello 週的星期幾 |
| YearlyRetentionDuration |十進位數字 |所設定備份的總保留期間 (以年為單位) |
| YearlyRetentionFormat |文字 |每年保留期的設定類型 (例如，以天為基礎則每日、以週為基礎則每週) |
| YearlyRetentionMonthsOfTheYear |文字 |Hello 年度月份選取每年保留期 |
| YearlyRetentionTimes |文字 |每年保留期的設定日期和時間 |
| YearlyRetentionWeeksOfTheMonth |文字 |每年保留期時的 hello 月份的週數，例如設定第一個、 最後一個等。 |

### <a name="protected-server"></a>受保護的伺服器
下表提供基本欄位和各種受保護伺服器相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #ProtectedServers |整數 |受保護的伺服器數目 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| AzureBackupAgentOSType |文字 |Azure 備份代理程式的 OS 類型 |
| AzureBackupAgentOSVersion |文字 |Azure 備份代理程式的 OS 版本 |
| AzureBackupAgentUpdateDate |文字 |代理程式備份代理程式的更新日期 |
| AzureBackupAgentVersion |文字 |代理程式備份版本的版本號碼 |
| BackupManagementType |文字 |用於執行備份的提供者類型 (例如，IaaSVM、FileFolder) |
| EntityState |文字 |例如，作用中、 已刪除的 hello 受保護的伺服器物件的目前狀態 |
| ProtectedServerFriendlyName |文字 |受保護伺服器的易記名稱 |
| ProtectedServerName |文字 |受保護伺服器的名稱 |
| ProtectedServerType |文字 |所備份的受保護伺服器類型 (例如，IaaSVMContainer) |
| ProtectedServerName |文字 |所屬的受保護的伺服器 toowhich 備份項目名稱 |
| RegisteredContainerId |文字 |已註冊要進行備份的容器識別碼 |

### <a name="storage"></a>儲存體
下表提供基本欄位和各種儲存體相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #ProtectedInstances |十進位數字 |用於在帳單中計算前端儲存體的受保護執行個體數目，在計算時會以所選時間內的最後數值為依據 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| CloudStorageInMB |十進位數字 |備份所使用的雲端備份儲存體，在計算時會以所選時間內的最後數值為依據 |
| EntityState |文字 |例如，作用中、 已刪除的 hello 物件目前的狀態 |
| LastUpdatedDate |日期 |所選資料列的上次更新日期 |

### <a name="time"></a>時間
下表提供時間相關欄位的詳細資料。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| 小時 |時間 |Hello 天，例如 1:00:00 PM 的小時數 |
| HourNumber |十進位數字 |在 hello 天，例如 13.00 的小時數 |
| 分鐘 |十進位數字 |Hello 小時的分鐘數 |
| PeriodOfTheDay |文字 |Hello 天，例如上午 12-3 中的時間週期位置 |
| 時間 |時間 |Hello 一天，例如 12:00:01 AM 的時間 |
| TimeKey |文字 |索引鍵值 toorepresent 時間 |

### <a name="vault"></a>保存庫
下表提供基本欄位和各種保存庫相關欄位的彙總。

| 欄位 | 資料類型 | 說明 |
| --- | --- | --- |
| #Vaults |整數 |保存庫數目 |
| AsOnDateTime |日期/時間 |最新重新整理 hello 選取的資料列的時間 |
| AzureDataCenter |文字 |保存庫所在的資料中心 |
| EntityState |文字 |例如，作用中、 已刪除的 hello 保存庫物件目前的狀態 |
| StorageReplicationType |文字 |Hello 保存庫，例如 GeoRedundant 的儲存體複寫類型 |
| SubscriptionId |文字 |選取要產生報表的 hello 客戶的訂用帳戶 Id |
| VaultName |文字 |Hello 保存庫的名稱 |
| VaultTags |文字 |標記相關聯的 toohello 保存庫 |

## <a name="next-steps"></a>後續步驟
一旦檢閱 hello 資料模型來建立 Azure Backup 報表時，請參閱下列文件，如需詳細資訊，建立和檢視報表，在 Power BI 中的 hello。

* [在 Power BI 中建立報告](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)
* [在 Power BI 中篩選報告](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
