---
title: "aaaCreate 連接 tooAzure 服務的函式 |Microsoft 文件"
description: "使用 Azure 函式 toocreate 連接 tooother Azure 的無伺服器應用程式服務。"
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a><span data-ttu-id="dc6c1-104">使用 Azure 函式 toocreate 函式連接 tooother Azure 服務</span><span class="sxs-lookup"><span data-stu-id="dc6c1-104">Use Azure Functions toocreate a function that connects tooother Azure services</span></span>

<span data-ttu-id="dc6c1-105">本主題說明如何 toocreate 會接聽在 Azure 儲存體佇列和複製 hello toomessages 的 Azure 功能中的函式訊息 toorows Azure 儲存體資料表中。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-105">This topic shows you how toocreate a function in Azure Functions that listens toomessages on an Azure Storage queue and copies hello messages toorows in an Azure Storage table.</span></span> <span data-ttu-id="dc6c1-106">計時器觸發函式是使用的 tooload 到 hello 佇列的訊息。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-106">A timer triggered function is used tooload messages into hello queue.</span></span> <span data-ttu-id="dc6c1-107">第二個函式會從 hello 佇列讀取，並將訊息 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-107">A second function reads from hello queue and writes messages toohello table.</span></span> <span data-ttu-id="dc6c1-108">Hello 佇列和 hello 資料表建立您的 Azure hello 繫結定義為基礎的函式。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-108">Both hello queue and hello table are created for you by Azure Functions based on hello binding definitions.</span></span> 

<span data-ttu-id="dc6c1-109">更有趣的 toomake 項目，一個函式以 JavaScript 撰寫並 hello 其他以 C# 指令碼。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-109">toomake things more interesting, one function is written in JavaScript and hello other is written in C# script.</span></span> <span data-ttu-id="dc6c1-110">這可示範函式應用程式如何擁有使用不同語言的函式。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="dc6c1-111">您可以看到 [Channel 9 影片](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)中示範的這個案例。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-toohello-queue"></a><span data-ttu-id="dc6c1-112">建立將寫入 toohello 佇列的函式</span><span class="sxs-lookup"><span data-stu-id="dc6c1-112">Create a function that writes toohello queue</span></span>

