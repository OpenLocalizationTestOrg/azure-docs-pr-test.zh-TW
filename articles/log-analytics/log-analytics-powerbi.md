---
title: "aaaExport 記錄分析資料 tooPower BI |Microsoft 文件"
description: "Power BI 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。  記錄分析可以持續將資料匯出 hello OMS 儲存機制到 Power BI，您可以利用其視覺效果與分析工具。  本文說明如何 tooconfigure 查詢中的自動匯出 tooPower BI 定期記錄分析。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>匯出記錄分析資料 tooPower BI

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則匯出記錄分析資料 tooPower BI 此程序將無法再運作。  您在升級之前建立的任何現有排程將會變成停用。 
>
> 升級之後，Azure 記錄分析會使用 hello Application Insights 為相同的平台，而且您使用相同的處理序 tooexport 記錄分析查詢 tooPower 為 BI hello [hello 程序 tooexport Application Insights 查詢 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)。  您可以將匯出 hello 查詢使用 hello 分析主控台，如下所示該發行項，或者您可以選取 hello **Power BI** hello 畫面頂端的 hello hello 記錄搜尋入口網站中的按鈕。



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) 是 Microsoft 的雲端架構商務分析服務，能提供豐富的視覺效果和不同資料集的分析報告。  記錄分析可以自動將資料匯出 hello OMS 儲存機制到 Power BI，您可以利用其視覺效果與分析工具。

當您設定 Power BI 與記錄分析時，您會建立匯出結果 toocorresponding 資料集在 Power BI 中的記錄查詢。  hello 查詢和匯出會繼續 tooautomatically hello 最新記錄分析所收集的資料定義總 toodate tookeep hello 資料集的排程執行。

