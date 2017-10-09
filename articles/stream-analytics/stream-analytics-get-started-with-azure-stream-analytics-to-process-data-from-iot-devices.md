---
title: "aaaIoT 即時資料流和 Azure Stream Analytics |Microsoft 文件"
description: "IoT 感應器標記和具有串流分析的資料串流與即時資料處理"
keywords: "IoT 解決方案，開始使用 IoT"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>開始使用 Azure Stream Analytics tooprocess 資料從 IoT 裝置
在此教學課程中，您將學習如何 toocreate 資料流處理邏輯 toogather 物聯網 (IoT) 裝置的資料。 我們將如何使用真實世界的物聯網 (IoT) 使用案例 toodemonstrate toobuild 方案快速且經濟。

## <a name="prerequisites"></a>必要條件
* [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)
* 範例查詢和資料檔案可從 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>案例
Contoso，這是一家公司 hello 工業自動化空間中的，已完全自動化其製造程序。 在這種植物 hello 機制有能夠發出的即時資料流的感應器。 在此案例中，生產 floor 經理想 toohave hello 感應器資料 toolook 從即時深入資訊的模式，並對其採取動作。 我們將使用在 hello 感應器資料 toofind 有趣模式上的資料流分析查詢語言 (SAQL) hello 從 hello 內送資料流的資料。

這裡的資料是從 Texas Instrument 的感應器標籤裝置產生。

