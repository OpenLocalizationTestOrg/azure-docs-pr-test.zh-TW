---
title: "在 OMS 記錄分析 aaaCreating 警示 |Microsoft 文件"
description: "警示記錄分析中的識別您的 OMS 儲存機制中的重要資訊和可以主動通知您的問題或叫用動作 tooattempt toocorrect 它們。  本文說明如何 toocreate 警示的規則和詳細資料 hello 不同動作才會。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>使用 Log Analytics 中的警示規則
警示會由自動定期執行記錄搜尋的警示規則所建立。  如果 hello 結果符合特定準則，他們就會建立警示的記錄。  hello 規則然後就可以自動執行一個或多個動作 tooproactively 通知您 hello 警示，或叫用另一個處理序。   

本文描述 hello 處理程序 toocreate，並編輯使用 hello OMS 入口網站的警示規則。  如需 hello 不同的設定，以及如何 tooimplement 所需的邏輯的詳細資訊，請參閱[中記錄分析了解警示](log-analytics-alerts.md)。

>[!NOTE]
> 您目前無法建立或修改使用 hello Azure 入口網站警示規則。 

## <a name="create-an-alert-rule"></a>建立警示規則

toocreate 使用 hello OMS 入口網站警示規則，先建立記錄檔搜尋應該叫用 hello 警示的 hello 記錄。  hello**警示**按鈕將可以讓您可以建立並設定 hello 警示規則。

>[!NOTE]
> 目前最多可以在 OMS 工作區中建立 250 個警示規則。 