![記錄分析 tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Power BI 排程
A *Power BI 排程*包含 hello OMS 儲存機制 tooa 對應中的資料集 Power BI 和排程，定義此搜尋會執行目前的 tookeep hello 資料集的頻率從匯出的資料集的記錄搜尋。

hello hello 資料集中的欄位會比對 hello 記錄 hello 記錄搜尋所傳回的 hello 的屬性。  如果 hello 搜尋傳回不同類型的記錄，則 hello 資料集將包含的所有記錄類型包含從每個 hello 的 hello 屬性。  

> [!NOTE]
> 它是最佳的作法 toouse 傳回未經處理資料，但不要 tooperforming 為任何彙總，例如使用命令的記錄搜尋查詢[量值](log-analytics-search-reference.md#measure)。  您可以在 Power BI 中執行任何彙總與計算，從 hello 未經處理資料。
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>連接的 OMS 工作區 tooPower BI
您可以從記錄分析 tooPower BI 匯出之前，您必須連接您的 OMS 工作區 tooyour Power BI 帳戶使用下列程序的 hello。  

1. 在 hello OMS 主控台中，按一下 hello**設定**磚。
2. 選取 [帳戶] 。
3. 在 hello**工作區資訊**區段中，按一下**連接 tooPower BI 帳戶**。
4. 輸入您的 Power BI 帳戶 hello 認證。

## <a name="create-a-power-bi-schedule"></a>建立 Power BI 排程
建立 Power BI 排程每個資料集使用下列程序的 hello。

1. 在 hello OMS 主控台中，按一下 hello**記錄搜尋**磚。
2. 在新的查詢中輸入或選取已儲存的搜尋傳回 hello 太想 tooexport 資料**Power BI**。  
3. 按一下 hello **Power BI**按鈕上方的 hello 頁面 tooopen hello hello **Power BI**對話方塊。
4. 提供在下列資料表，並按一下的 hello hello 資訊**儲存**。

| 屬性 | 說明 |
|:--- |:--- |
| 名稱 |名稱 tooidentify hello 排定的時間檢視的 Power BI 排程 hello 清單。 |
| 已儲存的搜尋 |hello 記錄搜尋 toorun。  您可以選取 hello 目前的查詢，或從 hello 下拉式清單方塊中選取現有的儲存的搜尋。 |
| 排程 |頻率 toorun hello 儲存搜尋及匯出 toohello Power BI 資料集。  hello 值必須是 15 分鐘到 24 小時之間。 |
| 資料集名稱 |hello hello Power BI 中的資料集名稱。  如果不存在便會建立，如果存在則會更新。 |

## <a name="viewing-and-removing-power-bi-schedules"></a>檢視和移除 Power BI 排程
檢視現有的 Power BI 排程，以下列程序的 hello 的 hello 清單。

1. 在 hello OMS 主控台中，按一下 hello**設定**磚。
2. 選取 [Power BI] 。

此外 toohello 詳細資料的 hello 排程、 過去一週執行 hello 的次數 hello 排程在 hello 和 hello hello 上次同步處理狀態會顯示。  如果 hello 同步處理遇到錯誤，您可以按一下 hello 連結 toorun hello 錯誤的詳細資料與記錄的記錄搜尋。

您可以在 hello 上的 移除排程**X**在 hello**移除資料行**。  您可以選取 [關閉] 來停用排程。  toomodify 排程必須移除並重新建立它的 hello 新設定。

![Power BI 排程](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>範例逐步解說
hello 下一節逐步解說範例建立 Power BI 排程，並使用其資料集 toocreate 一份簡單報表。  在此範例中，一組電腦的所有效能資料都是匯出的 tooPower BI，而線條圖則都會建立 toodisplay 處理器使用率。

### <a name="create-log-search"></a>建立記錄搜尋
我們先建立 hello 資料，我們要 toosend toohello 資料集的記錄搜尋。  在此範例中，我們將使用一個查詢，傳回名稱開頭為 *srv*之電腦的所有效能資料。  

![Power BI 排程](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>建立 Power BI 搜尋
我們按一下 hello **Power BI**按鈕 tooopen hello Power BI 對話方塊，並提供所需的 hello 資訊。  我們想要每小時一次此搜尋 toorun 和建立資料集稱為*Contoso 效能*。  因為我們已經建立 hello 資料，我們想要的 hello 搜尋開啟，我們會保留 hello 預設值是*使用目前的搜尋查詢*如**已儲存搜尋**。

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>驗證 Power BI 搜尋
tooverify 我們正確建立 hello 排程，我們會檢視 Power BI 搜尋下 hello hello 清單**設定**hello OMS 儀表板磚。  我們稍等幾分鐘，並重新整理此檢視，直到它會報告已執行 hello 同步處理。

![Power BI 搜尋](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>驗證 Power BI 中的 hello 資料集
我們會記錄在我們考量[powerbi.microsoft.com](http://powerbi.microsoft.com/)太捲動**資料集**在 hello hello 左窗格的底部。  我們可以看到該 hello *Contoso 效能*指出我們匯出已順利執行所列的資料集。

![Power BI 資料集](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>根據資料集建立報表
我們選取 hello **Contoso 效能**資料集，然後按一下**結果**在 hello**欄位**屬於這個 dataset 的 hello 右 tooview hello 欄位 窗格。  toocreate 每一部電腦一行圖形顯示處理器使用率，我們會執行下列動作的 hello。

1. 選取 hello 行圖表視覺效果。
2. 拖曳**ObjectName**太**報表層級篩選**並檢查**處理器**。
3. 拖曳**CounterName**太**報表層級篩選**並檢查**%Processor Time**。
4. 拖曳**CounterValue**太**值**。
5. 拖曳**電腦**太**圖例**。
6. 拖曳**TimeGenerated**太**軸**。

我們可以看到該 hello 產生折線圖會顯示 hello 我們的資料集的資料。

![Power BI 折線圖](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>儲存 hello 報表
我們儲存按一下 hello hello 報告儲存在 hello 囉 」 畫面最上方的按鈕，並驗證它現在列在 hello hello 左窗格中的報表區段。

![Power BI 報表](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)toobuild 查詢可匯出 tooPower BI。
* 深入了解[Power BI](http://powerbi.microsoft.com) toobuild 視覺效果是根據記錄分析的匯出。
