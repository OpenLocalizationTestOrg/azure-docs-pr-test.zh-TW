---
title: "aaaDeep 深入了解預測一種載具，健全狀況和驅動習慣-Azure |Microsoft 文件"
description: "一種載具，健全狀況使用 Cortana 智慧 toogain 即時和預測 insights hello 功能和驅動習慣。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>一種載具遙測分析方案腳本： hello 方案深入探討
這**功能表**連結此腳本 toohello 區段： 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

此區段向下切入到每個所述的指示和指標以自訂的解決方案架構 hello hello 階段。 

## <a name="data-sources"></a>資料來源
hello 解決方案會使用兩個不同的資料來源：

* **模擬車輛訊號和診斷資料集** 和 
* **車輛類別目錄**

此方案包含車輛遠程資訊服務模擬器。 它會發出診斷資訊，並發出對應 toohello 狀態 hello vehicle 和 toohello 時間推動特定時點的模式。 按一下[Vehicle 車用通訊模擬器](http://go.microsoft.com/fwlink/?LinkId=717075)toodownload hello **Vehicle 車用通訊模擬器 Visual Studio 方案**適用於您的需求為基礎的自訂。 hello vehicle 類別目錄含有 VIN toomodel 對應的參考資料集。

![車輛遠程資訊服務模擬器](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

圖 1 – 車輛遠程資訊服務模擬器

這是 JSON 格式的資料集，其中包含下列結構描述的 hello。

| 資料欄 | 說明 | 值 |
| --- | --- | --- |
| VIN |隨機產生的車輛識別號碼 |這取自於一份含有 10,000 個隨機產生車輛識別號碼的主要清單。 |
| Outside temperature |hello 外溫度 hello vehicle 驅動的位置 |從 0-100 隨機產生的數字 |
| Engine temperature |hello 汽車的 hello 引擎溫度 |從 0-500 隨機產生的數字 |
| 速度 |一種載具，隨著控制在哪些 hello hello 引擎速度 |從 0-100 隨機產生的數字 |
| Fuel |hello vehicle hello 燃料層級 |從 0-100 隨機產生的數字 (表示燃油量百分比) |
| EngineOil |hello 的 hello 汽車引擎石油層級 |從 0-100 隨機產生的數字 (表示機油量百分比) |
| 胎壓 |hello 汽車的 hello tire 壓力 |從 0-50 隨機產生的數字 (表示胎壓位準百分比) |
| Odometer |hello 里程計讀取的一種載具，hello |從 0-200000 隨機產生的數字 |
| Accelerator_pedal_position |hello accelerator 踏板位置的一種載具，hello |從 0-100 隨機產生的數字 (表示油門位準百分比) |
| Parking_brake_status |指出是否駐留 hello vehicle |True 或 False |
| Headlamp_status |指出其中 hello headlamp 上為 |True 或 False |
| Brake_pedal_status |指出是否 hello 剎車組踏板或不已按下 |True 或 False |
| Transmission_gear_position |hello 車輛的 hello 傳輸齒輪位置 |狀態：first、second、third、fourth、fifth、sixth、seventh、eighth |
| Ignition_status |表示一種載具，hello 執行或完全停止 |True 或 False |
| Windshield_wiper_status |指出是否 hello 擋風玻璃挪移或未開啟 |True 或 False |
| ABS |指出 ABS 是否發揮作用 |True 或 False |
| Timestamp |hello 建立 hello 資料點時的時間戳記 |Date |
| City |一種載具，hello 的 hello 位置 |此方案中有 4 個城市：Bellevue、Redmond、Sammamish、Seattle |

hello vehicle 模型參考資料集包含 VIN toohello 模型對應。 

| VIN | 模型 |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |轎車 |
| 8J0U8XCPRGW4Z3NQE |混合式 |
| WORG68Z2PLTNZDBI7 |家庭房車 |
| JTHMYHQTEPP4WBMRN |轎車 |
| W9FTHG27LZN1YWO0Y |混合式 |
| MHTP9N792PHK08WJM |家庭房車 |
| EI4QXI2AXVQQING4I |轎車 |
| 5KKR2VB4WHQH97PF8 |混合式 |
| W9NSZ423XZHAONYXB |家庭房車 |
| 26WJSGHX4MA5ROHNL |敞篷車 |
| GHLUB6ONKMOSI7E77 |旅行車 |
| 9C2RHVRVLMEJDBXLP |小型車 |
| BRNHVMZOUJ6EOCP32 |小型 SUV |
| VCYVW0WUZNBTM594J |跑車 |
| HNVCE6YFZSA5M82NY |中型 SUV |
| 4R30FOR7NUOBL05GJ |旅行車 |
| WYNIIY42VKV6OQS1J |大型 SUV |
| 8Y5QKG27QET1RBK7I |大型 SUV |
| DF6OX2WSRA6511BVG |兩人座轎車 |
| Z2EOZWZBXAEW3E60T |轎車 |
| M4TV6IEALD5QDS3IR |混合式 |
| VHRA1Y2TGTA84F00H |家庭房車 |
| R0JAUHT1L1R3BIKI0 |轎車 |
| 9230C202Z60XX84AU |混合式 |
| T8DNDN5UDCWL7M72H |家庭房車 |
| 4WPYRUZII5YV7YA42 |轎車 |
| D1ZVY26UV2BFGHZNO |混合式 |
| XUF99EW9OIQOMV7Q7 |家庭房車 |
| 8OMCL3LGI7XNCC21U |敞篷車 |
| ……. | |

### <a name="references"></a>參考
[Vehicle Telematics Simulator Visual Studio 方案](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Azure 事件中樞](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>擷取
Azure 事件中樞、 Stream Analytics 中，與 Data Factory 的組合會運用 tooingest hello vehicle 訊號，hello 診斷事件，與即時和批次分析。 所有這些元件建立和設定為 hello 方案部署的一部分。 

### <a name="real-time-analysis"></a>即時分析
hello hello Vehicle 車用通訊模擬器所產生的事件發行 toohello 事件中心使用 hello 事件中樞 SDK。 hello 資料流分析工作內嵌 hello 事件中心中的這些事件和處理序 hello 即時 tooanalyze hello vehicle 健全狀況中的資料。 

![事件中樞儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

圖 4 - 事件中樞儀表板

![處理資料的串流分析作業](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

圖 5 - 處理資料的串流分析作業

hello 資料流分析工作。

* 內嵌 hello 事件中心的資料 
* 執行與 hello 的參考資料 toomap hello vehicle VIN toohello 對應模型的聯結 
* 將資料保存到 Azure Blob 儲存體以進行充分的批次分析。 

下列資料流分析查詢的 hello 是使用的 toopersist hello 資料到 Azure blob 儲存體。 

![用於擷取資料的串流分析作業查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

圖 6 - 用於擷取資料的串流分析作業查詢

### <a name="batch-analysis"></a>批次分析
我們也會產生另一批模擬車輛訊號和診斷資料集，以進行更多樣的批次分析。 這是必要的 tooensure 批次處理的良好的代表性資料磁碟區。 基於此目的，我們會使用管線 hello Azure Data Factory 的工作流程 toogenerate 中名為"PrepareSampleDataPipeline"模擬的 vehicle 訊號和診斷的資料集的一年的價值。 按一下[Data Factory 的自訂活動](http://go.microsoft.com/fwlink/?LinkId=717077)toodownload hello Data Factory 自訂 DotNet 活動 Visual Studio 方案的自訂項目會根據您的需求。 

![準備批次處理工作流程的範例資料](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

圖 7 - 準備批次處理工作流程的範例資料

hello 管線包含自訂的 ADF.Net 這裡顯示的活動：

![PrepareSampleDataPipeline 活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

圖 8 - PrepareSampleDataPipeline

一旦 hello 管線執行成功，並且 「 RawCarEventsTable 」 資料集標示為 「 準備 」，一年值得的一種載具，模擬的訊號和診斷資料所產生。 您看到 hello 下列資料夾和 hello"connectedcar 」 容器下的儲存體帳戶中建立的檔案：

![PrepareSampleDataPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

圖 9 - PrepareSampleDataPipeline 輸出

### <a name="references"></a>參考
[適用於串流擷取的 Azure 事件中樞 SDK](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Azure Data Factory 資料移動功能](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet 活動](../data-factory/data-factory-use-custom-activities.md)

[適用於準備範例資料的 Azure Data Factory DotNet 活動 Visual Studio 方案](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>資料分割 hello 資料集
hello 原始半結構化的車輛訊號和診斷的資料集被分割成年/月格式 hello 資料準備步驟中。 接下來，做為 hello 第一個帳戶啟用容錯移轉從某個 blob 帳戶 toohello 可擴充長期的儲存體已滿和這樣的分割升級更有效率的查詢。 

>[!NOTE] 
>Hello 方案中的這個步驟是適用的唯一 toobatch 處理。

輸入和輸出資料的資料管理︰

* hello**輸出資料**(標示為*PartitionedCarEventsTable*) toobe 保留很長一段時間的形式 hello 基本 /"rawest"hello 客戶 」 資料湖"中的資料。 
* hello**輸入資料**toothis 管線會通常會被捨去 hello 輸出資料具有完整不失真 toohello 輸入-只儲存 （分割） 更好供後續使用。

![分割汽車事件工作流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

圖 10 – 分割汽車事件工作流程

hello 未經處理資料分割"PartitionCarEventsPipeline 」 中使用 Hive HDInsight 活動。 依年/月會分割為一年產生在步驟 1 中的 hello 範例資料。 hello 分割區是使用的 toogenerate vehicle 訊號和診斷資料，每個月 （總計 12 個資料分割） 的一年。 

![PartitionCarEventsPipeline 活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

圖 11 - PartitionCarEventsPipeline

PartitionConnectedCarEvents Hive 指令碼

hello 下列 Hive 指令碼名為"partitioncarevents.hql 」，用於資料分割和位於 hello 下載 zip hello"\demo\src\connectedcar\scripts"資料夾中。 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。

![分割的輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

圖 12 - 分割的輸出

hello 資料現在已最佳化，更容易管理而且準備好進行進一步的處理 toogain 豐富的批次的深入資訊。 

## <a name="data-analysis"></a>資料分析
在本節中，您會看到 toocombine Azure Stream Analytics、 Azure 機器學習服務、 Azure Data Factory 和豐富的 Azure HDInsight 的進階分析一種載具，健全狀況和推動習慣。 以下共有三個小節︰

1. **機器學習**： 本小節包含我們已使用需要的服務維護和車輛需要恢復 toosafety 問題因為此方案 toopredict 車輛的 hello 異常偵測實驗的詳細資訊。
2. **即時分析**： 本小節包含有關 hello 即時分析使用 hello Stream Analytics 查詢語言，並運用 hello 機器學習實驗中使用自訂的應用程式的即時資訊。
3. **批次分析**： 本小節包含 hello 轉換和使用 Azure HDInsight 和 Azure Machine Learning 實際運作的 Azure Data Factory 的 hello 批次資料處理的相關資訊。

### <a name="machine-learning"></a>機器學習服務
我們的目標是 toopredict hello 車輛，需要維護或重新叫用特定的健全狀況統計資料為基礎。 我們進行下列假設 hello

* 如果其中一個 hello 下列三個條件都成立，hello 車輛需要**服務維護**:
  
  * 胎壓偏低
  * 機油量偏低
  * 引擎溫度偏高
* 如果其中一個 hello 下列條件都成立，可能會有 hello 車輛**安全性問題**，而且需要**回收**:
  
  * 引擎溫度偏高，但外部溫度偏低
  * 引擎溫度偏低，但外部溫度偏高

根據 hello 先前的需求，我們已經建立兩個不同的模型 toodetect 異常 vehicle 維護偵測，一個汽車重新叫用偵測。 在這兩個這些模型 hello 內建的主體元件分析 (PCA) 演算法用於異常偵測。 

**維修偵測模型**

如果其中一個三個指標-tire 不足的壓力，引擎石油或引擎溫度-滿足其各自的條件，hello 維護偵測模型報告異常狀況。 如此一來，我們只需要 tooconsider 這些建立 hello 模型中的三個變數。 在 Azure Machine Learning 中我們實驗中，我們會先使用**資料集中選取的資料行**模組 tooextract 這些三個變數。 接下來，我們會使用 hello PCA 為基礎的異常偵測模組 toobuild hello 異常偵測模型。 

主體元件分析 (PCA) 是可以套用的 toofeature 選取範圍、 分類以及異常偵測的機器學習中建立的技術。 PCA 會將一組包含可能相關變數的案例，轉換成一組稱為主成分的值。 hello 以 PCA 為基礎的模型化的索引鍵的概念是 tooproject 至較低維空間的資料，因此功能和異常情況更方便識別。

針對每個新的輸入太 hello 偵測模型，hello 異常偵測器會先計算上 hello 特徵向量，其投影，然後計算 hello 正規化重建錯誤。 這個正規化的錯誤是 hello 異常分數。 hello hello 錯誤的機率越高，hello 更多異常 hello 執行個體是。 

Hello 維護偵測問題，請在 3d 空間中的點由 tire 不足的壓力，引擎石油和引擎溫度座標可視為每一筆記錄。 toocapture 這些異常情況中，我們可以投射 hello hello 3d 空間中的原始資料使用 PCA 2 維度空間。 因此，我們會在 PCA toobe 2 中設定 hello 參數元件 toouse 數目。 在套用以 PCA 為基礎的異常偵測時，這個參數扮演重要的角色。 使用 PCA 投射資料之後，我們可以更輕鬆識別這些異常。

**回收異常偵測模型**hello 回收異常偵測模型，我們使用 hello 選取資料行中的資料集和 PCA 為基礎的異常偵測模組類似的方式。 具體來說，我們先擷取三個變數-引擎溫度、 外部溫度、 和速度-使用 hello**資料集中選取的資料行**模組。 我們也包含 hello 速度變數 hello 引擎溫度通常是因為相互關聯 toohello 速度。 接下來我們使用 PCA 為基礎的異常偵測模組 tooproject hello 資料從 hello 3d 空間至 2 維度空間。 hello 回收準則符合，而且引擎溫度外部溫度高負面相互關聯時 hello 一種載具，因此需要重新叫用。 使用以 PCA 為基礎的異常偵測演算法，我們可以執行 PCA 之後擷取 hello 異常狀況。 

訓練兩種模式中，我們需要 toouse 一般資料，不需要維護或重新叫用為 hello 輸入的資料 tootrain hello PCA 為基礎的異常偵測模型。 在 hello 計分實驗，我們會使用 hello 定型異常偵測模型 toodetect hello vehicle 需要維護或重新叫用。 

### <a name="real-time-analysis"></a>即時分析
hello 遵循串流分析 SQL 查詢會使用所有 tooget 都 hello 平均都 hello 重要的一種載具參數如 vehicle 速度、 燃料層級、 引擎溫度、 里程計讀取、 tire 不足的壓力，引擎石油層級，與其他人。 hello 平均值是使用的 toodetect 異常發出警示，並判斷 hello 的特定區域中運作的車輛通行狀況的整體健全狀況，然後關聯 toodemographics。 

![用於即時處理的串流分析查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

圖 13 – 用於即時處理的串流分析查詢

所有的 hello 平均會計算透過 3 秒 TumblingWindow。 因為我們需要非重疊和連續的時間間隔，所以在此案例中使用 TubmlingWindow。 

toolearn 進一步了解所有 hello 「 視窗 」 功能，在 Azure Stream Analytics 中，按一下[視窗化 (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx)。

**即時預測**

實際的時間，應用程式是 hello 方案 toooperationalize hello 機器學習模型的一部分。 此應用程式呼叫 「 RealTimeDashboardApp"建立並設定為 hello 方案部署的一部分。 hello 應用程式會執行下列 hello:

1. 會接聽 tooan 事件中樞執行個體，其中資料流分析會發佈 hello 事件模式中持續。 ![發行 hello 資料的資料流分析查詢](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png)*圖 14-發行 hello 資料 tooan 資料流分析查詢的輸出事件中樞執行個體* 
2. 對於此應用程式收到的每個事件： 
   
   * 處理序 hello 資料使用機器學習要求回應計分 (RR) 端點。 hello RR 端點就會自動發行 hello 部署的一部分。
   * hello RR 輸出為已發行的 tooa Power BI 資料集使用 hello 推入應用程式開發介面。

此模式也是您想 toointegrate 企業營運 (LoB) 應用程式與 hello 即時分析流量，例如警示、 通知和傳訊案例的適用 tooscenarios。

按一下[RealtimeDashboardApp 下載](http://go.microsoft.com/fwlink/?LinkId=717078)toodownload hello RealtimeDashboardApp Visual Studio 方案的自訂項目。 

**tooexecute hello 即時儀表板應用程式**
1. 在本機擷取並儲存 ![RealtimeDashboardApp 資料夾](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png)圖 16 – RealtimeDashboardApp 資料夾  
2. 執行 hello 應用程式 RealtimeDashboardApp.exe
3. 提供有效的 Power BI 認證、登入，然後按一下 [接受] ![即時儀表板應用程式登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![即時儀表板應用程式完成登入 tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*圖 17-RealtimeDashboardApp： 登入 tooPower BI*

>[!NOTE] 
>如果您想 tooflush hello Power BI 資料集時，執行 hello RealtimeDashboardApp hello"flushdata 」 參數： 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>批次分析
hello 現在的目標是的 tooshow Contoso 馬達如何利用 hello Azure 計算功能 tooharness 巨量資料 toogain 豐富的洞察能力模式、 使用方式的行為，以及一種載具，健全狀況。 這可達成下列目標：

* 改善 hello 客戶經驗並使其成本較低習慣以及燃料有效率驅動行為提供深入資訊
* 主動了解客戶和推動詳述 toogovern 業務決策，並在類別產品 & 服務最適合提供 hello

在此解決方案中，我們的目標 hello 下列度量：

1. **主動驅使行為**： 識別 hello 趨勢的 hello 模型、 位置、 推動條件與 hello 年 toogain 的洞察能力積極驅動模式的時間。 Contoso Motors 可使用這些了解來進行行銷活動、推出新的人性化功能，以及基於使用方式的保險。
2. **促進了有效率的推動行為**： 識別 hello 趨勢的 hello 模型、 位置、 推動條件與 hello 年 toogain 的洞察能力燃料有效率驅動模式的時間。 Contoso 馬達可以使用這些 insights 行銷活動時，驅動的新功能和主動式報告 toohello 驅動程式成本效益與環境易記驅動習慣。 
3. **前文提過模型**： 識別模型需要由運用 hello 異常偵測機器學習實驗的恢復

讓我們來看到 hello 詳細資料的每個這些度量，

**危險駕駛模式**

hello 分割 vehicle 訊號和診斷資料會處理在 hello 管線中名為"AggresiveDrivingPatternPipeline 」 使用 Hive toodetermine hello 模型、 位置、 一種載具，推動 and 表現其他參數積極驅動的模式。

![危險駕駛模式工作流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*圖 18 – 危險駕駛模式工作流程*


危險駕駛模式 Hive 查詢

hello 名為"aggresivedriving.hql 」 可用來分析積極驅動條件模式的 Hive 指令碼位於 「 \demo\src\connectedcar\scripts"hello 下載 zip 資料夾。 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


它會使用 hello 組合車輛的傳輸齒輪位置、 剎車組踏板狀態和速度 toodetect 魯莽/積極驅使行為根據煞車最高速度的模式。 

一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。

![AggressiveDrivingPatternPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

圖 19 – AggressiveDrivingPatternPipeline 輸出

**省油駕駛模式**

hello 分割 vehicle 訊號，然後在名為"FuelEfficientDrivingPatternPipeline"hello 管線中處理診斷資料。 Hive 是使用的 toodetermine hello 模型、 位置、 vehicle、 推動條件和其他屬性，才會看到燃料有效率驅動模式。

![省油駕駛模式](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

圖 20 – 省油駕駛模式工作流程

省油駕駛模式 Hive 查詢

hello 名為"fuelefficientdriving.hql 」 可用來分析積極驅動條件模式的 Hive 指令碼位於 「 \demo\src\connectedcar\scripts"hello 下載 zip 資料夾。 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


它會使用 hello 組合車輛的傳輸齒輪位置、 剎車組踏板狀態、 速度以及 accelerator 踏板位置 toodetect 燃料有效率驅動行為根據加速，煞車，並加速模式。 

一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。

![FuelEfficientDrivingPatternPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

圖 21 – FuelEfficientDrivingPatternPipeline 輸出

**召回預測**

hello 機器學習實驗佈建並發佈為 web 服務為 hello 方案部署的一部分。 此工作流程，註冊為資料連結的 factory 服務，並使用資料處理站批次計分活動實際運作可用 hello 批次計分結束點。

![機器學習服務端點](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

圖 22 – 在 Data Factory 中註冊為連結服務的機器學習服務端點

hello 註冊連結的服務用於使用 hello 異常偵測模型 hello DetectAnomalyPipeline tooscore hello 資料。 

![Data Factory 中的 Azure Machine Learning 批次評分活動](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

圖 23 – Data Factory 中的 Azure Machine Learning 批次評分活動 

有幾個步驟，讓它可以 operationalized hello 批次計分 web 服務，在資料準備為此管線中執行。 

![用於預測需要召回車輛的 DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

圖 24 – 用於預測需要召回車輛的 DetectAnomalyPipeline 

異常偵測 Hive 查詢

一旦完成 hello 計分，HDInsight 活動是使用的 tooprocess 和彙總的 hello 資料分類為異常 0.60 或更高的機率分數與 hello 模型。

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


一旦 hello 管線已成功執行之後，您會看到下列資料分割產生 hello"connectedcar 」 容器下的儲存體帳戶中的 hello。

![DetectAnomalyPipeline 輸出](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

圖 25 – DetectAnomalyPipeline 輸出

## <a name="publish"></a>發佈

### <a name="real-time-analysis"></a>即時分析
其中一個 hello 資料流分析作業中的 hello 查詢發行 hello 事件 tooan 輸出事件中樞執行個體。 

![串流分析工作發行 tooan 輸出事件中樞執行個體](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*圖 26 – 資料流分析工作發行 tooan 輸出事件中樞執行個體*

![資料流分析查詢 toopublish toohello 輸出事件中樞執行個體](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*圖 27-Stream Analytics 查詢 toopublish toohello 輸出事件中樞執行個體*

這個資料流的事件是由包含在 hello 解決方案中 RealTimeDashboardApp hello 取用。 此應用程式會利用進行即時計分 hello 機器學習要求-回應 web 服務，並將發佈 hello 產生的資料 tooa Power BI 資料集供取用。 

### <a name="batch-analysis"></a>批次分析
hello 的 hello 批次和即時處理的結果會耗用的已發行的 toohello Azure SQL Database 資料表。 hello Azure SQL Server、 資料庫和 hello 資料表會自動建立 hello 安裝指令碼的一部分。 

![批次處理結果複製 toodata 超市流程](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*圖 28-批次處理的結果複製 toodata 超市工作流程*

![串流分析工作發行 toodata 超市](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*圖 29 – 資料流分析工作發行 toodata 超市*

![串流分析作業中的資料超市設定](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

圖 30 – 串流分析作業中的資料超市設定

## <a name="consume"></a>取用
Power BI 給此方案一個豐富的儀表板來提供即時資料和預測性分析視覺效果。 

如需有關設定 hello Power BI 報表和 hello 儀表板的詳細指示，請按一下這裡。 hello 最終儀表板看起來像這樣：

![Power BI 儀表板](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

圖 31 - Power BI 儀表板

## <a name="summary"></a>摘要
本文件包含詳細的向下鑽研的 hello Vehicle 遙測分析解決方案。 這以預測和動作示範即時和批次分析的 Lambda 架構模式。 此模式適用於 tooa 各種不同的使用案例需要最忙碌路徑 （即時） 和 （批次） 的冷路徑分析。 