<span data-ttu-id="dc6c1-113">您可以連接 tooa 儲存體佇列之前，您會需要 toocreate 載入 hello 訊息佇列的函式。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-113">Before you can connect tooa storage queue, you need toocreate a function that loads hello message queue.</span></span> <span data-ttu-id="dc6c1-114">這個 JavaScript 函式會使用計時器觸發程序會寫入訊息 toohello 佇列每隔 10 秒。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-114">This JavaScript function uses a timer trigger that writes a message toohello queue every 10 seconds.</span></span> <span data-ttu-id="dc6c1-115">如果您還沒有 Azure 帳戶，請參閱 hello[再試一次 Azure 函式](https://functions.azure.com/try)體驗，或[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-115">If you don't already have an Azure account, check out hello [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="dc6c1-116">請 toohello Azure 入口網站，並找出您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-116">Go toohello Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="dc6c1-117">按一下 [新增函式] > [TimerTrigger JavaScript]。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="dc6c1-118">命名 hello 函式**FunctionsBindingsDemo1**，輸入 cron 運算式值為`0/10 * * * * *`如**排程**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-118">Name hello function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![新增計時器觸發函式](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="dc6c1-120">您現在已建立會每隔 10 秒執行一次的計時器觸發函式。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="dc6c1-121">在 hello**開發**索引標籤上，按一下 **記錄檔**及檢視 hello 記錄檔中的 hello 活動。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-121">On hello **Develop** tab, click **Logs** and view hello activity in hello log.</span></span> <span data-ttu-id="dc6c1-122">您會看到每隔 10 秒寫入的記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-122">You see a log entry written every 10 seconds.</span></span>
   
    ![檢視 hello 記錄 tooverify hello 函式運作方式](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="dc6c1-124">新增訊息佇列輸出繫結</span><span class="sxs-lookup"><span data-stu-id="dc6c1-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="dc6c1-125">在 hello**整合**索引標籤上，選擇**新輸出** > **Azure 佇列儲存體** > **選取**。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-125">On hello **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![新增觸發計時器函式](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="dc6c1-127">輸入`myQueueItem`如**訊息參數名稱**和`functions-bindings`如**佇列名稱**，選取現有**儲存體帳戶連接**或按一下**新**toocreate 儲存體帳戶連接，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** toocreate a storage account connection, and then click **Save**.</span></span>  

    ![建立 hello 輸出繫結 toohello 儲存體佇列](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="dc6c1-129">在 hello**開發**索引標籤上，新增下列程式碼 toohello 函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc6c1-129">Back in hello **Develop** tab, append hello following code toohello function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="dc6c1-130">找出 hello*如果*陳述式的大約行 9 hello 函式，並插入 hello 下列程式碼會在該陳述式之後。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-130">Locate hello *if* statement around line 9 of hello function, and insert hello following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="dc6c1-131">此程式碼建立**myQueueItem**並設定其**時間**屬性 toohello 目前時間戳記。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-131">This code creates a **myQueueItem** and sets its **time** property toohello current timeStamp.</span></span> <span data-ttu-id="dc6c1-132">接著它會加入 hello 新佇列項目 toohello 內容的**myQueueItem**繫結。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-132">It then adds hello new queue item toohello context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="dc6c1-133">按一下 [儲存並執行]。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="dc6c1-134">使用儲存體總管來檢視儲存體更新</span><span class="sxs-lookup"><span data-stu-id="dc6c1-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="dc6c1-135">您可以確認您的函式正在檢視您所建立的 hello 佇列中的訊息。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-135">You can verify that your function is working by viewing messages in hello queue you created.</span></span>  <span data-ttu-id="dc6c1-136">您可以使用 Visual Studio 中的 Cloud Explorer 來連線 tooyour 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-136">You can connect tooyour storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="dc6c1-137">不過，hello 入口網站可讓您輕鬆 tooconnect tooyour 儲存體帳戶使用 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-137">However, hello portal makes it easy tooconnect tooyour storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="dc6c1-138">在 hello**整合**索引標籤上，按一下您的佇列輸出繫結 >**文件**，然後取消隱藏 hello 連接字串儲存體帳戶，並複製 hello 值。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-138">In hello **Integrate** tab, click your queue output binding > **Documentation**, then unhide hello Connection String for your storage account and copy hello value.</span></span> <span data-ttu-id="dc6c1-139">您使用此值 tooconnect tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-139">You use this value tooconnect tooyour storage account.</span></span>

    ![下載 Azure 儲存體總管](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="dc6c1-141">如果您還沒有這麼做，請下載並安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="dc6c1-142">按一下 [儲存體總管] 中的 hello 連接 tooAzure 儲存體圖示、 在 hello 欄位中，貼上 hello 連接字串並完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-142">In Storage Explorer, click hello connect tooAzure Storage icon, paste hello connection string in hello field, and complete hello wizard.</span></span>

    ![儲存體總管新增連接](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="dc6c1-144">在下**本機和附加**，依序展開**儲存體帳戶**> 儲存體帳戶 >**佇列** > **函式繫結**並確認訊息會寫入 toohello 佇列。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written toohello queue.</span></span>

    ![Hello 佇列中訊息的檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="dc6c1-146">如果 hello 佇列不存在，或為空白，則最有可能您函式繫結或程式碼發生問題。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-146">If hello queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-hello-queue"></a><span data-ttu-id="dc6c1-147">建立從 hello 佇列讀取的函式</span><span class="sxs-lookup"><span data-stu-id="dc6c1-147">Create a function that reads from hello queue</span></span>

<span data-ttu-id="dc6c1-148">既然您已加入 toohello 佇列的訊息時，您可以建立另一個函式會從 hello 佇列讀取和寫入 hello 訊息永久 tooan Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-148">Now that you have messages being added toohello queue, you can create another function that reads from hello queue and writes hello messages permanently tooan Azure Storage table.</span></span>

1. <span data-ttu-id="dc6c1-149">按一下 [新增函式] > [QueueTrigger-CSharp]。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="dc6c1-150">命名 hello 函式`FunctionsBindingsDemo2`，輸入**函式繫結**在 hello**佇列名稱**欄位中，選取現有的儲存體帳戶或建立一個，，然後按一下**建立**.</span><span class="sxs-lookup"><span data-stu-id="dc6c1-150">Name hello function `FunctionsBindingsDemo2`, enter **functions-bindings** in hello **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![新增輸出佇列計時器函式](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="dc6c1-152">（選擇性）您可以確認 hello 新函式運作方式是在做為之前的存放裝置總管 中檢視 hello 新佇列。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-152">(Optional) You can verify that hello new function works by viewing hello new queue in Storage Explorer as before.</span></span> <span data-ttu-id="dc6c1-153">您也可以使用 Visual Studio 中的雲端總管。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="dc6c1-154">（選擇性）重新整理 hello**函式繫結**排入佇列，並注意從 hello 佇列已經移除項目。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-154">(Optional) Refresh hello **functions-bindings** queue and notice that items have been removed from hello queue.</span></span> <span data-ttu-id="dc6c1-155">hello 移除會發生 hello 函式繫結的 toohello**函式繫結**輸入觸發程序和 hello 函式讀取 hello 佇列的佇列。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-155">hello removal occurs because hello function is bound toohello **functions-bindings** queue as an input trigger and hello function reads hello queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="dc6c1-156">新增資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="dc6c1-156">Add a table output binding</span></span>

1. <span data-ttu-id="dc6c1-157">在 FunctionsBindingsDemo2 中，按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![新增繫結 tooan Azure 儲存體資料表](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="dc6c1-159">輸入 `functionbindings` 做為 資料表名稱 以及輸入 `myTable` 做為 資料表參數名稱，選擇 儲存體帳戶連線 或建立新的連線，然後按一下儲存。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![設定 hello 儲存體資料表繫結](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="dc6c1-161">在 hello**開發**索引標籤上，hello 現有函式程式碼取代 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="dc6c1-161">In hello **Develop** tab, replace hello existing function code with hello following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="dc6c1-162">hello **TableItem**類別代表 hello 儲存體資料表中的資料列並加入 hello 項目 toohello`myTable`集合**TableItem**物件。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-162">hello **TableItem** class represents a row in hello storage table, and you add hello item toohello `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="dc6c1-163">您必須設定 hello **PartitionKey**和**RowKey**屬性 toobe 無法 tooinsert hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-163">You must set hello **PartitionKey** and **RowKey** properties toobe able tooinsert into hello table.</span></span>

4. <span data-ttu-id="dc6c1-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-164">Click **Save**.</span></span>  <span data-ttu-id="dc6c1-165">最後，您可以藉由檢視儲存體總管或 Visual Studio Cloud Explorer 中的 hello 資料表來確認 hello 函式可運作。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-165">Finally, you can verify hello function works by viewing hello table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="dc6c1-166">（選擇性）在儲存體帳戶在儲存體總管 中，依序展開**資料表** > **functionsbindings**並確認資料列會加入 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added toohello table.</span></span> <span data-ttu-id="dc6c1-167">您可以在 Visual Studio 中的 Cloud Explorer 中 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-167">You can do hello same in Cloud Explorer in Visual Studio.</span></span>

    ![Hello 資料表中資料列的檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="dc6c1-169">如果 hello 資料表不存在，或為空白，則最有可能您函式繫結或程式碼發生問題。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-169">If hello table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="dc6c1-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc6c1-170">Next steps</span></span>
<span data-ttu-id="dc6c1-171">如需 Azure 函式的詳細資訊，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc6c1-171">For more information about Azure Functions, see hello following topics:</span></span>

* [<span data-ttu-id="dc6c1-172">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="dc6c1-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="dc6c1-173">可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="dc6c1-174">測試 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="dc6c1-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="dc6c1-175">說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="dc6c1-176">如何 tooscale Azure 函式</span><span class="sxs-lookup"><span data-stu-id="dc6c1-176">How tooscale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="dc6c1-177">討論適用於 Azure 函式，包括 hello 耗用量主控方案，以及如何 toochoose hello 右計劃的服務方案。</span><span class="sxs-lookup"><span data-stu-id="dc6c1-177">Discusses service plans available with Azure Functions, including hello Consumption hosting plan, and how toochoose hello right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