![Texas Instruments 的感應器標籤](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

hello 裝載的 hello 資料的 JSON 格式，而且看起來像下列 hello:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

在真實世界的案例中，您可以擁有數百個此類感應器，產生事件作為串流。 在理想情況下，閘道裝置會執行程式碼 toopush 這些事件太[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)或[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)。 串流分析工作會擷取這些事件，從事件中樞，並針對 hello 資料流執行即時分析查詢。 然後，您可以傳送的 hello hello 結果 tooone[支援輸出](stream-analytics-define-outputs.md)。

為了方便使用，本入門指南會提供擷取自實際感應器標籤裝置的範例資料檔。 您可以在 hello 範例資料上執行查詢，並查看結果。 在後續的教學課程，您將學習如何 tooconnect 您作業 tooinputs 和輸出，並將其部署 toohello Azure 服務。

## <a name="create-a-stream-analytics-job"></a>建立串流分析工作
1. 在 hello [Azure 入口網站](http://portal.azure.com)，按一下加號 hello，然後輸入**STREAM ANALYTICS** hello 文字視窗 toohello 右中。 然後選取**資料流分析工作**hello [結果] 清單中。
   
    ![建立新的串流分析作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. 輸入唯一的作業名稱，並確認 hello 訂用帳戶是 hello 正確的另一個用於您的工作。 然後建立新的資源群組，或在您的訂用帳戶上選取現有的資源群組。
3. 然後選取作業的位置。 處理速度和降低成本選取 hello 的資料傳輸的建議與 hello 資源群組和預期的儲存體帳戶相同的位置。
   
    ![建立新的串流分析作業詳細資料](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > 每個區域只應該建立一次此儲存體帳戶。 此儲存體會供該區域中建立的所有串流分析作業共用。
   > 
   > 
4. 檢查 hello 方塊 tooplace 您儀表板上的工作，然後按一下**建立**。
   
    ![正在建立作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. 您應該會看到 '部署已開始...' hello 右上方瀏覽器視窗的顯示。 很快就將會變更已完成的 tooa 視窗，如下所示。
   
    ![正在建立作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>建立 Azure 串流分析查詢
您的工作之後建立的時間 tooopen 它與建置查詢。 您可以按一下 hello 磚輕鬆存取您的工作。

![作業圖格](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

在 [hello**作業拓撲**] 窗格中按一下 hello**查詢**方塊 toogo toohello 查詢編輯器。 hello**查詢**編輯器可讓您透過 hello 內送事件資料執行 hello 轉換的 tooenter T-SQL 查詢。

![查詢方塊](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>查詢：封存未經處理資料
hello 查詢最簡單形式是封存指定輸出的所有輸入的資料 tooits 之傳遞查詢。 下載 hello 範例資料檔從[GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa 您電腦上的位置。 

1. 貼上從 hello PassThrough.txt 檔案 hello 查詢。 
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. 按一下 hello 三個點下一步 tooyour 輸入，然後選取**從檔案的範例資料上傳**方塊。
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. 窗格會在 hello 開啟右如此一來，它選取 hello HelloWorldASA InputStream.json 資料檔從您的下載位置，並按一下**確定**在 hello hello 窗格的底部。
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. 然後按一下 [hello**測試**齒輪 hello 左上角區域中的 hello] 視窗中，然後處理 hello 範例資料集對測試查詢。 Hello 處理完成時，會開啟下您的查詢結果 視窗。
   
    ![測試結果](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>篩選 hello 資料為基礎的查詢：
我們來試試 toofilter hello 結果根據條件。 我們希望 tooshow 結果事件來自 「 sensorA。 」 hello 查詢是 hello Filtering.txt 檔案中。

![篩選資料串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

請注意，hello 區分大小寫的查詢比較的字串值。 按一下 hello**測試**齒輪再次 tooexecute hello 查詢。 hello 查詢必須傳回 389 從 1860年事件的資料列。

![查詢測試的第二個輸出結果](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>查詢： 警示 tootrigger 商務工作流程
讓我們的查詢變得更為詳細。 每種感應器的類型，我們會想 toomonitor 平均溫度每 30 秒的時間，高於 100 度的 hello 平均溫度時，才會顯示結果。 我們會撰寫 hello 下列查詢，然後按一下**測試**toosee hello 結果。 hello 查詢是 hello ThresholdAlerting.txt 檔案中。

![30 秒篩選查詢](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

您現在應該會看到包含只 245 的資料列和感應器的名稱結果 hello 平均冰點大於 100。 此查詢群組 hello 依事件資料流**dspl**，即 hello 感應器的名稱，超過**輪轉視窗**30 秒。 暫時查詢必須我們要如何時間 tooprogress 的狀態。 使用 hello **TIMESTAMP BY**子句中，我們已指定 hello **OUTPUTTIME**所有時態計算資料行 tooassociate 時間。 如需詳細資訊，閱讀 hello MSDN 文章[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[視窗化函數](https://msdn.microsoft.com/library/azure/dn835019.aspx)。

### <a name="query-detect-absence-of-events"></a>查詢：測不存在的事件
我們如何寫入查詢 toofind 缺乏輸入事件？ 感應器傳送的資料和未傳送嗨事件下一分鐘，讓我們尋找 hello 最後一次。 hello 查詢是 hello AbsenseOfEvent.txt 檔案中。

![偵測不存在的事件](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

我們在此使用**LEFT OUTER**聯結 toohello 相同的資料流 （自我聯結）。 對於 **INNER** 聯結，只會在找到相符項目時傳回結果。  如**LEFT OUTER**聯結中，如果從 hello hello 聯結的左方事件不相符，對所有 hello hello 右端的資料行有 NULL 的資料列就會傳回。 這項技術會很有幫助 toofind 的事件不存在。 如需 [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx) 的詳細資訊，請參閱我們的 MSDN 文件。

## <a name="conclusion"></a>結論
hello 本教學課程的目的是的 toodemonstrate toowrite 不同的資料流分析查詢語言查詢，並查看結果 hello 瀏覽器中的方式。 但是，這只是剛開始。 您還可以使用串流分析執行更多功能。 串流分析支援各種不同的輸入和輸出和可以甚至使用函式在 Azure Machine Learning toomake 它健全的工具來分析資料流。 您可以使用來啟動更多關於資料流分析 tooexplore 我們[學習地圖](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/)。 如需有關如何查詢 toowrite hello 文章閱讀有關[常見的查詢模式](stream-analytics-stream-analytics-query-patterns.md)。

