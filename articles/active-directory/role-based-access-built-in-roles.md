---
title: "aaaActions 以及 NotActions-Azure 角色型存取控制 (RBAC) |Microsoft 文件"
description: "本主題描述 hello 內建的角色型存取控制 (RBAC) 的角色。 hello 角色持續加入，因此核取 hello 文件有效性。"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: 
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/28/2017
ms.author: andredm
ms.reviewer: 
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a4ef9923fe05ec38e968534951911eaa4440b88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="built-in-roles-for-azure-role-based-access-control"></a>Azure 角色型存取控制的內建角色
Azure 角色型存取控制 (RBAC) 隨附於下列內建角色指派 toousers、 群組和服務的 hello。 您無法修改 hello 定義的內建的角色。 不過，您可以建立[Azure rbac 進行中的自訂角色](role-based-access-control-custom-roles.md)toofit hello 的特定需求的組織。

## <a name="roles-in-azure"></a>Azure 中的角色
hello 下表提供的 hello 的簡短說明內建的角色。 按一下 hello 角色名稱 toosee hello 的詳細的清單**動作**和**notactions** hello 角色。 hello**動作**屬性會指定 hello Azure 資源上允許的動作。 動作字串可以使用萬用字元。 hello **notactions**屬性會指定 hello 動作排除在 hello 允許的動作。

hello 動作會定義您可以在指定的資源類型執行的作業的類型。 例如：
- **寫入**可讓您 tooperform PUT、 POST、 PATCH、 和刪除作業。
- **讀取**可讓您 tooperform GET 作業。

本文只解決 hello 今日的不同角色。 當您指派角色 tooa 使用者時，不過，您可以限制 hello 允許進一步的動作所定義的範圍。 這是有幫助，如果您想要讓 toomake 人網站參與者，但是僅針對一個資源群組。

> [!NOTE]
> 不斷演變的 hello Azure 角色定義。 這篇文章會保留為向上 toodate 越好，但是您可以一律找到 hello 最新的角色定義在 Azure PowerShell 中。 使用 hello [Get AzureRmRoleDefinition](/powershell/module/azurerm.resources/get-azurermroledefinition) cmdlet toolist 所有目前的角色。 您可以深入了解在特定角色中使用 tooa`(get-azurermroledefinition "<role name>").actions`或`(get-azurermroledefinition "<role name>").notactions`適用。 使用[Get AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) toolist 作業特定的 Azure 資源提供者。


