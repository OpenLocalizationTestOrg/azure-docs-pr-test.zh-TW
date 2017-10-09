---
title: "Azure 資料流分析 Tools for Visual Studio aaaUse |Microsoft 文件"
description: "Hello Azure 資料流分析 Tools for Visual Studio 使用者入門教學課程"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>使用適用於 Visual Studio 的 Azure 串流分析工具
## <a name="introduction"></a>簡介
在本教學課程中，您將學習如何 toouse Azure 資料流分析 Tools for Visual Studio toocreate 撰寫、 在本機測試，和偵錯資料流分析工作。 

完成本教學課程之後，您將能夠：
* 熟悉適用於 Visual Studio 的串流分析工具。
* 設定及部署串流分析工作。
* 使用本機範例資料於本機測試作業。
* 使用監視 tootroubleshoot 問題。
* 將現有的工作 tooprojects 的匯出。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要下列必要條件 hello:
* 在 hello 完成前面的 「 建立資料流分析工作 」 的 hello 步驟[使用 Stream Analytics 教學課程建置的 IoT 解決方案](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics)。 
* 使用 Visual Studio 2015、Visual Studio 2013 Update 4 或 Visual Studio 2012。 支援 Enterprise (Ultimate/Premium)、Professional 和 Community 版本。 不支援 Express 版本。 不支援 Visual Studio 2017。 
* 使用 hello Azure SDK for.NET 版本 2.7.1 或更新版本。 安裝使用 hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx)。
* 安裝 hello[資料流分析 Tools for Visual Studio](http://aka.ms/asatoolsvs)。

## <a name="create-a-stream-analytics-project"></a>建立串流分析專案
1. 在 Visual Studio 中，按一下 hello**檔案**功能表，然後選取**新專案**。 

2. 在左側 hello hello 範本清單中選取**Stream Analytics** ，然後按一下 **Azure 資料流分析應用程式**。

3. 輸入 hello 專案**名稱**，**位置**，和**方案名稱**的其他專案一樣。

    ![[新增專案] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    [方案總管] 中會產生 **Toll** 專案。

    ![[方案總管] 中產生的 Toll 專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>選擇 hello 正確的訂用帳戶
1. 在 Visual Studio 中，按一下 hello**檢視**功能表，並開啟**伺服器總管**。

2. 使用 Azure 帳戶進行登入。 

## <a name="define-hello-input-sources"></a>定義 hello 輸入的來源
1.  在**方案總管] 中**，依序展開 [hello**輸入**節點，然後重新命名**Input.json**太**EntryStream.json**。 按兩下 **EntryStream.json**。
2.  hello**輸入別名**現在**EntryStream**。 hello 輸入別名是 hello 查詢指令碼中使用。 
3.  在 [來源類型] 中，選取 [資料流]。
4.  在 [來源] 中，選取 [事件中樞]。
5.  在**服務匯流排命名空間**，選取 hello **TollData**選項。
6.  在 [事件中樞名稱] 中，選取 [entry]。
7.  在**事件中樞原則名稱**，選取**RootManageSharedAccessKey** (hello 預設值)。
8.  在 [事件序列化格式] 中，選取 [Json]。 
9.  在 [編碼] 中，選取 [UTF8]。 您的設定應該看起來像下列螢幕擷取畫面的 hello:

    ![[輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. toofinish hello 精靈] 中，按一下 [**儲存**。 現在您可以加入另一個輸入的來源 toocreate hello 結束資料流。 以滑鼠右鍵按一下 hello**輸入**節點，然後選取**新項目**。

    ![新增項目](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. 在 hello 視窗中，選取  **Azure 資料流分析輸入**，並變更 hello**名稱**太**ExitStream.json**。 按一下 [新增] 。

    ![[加入新項目] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. 按兩下**ExitStream.json** hello 專案和後續 hello 相同步驟的 hello 項目資料流中。 要確定 tooenter**結束**hello**事件中樞名稱**hello 下列螢幕擷取畫面所示：

    ![ExitStream 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    您現在已定義兩個輸入資料流：

    ![進入和離開的輸入資料流](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    接下來，加入包含汽車註冊資料的 hello blob 檔案的參考資料輸入。

13. 以滑鼠右鍵按一下 hello**輸入**hello 專案，然後再遵循 hello 相同步驟 hello 資料流輸入的節點。 在 [輸入別名] 中，輸入 **Registration**，然後在 [來源類型] 中，選取 [參考資料]。

    ![[註冊] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. 在**儲存體帳戶**，選取 hello **tolldata**選項。 在 [容器] 中，選取 [tolldata]，然後在 [路徑模式] 中，輸入 **registration.json**。 這個檔案名稱會區分大小寫，且應該是小寫。
15. toofinish hello 精靈] 中，按一下 [**儲存**。

現在會定義所有 hello 輸入值。

## <a name="define-hello-output"></a>定義 hello 輸出
1.  在**方案總管] 中**，依序展開 [hello**輸入**節點，然後按兩下**Output.json**。

2.  在 [輸出別名] 中，輸入 **output**。 
3.  在 [接收] 中，選取 [SQL Database]。
4.  在 [資料庫] 中，選取 [TollDataDB]。
5.  在 [使用者名稱] 中，輸入 **tolladmin**。 
6.  在 [密碼] 中，輸入 **123toll!**。
7.  在 [資料表] 中，輸入 **TollDataRefJoin**。
8.  按一下 [儲存] 。

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>建立串流分析查詢
本教學課程中嘗試 tooanswer tootoll 相關資料的數個商務問題。 它也會建構資料流分析查詢，可用於資料流分析 tooprovide 相關解答。
在您開始第一個資料流分析工作之前，讓我們來探索簡單的案例和 hello 查詢語法。

### <a name="introduction-toohello-stream-analytics-query-language"></a>簡介 toohello 串流分析查詢語言
例如，假設您需要輸入收費亭的車輛 toocount hello 數目。 這個範例是連續的資料流的事件，因為您尚未 toodefine 一段時間。 修改 hello 問題 toobe 「 多少車輛輸入收費亭每隔三分鐘？ 」 這通常是資料的方式 toocount 稱為 tooas hello 輪轉計數。

查看 hello 資料流分析查詢，此問題的答案：

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

資料流分析會使用類似 SQL 的查詢語言加入幾個擴充功能 toospecify 時間相關的層面 hello 查詢。

如需詳細資訊，請參閱[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)從 MSDN 的 hello 查詢中使用的建構。

現在您已經撰寫第一個資料流分析查詢，它是時間 tootest 它。 使用位於下列路徑的 hello 中您 TollApp 資料夾中的 hello 範例資料檔：

..\TollApp\TollApp\Data

此資料夾包含下列檔案的 hello:
*   Entry.json
*   Exit.json
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>計算 hello 進入收費亭的車輛數目。
在 hello 專案中，按兩下**Script.asaql** tooopen hello 指令碼在 hello**查詢編輯器**。 複製並貼入 hello 指令碼 hello 前一節中 hello 編輯器。 hello 查詢編輯器支援 IntelliSense、 語法著色和 hello 錯誤標記。

![查詢編輯器](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>在本機測試串流分析查詢

1. 如果沒有語法錯誤，toocompile hello 查詢 toosee hello 專案上按一下滑鼠右鍵，然後選取**建置**。 

2. toovalidate 這項查詢針對取樣資料，您可以使用本機的範例資料。 以滑鼠右鍵按一下 hello 輸入，然後選取**新增本機輸入**。

    ![新增本機輸入](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. 在 hello 快顯視窗中，請從您的本機路徑選取 hello 範例資料。 按一下 [儲存] 。

    ![[新增本機輸入] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    名為**local_EntryStream.json**會自動加入 tooyour 輸入資料夾。

    ![檔案已加入的 tooinputs 資料夾](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. 在 hello**查詢編輯器**，按一下 **在本機執行**。 或者，您可以按 F5 鍵，hello。

    ![在本機執行](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![本機執行輸出](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    在 hello 中按下任何鍵 tooview hello 輸出**ASA 本機執行結果**Visual Studio 中的視窗。 

    ![[ASA 本機執行結果] 視窗](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. 按一下**開啟結果資料夾**toocheck hello 輸出檔案，兩者都採用 CSV 和 JSON 格式。

    ![開啟結果資料夾輸出](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>範例 hello 輸入的資料
您也可以從輸入的來源 tooa 本機檔案的範例輸入的資料。 
1. Hello 輸入的組態檔中，以滑鼠右鍵按一下並選取**範例資料**。 

   ![範例資料](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    目前只能取樣事件中樞或 IoT 中樞。 不支援其他輸入來源。

2. 在 [hello] 快顯視窗中，輸入 hello 用的本機路徑 toosave hello 範例資料。 按一下 [取樣]。

    ![[範例資料] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    您可以看到在 hello hello 進度**輸出**視窗。 

    ![[輸出] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>提交資料流分析查詢 tooAzure
1. 在 hello**查詢編輯器**，按一下 **提交 tooAzure** hello 指令碼編輯器中。

    ![提交 tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. 選取 [建立新的 Azure 串流分析作業]。 輸入 hello**工作名稱**，並選取正確的 hello**訂用帳戶**。 按一下 [提交] 。

    ![[提交作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>啟動作業
現在，建立您的工作時，會自動開啟 hello 工作檢視。 
1. toostart hello 作業中，按一下 hello**綠色箭號** 按鈕。

    ![啟動作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. 選取 hello 預設設定，然後按一下**啟動**。
 
    ![[啟動作業] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    hello 作業**狀態**變更太**執行**，和**輸入事件**和**輸出事件**出現。

    ![作業摘要中的 [執行中] 狀態](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>檢查 Visual Studio 中的 hello 結果
1. 在 Visual Studio 中開啟**伺服器總管**並以滑鼠右鍵按一下 hello **TollDataRefJoin**資料表。
2. 選取**顯示資料表資料**toosee hello 輸出的工作。
   
    ![在伺服器總管中選取 [顯示資料表資料]](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>檢視 hello 工作指標
您可以在 [作業計量] 找到一些基本的作業統計資料。 

![[作業計量] 視窗](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>在伺服器總管 中的清單 hello 工作
在 伺服器總管 中，按一下 串流分析作業，然後按一下重新整理。 hello 作業之下**串流分析工作**。

![伺服器總管中列出的串流分析作業](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>開啟 hello 工作檢視
tooopen hello 工作檢視中，展開作業節點，然後按兩下 hello**工作檢視**節點。

![[作業檢視] 節點](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>匯出工作 tooa 現有專案
有兩種方式，您可以將現有的工作 tooa 專案匯出。

中**伺服器總管**，以滑鼠右鍵按一下 hello 作業節點在 hello**資料流分析工作**節點，然後選取**匯出 tooNew 資料流分析專案**。

![匯出 tooNew 資料流分析的專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

hello 專案中產生**方案總管 中**。

![[方案總管] 中產生的專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
您也可以使用 hello 工作檢視，然後按一下**產生專案**。

![產生專案](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>已知問題與限制
 
- 不支援 Power BI 輸出和 Azure Data Lake Store 輸出。
- 編輯器不支援新增或變更 JavaScript 使用者定義函式。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure 串流分析](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
