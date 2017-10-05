---
title: "建立連接到 Azure 服務的函式 | Microsoft Docs"
description: "使用 Azure Functions 來建立連接至其他 Azure 服務的無伺服器應用程式。"
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
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="62c96-104">使用 Azure Functions 來建立連接至其他 Azure 服務的函式</span><span class="sxs-lookup"><span data-stu-id="62c96-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="62c96-105">本主題說明如何在 Azure Functions 中建立函式，以接聽 Azure 儲存體佇列上的訊息，以及將訊息複製到 Azure 儲存體資料表中的資料列。</span><span class="sxs-lookup"><span data-stu-id="62c96-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="62c96-106">計時器觸發函式用將訊息載入佇列中。</span><span class="sxs-lookup"><span data-stu-id="62c96-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="62c96-107">第二個函式會從佇列讀取並將訊息寫入資料表中。</span><span class="sxs-lookup"><span data-stu-id="62c96-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="62c96-108">Azure Functions 會根據繫結定義為您建立佇列和資料表。</span><span class="sxs-lookup"><span data-stu-id="62c96-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="62c96-109">更有趣的做法是以 JavaScript 撰寫一個函式，並另以 C# 指令碼撰寫另一個函式。</span><span class="sxs-lookup"><span data-stu-id="62c96-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="62c96-110">這可示範函式應用程式如何擁有使用不同語言的函式。</span><span class="sxs-lookup"><span data-stu-id="62c96-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="62c96-111">您可以看到 [Channel 9 影片](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player)中示範的這個案例。</span><span class="sxs-lookup"><span data-stu-id="62c96-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="62c96-112">建立可寫入佇列的函式</span><span class="sxs-lookup"><span data-stu-id="62c96-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="62c96-113">您必須先建立可載入訊息佇列的函式，才可以連接到儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="62c96-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="62c96-114">這個 JavaScript 函式使用計時器觸發程序，每隔 10 秒將訊息寫入佇列。</span><span class="sxs-lookup"><span data-stu-id="62c96-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="62c96-115">如果您沒有 Azure 帳戶，請查看[試用 Azure Functions](https://functions.azure.com/try) 體驗，或[建立免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="62c96-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="62c96-116">移至 Azure 入口網站，並找出您的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="62c96-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="62c96-117">按一下 [新增函式] > [TimerTrigger JavaScript]。</span><span class="sxs-lookup"><span data-stu-id="62c96-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="62c96-118">將函式命名為 **FunctionsBindingsDemo1**，針對 [排程] 輸入 cron 運算式值 `0/10 * * * * *`，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="62c96-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![新增計時器觸發函式](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="62c96-120">您現在已建立會每隔 10 秒執行一次的計時器觸發函式。</span><span class="sxs-lookup"><span data-stu-id="62c96-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="62c96-121">在 [開發] 索引標籤上，按一下 [記錄檔] 並檢視記錄檔中的活動。</span><span class="sxs-lookup"><span data-stu-id="62c96-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="62c96-122">您會看到每隔 10 秒寫入的記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="62c96-122">You see a log entry written every 10 seconds.</span></span>
   
    ![檢視記錄檔以確認函式可運作](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="62c96-124">新增訊息佇列輸出繫結</span><span class="sxs-lookup"><span data-stu-id="62c96-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="62c96-125">在 [整合] 索引標籤上，選擇 [新增輸出] > [Azure 佇列儲存體] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="62c96-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![新增觸發計時器函式](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="62c96-127">輸入 `myQueueItem` 做為 [訊息參數名稱] 以及輸入 `functions-bindings` 做為 [佇列名稱]，選取現有的 [儲存體帳戶連線]，或按一下 [新增] 以建立儲存體帳戶連線，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="62c96-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![建立儲存體佇列的輸出繫結](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="62c96-129">回到 [開發] 索引標籤，將下列程式碼附加至函式︰</span><span class="sxs-lookup"><span data-stu-id="62c96-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="62c96-130">找出 if 陳述式 (大約在函式的第 9 行)，並在該陳述式之後插入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="62c96-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="62c96-131">此程式碼會建立 **myQueueItem**，並將其 [時間] 屬性設定為目前的 timeStamp。</span><span class="sxs-lookup"><span data-stu-id="62c96-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="62c96-132">然後，它會將新的佇列項目新增至內容的 **myQueueItem** 繫結。</span><span class="sxs-lookup"><span data-stu-id="62c96-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="62c96-133">按一下 [儲存並執行]。</span><span class="sxs-lookup"><span data-stu-id="62c96-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="62c96-134">使用儲存體總管來檢視儲存體更新</span><span class="sxs-lookup"><span data-stu-id="62c96-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="62c96-135">您可以檢視您所建立的佇列中的訊息，以確認您的函式運作正常。</span><span class="sxs-lookup"><span data-stu-id="62c96-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="62c96-136">您可以使用 Visual Studio 中的雲端總管連接到您的儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="62c96-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="62c96-137">不過，透過入口網站即可輕鬆使用 Microsoft Azure 儲存體總管連接到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c96-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="62c96-138">在 [整合] 索引標籤中，按一下您的佇列輸出繫結 > [文件]，然後取消隱儲存體帳戶的藏連接字串並複製該值。</span><span class="sxs-lookup"><span data-stu-id="62c96-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="62c96-139">您可以使用此值來連接到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="62c96-139">You use this value to connect to your storage account.</span></span>

    ![下載 Azure 儲存體總管](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="62c96-141">如果您還沒有這麼做，請下載並安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com)。</span><span class="sxs-lookup"><span data-stu-id="62c96-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="62c96-142">在儲存體總管中，按一下連接到 Azure 儲存體圖示，在欄位中貼上連接字串，並完成精靈。</span><span class="sxs-lookup"><span data-stu-id="62c96-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![儲存體總管新增連接](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="62c96-144">在 [本機和附加] 之下，展開 [儲存體帳戶] > 您的儲存體帳戶 > [佇列] > [functions-bindings]，並確認訊息會寫入佇列。</span><span class="sxs-lookup"><span data-stu-id="62c96-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![佇列中的訊息檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="62c96-146">如果佇列不存在或是空的，很可能是您的函式繫結或程式碼有問題。</span><span class="sxs-lookup"><span data-stu-id="62c96-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="62c96-147">建立可從佇列讀取訊息的函式</span><span class="sxs-lookup"><span data-stu-id="62c96-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="62c96-148">您已將訊息新增至佇列，您可以建立另一個函式，以便從佇列讀取訊息並將訊息永久寫入 Azure 儲存體資料表。</span><span class="sxs-lookup"><span data-stu-id="62c96-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="62c96-149">按一下 [新增函式] > [QueueTrigger-CSharp]。</span><span class="sxs-lookup"><span data-stu-id="62c96-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="62c96-150">將函式命名為 `FunctionsBindingsDemo2`，在 [佇列名稱] 欄位中輸入 **functions-bindings**，選取現有的儲存體帳戶或加以建立，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="62c96-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![新增輸出佇列計時器函式](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="62c96-152">(選擇性) 您可以如先前一樣在儲存體總管中檢視新的佇列，以確認新的函式運作正常。</span><span class="sxs-lookup"><span data-stu-id="62c96-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="62c96-153">您也可以使用 Visual Studio 中的雲端總管。</span><span class="sxs-lookup"><span data-stu-id="62c96-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="62c96-154">(選擇性) 重新整理 **functions-bindings** 佇列，並請注意已從佇列中移除項目。</span><span class="sxs-lookup"><span data-stu-id="62c96-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="62c96-155">發生移除的原因是函式已繫結至 **functions-bindings** 佇列做為輸入觸發程序，而且此函式會讀取佇列。</span><span class="sxs-lookup"><span data-stu-id="62c96-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="62c96-156">新增資料表輸出繫結</span><span class="sxs-lookup"><span data-stu-id="62c96-156">Add a table output binding</span></span>

1. <span data-ttu-id="62c96-157">在 FunctionsBindingsDemo2 中，按一下 [整合] > [新增輸出] > [Azure 資料表儲存體] > [選取]。</span><span class="sxs-lookup"><span data-stu-id="62c96-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![將繫結新增至 Azure 儲存體資料表](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="62c96-159">輸入 `functionbindings` 做為 [資料表名稱] 以及輸入 `myTable` 做為 [資料表參數名稱]，選擇 [儲存體帳戶連線] 或建立新的連線，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="62c96-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![設定儲存體資料表繫結](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="62c96-161">在 [開發] 索引標籤中，以下列程式碼取代現有的函式程式碼︰</span><span class="sxs-lookup"><span data-stu-id="62c96-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
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
        
        // Add the item to the table binding collection.
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
    <span data-ttu-id="62c96-162">**TableItem** 類別代表儲存體資料表中的資料列，而且您將此項目新增至 **TableItem** 物件的 `myTable` 集合。</span><span class="sxs-lookup"><span data-stu-id="62c96-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="62c96-163">您必須設定 **PartitionKey** 和 **RowKey** 屬性，才能插入資料表中。</span><span class="sxs-lookup"><span data-stu-id="62c96-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="62c96-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="62c96-164">Click **Save**.</span></span>  <span data-ttu-id="62c96-165">(選擇性) 您可以在儲存體總管或 Visual Studio 雲端總管中檢視資料表，以確認此函式運作正常。</span><span class="sxs-lookup"><span data-stu-id="62c96-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="62c96-166">(選擇性) 在儲存體總管中您的儲存體帳戶中，展開 [資料表] >  [functionsbindings]，並確認資料列已新增到資料表。</span><span class="sxs-lookup"><span data-stu-id="62c96-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="62c96-167">您可以在 Visual Studio 的雲端總管中執行相同作業。</span><span class="sxs-lookup"><span data-stu-id="62c96-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![資料表中的資料列檢視](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="62c96-169">如果資料表不存在或是空的，很可能是您的函式繫結或程式碼有問題。</span><span class="sxs-lookup"><span data-stu-id="62c96-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="62c96-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62c96-170">Next steps</span></span>
<span data-ttu-id="62c96-171">如需 Azure Functions 的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="62c96-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="62c96-172">Azure Functions 開發人員參考</span><span class="sxs-lookup"><span data-stu-id="62c96-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="62c96-173">可供程式設計人員撰寫函數程式碼及定義觸發程序和繫結時參考。</span><span class="sxs-lookup"><span data-stu-id="62c96-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="62c96-174">測試 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="62c96-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="62c96-175">說明可用於測試函式的各種工具和技巧。</span><span class="sxs-lookup"><span data-stu-id="62c96-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="62c96-176">如何調整 Azure 函式</span><span class="sxs-lookup"><span data-stu-id="62c96-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="62c96-177">討論 Azure Functions 可用的服務方案，包括使用情況主控方案，以及如何選擇正確的方案。</span><span class="sxs-lookup"><span data-stu-id="62c96-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

