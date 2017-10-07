---
title: "aaaAdd hello Azure blob 儲存體邏輯應用程式中的連接器 |Microsoft 文件"
description: "開始使用和設定邏輯應用程式中的 hello Azure blob 儲存體連接器"
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
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a><span data-ttu-id="9eb84-103">在邏輯應用程式中使用 hello Azure blob 儲存體連接器</span><span class="sxs-lookup"><span data-stu-id="9eb84-103">Use hello Azure blob storage connector in a logic app</span></span>
<span data-ttu-id="9eb84-104">使用 hello Azure Blob 儲存體連接器 tooupload，更新、 取得，並刪除 blob 儲存體帳戶，全部都在邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="9eb84-104">Use hello Azure Blob storage connector tooupload, update, get, and delete blobs in your storage account, all within a logic app.</span></span>  

<span data-ttu-id="9eb84-105">您可以利用 Azure Blob 儲存體來：</span><span class="sxs-lookup"><span data-stu-id="9eb84-105">With Azure blob storage, you:</span></span>

* <span data-ttu-id="9eb84-106">上傳新專案或取得最近更新的檔案以建置工作流程。</span><span class="sxs-lookup"><span data-stu-id="9eb84-106">Build your workflow by uploading new projects, or getting files that have been recently updated.</span></span>
* <span data-ttu-id="9eb84-107">使用動作 tooget 檔案中繼資料，請刪除檔案、 複製檔案等等。</span><span class="sxs-lookup"><span data-stu-id="9eb84-107">Use actions tooget file metadata, delete a file, copy files, and more.</span></span> <span data-ttu-id="9eb84-108">例如，當 Azure 網站中的工具更新時 (觸發程序)，便更新 Blob 儲存體中的檔案 (動作)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-108">For example, when a tool is updated in an Azure web site (a trigger), then update a file in blob storage (an action).</span></span> 

<span data-ttu-id="9eb84-109">本主題說明如何 toouse hello blob 儲存體邏輯應用程式中的連接器。</span><span class="sxs-lookup"><span data-stu-id="9eb84-109">This topic shows you how toouse hello blob storage connector in a logic app.</span></span>

<span data-ttu-id="9eb84-110">toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<span data-ttu-id="9eb84-111">toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-blob-storage"></a><span data-ttu-id="9eb84-112">連接 tooAzure blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="9eb84-112">Connect tooAzure blob storage</span></span>
<span data-ttu-id="9eb84-113">邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="9eb84-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="9eb84-114">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="9eb84-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="9eb84-115">例如，tooconnect tooa 儲存體帳戶，您先建立 blob 儲存體*連接*。</span><span class="sxs-lookup"><span data-stu-id="9eb84-115">For example, tooconnect tooa storage account, you first create a blob storage *connection*.</span></span> <span data-ttu-id="9eb84-116">toocreate 連接，輸入您平常用 tooaccess hello 服務，您所連接的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="9eb84-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="9eb84-117">Azure 儲存體，因此輸入 hello 認證 tooyour 儲存體帳戶 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="9eb84-117">So with Azure storage, enter hello credentials tooyour storage account toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="9eb84-118">建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="9eb84-118">Create hello connection</span></span>
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a><span data-ttu-id="9eb84-119">使用觸發程序</span><span class="sxs-lookup"><span data-stu-id="9eb84-119">Use a trigger</span></span>
<span data-ttu-id="9eb84-120">此連接器並沒有任何觸發程序。</span><span class="sxs-lookup"><span data-stu-id="9eb84-120">This connector does not have any triggers.</span></span> <span data-ttu-id="9eb84-121">使用其他觸發程序 toostart hello 邏輯應用程式，例如循環觸發程序、 HTTP Webhook 觸發程序、 觸發程序適用於其他連接器，等等。</span><span class="sxs-lookup"><span data-stu-id="9eb84-121">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="9eb84-122">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。</span><span class="sxs-lookup"><span data-stu-id="9eb84-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="9eb84-123">使用動作</span><span class="sxs-lookup"><span data-stu-id="9eb84-123">Use an action</span></span>
<span data-ttu-id="9eb84-124">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="9eb84-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span>

1. <span data-ttu-id="9eb84-125">選取加號 hello。</span><span class="sxs-lookup"><span data-stu-id="9eb84-125">Select hello plus sign.</span></span> <span data-ttu-id="9eb84-126">您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。</span><span class="sxs-lookup"><span data-stu-id="9eb84-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. <span data-ttu-id="9eb84-127">選擇 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="9eb84-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="9eb84-128">在 [hello] 文字方塊中，輸入"blob"tooget 所有 hello 可用動作的清單。</span><span class="sxs-lookup"><span data-stu-id="9eb84-128">In hello text box, type “blob” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. <span data-ttu-id="9eb84-129">在我們的範例中，選擇 [AzureBlob - 使用路徑取得檔案中繼資料]。</span><span class="sxs-lookup"><span data-stu-id="9eb84-129">In our example, choose **AzureBlob - Get file metadata using path**.</span></span> <span data-ttu-id="9eb84-130">如果連接已存在，然後選取 hello **...**按鈕 tooselect 檔案 （顯示選擇器）。</span><span class="sxs-lookup"><span data-stu-id="9eb84-130">If a connection already exists, then select hello **...** (Show Picker) button tooselect a file.</span></span>
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    <span data-ttu-id="9eb84-131">如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。</span><span class="sxs-lookup"><span data-stu-id="9eb84-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="9eb84-132">[建立 hello 連接](connectors-create-api-azureblobstorage.md#create-the-connection)本主題說明這些屬性。</span><span class="sxs-lookup"><span data-stu-id="9eb84-132">[Create hello connection](connectors-create-api-azureblobstorage.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9eb84-133">在此範例中，我們可以得到 hello 中繼資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="9eb84-133">In this example, we get hello metadata of a file.</span></span> <span data-ttu-id="9eb84-134">toosee hello 中繼資料，並將另一個動作，建立新的檔案，使用另一個連接器。</span><span class="sxs-lookup"><span data-stu-id="9eb84-134">toosee hello metadata, add another action that creates a new file using another connector.</span></span> <span data-ttu-id="9eb84-135">例如，加入建立 hello 中繼資料為基礎的新 「 測試 」 檔案的 OneDrive 動作。</span><span class="sxs-lookup"><span data-stu-id="9eb84-135">For example, add a OneDrive action that creates a new "test" file based on hello metadata.</span></span> 


5. <span data-ttu-id="9eb84-136">**儲存**您的變更 （hello 工具列的左上的角）。</span><span class="sxs-lookup"><span data-stu-id="9eb84-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="9eb84-137">邏輯應用程式將會儲存，而且可能會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="9eb84-137">Your logic app is saved and may be automatically enabled.</span></span>

> [!TIP]
> <span data-ttu-id="9eb84-138">[儲存體總管](http://storageexplorer.com/)是很棒的工具太管理多個儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="9eb84-138">[Storage Explorer](http://storageexplorer.com/) is a great tool too manage multiple storage accounts.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="9eb84-139">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="9eb84-139">Connector-specific details</span></span>

<span data-ttu-id="9eb84-140">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/azureblobconnector/)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/azureblobconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9eb84-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9eb84-141">Next steps</span></span>
<span data-ttu-id="9eb84-142">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-142">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="9eb84-143">瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="9eb84-143">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