1. 從 hello OMS 的 概觀 頁面上，按一下 **記錄搜尋**。
2. 建立新的記錄檔搜尋查詢，或選取已儲存的記錄檔搜尋。 
3. 按一下**警示**頂端的 hello 頁面 tooopen hello hello**加入警示規則**螢幕。
4. 設定使用中的資訊 hello 警示規則[警示規則的詳細資料](#details-of-alert-rules)下方。
6. 按一下**儲存**toocomplete hello 警示規則。  該警示規則會立即開始執行。


## <a name="edit-an-alert-rule"></a>編輯警示規則
您可以取得所有的警示規則的清單中 hello**警示**記錄分析中的功能表**設定**。  

![管理警示](./media/log-analytics-alerts/configure.png)

1. 在 hello OMS 主控台選取 hello**設定**磚。
2. 選取 [警示] 。

您可以在此檢視中執行多個動作。

* 選取 [停用規則**關閉**tooit 下一步]。
* 按一下 hello 鉛筆圖示下一步 tooit 編輯警示規則。
* 移除警示規則，依序按一下 hello **X**圖示下一步 tooit。 

## <a name="details-of-alert-rules"></a>警示規則詳細資訊
當您建立或編輯警示規則 hello OMS 入口網站中的時，搭配 hello**加入警示規則**或**編輯警示規則**頁面。  hello 下表描述在此畫面中的 hello 欄位。

![警示規則](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>警示資訊
這些是基本 hello 警示規則，它會建立 hello 警示設定。

| 屬性 | 說明 |
|:--- |:---|
| 名稱 | 唯一名稱 tooidentify hello 的警示規則。 這個名稱會包含在 hello 規則所建立的任何警示。  |
| 說明 | Hello 警示規則的選擇性描述。 |
| 嚴重性 |此規則所建立之任何警示的嚴重性。 |

### <a name="search-query-and-time-window"></a>搜尋查詢和時間範圍
傳回會評估的 toodetermine，如果應建立任何警示的 hello 記錄 hello 搜尋查詢和時間範圍。

| 屬性 | 說明 |
|:--- |:---|
| 搜尋查詢 | 這是將執行的 hello 查詢。  此查詢所傳回的 hello 記錄將會使用的 toodetermine 是否建立警示。<br><br>選取**使用目前的搜尋查詢**toouse hello 目前的查詢，或選取現有的儲存搜尋從 hello 清單。  其中您可以視需要修改它的 hello 文字方塊中提供 hello 查詢語法。 |
| 時間範圍 |指定 hello hello 查詢的時間範圍。  hello 查詢會傳回目前時間的 hello 這個範圍內所建立的記錄。  可以是介於 5 分鐘與 24 小時之間的任何值。  它應該是大於或等於 toohello 警示的頻率。  <br><br> 例如，如果 hello too60 分鐘和 hello 查詢設定 視窗的時間執行在下午 1:15，將傳回 12:15 PM 和 1:15 PM 之間建立的記錄。 |

當您提供 hello 時段 hello 警示規則時，會顯示 hello 數目符合該時間視窗的 hello 搜尋條件的現有記錄。  這可協助您判斷 hello 頻率，以提供您 hello 您預期的結果數目。

### <a name="schedule"></a>排程
定義頻率 hello 搜尋執行查詢。

| 屬性 | 說明 |
|:--- |:---|
| 警示頻率 | 指定頻率 hello 應該執行查詢。 可以是介於 5 分鐘與 24 小時之間的任何值。 應該是等於 tooor 小於 hello 時間間隔。  如果 hello 值大於 hello 的時段，然後可能會遺漏的記錄。<br><br>例如，請考慮 30 分鐘的時間範圍，以及 60 分鐘的頻率。  如果 hello 查詢 1:00 執行，它會傳回 12:30 下午 1:00 之間的記錄。  hello hello 查詢就會執行下一次為 2:00 時，它就會傳回 1:30 到 2:00 之間的記錄。  1:00 和 1:30 之間建立的任何記錄一律不會評估。 |


### <a name="generate-alert-based-on"></a>產生警示的依據
定義的 hello 應該建立將會評估 hello hello 的搜尋查詢 toodetermine 如果警示結果的準則。  這些詳細資料會根據您選取的警示規則的 hello 類型而不同。  您可以取得詳細資料 hello 從不同的警示規則類型[中記錄分析了解警示](log-analytics-alerts.md)。

| 屬性 | 說明 |
|:--- |:---|
| 隱藏警示 | 當您開啟 hello 警示規則隱藏項目時，定義建立新的警示之後的時間長度的 hello 規則的動作會停用。 hello 規則仍在執行，並符合 hello 準則，則會建立警示記錄。 這是 tooallow toocorrect hello 問題的時間而不需執行重複的動作。 |

#### <a name="number-of-results-alert-rules"></a>結果數目警示規則

| 屬性 | 說明 |
|:--- |:---|
| 結果數目 |如果 hello hello 查詢所傳回的記錄數目可能是建立警示**大於**或**小於**hello 您提供的值。  |

#### <a name="metric-measurement-alert-rules"></a>公制度量單位的警示規則

| 屬性 | 說明 |
|:--- |:---|
| 彙總值 | Hello 結果中每個彙總的值必須超過 toobe 臨界值會被視為有入侵。 |
| 觸發警示的依據 | 建立警示 toobe 的漏洞的 hello 數目。  您可以指定**總計漏洞**漏洞 hello 結果之間的任何組合的設定或**連續漏洞**hello 漏洞的 toorequire 必須位於連續取樣。 |

### <a name="actions"></a>動作
永遠會建立警示規則[警示記錄](#alert-records)hello 臨界值到達時。  您也可以定義一個或多個回應 toobe 執行，例如傳送電子郵件或啟動 runbook。



#### <a name="email-actions"></a>電子郵件動作
電子郵件動作會傳送 hello 的 hello 警示 tooone 或多個收件者的詳細資料的電子郵件。

| 屬性 | 說明 |
|:--- |:---|
| 電子郵件通知 |指定**是**如果您想 hello 在警示觸發時傳送電子郵件 toobe。 |
| 主旨 |Hello 電子郵件的主旨。  您無法修改 hello 郵件 hello 主體。 |
| 收件者 |所有電子郵件收件者的地址。  如果您指定一個以上的地址，然後個別 hello 位址以分號 （;）。 |

#### <a name="webhook-actions"></a>Webhook 動作
Webhook 動作可讓您 tooinvoke 外部處理序，透過單一的 HTTP POST 要求。

| 屬性 | 說明 |
|:--- |:---|
| Webhook |指定**是**如果 hello 在警示觸發時，您會想 toocall webhook。 |
| Webhook URL |hello hello webhook URL。 |
| 包含自訂 JSON 承載 |如果您想要使用自訂承載 tooreplace hello 預設內容，請選取此選項。 |
| 輸入您的自訂 JSON 承載 |hello webhook hello 自訂裝載。  如需詳細資料，請參閱上一節。 |

#### <a name="runbook-actions"></a>Runbook 動作
Runbook 動作可在 Azure 自動化中啟動 Runbook。 

>[!NOTE]
> 您必須安裝在您的工作區的 啟用這個動作 toobe hello 自動化解決方案。 


| 屬性 | 說明 |
|:--- |:---|
| Runbook | 指定**是**如果 hello 在警示觸發時，您會想 toostart Azure 自動化 runbook。  |
| 自動化帳戶 | 指定 hello runbook 會從選取的自動化帳戶。  這是已連結 toohello 工作區中的 hello 動作帳戶。 |
| 啟動 Runbook | 選取您在建立警示時要 toostart hello runbook。 |
| 執行位置 | 選取**Azure** toorun hello runbook hello 雲端中的。  選取**Hybrid worker** toorun hello runbook 上的代理程式[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )安裝。  |




## <a name="next-steps"></a>後續步驟
* 安裝 hello[警示管理解決方案](log-analytics-solution-alert-management.md)tooanalyze 警示與警示一起建立記錄分析中收集從 System Center Operations Manager (SCOM)。
* 深入了解可產生警示的 [記錄檔搜尋](log-analytics-log-searches.md) 。
* 完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。  
* 深入了解如何 toowrite [Azure 自動化中的 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 警示所識別的問題。