| 角色名稱 | 說明 |
| --- | --- |
| [API 管理服務參與者](#api-management-service-contributor) |可以管理 API 管理服務和應用程式開發介面 hello |
| [API 管理服務操作員角色](#api-management-service-operator-role) | 可以管理 API 管理服務，但 hello 本身應用程式開發介面 |
| [API 管理服務讀取者角色](#api-management-service-reader-role) | 唯讀存取 tooAPI 管理服務和應用程式開發介面 |
| [Application Insights 元件參與者](#application-insights-component-contributor) |可以管理 Application Insights 元件 |
| [自動化運算子](#automation-operator) |無法 toostart，停止、 暫停和繼續工作 |
| [備份參與者](#backup-contributor) | 可以管理復原服務保存庫中的備份 |
| [備份操作員](#backup-operator) | 可以管理復原服務保存庫中的備份，但不能移除備份 |
| [備份讀取者](#backup-reader) | 可以檢視所有的備份管理服務  |
| [帳單讀取器](#billing-reader) | 可檢視所有帳單資訊  |
| [BizTalk 參與者](#biztalk-contributor) |可以管理 BizTalk 服務 |
| [ClearDB MySQL DB 參與者](#cleardb-mysql-db-contributor) |可以管理 ClearDB MySQL 資料庫 |
| [參與者](#contributor) |可以管理存取以外的所有內容。 |
| [Data Factory 參與者](#data-factory-contributor) |可以建立和管理 Data Factory 以及其中的子資源。 |
| [DevTest Labs 使用者](#devtest-labs-user) |可以檢視所有項目，並連接、啟動、重新啟動和關閉虛擬機器 |
| [DNS 區域參與者](#dns-zone-contributor) |可以管理 DNS 區域和記錄 |
| [Azure Cosmos DB 帳戶參與者](#documentdb-account-contributor) |可以管理 Azure Cosmos DB 帳戶 |
| [Intelligent Systems 帳戶參與者](#intelligent-systems-account-contributor) |可以管理 Intelligent Systems 帳戶 |
| 邏輯應用程式參與者 | 可以管理邏輯應用程式的所有層面，但是無法建立新的層面。 |
| 邏輯應用程式操作員 |可以啟動及停止在邏輯應用程式內定義的工作流程。 |
| [監視讀取器](#monitoring-reader) |可以讀取所有監視資料 |
| [監視參與者](#monitoring-contributor) |可以讀取監視資料並編輯監視設定 |
| [網路參與者](#network-contributor) |可以管理網路資源 |
| [New Relic APM 帳戶參與者](#new-relic-apm-account-contributor) |可以管理 New Relic 應用程式效能管理帳戶和應用程式 |
| [擁有者](#owner) |可以管理所有項目，包括存取 |
| [讀取者](#reader) |可以檢視所有項目，但是無法進行變更 |
| [Redis 快取參與者](#redis-cache-contributor) |可以管理 Redis 快取 |
| [排程器工作集合參與者](#scheduler-job-collections-contributor) |可以管理排程器工作集合 |
| [搜尋服務參與者](#search-service-contributor) |可以管理搜尋服務 |
| [安全性管理員](#security-manager) |可以管理安全性元件、安全性原則及虛擬機器 |
| [Site Recovery 參與者](#site-recovery-contributor) | 可以管理復原服務保存庫中的 Site Recovery |
| [Site Recovery 操作員](#site-recovery-operator) | 可以管理復原服務保存庫中 Site Recovery 的容錯移轉和容錯回復作業 |
| [Site Recovery 讀取者](#site-recovery-reader) | 可以檢視所有 Site Recovery 管理作業  |
| [SQL DB 參與者](#sql-db-contributor) |可以管理 SQL 資料庫，但是無法管理它們的安全性相關原則 |
| [SQL 安全性管理員](#sql-security-manager) |可以管理 hello SQL 伺服器和資料庫的安全性相關原則 |
| [SQL Server 參與者](#sql-server-contributor) |可以管理 SQL Server 和資料庫，但是無法管理它們的安全性相關原則 |
| [傳統儲存體帳戶參與者](#classic-storage-account-contributor) |可以管理傳統儲存體帳戶 |
| [儲存體帳戶參與者](#storage-account-contributor) |可以管理儲存體帳戶 |
| [支援要求參與者](#support-request-contributor) | 可以建立及管理支援要求 |
| [使用者存取系統管理員](#user-access-administrator) |可以管理使用者存取 tooAzure 資源 |
| [傳統虛擬機器參與者](#classic-virtual-machine-contributor) |可管理傳統的虛擬機器，但不是 hello 虛擬網路或儲存體帳戶 toowhich 連線 |
| [虛擬機器參與者](#virtual-machine-contributor) |可以管理虛擬機器，但不是 hello 虛擬網路或存放裝置帳戶 toowhich 連線 |
| [傳統網路參與者](#classic-network-contributor) |可以管理傳統虛擬網路和保留 IP |
| [Web 方案參與者](#web-plan-contributor) |可以管理 Web 方案 |
| [網站參與者](#website-contributor) |可以管理網站，但不是 hello web 計劃 toowhich 連線 |

## <a name="role-permissions"></a>角色權限
hello 下列表格說明 hello tooeach 權限的特定權限。 這可以包括授與權限的 **Actions** 和限制權限的 **NotActions**。

### <a name="api-management-service-contributor"></a>API 管理服務參與者
可以管理 API 管理服務

| **動作** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/* |建立和管理 API 管理服務 |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取角色和角色指派 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="api-management-service-operator-role"></a>API 管理服務操作員角色
可以管理 API 管理服務

| **動作** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | 讀取 API 管理服務執行個體 |
| Microsoft.ApiManagement/Service/backup/action | 備份 API 管理服務 toohello 指定容器中使用者，提供儲存體帳戶 |
| Microsoft.ApiManagement/Service/delete | 刪除 API 管理服務執行個體 |
| Microsoft.ApiManagement/Service/managedeployments/action | 變更 SKU/單位；新增或移除 API 管理服務的區域部署 |
| Microsoft.ApiManagement/Service/read | 讀取 API 管理服務執行個體的中繼資料 |
| Microsoft.ApiManagement/Service/restore/action | 還原使用者，提供儲存體帳戶中的 hello 指定容器的 API 管理服務 |
| Microsoft.ApiManagement/Service/updatehostname/action | 設定、更新或移除 API 管理服務的自訂網域名稱 |
| Microsoft.ApiManagement/Service/write | 建立 API 管理服務的新執行個體 |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取角色和角色指派 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="api-management-service-reader-role"></a>API 管理服務讀取者角色
可以管理 API 管理服務

| **動作** |  |
| --- | --- |
| Microsoft.ApiManagement/Service/*/read | 讀取 API 管理服務執行個體 |
| Microsoft.ApiManagement/Service/read | 讀取 API 管理服務執行個體的中繼資料 |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取角色和角色指派 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="application-insights-component-contributor"></a>Application Insights 元件參與者
可以管理 Application Insights 元件

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.Insights/components/* |建立和管理 Insights 元件 |
| Microsoft.Insights/webtests/* |建立和管理 Web 測試 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="automation-operator"></a>自動化運算子
無法 toostart，停止、 暫停和繼續工作

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Automation/automationAccounts/jobs/read |讀取自動化帳戶工作 |
| Microsoft.Automation/automationAccounts/jobs/resume/action |繼續自動化帳戶工作 |
| Microsoft.Automation/automationAccounts/jobs/stop/action |停止自動化帳戶工作 |
| Microsoft.Automation/automationAccounts/jobs/streams/read |讀取自動化帳戶作業串流 |
| Microsoft.Automation/automationAccounts/jobs/suspend/action |暫停自動化帳戶工作 |
| Microsoft.Automation/automationAccounts/jobs/write |撰寫自動化帳戶工作 |
| Microsoft.Automation/automationAccounts/jobSchedules/read |讀取自動化帳戶工作排程 |
| Microsoft.Automation/automationAccounts/jobSchedules/write |讀取自動化帳戶工作排程 |
| Microsoft.Automation/automationAccounts/read |讀取自動化帳戶 |
| Microsoft.Automation/automationAccounts/runbooks/read |讀取自動化 Runbook |
| Microsoft.Automation/automationAccounts/schedules/read |讀取自動化帳戶排程 |
| Microsoft.Automation/automationAccounts/schedules/write |撰寫自動化帳戶排程 |
| Microsoft.Insights/components/* |建立和管理 Insights 元件 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="backup-contributor"></a>備份參與者
可以管理所有的備份管理動作，除了建立復原服務保存庫，並提供存取 tooothers

| **動作** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | 讀取虛擬網路 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/* | 管理備份管理上作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/* | 在復原服務保存庫的備份網狀架構內建立和管理備份容器 |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | 建立和管理備份作業 |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | 將備份作業匯出到 Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/* | 建立和管理中繼資料相關 toobackup 管理 |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | 建立和管理備份管理作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupPolicies/* | 建立和管理備份原則 |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | 建立和管理可以備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/* | 建立和管理備份項目 |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/* | 建立和管理保存備份項目的容器 |
| Microsoft.RecoveryServices/Vaults/certificates/* | 建立及管理復原服務保存庫中的憑證相關的 toobackup |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | 建立及管理相關的擴充的資訊 toovault |
| Microsoft.RecoveryServices/Vaults/read | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | 管理擷取新建立容器的探索作業 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | 建立和管理註冊的身分識別 |
| Microsoft.RecoveryServices/Vaults/usages/* | 建立和管理復原服務保存庫的使用方式 |
| Microsoft.Resources/deployments/* | 建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read | 讀取資源群組 |
| Microsoft.Storage/storageAccounts/read | 讀取儲存體帳戶 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="backup-operator"></a>備份操作員
可以管理建立保存庫、 移除備份和提供存取 tooothers 以外的所有備份的管理動作

| **動作** | |
| --- | --- |
| Microsoft.Network/virtualNetworks/read | 讀取虛擬網路 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read | 讀取備份管理上作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read | 讀取保護容器上的作業結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/backup/action | 在備份項目上執行隨選備份作業 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read | 讀取備份項目上執行作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read | 讀取備份項目上執行作業的狀態 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read | 讀取備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/read | 讀取備份項目的復原點 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/recoveryPoints/restore/action | 使字備份項目的復原點執行還原作業 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/write | 建立備份項目 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read | 讀取保存備份項目的容器 |
| Microsoft.RecoveryServices/Vaults/backupJobs/* | 建立和管理備份作業 |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | 將備份作業匯出到 Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read | 讀取的中繼資料相關 toobackup 管理 |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/* | 建立和管理備份管理作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read | 讀取備份原則上執行作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read | 讀取備份原則 |
| Microsoft.RecoveryServices/Vaults/backupProtectableItems/* | 建立和管理可以備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read | 讀取備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read | 讀取保存備份項目的備份容器 |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | 讀取延伸資訊相關 toovault |
| Microsoft.RecoveryServices/Vaults/extendedInformation/write | 寫入擴充資訊相關 toovault |
| Microsoft.RecoveryServices/Vaults/read | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/* | 管理擷取新建立容器的探索作業 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | Hello 保存庫的註冊項目執行讀取作業的結果 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | 讀取 hello 保存庫的已註冊的項目 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/write | 寫入登錄項目 toovault |
| Microsoft.RecoveryServices/Vaults/usages/read | 讀取的 hello 復原服務保存庫使用的方式 |
| Microsoft.Resources/deployments/* | 建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read | 讀取資源群組 |
| Microsoft.Storage/storageAccounts/read | 讀取儲存體帳戶 |
| Microsoft.Support/* | 建立和管理支援票證 |

### <a name="backup-reader"></a>備份讀取者
可以監視復原服務保存庫中的備份管理

| **動作** | |
| --- | --- |
| Microsoft.RecoveryServices/Vaults/backupFabrics/operationResults/read  | 讀取備份管理上作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/operationResults/read  | 讀取保護容器上的作業結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationResults/read  | 讀取備份項目上執行作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/operationStatus/read  | 讀取備份項目上執行作業的狀態 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/protectedItems/read  | 讀取備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupFabrics/protectionContainers/read  | 讀取保存備份項目的容器 |
| Microsoft.RecoveryServices/Vaults/backupJobs/operationResults/read  | 讀取備份作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupJobs/read  | 讀取備份作業 |
| Microsoft.RecoveryServices/Vaults/backupJobsExport/action | 將備份作業匯出到 Excel |
| Microsoft.RecoveryServices/Vaults/backupManagementMetaData/read  | 讀取的中繼資料相關 toobackup 管理 |
| Microsoft.RecoveryServices/Vaults/backupOperationResults/read  | 讀取備份管理作業結果 |
| Microsoft.RecoveryServices/Vaults/backupPolicies/operationResults/read  | 讀取備份原則上執行作業的結果 |
| Microsoft.RecoveryServices/Vaults/backupPolicies/read  | 讀取備份原則 |
| Microsoft.RecoveryServices/Vaults/backupProtectedItems/read  |  讀取備份的項目 |
| Microsoft.RecoveryServices/Vaults/backupProtectionContainers/read  | 讀取保存備份項目的備份容器 |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | 讀取延伸資訊相關 toovault |
| Microsoft.RecoveryServices/Vaults/read  | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | 讀取擷取新建立容器的探索作業結果 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | Hello 保存庫的註冊項目執行讀取作業的結果 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | 讀取 hello 保存庫的已註冊的項目 |
| Microsoft.RecoveryServices/Vaults/usages/read  |  讀取的 hello 復原服務保存庫使用的方式 |

### <a name="billing-reader"></a>帳單讀取器
可檢視所有帳單資訊

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Billing/*/read |讀取帳單資訊 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="biztalk-contributor"></a>BizTalk 參與者
可以管理 BizTalk 服務

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.BizTalkServices/BizTalk/* |建立和管理 BizTalk 服務 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="cleardb-mysql-db-contributor"></a>ClearDB MySQL DB 參與者
可以管理 ClearDB MySQL 資料庫

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |
| successbricks.cleardb/databases/* |建立和管理 ClearDB MySQL 資料庫 |

### <a name="contributor"></a>參與者
可以管理存取以外的所有內容

| **動作** |  |
| --- | --- |
| * |建立和管理所有類型的資源 |

| **NotActions** |  |
| --- | --- |
| Microsoft.Authorization/*/Delete |無法刪除角色和角色指派 |
| Microsoft.Authorization/*/Write |無法建立角色和角色指派 |

### <a name="data-factory-contributor"></a>Data Factory 參與者
建立和管理 Data Factory 以及其中的子資源。

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.DataFactory/dataFactories/* |建立和管理 Data Factory 以及其中的子資源。 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="devtest-labs-user"></a>DevTest Labs 使用者
可以檢視所有項目，並連接、啟動、重新啟動和關閉虛擬機器

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Compute/availabilitySets/read |讀取 hello 屬性的可用性設定組 |
| Microsoft.Compute/virtualMachines/*/read |讀取虛擬機器 （VM 大小、 執行階段狀態，VM 擴充功能等等） 的 hello 屬性 |
| Microsoft.Compute/virtualMachines/deallocate/action |取消配置虛擬機器 |
| Microsoft.Compute/virtualMachines/read |讀取虛擬機器的 hello 屬性 |
| Microsoft.Compute/virtualMachines/restart/action |重新啟動虛擬機器 |
| Microsoft.Compute/virtualMachines/start/action |啟動虛擬機器 |
| Microsoft.DevTestLab/*/read |讀取的實驗室環境的 hello 屬性 |
| Microsoft.DevTestLab/labs/createEnvironment/action |建立實驗室環境 |
| Microsoft.DevTestLab/labs/formulas/delete |刪除公式 |
| Microsoft.DevTestLab/labs/formulas/read |讀取公式 |
| Microsoft.DevTestLab/labs/formulas/write |新增或修改公式 |
| Microsoft.DevTestLab/labs/policySets/evaluatePolicies/action |評估實驗室原則 |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |加入負載平衡器後端位址集區 |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |加入負載平衡器輸入 NAT 規則 |
| Microsoft.Network/networkInterfaces/*/read |讀取網路介面的 hello 屬性 （例如，所有的 hello 負載平衡器 hello 網路介面是的一部分） |
| Microsoft.Network/networkInterfaces/join/action |加入虛擬機器 tooa 網路介面 |
| Microsoft.Network/networkInterfaces/read |讀取網路介面 |
| Microsoft.Network/networkInterfaces/write |撰寫網路介面 |
| Microsoft.Network/publicIPAddresses/*/read |讀取 hello 屬性的公用 IP 位址 |
| Microsoft.Network/publicIPAddresses/join/action |加入公用 IP 位址 |
| Microsoft.Network/publicIPAddresses/read |讀取網路公用 IP 位址 |
| Microsoft.Network/virtualNetworks/subnets/join/action |加入虛擬網路 |
| Microsoft.Resources/deployments/operations/read |讀取部署作業 |
| Microsoft.Resources/deployments/read |讀取部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Storage/storageAccounts/listKeys/action |列出儲存體帳戶金鑰 |

### <a name="dns-zone-contributor"></a>DNS 區域參與者
可以管理 DNS 區域和記錄。

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/\*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/\* |建立及管理警示規則 |
| Microsoft.Network/dnsZones/\* |建立和管理 DNS 區域和記錄 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取 hello hello 資源健全狀況 |
| Microsoft.Resources/deployments/\* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/\* |建立和管理支援票證 |

### <a name="azure-cosmos-db-account-contributor"></a>Azure Cosmos DB 帳戶參與者
可以管理 Azure Cosmos DB 帳戶

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.DocumentDb/databaseAccounts/* |建立及管理 DocumentDB 帳戶 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="intelligent-systems-account-contributor"></a>Intelligent Systems 帳戶參與者
可以管理 Intelligent Systems 帳戶

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.IntelligentSystems/accounts/* |建立及管理 Intelligent Systems 帳戶 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="monitoring-reader"></a>監視讀取器
可以讀取所有監視資料 (計量、記錄檔等等)。 請參閱[開始使用 Azure 監視器的角色、權限和安全性](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles)。

| **動作** |  |
| --- | --- |
| */read |讀取密碼以外的所有類型的資源。 |
| Microsoft.OperationalInsights/workspaces/search/action |搜尋 Log Analytics 資料 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="monitoring-contributor"></a>監視參與者
可以讀取所有監視資料並編輯監視設定。 請參閱[開始使用 Azure 監視器的角色、權限和安全性](/monitoring-and-diagnostics/monitoring-roles-permissions-security.md#built-in-monitoring-roles)。

| **動作** |  |
| --- | --- |
| */read |讀取密碼以外的所有類型的資源。 |
| Microsoft.Insights/AlertRules/* |讀取/寫入/刪除警示規則。 |
| Microsoft.Insights/components/* |讀取/寫入/刪除 Application Insights 元件。 |
| Microsoft.Insights/DiagnosticSettings/* |讀取/寫入/刪除診斷設定。 |
| Microsoft.Insights/eventtypes/* |列出訂用帳戶中的活動記錄檔事件 (管理事件)。 此權限是適用的 tooboth 程式設計和入口網站存取 toohello 活動記錄檔。 |
| Microsoft.Insights/LogDefinitions/* |此權限是必要的使用者需要存取 tooActivity 透過 hello 入口網站的記錄檔。 列出活動記錄檔中的記錄檔分類。 |
| Microsoft.Insights/MetricDefinitions/* |讀取度量定義 (可用資源的度量類型清單)。 |
| Microsoft.Insights/Metrics/* |讀取資源的度量。 |
| Microsoft.Insights/Register/Action |註冊 hello Microsoft.Insights 提供者。 |
| Microsoft.Insights/webtests/* |讀取/寫入/刪除 Application Insights Web 測試。 |
| Microsoft.OperationalInsights/workspaces/intelligencepacks/* |讀取/寫入/刪除 Log Analytics 解決方案套件。 |
| Microsoft.OperationalInsights/workspaces/savedSearches/* |讀取/寫入/刪除 Log Analytics 已儲存的搜尋。 |
| Microsoft.OperationalInsights/workspaces/search/action |搜尋 Log Analytics 工作區。 |
| Microsoft.OperationalInsights/workspaces/sharedKeys/action |列出 Log Analytics 工作區的金鑰。 |
| Microsoft.OperationalInsights/workspaces/storageinsightconfigs/* |讀取/寫入/刪除 Log Analytics 儲存體深入解析設定。 |

### <a name="network-contributor"></a>網路參與者
可以管理網路資源

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.Network/* |建立和管理網路 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="new-relic-apm-account-contributor"></a>New Relic APM 帳戶參與者
可以管理 New Relic 應用程式效能管理帳戶和應用程式

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |
| NewRelic.APM/accounts/* |建立和管理 New Relic 應用程式效能管理帳戶 |

### <a name="owner"></a>擁有者
可以管理所有項目，包括存取

| **動作** |  |
| --- | --- |
| * |建立和管理所有類型的資源 |

### <a name="reader"></a>讀取者
可以檢視所有項目，但是無法進行變更

| **動作** |  |
| --- | --- |
| */read |讀取密碼以外的所有類型的資源。 |

### <a name="redis-cache-contributor"></a>Redis 快取參與者
可以管理 Redis 快取

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Cache/redis/* |建立和管理 Redis 快取 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="scheduler-job-collections-contributor"></a>排程器工作集合參與者
可以管理排程器工作集合

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Scheduler/jobcollections/* |建立和管理工作集合 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="search-service-contributor"></a>搜尋服務參與者
可以管理搜尋服務

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Search/searchServices/* |建立和管理搜尋服務 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="security-manager"></a>安全性管理員
可以管理安全性元件、安全性原則及虛擬機器

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.ClassicCompute/*/read |讀取傳統運算虛擬機器的組態資訊 |
| Microsoft.ClassicCompute/virtualMachines/*/write |撰寫虛擬機器的組態 |
| Microsoft.ClassicNetwork/*/read |讀取傳統網路的組態資訊 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Security/* |建立和管理安全性元件和原則 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="site-recovery-contributor"></a>Site Recovery 參與者
可以管理所有的站台復原管理動作，除了建立復原服務保存庫並指派存取權限 tooother 使用者

| **動作** | |
| --- | --- |
| Microsoft.Authorization/*/read | 讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* | 建立及管理警示規則 |
| Microsoft.Network/virtualNetworks/read | 讀取虛擬網路 |
| Microsoft.RecoveryServices/Vaults/certificates/write | 更新 hello 保存庫認證憑證 |
| Microsoft.RecoveryServices/Vaults/extendedInformation/* | 建立及管理相關的擴充的資訊 toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | 讀取 hello 復原服務保存庫的警示 |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | 讀取復原服務保存庫通知設定 |
| Microsoft.RecoveryServices/Vaults/read | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | 管理擷取新建立容器的探索作業 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/* | 建立和管理註冊的身分識別 |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/* | 建立或更新複寫警示設定 |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | 讀取複寫事件 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/* | 建立和管理複寫網狀架構 |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | 建立和管理複寫作業 |
| Microsoft.RecoveryServices/vaults/replicationPolicies/* | 建立和管理複寫原則 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/* | 建立和管理復原計劃 |
| Microsoft.RecoveryServices/Vaults/storageConfig/* | 建立和管理復原服務保存庫的儲存體設定 |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | 讀取復原服務保存庫權杖資訊 |
| Microsoft.RecoveryServices/Vaults/usages/read | 讀取復原服務保存庫的使用量詳細資料 |
| Microsoft.ResourceHealth/availabilityStatuses/read | 讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* | 建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read | 讀取資源群組 |
| Microsoft.Storage/storageAccounts/read | 讀取儲存體帳戶 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="site-recovery-operator"></a>Site Recovery 操作員
可以使用容錯移轉和容錯回復，但是可以不執行其他站台復原 」 管理動作或指派存取 tooother 使用者

| **動作** | |
| --- | --- |
| Microsoft.Authorization/*/read | 讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* | 建立及管理警示規則 |
| Microsoft.Network/virtualNetworks/read | 讀取虛擬網路 |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read | 讀取延伸資訊相關 toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/*  | 讀取 hello 復原服務保存庫的警示 |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | 讀取復原服務保存庫通知設定 |
| Microsoft.RecoveryServices/Vaults/read | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read | 管理擷取新建立容器的探索作業 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read | 讀取已提交作業的作業狀態和結果 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read | 讀取資源的已註冊容器 |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | 讀取複寫警示設定 |
| Microsoft.RecoveryServices/vaults/replicationEvents/read | 讀取複寫事件 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/checkConsistency/action | 檢查一致性 hello 網狀架構 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read | 讀取複寫網狀架構 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ reassociateGateway/action | 重新關聯複寫閘道 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/renewcertificate/action | 更新複寫網狀架構憑證 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read | 讀取複寫網狀架構網路 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read | 讀取複寫網狀架構網路對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read | 讀取保護容器 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read | 取得所有可保護項目的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ applyRecoveryPoint/action | 套用特定復原點 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ failoverCommit/action | 認可容錯移轉項目的容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ plannedFailover/action | 啟動受保護項目的計劃性容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read | 取得所有受保護項目的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read | 取得可用復原點的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ repairReplication/action | 修復受保護項目的複寫 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/reProtect/action | 開始受保護項目的重新保護|
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/testFailover/action | 啟動受保護項目的測試容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ testFailoverCleanup/action | 啟動測試容錯移轉的清除 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ unplannedFailover/action | 啟動受保護項目的未計劃容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/ updateMobilityService/action | 更新 hello 行動服務 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read | 讀取保護容器對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read | 讀取復原服務提供者 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/refreshProvider/action | 重新整理復原服務提供者 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read | 讀取複寫網狀架構的儲存體分類 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read | 讀取儲存體分類對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read | 讀取已註冊 vCenter 資訊 |
| Microsoft.RecoveryServices/vaults/replicationJobs/* | 建立和管理複寫作業 |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read | 讀取複寫原則 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ failoverCommit/action | 認可復原方案容錯移轉的容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ plannedFailover/action | 啟動復原方案的容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read | 讀取復原方案 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/reProtect/action | 啟動復原方案的重新保護 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/testFailover/action | 啟動復原方案的測試容錯移轉 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ testFailoverCleanup/action | 啟動復原方案測試容錯移轉的清除 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/ unplannedFailover/action | 啟動復原方案的未計劃容錯移轉 |
| Microsoft.RecoveryServices/Vaults/storageConfig/read | 讀取復原服務保存庫的儲存體設定 |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read | 讀取復原服務保存庫權杖資訊 |
| Microsoft.RecoveryServices/Vaults/usages/read | 讀取復原服務保存庫的使用量詳細資料 |
| Microsoft.ResourceHealth/availabilityStatuses/read | 讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* | 建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read | 讀取資源群組 |
| Microsoft.Storage/storageAccounts/read | 讀取儲存體帳戶 |
| Microsoft.Support/* | 建立和管理支援票證 |

### <a name="site-recovery-reader"></a>Site Recovery 讀取者
可以監視復原服務保存庫中的 Site Recovery 狀態，並且引發支援票證

| **動作** | |
| --- | --- |
| Microsoft.Authorization/*/read | 讀取角色和角色指派 |
| Microsoft.RecoveryServices/Vaults/extendedInformation/read  | 讀取延伸資訊相關 toovault |
| Microsoft.RecoveryServices/Vaults/monitoringAlerts/read  | 讀取 hello 復原服務保存庫的警示 |
| Microsoft.RecoveryServices/Vaults/monitoringConfigurations/ notificationConfiguration/read  | 讀取復原服務保存庫通知設定 |
| Microsoft.RecoveryServices/Vaults/read  | 讀取復原服務保存庫 |
| Microsoft.RecoveryServices/Vaults/refreshContainers/read  | 管理擷取新建立容器的探索作業 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/operationResults/read  | 讀取已提交作業的作業狀態和結果 |
| Microsoft.RecoveryServices/Vaults/registeredIdentities/read  | 讀取資源的已註冊容器 |
| Microsoft.RecoveryServices/vaults/replicationAlertSettings/read | 讀取複寫警示設定 |
| Microsoft.RecoveryServices/vaults/replicationEvents/read  | 讀取複寫事件 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/read  | 讀取複寫網狀架構 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationNetworks/read  | 讀取複寫網狀架構網路 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationNetworks/replicationNetworkMappings/read  | 讀取複寫網狀架構網路對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/read  |  讀取保護容器 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectableItems/read  | 取得所有可保護項目的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/read  | 取得所有受保護項目的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectedItems/recoveryPoints/read  | 取得可用復原點的清單 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationProtectionContainers/replicationProtectionContainerMappings/read  | 讀取保護容器對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationRecoveryServicesProviders/read  | 讀取復原服務提供者 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/read  | 讀取複寫網狀架構的儲存體分類 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/ replicationStorageClassifications/replicationStorageClassificationMappings/read  |  讀取儲存體分類對應 |
| Microsoft.RecoveryServices/vaults/replicationFabrics/replicationvCenters/read  |  讀取已註冊 vCenter 資訊 |
| Microsoft.RecoveryServices/vaults/replicationJobs/read  |  讀取複寫作業的狀態 |
| Microsoft.RecoveryServices/vaults/replicationPolicies/read  |  讀取複寫原則 |
| Microsoft.RecoveryServices/vaults/replicationRecoveryPlans/read  |  讀取復原方案 |
| Microsoft.RecoveryServices/Vaults/storageConfig/read  |  讀取復原服務保存庫的儲存體設定 |
| Microsoft.RecoveryServices/Vaults/tokenInfo/read  |  讀取復原服務保存庫權杖資訊 |
| Microsoft.RecoveryServices/Vaults/usages/read  |  讀取復原服務保存庫的使用量詳細資料 |
| Microsoft.Support/*  |  建立和管理支援票證 |

### <a name="sql-db-contributor"></a>SQL DB 參與者
可以管理 SQL 資料庫，但是無法管理它們的安全性相關原則

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取角色和角色指派 |
| Microsoft.Insights/alertRules/* |建立及管理警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Sql/servers/databases/* |建立和管理 SQL 資料庫 |
| Microsoft.Sql/servers/read |讀取 SQL Server |
| Microsoft.Support/* |建立和管理支援票證 |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/databases/auditingPolicies/* |無法編輯稽核原則 |
| Microsoft.Sql/servers/databases/auditingSettings/* |無法編輯稽核設定 |
| Microsoft.Sql/servers/databases/auditRecords/read |無法讀取稽核記錄 |
| Microsoft.Sql/servers/databases/connectionPolicies/* |無法編輯連接原則 |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |無法編輯資料遮罩原則 |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |無法編輯安全性警示原則 |
| Microsoft.Sql/servers/databases/securityMetrics/* |無法編輯安全性度量 |

### <a name="sql-security-manager"></a>SQL 安全性管理員
可以管理 hello SQL 伺服器和資料庫的安全性相關原則

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取 Microsoft 授權 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Sql/servers/auditingPolicies/* |建立和管理 SQL Server 稽核原則 |
| Microsoft.Sql/servers/auditingSettings/* |建立和管理 SQL Server 稽核設定 |
| Microsoft.Sql/servers/databases/auditingPolicies/* |建立和管理 SQL Server 資料庫稽核原則 |
| Microsoft.Sql/servers/databases/auditingSettings/* |建立和管理 SQL Server 資料庫稽核設定 |
| Microsoft.Sql/servers/databases/auditRecords/read |讀取稽核記錄 |
| Microsoft.Sql/servers/databases/connectionPolicies/* |建立和管理 SQL Server 資料庫連接原則 |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |建立和管理 SQL Server 資料庫資料遮罩原則 |
| Microsoft.Sql/servers/databases/read |讀取 SQL 資料庫 |
| Microsoft.Sql/servers/databases/schemas/read |讀取 SQL Server 資料庫結構描述 |
| Microsoft.Sql/servers/databases/schemas/tables/columns/read |讀取 SQL Server 資料庫資料表資料行 |
| Microsoft.Sql/servers/databases/schemas/tables/read |讀取 SQL Server 資料庫資料表 |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |建立和管理 SQL Server 資料庫安全性警示原則 |
| Microsoft.Sql/servers/databases/securityMetrics/* |建立和管理 SQL Server 資料庫安全性度量 |
| Microsoft.Sql/servers/read |讀取 SQL Server |
| Microsoft.Sql/servers/securityAlertPolicies/* |建立和管理 SQL Server 安全性警示原則 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="sql-server-contributor"></a>SQL Server 參與者
可以管理 SQL Server 和資料庫，但是無法管理它們的安全性相關原則

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Sql/servers/* |建立和管理 SQL Server |
| Microsoft.Support/* |建立和管理支援票證 |

| **NotActions** |  |
| --- | --- |
| Microsoft.Sql/servers/auditingPolicies/* |無法編輯 SQL Server 稽核原則 |
| Microsoft.Sql/servers/auditingSettings/* |無法編輯 SQL Server 稽核設定 |
| Microsoft.Sql/servers/databases/auditingPolicies/* |無法編輯 SQL Server 資料庫稽核原則 |
| Microsoft.Sql/servers/databases/auditingSettings/* |無法編輯 SQL Server 資料庫稽核設定 |
| Microsoft.Sql/servers/databases/auditRecords/read |無法讀取稽核記錄 |
| Microsoft.Sql/servers/databases/connectionPolicies/* |無法編輯 SQL Server 資料庫連接原則 |
| Microsoft.Sql/servers/databases/dataMaskingPolicies/* |無法編輯 SQL Server 資料庫資料遮罩原則 |
| Microsoft.Sql/servers/databases/securityAlertPolicies/* |無法編輯 SQL Server 資料庫安全性警示原則 |
| Microsoft.Sql/servers/databases/securityMetrics/* |無法編輯 SQL Server 資料庫安全性度量 |
| Microsoft.Sql/servers/securityAlertPolicies/* |無法編輯 SQL Server 安全性警示原則 |

### <a name="classic-storage-account-contributor"></a>傳統儲存體帳戶參與者
可以管理傳統儲存體帳戶

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.ClassicStorage/storageAccounts/* |建立及管理儲存體帳戶 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="storage-account-contributor"></a>儲存體帳戶參與者
可以管理儲存體帳戶，但是不會存取 toothem。

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取所有授權 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.Insights/diagnosticSettings/* |管理診斷設定 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Storage/storageAccounts/* |建立及管理儲存體帳戶 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="support-request-contributor"></a>支援要求參與者
可以建立及管理支援票證 hello 訂用帳戶範圍

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read | 讀取授權 |
| Microsoft.Support/* | 建立和管理支援票證 |
| Microsoft.Resources/subscriptions/resourceGroups/read | 讀取角色和角色指派 |

### <a name="user-access-administrator"></a>使用者存取系統管理員
可以管理使用者存取 tooAzure 資源

| **動作** |  |
| --- | --- |
| */read |讀取密碼以外的所有類型的資源。 |
| Microsoft.Authorization/* |管理授權 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="classic-virtual-machine-contributor"></a>傳統虛擬機器參與者
可管理傳統虛擬機器，但不是 hello 虛擬網路或儲存體帳戶 toowhich 連線

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.ClassicCompute/domainNames/* |建立和管理傳統運算網域名稱 |
| Microsoft.ClassicCompute/virtualMachines/* |建立和管理虛擬機器 |
| Microsoft.ClassicNetwork/networkSecurityGroups/join/action |加入網路安全性群組 |
| Microsoft.ClassicNetwork/reservedIps/link/action |連結保留 IP |
| Microsoft.ClassicNetwork/reservedIps/read |讀取保留的 IP 位址 |
| Microsoft.ClassicNetwork/virtualNetworks/join/action |加入虛擬網路 |
| Microsoft.ClassicNetwork/virtualNetworks/read |讀取虛擬網路 |
| Microsoft.ClassicStorage/storageAccounts/disks/read |讀取儲存體帳戶磁碟 |
| Microsoft.ClassicStorage/storageAccounts/images/read |讀取儲存體帳戶映像 |
| Microsoft.ClassicStorage/storageAccounts/listKeys/action |列出儲存體帳戶金鑰 |
| Microsoft.ClassicStorage/storageAccounts/read |讀取傳統儲存體帳戶 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="virtual-machine-contributor"></a>虛擬機器參與者
可以管理虛擬機器，但不是 hello 虛擬網路或存放裝置帳戶 toowhich 連線

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Compute/availabilitySets/* |建立和管理運算可用性集合 |
| Microsoft.Compute/locations/* |建立和管理運算位置 |
| Microsoft.Compute/virtualMachines/* |建立和管理虛擬機器 |
| Microsoft.Compute/virtualMachineScaleSets/* |建立和管理虛擬機器擴展集 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.Network/applicationGateways/backendAddressPools/join/action |加入網路應用程式閘道器後端位址集區 |
| Microsoft.Network/loadBalancers/backendAddressPools/join/action |加入負載平衡器後端位址集區 |
| Microsoft.Network/loadBalancers/inboundNatPools/join/action |加入負載平衡器輸入 NAT 集區 |
| Microsoft.Network/loadBalancers/inboundNatRules/join/action |加入負載平衡器輸入 NAT 規則 |
| Microsoft.Network/loadBalancers/read |讀取負載平衡器 |
| Microsoft.Network/locations/* |建立和管理網路位置 |
| Microsoft.Network/networkInterfaces/* |建立和管理網路介面 |
| Microsoft.Network/networkSecurityGroups/join/action |加入網路安全性群組 |
| Microsoft.Network/networkSecurityGroups/read |讀取網路安全性群組 |
| Microsoft.Network/publicIPAddresses/join/action |加入網路公用 IP 位址 |
| Microsoft.Network/publicIPAddresses/read |讀取網路公用 IP 位址 |
| Microsoft.Network/virtualNetworks/read |讀取虛擬網路 |
| Microsoft.Network/virtualNetworks/subnets/join/action |加入虛擬網路子網路 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Storage/storageAccounts/listKeys/action |列出儲存體帳戶金鑰 |
| Microsoft.Storage/storageAccounts/read |讀取儲存體帳戶 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="classic-network-contributor"></a>傳統網路參與者
可以管理傳統虛擬網路和保留 IP

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.ClassicNetwork/* |建立和管理傳統網路 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |

### <a name="web-plan-contributor"></a>Web 方案參與者
可以管理 Web 方案

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |
| Microsoft.Web/serverFarms/* |建立和管理伺服器陣列 |

### <a name="website-contributor"></a>網站參與者
可以管理網站，但不是 hello web 計劃 toowhich 連線

| **動作** |  |
| --- | --- |
| Microsoft.Authorization/*/read |讀取授權 |
| Microsoft.Insights/alertRules/* |建立和管理 Insights 警示規則 |
| Microsoft.Insights/components/* |建立和管理 Insights 元件 |
| Microsoft.ResourceHealth/availabilityStatuses/read |讀取的 hello 資源健全狀況 |
| Microsoft.Resources/deployments/* |建立和管理資源群組部署 |
| Microsoft.Resources/subscriptions/resourceGroups/read |讀取資源群組 |
| Microsoft.Support/* |建立和管理支援票證 |
| Microsoft.Web/certificates/* |建立和管理網站憑證 |
| Microsoft.Web/listSitesAssignedToHostName/read |讀取網站指派 tooa 主機名稱 |
| Microsoft.Web/serverFarms/join/action |加入伺服器陣列 |
| Microsoft.Web/serverFarms/read |讀取伺服器陣列 |
| Microsoft.Web/sites/* |建立和管理網站 （網站架設也需要寫入權限 toohello 相關聯應用程式服務方案） |

## <a name="see-also"></a>另請參閱
* [角色型存取控制](role-based-access-control-configure.md)： 開始使用 RBAC hello Azure 入口網站中。
* [在 Azure rbac 進行的自訂角色](role-based-access-control-custom-roles.md)： 了解 toocreate 自訂角色 toofit 您存取需要的方式。
* [建立存取權變更歷程記錄報告](role-based-access-control-access-change-history-report.md)︰追蹤 RBAC 中的角色指派變更。
* [角色型存取控制疑難排解](role-based-access-control-troubleshooting.md)︰取得修正常見問題的建議。
