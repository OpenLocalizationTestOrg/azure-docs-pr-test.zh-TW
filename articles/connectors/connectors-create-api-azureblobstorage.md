---
title: "在您的 Logic Apps 中新增 Azure Blob 儲存體連接器 | Microsoft Docs"
description: "在邏輯應用程式中開始使用及設定 Azure Blob 儲存體連接器"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: bc7908868828bd1628633cf9e57f8c44f8000827
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="f0d6d-103">在邏輯應用程式中使用 Azure Blob 儲存體連接器</span><span class="sxs-lookup"><span data-stu-id="f0d6d-103">Use the Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="f0d6d-104">您可以使用 Azure Blob 儲存體連接器來上傳、更新、取得及刪除您儲存體帳戶中的 Blob，所有這些操作都在一個邏輯應用程式內完成。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-104">Use the Azure Blob storage connector to upload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="f0d6d-105">您可以利用 Azure Blob 儲存體來：</span><span class="sxs-lookup"><span data-stu-id="f0d6d-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="f0d6d-106">上傳新專案或取得最近更新的檔案以建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="f0d6d-107">使用動作來取得檔案中繼資料、刪除檔案、複製檔案和進行其他作業。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-107">Use actions to get file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="f0d6d-108">例如，當 Azure 網站中的工具更新時 (觸發程序)，便更新 Blob 儲存體中的檔案 (動作)。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="f0d6d-109">本主題說明如何在邏輯應用程式中使用 Blob 儲存體連接器。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-109">This topic shows you how to use the blob storage connector in a logic app.</span></span>

<span data-ttu-id="f0d6d-110">若要深入瞭解 Logic Apps，請參閱[什麼是邏輯應用程式](../logic-apps/logic-apps-what-are-logic-apps.md)以及[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="f0d6d-111">若要深入瞭解 Logic Apps，請參閱[什麼是邏輯應用程式](../logic-apps/logic-apps-what-are-logic-apps.md)以及[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-blob-storage"></a><span data-ttu-id="f0d6d-112">連線至 Azure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="f0d6d-112">Connect to Azure blob storage</span></span>
<span data-ttu-id="f0d6d-113">您必須先建立與服務的「連線」，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="f0d6d-114">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f0d6d-115">例如，若要連線至儲存體帳戶，您得先建立 Blob 儲存體連線。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-115">For example, to connect to a storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="f0d6d-116">若要建立連線，請輸入平常用來存取所連線服務的認證。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-116">To create a connection, enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="f0d6d-117">因此，請在 Azure 儲存體中，輸入儲存體帳戶的認證以建立連線。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-117">So with Azure storage, enter the credentials to your storage account to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="f0d6d-118">建立連線</span><span class="sxs-lookup"><span data-stu-id="f0d6d-118">Create the connection</span></span>
> [!INCLUDE [Create a connection to Azure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="f0d6d-119">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="f0d6d-119">Use a trigger</span></span>
<span data-ttu-id="f0d6d-120">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-120">This connector does not have any triggers.</span></span> <span data-ttu-id="f0d6d-121">請使用其他觸發程序來啟動邏輯應用程式，例如循環觸發程序、HTTP Webhook 觸發程序、其他連接器適用的觸發程序等等。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-121">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="f0d6d-122">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="f0d6d-123">使用動作</span><span class="sxs-lookup"><span data-stu-id="f0d6d-123">Use an action</span></span>
<span data-ttu-id="f0d6d-124">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-124">An action is an operation carried out by the workflow defined in a logic app.</span></span>

1. <span data-ttu-id="f0d6d-125">選取加號。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-125">Select the plus sign.</span></span> <span data-ttu-id="f0d6d-126">您會看到幾個選擇︰[新增動作]、[新增條件] 或其中一個 [其他] 選項。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="f0d6d-127">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="f0d6d-128">在文字方塊中，輸入「blob」以取得所有可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-128">In the text box, type “blob” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="f0d6d-129">在我們的範例中，選擇 [AzureBlob - 使用路徑取得檔案中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="f0d6d-130">如果連線已存在，請選取 [...](顯示選擇器) 按鈕來選取檔案。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-130">If a connection already exists, then select the **...** (Show Picker) button to select a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="f0d6d-131">如果系統提示您輸入連線資訊，請輸入詳細資料以建立連線。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="f0d6d-132">本主題的[建立連線](connectors-create-api-azureblobstorage.md#create-the-connection)一節會說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-132">[Create the connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f0d6d-133">在此範例中，我們會取得檔案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-133">In this example, we get the metadata of a file.</span></span> <span data-ttu-id="f0d6d-134">若要查看中繼資料，請新增另一個動作，以使用另一個連接器建立新檔案。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-134">To see the metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="f0d6d-135">例如，新增 OneDrive 動作，以根據中繼資料建立新的「測試」檔案。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-135">For example, add a OneDrive action that creates a new "test" file based on the metadata.</span></span> 


5. <span data-ttu-id="f0d6d-136">**儲存**您的變更 (工具列的左上角)。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="f0d6d-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="f0d6d-138">[儲存體總管](http://storageexplorer.com/)是很適合用來管理多個儲存體帳戶的工具。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-138">[Storage Explorer](http://storageexplorer.com/) is a great tool to  manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="f0d6d-139">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="f0d6d-139">Connector-specific details</span></span>

<span data-ttu-id="f0d6d-140">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/azureblobconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f0d6d-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0d6d-141">Next steps</span></span>
<span data-ttu-id="f0d6d-142">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="f0d6d-143">請到我們的 [API 清單](apis-list.md)探索 Logic Apps 中其他可用的連接器。</span><span class="sxs-lookup"><span data-stu-id="f0d6d-143">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

