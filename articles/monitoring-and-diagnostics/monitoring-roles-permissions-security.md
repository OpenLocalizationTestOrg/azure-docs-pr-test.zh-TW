---
title: "角色、 權限和安全性的 Azure 監視入門 aaaGet |Microsoft 文件"
description: "了解 toouse Azure 監視的內建的角色和權限 toorestrict 存取 toomonitoring 資源的方式。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>開始使用 Azure 監視器的角色、權限和安全性
許多小組需要 toostrictly 規範存取 toomonitoring 資料和設定。 例如，如果您有只在監視 （技術支援工程師，devops 工程師） 上之小組成員，或如果您使用受管理的服務提供者，您可能會想 toogrant 這些使用者存取監視資料，同時限制他們能夠 toocreate tooonly，修改，或刪除資源。 本文示範如何 tooquickly 套用內建監視 RBAC 角色 tooa 使用者在 Azure 中的或建立您自己自訂的角色需要有限的監視權限的使用者。 接著討論您的 Azure 監視相關資源的安全性考量，而且包含您可以限制存取 toohello 資料的方式。

## <a name="built-in-monitoring-roles"></a>內建的監視角色
Azure 監視的內建角色設計的 toohelp 限制存取 tooresources，同時仍可讓這些訂用帳戶中負責監視基礎結構 tooobtain 並設定所需的 hello 資料。 Azure 監視器提供兩個現成的角色︰監視讀取器和監視參與者。

### <a name="monitoring-reader"></a>監視讀取器
指派 hello 監視讀取者角色的人員可以將檢視訂用帳戶中的所有監視的資料，但無法修改任何資源或編輯任何設定的相關的 toomonitoring 資源。 這個角色是適用於組織，例如支援或作業工程師，需要能夠 toobe 中的使用者：

* Hello 入口網站中檢視監視儀表板，並建立其自己私用的監視儀表板。
* 查詢度量使用 hello [Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn931930.aspx)， [PowerShell cmdlet](insights-powershell-samples.md)，或[跨平台 CLI](insights-cli-samples.md)。
* 查詢 hello 使用 hello 入口網站、 Azure 監視 REST API、 PowerShell 指令程式或跨平台 CLI 活動記錄檔。
* 檢視 hello[診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)資源。
* 檢視 hello[記錄設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)訂用帳戶。
* 檢視自動調整設定。
* 檢視警示活動和設定。
* 存取 Application Insights 資料，並檢視 AI 分析中的資料。
* 搜尋包括 hello 工作區的使用量資料記錄分析 (OMS) 工作區的資料。
* 檢視 Log Analytics (OMS) 管理群組。
* 擷取 hello 記錄分析 (OMS) 的搜尋結構描述。
* 列出 Log Analytics (OMS) 智慧套件。
* 擷取並執行 Log Analytics (OMS) 已儲存的搜尋。
* 擷取 hello 記錄分析 (OMS) 存放裝置設定。

