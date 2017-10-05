---
title: "適用於 Azure Functions 的串流分析即時處理 | Microsoft Docs"
description: "了解如何使用連接到服務匯流排佇列的 Azure 函式，從串流分析工作的輸出填入 Azure Redis 快取。"
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
ms.openlocfilehash: ad14cc858ff513573e2718a26a9ab5c524e1adc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="282ba-104">如何使用 Azure Functions 在 Azure Redis 快取中儲存 Azure 串流分析的資料</span><span class="sxs-lookup"><span data-stu-id="282ba-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="282ba-105">Azure 串流分析可讓您快速開發及部署低成本的解決方案，即時獲取裝置、感應器、基礎結構與應用程式，或任何資料流的深入解析。</span><span class="sxs-lookup"><span data-stu-id="282ba-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="282ba-106">它可啟用不同的使用案例，例如即時管理與監視、命令與控制、詐騙偵測、Connected Cars 等等。</span><span class="sxs-lookup"><span data-stu-id="282ba-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="282ba-107">在許多類似情況下，您可能希望將 Azure 串流分析輸出的資料儲存到分散式資料存放區，例如 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="282ba-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="282ba-108">假設您是電信公司的員工。</span><span class="sxs-lookup"><span data-stu-id="282ba-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="282ba-109">您正在嘗試偵測 SIM 卡詐騙，並尋找於相同時間來自相同身分，卻位於不同地理位置的多個通話。</span><span class="sxs-lookup"><span data-stu-id="282ba-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="282ba-110">您的工作是將所有潛在的詐騙電話儲存在 Azure Redis 快取中。</span><span class="sxs-lookup"><span data-stu-id="282ba-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="282ba-111">在此部落格中，我們將提供如何輕鬆地完成此工作的指引。</span><span class="sxs-lookup"><span data-stu-id="282ba-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="282ba-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="282ba-112">Prerequisites</span></span>
<span data-ttu-id="282ba-113">完成 ASA 的[即時詐騙偵測][fraud-detection]逐步解說</span><span class="sxs-lookup"><span data-stu-id="282ba-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="282ba-114">架構概觀</span><span class="sxs-lookup"><span data-stu-id="282ba-114">Architecture Overview</span></span>
![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="282ba-116">如上圖所示，串流分析允許查詢串流輸入資料並將之傳送至輸出。</span><span class="sxs-lookup"><span data-stu-id="282ba-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="282ba-117">根據輸出，Azure Functions 可以接著觸發某些事件類型。</span><span class="sxs-lookup"><span data-stu-id="282ba-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="282ba-118">在此部落格中，我們會著重在此管線中 Azure Functions 的部分，若要更明確地說，則是觸發將詐騙資料儲存到快取的事件。</span><span class="sxs-lookup"><span data-stu-id="282ba-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="282ba-119">完成[即時詐騙偵測][fraud-detection]教學課程之後，您將會有已設定並正在執行的輸入 (事件中樞)、查詢，以及輸出 (Blob 儲存體)。</span><span class="sxs-lookup"><span data-stu-id="282ba-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="282ba-120">在此部落格中，我們將輸出改為使用「服務匯流排佇列」。</span><span class="sxs-lookup"><span data-stu-id="282ba-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="282ba-121">接下來，我們將一個 Azure 函式與這個佇列連接。</span><span class="sxs-lookup"><span data-stu-id="282ba-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="282ba-122">建立並連接服務匯流排佇列輸出</span><span class="sxs-lookup"><span data-stu-id="282ba-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="282ba-123">若要建立服務匯流排佇列，請遵循[開始使用服務匯流排佇列][servicebus-getstarted]中＜.NET＞一節的步驟 1 和 2。</span><span class="sxs-lookup"><span data-stu-id="282ba-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="282ba-124">現在讓我們將佇列連接到先前在詐騙偵測逐步解說中所建立的串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="282ba-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="282ba-125">在 Azure 入口網站中，移至工作的 [輸出] 刀鋒視窗，然後選取頁面頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="282ba-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![加入輸出](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="282ba-127">選擇 [服務匯流排佇列] 為 [接收]，並遵循螢幕上的指示。</span><span class="sxs-lookup"><span data-stu-id="282ba-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="282ba-128">請務必選擇您在[開始使用服務匯流排佇列][servicebus-getstarted]中建立的服務匯流排佇列命名空間。</span><span class="sxs-lookup"><span data-stu-id="282ba-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="282ba-129">當您完成時，請按一下「右鍵」。</span><span class="sxs-lookup"><span data-stu-id="282ba-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="282ba-130">指定下列值：</span><span class="sxs-lookup"><span data-stu-id="282ba-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="282ba-131">**事件序列化程式格式**：JSON</span><span class="sxs-lookup"><span data-stu-id="282ba-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="282ba-132">**編碼**：UTF8</span><span class="sxs-lookup"><span data-stu-id="282ba-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="282ba-133">**格式**：列分隔</span><span class="sxs-lookup"><span data-stu-id="282ba-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="282ba-134">按一下 [建立]  按鈕以新增這個來源，並確認串流分析可以成功連接到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="282ba-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="282ba-135">在 [查詢]  索引標籤上，以下列項目取代目前的查詢。</span><span class="sxs-lookup"><span data-stu-id="282ba-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="282ba-136">使用您在步驟 3 中所建立的輸出名稱取代 *[您的服務匯流排名稱]*。</span><span class="sxs-lookup"><span data-stu-id="282ba-136">Replace *[YOUR SERVICE BUS NAME] * with the output name you created in step 3.</span></span> 
   
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

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="282ba-137">建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="282ba-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="282ba-138">遵循[如何使用 Azure Redis 快取][use-rediscache]中的＜.NET＞一節到＜設定快取用戶端＞一節的內容，建立 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="282ba-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="282ba-139">完成後，您將具有新的 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="282ba-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="282ba-140">在 [所有設定] 底下，選取 [存取金鑰] 並記下 [主要連接字串] 的內容。</span><span class="sxs-lookup"><span data-stu-id="282ba-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![架構的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="282ba-142">建立 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="282ba-142">Create an Azure Function</span></span>
<span data-ttu-id="282ba-143">遵循[建立您的第一個 Azure 函式][functions-getstarted]教學課程以開始使用 Azure Functions。</span><span class="sxs-lookup"><span data-stu-id="282ba-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="282ba-144">如果您已經有想要使用的 Azure 函式，則請直接跳到 [寫入至 Redis 快取](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="282ba-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="282ba-145">在入口網站中，從左側導覽中選取 [應用程式服務]，然後按一下您的 Azure 函數應用程式名稱，以取得函式的應用程式網站。</span><span class="sxs-lookup"><span data-stu-id="282ba-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="282ba-146">![應用程式服務函式清單的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="282ba-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="282ba-147">按一下 [新增函式] > [ServiceBusQueueTrigger – C#]。</span><span class="sxs-lookup"><span data-stu-id="282ba-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="282ba-148">針對下列欄位，請遵循下列指示︰</span><span class="sxs-lookup"><span data-stu-id="282ba-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="282ba-149">**佇列名稱**：與您在[開始使用服務匯流排佇列][servicebus-getstarted]中建立佇列時所輸入的名稱相同 (不是服務匯流排的名稱)。</span><span class="sxs-lookup"><span data-stu-id="282ba-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="282ba-150">請確定您式使用連線到串流分析輸出的佇列。</span><span class="sxs-lookup"><span data-stu-id="282ba-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="282ba-151">**服務匯流排連接**︰選取 [加入連接字串]。</span><span class="sxs-lookup"><span data-stu-id="282ba-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="282ba-152">若要尋找連接字串，請移至傳統入口網站，依序選取 [服務匯流排]、您所建立的服務匯流排，以及畫面底部的 [連接資訊]。</span><span class="sxs-lookup"><span data-stu-id="282ba-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="282ba-153">請確定您是位於此頁面的主畫面上。</span><span class="sxs-lookup"><span data-stu-id="282ba-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="282ba-154">請複製並貼上連接字串。</span><span class="sxs-lookup"><span data-stu-id="282ba-154">Copy and paste the connection string.</span></span> <span data-ttu-id="282ba-155">請隨意輸入任何連接名稱。</span><span class="sxs-lookup"><span data-stu-id="282ba-155">Feel free to enter any connection name.</span></span>
     
       ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="282ba-157">**AccessRights**︰選擇 [管理]</span><span class="sxs-lookup"><span data-stu-id="282ba-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="282ba-158">按一下 [建立] </span><span class="sxs-lookup"><span data-stu-id="282ba-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="282ba-159">寫入至 Redis 快取</span><span class="sxs-lookup"><span data-stu-id="282ba-159">Writing to Redis Cache</span></span>
<span data-ttu-id="282ba-160">我們現在已經建立一個可從服務匯流排佇列進行讀取的 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="282ba-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="282ba-161">我們還需使用函式將此資料寫入 Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="282ba-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="282ba-162">選取您剛建立的 **ServiceBusQueueTrigger**，並按一下右上角的 [函式應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="282ba-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="282ba-163">選取 [移至 App Service 設定] > [設定] > [應用程式設定]</span><span class="sxs-lookup"><span data-stu-id="282ba-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="282ba-164">在 [連接字串] 區段中，於 [名稱]  區段中建立一個名稱。</span><span class="sxs-lookup"><span data-stu-id="282ba-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="282ba-165">在 [值] 區段中，貼上您在 [建立 Redis 快取] 步驟中找到的主要連接字串。</span><span class="sxs-lookup"><span data-stu-id="282ba-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="282ba-166">在 [SQL 資料庫]的位置選取 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="282ba-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="282ba-167">按一下頂端的 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="282ba-167">Click **Save** at the top.</span></span>
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="282ba-169">現在回到 [App Service 設定]，然後選取 [工具] > [App Service 編輯器 (預覽)] > [開啟] > [前往]。</span><span class="sxs-lookup"><span data-stu-id="282ba-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![服務匯流排連線的螢幕擷取畫面](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="282ba-171">在您選擇的編輯器中，使用下列項目建立名為 **project.json** 的 JSON 檔案，並將它儲存至本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="282ba-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
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
6. <span data-ttu-id="282ba-172">將此檔案上傳至您函式的根目錄 (不是 WWWROOT)。</span><span class="sxs-lookup"><span data-stu-id="282ba-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="282ba-173">您應該會看到名為 **project.lock.json** 的檔案自動顯示，確認 Nuget 封裝 "StackExchange.Redis" 和 "Newtonsoft.Json" 已經匯入。</span><span class="sxs-lookup"><span data-stu-id="282ba-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="282ba-174">在 **run.csx** 檔案中，使用下列程式碼取代預先產生的程式碼。</span><span class="sxs-lookup"><span data-stu-id="282ba-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="282ba-175">在 lazyConnection 函式中，使用您在 **將資料儲存至 Redis 快取**的步驟 2 中所建立的名稱取代 "CONN NAME"。</span><span class="sxs-lookup"><span data-stu-id="282ba-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
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

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="282ba-176">啟動串流分析工作</span><span class="sxs-lookup"><span data-stu-id="282ba-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="282ba-177">啟動 telcodatagen.exe 應用程式。</span><span class="sxs-lookup"><span data-stu-id="282ba-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="282ba-178">使用方式如下： ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="282ba-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="282ba-179">從入口網站中的 [串流分析工作] 刀鋒視窗中，按一下頁面頂端的 [啟動]  。</span><span class="sxs-lookup"><span data-stu-id="282ba-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![開始工作的螢幕擷取畫面](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="282ba-181">在顯示的 [開始工作] 刀鋒視窗中，選取 [立即] 然後按一下畫面底部的 [啟動] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="282ba-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="282ba-182">工作狀態會變更為 [啟動中]，稍後則會變更為 [執行中]。</span><span class="sxs-lookup"><span data-stu-id="282ba-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![開始工作時間範圍的螢幕擷取畫面](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="282ba-184">執行解決方案並檢查結果</span><span class="sxs-lookup"><span data-stu-id="282ba-184">Run solution and check results</span></span>
<span data-ttu-id="282ba-185">回到您的 **ServiceBusQueueTrigger** 頁面上，您現在應該會看到記錄陳述式。</span><span class="sxs-lookup"><span data-stu-id="282ba-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="282ba-186">這些記錄檔顯示您從服務匯流排佇列取得某些項目、將該項目放入資料庫，並使用時間做為索引鍵將該項目擷取出來！</span><span class="sxs-lookup"><span data-stu-id="282ba-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="282ba-187">若要確認您的資料位於 Redis 快取中，請移至新入口網站中的 Redis 快取頁面 (如先前在 [建立 Azure Redis 快取](#Create-an-Azure-Redis-Cache) 步驟中所示)，然後選取主控台。</span><span class="sxs-lookup"><span data-stu-id="282ba-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="282ba-188">您現在可以撰寫 Redis 命令以確認資料實際位於快取中。</span><span class="sxs-lookup"><span data-stu-id="282ba-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Redis 主控台的螢幕擷取畫面](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="282ba-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="282ba-190">Next steps</span></span>
<span data-ttu-id="282ba-191">我們對於 Azure Functions 及串流分析可以協力執行的新功能感到十分興奮，並希望這會為您帶來新的可能性。</span><span class="sxs-lookup"><span data-stu-id="282ba-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="282ba-192">如果您對自己所需要的功能有任何意見反應，歡迎使用 [Azure UserVoice 網站](https://feedback.azure.com/forums/270577-stream-analytics)。</span><span class="sxs-lookup"><span data-stu-id="282ba-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="282ba-193">如果您不熟悉 Microsoft Azure，我們邀請您透過註冊 [免費 Azure 試用帳戶](https://azure.microsoft.com/pricing/free-trial/)來親自嘗試。</span><span class="sxs-lookup"><span data-stu-id="282ba-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="282ba-194">如果您不熟悉串流分析，我們邀請您 [建立您的第一個串流分析工作](stream-analytics-create-a-job.md)。</span><span class="sxs-lookup"><span data-stu-id="282ba-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="282ba-195">如果您需要任何協助或有任何問題，請在 [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) 或 [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) 論壇中提出。</span><span class="sxs-lookup"><span data-stu-id="282ba-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="282ba-196">您也可以查看下列資源︰</span><span class="sxs-lookup"><span data-stu-id="282ba-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="282ba-197">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="282ba-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="282ba-198">Azure Functions C# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="282ba-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="282ba-199">Azure Functions F# 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="282ba-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="282ba-200">Azure Functions NodeJS 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="282ba-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="282ba-201">Azure Functions 觸發程序和繫結</span><span class="sxs-lookup"><span data-stu-id="282ba-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="282ba-202">如何監視 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="282ba-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="282ba-203">若要隨時掌握所有最新消息及功能，請在 Twitter 上追蹤 [@AzureStreaming](https://twitter.com/AzureStreaming) 。</span><span class="sxs-lookup"><span data-stu-id="282ba-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
