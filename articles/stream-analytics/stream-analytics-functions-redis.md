---
title: "Azure 函式的 aaaStream 分析即時處理 |Microsoft 文件"
description: "了解如何 toouse Azure 函式連接的服務匯流排佇列，toopopulate hello 輸出資料流分析工作的 Azure Redis 快取。"
keywords: "data stream, redis cache, service bus queue, 資料流, redis 快取, 服務匯流排佇列"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="abe5e-104">如何從 Azure Redis 快取 Azure 函式的使用中的 Azure Stream Analytics toostore 資料</span><span class="sxs-lookup"><span data-stu-id="abe5e-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="abe5e-105">Azure 串流分析可讓您快速開發和部署的低成本的解決方案 toogain 即時深入資訊從裝置、 感應器、 基礎結構，和應用程式或資料的任何資料流。</span><span class="sxs-lookup"><span data-stu-id="abe5e-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="abe5e-106">它可啟用不同的使用案例，例如即時管理與監視、命令與控制、詐騙偵測、Connected Cars 等等。</span><span class="sxs-lookup"><span data-stu-id="abe5e-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="abe5e-107">在許多這類案例中，您可能想 toostore Azure 串流分析輸出到分散式的資料存放區，例如 Azure Redis 快取的資料。</span><span class="sxs-lookup"><span data-stu-id="abe5e-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="abe5e-108">假設您是電信公司的員工。</span><span class="sxs-lookup"><span data-stu-id="abe5e-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="abe5e-109">您嘗試 toodetect SIM 詐騙，其中來自多個呼叫 hello 相同的識別、 在 hello 相同的時間，但在不同地理位置。</span><span class="sxs-lookup"><span data-stu-id="abe5e-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="abe5e-110">您負責 Azure Redis 快取中儲存所有 hello 潛在詐騙撥打電話。</span><span class="sxs-lookup"><span data-stu-id="abe5e-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="abe5e-111">在此部落格中，我們將提供如何輕鬆地完成此工作的指引。</span><span class="sxs-lookup"><span data-stu-id="abe5e-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="abe5e-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="abe5e-112">Prerequisites</span></span>
<span data-ttu-id="abe5e-113">完整的 hello[即時詐騙偵測][ fraud-detection] ASA 的逐步解說</span><span class="sxs-lookup"><span data-stu-id="abe5e-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="abe5e-114">架構概觀</span><span class="sxs-lookup"><span data-stu-id="abe5e-114">Architecture Overview</span></span>
![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="abe5e-116">Hello 前圖所示，資料流分析可讓資料流的輸入的資料 toobe 查詢和傳送 tooan 輸出。</span><span class="sxs-lookup"><span data-stu-id="abe5e-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="abe5e-117">根據 hello 輸出，Azure 函式可以接著會觸發某些類型事件。</span><span class="sxs-lookup"><span data-stu-id="abe5e-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="abe5e-118">在這篇部落格，我們將重點放在此管線 hello Azure 函式部分或更明確地說 hello 觸發的事件儲存到 hello 快取的詐騙資料。</span><span class="sxs-lookup"><span data-stu-id="abe5e-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="abe5e-119">完成 hello 之後[即時詐騙偵測][ fraud-detection]教學課程中，您已輸入 （事件中心）、 查詢，以及輸出 （blob 儲存） 已設定及執行。</span><span class="sxs-lookup"><span data-stu-id="abe5e-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="abe5e-120">在這篇部落格，我們，改為變更 hello 輸出 toouse 服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="abe5e-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="abe5e-121">在這之後，我們連接 Azure 函式 toothis 佇列。</span><span class="sxs-lookup"><span data-stu-id="abe5e-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="abe5e-122">建立並連接服務匯流排佇列輸出</span><span class="sxs-lookup"><span data-stu-id="abe5e-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="abe5e-123">toocreate 服務匯流排佇列，請依照下列步驟 1 和 2 中的 hello.NET 區段[開始使用 Service Bus 佇列][servicebus-getstarted]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="abe5e-124">現在讓我們將連接 hello 佇列 toohello 資料流分析工作所建立 hello 早詐騙偵測逐步解說。</span><span class="sxs-lookup"><span data-stu-id="abe5e-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="abe5e-125">在 hello Azure 入口網站，移 toohello**輸出**刀鋒視窗中的工作，然後選取**新增**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="abe5e-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![加入輸出](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="abe5e-127">選擇**服務匯流排佇列**為 hello **Sink**依照囉 」 畫面上 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="abe5e-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="abe5e-128">確定 toochoose hello 命名空間的 hello 服務匯流排佇列中您建立[開始使用 Service Bus 佇列][servicebus-getstarted]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="abe5e-129">當您完成時，請按一下 hello 「 右邊 」 按鈕。</span><span class="sxs-lookup"><span data-stu-id="abe5e-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="abe5e-130">指定下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="abe5e-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="abe5e-131">**事件序列化程式格式**：JSON</span><span class="sxs-lookup"><span data-stu-id="abe5e-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="abe5e-132">**編碼**：UTF8</span><span class="sxs-lookup"><span data-stu-id="abe5e-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="abe5e-133">**格式**：列分隔</span><span class="sxs-lookup"><span data-stu-id="abe5e-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="abe5e-134">按一下 hello**建立**按鈕 tooadd 這個來源和 tooverify 資料流分析可以成功連線 toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="abe5e-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="abe5e-135">在 hello**查詢**索引標籤上，取代 hello 下列中的 hello 目前的查詢。</span><span class="sxs-lookup"><span data-stu-id="abe5e-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="abe5e-136">取代 * [您的服務匯流排名稱] * 與您在步驟 3 中建立的 hello 輸出名稱。</span><span class="sxs-lookup"><span data-stu-id="abe5e-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="abe5e-137">建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="abe5e-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="abe5e-138">依照下列中的 hello.NET 一節建立的 Azure Redis 快取[如何 tooUse Azure Redis 快取][ use-rediscache]之前稱為 hello 區段***設定 hello 快取用戶端***。</span><span class="sxs-lookup"><span data-stu-id="abe5e-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="abe5e-139">完成後，您將具有新的 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="abe5e-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="abe5e-140">在下**所有設定**，選取**存取金鑰**並記下 hello***主要連接字串***。</span><span class="sxs-lookup"><span data-stu-id="abe5e-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="abe5e-142">建立 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="abe5e-142">Create an Azure Function</span></span>
<span data-ttu-id="abe5e-143">請遵循[建立您的第一個 Azure 函式][ functions-getstarted]教學課程 tooget 開始使用 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="abe5e-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="abe5e-144">如果您已經有 Azure 的函式就像 toouse，然後跳過[撰寫 tooRedis 快取](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="abe5e-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="abe5e-145">在 hello 入口網站選取應用程式服務從 hello 左側瀏覽，然後按一下 Azure 函式應用程式名稱 tooget toohello 函式的應用程式的網站。</span><span class="sxs-lookup"><span data-stu-id="abe5e-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="abe5e-146">![應用程式服務函式清單的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="abe5e-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="abe5e-147">按一下 [新增函式] > [ServiceBusQueueTrigger – C#]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="abe5e-148">Hello 下列欄位，請遵循這些指示：</span><span class="sxs-lookup"><span data-stu-id="abe5e-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="abe5e-149">**佇列名稱**： 名稱為您輸入當您建立 hello 佇列中的 hello 名稱相同的 hello[開始使用 Service Bus 佇列][ servicebus-getstarted] （非 hello service bus 的 hello 名稱）。</span><span class="sxs-lookup"><span data-stu-id="abe5e-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="abe5e-150">請確定您使用之輸出資料流分析連線的 toohello hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="abe5e-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="abe5e-151">**服務匯流排連接**︰選取 [加入連接字串]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="abe5e-152">toofind hello 連接字串中，移 toohello 傳統入口網站，選取**Service Bus**，hello 您所建立的服務匯流排和**連接資訊**在 hello 囉 」 畫面底部。</span><span class="sxs-lookup"><span data-stu-id="abe5e-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="abe5e-153">請確定您是在此頁面上的 hello 主畫面上。</span><span class="sxs-lookup"><span data-stu-id="abe5e-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="abe5e-154">複製並貼上 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="abe5e-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="abe5e-155">您可用 tooenter 任何連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="abe5e-155">Feel free tooenter any connection name.</span></span>
     
       ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="abe5e-157">**AccessRights**︰選擇 [管理]</span><span class="sxs-lookup"><span data-stu-id="abe5e-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="abe5e-158">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="abe5e-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="abe5e-159">寫入 tooRedis 快取</span><span class="sxs-lookup"><span data-stu-id="abe5e-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="abe5e-160">我們現在已經建立一個可從服務匯流排佇列進行讀取的 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="abe5e-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="abe5e-161">Toodo 剩下的就是使用我們的函式 toowrite 此資料 toohello Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="abe5e-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="abe5e-162">選取您新建**ServiceBusQueueTrigger**，然後按一下**函式應用程式設定**hello 最上層顯示右下角。</span><span class="sxs-lookup"><span data-stu-id="abe5e-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="abe5e-163">選取**移 tooApp 服務設定 > 設定 > 應用程式設定**</span><span class="sxs-lookup"><span data-stu-id="abe5e-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="abe5e-164">在 hello 連接字串區段，會建立 hello 中的名稱**名稱**> 一節。</span><span class="sxs-lookup"><span data-stu-id="abe5e-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="abe5e-165">貼上您在 hello 找到 hello 主要連接字串**建立 Redis 快取**逐步執行 hello**值**> 一節。</span><span class="sxs-lookup"><span data-stu-id="abe5e-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="abe5e-166">在 [SQL 資料庫]的位置選取 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="abe5e-167">按一下**儲存**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="abe5e-167">Click **Save** at hello top.</span></span>
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="abe5e-169">現在返回 toohello 應用程式服務設定，並選取**工具 > 應用程式服務編輯器 （預覽） > 上 > 移**。</span><span class="sxs-lookup"><span data-stu-id="abe5e-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="abe5e-171">在您選擇的編輯器，建立名為 JSON 檔案**project.json**與 hello 後面，並將它儲存 tooyour 本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="abe5e-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="abe5e-172">此檔案上傳至您的函式 (不 WWWROOT) hello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="abe5e-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="abe5e-173">您應該會看到名為**project.lock.json**自動出現，請確認該 hello Nuget"StackExchange.Redis"和"Newtonsoft.Json"封裝已匯入。</span><span class="sxs-lookup"><span data-stu-id="abe5e-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="abe5e-174">在 hello **run.csx**檔案時，請取代下列程式碼的 hello hello 預先產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="abe5e-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="abe5e-175">在 hello lazyConnection 函式，取代您在步驟 2 中建立的 hello 名稱"CONN NAME"**資料儲存到 hello Redis 快取**。</span><span class="sxs-lookup"><span data-stu-id="abe5e-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="abe5e-176">啟動 hello 資料流分析工作</span><span class="sxs-lookup"><span data-stu-id="abe5e-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="abe5e-177">啟動 hello telcodatagen.exe 應用程式。</span><span class="sxs-lookup"><span data-stu-id="abe5e-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="abe5e-178">hello 用法如下所示：````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="abe5e-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="abe5e-179">從 hello hello 入口網站中的資料流分析工作刀鋒視窗，按一下 **啟動**hello 頁面頂端的 hello。</span><span class="sxs-lookup"><span data-stu-id="abe5e-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![開始工作的螢幕擷取畫面](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="abe5e-181">在 hello**開始工作**刀鋒視窗中，選取**現在**然後按一下hello**啟動**在 hello 囉 」 畫面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="abe5e-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="abe5e-182">hello 作業狀態變更 tooStarting 後一些時間變更 tooRunning。</span><span class="sxs-lookup"><span data-stu-id="abe5e-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![開始工作時間範圍的螢幕擷取畫面](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="abe5e-184">執行解決方案並檢查結果</span><span class="sxs-lookup"><span data-stu-id="abe5e-184">Run solution and check results</span></span>
<span data-ttu-id="abe5e-185">返回 tooyour **ServiceBusQueueTrigger**頁面上，您現在應該會看到記錄陳述式。</span><span class="sxs-lookup"><span data-stu-id="abe5e-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="abe5e-186">這些記錄檔會顯示 hello 服務匯流排佇列，放入 hello 資料庫中取得的項目，提取出使用 hello 時間當做 hello 機碼 ！</span><span class="sxs-lookup"><span data-stu-id="abe5e-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="abe5e-187">tooverify 您資料的 Redis 快取中，移至 tooyour Redis 快取頁面 hello 新入口網站 (hello 前面所示[建立 Azure Redis 快取](#Create-an-Azure-Redis-Cache)步驟)，選取 [主控台]。</span><span class="sxs-lookup"><span data-stu-id="abe5e-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="abe5e-188">現在您可以撰寫 Redis 命令 tooconfirm 資料實際上位於 hello 快取。</span><span class="sxs-lookup"><span data-stu-id="abe5e-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Redis 主控台的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="abe5e-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abe5e-190">Next steps</span></span>
<span data-ttu-id="abe5e-191">我們很高興解 hello 新項目的 Azure 函式和資料流分析可以一起執行，我們希望這帶來新的可能性的。</span><span class="sxs-lookup"><span data-stu-id="abe5e-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="abe5e-192">如果您有任何意見反應上您想要接下來，則可以免費 toouse hello [Azure UserVoice 網站](https://feedback.azure.com/forums/270577-stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="abe5e-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="abe5e-193">如果您是新的 Microsoft Azure 時，我們邀請您 tootry 它編寫透過註冊[免費試用的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="abe5e-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="abe5e-194">如果您是新 tooStream 分析，則太邀請[建立第一個資料流分析工作](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="abe5e-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="abe5e-195">如果您需要任何協助或有任何問題，請在 [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 或 [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) 論壇中提出。</span><span class="sxs-lookup"><span data-stu-id="abe5e-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="abe5e-196">您也可以查看下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="abe5e-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="abe5e-197">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="abe5e-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="abe5e-198">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="abe5e-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="abe5e-199">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="abe5e-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="abe5e-200">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="abe5e-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="abe5e-201">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="abe5e-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="abe5e-202">如何 toomonitor Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="abe5e-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="abe5e-203">toostay 最新的所有 hello 最新消息和功能，請遵循[ @AzureStreaming ](https://twitter.com/AzureStreaming) Twitter 上。</span><span class="sxs-lookup"><span data-stu-id="abe5e-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
