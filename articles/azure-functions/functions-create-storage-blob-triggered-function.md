---
title: "在 Azure Blob 儲存體所觸發的函式 aaaCreate |Microsoft 文件"
description: "使用 Azure 函式 toocreate 無伺服器的函式項目所叫用加入 tooAzure Blob 儲存體。"
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="7b61d-103">建立 Azure Blob 儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="7b61d-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="7b61d-104">了解如何 toocreate 檔案時所觸發的函式上傳 tooor 在 Azure Blob 儲存體中更新。</span><span class="sxs-lookup"><span data-stu-id="7b61d-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="7b61d-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b61d-106">Prerequisites</span></span>

+ <span data-ttu-id="7b61d-107">下載並安裝 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="7b61d-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="7b61d-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b61d-108">An Azure subscription.</span></span> <span data-ttu-id="7b61d-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="7b61d-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="7b61d-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="7b61d-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="7b61d-112">接下來，您會在 hello 新函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="7b61d-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="7b61d-113">建立由 Blob 儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="7b61d-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="7b61d-114">展開您的函式應用程式，然後按一下 hello  **+** 太下一步按鈕**函式**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="7b61d-115">如果 hello 函式應用程式中的第一個函式，請選取**自訂函式**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="7b61d-116">這會顯示 hello 組完整的函式樣板。</span><span class="sxs-lookup"><span data-stu-id="7b61d-116">This displays hello complete set of function templates.</span></span>

    ![在 Azure 入口網站的 hello 函式 [快速入門] 頁面](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="7b61d-118">選取 hello **BlobTrigger**您想要的語言，以及使用 hello 類似設定 hello 表中所指定的範本。</span><span class="sxs-lookup"><span data-stu-id="7b61d-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![建立 hello Blob 儲存體觸發函式。](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="7b61d-120">設定</span><span class="sxs-lookup"><span data-stu-id="7b61d-120">Setting</span></span> | <span data-ttu-id="7b61d-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="7b61d-121">Suggested value</span></span> | <span data-ttu-id="7b61d-122">說明</span><span class="sxs-lookup"><span data-stu-id="7b61d-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="7b61d-123">**路徑**</span><span class="sxs-lookup"><span data-stu-id="7b61d-123">**Path**</span></span>   | <span data-ttu-id="7b61d-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="7b61d-124">mycontainer/{name}</span></span>    | <span data-ttu-id="7b61d-125">受監視 Blob 儲存體中的位置。</span><span class="sxs-lookup"><span data-stu-id="7b61d-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="7b61d-126">hello hello blob 檔案名稱傳入 hello 繫結作為 hello_名稱_參數。</span><span class="sxs-lookup"><span data-stu-id="7b61d-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="7b61d-127">**儲存體帳戶連線**</span><span class="sxs-lookup"><span data-stu-id="7b61d-127">**Storage account connection**</span></span> | <span data-ttu-id="7b61d-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="7b61d-128">AzureWebJobStorage</span></span> | <span data-ttu-id="7b61d-129">您可以使用應用程式的函式，已經使用 hello 儲存體帳戶連接或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="7b61d-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="7b61d-130">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="7b61d-130">**Name your function**</span></span> | <span data-ttu-id="7b61d-131">函式應用程式中的唯一名稱</span><span class="sxs-lookup"><span data-stu-id="7b61d-131">Unique in your function app</span></span> | <span data-ttu-id="7b61d-132">這個由 blob 所觸發之函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="7b61d-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="7b61d-133">按一下**建立**toocreate 您的函式。</span><span class="sxs-lookup"><span data-stu-id="7b61d-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="7b61d-134">接下來，您連接 tooyour Azure 儲存體帳戶，並建立 hello **mycontainer**容器。</span><span class="sxs-lookup"><span data-stu-id="7b61d-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="7b61d-135">建立 hello 容器</span><span class="sxs-lookup"><span data-stu-id="7b61d-135">Create hello container</span></span>

1. <span data-ttu-id="7b61d-136">在您的函式中，按一下 [整合]，展開 [文件]，然後複製**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="7b61d-137">您使用這些認證 tooconnect toohello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b61d-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="7b61d-138">如果您已連接儲存體帳戶，略過 toostep 4。</span><span class="sxs-lookup"><span data-stu-id="7b61d-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![收到 hello 儲存體帳戶的連接認證。](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="7b61d-140">執行 hello [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，請按一下 hello 連接 hello 左邊的圖示，請選擇**使用儲存體帳戶名稱和金鑰**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![執行 hello 儲存體帳戶總管工具。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="7b61d-142">輸入 hello**帳戶名稱**和**帳戶金鑰**從步驟 1 中，按一下 **下一步**然後**連接**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![輸入 hello 儲存體認證和連接。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="7b61d-144">展開 hello 附加儲存體帳戶，以滑鼠右鍵按一下**Blob 容器**，按一下 **建立 blob 容器**，型別`mycontainer`，然後按下 enter。</span><span class="sxs-lookup"><span data-stu-id="7b61d-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![建立儲存體佇列。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="7b61d-146">有 blob 容器之後，您可以上傳檔案 toohello 容器來測試 hello 函式。</span><span class="sxs-lookup"><span data-stu-id="7b61d-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="7b61d-147">測試 hello 函式</span><span class="sxs-lookup"><span data-stu-id="7b61d-147">Test hello function</span></span>

1. <span data-ttu-id="7b61d-148">在 hello Azure 入口網站，瀏覽 tooyour 函式展開 hello**記錄**底部 hello hello 頁面，並確定該記錄檔資料流不已暫停。</span><span class="sxs-lookup"><span data-stu-id="7b61d-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="7b61d-149">在儲存體總管中，依序展開您的儲存體帳戶、[Blob 容器] 和 [mycontainer]。</span><span class="sxs-lookup"><span data-stu-id="7b61d-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="7b61d-150">依序按一下 [上傳] 和 [上傳檔案...]。</span><span class="sxs-lookup"><span data-stu-id="7b61d-150">Click **Upload** and then **Upload files...**.</span></span>

    ![上傳檔案 toohello blob 容器。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="7b61d-152">在 hello**將檔案上傳**對話方塊方塊中，按一下 hello**檔案**欄位。</span><span class="sxs-lookup"><span data-stu-id="7b61d-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="7b61d-153">瀏覽 tooa 檔案儲存在本機電腦，例如映像檔、 選取它，然後按一下**開啟**然後**上傳**。</span><span class="sxs-lookup"><span data-stu-id="7b61d-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="7b61d-154">返回 tooyour 函數記錄檔，並確認該 hello blob 的讀取。</span><span class="sxs-lookup"><span data-stu-id="7b61d-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Hello 記錄檔中檢視訊息。](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="7b61d-156">當函式應用程式執行 hello 預設耗用量計劃時，可能會觸發函式的總 tooseveral hello 已加入或更新的 blob 和 hello 之間的分鐘的延遲。</span><span class="sxs-lookup"><span data-stu-id="7b61d-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="7b61d-157">如果您不想讓 Blob 所觸發的函式延遲太久，請考慮在 App Service 方案執行函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b61d-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="7b61d-158">清除資源</span><span class="sxs-lookup"><span data-stu-id="7b61d-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="7b61d-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b61d-159">Next steps</span></span>

<span data-ttu-id="7b61d-160">您已建立 Blob 儲存體 blob 加入 tooor 更新時執行的函式。</span><span class="sxs-lookup"><span data-stu-id="7b61d-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7b61d-161">如需 Blob 儲存體觸發程序的詳細資訊，請參閱 [Azure Functions Blob 儲存體繫結](functions-bindings-storage-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="7b61d-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