> [!NOTE]
> 此角色沒有提供經過資料流處理的 tooan 事件中心或儲存在儲存體帳戶的讀取權限 toolog 資料。 [請參閱下文](#security-considerations-for-monitoring-data)如需設定存取 toothese 資源資訊。
> 
> 

### <a name="monitoring-contributor"></a>監視參與者
指定人員 hello 監視參與者角色可以在訂用帳戶中檢視監視的所有資料並建立或修改的監視設定，但無法修改任何其他資源。 這個角色是 hello 監視讀取器角色中的超集，而且是適當的成員組織監視小組或受管理的服務提供者，此外 toohello 權限以上版本，也需要 toobe 能夠：

* 將監視儀表板發佈為共用儀表板。
* 設定用於資源的[診斷設定](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings)。*
* 設定 hello[記錄設定檔](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile)subscription.* 的
* 設定警示活動和設定。
* 建立 Application Insights web 測試和元件。
* 列出 Log Analytics (OMS) 工作區共用金鑰。
* 啟用或停用 Log Analytics (OMS) 智慧套件。
* 建立及刪除及執行 Log Analytics (OMS) 已儲存的搜尋。
* 建立及刪除 hello 記錄分析 (OMS) 存放裝置設定。

* 使用者必須另外也有權 Listkey hello 目標資源 （儲存體帳戶或事件中樞命名空間） tooset 記錄檔的設定檔或診斷設定。

> [!NOTE]
> 此角色沒有提供經過資料流處理的 tooan 事件中心或儲存在儲存體帳戶的讀取權限 toolog 資料。 [請參閱下文](#security-considerations-for-monitoring-data)如需設定存取 toothese 資源資訊。
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>監視權限和自訂的 RBAC 角色
如果 hello 上方內建的角色不符合您的小組的 hello 確切需求，您可以[建立自訂的 RBAC 角色](../active-directory/role-based-access-control-custom-roles.md)具有更細微的權限。 以下是一般的 Azure 監視 RBAC 作業，其描述 hello。

| 作業 | 說明 |
| --- | --- |
| Microsoft.Insights/AlertRules/[讀取、寫入、刪除] |讀取/寫入/刪除警示規則。 |
| Microsoft.Insights/AlertRules/Incidents/Read |列出警示規則事件 （hello 觸發的警示規則的記錄）。 這只適用於 toohello 入口網站。 |
| Microsoft.Insights/AutoscaleSettings/[讀取、寫入、刪除] |讀取/寫入/刪除自動調整設定。 |
| Microsoft.Insights/DiagnosticSettings/[讀取、寫入、刪除] |讀取/寫入/刪除診斷設定。 |
| Microsoft.Insights/eventtypes/digestevents/Read |此權限是必要的使用者需要存取 tooActivity 透過 hello 入口網站的記錄檔。 |
| Microsoft.Insights/eventtypes/values/Read |列出訂用帳戶中的活動記錄檔事件 (管理事件)。 此權限是適用的 tooboth 程式設計和入口網站存取 toohello 活動記錄檔。 |
| Microsoft.Insights/LogDefinitions/Read |此權限是必要的使用者需要存取 tooActivity 透過 hello 入口網站的記錄檔。 |
| Microsoft.Insights/MetricDefinitions/Read |讀取度量定義 (可用資源的度量類型清單)。 |
| Microsoft.Insights/Metrics/Read |讀取資源的度量。 |

> [!NOTE]
> 存取 tooalerts、 診斷的設定和度量的資源需要該 hello 使用者具有讀取權限 toohello 資源類型和該資源的範圍。 診斷的設定或記錄檔的設定檔，封存 tooa 儲存體帳戶或資料流 tooevent 中心需要 hello 使用者 tooalso hello 目標資源具有 Listkey 權限建立 （「 寫入 」）。
> 
> 

比方說，透過使用資料表上方的 hello 您可以為 「 活動記錄讀取器 」 就像這樣建立自訂的 RBAC 角色：

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>監視資料的安全性考量
監視資料 (尤其是記錄檔)，可以包含機密資訊，例如 IP 位址或使用者名稱。 來自 Azure 的監視資料有三種基本形式︰

1. hello 活動記錄檔，其中描述 Azure 訂用帳戶的控制平面的所有動作。
2. 診斷記錄檔，是由資源發出的記錄檔。
3. 度量，是由資源發出。

這三種資料型別可以儲存在儲存體帳戶，或資料流處理 tooEvent 集線器，兩者都是一般用途的 Azure 資源。 由於這些是一般用途的資源，因此對其進行建立、刪除及存取通常是保留給系統管理員的特殊權限作業。 我們建議您使用下列做法監視相關資源的 tooprevent 誤用 hello:

* 針對監視資料使用單一、專用的儲存體帳戶。 如果您需要 tooseparate 監視資料到多個儲存體帳戶時，絕對不會共用儲存體帳戶之間監視的使用方式和非監視資料，因為這樣可能會不小心讓只需要存取 （例如 toomonitoring 資料的使用者 第三方 SIEM) 存取 toonon 監視資料。
* 理由與上面相同的 hello 跨所有診斷設定使用單一的專用或 服務匯流排事件中樞命名空間。
* 由將其保存在個別的資源群組中，會限制存取 toomonitoring 相關的儲存體帳戶或事件中心和[使用範圍](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure)您監視角色 toolimit 存取 tooonly 資源群組。
* 當使用者只需要存取 toomonitoring 資料永遠不會授與 hello Listkey 權限的儲存體帳戶或事件中心在訂用帳戶範圍。 相反地，授與這些權限 toohello 使用者在資源或資源群組 （如果您有專用的監視資源群組） 範圍。

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>限制存取 toomonitoring 相關的儲存體帳戶
當使用者或應用程式需要存取 toomonitoring 資料儲存體帳戶中的時，您應該[產生帳戶 SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx) hello 包含具有唯讀存取的服務層級 tooblob 存放裝置的監視資料的儲存體帳戶上。 在 PowerShell 中，它看起來應該如下所示：

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

然後，您可以將需要從該儲存體帳戶，tooread hello 語彙基元 toohello 實體，其可以清單，並從該儲存體帳戶中的所有 blob 讀取。

或者，如果您需要 toocontrol RBAC 具有此權限，您可以授與該實體 hello Microsoft.Storage/storageAccounts/listkeys/action 該特定的儲存體帳戶的權限。 這是必要的使用者需要 toobe 無法 tooset 診斷設定或記錄檔的設定檔 tooarchive tooa 儲存體帳戶。 例如，您可以建立遵循自訂的 RBAC 角色的使用者或應用程式只需要從一個儲存體帳戶的 tooread hello:

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> hello Listkey 權限可讓 hello 使用者 toolist hello 主要和次要儲存體帳戶金鑰。 這些金鑰授與 hello 使用者所有已簽署的權限 （讀取、 寫入、 建立 blob、 刪除 blob 等等） 在所有已簽署該儲存體帳戶中的服務 （blob、 佇列、 表格及檔案）。 我們建議盡可能使用上述的帳戶 SAS。
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>限制存取 toomonitoring 相關的事件中心
使用事件中心可依照類似的模式，但首先您需要 toocreate 專用的接聽授權規則。 如果您想 toogrant 存取 tooan 應用程式只需要 toolisten toomonitoring 相關的事件中樞時，請勿 hello 遵循：

1. 為資料流只接聽宣告的監視資料所建立的 hello 事件中樞上建立共用的存取原則。 這可以在 hello 入口網站中完成。 例如，您可能會將它稱為 “monitoringReadOnly”。 可能的話，您會想 toogive 金鑰直接 toohello 取用者，並略過 hello 下一個步驟。
2. 如果 hello 取用者需要 toobe 無法 tooget hello 金鑰特定，授與該事件中心 hello 使用者 hello Listkey 動作。 這也是必要的使用者需要 toobe 無法 tooset 診斷設定，或記錄設定檔 toostream tooevent 集線器。 例如，您可能會建立 RBAC 規則︰
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>後續步驟
* [深入了解 RBAC 和 Resource Manager 中的權限](../active-directory/role-based-access-control-what-is.md)
* [讀取的監視在 Azure 中的 hello 概觀](monitoring-overview.md)

