---
title: "在 Azure Stream Analytics aaaPower BI 儀表板 |Microsoft 文件"
description: "使用即時串流 Power BI 儀表板 toogather 商業智慧和分析大量資料從資料流分析工作。"
keywords: "分析儀表板, 即時儀表板"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>串流分析及 Power BI：適用於串流資料的即時分析儀表板
Azure 串流分析可讓您的 hello 開頭商業智慧工具，其中一個 tootake 利用[Microsoft Power BI](https://powerbi.com/)。 在本文中，您將了解如何使用 Power BI 作為 Azure 串流分析作業的輸出，以建立商業智慧工具。 您也學到如何 toocreate 和使用即時儀表板。

本文會繼續從資料流分析 hello[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程。 它建立在該教學課程中的 hello 工作流程為基礎，並新增輸出，讓您可以視覺化資料流分析工作所偵測到的詐騙撥打電話的 Power BI。 

您可以觀看此情節的[影片](https://www.youtube.com/watch?v=SGUpT-a99MA)。


## <a name="prerequisites"></a>必要條件

開始之前，請確定您擁有 hello 下列：

* 一個 Azure 帳戶。
* Power BI 的帳戶。 您可以使用公司帳戶或學校帳戶。
* 完整的版的 hello[即時詐騙偵測](stream-analytics-real-time-fraud-detection.md)教學課程。 hello 教學課程包含產生虛構的電話的中繼資料的應用程式。 在 hello 教學課程中，您可以建立事件中樞，並傳送 hello 串流通話資料 toohello 事件中心。 您撰寫查詢可偵測詐騙的呼叫 （來自相同數字在 hello hello 呼叫相同的時間在不同的位置）。 


## <a name="add-power-bi-output"></a>新增 Power BI 輸出
Hello 即時詐騙偵測教學課程中，在 hello 輸出會傳送 tooAzure Blob 儲存體。 在本節中，您可以將傳送資訊 tooPower BI 輸出。

1. 在 hello Azure 入口網站，開啟您稍早建立的 hello 串流分析工作。 如果您使用 hello 建議的名稱，hello 作業會命名為`sa_frauddetection_job_demo`。

2. 選取 hello**輸出**hello 中間 hello 作業儀表板的方塊，然後選取  **+ 加**。

3. 在 [輸出別名] 中，輸入 `CallStream-PowerBI`。 您可以使用不同的名稱。 如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。 

4. 在 [接收] 下，選取 [Power BI]。

   ![建立 Power BI 的輸出](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. 按一下 [授權]。

    隨即會開啟視窗，讓您提供公司或學校帳戶的 Azure 認證。 

    ![輸入存取 tooPower BI 認證](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. 輸入認證。 請注意，則當您輸入認證時，您正在也賦予的權限 toohello 串流分析工作 tooaccess 您 Power BI 的區域。

7. 當您正在傳回 toohello**新輸出**刀鋒視窗中，輸入下列資訊的 hello:

    * **群組工作區**： 選取您想要 toocreate hello 資料集的 Power BI 租用戶中的工作區。
    * **資料集名稱**：輸入 `sa-dataset`。 您可以使用不同的名稱。 如果這樣做，請記下來供稍後使用。
    * **資料表名稱**：輸入 `fraudulent-calls`。 目前，串流分析作業的 Power BI 輸出在資料集內只能有一個資料表。

    ![PBI 工作區](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > 如果有 Power BI 資料集，而且資料表中具有 hello hello 相同的名稱是您在 hello 資料流分析作業中指定，會覆寫現有的 hello。
    > 我們不建議您在 Power BI 帳戶中明確建立此資料集和資料表。 當您啟動串流分析工作，且 hello 工作開始提取的輸出放入 Power BI 會自動建立。 如果您工作的查詢沒有傳回任何結果，hello 資料集和資料表就不會建立。
    >

8. 按一下 [建立] 。

使用下列設定的 hello 建立 hello 資料集：

* **defaultRetentionPolicy: BasicFIFO**：資料是 FIFO，最大資料列數 20 萬。
* **defaultMode: pushStreaming**: hello 資料集可支援資料流的圖格和傳統的報表視覺效果 （也稱為 (又稱為發送)。

您目前無法建立具有其他旗標的資料集。

如需有關 Power BI 資料集的詳細資訊，請參閱 hello [Power BI REST API](https://msdn.microsoft.com/library/mt203562.aspx)參考。


## <a name="write-hello-query"></a>撰寫 hello 查詢

1. 關閉 hello**輸出**刀鋒視窗，然後傳回 toohello 作業刀鋒視窗。

2. 按一下 hello**查詢**方塊。 

3. 輸入下列查詢的 hello。 此查詢是類似 toohello 自我聯結的查詢在 hello 詐騙偵測教學課程中建立。 hello 差異在於，此查詢會傳送新的結果 toohello 輸出您所建立 (`CallStream-PowerBI`)。 

    >[!NOTE]
    >如果您未命名 hello 輸入`CallStream`在 hello 詐騙偵測教學課程中，以取代您的名稱`CallStream`在 hello **FROM**和**聯結**hello 查詢中的子句。

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. 按一下 [儲存] 。


## <a name="test-hello-query"></a>測試 hello 查詢
此為選擇性區段，但建議執行。 

1. 如果目前沒有執行 hello TelcoStreaming 應用程式，則會開始依照下列步驟：

    * 開啟命令視窗。
    * 移 toohello hello telcogenerator.exe 和修改的 telcodatagen.exe.config 檔案所在的資料夾。
    * 執行下列命令的 hello:

            telcodatagen.exe 1000 .2 2

2. 在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`CallStream`輸入，然後選取 **範例從輸入資料**。

3. 指定您想要取得三分鐘的資料，然後按一下 [確定]。 請等到您收到 hello 資料取樣。

4. 按一下 [測試]，並確定開始產生結果。


## <a name="run-hello-job"></a>執行 hello 工作

1. 請確定該 hello TelcoStreaming 應用程式正在執行。

2. 關閉 hello**查詢**刀鋒視窗。

3. 在 hello 作業刀鋒視窗中，按一下 **啟動**。

    ![啟動 hello 資料流分析工作](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

串流分析工作會開始尋找 hello 內送資料流中的詐騙呼叫。 hello 作業也會建立 hello 資料集和資料表在 Power BI 中，並啟動傳送 hello 詐騙呼叫 toothem 相關資料。


## <a name="create-hello-dashboard-in-power-bi"></a>在 Power BI 中建立 hello 儀表板

1. 跳過[Powerbi.com](https://powerbi.com)並以您的工作或學校帳戶登入。 如果 hello 資料流分析工作查詢結果的輸出，您會看到已建立的資料集：

    ![Power BI 中的串流資料集](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. 在工作區中，按一下 [+&nbsp;建立]。

    ![在 Power BI 工作區中的 hello 建立按鈕](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. 建立新的儀表板並命名為 `Fraudulent Calls`。

    ![在 Power BI 工作區中建立並命名儀表板](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. 在 hello hello 視窗頂端，按一下 **新增磚**，選取**自訂串流資料**，然後按一下**下一步**。

    ![自訂串流資料集](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. 在 [您的資料集] 底下，選取資料集，然後按 [下一步]。

    ![您的串流資料集](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. 在下**視覺效果類型**，選取**卡**，然後在 hello**欄位**清單中，選取**fraudulentcalls**。

    ![新磚的視覺效果詳細資料](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. 按一下 [下一步] 。

8. 填寫磚詳細資料，例如標題和副標題。

    ![新磚的標題和副標題](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. 按一下 [Apply (套用)] 。

    您現在有一個詐騙計數器了！

    ![詐騙計數器](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. 後續 hello 步驟再次 tooadd 磚 （以步驟 4 開始）。 這次不要 hello 遵循：

    * 當您收到太**視覺效果類型**，選取**折線圖**。 
    * 新增軸並選取 [windowend]。 
    * 新增值並選取 [fraudulentcalls]。
    * 如**時間視窗 toodisplay**，選取 hello 過去 10 分鐘。

    ![建立折線圖的磚](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. 按 [下一步]，新增標題和副標題，然後按一下 [套用]。

    hello Power BI 儀表板現在可以讓您有關詐騙呼叫兩個資料檢視偵測到在 hello 串流資料。

    ![完成的 Power BI 儀表板，以兩個磚來顯示詐騙電話](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>深入了解 Power BI

本教學課程示範如何 toocreate 只有幾種不同的資料集的視覺效果。 Power BI 可協助您為組織建立其他客戶商業智慧型工具。 如需詳細資訊，請參閱下列資源的 hello:

* 在 Power BI 儀表板的另一個範例，監看的 hello[開始使用 Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s)視訊。
* 如需有關設定資料流分析工作輸出 tooPower BI，並使用 Power BI 群組，請檢閱 hello [Power BI](stream-analytics-define-outputs.md#power-bi)區段 hello[輸出資料流分析](stream-analytics-define-outputs.md)發行項。 
* 如需 Power BI 一般用法的相關資訊，請參閱 [Power BI 中的儀表板](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)。


## <a name="learn-about-limitations-and-best-practices"></a>了解限制和最佳作法
目前來說，系統大約每秒可呼叫 Power BI 一次。 串流視覺效果支援 15 KB 的封包。 此外，資料流的視覺效果失敗 （但發送繼續 toowork）。 由於這些限制，Power BI 本身最自然 toocases Azure Stream Analytics 並大幅減少資料載入的位置。 我們建議使用輪轉視窗或 Hopping 視窗 tooensure 資料推入已最多每秒一個推入，而且查詢落在 hello 輸送量需求。

您可以使用下列方程式 toocompute hello 值 toogive hello 您的視窗，以秒為單位：

![Equation1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

例如：

* 您有 1 千個以一秒間隔傳送資料的裝置。
* 您正在使用 hello Power BI Pro SKU 支援每小時 1,000,000 個資料列。
* 您想 toopublish hello 數量平均每個裝置 tooPower BI 的資料。

如此一來，hello 方程式會變成：

![Equation2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

指定這個設定，您可以變更原始查詢 toohello 下列 hello:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>更新授權
如果 hello 密碼已變更您的工作已建立或上次經過驗證之後，您需要 tooreauthenticate Power BI 帳戶。 如果您的 Azure Active Directory (Azure AD) 租用戶上設定了 Azure Multi-factor Authentication，您也需要 toorenew 每隔兩週的 Power BI 授權。 如果您未更新，您可以查看徵兆，例如工作輸出缺少或`Authenticate user error`hello 作業記錄檔中。

同樣地，如果 hello 語彙基元過期之後，就會啟動一個工作，就會發生錯誤，並 hello 作業失敗時。 tooresolve 這個問題，請停止正在執行的 hello 工作，並移的 tooyour Power BI 輸出。 tooavoid 資料遺失，選取 hello**更新授權**連結，然後再重新啟動您的工作，從 hello**上次停止時間**。

已使用 Power BI 重新整理 hello 授權之後，綠色的警示會出現在 hello 授權區域 tooreflect hello 問題已解決。

## <a name="get-help"></a>取得說明
如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟
* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [開始使用 Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure 串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
