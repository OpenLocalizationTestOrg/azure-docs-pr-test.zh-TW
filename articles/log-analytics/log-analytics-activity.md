---
title: "aaaView Azure 活動記錄檔記錄分析 |Microsoft 文件"
description: "您可以在所有 Azure 訂閱使用 hello Azure 活動記錄檔方案 tooanalyze 和搜尋 hello Azure 活動記錄檔。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>檢視 Azure 活動記錄

![Azure 活動記錄符號](./media/log-analytics-activity/activity-log-analytics.png)

hello 活動記錄分析解決方案可協助您分析及搜尋 hello [Azure 活動記錄檔](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)跨所有您 Azure 訂用帳戶。 hello Azure 活動記錄檔是可提供深入了解您的訂用帳戶中的資源上所執行的 hello 作業記錄。 hello 活動記錄檔先前稱為*稽核記錄檔*或*操作記錄檔*因為它會報告訂用帳戶的事件。

使用 hello 活動記錄檔，您可以決定 hello*什麼*，*人員*，和*時*的任何寫入作業 (PUT、 POST、 DELETE) 對您的訂用帳戶中的 hello 資源。 您也可以了解 hello 狀態 hello 作業和其他相關屬性。 hello 活動記錄檔不包括讀取 (GET) 作業或作業，以使用 hello 傳統部署模型的資源。

當您連接您的 Azure 活動記錄檔 tooLog 分析時，您可以：

- 分析 hello 與預先定義檢視的活動記錄檔
- 分析和搜尋多個 Azure 訂用帳戶的活動記錄
- 保留活動記錄超過 90 天<sup>1</sup>
- 使活動記錄與其他 Azure 平台和應用程式資料產生關聯
- 請參閱依狀態彙總的作業活動
- 檢視每個 Azure 服務發生的活動所呈現的趨勢
- 報告所有 Azure 資源的授權變更
- 找出影響資源的中斷或服務健全狀況問題
- 使用記錄搜尋 toocorrelate 使用者活動、 自動調整規模作業、 授權變更和服務健全狀況 tooother 記錄檔或從您的環境的度量

<sup>1</sup>根據預設，記錄分析會保留您 Azure 活動記錄檔之 90 天，即使您是在 hello 免費層。 或者，如果您有少於 90 天的工作區中保留期設定。 如果您的工作區中有超過 90 天的保留，hello 活動記錄檔會保留工作區的 hello 保留週期。

記錄分析會收集免費提供的活動記錄檔，並儲存 90 天的免費的 hello 記錄檔。 如果您儲存的時間超過 90 天的記錄檔，就會發生資料保留 hello 資料儲存時間超過 90 天的費用。

當您在免費定價層的 hello 時，活動記錄檔不會套用 tooyour 每日的資料使用。

## <a name="connected-sources"></a>連接的來源

不同於大部分其他 Log Analytics 解決方案，代理程式不會收集活動記錄的資料。 Hello 方案所使用的所有資料都是直接來自 Azure。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 否 | hello 方案不會從 Windows 代理程式收集的資訊。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 | hello 解決方案不會收集從 Linux 代理程式的資訊。 |
| [SCOM 管理群組](log-analytics-om-agents.md) | 否 | hello 方案不會從已連線的 SCOM 管理群組中的代理程式收集的資訊。 |
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | hello 方案並不會收集自 Azure 儲存體資訊。 |

## <a name="prerequisites"></a>必要條件

- tooaccess Azure 活動記錄檔資訊，您必須具有 Azure 訂用帳戶。

## <a name="configuration"></a>組態

執行下列步驟 tooconfigure hello 您工作區的活動記錄分析解決方案的 hello。

1. 啟用從 hello hello 活動記錄分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 設定活動記錄檔 toogo tooyour 記錄分析工作區。
    1. 在 hello Azure 入口網站，選取您的工作區，然後按一下**Azure 活動記錄檔**。
    2. 每個訂用帳戶中，按一下 hello 訂用帳戶名稱。  
        ![新增訂用帳戶](./media/log-analytics-activity/add-subscription.png)
    3. 在 hello*訂用帳戶名稱*刀鋒視窗中，按一下 **連接**。  
        ![connect subscription](./media/log-analytics-activity/subscription-connect.png)

如果您新增使用 hello OMS 入口網站的 hello 解決方案，您會看到 hello 下列磚。 登入 Azure 入口網站 tooconnect toohello 的 Azure 訂用帳戶 tooyour 工作區。  
![執行評估](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>使用 hello 解決方案

當您新增 hello 活動記錄分析解決方案 tooyour 工作區時，hello **Azure 活動記錄檔**tooyour 概觀儀表板的磚加入。 此磚會顯示 hello Azure 活動記錄的數目的計數的 hello hello 方案中有 Azure 訂用帳戶的存取。

![Azure 活動記錄圖格](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>檢視 Azure 活動記錄

按一下 hello **Azure 活動記錄檔**磚 tooopen hello **Azure 活動記錄檔**儀表板。 hello 儀表板會納入 hello 下表中的 hello 刀鋒視窗。 每個刀鋒視窗會列出 too10 hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。 您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello 的 hello 刀鋒視窗，或按一下 hello 刀鋒視窗中的標頭。

活動記錄資料，才會出現*之後*您設定活動記錄檔 toogo toohello 方案，所以您無法檢視資料之前。

| 刀鋒視窗 | 說明 |
| --- | --- |
| Azure 活動記錄項目 | 顯示的橫條圖的 hello 頂端 Azure 活動記錄檔項目記錄您選取的 hello 日期範圍內的總計，並顯示一份 hello 前 10 個活動呼叫端。 按一下橫條圖 toorun hello 的記錄搜尋<code>Type=AzureActivity</code>。 按一下 呼叫端的項目 toorun 記錄搜尋，傳回所有活動記錄項目，該項目。 |
| 依狀態列出的活動記錄 | 顯示您所選取的 hello 日期範圍內的 Azure 活動記錄狀態的環圈圖。 也會顯示清單 hello 前十個狀態記錄的清單。 按一下 記錄搜尋 hello 圖表 toorun <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>。 按一下狀態項目 toorun 記錄搜尋，傳回該狀態記錄的所有活動記錄檔項目。 |
| 依資源列出的活動記錄 | 顯示 hello 總數的活動記錄檔的資源，並列出 hello 前十個資源記錄會計算每個資源。 按一下 記錄搜尋 hello 總面積 toorun <code>Type=AzureActivity &#124; measure count() by Resource</code>，其中顯示所有的 Azure 資源可用 toohello 解決方案。 按一下 資源 toorun 傳回該資源的所有活動記錄的記錄搜尋。 |
| 依資源提供者列出的活動記錄 | 顯示 hello 總數產生活動的資源提供者記錄檔，並列出 hello 的前十個。 按一下 記錄搜尋 hello 總面積 toorun <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>，其中顯示所有的 Azure 資源提供者。 按一下 [資源提供者 toorun 傳回 hello 提供者的所有活動記錄的記錄搜尋]。 |

![Azure 活動記錄儀表板](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>後續步驟

- 特定活動時建立[警示](log-analytics-alerts-creating.md)。
- 使用[記錄搜尋](log-analytics-log-searches.md)tooview 的詳細資訊，從您的活動記錄檔。
