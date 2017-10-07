---
title: "在 Azure 佇列訊息所觸發的函式 aaaCreate |Microsoft 文件"
description: "使用 Azure 函式 toocreate 無伺服器的函式會叫用的訊息提交 tooan Azure 儲存體佇列。"
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
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="0a432-103">建立 Azure 佇列儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="0a432-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="0a432-104">了解如何 toocreate 郵件時所觸發的函式提交 tooan Azure 儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="0a432-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="0a432-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="0a432-106">Prerequisites</span></span>

- <span data-ttu-id="0a432-107">下載並安裝 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="0a432-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="0a432-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a432-108">An Azure subscription.</span></span> <span data-ttu-id="0a432-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="0a432-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="0a432-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="0a432-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="0a432-112">接下來，您會在 hello 新函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="0a432-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="0a432-113">建立由佇列觸發的函式</span><span class="sxs-lookup"><span data-stu-id="0a432-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="0a432-114">展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。</span><span class="sxs-lookup"><span data-stu-id="0a432-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="0a432-115">如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。</span><span class="sxs-lookup"><span data-stu-id="0a432-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="0a432-116">這會顯示 hello 組完整的函式樣板。</span><span class="sxs-lookup"><span data-stu-id="0a432-116">This displays hello complete set of function templates.</span></span>

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="0a432-118">選取 hello **QueueTrigger**您想要的語言，以及使用 hello 類似設定 hello 表中所指定的範本。</span><span class="sxs-lookup"><span data-stu-id="0a432-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![建立 hello 儲存觸發佇列函式。](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="0a432-120">設定</span><span class="sxs-lookup"><span data-stu-id="0a432-120">Setting</span></span> | <span data-ttu-id="0a432-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="0a432-121">Suggested value</span></span> | <span data-ttu-id="0a432-122">說明</span><span class="sxs-lookup"><span data-stu-id="0a432-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="0a432-123">**佇列名稱**</span><span class="sxs-lookup"><span data-stu-id="0a432-123">**Queue name**</span></span>   | <span data-ttu-id="0a432-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="0a432-124">myqueue-items</span></span>    | <span data-ttu-id="0a432-125">名稱的 hello 佇列 tooconnect tooin 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a432-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="0a432-126">**儲存體帳戶連線**</span><span class="sxs-lookup"><span data-stu-id="0a432-126">**Storage account connection**</span></span> | <span data-ttu-id="0a432-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="0a432-127">AzureWebJobStorage</span></span> | <span data-ttu-id="0a432-128">您可以使用應用程式的函式，已經使用 hello 儲存體帳戶連接或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="0a432-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="0a432-129">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="0a432-129">**Name your function**</span></span> | <span data-ttu-id="0a432-130">函式應用程式中的唯一名稱</span><span class="sxs-lookup"><span data-stu-id="0a432-130">Unique in your function app</span></span> | <span data-ttu-id="0a432-131">這個由佇列所觸發之函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="0a432-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="0a432-132">按一下**建立**toocreate 您的函式。</span><span class="sxs-lookup"><span data-stu-id="0a432-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="0a432-133">接下來，您連接 tooyour Azure 儲存體帳戶，並建立 hello **myqueue 項目**儲存體佇列。</span><span class="sxs-lookup"><span data-stu-id="0a432-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="0a432-134">建立 hello 佇列</span><span class="sxs-lookup"><span data-stu-id="0a432-134">Create hello queue</span></span>

1. <span data-ttu-id="0a432-135">在您的函式中，按一下 [整合]，展開 [文件]，然後複製**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="0a432-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="0a432-136">您使用這些認證 tooconnect toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0a432-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="0a432-137">如果您已連接儲存體帳戶，略過 toostep 4。</span><span class="sxs-lookup"><span data-stu-id="0a432-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![收到 hello 儲存體帳戶的連接認證。](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="0a432-139">v</span><span class="sxs-lookup"><span data-stu-id="0a432-139">v</span></span>

1. <span data-ttu-id="0a432-140">執行 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，請按一下 hello 連接 hello 左邊的圖示，請選擇**使用儲存體帳戶名稱和金鑰**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="0a432-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![執行 hello 儲存體帳戶總管工具。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="0a432-142">輸入 hello**帳戶名稱**和**帳戶金鑰**從步驟 1 中，按一下 **下一步**然後**連接**。</span><span class="sxs-lookup"><span data-stu-id="0a432-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![輸入 hello 儲存體認證和連接。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="0a432-144">展開 hello 附加儲存體帳戶，以滑鼠右鍵按一下**佇列**，按一下 **建立佇列**，型別`myqueue-items`，然後按下 enter。</span><span class="sxs-lookup"><span data-stu-id="0a432-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![建立儲存體佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="0a432-146">您已經有儲存體佇列，您可以藉由新增訊息 toohello 佇列測試 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="0a432-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="0a432-147">測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="0a432-147">Test hello function</span></span>

1. <span data-ttu-id="0a432-148">在 hello Azure 入口網站，瀏覽 tooyour 函式展開 hello**記錄**底部 hello hello 頁面，並確定該記錄檔資料流不已暫停。</span><span class="sxs-lookup"><span data-stu-id="0a432-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="0a432-149">在儲存體總管中，依序展開您的儲存體帳戶、[佇列] 和 [myqueue-items]，然後按一下 [新增訊息]。</span><span class="sxs-lookup"><span data-stu-id="0a432-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![新增訊息 toohello 佇列。](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="0a432-151">將您的 "Hello World!" 輸入</span><span class="sxs-lookup"><span data-stu-id="0a432-151">Type your "Hello World!"</span></span> <span data-ttu-id="0a432-152">在 [訊息文字] 訊息中，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0a432-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="0a432-153">等候數秒鐘，然後返回 tooyour 函數記錄檔並確認已從 hello 佇列讀取該 hello 新訊息。</span><span class="sxs-lookup"><span data-stu-id="0a432-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="0a432-155">在 儲存體總管 中，按一下 **重新整理**並確認該 hello 訊息已處理，而且已不存在於 hello 佇列。</span><span class="sxs-lookup"><span data-stu-id="0a432-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0a432-156">清除資源</span><span class="sxs-lookup"><span data-stu-id="0a432-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="0a432-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a432-157">Next steps</span></span>

<span data-ttu-id="0a432-158">您已建立執行時加入 tooa 儲存體佇列訊息的函式。</span><span class="sxs-lookup"><span data-stu-id="0a432-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="0a432-159">如需佇列儲存體觸發程序的詳細資訊，請參閱 [Azure Functions 儲存體佇列繫結](functions-bindings-storage-queue.md)。</span><span class="sxs-lookup"><span data-stu-id="0a432-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>