# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a><span data-ttu-id="7002e-101">開始使用 Azure 串流分析：即時詐騙偵測</span><span class="sxs-lookup"><span data-stu-id="7002e-101">Get started using Azure Stream Analytics: Real-time fraud detection</span></span>

<span data-ttu-id="7002e-102">本教學課程提供端對端實例的方式 toouse Azure Stream Analytics。</span><span class="sxs-lookup"><span data-stu-id="7002e-102">This tutorial provides an end-to-end illustration of how toouse Azure Stream Analytics.</span></span> <span data-ttu-id="7002e-103">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="7002e-103">You learn how to:</span></span> 

* <span data-ttu-id="7002e-104">將串流事件帶入 Azure 事件中樞的執行個體中。</span><span class="sxs-lookup"><span data-stu-id="7002e-104">Bring streaming events into an instance of Azure Event Hubs.</span></span> <span data-ttu-id="7002e-105">在本教學課程中，您將使用我們提供的應用程式來模擬行動電話中繼資料記錄流。</span><span class="sxs-lookup"><span data-stu-id="7002e-105">In this tutorial, you'll use an app that we provide that simulates a stream of mobile-phone metadata records.</span></span>

* <span data-ttu-id="7002e-106">撰寫類似 SQL 的串流分析查詢 tootransform 資料、 彙總資訊或尋求模式。</span><span class="sxs-lookup"><span data-stu-id="7002e-106">Write SQL-like Stream Analytics queries tootransform data, aggregating information or looking for patterns.</span></span> <span data-ttu-id="7002e-107">您會看到 toouse 查詢 tooexamine hello 內送資料流的方式，並尋找可能是詐騙的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7002e-107">You will see how toouse a query tooexamine hello incoming stream and look for calls that might be fraudulent.</span></span>

* <span data-ttu-id="7002e-108">傳送 hello 結果 tooan 輸出接收 （儲存體），您可以分析其他深入資訊。</span><span class="sxs-lookup"><span data-stu-id="7002e-108">Send hello results tooan output sink (storage) that you can analyze for additional insights.</span></span> <span data-ttu-id="7002e-109">在此情況下，您將會傳送 hello 可疑呼叫資料 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="7002e-109">In this case, you'll send hello suspicious call data tooAzure Blob storage.</span></span>

<span data-ttu-id="7002e-110">在本教學課程中，我們使用電話資料為基礎的即時詐騙偵測 hello 的範例。</span><span class="sxs-lookup"><span data-stu-id="7002e-110">In  this tutorial, we use hello example of real-time fraud detection based on phone-call data.</span></span> <span data-ttu-id="7002e-111">但是，我們將說明 hello 技術也適用於其他類型的詐騙偵測，例如信用卡詐騙或身分識別盜用。</span><span class="sxs-lookup"><span data-stu-id="7002e-111">But hello technique we illustrate is also suited for other types of fraud detection, such as credit card fraud or identity theft.</span></span> 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a><span data-ttu-id="7002e-112">案例：即時偵測電信與 SIM 詐騙</span><span class="sxs-lookup"><span data-stu-id="7002e-112">Scenario: Telecommunications and SIM fraud detection in real time</span></span>

<span data-ttu-id="7002e-113">電信公司有大量的資料都是來電。</span><span class="sxs-lookup"><span data-stu-id="7002e-113">A telecommunications company has a large volume of data for incoming calls.</span></span> <span data-ttu-id="7002e-114">hello 公司希望有詐騙 toodetect 呼叫即時，讓他們可以通知客戶即將發生或關閉特定數目的服務。</span><span class="sxs-lookup"><span data-stu-id="7002e-114">hello company wants toodetect fraudulent calls in real time so that they can notify customers or shut down service for a specific number.</span></span> <span data-ttu-id="7002e-115">一種類型的 SIM 詐騙牽涉到多個的 hello 呼叫 hello 周圍的相同身分識別相同時間但在不同地理位置。</span><span class="sxs-lookup"><span data-stu-id="7002e-115">One type of SIM fraud involves multiple calls from hello same identity around hello same time but in geographically different locations.</span></span> <span data-ttu-id="7002e-116">toodetect 詐騙，這種 hello 公司需求 tooexamine 傳入電話記錄和尋找特定的模式，在此情況下，對呼叫進行 hello 不同國家/地區中相同的時間。</span><span class="sxs-lookup"><span data-stu-id="7002e-116">toodetect this type of fraud, hello company needs tooexamine incoming phone records and look for specific patterns—in this case, for calls made around hello same time in different countries.</span></span> <span data-ttu-id="7002e-117">歸類到此類別的任何電話記錄會寫入 toostorage 進行後續分析。</span><span class="sxs-lookup"><span data-stu-id="7002e-117">Any phone records that fall into this category are written toostorage for subsequent analysis.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7002e-118">必要條件</span><span class="sxs-lookup"><span data-stu-id="7002e-118">Prerequisites</span></span>

<span data-ttu-id="7002e-119">在本教學課程中，您會透過用戶端應用程式來產生範例通話中繼資料，以模擬通話資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-119">In this tutorial, you'll simulate phone-call data by using a client app that generates sample phone call metadata.</span></span> <span data-ttu-id="7002e-120">有些 hello 應用程式的 hello 記錄產生看起來像詐騙的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7002e-120">Some of hello records that hello app produces look like fraudulent calls.</span></span> 

<span data-ttu-id="7002e-121">開始之前，請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7002e-121">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="7002e-122">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7002e-122">An Azure account.</span></span>
* <span data-ttu-id="7002e-123">hello 呼叫事件產生器應用程式。</span><span class="sxs-lookup"><span data-stu-id="7002e-123">hello call-event generator app.</span></span> <span data-ttu-id="7002e-124">您可以取得此下載 hello [TelcoGenerator.zip 檔案](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip)從 Microsoft 下載中心 hello。</span><span class="sxs-lookup"><span data-stu-id="7002e-124">You can get this by downloading hello [TelcoGenerator.zip file](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) from hello Microsoft Download Center.</span></span> <span data-ttu-id="7002e-125">將此套件解壓縮至電腦上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7002e-125">Unzip this package into a folder on your computer.</span></span> <span data-ttu-id="7002e-126">如果您希望 toosee hello 原始程式碼和偵錯工具中執行的 hello 應用程式，您可以取得 hello 應用程式原始程式碼，從[GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)。</span><span class="sxs-lookup"><span data-stu-id="7002e-126">If you want toosee hello source code and run hello app in a debugger, you can get hello app source code from [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="7002e-127">Windows 可能會封鎖 hello 下載.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="7002e-127">Windows might block hello downloaded .zip file.</span></span> <span data-ttu-id="7002e-128">如果您無法將它解壓縮，hello 檔案上按一下滑鼠右鍵，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="7002e-128">If you can't unzip it, right-click hello file and select **Properties**.</span></span> <span data-ttu-id="7002e-129">如果您看到 hello"這個檔案來自另一部電腦，可能會封鎖的 toohelp 保護您的電腦 」 的訊息、 選取 hello**解除封鎖**選項，然後再按一下**套用**。</span><span class="sxs-lookup"><span data-stu-id="7002e-129">If you see hello "This file came from another computer and might be blocked toohelp protect this computer" message, select hello **Unblock** option and then click **Apply**.</span></span>

