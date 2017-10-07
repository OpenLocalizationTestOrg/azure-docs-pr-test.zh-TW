---
title: "hello Azure 活動記錄檔的 aaaOverview |Microsoft 文件"
description: "瞭解什麼是 Azure 活動記錄檔的 hello，以及如何使用它 toounderstand 您 Azure 訂用帳戶內發生的事件。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>監視訂閱活動與 hello Azure 活動記錄檔
hello **Azure 活動記錄檔**是提供深入了解發生在 Azure 中的訂用帳戶層級事件的訂閱記錄。 這包括資料，從 Azure 資源管理員服務健全狀況事件的操作資料 tooupdates 的範圍。 hello 活動記錄檔先前稱為 「 稽核記錄檔 」 或 「 操作記錄檔 」，因為 hello 系統管理類別目錄報表訂用帳戶的控制平面事件。 使用 hello 活動記錄檔，您可以決定 hello '功能，對象、 及何時' 的任何寫入作業 (PUT、 POST、 DELETE) 在您的訂用帳戶中的 hello 資源。 您也可以了解 hello 狀態 hello 作業以及其他相關的屬性。 hello 活動記錄檔不包括讀取 (GET) 作業或使用 hello 傳統資源的作業 /"RDFE 」 模型。

![活動記錄與其他類型的記錄 ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

圖 1：活動記錄與其他類型的記錄

hello 活動記錄檔不同於[診斷記錄檔](monitoring-overview-of-diagnostic-logs.md)。 活動記錄檔提供 hello hello 之外 (hello"控制項的平面 」) 中的資源作業的相關資料。 診斷記錄檔所發出的資源，並提供該資源 (hello 」 資料平面 」) 的 hello 作業的相關資訊。

您可以從您使用 hello Azure 入口網站，CLI、 PowerShell 指令程式的活動記錄檔擷取的事件和 Azure 監視 REST API。


> [!WARNING]
> hello Azure 活動記錄檔是主要發生之活動的 Azure 資源管理員中。 它不會追蹤資源使用 hello 傳統/RDFE 模型。 某些傳統資源類型在 Azure Resource Manager 中有 Proxy 資源提供者 (例如，Microsoft.ClassicCompute)。 如果您使用傳統資源類型透過 Azure 資源管理員使用這些 proxy 資源提供者互動時，請 hello 作業就會出現在 hello 活動記錄檔中。 如果您互動傳統資源輸入 hello 傳統入口網站或否則之外 hello Azure 資源管理員的 proxy，您的動作只能記錄 hello 作業記錄檔中。 只有在 hello 傳統入口網站存取 hello 作業記錄檔。
>
>

下列影片介紹 hello 活動記錄檔檢視 hello。
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Hello 活動記錄檔中的類別
hello 活動記錄檔包含數個分類的資料。 如需 hello 結構描述，這些類別目錄的完整細節[請參閱本文章](monitoring-activity-log-schema.md)。 其中包含：
* **系統管理**-這個類別所包含的所有 hello 記錄建立、 更新、 刪除和動作的作業執行透過資源管理員。 Hello 類型的事件，您會看到此類別中包含的範例 「 建立虛擬機器 」 和 「 刪除網路安全性群組 」 每個使用者所採取的動作，或使用資源管理員的應用程式會模型化為特定資源類型上的作業。 如果 hello 作業類型是寫入刪除或動作，hello 記錄 hello 開始和成功或失敗的作業都會記錄在 hello 系統管理類別。 hello 系統管理類別也會包含在訂閱中的任何變更 toorole 型存取控制。
* **服務健全狀況**-這個類別所包含的任何服務健全狀況事件發生在 Azure 中的 hello 記錄。 舉例來說，hello 您將會看到此類別中類型是事件的"SQL Azure，在美國東部發生停機。 」 服務健全狀況事件有五種： 所需的動作、 協助復原、 事件、 維護、 資訊或安全性，和，才會出現您擁有 hello 訂用帳戶會受到 hello 事件中的資源。
* **警示**-這個類別所包含的所有啟用的 Azure 警示 hello 記錄。 Hello 您將會看到此類別中類型的範例是事件的"myVM 上的 CPU 百分比已超過 80 hello 過去 5 分鐘。 」 各種 Azure 系統都有警示概念，您可以定義某種類型的規則，並在條件符合該規則時接收通知。 每次支援 Azure 的警示類型 '啟動，' 或 hello 條件都符合的 toogenerate 通知，hello 啟用的記錄也會推入 toothis 類別目錄的 hello 活動記錄檔。
* **自動調整規模**-這個類別所包含 hello 作業的記錄任何事件相關的 toohello hello 自動調整引擎根據您定義您的訂用帳戶中的任何自動調整規模設定。 Hello 您將會看到此類別中類型的範例是事件的 「 自動調整規模小數位數設定動作失敗。 」 使用自動調整規模，您可以自動向外擴充或調整在 hello 中支援的資源類型的執行個體的數目會根據使用自動調整規模設定的日期和/或負載 （標準） 的資料的時間。 Hello 條件符合時 tooscale 向上或向下、 hello 開始與成功或失敗的事件都會記錄在此類別中。
* **建議** - 此類別包含來自特定資源類型 (如網站和 SQL 伺服器) 的建議事件。 這些事件提供建議 toobetter 如何利用您的資源。 只有擁有會發出建議的資源時，您才會收到此類型的事件。
* **原則、安全性及資源健康情況** - 這些類別不包含任何事件；僅保留以供未來使用。

## <a name="event-schema-per-category"></a>每個類別的事件結構描述
[請參閱此文章 toounderstand hello 活動記錄檔事件結構描述每個類別。](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>您可以執行以 hello 活動記錄檔
以下是一些您可以執行以 hello 活動記錄檔的 hello 事項：

![Azure 活動記錄](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* 查詢和檢視中 hello **Azure 入口網站**。
* [根據活動記錄事件建立警示。](monitoring-activity-log-alerts.md)
* [串流 tooan**事件中心**](monitoring-stream-activity-logs-event-hubs.md)來擷取第三方服務或自訂的分析解決方案，例如 power Bi。
* 分析中使用 hello PowerBI [ **power Bi 內容套件**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)。
* [將它儲存 tooa**儲存體帳戶**封存或手動檢查](monitoring-archive-activity-log.md)。 您可以指定 hello 保留時間 （以天為單位） 使用 hello**記錄檔的設定檔**。
* 透過 PowerShell Cmdlet、CLI 或 REST API 查詢活動記錄。

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>在 hello Azure 入口網站中的查詢 hello 活動記錄檔
Hello Azure 入口網站中您可以檢視活動記錄在幾個地方：
* hello**活動記錄 刀鋒視窗**，您可以藉由搜尋 hello 左側導覽窗格中的 hello 活動記錄檔中 「 更多服務 」 存取。
* hello**監視器刀鋒視窗**，hello 左側導覽窗格中，預設會出現。 hello 活動記錄檔是一個區段的此 Azure 監視器刀鋒視窗。
* 任何資源**資源刀鋒視窗**，例如 hello 組態刀鋒視窗中的虛擬機器。 hello 活動記錄檔是其中一個 hello 章節於大部分的這些資源刀鋒視窗，並在其上按一下 自動篩選 hello 事件 toothose 相關 toothat 特定資源。

在 hello Azure 入口網站，您可以篩選您依這些欄位的活動記錄檔：
* Timespan-hello 開始和結束時間的事件。
* 類別-hello 事件類別目錄 （如上所述）。
* 訂用帳戶 - 一或多個 Azure 訂用帳戶名稱。
* 資源群組 - 這些訂用帳戶中的一或多個資源群組。
* 資源 （名稱）-hello 特定資源的名稱。
* 資源類型資源，例如 Microsoft.Compute/virtualmachines hello 類型。
* 作業名稱的 Azure 資源管理員作業，例如 Microsoft.SQL/servers/Write hello 名稱。
* 嚴重性-hello 事件 (資訊、 警告、 錯誤、 Critical) hello 嚴重性層級。
* 由-hello 'caller，' 或執行 hello 作業的使用者啟動的事件。
* 開啟搜尋 - 這是開啟文字搜尋方塊，可在所有事件的所有欄位中搜尋該字串。

一旦定義了一組篩選之後，您就可以將它儲存為查詢，如果您需要 tooperform，在工作階段之間保存的 hello 同樣的查詢與在未來的 hello 重新套用這些篩選。 您也可以釘選查詢 tooyour Azure 儀表板 tooalways 保持落在特定事件。

按一下 [套用] 執行您的查詢，並顯示所有相符的事件。 按一下顯示 hello 該事件的摘要，以及 hello 該事件的完整原始 JSON hello 清單中的任何事件。

取得更多電源，您可以按一下 hello**記錄搜尋**圖示，顯示活動記錄資料中 hello[記錄分析活動記錄分析解決方案](../log-analytics/log-analytics-activity.md)。 hello 活動記錄 刀鋒視窗會提供基本的篩選條件/瀏覽體驗上記錄檔，但記錄分析可讓您 toopivot 查詢，並將資料視覺化功能更強大的方式。

## <a name="export-hello-activity-log-with-a-log-profile"></a>匯出 hello 活動記錄檔與記錄檔的設定檔
**記錄檔設定檔** 控制活動記錄檔的匯出方式。 使用記錄檔設定檔，您可以設定︰

* （儲存體帳戶或事件中心） 其中傳送嗨活動記錄檔
* 應該要傳送何種事件分類 (Write、Delete、Action)。 *hello 意義的 「 類別目錄 」 中設定記錄檔和活動記錄檔事件會不同。Hello 記錄檔的設定檔，在 「 類別目錄 」 會代表 hello 作業類型 （寫入、 刪除、 動作）。活動記錄檔事件、 hello 「 類別目錄 」 屬性會代表 hello 來源或類型的事件 （例如，管理、 ServiceHealth、 警示及多個）。*
* 應該要匯出哪一個區域 (位置)。 請確定 tooinclude 「 全域 」，因為 hello 活動記錄檔中的許多事件都是全域的事件。
* 多久 hello 活動記錄應保留在儲存體帳戶。
    - 保留期為 0 天表示會永遠保留記錄。 否則，hello 值可以是任意數目的 1 到 2147483647 之間的天數。
    - 如果設定保留原則，但記錄檔儲存體帳戶中已停用儲存 （例如，如果只選取事件中心 或 OMS 選項），hello 保留原則會有任何作用。
    - 保留原則套用的每日，因此在 hello 結束日 (UTC) 的記錄從 hello 天現在超出 hello 保留原則會刪除。 例如，如果您在一天的保留原則，hello 從今天 hello 日開始時 hello hello 天前昨天的記錄檔會刪除。

您可以使用儲存體帳戶，或未出現在事件中樞命名空間 hello 相同訂用帳戶，因為 hello 一個發出記錄檔。 將設定 hello 設定的 hello 使用者必須擁有 hello 適當 RBAC 存取 tooboth 訂用帳戶。

透過在 hello hello 入口網站中的活動記錄 刀鋒視窗的 hello 「 匯出 」 選項，可以設定這些設定。 它們也可以設定以程式設計方式[使用 hello Azure 監視 REST API](https://msdn.microsoft.com/library/azure/dn931927.aspx)，PowerShell cmdlet 或 CLI。 一個訂用帳戶只能有一個記錄檔的設定檔。

### <a name="configure-log-profiles-using-hello-azure-portal"></a>設定記錄檔的設定檔使用 hello Azure 入口網站
您可以串流處理 hello 活動記錄檔 tooan 事件中心，或將其儲存在儲存體帳戶中，利用 hello Azure 入口網站中的 hello 「 匯出 」 選項。

1. 瀏覽 toohello**活動記錄檔**刀鋒視窗上 hello hello 入口網站的左側使用 hello 功能表。

    ![瀏覽 tooActivity 記錄在入口網站](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. 按一下 hello**匯出**在 hello hello 刀鋒視窗頂端的按鈕。

    ![入口網站中的匯出按鈕](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. 在 hello 刀鋒視窗中出現，您可以選取：  
  * 區域，您想要 tooexport 事件
  * hello 儲存體帳戶 toowhich 希望 toosave 事件
  * hello 要 tooretain 這些事件的儲存體中的日數。 如果設定為 0 天會永遠保留 hello 記錄檔。
  * hello 服務匯流排命名空間中，您想要串流處理這些事件建立事件中樞 toobe。

     ![匯出活動記錄檔刀鋒視窗](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. 按一下**儲存**toosave 這些設定。 hello 設定會立即會套用的 tooyour 訂用帳戶。

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>設定記錄檔的設定檔使用 hello Azure PowerShell Cmdlet
#### <a name="get-existing-log-profile"></a>取得現有的記錄檔設定檔
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>新增記錄檔設定檔
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| Name |是 |記錄檔設定檔的名稱。 |
| StorageAccountId |否 |應該儲存 hello 儲存體帳戶 toowhich hello 活動記錄檔的資源識別碼。 |
| serviceBusRuleId |否 |服務匯流排 hello 服務匯流排命名空間，您想要 toohave 事件中樞中建立的規則識別碼。 將會是此格式的字串︰`{service bus resource ID}/authorizationrules/{key name}`。 |
| 位置 |是 |以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。 |
| RetentionInDays |是 |事件應保留的天數，1 到 2147483647 之間。 值為 0 會無限期儲存 hello 記錄檔 （永久）。 |
| 類別 |否 |以逗號分隔的類別清單，其中列出應該收集的事件類別。 可能的值有 Write、Delete、Action。 |

#### <a name="remove-a-log-profile"></a>移除記錄檔設定檔
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>設定記錄檔的設定檔使用 hello Azure 跨平台 CLI
#### <a name="get-existing-log-profile"></a>取得現有的記錄檔設定檔
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
hello`name`屬性應該是 hello 您記錄檔的設定檔名稱。

#### <a name="add-a-log-profile"></a>新增記錄檔設定檔
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| 名稱 |是 |記錄檔設定檔的名稱。 |
| storageId |否 |應該儲存 hello 儲存體帳戶 toowhich hello 活動記錄檔的資源識別碼。 |
| serviceBusRuleId |否 |服務匯流排 hello 服務匯流排命名空間，您想要 toohave 事件中樞中建立的規則識別碼。 將會是此格式的字串︰`{service bus resource ID}/authorizationrules/{key name}`。 |
| 位置 |是 |以逗號分隔清單的區域，您想要 toocollect 活動記錄檔事件。 |
| RetentionInDays |是 |事件應保留的天數，1 到 2147483647 之間。 值為 0 會無限期儲存 hello 記錄檔 （永久）。 |
| 類別 |否 |以逗號分隔的類別清單，其中列出應該收集的事件類別。 可能的值有 Write、Delete、Action。 |

#### <a name="remove-a-log-profile"></a>移除記錄檔設定檔
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>後續步驟
* [深入了解 hello 活動記錄檔 （先前稱為稽核記錄檔）](../azure-resource-manager/resource-group-audit.md)
* [資料流 hello Azure 活動記錄檔 tooEvent 集線器](monitoring-stream-activity-logs-event-hubs.md)
