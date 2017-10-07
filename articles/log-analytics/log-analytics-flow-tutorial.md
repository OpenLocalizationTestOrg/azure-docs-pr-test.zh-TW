---
title: "使用 Microsoft Flow 的 aaaAutomate Azure Log Analytics 處理"
description: "了解如何使用 Microsoft Flow tooquickly 使用 hello Azure Log Analytics 連接器來自動化重複程序。"
services: log-analytics
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: log-analytics
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: bwren
ms.openlocfilehash: 52026df968682842cc9f8d55f6f9875c5f9c10b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="automate-log-analytics-processes-with-hello-connector-for-microsoft-flow"></a>Microsoft flow 自動化與 hello 連接器的記錄分析程序
[Microsoft Flow](https://ms.flow.microsoft.com)可讓您使用的各種服務數百個動作的 toocreate 自動化工作流程。 從一個動作的輸出可以用作 toocreate 不同的服務之間的整合可讓您輸入 tooanother。  Microsoft flow hello Azure Log Analytics 連接器可讓您 toobuild 工作流程包含在記錄分析記錄搜尋所擷取的資料。

比方說，您可以從 Office 365 電子郵件通知中使用 Microsoft Flow toouse 記錄分析資料、 在 Visual Studio Team Services 中建立 bug 或張貼 Slack 的訊息。  您可以使用簡易排程或從連接的服務中的某個動作觸發工作流程，例如收到郵件或推文時。  


> [!NOTE]
> Microsoft flow hello Azure Log Analytics 連接器需要您工作區升級 toobe toohello 新記錄分析查詢語言。 您可以深入了解 hello 新語言，並取得 hello 程序 tooupgrade 在工作區[升級您的 Azure 記錄分析工作區 toonew 記錄搜尋](log-analytics-log-search-upgrade.md)。  

本文章中的 hello 教學課程會示範如何 toocreate 流程，會自動傳送 hello 透過電子郵件、 一個範例，告訴您可以使用 Microsoft Flow 的記錄分析的記錄分析記錄搜尋結果。 


## <a name="step-1-create-a-flow"></a>步驟 1：建立流程
1. 登入太[Microsoft Flow](http://flow.microsoft.com)，然後選取**我流動**。
2. 按一下 [+ 從空白建立]。

## <a name="step-2-create-a-trigger-for-your-flow"></a>步驟 2：建立流程的觸發程序
1. 按一下 [Search hundreds of connectors and triggers] \(搜尋數以百計的連接器和觸發程序) 。
2. 型別**排程**hello [搜尋] 方塊中。
3. 依序選取 [排程] 和 [排程 - 重複]。
4. 在 hello**頻率**中，選取**天**在 hello**間隔**方塊中，輸入**1**。<br><br>![Microsoft Flow 觸發程序對話方塊](media/log-analytics-flow-tutorial/flow01.png)


## <a name="step-3-add-a-log-analytics-action"></a>步驟 3：新增 Log Analytics 動作
1. 按一下 + 新增步驟，然後按一下新增動作。
2. 搜尋 **Log Analytics**。
3. 按一下 [Azure Log Analytics – Run query and visualize results] \(Azure Log Analytics – 執行查詢，並將結果視覺化) 。<br><br>![Log Analytics 執行查詢視窗](media/log-analytics-flow-tutorial/flow02.png)

## <a name="step-4-configure-hello-log-analytics-action"></a>步驟 4： 設定 hello 記錄分析動作

1. 指定您包括 hello 訂用帳戶 ID、 資源群組和工作區名稱的工作區的 hello 詳細資料。
2. 新增下列記錄分析查詢 toohello hello**查詢**視窗。  這只是範例查詢，您可以使用任何其他可傳回資料的查詢取代。
```
    Event
    | where EventLevelName == "Error" 
    | where TimeGenerated > ago(1day)
    | summarize count() by Computer
    | sort by Computerindow. 
```

2. 選取**HTML 表格**hello**圖表類型**。<br><br>![Log Analytics 動作](media/log-analytics-flow-tutorial/flow03.png)

## <a name="step-5-configure-hello-flow-toosend-email"></a>步驟 5： 設定 hello 流程 toosend 電子郵件

1. 按一下 新增步驟，然後按一下+ 新增動作。
2. 搜尋 **Office 365 Outlook**。
3. 按一下 [Office 365 Outlook – 傳送電子郵件]。<br><br>![Office 365 Outlook 選取視窗](media/log-analytics-flow-tutorial/flow04.png)

4. 指定在 hello hello 收件者的電子郵件地址**至**視窗，並在 hello 電子郵件的主旨**主旨**。
5. 按一下任何位置中的 hello**主體**方塊。  隨即開啟 [動態內容] 視窗，並具有來自先前動作的值。  
6. 選取 [內文]。  這是 hello hello 記錄分析動作中的 hello 查詢的結果。
6. 按一下 [顯示進階選項]。
7. 在 hello**是 HTML**方塊中，選取**是**。<br><br>![Office 365 電子郵件設定畫面](media/log-analytics-flow-tutorial/flow05.png)

## <a name="step-6-save-and-test-your-flow"></a>步驟 6：儲存並測試流程
1. 在 hello**流程名稱**方塊中，加入您的流程的名稱，然後按一下**建立流程**。<br><br>![儲存流程](media/log-analytics-flow-tutorial/flow06.png)
2. hello 流程現在所建立，而且這是您指定的 hello 排程一天後會執行。 
3. tooimmediately 測試 hello 流程中，按一下 **立即執行**然後**執行流程**。<br><br>![執行流程](media/log-analytics-flow-tutorial/flow07.png)
3. Hello 流程完成時，請檢查 hello hello 收件者所指定的郵件。  您應該會收到郵件本文類似 toohello 下列：<br><br>![範例電子郵件](media/log-analytics-flow-tutorial/flow08.png)


## <a name="next-steps"></a>後續步驟

- 深入了解 [Log Analytics 中的記錄搜尋](log-analytics-log-search-new.md)。
- 深入了解 [Microsoft Flow](https://ms.flow.microsoft.com)。