<span data-ttu-id="7002e-130">如果您想 tooexamine hello hello 串流分析工作結果，您也需要工具來檢視 Azure Blob 儲存體容器的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="7002e-130">If you want tooexamine hello results of hello Streaming Analytics job, you also need a tool for viewing hello contents of a Azure Blob Storage container.</span></span> <span data-ttu-id="7002e-131">如果您使用 Visual Studio，您可以使用 [Azure Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 或 [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer)。</span><span class="sxs-lookup"><span data-stu-id="7002e-131">If you use Visual Studio, you can use [Azure Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) or [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer).</span></span> <span data-ttu-id="7002e-132">或者，您可以安裝獨立工具，例如 [Azure 儲存體總管](http://storageexplorer.com/)或 [Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)。</span><span class="sxs-lookup"><span data-stu-id="7002e-132">Alternatively, you can install standalone tools like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

## <a name="create-an-azure-event-hubs-tooingest-events"></a><span data-ttu-id="7002e-133">建立 Azure 事件中心 tooingest 事件</span><span class="sxs-lookup"><span data-stu-id="7002e-133">Create an Azure event hubs tooingest events</span></span>

<span data-ttu-id="7002e-134">tooanalyze 資料流，您*內嵌*到 Azure。</span><span class="sxs-lookup"><span data-stu-id="7002e-134">tooanalyze a data stream, you *ingest* it into Azure.</span></span> <span data-ttu-id="7002e-135">典型 tooingest 資料是 toouse [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)，可讓您內嵌的數百萬個每秒的事件，然後處理以及儲存 hello 事件資訊。</span><span class="sxs-lookup"><span data-stu-id="7002e-135">A typical way tooingest data is toouse [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md), which lets you ingest millions of events per second and then process and store hello event information.</span></span> <span data-ttu-id="7002e-136">此教學課程中，您會建立事件中樞時，而擁有 hello 呼叫事件產生器應用程式傳送呼叫資料 toothat 事件中心。</span><span class="sxs-lookup"><span data-stu-id="7002e-136">For this tutorial, you create an event hub and then have hello call-event generator app send call data toothat event hub.</span></span> <span data-ttu-id="7002e-137">如需有關事件中心的詳細資訊，請參閱 hello [Azure 服務匯流排文件](https://docs.microsoft.com/en-us/azure/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="7002e-137">For more about event hubs, see hello [Azure Service Bus documentation](https://docs.microsoft.com/en-us/azure/service-bus/).</span></span>

>[!NOTE]
><span data-ttu-id="7002e-138">如需此程序更詳細的版本，請參閱[建立事件中樞命名空間，並使用您建立事件中樞 hello Azure 入口網站](../event-hubs/event-hubs-create.md)。</span><span class="sxs-lookup"><span data-stu-id="7002e-138">For a more detailed version of this procedure, see [Create an Event Hubs namespace and an event hub using hello Azure portal](../event-hubs/event-hubs-create.md).</span></span> 

### <a name="create-a-namespace-and-event-hub"></a><span data-ttu-id="7002e-139">建立命名空間和事件中樞</span><span class="sxs-lookup"><span data-stu-id="7002e-139">Create a namespace and event hub</span></span>
<span data-ttu-id="7002e-140">在此程序，您先建立事件中樞命名空間中，並將事件中樞 toothat namepsace。</span><span class="sxs-lookup"><span data-stu-id="7002e-140">In this procedure, you first create an event hub namespace, and then you add an event hub toothat namepsace.</span></span> <span data-ttu-id="7002e-141">事件中樞命名空間用 toologically 群組相關的事件匯流排執行個體。</span><span class="sxs-lookup"><span data-stu-id="7002e-141">Event hub namespaces are used toologically group related event bus instances.</span></span> 

1. <span data-ttu-id="7002e-142">登入 hello Azure 入口網站並按一下**新增** > **物聯網** > **事件中心**。</span><span class="sxs-lookup"><span data-stu-id="7002e-142">Log  into hello Azure portal and click **New** > **Internet of Things** > **Event Hub**.</span></span> 

2. <span data-ttu-id="7002e-143">在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱，例如`<yourname>-eh-ns-demo`。</span><span class="sxs-lookup"><span data-stu-id="7002e-143">In hello **Create namespace** blade, enter a namespace name such as `<yourname>-eh-ns-demo`.</span></span> <span data-ttu-id="7002e-144">您可以使用任何名稱，如 hello 命名空間，但是 hello 名稱必須是有效的 URL，而且它必須是唯一的 Azure。</span><span class="sxs-lookup"><span data-stu-id="7002e-144">You can use any name for hello namespace, but hello name must be valid for a URL and it must be unique across Azure.</span></span> 
    
3. <span data-ttu-id="7002e-145">選取訂用帳戶並建立或選擇資源群組，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7002e-145">Select a subscription and create or choose a resource group , then click **Create**.</span></span> 

    ![建立事件中樞命名空間](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. <span data-ttu-id="7002e-147">當部署完成 hello 命名空間時，尋找 hello 事件中樞命名空間清單中的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="7002e-147">When hello namespace has finished deploying, find hello event hub namespace in your list of Azure resources.</span></span> 

5. <span data-ttu-id="7002e-148">按一下 hello 新命名空間，然後在 hello 命名空間刀鋒視窗中，按一下 **+&nbsp;事件中心**。</span><span class="sxs-lookup"><span data-stu-id="7002e-148">Click hello new namespace, and in hello namespace blade, click **+&nbsp;Event Hub**.</span></span> 

    ![<span data-ttu-id="7002e-149">hello 新增事件中樞按鈕建立新的事件中樞</span><span class="sxs-lookup"><span data-stu-id="7002e-149">hello Add Event Hub button for creating a new event hub</span></span> ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. <span data-ttu-id="7002e-150">名稱資料行 hello 新的事件中樞`sa-eh-frauddetection-demo`。</span><span class="sxs-lookup"><span data-stu-id="7002e-150">Name hello new event hub `sa-eh-frauddetection-demo`.</span></span> <span data-ttu-id="7002e-151">您可以使用不同的名稱。</span><span class="sxs-lookup"><span data-stu-id="7002e-151">You can use a different name.</span></span> <span data-ttu-id="7002e-152">如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7002e-152">If you do, make a note of it, because you need hello name later.</span></span> <span data-ttu-id="7002e-153">您不需要 tooset 任何其他選項 hello 事件中樞現在。</span><span class="sxs-lookup"><span data-stu-id="7002e-153">You don't need tooset any other options for hello event hub right now.</span></span>

    ![建立新事件中樞的刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. <span data-ttu-id="7002e-155">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-155">Click **Create**.</span></span>
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a><span data-ttu-id="7002e-156">授與存取 toohello 事件中樞，並取得連接字串</span><span class="sxs-lookup"><span data-stu-id="7002e-156">Grant access toohello event hub and get a connection string</span></span>

<span data-ttu-id="7002e-157">處理程序可以傳送資料 tooan 事件中心之前，hello 事件中心必須要有原則，可讓適當的存取權。</span><span class="sxs-lookup"><span data-stu-id="7002e-157">Before a process can send data tooan event hub, hello event hub must have a policy that allows appropriate access.</span></span> <span data-ttu-id="7002e-158">hello 存取原則會產生包含授權資訊的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-158">hello access policy produces a connection string that includes authorization information.</span></span>

1.  <span data-ttu-id="7002e-159">在 hello 事件命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下新的事件中樞的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7002e-159">In hello event namespace blade, click **Event Hubs** and then click hello name of your new event hub.</span></span>

2.  <span data-ttu-id="7002e-160">在 hello 事件中樞刀鋒視窗中，按一下 **共用存取原則**，然後按一下  **+&nbsp;新增**。</span><span class="sxs-lookup"><span data-stu-id="7002e-160">In hello event hub blade, click **Shared access policies** and then click **+&nbsp;Add**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7002e-161">請確定您正在使用 hello 事件中心不 hello 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="7002e-161">Make sure you're working with hello event hub, not hello event hub namespace.</span></span>

3.  <span data-ttu-id="7002e-162">新增名為 `sa-policy-manage-demo` 的原則，然後在 [宣告] 中，選取 [管理]。</span><span class="sxs-lookup"><span data-stu-id="7002e-162">Add a policy named `sa-policy-manage-demo` and for **Claim**, select **Manage**.</span></span>

    ![建立新事件中樞存取原則的刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  <span data-ttu-id="7002e-164">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-164">Click **Create**.</span></span>

5.  <span data-ttu-id="7002e-165">Hello 原則已部署之後，請按一下它在 hello 清單中的共用的存取原則。</span><span class="sxs-lookup"><span data-stu-id="7002e-165">After hello policy has been deployed, click it in hello list of shared access policies.</span></span>

6.  <span data-ttu-id="7002e-166">尋找 hello 方塊標示為**連接字串-主索引鍵**按一下 hello 複製按鈕下一步 toohello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-166">Find hello box labeled **CONNECTION STRING-PRIMARY KEY** and click hello copy button next toohello connection string.</span></span> 
    
    ![複製 hello 主要連接字串索引鍵與 hello 存取原則](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  <span data-ttu-id="7002e-168">貼入文字編輯器中的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-168">Paste hello connection string into a text editor.</span></span> <span data-ttu-id="7002e-169">Hello 下一節中，進行一些稍微修改 tooit 之後，您需要開啟這個連接字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-169">You need this connection string for hello next section, after you make some small edits tooit.</span></span>

    <span data-ttu-id="7002e-170">hello 連接字串看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="7002e-170">hello connection string looks like this:</span></span>

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    <span data-ttu-id="7002e-171">請注意 hello 連接字串包含多個索引鍵-值組，並以分號分隔： `Endpoint`， `SharedAccessKeyName`， `SharedAccessKey`，和`EntityPath`。</span><span class="sxs-lookup"><span data-stu-id="7002e-171">Notice that hello connection string contains multiple key-value pairs, separated with semicolons: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, and `EntityPath`.</span></span>  

## <a name="configure-and-start-hello-event-generator-application"></a><span data-ttu-id="7002e-172">設定並啟動 hello 事件產生器應用程式</span><span class="sxs-lookup"><span data-stu-id="7002e-172">Configure and start hello event generator application</span></span>

<span data-ttu-id="7002e-173">開始 hello TelcoGenerator 應用程式之前，您設定它，讓它會將傳送您剛才建立的呼叫記錄 toohello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="7002e-173">Before you start hello TelcoGenerator app, you configure it so that it will send call records toohello event hub you just created.</span></span>

### <a name="configure-hello-telcogeneratorapp"></a><span data-ttu-id="7002e-174">設定 hello TelcoGeneratorapp</span><span class="sxs-lookup"><span data-stu-id="7002e-174">Configure hello TelcoGeneratorapp</span></span>

1.  <span data-ttu-id="7002e-175">在您用來複製 hello 連接字串 hello 編輯器中，記下 hello`EntityPath`值，然後再移除 hello`EntityPath`組 （別忘了在它之前的 tooremove hello 分號）。</span><span class="sxs-lookup"><span data-stu-id="7002e-175">In hello editor where you copied hello connection string, make a note of hello `EntityPath` value, and then remove hello `EntityPath` pair (don't forget tooremove hello semicolon that precedes it).</span></span> 

2.  <span data-ttu-id="7002e-176">在您解壓縮 hello TelcoGenerator.zip 檔案 hello 資料夾中，開啟 hello telcodatagen.exe.config 檔案在編輯器中。</span><span class="sxs-lookup"><span data-stu-id="7002e-176">In hello folder where you unzipped hello TelcoGenerator.zip file, open hello telcodatagen.exe.config file in an editor.</span></span> <span data-ttu-id="7002e-177">（沒有一個以上的.config 檔案，因此請確定您開啟 hello 右移一個）。</span><span class="sxs-lookup"><span data-stu-id="7002e-177">(There is more than one .config file, so be sure that you open hello right one.)</span></span>

3.  <span data-ttu-id="7002e-178">在 hello`<appSettings>`項目，執行這項操作：</span><span class="sxs-lookup"><span data-stu-id="7002e-178">In hello `<appSettings>` element, do this:</span></span>

    * <span data-ttu-id="7002e-179">設定 hello hello 值`EventHubName`金鑰 toohello 事件中樞名稱 （也就是 toohello 值 hello 實體路徑）。</span><span class="sxs-lookup"><span data-stu-id="7002e-179">Set hello value of hello `EventHubName` key toohello event hub name (that is, toohello value of hello entity path).</span></span>
    * <span data-ttu-id="7002e-180">設定 hello hello 值`Microsoft.ServiceBus.ConnectionString`金鑰 toohello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-180">Set hello value of hello `Microsoft.ServiceBus.ConnectionString` key toohello connection string.</span></span> 

    <span data-ttu-id="7002e-181">hello`<appSettings>`區段看起來像下列範例中的 hello。</span><span class="sxs-lookup"><span data-stu-id="7002e-181">hello `<appSettings>` section will look like hello following example.</span></span> <span data-ttu-id="7002e-182">（為了清楚起見，我們包裝 hello 行，而且移除某些字元 hello 授權權杖。）</span><span class="sxs-lookup"><span data-stu-id="7002e-182">(For clarity, we wrapped hello lines and removed some characters from hello authorization token.)</span></span>

    ![TelcoGenerator 顯示 hello 事件中樞的名稱和連接字串的應用程式組態檔](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  <span data-ttu-id="7002e-184">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7002e-184">Save hello file.</span></span> 

### <a name="start-hello-app"></a><span data-ttu-id="7002e-185">啟動 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="7002e-185">Start hello app</span></span>
1.  <span data-ttu-id="7002e-186">開啟命令視窗，並變更 toohello hello TelcoGenerator 應用程式解壓縮所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7002e-186">Open a command window and change toohello folder where hello TelcoGenerator app is unzipped.</span></span>
2.  <span data-ttu-id="7002e-187">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="7002e-187">Enter hello following command:</span></span>

        telcodatagen.exe 1000 .2 2

    <span data-ttu-id="7002e-188">hello 參數如下：</span><span class="sxs-lookup"><span data-stu-id="7002e-188">hello parameters are:</span></span> 

    * <span data-ttu-id="7002e-189">每小時的 CDR 數目。</span><span class="sxs-lookup"><span data-stu-id="7002e-189">Number of CDRs per hour.</span></span> 
    * <span data-ttu-id="7002e-190">SIM 卡詐騙機率： 頻率，以百分比表示的所有呼叫，該 hello 應用程式應該模擬的詐騙的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7002e-190">SIM Card Fraud Probability: How often, as a percentage of all calls, that hello app should simulate a fraudulent call.</span></span> <span data-ttu-id="7002e-191">hello 值.2 表示大約 20%的記錄 hello 呼叫看起來詐騙。</span><span class="sxs-lookup"><span data-stu-id="7002e-191">hello value .2 means that about 20% of hello call records will look fraudulent.</span></span>
    * <span data-ttu-id="7002e-192">持續時間 (小時)。</span><span class="sxs-lookup"><span data-stu-id="7002e-192">Duration in hours.</span></span> <span data-ttu-id="7002e-193">hello 的小時數 hello 應用程式應該執行。</span><span class="sxs-lookup"><span data-stu-id="7002e-193">hello number of hours that hello app should run.</span></span> <span data-ttu-id="7002e-194">您也可以停止 hello 應用程式隨時在 hello 命令列中按下 Ctrl + C。</span><span class="sxs-lookup"><span data-stu-id="7002e-194">You can also stop hello app any time by pressing Ctrl+C at hello command line.</span></span>

    <span data-ttu-id="7002e-195">幾秒之後，hello 應用程式會啟動 hello 螢幕上顯示通話記錄，因為它會傳送它們 toohello 事件中心。</span><span class="sxs-lookup"><span data-stu-id="7002e-195">After a few seconds, hello app starts displaying phone call records on hello screen as it sends them toohello event hub.</span></span>

<span data-ttu-id="7002e-196">您將使用此即時詐騙偵測應用程式中的 hello 索引鍵欄位有些 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7002e-196">Some of hello key fields that you will be using in this real-time fraud detection application are hello following:</span></span>

|<span data-ttu-id="7002e-197">**記錄**</span><span class="sxs-lookup"><span data-stu-id="7002e-197">**Record**</span></span>|<span data-ttu-id="7002e-198">**定義**</span><span class="sxs-lookup"><span data-stu-id="7002e-198">**Definition**</span></span>|
|----------|--------------|
|`CallrecTime`|<span data-ttu-id="7002e-199">hello hello 呼叫所花費的時間戳記的開始時間。</span><span class="sxs-lookup"><span data-stu-id="7002e-199">hello timestamp for hello call start time.</span></span> |
|`SwitchNum`|<span data-ttu-id="7002e-200">hello 電話交換機用 tooconnect hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="7002e-200">hello telephone switch used tooconnect hello call.</span></span> <span data-ttu-id="7002e-201">例如，hello 參數會是代表 hello 國家/地區 （US、 中國、 英國、 德國或澳洲） 的字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-201">For this example, hello switches are strings that represent hello country of origin (US, China, UK, Germany, or Australia).</span></span> |
|`CallingNum`|<span data-ttu-id="7002e-202">hello hello 呼叫端的電話號碼。</span><span class="sxs-lookup"><span data-stu-id="7002e-202">hello phone number of hello caller.</span></span> |
|`CallingIMSI`|<span data-ttu-id="7002e-203">hello 國際行動用戶識別碼 (IMSI)。</span><span class="sxs-lookup"><span data-stu-id="7002e-203">hello International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="7002e-204">這是 hello hello 呼叫端的唯一識別項。</span><span class="sxs-lookup"><span data-stu-id="7002e-204">This is hello Unique identifier of hello caller.</span></span> |
|`CalledNum`|<span data-ttu-id="7002e-205">hello hello 呼叫收件者電話號碼。</span><span class="sxs-lookup"><span data-stu-id="7002e-205">hello phone number of hello call recipient.</span></span> |
|`CalledIMSI`|<span data-ttu-id="7002e-206">國際行動用戶識別碼 (IMSI)。</span><span class="sxs-lookup"><span data-stu-id="7002e-206">International Mobile Subscriber Identity (IMSI).</span></span> <span data-ttu-id="7002e-207">這是 hello hello 呼叫收件者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="7002e-207">This is hello unique identifier of hello call recipient.</span></span> |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a><span data-ttu-id="7002e-208">建立串流資料的資料流分析工作 toomanage</span><span class="sxs-lookup"><span data-stu-id="7002e-208">Create a Stream Analytics job toomanage streaming data</span></span>

<span data-ttu-id="7002e-209">既然已取得通話事件的資料流，您可以開始設定串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="7002e-209">Now that you have a stream of call events, you can set up a Stream Analytics job.</span></span> <span data-ttu-id="7002e-210">hello 作業會從您設定的 hello 事件中心讀取資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-210">hello job will read data from hello event hub that you set up.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="7002e-211">建立 hello 作業</span><span class="sxs-lookup"><span data-stu-id="7002e-211">Create hello job</span></span> 

1. <span data-ttu-id="7002e-212">在 hello Azure 入口網站，按一下 **新增** > **物聯網** > **資料流分析工作**。</span><span class="sxs-lookup"><span data-stu-id="7002e-212">In hello Azure portal, click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>

2. <span data-ttu-id="7002e-213">名稱 hello 工作`sa_frauddetection_job_demo`，指定的訂用帳戶、 資源群組和位置。</span><span class="sxs-lookup"><span data-stu-id="7002e-213">Name hello job `sa_frauddetection_job_demo`, specify a subscription, resource group, and location.</span></span>

    <span data-ttu-id="7002e-214">它是個不錯的主意 tooplace hello 作業和 hello 事件中樞 hello，以免付出 tootransfer 資料區域之間的最佳效能，所以相同的區域。</span><span class="sxs-lookup"><span data-stu-id="7002e-214">It's a good idea tooplace hello job and hello event hub in hello same region for best performance and so that you don't pay tootransfer data between regions.</span></span>

    ![建立新的串流分析作業](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. <span data-ttu-id="7002e-216">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-216">Click **Create**.</span></span>

    <span data-ttu-id="7002e-217">建立 hello 工作，而 hello 入口網站會顯示工作詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-217">hello job is created and hello portal displays job details.</span></span> <span data-ttu-id="7002e-218">執行任何動作正在執行，不過，您有 tooconfigure hello 工作，才能啟動。</span><span class="sxs-lookup"><span data-stu-id="7002e-218">Nothing is running yet, though—you have tooconfigure hello job before it can be started.</span></span>

### <a name="configure-job-input"></a><span data-ttu-id="7002e-219">設定作業輸入</span><span class="sxs-lookup"><span data-stu-id="7002e-219">Configure job input</span></span>

1. <span data-ttu-id="7002e-220">在 hello 儀表板或 hello**所有資源**刀鋒視窗中，尋找並選取 hello`sa_frauddetection_job_demo`資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7002e-220">In hello dashboard or hello **All resources** blade, find and select hello `sa_frauddetection_job_demo` Stream Analytics job.</span></span> 
2. <span data-ttu-id="7002e-221">在 hello**作業拓撲**區段 hello 資料流分析工作刀鋒視窗中，按一下 hello**輸入**方塊。</span><span class="sxs-lookup"><span data-stu-id="7002e-221">In hello **Job Topology** section of hello Stream Analytics job blade, click hello **Input** box.</span></span>

    ![在拓撲 hello 串流分析工作刀鋒視窗中的輸入的方塊](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. <span data-ttu-id="7002e-223">按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：</span><span class="sxs-lookup"><span data-stu-id="7002e-223">Click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="7002e-224">**輸入的別名**： 使用 hello 名稱`CallStream`。</span><span class="sxs-lookup"><span data-stu-id="7002e-224">**Input alias**: Use hello name `CallStream`.</span></span> <span data-ttu-id="7002e-225">如果使用不同的名稱，請記下來，因為稍後需要用到。</span><span class="sxs-lookup"><span data-stu-id="7002e-225">If you use a different name, make a note of it because you'll need it later.</span></span>
    * <span data-ttu-id="7002e-226">**來源類型**：選取 [資料流]。</span><span class="sxs-lookup"><span data-stu-id="7002e-226">**Source type**: Select **Data stream**.</span></span> <span data-ttu-id="7002e-227">(**參考資料**參考 toostatic 查閱資料，您將不會在本教學課程中使用。)</span><span class="sxs-lookup"><span data-stu-id="7002e-227">(**Reference data** refers toostatic lookup data, which you won't use in this tutorial.)</span></span>
    * <span data-ttu-id="7002e-228">**來源**：選取 [事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="7002e-228">**Source**: Select **Event hub**.</span></span>
    * <span data-ttu-id="7002e-229">**匯入選項**：選取 [使用目前訂用帳戶的事件中樞]。</span><span class="sxs-lookup"><span data-stu-id="7002e-229">**Import option**: Select **Use event hub from current subscription**.</span></span> 
    * <span data-ttu-id="7002e-230">**服務匯流排命名空間**： 選取 hello 事件中樞命名空間您稍早建立 (`<yourname>-eh-ns-demo`)。</span><span class="sxs-lookup"><span data-stu-id="7002e-230">**Service bus namespace**: Select hello event hub namespace that you created earlier (`<yourname>-eh-ns-demo`).</span></span>
    * <span data-ttu-id="7002e-231">**事件中心**: hello 選取您稍早建立的事件中心 (`sa-eh-frauddetection-demo`)。</span><span class="sxs-lookup"><span data-stu-id="7002e-231">**Event hub**: Select hello event hub that you created earlier (`sa-eh-frauddetection-demo`).</span></span>
    * <span data-ttu-id="7002e-232">**事件中樞原則名稱**： 選取您稍早建立的 hello 存取原則 (`sa-policy-manage-demo`)。</span><span class="sxs-lookup"><span data-stu-id="7002e-232">**Event hub policy name**: Select hello access policy that you created earlier (`sa-policy-manage-demo`).</span></span>

    ![建立串流分析作業的新輸入](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="7002e-234">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-234">Click **Create**.</span></span>

## <a name="create-queries-tootransform-real-time-data"></a><span data-ttu-id="7002e-235">建立查詢 tootransform 即時資料</span><span class="sxs-lookup"><span data-stu-id="7002e-235">Create queries tootransform real-time data</span></span>

<span data-ttu-id="7002e-236">此時，您必須設定 tooread 內送資料流資料流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7002e-236">At this point, you have a Stream Analytics job set up tooread an incoming data stream.</span></span> <span data-ttu-id="7002e-237">hello 下一個步驟是 toocreate 分析即時 hello 資料的轉換。</span><span class="sxs-lookup"><span data-stu-id="7002e-237">hello next step is toocreate a transformation that analyzes hello data in real time.</span></span> <span data-ttu-id="7002e-238">做法是建立查詢。</span><span class="sxs-lookup"><span data-stu-id="7002e-238">You do this by creating a query.</span></span> <span data-ttu-id="7002e-239">串流分析支援用來說明轉換的簡單、宣告式查詢模型，以供即時處理。</span><span class="sxs-lookup"><span data-stu-id="7002e-239">Stream Analytics supports a simple, declarative query model that describes transformations for real-time processing.</span></span> <span data-ttu-id="7002e-240">hello 查詢使用具有某些延伸模組特定 toostream 分析類似 SQL 的語言。</span><span class="sxs-lookup"><span data-stu-id="7002e-240">hello queries use a SQL-like language that has some extensions specific toostream analytics.</span></span> 

<span data-ttu-id="7002e-241">非常簡單的查詢可能會直接讀取所有 hello 內送資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-241">A very simple query might simply read all hello incoming data.</span></span> <span data-ttu-id="7002e-242">不過，您通常會建立查詢的特定資料或 hello 資料中關聯性的查詢。</span><span class="sxs-lookup"><span data-stu-id="7002e-242">However, you often create queries that look for specific data or for relationships in hello data.</span></span> <span data-ttu-id="7002e-243">在本節中的 hello 教學課程，您會建立並測試數個查詢 toolearn 在其中您可以將分析的輸入資料流轉換的數種方法。</span><span class="sxs-lookup"><span data-stu-id="7002e-243">In this section of hello tutorial, you will create and test several queries toolearn a few ways in which you can transform an input stream for analysis.</span></span> 

<span data-ttu-id="7002e-244">您在此處建立 hello 查詢將只會顯示 hello 已轉換的資料 toohello 螢幕。</span><span class="sxs-lookup"><span data-stu-id="7002e-244">hello queries you create here will just display hello transformed data toohello screen.</span></span> <span data-ttu-id="7002e-245">在更新版本的區段中，您需要設定的輸出來源，以及寫入 hello 已轉換的資料 toothat 接收器的查詢。</span><span class="sxs-lookup"><span data-stu-id="7002e-245">In a later section, you'll configure an output sink and a query that writes hello transformed data toothat sink.</span></span>

<span data-ttu-id="7002e-246">toolearn 進一步了解 hello 語言，請參閱 hello [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/dn834998.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7002e-246">toolearn more about hello language, see hello [Azure Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/dn834998.aspx).</span></span>

### <a name="get-sample-data-for-testing-queries"></a><span data-ttu-id="7002e-247">取得範例資料來測試查詢</span><span class="sxs-lookup"><span data-stu-id="7002e-247">Get sample data for testing queries</span></span>

<span data-ttu-id="7002e-248">hello TelcoGenerator 應用程式正在呼叫記錄 toohello 事件中樞與串流分析工作會從 hello 事件中樞設定的 tooread。</span><span class="sxs-lookup"><span data-stu-id="7002e-248">hello TelcoGenerator app is sending call records toohello event hub, and your Stream Analytics job is configured tooread from hello event hub.</span></span> <span data-ttu-id="7002e-249">您可以使用查詢 tootest hello 作業 toomake 確定正確讀取。</span><span class="sxs-lookup"><span data-stu-id="7002e-249">You can use a query tootest hello job toomake sure that it's reading correctly.</span></span> <span data-ttu-id="7002e-250">太測試查詢 hello Azure 主控台中，您需要範例資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-250">too test a query in hello Azure console, you need sample data.</span></span> <span data-ttu-id="7002e-251">這個逐步解說中，您將範例資料擷取 hello 事件中心傳入的 hello 資料流。</span><span class="sxs-lookup"><span data-stu-id="7002e-251">For this walkthrough, you'll extract sample data from hello stream that's coming into hello event hub.</span></span>

1. <span data-ttu-id="7002e-252">請確定該 hello TelcoGenerator 應用程式正在執行，而且會產生記錄呼叫。</span><span class="sxs-lookup"><span data-stu-id="7002e-252">Make sure that hello TelcoGenerator app is running and producing call records.</span></span>
2. <span data-ttu-id="7002e-253">在 hello 入口網站中，傳回 toohello 串流分析工作刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7002e-253">In hello portal, return toohello Streaming Analytics job blade.</span></span> <span data-ttu-id="7002e-254">(如果您關閉 hello 刀鋒視窗中，搜尋`sa_frauddetection_job_demo`在 hello**所有資源**刀鋒視窗。)</span><span class="sxs-lookup"><span data-stu-id="7002e-254">(If you closed hello blade, search for `sa_frauddetection_job_demo` in hello **All resources** blade.)</span></span>
3. <span data-ttu-id="7002e-255">按一下 hello**查詢**方塊。</span><span class="sxs-lookup"><span data-stu-id="7002e-255">Click hello **Query** box.</span></span> <span data-ttu-id="7002e-256">Azure 會列出 hello 輸入及輸出，已設定為 hello 工作，並可讓您建立查詢，可讓您轉換 hello 輸入資料流傳送 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7002e-256">Azure lists hello inputs and outputs that are configured for hello job, and lets you create a query that lets you transform hello input stream as it is sent toohello output.</span></span>
4. <span data-ttu-id="7002e-257">在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`CallStream`輸入，然後選取 **範例從輸入資料**。</span><span class="sxs-lookup"><span data-stu-id="7002e-257">In hello **Query** blade, click hello dots next toohello `CallStream` input and then select **Sample data from input**.</span></span>

    ![功能表選項 toouse 的範例資料 hello 串流分析工作項目，如 「 範例資料從輸入 」 選取](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    <span data-ttu-id="7002e-259">這會開啟可讓您指定以 tooread hello 多久輸入資料流定義多少範例資料 tooget 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7002e-259">This opens a blade that lets you specify how much sample data tooget, defined in terms of how long tooread hello input stream.</span></span>

5. <span data-ttu-id="7002e-260">設定**分鐘**too3，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="7002e-260">Set **Minutes** too3 and then click **OK**.</span></span> 
    
    ![取樣 hello 輸入資料流，與 「 3 分鐘 」，選取選項。](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    <span data-ttu-id="7002e-262">Azure 範例 3 分鐘 hello 輸入資料流中的資料量與 hello 範例資料已就緒時通知您。</span><span class="sxs-lookup"><span data-stu-id="7002e-262">Azure samples 3 minutes' worth of data from hello input stream and notifies you when hello sample data is ready.</span></span> <span data-ttu-id="7002e-263">(這需要等一下。)</span><span class="sxs-lookup"><span data-stu-id="7002e-263">(This takes a short while.)</span></span> 

<span data-ttu-id="7002e-264">hello 範例資料會暫時存放，可同時有 hello 查詢視窗中開啟。</span><span class="sxs-lookup"><span data-stu-id="7002e-264">hello sample data is stored temporarily and is available while you have hello query window open.</span></span> <span data-ttu-id="7002e-265">如果您關閉 hello 查詢視窗中，會捨棄 hello 範例資料，而且必須 toocreate 一組新的範例資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-265">If you close hello query window, hello sample data is discarded, and you'll have toocreate a new set of sample data.</span></span> 

<span data-ttu-id="7002e-266">或者，您可以取得中有範例資料的.json 檔案[從 GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)，然後將該.json 檔案 toouse 上傳為範例資料以供 hello`CallStream`輸入。</span><span class="sxs-lookup"><span data-stu-id="7002e-266">As an alternative, you can get a .json file that has sample data in it [from GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json), and then upload that .json file toouse as sample data for hello `CallStream` input .</span></span> 

### <a name="test-using-a-pass-through-query"></a><span data-ttu-id="7002e-267">使用傳遞查詢來測試</span><span class="sxs-lookup"><span data-stu-id="7002e-267">Test using a pass-through query</span></span>

<span data-ttu-id="7002e-268">如果您想 tooarchive 每個事件，您可以使用傳遞查詢 tooread hello 事件的 hello 承載中的所有 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="7002e-268">If you want tooarchive every event, you can use a pass-through query tooread all hello fields in hello payload of hello event.</span></span>

1. <span data-ttu-id="7002e-269">在 hello 查詢視窗中，輸入以下查詢：</span><span class="sxs-lookup"><span data-stu-id="7002e-269">In hello query window, enter this query:</span></span>

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    ><span data-ttu-id="7002e-270">如同 SQL，關鍵字不區分大小寫，空白字元也不重要。</span><span class="sxs-lookup"><span data-stu-id="7002e-270">As with SQL, keywords are not case sensitive, and whitespace is not significant.</span></span>

    <span data-ttu-id="7002e-271">在此查詢中，`CallStream`是 hello 別名，指定當您建立 hello 輸入。</span><span class="sxs-lookup"><span data-stu-id="7002e-271">In this query, `CallStream` is hello alias that you specified when you created hello input.</span></span> <span data-ttu-id="7002e-272">如果您使用不同的別名，請改為使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="7002e-272">If you used a different alias, use that name instead.</span></span>

2. <span data-ttu-id="7002e-273">按一下 [ **測試**]。</span><span class="sxs-lookup"><span data-stu-id="7002e-273">Click **Test**.</span></span>

    <span data-ttu-id="7002e-274">hello 資料流分析工作會針對 hello 取樣資料執行 hello 查詢，並在 hello hello 視窗底部顯示 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7002e-274">hello Stream Analytics job runs hello query against hello sample data and displays hello output at hello bottom of hello window.</span></span> <span data-ttu-id="7002e-275">這會告訴您正確設定 hello 事件中樞與 hello 串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7002e-275">This tells you that hello event hub and hello Streaming Analytics job are configured correctly.</span></span> <span data-ttu-id="7002e-276">(如所述，稍後您將建立的輸出接收該 hello 查詢可以將資料寫入。)</span><span class="sxs-lookup"><span data-stu-id="7002e-276">(As noted, later you'll create an output sink that hello query can write data to.)</span></span>

    ![串流分析作業輸出，顯示已產生 73 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    <span data-ttu-id="7002e-278">hello 的記錄，您會看到的確切數目將取決於在 3 分鐘範例中所擷取的記錄數目。</span><span class="sxs-lookup"><span data-stu-id="7002e-278">hello exact number of records you see will depend on how many records were captured in your 3-minute sample.</span></span>
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a><span data-ttu-id="7002e-279">減少 hello 使用資料行投射的欄位數目</span><span class="sxs-lookup"><span data-stu-id="7002e-279">Reduce hello number of fields using a column projection</span></span>

<span data-ttu-id="7002e-280">在許多情況下，您分析不需要從 hello 輸入資料流的所有 hello 資料行。</span><span class="sxs-lookup"><span data-stu-id="7002e-280">In many cases, your analysis doesn't need all hello columns from hello input stream.</span></span> <span data-ttu-id="7002e-281">您可以使用較少的欄位比查詢傳回的 hello 傳遞查詢 tooproject。</span><span class="sxs-lookup"><span data-stu-id="7002e-281">You can use a query tooproject a smaller set of returned fields than in hello pass-through query.</span></span>

1. <span data-ttu-id="7002e-282">變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：</span><span class="sxs-lookup"><span data-stu-id="7002e-282">Change hello query in hello code editor toohello following:</span></span>

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. <span data-ttu-id="7002e-283">再按一次 [測試]。</span><span class="sxs-lookup"><span data-stu-id="7002e-283">Click **Test** again.</span></span> 

    ![投影的串流分析作業輸出，顯示已產生 25 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a><span data-ttu-id="7002e-285">各區域的來電計數：含彙總的輪轉視窗</span><span class="sxs-lookup"><span data-stu-id="7002e-285">Count incoming calls by region: Tumbling window with aggregation</span></span>

<span data-ttu-id="7002e-286">假設您想要的連入呼叫每個區域的 toocount hello 數字。</span><span class="sxs-lookup"><span data-stu-id="7002e-286">Suppose you want toocount hello number of incoming calls per region.</span></span> <span data-ttu-id="7002e-287">在資料流處理資料，當您想 tooperform 彙總函式，例如計算，您需要 toosegment hello 資料流到暫時的單位 （因為 hello 資料流本身是有效的無止盡的）。</span><span class="sxs-lookup"><span data-stu-id="7002e-287">In streaming data, when you want tooperform aggregate functions like counting, you need toosegment hello stream into temporal units (since hello data stream itself is effectively endless).</span></span> <span data-ttu-id="7002e-288">做法是使用串流分析[視窗函式](stream-analytics-window-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="7002e-288">You do this using a Streaming Analytics [window function](stream-analytics-window-functions.md).</span></span> <span data-ttu-id="7002e-289">您接著可以使用該視窗內 hello 資料，做為一個單位。</span><span class="sxs-lookup"><span data-stu-id="7002e-289">You can then work with hello data inside that window as a unit.</span></span>

<span data-ttu-id="7002e-290">在這個轉換過程中，您需要有一連串不重疊的時態性視窗，每個視窗會有一組特定的資料讓您分組和彙總。</span><span class="sxs-lookup"><span data-stu-id="7002e-290">For this transformation, you want a sequence of temporal windows that don't overlap—each window will have a discrete set of data that you can group and aggregate.</span></span> <span data-ttu-id="7002e-291">這種類型的視窗是參照的 tooas*輪轉視窗*。</span><span class="sxs-lookup"><span data-stu-id="7002e-291">This type of window is referred tooas a *Tumbling window* .</span></span> <span data-ttu-id="7002e-292">在 hello 輪轉視窗中，您可以取得 hello 分組的連入呼叫計數`SwitchNum`，代表 hello hello 呼叫起源所在的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="7002e-292">Within hello Tumbling window, you can get a count of hello incoming calls grouped by `SwitchNum`, which represents hello country where hello call originated.</span></span> 

1. <span data-ttu-id="7002e-293">變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：</span><span class="sxs-lookup"><span data-stu-id="7002e-293">Change hello query in hello code editor toohello following:</span></span>

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    <span data-ttu-id="7002e-294">此查詢會使用 hello`Timestamp By`關鍵字 hello`FROM`子句 toospecify hello 中的哪一個時間戳記欄位輸入資料流 toouse toodefine hello 輪轉視窗。</span><span class="sxs-lookup"><span data-stu-id="7002e-294">This query uses hello `Timestamp By` keyword in hello `FROM` clause toospecify which timestamp field in hello input stream toouse toodefine hello Tumbling window.</span></span> <span data-ttu-id="7002e-295">在此情況下，hello 視窗分成 hello 資料區段的 hello`CallRecTime`欄位中每一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="7002e-295">In this case, hello window divides hello data into segments by hello `CallRecTime` field in each record.</span></span> <span data-ttu-id="7002e-296">（如果未不指定任何欄位，則 hello 視窗化作業會使用每個事件抵達 hello 事件中心的 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="7002e-296">(If no field is specified, hello windowing operation uses hello time that each event arrives at hello event hub.</span></span> <span data-ttu-id="7002e-297">請參閱[串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)中的＜抵達時間與應用時間的比較＞。</span><span class="sxs-lookup"><span data-stu-id="7002e-297">See "Arrival Time Vs Application Time" in [Stream Analytics Query Language Reference](https://msdn.microsoft.com/library/azure/dn834998.aspx).</span></span> 

    <span data-ttu-id="7002e-298">hello 投影包含`System.Timestamp`，它會傳回每個視窗的 hello 結束的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="7002e-298">hello projection includes `System.Timestamp`, which returns a timestamp for hello end of each window.</span></span> 

    <span data-ttu-id="7002e-299">您想 toouse 輪轉視窗 toospecify，使用 hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx)函式在 hello`GROUP BY `子句。</span><span class="sxs-lookup"><span data-stu-id="7002e-299">toospecify that you want toouse a Tumbling window, you use hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) function in hello `GROUP BY `clause.</span></span> <span data-ttu-id="7002e-300">在 hello 函式，您可以指定時間單位 （從微秒 tooa 每天） 和視窗大小 （單位數量）。</span><span class="sxs-lookup"><span data-stu-id="7002e-300">In hello function, you specify a time unit (anywhere from a microsecond tooa day) and a window size (how many units).</span></span> <span data-ttu-id="7002e-301">在此範例中，hello 輪轉視窗組成 5 秒的間隔，以便每隔 5 秒的價值的呼叫會取得依國家/地區的計數。</span><span class="sxs-lookup"><span data-stu-id="7002e-301">In this example, hello Tumbling window consists of 5-second intervals, so you will get a count by country for every 5 seconds' worth of calls.</span></span>

2. <span data-ttu-id="7002e-302">再按一次 [測試]。</span><span class="sxs-lookup"><span data-stu-id="7002e-302">Click **Test** again.</span></span> <span data-ttu-id="7002e-303">在 hello 結果中，請注意下的該 hello 時間戳記**WindowEnd**在 5 秒為增量單位。</span><span class="sxs-lookup"><span data-stu-id="7002e-303">In hello results, notice that hello timestamps under **WindowEnd** are in 5-second increments.</span></span>

    ![彙總的串流分析作業輸出，顯示已產生 13 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a><span data-ttu-id="7002e-305">使用自我聯結來偵測 SIM 詐騙</span><span class="sxs-lookup"><span data-stu-id="7002e-305">Detect SIM fraud using a self-join</span></span>

<span data-ttu-id="7002e-306">針對此範例中，我們可以考慮詐騙使用量 toobe 呼叫源自 hello 相同使用者但在不同的另一個 5 秒內的位置。</span><span class="sxs-lookup"><span data-stu-id="7002e-306">For this example, we can consider fraudulent usage toobe calls that originate from hello same user but in different locations within 5 seconds of one another.</span></span> <span data-ttu-id="7002e-307">例如，hello 相同的使用者無法合法撥打電話，從 hello 美國和澳大利亞 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="7002e-307">For example, hello same user can't legitimately make a call from hello US and Australia at hello same time.</span></span> 

<span data-ttu-id="7002e-308">toocheck 在這些情況下的，您可以使用自我聯結的資料流資料 toojoin hello 資料流 tooitself 根據 hello hello`CallRecTime`值。</span><span class="sxs-lookup"><span data-stu-id="7002e-308">toocheck for these cases, you can use a self-join of hello streaming data toojoin hello stream tooitself based on hello `CallRecTime` value.</span></span> <span data-ttu-id="7002e-309">然後您可以查看呼叫記錄在 hello`CallingIMSI`值 (hello 起始數字) 是 hello 相同，但 hello `SwitchNum` （國家/地區） 的值不是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="7002e-309">You can then look for call records where hello `CallingIMSI` value (hello originating number) is hello same, but hello `SwitchNum` value (country of origin) is not hello same.</span></span>

<span data-ttu-id="7002e-310">當您使用資料流資料使用聯結時，hello 聯結必須提供遠比對資料列的 hello 一些限制，可以及時區隔。</span><span class="sxs-lookup"><span data-stu-id="7002e-310">When you use a join with streaming data, hello join must provide some limits on how far hello matching rows can be separated in time.</span></span> <span data-ttu-id="7002e-311">（如前文所述，hello 串流資料是有效的無止盡）。指定 hello hello 關聯性的時間範圍內 hello`ON`使用 hello 的 hello 聯結子句`DATEDIFF`函式。</span><span class="sxs-lookup"><span data-stu-id="7002e-311">(As noted earlier, hello streaming data is effectively endless.) hello time bounds for hello relationship are specified inside hello `ON` clause of hello join, using hello `DATEDIFF` function .</span></span> <span data-ttu-id="7002e-312">在此情況下，hello 聯結根據在 5 秒的間隔呼叫資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-312">In this case, hello join is based on a 5-second interval of call data .</span></span>

1. <span data-ttu-id="7002e-313">變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：</span><span class="sxs-lookup"><span data-stu-id="7002e-313">Change hello query in hello code editor toohello following:</span></span> 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    <span data-ttu-id="7002e-314">此查詢就像除了 hello 任何 SQL 聯結`DATEDIFF`hello 聯結中的函式。</span><span class="sxs-lookup"><span data-stu-id="7002e-314">This query is like any SQL join except for hello `DATEDIFF` function in hello join.</span></span> <span data-ttu-id="7002e-315">這是版本`DATEDIFF`特定 tooStreaming 分析，而且它必須出現在 hello`ON...BETWEEN`子句。</span><span class="sxs-lookup"><span data-stu-id="7002e-315">This is a version of `DATEDIFF` that's specific tooStreaming Analytics, and it must appear in hello `ON...BETWEEN` clause.</span></span> <span data-ttu-id="7002e-316">hello 參數為時間單位 （在此範例中為秒） 和 hello 別名的 hello hello 聯結兩個來源。</span><span class="sxs-lookup"><span data-stu-id="7002e-316">hello parameters are a time unit (seconds in this example) and hello aliases of hello two sources for hello join.</span></span> <span data-ttu-id="7002e-317">(這點不同於 hello 標準 SQL`DATEDIFF`函式。)</span><span class="sxs-lookup"><span data-stu-id="7002e-317">(This is different from hello standard SQL `DATEDIFF` function.)</span></span> 

    <span data-ttu-id="7002e-318">hello`WHERE`子句包含 hello 詐騙呼叫加上旗標的 hello 條件： hello 原始參數不是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="7002e-318">hello `WHERE` clause includes hello condition that flags hello fraudulent call: hello originating switches are not hello same.</span></span> 

2. <span data-ttu-id="7002e-319">再按一次 [測試]。</span><span class="sxs-lookup"><span data-stu-id="7002e-319">Click **Test** again.</span></span> 

    ![自我聯結的串流分析作業輸出，顯示已產生 6 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. <span data-ttu-id="7002e-321">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-321">Click **Save**.</span></span> <span data-ttu-id="7002e-322">這可以節省 hello 自我聯結查詢 hello 串流分析工作的一部分。</span><span class="sxs-lookup"><span data-stu-id="7002e-322">This saves hello self-join query as part of hello Streaming Analytics job.</span></span> <span data-ttu-id="7002e-323">（它不會儲存 hello 範例資料）。</span><span class="sxs-lookup"><span data-stu-id="7002e-323">(It doesn't save hello sample data.)</span></span>

    ![儲存串流分析作業](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a><span data-ttu-id="7002e-325">建立輸出接收 toostore 轉換資料</span><span class="sxs-lookup"><span data-stu-id="7002e-325">Create an output sink toostore transformed data</span></span>

<span data-ttu-id="7002e-326">您已定義的事件資料流、 事件中樞輸入的 tooingest 事件，以及查詢 tooperform 轉換 hello 資料流上。</span><span class="sxs-lookup"><span data-stu-id="7002e-326">You've defined an event stream, an event hub input tooingest events, and a query tooperform a transformation over hello stream.</span></span> <span data-ttu-id="7002e-327">hello 最後一個步驟是 toodefine 為 hello 工作的輸出來源 — 也就是將 toowrite hello 轉換資料流。</span><span class="sxs-lookup"><span data-stu-id="7002e-327">hello last step is toodefine an output sink for hello job—that is, a place toowrite hello transformed stream to.</span></span> 

<span data-ttu-id="7002e-328">您可以使用許多資源作為輸出接收，例如 SQL Server 資料庫、資料表儲存體、Data Lake 儲存體、Power BI，甚至是另一個事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7002e-328">You can use many resources as output sinks—a SQL Server database, table storage, Data Lake storage, Power BI, and even another event hub.</span></span> <span data-ttu-id="7002e-329">此教學課程中，您會將寫入 hello 資料流 tooAzure Blob 儲存體，這是典型的選擇，來收集事件資訊，以便稍後進行分析，因為它適用於非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-329">For this tutorial, you'll write hello stream tooAzure Blob Storage, which is a typical choice for collecting event information for later analysis, since it accommodates unstructured data .</span></span>

<span data-ttu-id="7002e-330">如果您已有 blob 儲存體帳戶，則可直接使用。</span><span class="sxs-lookup"><span data-stu-id="7002e-330">If you have an existing blob storage account, you can use that.</span></span> <span data-ttu-id="7002e-331">此教學課程中，我們將為您示範如何 toocreate 新的儲存體帳戶只針對本教學課程。</span><span class="sxs-lookup"><span data-stu-id="7002e-331">For this tutorial, we'll show you how toocreate a new storage account just for this tutorial.</span></span>

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="7002e-332">建立 Azure Blob 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="7002e-332">Create an Azure Blob Storage account</span></span>

1. <span data-ttu-id="7002e-333">在 hello Azure 入口網站，會傳回 toohello 串流分析工作刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7002e-333">In hello Azure portal, return toohello Streaming Analytics job blade.</span></span> <span data-ttu-id="7002e-334">(如果您關閉 hello 刀鋒視窗中，搜尋`sa_frauddetection_job_demo`在 hello**所有資源**刀鋒視窗。)</span><span class="sxs-lookup"><span data-stu-id="7002e-334">(If you closed hello blade, search for `sa_frauddetection_job_demo` in hello **All resources** blade.)</span></span>
2. <span data-ttu-id="7002e-335">在 hello**作業拓撲**區段中，按一下 hello**輸出**方塊。</span><span class="sxs-lookup"><span data-stu-id="7002e-335">In hello **Job Topology** section, click hello **Output** box.</span></span> 
3. <span data-ttu-id="7002e-336">在 hello**輸出**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：</span><span class="sxs-lookup"><span data-stu-id="7002e-336">In hello **Outputs** blade, click **+&nbsp;Add** and then fill out hello blade with these values:</span></span>

    * <span data-ttu-id="7002e-337">**輸出別名**： 使用 hello 名稱`CallStream-FraudulentCalls`。</span><span class="sxs-lookup"><span data-stu-id="7002e-337">**Output alias**: Use hello name `CallStream-FraudulentCalls`.</span></span> 
    * <span data-ttu-id="7002e-338">**接收器**：選取 [Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="7002e-338">**Sink**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="7002e-339">**匯入選項**：選取 [使用來自目前訂用帳戶的 Blob 儲存體]。</span><span class="sxs-lookup"><span data-stu-id="7002e-339">**Import options**: Select **Use blob storage from current subscription**.</span></span>
    * <span data-ttu-id="7002e-340">**儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="7002e-340">**Storage account**.</span></span> <span data-ttu-id="7002e-341">選取 [建立新儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="7002e-341">Select **Create new storage account.**</span></span>
    * <span data-ttu-id="7002e-342">**儲存體帳戶** (第二個方塊)。</span><span class="sxs-lookup"><span data-stu-id="7002e-342">**Storage account** (second box).</span></span> <span data-ttu-id="7002e-343">輸入 `YOURNAMEsademo`，其中 `YOURNAME` 是您的名稱或另一個唯一字串。</span><span class="sxs-lookup"><span data-stu-id="7002e-343">Enter `YOURNAMEsademo`, where `YOURNAME` is your name or another unique string.</span></span> <span data-ttu-id="7002e-344">hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。</span><span class="sxs-lookup"><span data-stu-id="7002e-344">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 
    * <span data-ttu-id="7002e-345">**容器**。</span><span class="sxs-lookup"><span data-stu-id="7002e-345">**Container**.</span></span> <span data-ttu-id="7002e-346">輸入 `sa-fraudulentcalls-demo`。</span><span class="sxs-lookup"><span data-stu-id="7002e-346">Enter `sa-fraudulentcalls-demo`.</span></span>
    <span data-ttu-id="7002e-347">hello 儲存體帳戶名稱及容器名稱是使用同時 tooprovide hello blob 儲存體，像這樣的 URI:</span><span class="sxs-lookup"><span data-stu-id="7002e-347">hello storage account name and container name are used together tooprovide a URI for hello blob storage, like this:</span></span> 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![串流分析作業的 [新輸出] 刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. <span data-ttu-id="7002e-349">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-349">Click **Create**.</span></span> 

    <span data-ttu-id="7002e-350">Azure 會建立 hello 儲存體帳戶，並會自動產生索引鍵。</span><span class="sxs-lookup"><span data-stu-id="7002e-350">Azure creates hello storage account and generates a key automatically.</span></span> 

5. <span data-ttu-id="7002e-351">關閉 hello**輸出**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7002e-351">Close hello **Outputs** blade.</span></span> 

## <a name="start-hello-streaming-analytics-job"></a><span data-ttu-id="7002e-352">啟動 hello 串流分析工作</span><span class="sxs-lookup"><span data-stu-id="7002e-352">Start hello Streaming Analytics job</span></span>

<span data-ttu-id="7002e-353">hello 工作現在已設定。</span><span class="sxs-lookup"><span data-stu-id="7002e-353">hello job is now configured.</span></span> <span data-ttu-id="7002e-354">您所指定的輸入 （hello 事件中心）、 (hello 查詢詐騙呼叫的 toolook，) 的轉換和輸出 （blob 儲存）。</span><span class="sxs-lookup"><span data-stu-id="7002e-354">You've specified an input (hello event hub), a transformation (hello query toolook for fraudulent calls), and an output (blob storage).</span></span> <span data-ttu-id="7002e-355">您現在可以啟動 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="7002e-355">You can now start hello job.</span></span> 

1. <span data-ttu-id="7002e-356">請確定 hello TelcoGenerator 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="7002e-356">Make sure hello TelcoGenerator app is running.</span></span>

2. <span data-ttu-id="7002e-357">在 hello 作業刀鋒視窗中，按一下 **啟動**。</span><span class="sxs-lookup"><span data-stu-id="7002e-357">In hello job blade, click **Start**.</span></span>

    ![啟動 hello 資料流分析工作](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. <span data-ttu-id="7002e-359">在 hello**開始工作**刀鋒視窗中的，對於作業輸出開始時間，請選取**現在**。</span><span class="sxs-lookup"><span data-stu-id="7002e-359">In hello **Start job** blade, for Job output start time, select **Now**.</span></span> 

4. <span data-ttu-id="7002e-360">按一下 [啟動] 。</span><span class="sxs-lookup"><span data-stu-id="7002e-360">Click **Start**.</span></span> 

    ![「 啟動工作 」 刀鋒視窗中的 hello 資料流分析工作](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    <span data-ttu-id="7002e-362">Azure 通知您，當 hello 作業已啟動，而且 hello 作業刀鋒視窗中，在 hello 狀態會顯示為**執行**。</span><span class="sxs-lookup"><span data-stu-id="7002e-362">Azure notifies you when hello job has started, and in hello job blade, hello status is displayed as **Running**.</span></span>

    ![串流分析作業狀態，顯示「執行中」](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a><span data-ttu-id="7002e-364">檢查 hello 轉換資料</span><span class="sxs-lookup"><span data-stu-id="7002e-364">Examine hello transformed data</span></span>

<span data-ttu-id="7002e-365">您現在已完成串流分析作業。</span><span class="sxs-lookup"><span data-stu-id="7002e-365">You now have a complete Streaming Analytics job.</span></span> <span data-ttu-id="7002e-366">hello 作業是檢查通話中繼資料的資料流、 尋找即時詐騙撥打電話，以及撰寫這些詐騙呼叫 toostorage 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7002e-366">hello job is examining a stream of phone call metadata, looking for fraudulent phone calls in real time, and writing information about those fraudulent calls toostorage.</span></span> 

<span data-ttu-id="7002e-367">toocomplete 本教學課程中，您可能會想 toolook hello hello 串流分析工作所擷取的資料。</span><span class="sxs-lookup"><span data-stu-id="7002e-367">toocomplete this tutorial, you might want toolook at hello data being captured by hello Streaming Analytics job.</span></span> <span data-ttu-id="7002e-368">hello 資料寫入 Blob 儲存體 tooAzure 區塊 （chunk） （檔案）。</span><span class="sxs-lookup"><span data-stu-id="7002e-368">hello data is being written tooAzure Blog Storage in chunks (files).</span></span> <span data-ttu-id="7002e-369">您可以使用任何可讀取 Azure Blob 儲存體的工具。</span><span class="sxs-lookup"><span data-stu-id="7002e-369">You can use any tool that reads Azure Blob Storage.</span></span> <span data-ttu-id="7002e-370">Hello 必要條件 > 一節所述，您可以在 Visual Studio 中，使用 Azure 擴充功能，或者您可以使用這類工具[Azure 儲存體總管](http://storageexplorer.com/)或[Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)。</span><span class="sxs-lookup"><span data-stu-id="7002e-370">As noted in hello Prerequisites section, you can use Azure extensions in Visual Studio, or you can use a tool like [Azure Storage Explorer](http://storageexplorer.com/) or [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction).</span></span> 

<span data-ttu-id="7002e-371">當您檢查 hello blob 儲存體中的檔案內容時，您會看到類似下列 hello:</span><span class="sxs-lookup"><span data-stu-id="7002e-371">When you examine hello contents of a file in blob storage, you see something like hello following :</span></span>

![Azure blob 儲存體與串流分析輸出](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="7002e-373">清除資源</span><span class="sxs-lookup"><span data-stu-id="7002e-373">Clean up resources</span></span>

<span data-ttu-id="7002e-374">我們有其他發行項，繼續進行 hello 詐騙偵測案例，並使用您已建立本教學課程中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7002e-374">We have additional articles that continue with hello fraud-detection scenario and that use hello resources that you've created in this tutorial.</span></span> <span data-ttu-id="7002e-375">如果您想 toocontinue，請參閱底下的 hello 建議**後續步驟**更新版本。</span><span class="sxs-lookup"><span data-stu-id="7002e-375">If you want toocontinue, see hello suggestions under **Next steps** later.</span></span>

<span data-ttu-id="7002e-376">不過，如果您完成時，您不需要您已建立 hello 資源，您可以刪除它們，讓您不會產生不必要的 Azure 費用。</span><span class="sxs-lookup"><span data-stu-id="7002e-376">However, if you're done and you don't need hello resources you've created, you can delete them so that you don't incur unnecessary Azure charges.</span></span> <span data-ttu-id="7002e-377">在此情況下，我們建議您不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="7002e-377">In that case, we suggest that you do hello following:</span></span>

1. <span data-ttu-id="7002e-378">停止 hello 串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7002e-378">Stop hello Streaming Analytics job.</span></span> <span data-ttu-id="7002e-379">在 hello**作業**刀鋒視窗中，按一下 **停止**hello 頂端。</span><span class="sxs-lookup"><span data-stu-id="7002e-379">In hello **Jobs** blade, click **Stop** at hello top.</span></span>
2. <span data-ttu-id="7002e-380">停止 hello 電信公司產生器應用程式。</span><span class="sxs-lookup"><span data-stu-id="7002e-380">Stop hello Telco Generator app.</span></span> <span data-ttu-id="7002e-381">在 hello 命令視窗，在您啟動 hello 應用程式，請按 Ctrl + C。</span><span class="sxs-lookup"><span data-stu-id="7002e-381">In hello command window where you started hello app, press Ctrl+C.</span></span>
3. <span data-ttu-id="7002e-382">如果您建立的新 blob 儲存體帳戶只用於本教學課程，請刪除它。</span><span class="sxs-lookup"><span data-stu-id="7002e-382">If you created a new blob storage account just for this tutorial, delete it.</span></span> 
4. <span data-ttu-id="7002e-383">刪除 hello 串流分析工作。</span><span class="sxs-lookup"><span data-stu-id="7002e-383">Delete hello Streaming Analytics job.</span></span>
5. <span data-ttu-id="7002e-384">刪除 hello 事件中樞。</span><span class="sxs-lookup"><span data-stu-id="7002e-384">Delete hello event hub.</span></span>
6. <span data-ttu-id="7002e-385">刪除 hello 事件中樞命名空間。</span><span class="sxs-lookup"><span data-stu-id="7002e-385">Delete hello event hub namespace.</span></span>

## <a name="get-support"></a><span data-ttu-id="7002e-386">取得支援</span><span class="sxs-lookup"><span data-stu-id="7002e-386">Get support</span></span>

<span data-ttu-id="7002e-387">如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。</span><span class="sxs-lookup"><span data-stu-id="7002e-387">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7002e-388">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7002e-388">Next steps</span></span>

<span data-ttu-id="7002e-389">您可以繼續本教學課程以 hello 下列文章：</span><span class="sxs-lookup"><span data-stu-id="7002e-389">You can continue this tutorial with hello following articles:</span></span>

* <span data-ttu-id="7002e-390">[串流分析及 Power BI：適用於串流資料的即時分析儀表板](stream-analytics-power-bi-dashboard.md)。</span><span class="sxs-lookup"><span data-stu-id="7002e-390">[Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](stream-analytics-power-bi-dashboard.md).</span></span> <span data-ttu-id="7002e-391">本文章將示範如何 toosend hello 電信公司輸出的 hello 資料流分析作業 tooPower BI 即時的視覺效果和分析。</span><span class="sxs-lookup"><span data-stu-id="7002e-391">This article shows you how toosend hello TelCo output of hello Stream Analytics job tooPower BI for real-time visualization and analysis.</span></span>
* <span data-ttu-id="7002e-392">[如何從 Azure Redis 快取 Azure 函式的使用中的 Azure Stream Analytics toostore 資料](stream-analytics-functions-redis.md)。</span><span class="sxs-lookup"><span data-stu-id="7002e-392">[How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions](stream-analytics-functions-redis.md).</span></span> <span data-ttu-id="7002e-393">本文將說明如何 toouse Azure 函式 toowrite 詐騙呼叫 tooan Azure Redis 快取透過服務匯流排佇列。</span><span class="sxs-lookup"><span data-stu-id="7002e-393">This article shows how toouse Azure Functions toowrite fraudulent calls tooan Azure Redis cache via a Service Bus queue.</span></span>

<span data-ttu-id="7002e-394">如需串流分析在整體上的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="7002e-394">For more information about Stream Analytics in general, try these articles:</span></span>

* [<span data-ttu-id="7002e-395">簡介 tooAzure 資料流分析</span><span class="sxs-lookup"><span data-stu-id="7002e-395">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="7002e-396">調整 Azure Stream Analytics 工作</span><span class="sxs-lookup"><span data-stu-id="7002e-396">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="7002e-397">Azure Stream Analytics 查詢語言參考</span><span class="sxs-lookup"><span data-stu-id="7002e-397">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="7002e-398">Azure 串流分析管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="7002e-398">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
