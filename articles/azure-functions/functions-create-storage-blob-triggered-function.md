---
title: "在 Azure 中建立由 Blob 儲存體所觸發的函式 | Microsoft Docs"
description: "使用 Azure Functions 來建立無伺服器函式，並讓此函式由新增至 Azure Blob 儲存體的項目來叫用。"
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
ms.openlocfilehash: 1ddd056903b1a2f973a58bd7054ea2b8281607c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="f537e-103">建立 Azure Blob 儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="f537e-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="f537e-104">了解如何建立函式，並讓此函式在檔案上傳至 Azure Blob 儲存體時或 Azure Blob 儲存體中的檔案更新時觸發。</span><span class="sxs-lookup"><span data-stu-id="f537e-104">Learn how to create a function triggered when files are uploaded to or updated in Azure Blob storage.</span></span>

![檢視記錄中的訊息。](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="f537e-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f537e-106">Prerequisites</span></span>

+ <span data-ttu-id="f537e-107">下載並安裝 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="f537e-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="f537e-108">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f537e-108">An Azure subscription.</span></span> <span data-ttu-id="f537e-109">如果您沒有 Azure 訂用帳戶，請在開始前建立[免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="f537e-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="f537e-110">建立 Azure 函數應用程式</span><span class="sxs-lookup"><span data-stu-id="f537e-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![已成功建立函式應用程式。](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="f537e-112">接下來，您要在新的函式應用程式中建立函式。</span><span class="sxs-lookup"><span data-stu-id="f537e-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="f537e-113">建立由 Blob 儲存體所觸發的函式</span><span class="sxs-lookup"><span data-stu-id="f537e-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="f537e-114">展開函式應用程式，然後按一下 [Functions] 旁的 [+] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f537e-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="f537e-115">如果這是您函式應用程式中的第一個函式，請選取 [自訂函式]。</span><span class="sxs-lookup"><span data-stu-id="f537e-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="f537e-116">這會顯示一組完整的函式範本。</span><span class="sxs-lookup"><span data-stu-id="f537e-116">This displays the complete set of function templates.</span></span>

    ![Azure 入口網站中的 Functions 快速入門](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="f537e-118">為您想要的語言選取 **BlobTrigger** 範本，並使用如表格中指定的設定。</span><span class="sxs-lookup"><span data-stu-id="f537e-118">Select the **BlobTrigger** template for your desired language, and use the settings as specified in the table.</span></span>

    ![建立由 Blob 儲存體所觸發的函式。](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="f537e-120">設定</span><span class="sxs-lookup"><span data-stu-id="f537e-120">Setting</span></span> | <span data-ttu-id="f537e-121">建議的值</span><span class="sxs-lookup"><span data-stu-id="f537e-121">Suggested value</span></span> | <span data-ttu-id="f537e-122">說明</span><span class="sxs-lookup"><span data-stu-id="f537e-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="f537e-123">**路徑**</span><span class="sxs-lookup"><span data-stu-id="f537e-123">**Path**</span></span>   | <span data-ttu-id="f537e-124">mycontainer/{name}</span><span class="sxs-lookup"><span data-stu-id="f537e-124">mycontainer/{name}</span></span>    | <span data-ttu-id="f537e-125">受監視 Blob 儲存體中的位置。</span><span class="sxs-lookup"><span data-stu-id="f537e-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="f537e-126">在繫結中，Blob 的檔案名稱會以「名稱」參數的形式來傳遞。</span><span class="sxs-lookup"><span data-stu-id="f537e-126">The file name of the blob is passed in the binding as the _name_ parameter.</span></span>  |
    | <span data-ttu-id="f537e-127">**儲存體帳戶連線**</span><span class="sxs-lookup"><span data-stu-id="f537e-127">**Storage account connection**</span></span> | <span data-ttu-id="f537e-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="f537e-128">AzureWebJobStorage</span></span> | <span data-ttu-id="f537e-129">您可以使用應用程式函式已在使用的儲存體帳戶連線，或建立新的連線。</span><span class="sxs-lookup"><span data-stu-id="f537e-129">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="f537e-130">**函式命名**</span><span class="sxs-lookup"><span data-stu-id="f537e-130">**Name your function**</span></span> | <span data-ttu-id="f537e-131">函式應用程式中的唯一名稱</span><span class="sxs-lookup"><span data-stu-id="f537e-131">Unique in your function app</span></span> | <span data-ttu-id="f537e-132">這個由 blob 所觸發之函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="f537e-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="f537e-133">按一下 [建立] 可建立函式。</span><span class="sxs-lookup"><span data-stu-id="f537e-133">Click **Create** to create your function.</span></span>

<span data-ttu-id="f537e-134">接下來，您要連線到 Azure 儲存體帳戶並建立 **mycontainer** 容器。</span><span class="sxs-lookup"><span data-stu-id="f537e-134">Next, you connect to your Azure Storage account and create the **mycontainer** container.</span></span>

## <a name="create-the-container"></a><span data-ttu-id="f537e-135">建立容器</span><span class="sxs-lookup"><span data-stu-id="f537e-135">Create the container</span></span>

1. <span data-ttu-id="f537e-136">在您的函式中，按一下 [整合]，展開 [文件]，然後複製**帳戶名稱**和**帳戶金鑰**。</span><span class="sxs-lookup"><span data-stu-id="f537e-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="f537e-137">您會使用這些認證來連線至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f537e-137">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="f537e-138">如果您已連線至儲存體帳戶，請跳至步驟 4。</span><span class="sxs-lookup"><span data-stu-id="f537e-138">If you have already connected your storage account, skip to step 4.</span></span>

    ![取得儲存體帳戶的連線認證。](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="f537e-140">執行 [Microsoft Azure 儲存體總管](http://storageexplorer.com/)工具，按一下左側的 [連線] 圖示，選擇 [使用儲存體帳戶名稱和金鑰]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="f537e-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![執行「儲存體帳戶總管」工具。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="f537e-142">輸入從步驟 1 得到的 [帳戶名稱] 和 [帳戶金鑰]，按 [下一步]，然後按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="f537e-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![輸入儲存體認證和連線。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="f537e-144">展開連結的儲存體帳戶，以滑鼠右鍵按一下 [Blob 容器]，按一下 [建立 Blob 容器]，輸入 `mycontainer`，然後按 Enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="f537e-144">Expand the attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![建立儲存體佇列。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="f537e-146">您已擁有 Blob 容器，接下來您可以將檔案上傳至容器以測試函式。</span><span class="sxs-lookup"><span data-stu-id="f537e-146">Now that you have a blob container, you can test the function by uploading a file to the container.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="f537e-147">測試函式</span><span class="sxs-lookup"><span data-stu-id="f537e-147">Test the function</span></span>

1. <span data-ttu-id="f537e-148">回到 Azure 入口網站，瀏覽至您的函式，展開頁面底部的 [記錄]，並確定記錄串流並未暫停。</span><span class="sxs-lookup"><span data-stu-id="f537e-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="f537e-149">在儲存體總管中，依序展開您的儲存體帳戶、[Blob 容器] 和 [mycontainer]。</span><span class="sxs-lookup"><span data-stu-id="f537e-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="f537e-150">依序按一下 [上傳] 和 [上傳檔案...]。</span><span class="sxs-lookup"><span data-stu-id="f537e-150">Click **Upload** and then **Upload files...**.</span></span>

    ![將檔案上傳至 Blob 容器。](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="f537e-152">在 [上傳檔案] 對話方塊中，按一下 [檔案] 欄位。</span><span class="sxs-lookup"><span data-stu-id="f537e-152">In the **Upload files** dialog box, click the **Files** field.</span></span> <span data-ttu-id="f537e-153">瀏覽至本機電腦上的檔案 (例如影像檔)，加以選取，然後依序按一下 [開啟] 和 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="f537e-153">Browse to a file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="f537e-154">返回您的函式記錄，並確認系統已讀取 Blob。</span><span class="sxs-lookup"><span data-stu-id="f537e-154">Go back to your function logs and verify that the blob has been read.</span></span>

   ![檢視記錄中的訊息。](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="f537e-156">當函式應用程式以預設的取用方案執行時，從有 Blob 新增或更新到系統觸發函式，中間可能會延遲好幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="f537e-156">When your function app runs in the default Consumption plan, there may be a delay of up to several minutes between the blob being added or updated and the function being triggered.</span></span> <span data-ttu-id="f537e-157">如果您不想讓 Blob 所觸發的函式延遲太久，請考慮在 App Service 方案執行函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="f537e-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f537e-158">清除資源</span><span class="sxs-lookup"><span data-stu-id="f537e-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f537e-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f537e-159">Next steps</span></span>

<span data-ttu-id="f537e-160">您已建立了函式，並讓它在 Blob 儲存體中有 Blob 新增或更新時執行。</span><span class="sxs-lookup"><span data-stu-id="f537e-160">You have created a function that runs when a blob is added to or updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="f537e-161">如需 Blob 儲存體觸發程序的詳細資訊，請參閱 [Azure Functions Blob 儲存體繫結](functions-bindings-storage-blob.md)。</span><span class="sxs-lookup"><span data-stu-id="f537e-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
