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
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a><span data-ttu-id="7a985-104">開始使用 Azure Stream Analytics tooprocess 資料從 IoT 裝置</span><span class="sxs-lookup"><span data-stu-id="7a985-104">Get started with Azure Stream Analytics tooprocess data from IoT devices</span></span>
<span data-ttu-id="7a985-105">在此教學課程中，您將學習如何 toocreate 資料流處理邏輯 toogather 物聯網 (IoT) 裝置的資料。</span><span class="sxs-lookup"><span data-stu-id="7a985-105">In this tutorial, you will learn how toocreate stream-processing logic toogather data from Internet of Things (IoT) devices.</span></span> <span data-ttu-id="7a985-106">我們將如何使用真實世界的物聯網 (IoT) 使用案例 toodemonstrate toobuild 方案快速且經濟。</span><span class="sxs-lookup"><span data-stu-id="7a985-106">We will use a real-world, Internet of Things (IoT) use case toodemonstrate how toobuild your solution quickly and economically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a985-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a985-107">Prerequisites</span></span>
* [<span data-ttu-id="7a985-108">Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7a985-108">Azure subscription</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* <span data-ttu-id="7a985-109">範例查詢和資料檔案可從 [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span><span class="sxs-lookup"><span data-stu-id="7a985-109">Sample query and data files downloadable from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span></span>

## <a name="scenario"></a><span data-ttu-id="7a985-110">案例</span><span class="sxs-lookup"><span data-stu-id="7a985-110">Scenario</span></span>
<span data-ttu-id="7a985-111">Contoso，這是一家公司 hello 工業自動化空間中的，已完全自動化其製造程序。</span><span class="sxs-lookup"><span data-stu-id="7a985-111">Contoso, which is a company in hello industrial automation space, has completely automated its manufacturing process.</span></span> <span data-ttu-id="7a985-112">在這種植物 hello 機制有能夠發出的即時資料流的感應器。</span><span class="sxs-lookup"><span data-stu-id="7a985-112">hello machinery in this plant has sensors that are capable of emitting streams of data in real time.</span></span> <span data-ttu-id="7a985-113">在此案例中，生產 floor 經理想 toohave hello 感應器資料 toolook 從即時深入資訊的模式，並對其採取動作。</span><span class="sxs-lookup"><span data-stu-id="7a985-113">In this scenario, a production floor manager wants toohave real-time insights from hello sensor data toolook for patterns and take actions on them.</span></span> <span data-ttu-id="7a985-114">我們將使用在 hello 感應器資料 toofind 有趣模式上的資料流分析查詢語言 (SAQL) hello 從 hello 內送資料流的資料。</span><span class="sxs-lookup"><span data-stu-id="7a985-114">We will use hello Stream Analytics Query Language (SAQL) over hello sensor data toofind interesting patterns from hello incoming stream of data.</span></span>

<span data-ttu-id="7a985-115">這裡的資料是從 Texas Instrument 的感應器標籤裝置產生。</span><span class="sxs-lookup"><span data-stu-id="7a985-115">Here data is being generated from a Texas Instruments sensor tag device.</span></span>

![Texas Instruments 的感應器標籤](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

<span data-ttu-id="7a985-117">hello 裝載的 hello 資料的 JSON 格式，而且看起來像下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7a985-117">hello payload of hello data is in JSON format and looks like hello following:</span></span>

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

<span data-ttu-id="7a985-118">在真實世界的案例中，您可以擁有數百個此類感應器，產生事件作為串流。</span><span class="sxs-lookup"><span data-stu-id="7a985-118">In a real-world scenario, you could have hundreds of these sensors generating events as a stream.</span></span> <span data-ttu-id="7a985-119">在理想情況下，閘道裝置會執行程式碼 toopush 這些事件太[Azure 事件中心](https://azure.microsoft.com/services/event-hubs/)或[Azure IoT 中樞](https://azure.microsoft.com/services/iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="7a985-119">Ideally, a gateway device would run code toopush these events too[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="7a985-120">串流分析工作會擷取這些事件，從事件中樞，並針對 hello 資料流執行即時分析查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-120">Your Stream Analytics job would ingest these events from Event Hubs and run real-time analytics queries against hello streams.</span></span> <span data-ttu-id="7a985-121">然後，您可以傳送的 hello hello 結果 tooone[支援輸出](stream-analytics-define-outputs.md)。</span><span class="sxs-lookup"><span data-stu-id="7a985-121">Then, you could send hello results tooone of hello [supported outputs](stream-analytics-define-outputs.md).</span></span>

<span data-ttu-id="7a985-122">為了方便使用，本入門指南會提供擷取自實際感應器標籤裝置的範例資料檔。</span><span class="sxs-lookup"><span data-stu-id="7a985-122">For ease of use, this getting started guide provides a sample data file, which was captured from real sensor tag devices.</span></span> <span data-ttu-id="7a985-123">您可以在 hello 範例資料上執行查詢，並查看結果。</span><span class="sxs-lookup"><span data-stu-id="7a985-123">You can run queries on hello sample data and see results.</span></span> <span data-ttu-id="7a985-124">在後續的教學課程，您將學習如何 tooconnect 您作業 tooinputs 和輸出，並將其部署 toohello Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7a985-124">In subsequent tutorials, you will learn how tooconnect your job tooinputs and outputs and deploy them toohello Azure service.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="7a985-125">建立串流分析工作</span><span class="sxs-lookup"><span data-stu-id="7a985-125">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="7a985-126">在 hello [Azure 入口網站](http://portal.azure.com)，按一下加號 hello，然後輸入**STREAM ANALYTICS** hello 文字視窗 toohello 右中。</span><span class="sxs-lookup"><span data-stu-id="7a985-126">In hello [Azure portal](http://portal.azure.com), click hello plus sign and then type **STREAM ANALYTICS** in hello text window toohello right.</span></span> <span data-ttu-id="7a985-127">然後選取**資料流分析工作**hello [結果] 清單中。</span><span class="sxs-lookup"><span data-stu-id="7a985-127">Then select **Stream Analytics job** in hello results list.</span></span>
   
    ![建立新的串流分析作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. <span data-ttu-id="7a985-129">輸入唯一的作業名稱，並確認 hello 訂用帳戶是 hello 正確的另一個用於您的工作。</span><span class="sxs-lookup"><span data-stu-id="7a985-129">Enter a unique job name and verify hello subscription is hello correct one for your job.</span></span> <span data-ttu-id="7a985-130">然後建立新的資源群組，或在您的訂用帳戶上選取現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a985-130">Then either create a new resource group or select an existing one on your subscription.</span></span>
3. <span data-ttu-id="7a985-131">然後選取作業的位置。</span><span class="sxs-lookup"><span data-stu-id="7a985-131">Then select a location for your job.</span></span> <span data-ttu-id="7a985-132">處理速度和降低成本選取 hello 的資料傳輸的建議與 hello 資源群組和預期的儲存體帳戶相同的位置。</span><span class="sxs-lookup"><span data-stu-id="7a985-132">For speed of processing and reduction of cost in data transfer selecting hello same location as hello resource group and intended storage account is recommended.</span></span>
   
    ![建立新的串流分析作業詳細資料](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > <span data-ttu-id="7a985-134">每個區域只應該建立一次此儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7a985-134">You should create this storage account only once per region.</span></span> <span data-ttu-id="7a985-135">此儲存體會供該區域中建立的所有串流分析作業共用。</span><span class="sxs-lookup"><span data-stu-id="7a985-135">This storage will be shared across all Stream Analytics jobs that are created in that region.</span></span>
   > 
   > 
4. <span data-ttu-id="7a985-136">檢查 hello 方塊 tooplace 您儀表板上的工作，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="7a985-136">Check hello box tooplace your job on your dashboard and then click **CREATE**.</span></span>
   
    ![正在建立作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. <span data-ttu-id="7a985-138">您應該會看到 '部署已開始...' hello 右上方瀏覽器視窗的顯示。</span><span class="sxs-lookup"><span data-stu-id="7a985-138">You should see a 'Deployment started...' displayed in hello top right of your browser window.</span></span> <span data-ttu-id="7a985-139">很快就將會變更已完成的 tooa 視窗，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7a985-139">Soon it will change tooa completed window as shown below.</span></span>
   
    ![正在建立作業](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a><span data-ttu-id="7a985-141">建立 Azure 串流分析查詢</span><span class="sxs-lookup"><span data-stu-id="7a985-141">Create an Azure Stream Analytics query</span></span>
<span data-ttu-id="7a985-142">您的工作之後建立的時間 tooopen 它與建置查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-142">After your job is created it's time tooopen it and build a query.</span></span> <span data-ttu-id="7a985-143">您可以按一下 hello 磚輕鬆存取您的工作。</span><span class="sxs-lookup"><span data-stu-id="7a985-143">You can easily access your job by clicking hello tile for it.</span></span>

![作業圖格](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

<span data-ttu-id="7a985-145">在 [hello**作業拓撲**] 窗格中按一下 hello**查詢**方塊 toogo toohello 查詢編輯器。</span><span class="sxs-lookup"><span data-stu-id="7a985-145">In hello **Job Topology** pane click hello **QUERY** box toogo toohello Query Editor.</span></span> <span data-ttu-id="7a985-146">hello**查詢**編輯器可讓您透過 hello 內送事件資料執行 hello 轉換的 tooenter T-SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-146">hello **QUERY** editor allows you tooenter a T-SQL query that performs hello transformation over hello incoming event data.</span></span>

![查詢方塊](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a><span data-ttu-id="7a985-148">查詢：封存未經處理資料</span><span class="sxs-lookup"><span data-stu-id="7a985-148">Query: Archive your raw data</span></span>
<span data-ttu-id="7a985-149">hello 查詢最簡單形式是封存指定輸出的所有輸入的資料 tooits 之傳遞查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-149">hello simplest form of query is a pass-through query that archives all input data tooits designated output.</span></span> <span data-ttu-id="7a985-150">下載 hello 範例資料檔從[GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa 您電腦上的位置。</span><span class="sxs-lookup"><span data-stu-id="7a985-150">Download hello sample data file from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa location on your computer.</span></span> 

1. <span data-ttu-id="7a985-151">貼上從 hello PassThrough.txt 檔案 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-151">Paste hello query from hello PassThrough.txt file.</span></span> 
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. <span data-ttu-id="7a985-153">按一下 hello 三個點下一步 tooyour 輸入，然後選取**從檔案的範例資料上傳**方塊。</span><span class="sxs-lookup"><span data-stu-id="7a985-153">Click hello three dots next tooyour input and select **Upload sample data from file** box.</span></span>
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. <span data-ttu-id="7a985-155">窗格會在 hello 開啟右如此一來，它選取 hello HelloWorldASA InputStream.json 資料檔從您的下載位置，並按一下**確定**在 hello hello 窗格的底部。</span><span class="sxs-lookup"><span data-stu-id="7a985-155">A pane opens on hello right as a result, in it select hello HelloWorldASA-InputStream.json data file from your downloaded location and click **OK** at hello bottom of hello pane.</span></span>
   
    ![測試輸入串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. <span data-ttu-id="7a985-157">然後按一下 [hello**測試**齒輪 hello 左上角區域中的 hello] 視窗中，然後處理 hello 範例資料集對測試查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-157">Then click hello **Test** gear in hello top left area of hello window and process your test query against hello sample dataset.</span></span> <span data-ttu-id="7a985-158">Hello 處理完成時，會開啟下您的查詢結果 視窗。</span><span class="sxs-lookup"><span data-stu-id="7a985-158">A results window will open below your query as hello processing is complete.</span></span>
   
    ![測試結果](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a><span data-ttu-id="7a985-160">篩選 hello 資料為基礎的查詢：</span><span class="sxs-lookup"><span data-stu-id="7a985-160">Query: Filter hello data based on a condition</span></span>
<span data-ttu-id="7a985-161">我們來試試 toofilter hello 結果根據條件。</span><span class="sxs-lookup"><span data-stu-id="7a985-161">Let’s try toofilter hello results based on a condition.</span></span> <span data-ttu-id="7a985-162">我們希望 tooshow 結果事件來自 「 sensorA。 」</span><span class="sxs-lookup"><span data-stu-id="7a985-162">We would like tooshow results for only those events that come from “sensorA.”</span></span> <span data-ttu-id="7a985-163">hello 查詢是 hello Filtering.txt 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a985-163">hello query is in hello Filtering.txt file.</span></span>

![篩選資料串流](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

<span data-ttu-id="7a985-165">請注意，hello 區分大小寫的查詢比較的字串值。</span><span class="sxs-lookup"><span data-stu-id="7a985-165">Note that hello case-sensitive query compares a string value.</span></span> <span data-ttu-id="7a985-166">按一下 hello**測試**齒輪再次 tooexecute hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="7a985-166">Click hello **Test** gear again tooexecute hello query.</span></span> <span data-ttu-id="7a985-167">hello 查詢必須傳回 389 從 1860年事件的資料列。</span><span class="sxs-lookup"><span data-stu-id="7a985-167">hello query should return 389 rows out of 1860 events.</span></span>

![查詢測試的第二個輸出結果](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a><span data-ttu-id="7a985-169">查詢： 警示 tootrigger 商務工作流程</span><span class="sxs-lookup"><span data-stu-id="7a985-169">Query: Alert tootrigger a business workflow</span></span>
<span data-ttu-id="7a985-170">讓我們的查詢變得更為詳細。</span><span class="sxs-lookup"><span data-stu-id="7a985-170">Let's make our query more detailed.</span></span> <span data-ttu-id="7a985-171">每種感應器的類型，我們會想 toomonitor 平均溫度每 30 秒的時間，高於 100 度的 hello 平均溫度時，才會顯示結果。</span><span class="sxs-lookup"><span data-stu-id="7a985-171">For every type of sensor, we want toomonitor average temperature per 30-second window and display results only if hello average temperature is above 100 degrees.</span></span> <span data-ttu-id="7a985-172">我們會撰寫 hello 下列查詢，然後按一下**測試**toosee hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7a985-172">We will write hello following query and then click **Test** toosee hello results.</span></span> <span data-ttu-id="7a985-173">hello 查詢是 hello ThresholdAlerting.txt 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a985-173">hello query is in hello ThresholdAlerting.txt file.</span></span>

![30 秒篩選查詢](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

<span data-ttu-id="7a985-175">您現在應該會看到包含只 245 的資料列和感應器的名稱結果 hello 平均冰點大於 100。</span><span class="sxs-lookup"><span data-stu-id="7a985-175">You should now see results that contain only 245 rows and names of sensors where hello average temperate is greater than 100.</span></span> <span data-ttu-id="7a985-176">此查詢群組 hello 依事件資料流**dspl**，即 hello 感應器的名稱，超過**輪轉視窗**30 秒。</span><span class="sxs-lookup"><span data-stu-id="7a985-176">This query groups hello stream of events by **dspl**, which is hello sensor name, over a **Tumbling Window** of 30 seconds.</span></span> <span data-ttu-id="7a985-177">暫時查詢必須我們要如何時間 tooprogress 的狀態。</span><span class="sxs-lookup"><span data-stu-id="7a985-177">Temporal queries must state how we want time tooprogress.</span></span> <span data-ttu-id="7a985-178">使用 hello **TIMESTAMP BY**子句中，我們已指定 hello **OUTPUTTIME**所有時態計算資料行 tooassociate 時間。</span><span class="sxs-lookup"><span data-stu-id="7a985-178">By using hello **TIMESTAMP BY** clause, we have specified hello **OUTPUTTIME** column tooassociate times with all temporal calculations.</span></span> <span data-ttu-id="7a985-179">如需詳細資訊，閱讀 hello MSDN 文章[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[視窗化函數](https://msdn.microsoft.com/library/azure/dn835019.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a985-179">For detailed information, read hello MSDN articles about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing functions](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

### <a name="query-detect-absence-of-events"></a><span data-ttu-id="7a985-180">查詢：測不存在的事件</span><span class="sxs-lookup"><span data-stu-id="7a985-180">Query: Detect absence of events</span></span>
<span data-ttu-id="7a985-181">我們如何寫入查詢 toofind 缺乏輸入事件？</span><span class="sxs-lookup"><span data-stu-id="7a985-181">How can we write a query toofind a lack of input events?</span></span> <span data-ttu-id="7a985-182">感應器傳送的資料和未傳送嗨事件下一分鐘，讓我們尋找 hello 最後一次。</span><span class="sxs-lookup"><span data-stu-id="7a985-182">Let’s find hello last time that a sensor sent data and then did not send events for hello next minute.</span></span> <span data-ttu-id="7a985-183">hello 查詢是 hello AbsenseOfEvent.txt 檔案中。</span><span class="sxs-lookup"><span data-stu-id="7a985-183">hello query is in hello AbsenseOfEvent.txt file.</span></span>

![偵測不存在的事件](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

<span data-ttu-id="7a985-185">我們在此使用**LEFT OUTER**聯結 toohello 相同的資料流 （自我聯結）。</span><span class="sxs-lookup"><span data-stu-id="7a985-185">Here we use a **LEFT OUTER** join toohello same data stream (self-join).</span></span> <span data-ttu-id="7a985-186">對於 **INNER** 聯結，只會在找到相符項目時傳回結果。</span><span class="sxs-lookup"><span data-stu-id="7a985-186">For an **INNER** join, a result is returned only when a match is found.</span></span>  <span data-ttu-id="7a985-187">如**LEFT OUTER**聯結中，如果從 hello hello 聯結的左方事件不相符，對所有 hello hello 右端的資料行有 NULL 的資料列就會傳回。</span><span class="sxs-lookup"><span data-stu-id="7a985-187">For a **LEFT OUTER** join, if an event from hello left side of hello join is unmatched, a row that has NULL for all hello columns of hello right side is returned.</span></span> <span data-ttu-id="7a985-188">這項技術會很有幫助 toofind 的事件不存在。</span><span class="sxs-lookup"><span data-stu-id="7a985-188">This technique is very useful toofind an absence of events.</span></span> <span data-ttu-id="7a985-189">如需 [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx) 的詳細資訊，請參閱我們的 MSDN 文件。</span><span class="sxs-lookup"><span data-stu-id="7a985-189">See our MSDN documentation for more information about [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="7a985-190">結論</span><span class="sxs-lookup"><span data-stu-id="7a985-190">Conclusion</span></span>
<span data-ttu-id="7a985-191">hello 本教學課程的目的是的 toodemonstrate toowrite 不同的資料流分析查詢語言查詢，並查看結果 hello 瀏覽器中的方式。</span><span class="sxs-lookup"><span data-stu-id="7a985-191">hello purpose of this tutorial is toodemonstrate how toowrite different Stream Analytics Query Language queries and see results in hello browser.</span></span> <span data-ttu-id="7a985-192">但是，這只是剛開始。</span><span class="sxs-lookup"><span data-stu-id="7a985-192">However, this is just getting started.</span></span> <span data-ttu-id="7a985-193">您還可以使用串流分析執行更多功能。</span><span class="sxs-lookup"><span data-stu-id="7a985-193">You can do so much more with Stream Analytics.</span></span> <span data-ttu-id="7a985-194">串流分析支援各種不同的輸入和輸出和可以甚至使用函式在 Azure Machine Learning toomake 它健全的工具來分析資料流。</span><span class="sxs-lookup"><span data-stu-id="7a985-194">Stream Analytics supports a variety of inputs and outputs and can even use functions in Azure Machine Learning toomake it a robust tool for analyzing data streams.</span></span> <span data-ttu-id="7a985-195">您可以使用來啟動更多關於資料流分析 tooexplore 我們[學習地圖](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/)。</span><span class="sxs-lookup"><span data-stu-id="7a985-195">You can start tooexplore more about Stream Analytics by using our [learning map](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/).</span></span> <span data-ttu-id="7a985-196">如需有關如何查詢 toowrite hello 文章閱讀有關[常見的查詢模式](stream-analytics-stream-analytics-query-patterns.md)。</span><span class="sxs-lookup"><span data-stu-id="7a985-196">For more information about how toowrite queries, read hello article about [common query patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>

