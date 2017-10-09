---
title: "aaaStream hello Azure 活動記錄檔 tooEvent 中心 |Microsoft 文件"
description: "了解如何 toostream hello Azure 活動記錄檔 tooEvent 集線器。"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>資料流 hello Azure 活動記錄檔 tooEvent 集線器
hello [ **Azure 活動記錄檔**](monitoring-overview-activity-logs.md)可以附近使用 hello 內建 「 匯出 」 選項在 hello 入口網站的即時 tooany 應用程式資料流中，或藉由啟用 hello hello 透過記錄檔中的服務匯流排規則識別碼Azure PowerShell Cmdlet 或 Azure CLI。

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>您可以使用 hello 活動記錄檔和事件中心執行
以下是幾個方法，您可能會使用 hello 串流 hello 活動記錄檔的功能：

* **資料流 toothird 合作對象記錄與遙測系統**– 一段時間，事件中心資料流將會變成 hello 機制 toopipe 活動記錄，到第三方 Siem 且記錄分析解決方案。
* **建置自訂的遙測及記錄平台**– 如果您已自訂的遙測平台，或都只考慮的建立一個具有高擴充性 hello 發行-訂閱性質的事件中心可讓您 tooflexibly 內嵌 hello活動記錄檔。 [請參閱 Dan Rosanova 指南 toousing 事件中心的全球遙測平台。](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>啟用資料流的 hello 活動記錄檔
您可以啟用以程式設計方式或透過 hello 入口網站的 hello 活動記錄檔資料流。 無論如何，您會選擇服務匯流排命名空間和共用的存取原則，該命名空間，且 hello 第一個新活動記錄檔事件發生時，將會建立該命名空間中的事件中心。 如果您沒有服務匯流排命名空間，您必須先 toocreate 其中一個。 如果您先前串流處理的資料活動記錄檔事件 toothis 服務匯流排命名空間，將會重複使用 hello 先前建立的事件中樞。 hello 共用存取原則是定義 hello hello 串流處理機制具有的權限。 現在，資料流 tooan 事件中心需要**管理**，**傳送**，和**接聽**權限。 您可以建立或修改您的服務匯流排命名空間的 hello hello 「 設定 」 索引標籤底下的傳統入口網站中的服務匯流排命名空間共用存取原則。 tooupdate hello 活動記錄檔記錄的設定檔 tooinclude 串流、 變更 hello hello 使用者必須擁有該服務匯流排的授權規則 hello ListKey 權限。

hello 服務匯流排或事件中樞命名空間中並沒有 toobe hello 發出記錄檔，只要將設定 hello 設定 hello 使用者擁有適當的 RBAC 存取 tooboth 訂閱 hello 訂用帳戶相同訂用帳戶。

### <a name="via-azure-portal"></a>透過 Azure 入口網站
1. 瀏覽 toohello**活動記錄檔**刀鋒視窗上 hello hello 入口網站的左側使用 hello 功能表。
   
    ![瀏覽 tooActivity 記錄在入口網站](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. 按一下 hello**匯出**在 hello hello 刀鋒視窗頂端的按鈕。
   
    ![入口網站中的匯出按鈕](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. 在 hello 刀鋒視窗中出現，您可以選取您想其 toostream 事件和 hello 服務匯流排命名空間中，您想要串流處理這些事件建立事件中樞 toobe hello 區域。
   
    ![匯出活動記錄檔刀鋒視窗](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. 按一下**儲存**toosave 這些設定。 hello 設定會立即會套用的 tooyour 訂用帳戶。

### <a name="via-powershell-cmdlets"></a>透過 PowerShell Cmdlet
如果記錄檔的設定檔已經存在，您必須先 tooremove 該設定檔。

1. 使用`Get-AzureRmLogProfile`tooidentify 如果記錄檔的設定檔
2. 如果是，使用`Remove-AzureRmLogProfile`tooremove 它。
3. 使用`Set-AzureRmLogProfile`toocreate 設定檔：

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

服務匯流排規則識別碼 hello 是這種格式的字串: {服務匯流排資源識別碼} /authorizationrules/ {索引鍵名稱}，例如 

### <a name="via-azure-cli"></a>透過 Azure CLI
如果記錄檔的設定檔已經存在，您必須先 tooremove 該設定檔。

1. 使用`azure insights logprofile list`tooidentify 如果記錄檔的設定檔
2. 如果是，使用`azure insights logprofile delete`tooremove 它。
3. 使用`azure insights logprofile add`toocreate 設定檔：

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

服務匯流排規則識別碼 hello 是這種格式的字串： `{service bus resource ID}/authorizationrules/{key name}`。

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>我要如何使用 hello 記錄資料，從事件中心？
[這裡會提供 hello hello 活動記錄檔的結構描述](monitoring-overview-activity-logs.md)。 每個事件位於名為「記錄」的 JSON blob 陣列中。

## <a name="next-steps"></a>後續步驟
* [封存 hello 活動記錄檔 tooa 儲存體帳戶](monitoring-archive-activity-log.md)
* [讀取 hello hello Azure 活動記錄檔的概觀](monitoring-overview-activity-logs.md)
* [根據活動記錄檔事件設定警示](insights-auditlog-to-webhook-email.md)

