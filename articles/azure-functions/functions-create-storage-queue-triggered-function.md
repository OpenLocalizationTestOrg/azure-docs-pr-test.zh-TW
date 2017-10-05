---
title: "在 Azure 中建立由佇列訊息所觸發的函式 | Microsoft Docs"
description: "使用 Azure Functions 來建立無伺服器函式，並讓此函式由提交至 Azure 儲存體佇列的訊息來叫用。"
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="9e21d-103">建立 Azure 佇列儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="9e21d-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="9e21d-104">了解如何建立函式，並讓此函式在訊息提交至 Azure 儲存體佇列時觸發。</span><span class="sxs-lookup"><span data-stu-id="9e21d-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![檢視記錄中的訊息。](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="9e21d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="9e21d-106">Prerequisites</span></span>

- <span data-ttu-id="9e21d-107">下載並安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="9e21d-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="9e21d-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e21d-108">An Azure subscription.</span></span> <span data-ttu-id="9e21d-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="9e21d-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="9e21d-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="9e21d-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="9e21d-112">接下來，您要在新的函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="9e21d-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="9e21d-113">建立由佇列觸發的函式</span><span class="sxs-lookup"><span data-stu-id="9e21d-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="9e21d-114">展開函式應用程式，然後按一下 [Functions] 旁的 [+] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9e21d-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="9e21d-115">如果這是您函式應用程式中的第一個函式，請選取 [自訂函式]。</span><span class="sxs-lookup"><span data-stu-id="9e21d-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="9e21d-116">這會顯示一組完整的函式範本。</span><span class="sxs-lookup"><span data-stu-id="9e21d-116">This displays the complete set of function templates.</span></span>

    ![Azure 入口網站中的 Functions 快速入門](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="9e21d-118">為您想要的語言選取 **QueueTrigger** 範本，並使用如表格中指定的設定。</span><span class="sxs-lookup"><span data-stu-id="9e21d-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![建立由儲存體佇列所觸發的函式。](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="9e21d-120">設定</span><span class="sxs-lookup"><span data-stu-id="9e21d-120">Setting</span></span> | <span data-ttu-id="9e21d-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="9e21d-121">Suggested value</span></span> | <span data-ttu-id="9e21d-122">說明</span><span class="sxs-lookup"><span data-stu-id="9e21d-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="9e21d-123">**佇列名稱**</span><span class="sxs-lookup"><span data-stu-id="9e21d-123">**Queue name**</span></span>   | <span data-ttu-id="9e21d-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="9e21d-124">myqueue-items</span></span>    | <span data-ttu-id="9e21d-125">儲存體帳戶中的連線目標佇列名稱。</span><span class="sxs-lookup"><span data-stu-id="9e21d-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="9e21d-126">**儲存體帳戶連線**</span><span class="sxs-lookup"><span data-stu-id="9e21d-126">**Storage account connection**</span></span> | <span data-ttu-id="9e21d-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="9e21d-127">AzureWebJobStorage</span></span> | <span data-ttu-id="9e21d-128">您可以使用應用程式函式已在使用的儲存體帳戶連線，或建立新的連線。</span><span class="sxs-lookup"><span data-stu-id="9e21d-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="9e21d-129">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="9e21d-129">**Name your function**</span></span> | <span data-ttu-id="9e21d-130">函式應用程式中的唯一名稱</span><span class="sxs-lookup"><span data-stu-id="9e21d-130">Unique in your function app</span></span> | <span data-ttu-id="9e21d-131">這個由佇列所觸發之函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="9e21d-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="9e21d-132">按一下 [建立] 可建立函式。</span><span class="sxs-lookup"><span data-stu-id="9e21d-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="9e21d-133">接下來，您要連線到 Azure 儲存體帳戶並建立 **myqueue-items** 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="9e21d-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="9e21d-134">建立佇列</span><span class="sxs-lookup"><span data-stu-id="9e21d-134">Create the queue</span></span>

1. <span data-ttu-id="9e21d-135">在您的函式中，按一下 [整合]，展開 [文件]，然後複製**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="9e21d-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="9e21d-136">您會使用這些認證來連線至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e21d-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="9e21d-137">如果您已連線至儲存體帳戶，請跳至步驟 4。</span><span class="sxs-lookup"><span data-stu-id="9e21d-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![取得儲存體帳戶的連線認證。](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="9e21d-139">v</span><span class="sxs-lookup"><span data-stu-id="9e21d-139">v</span></span>

1. <span data-ttu-id="9e21d-140">執行 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，按一下左側的 [連線] 圖示，選擇 [使用儲存體帳戶名稱和金鑰]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9e21d-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![執行「儲存體帳戶總管」工具。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="9e21d-142">輸入從步驟 1 得到的 [帳戶名稱] 和 [帳戶金鑰]，按 [下一步]，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="9e21d-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![輸入儲存體認證和連線。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="9e21d-144">展開連結的儲存體帳戶，以滑鼠右鍵按一下 [佇列]，按一下 [建立佇列]，輸入 `myqueue-items`，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="9e21d-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![建立儲存體佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="9e21d-146">您已擁有儲存體佇列，接下來您可以在佇列中新增訊息以測試函式。</span><span class="sxs-lookup"><span data-stu-id="9e21d-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="9e21d-147">測試函式</span><span class="sxs-lookup"><span data-stu-id="9e21d-147">Test the function</span></span>

1. <span data-ttu-id="9e21d-148">回到 Azure 入口網站，瀏覽至您的函式，展開頁面底部的 [記錄]，並確定記錄串流並未暫停。</span><span class="sxs-lookup"><span data-stu-id="9e21d-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="9e21d-149">在儲存體總管中，依序展開您的儲存體帳戶、[佇列] 和 [myqueue-items]，然後按一下 [新增訊息]。</span><span class="sxs-lookup"><span data-stu-id="9e21d-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![將訊息新增至佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="9e21d-151">將您的 "Hello World!" 輸入</span><span class="sxs-lookup"><span data-stu-id="9e21d-151">Type your "Hello World!"</span></span> <span data-ttu-id="9e21d-152">在 [訊息文字] 訊息中，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9e21d-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="9e21d-153">等候幾秒鐘，然後回到您的函式記錄，並確認系統已從佇列中讀取新訊息。</span><span class="sxs-lookup"><span data-stu-id="9e21d-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![檢視記錄中的訊息。](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="9e21d-155">回到儲存體總管，按一下 [重新整理]，然後確認系統已處理訊息，佇列中已沒有該訊息。</span><span class="sxs-lookup"><span data-stu-id="9e21d-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9e21d-156">清除資源</span><span class="sxs-lookup"><span data-stu-id="9e21d-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="9e21d-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e21d-157">Next steps</span></span>

<span data-ttu-id="9e21d-158">您已建立了函式，並讓它在儲存體佇列中有訊息新增時執行。</span><span class="sxs-lookup"><span data-stu-id="9e21d-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="9e21d-159">如需佇列儲存體觸發程序的詳細資訊，請參閱 [Azure Functions 儲存體佇列繫結](functions-bindings-storage-queue.md)。</span><span class="sxs-lookup"><span data-stu-id="9e21d-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>