---
title: "在 Azure 中建立由佇列訊息所觸發的函式 | Microsoft Docs"
description: "使用 Azure Functions 來建立無伺服器函式，並讓此函式由提交至 Azure 儲存體佇列的訊息來叫用。"
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 57c59273a9da55f3e357764c522b444ae2d73cb5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="add-messages-to-an-azure-storage-queue-using-functions"></a><span data-ttu-id="b7fc9-103">使用 Functions 在 Azure 儲存體佇列中新增訊息</span><span class="sxs-lookup"><span data-stu-id="b7fc9-103">Add messages to an Azure Storage queue using Functions</span></span>

<span data-ttu-id="b7fc9-104">在 Azure Functions 中，輸入和輸出繫結會提供宣告式方法，以便從函式連線到外部服務資料。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-104">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="b7fc9-105">在本主題中，請學習如何新增會將訊息傳送至 Azure 佇列儲存體的輸出繫結，以更新現有函式。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-105">In this topic, learn how to update an existing function by adding an output binding that sends messages to Azure Queue storage.</span></span>  

![檢視記錄中的訊息。](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a><span data-ttu-id="b7fc9-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b7fc9-107">Prerequisites</span></span> 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* <span data-ttu-id="b7fc9-108">安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-108">Install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <span data-ttu-id="b7fc9-109"><a name="add-binding"></a>新增輸出繫結</span><span class="sxs-lookup"><span data-stu-id="b7fc9-109"><a name="add-binding"></a>Add an output binding</span></span>
 
1. <span data-ttu-id="b7fc9-110">展開函式應用程式和函式。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-110">Expand both your function app and your function.</span></span>

2. <span data-ttu-id="b7fc9-111">選取 [整合] 和 [+ 新輸出]，然後選擇 [Azure 佇列儲存體] 和 [選取]。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-111">Select **Integrate** and **+ New output**, then choose **Azure Queue storage** and choose **Select**.</span></span>
    
    ![在 Azure 入口網站中對函式新增佇列儲存體輸出繫結。](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. <span data-ttu-id="b7fc9-113">使用表格中所指定的設定︰</span><span class="sxs-lookup"><span data-stu-id="b7fc9-113">Use the settings as specified in the table:</span></span> 

    ![在 Azure 入口網站中對函式新增佇列儲存體輸出繫結。](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | <span data-ttu-id="b7fc9-115">設定</span><span class="sxs-lookup"><span data-stu-id="b7fc9-115">Setting</span></span>      |  <span data-ttu-id="b7fc9-116">建議的值</span><span class="sxs-lookup"><span data-stu-id="b7fc9-116">Suggested value</span></span>   | <span data-ttu-id="b7fc9-117">說明</span><span class="sxs-lookup"><span data-stu-id="b7fc9-117">Description</span></span>                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | <span data-ttu-id="b7fc9-118">**佇列名稱**</span><span class="sxs-lookup"><span data-stu-id="b7fc9-118">**Queue name**</span></span>   | <span data-ttu-id="b7fc9-119">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="b7fc9-119">myqueue-items</span></span>    | <span data-ttu-id="b7fc9-120">儲存體帳戶中的連線目標佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-120">The name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="b7fc9-121">**儲存體帳戶連線**</span><span class="sxs-lookup"><span data-stu-id="b7fc9-121">**Storage account connection**</span></span> | <span data-ttu-id="b7fc9-122">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="b7fc9-122">AzureWebJobStorage</span></span> | <span data-ttu-id="b7fc9-123">您可以使用應用程式函式已在使用的儲存體帳戶連線，或建立新的連線。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-123">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="b7fc9-124">**訊息參數名稱**</span><span class="sxs-lookup"><span data-stu-id="b7fc9-124">**Message parameter name**</span></span> | <span data-ttu-id="b7fc9-125">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="b7fc9-125">outputQueueItem</span></span> | <span data-ttu-id="b7fc9-126">輸出繫結參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-126">The name of the output binding parameter.</span></span> | 

4. <span data-ttu-id="b7fc9-127">按一下 [儲存] 來新增繫結。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-127">Click **Save** to add the binding.</span></span>
 
<span data-ttu-id="b7fc9-128">您已定義了輸出繫結，接下來您需要將程式碼更新為使用繫結來對佇列新增訊息。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-128">Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.</span></span>  

## <a name="update-the-function-code"></a><span data-ttu-id="b7fc9-129">更新函式程式碼</span><span class="sxs-lookup"><span data-stu-id="b7fc9-129">Update the function code</span></span>

1. <span data-ttu-id="b7fc9-130">選取函式以在編輯器中顯示函式程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-130">Select your function to display the function code in the editor.</span></span> 

2. <span data-ttu-id="b7fc9-131">若為 C# 函式，請依下面的方式更新函式定義，以新增 **outputQueueItem** 儲存體繫結參數。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-131">For a C# function, update your function definition as follows to add the **outputQueueItem** storage binding parameter.</span></span> <span data-ttu-id="b7fc9-132">若為 JavaScript 函式，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-132">Skip this step for a JavaScript function.</span></span>

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. <span data-ttu-id="b7fc9-133">在方法傳回前，對函式新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-133">Add the following code to the function just before the method returns.</span></span> <span data-ttu-id="b7fc9-134">請使用您的函式語言所適用的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-134">Use the appropriate snippet for the language of your function.</span></span>

    ```javascript
    context.bindings.outputQueueItem = "Name passed to the function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed to the function: " + name);     
    ```

4. <span data-ttu-id="b7fc9-135">選取 [儲存] 來儲存變更。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-135">Select **Save** to save changes.</span></span>

<span data-ttu-id="b7fc9-136">傳遞至 HTTP 觸發程序的值會包含在新增至佇列的訊息中。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-136">The value passed to the HTTP trigger is included in a message added to the queue.</span></span>
 
## <a name="test-the-function"></a><span data-ttu-id="b7fc9-137">測試函式</span><span class="sxs-lookup"><span data-stu-id="b7fc9-137">Test the function</span></span> 

1. <span data-ttu-id="b7fc9-138">儲存程式碼的變更後，選取 [執行]。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-138">After the code changes are saved, select **Run**.</span></span> 

    ![在 Azure 入口網站中對函式新增佇列儲存體輸出繫結。](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. <span data-ttu-id="b7fc9-140">檢查記錄以確定函式已成功。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-140">Check the logs to make sure that the function succeeded.</span></span> <span data-ttu-id="b7fc9-141">您第一次使用輸出繫結時，Functions 執行階段會在儲存體帳戶中建立名為 **outqueue** 的新佇列。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-141">A new queue named **outqueue** is created in your Storage account by the Functions runtime when the output binding is first used.</span></span>

<span data-ttu-id="b7fc9-142">接下來，您可以連線到儲存體帳戶，以便驗證新佇列和您對佇列新增的訊息。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-142">Next, you can connect to your storage account to verify the new queue and the message you added to it.</span></span> 

## <a name="connect-to-the-queue"></a><span data-ttu-id="b7fc9-143">連線至佇列</span><span class="sxs-lookup"><span data-stu-id="b7fc9-143">Connect to the queue</span></span>

<span data-ttu-id="b7fc9-144">如果您已經安裝儲存體總管並將它連線至儲存體帳戶，請略過前三個步驟。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-144">Skip the first three steps if you have already installed Storage Explorer and connected it to your storage account.</span></span>    

1. <span data-ttu-id="b7fc9-145">在您的函式中，選擇 [整合] 和新的 **Azure 佇列儲存體**輸出繫結，然後展開 [文件]。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-145">In your function, choose **Integrate** and the new **Azure Queue storage** output binding, then expand **Documentation**.</span></span> <span data-ttu-id="b7fc9-146">複製**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-146">Copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="b7fc9-147">您會使用這些認證來連線至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-147">You use these credentials to connect to the storage account.</span></span>
 
    ![取得儲存體帳戶的連線認證。](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. <span data-ttu-id="b7fc9-149">執行 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，選取左側的 [連線] 圖示，選擇 [使用儲存體帳戶名稱和金鑰]，然後選取 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-149">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, select the connect icon on the left, choose **Use a storage account name and key**, and select **Next**.</span></span>

    ![執行「儲存體帳戶總管」工具。](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. <span data-ttu-id="b7fc9-151">將步驟 1 中的**帳戶名稱**和**帳戶金鑰**貼到其對應的欄位中，然後選取 [下一步] 和 [連線]。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-151">Paste the **Account name** and **Account key** from step 1 into their corresponding fields, then select **Next**, and **Connect**.</span></span> 
  
    ![貼上儲存體認證並連線。](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. <span data-ttu-id="b7fc9-153">展開連結的儲存體帳戶，展開 [佇列]，並確認有名為 **myqueue-items** 的佇列存在。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-153">Expand the attached storage account, expand **Queues** and verify that a queue named **myqueue-items** exists.</span></span> <span data-ttu-id="b7fc9-154">您也應該會看到佇列中已有訊息。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-154">You should also see a message already in the queue.</span></span>  
 
    ![建立儲存體佇列。](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a><span data-ttu-id="b7fc9-156">清除資源</span><span class="sxs-lookup"><span data-stu-id="b7fc9-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="b7fc9-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b7fc9-157">Next steps</span></span>

<span data-ttu-id="b7fc9-158">您已在現有函式中新增輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-158">You have added an output binding to an existing function.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="b7fc9-159">如需佇列儲存體繫結的詳細資訊，請參閱 [Azure Functions 儲存體佇列繫結](functions-bindings-storage-queue.md)。</span><span class="sxs-lookup"><span data-stu-id="b7fc9-159">For more information about binding to Queue storage, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span> 



