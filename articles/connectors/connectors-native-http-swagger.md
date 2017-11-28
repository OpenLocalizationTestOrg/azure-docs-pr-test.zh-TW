---
title: "aaaCall REST 端點，其中包含 HTTP + Swagger Azure 邏輯應用程式連接器 |Microsoft 文件"
description: "從邏輯應用程式透過 Swagger hello HTTP + Swagger 連接器連接 tooREST 端點"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="92d4d-103">開始使用 hello HTTP + Swagger 動作</span><span class="sxs-lookup"><span data-stu-id="92d4d-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="92d4d-104">您可以建立第一級連接器 tooany REST 端點，透過[Swagger 文件](https://swagger.io)當邏輯應用程式工作流程中使用 hello HTTP + Swagger 動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="92d4d-105">您也可以擴充邏輯應用程式 toocall 第一級的邏輯應用程式的設計工具經驗的任何 REST 端點。</span><span class="sxs-lookup"><span data-stu-id="92d4d-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="92d4d-106">如何 toocreate 邏輯應用程式使用連接器，請參閱的 toolearn[建立新的邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="92d4d-107">使用 HTTP + Swagger 做為觸發程序或動作</span><span class="sxs-lookup"><span data-stu-id="92d4d-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="92d4d-108">hello HTTP + Swagger 觸發程序和動作的工作會將相同 hello 與 hello [HTTP 動作](connectors-native-http.md)但提供較佳的體驗，在邏輯應用程式的設計工具中，藉由公開 hello API 結構和輸出 hello [Swagger 中繼資料](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="92d4d-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="92d4d-109">您也可以使用 hello HTTP + Swagger 連接器的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="92d4d-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="92d4d-110">如果您想 tooimplement 輪詢觸發程序，請依照下列所述的 hello 輪詢模式[邏輯應用程式從其他應用程式開發介面、 服務和系統建立自訂的應用程式開發介面 toocall](../logic-apps/logic-apps-create-api-app.md#polling-triggers)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="92d4d-111">深入了解 [邏輯應用程式觸發程序和動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="92d4d-112">以下是如何 toouse hello HTTP + Swagger 範例操作，因為邏輯應用程式中的工作流程中的動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="92d4d-113">選取 hello**新步驟** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92d4d-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="92d4d-114">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="92d4d-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="92d4d-115">在 hello 動作搜尋方塊中，輸入**swagger** toolist hello HTTP + Swagger 動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![選取 HTTP + Swagger 動作](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="92d4d-117">輸入 hello Swagger 文件的 URL:</span><span class="sxs-lookup"><span data-stu-id="92d4d-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="92d4d-118">toowork 從 hello 邏輯應用程式的設計工具，hello URL 必須是 HTTPS 端點，並啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="92d4d-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="92d4d-119">如果 hello Swagger 文件不符合此需求，您可以使用[Azure 儲存體與啟用 CORS](#hosting-swagger-from-storage) toostore hello 文件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="92d4d-120">按一下**下一步**tooread 和轉譯來自 hello Swagger 文件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="92d4d-121">新增任何所需的 hello HTTP 呼叫的參數。</span><span class="sxs-lookup"><span data-stu-id="92d4d-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![完成 HTTP 動作](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="92d4d-123">toosave 及發行應用程式邏輯，請按一下**儲存**設計工具工具列上。</span><span class="sxs-lookup"><span data-stu-id="92d4d-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="92d4d-124">從 Azure 儲存體託管 Swagger</span><span class="sxs-lookup"><span data-stu-id="92d4d-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="92d4d-125">您可能想 tooreference Swagger 文件所未裝載，或不符合 hello hello 設計工具的安全性和跨原始需求。</span><span class="sxs-lookup"><span data-stu-id="92d4d-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="92d4d-126">tooresolve 這個問題，您可以在 Azure 儲存體中儲存 hello Swagger 文件，並啟用 CORS tooreference hello 文件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="92d4d-127">以下是 hello 步驟 toocreate、 設定和 Swagger 文件儲存在 Azure 儲存體：</span><span class="sxs-lookup"><span data-stu-id="92d4d-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="92d4d-128">[使用 Azure Blob 儲存體建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="92d4d-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="92d4d-129">tooperform 這步驟，設定權限太**公用存取**。</span><span class="sxs-lookup"><span data-stu-id="92d4d-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="92d4d-130">啟用 CORS hello blob 上。</span><span class="sxs-lookup"><span data-stu-id="92d4d-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="92d4d-131">tooautomatically 設定此設定，您可以使用[這個 PowerShell 指令碼](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="92d4d-132">Hello Swagger 檔案 toohello blob 上傳。</span><span class="sxs-lookup"><span data-stu-id="92d4d-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="92d4d-133">您可以執行此步驟中，從 hello [Azure 入口網站](https://portal.azure.com)或從這類工具[Azure 儲存體總管](http://storageexplorer.com/)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="92d4d-134">參考 Azure Blob 儲存體中的 HTTPS 連結 toohello 文件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="92d4d-135">hello 連結會使用此格式：</span><span class="sxs-lookup"><span data-stu-id="92d4d-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="92d4d-136">技術詳細資訊</span><span class="sxs-lookup"><span data-stu-id="92d4d-136">Technical details</span></span>
<span data-ttu-id="92d4d-137">以下是 hello 詳細資料 hello 觸發程序和動作這個 HTTP + Swagger 連接器支援。</span><span class="sxs-lookup"><span data-stu-id="92d4d-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="92d4d-138">HTTP + Swagger 觸發程序</span><span class="sxs-lookup"><span data-stu-id="92d4d-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="92d4d-139">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="92d4d-140">深入了解觸發程序。</span><span class="sxs-lookup"><span data-stu-id="92d4d-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="92d4d-141">hello HTTP + Swagger 連接器有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="92d4d-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="92d4d-142">觸發程序</span><span class="sxs-lookup"><span data-stu-id="92d4d-142">Trigger</span></span> | <span data-ttu-id="92d4d-143">說明</span><span class="sxs-lookup"><span data-stu-id="92d4d-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92d4d-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="92d4d-144">HTTP + Swagger</span></span> |<span data-ttu-id="92d4d-145">進行 HTTP 呼叫，並傳回 hello 回應內容</span><span class="sxs-lookup"><span data-stu-id="92d4d-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="92d4d-146">HTTP + Swagger 動作</span><span class="sxs-lookup"><span data-stu-id="92d4d-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="92d4d-147">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="92d4d-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="92d4d-148">深入了解動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="92d4d-149">hello HTTP + Swagger 連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="92d4d-150">動作</span><span class="sxs-lookup"><span data-stu-id="92d4d-150">Action</span></span> | <span data-ttu-id="92d4d-151">說明</span><span class="sxs-lookup"><span data-stu-id="92d4d-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92d4d-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="92d4d-152">HTTP + Swagger</span></span> |<span data-ttu-id="92d4d-153">進行 HTTP 呼叫，並傳回 hello 回應內容</span><span class="sxs-lookup"><span data-stu-id="92d4d-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="92d4d-154">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="92d4d-154">Action details</span></span>
<span data-ttu-id="92d4d-155">hello HTTP + Swagger 連接器隨附一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="92d4d-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="92d4d-156">以下是每個 hello 動作、 必要和選擇性的輸入的欄位以及 hello 對應及其使用狀況與相關聯的輸出詳細資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="92d4d-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="92d4d-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="92d4d-157">HTTP + Swagger</span></span>
<span data-ttu-id="92d4d-158">在 Swagger 中繼資料的協助下提出 HTTP 輸出要求。</span><span class="sxs-lookup"><span data-stu-id="92d4d-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="92d4d-159">星號 (*) 表示必要的欄位。</span><span class="sxs-lookup"><span data-stu-id="92d4d-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="92d4d-160">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="92d4d-160">Display name</span></span> | <span data-ttu-id="92d4d-161">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92d4d-161">Property name</span></span> | <span data-ttu-id="92d4d-162">說明</span><span class="sxs-lookup"><span data-stu-id="92d4d-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92d4d-163">方法 *</span><span class="sxs-lookup"><span data-stu-id="92d4d-163">Method*</span></span> |<span data-ttu-id="92d4d-164">method</span><span class="sxs-lookup"><span data-stu-id="92d4d-164">method</span></span> |<span data-ttu-id="92d4d-165">HTTP 指令動詞 toouse。</span><span class="sxs-lookup"><span data-stu-id="92d4d-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="92d4d-166">URI*</span><span class="sxs-lookup"><span data-stu-id="92d4d-166">URI*</span></span> |<span data-ttu-id="92d4d-167">uri</span><span class="sxs-lookup"><span data-stu-id="92d4d-167">uri</span></span> |<span data-ttu-id="92d4d-168">Hello HTTP 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="92d4d-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="92d4d-169">headers</span><span class="sxs-lookup"><span data-stu-id="92d4d-169">Headers</span></span> |<span data-ttu-id="92d4d-170">headers</span><span class="sxs-lookup"><span data-stu-id="92d4d-170">headers</span></span> |<span data-ttu-id="92d4d-171">HTTP 標頭 tooinclude JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="92d4d-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="92d4d-172">內文</span><span class="sxs-lookup"><span data-stu-id="92d4d-172">Body</span></span> |<span data-ttu-id="92d4d-173">body</span><span class="sxs-lookup"><span data-stu-id="92d4d-173">body</span></span> |<span data-ttu-id="92d4d-174">hello HTTP 要求主體。</span><span class="sxs-lookup"><span data-stu-id="92d4d-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="92d4d-175">驗證</span><span class="sxs-lookup"><span data-stu-id="92d4d-175">Authentication</span></span> |<span data-ttu-id="92d4d-176">驗證</span><span class="sxs-lookup"><span data-stu-id="92d4d-176">authentication</span></span> |<span data-ttu-id="92d4d-177">要求的驗證 toouse。</span><span class="sxs-lookup"><span data-stu-id="92d4d-177">Authentication toouse for request.</span></span> <span data-ttu-id="92d4d-178">如需詳細資訊，請參閱 hello [HTTP 連接器](connectors-native-http.md#authentication)。</span><span class="sxs-lookup"><span data-stu-id="92d4d-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="92d4d-179">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="92d4d-179">**Output details**</span></span>

<span data-ttu-id="92d4d-180">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="92d4d-180">HTTP response</span></span>

| <span data-ttu-id="92d4d-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="92d4d-181">Property Name</span></span> | <span data-ttu-id="92d4d-182">資料類型</span><span class="sxs-lookup"><span data-stu-id="92d4d-182">Data type</span></span> | <span data-ttu-id="92d4d-183">說明</span><span class="sxs-lookup"><span data-stu-id="92d4d-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="92d4d-184">headers</span><span class="sxs-lookup"><span data-stu-id="92d4d-184">Headers</span></span> |<span data-ttu-id="92d4d-185">物件</span><span class="sxs-lookup"><span data-stu-id="92d4d-185">object</span></span> |<span data-ttu-id="92d4d-186">回應標頭</span><span class="sxs-lookup"><span data-stu-id="92d4d-186">Response headers</span></span> |
| <span data-ttu-id="92d4d-187">內文</span><span class="sxs-lookup"><span data-stu-id="92d4d-187">Body</span></span> |<span data-ttu-id="92d4d-188">物件</span><span class="sxs-lookup"><span data-stu-id="92d4d-188">object</span></span> |<span data-ttu-id="92d4d-189">回應物件</span><span class="sxs-lookup"><span data-stu-id="92d4d-189">Response object</span></span> |
| <span data-ttu-id="92d4d-190">Status Code</span><span class="sxs-lookup"><span data-stu-id="92d4d-190">Status Code</span></span> |<span data-ttu-id="92d4d-191">整數</span><span class="sxs-lookup"><span data-stu-id="92d4d-191">int</span></span> |<span data-ttu-id="92d4d-192">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="92d4d-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="92d4d-193">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="92d4d-193">HTTP responses</span></span>
<span data-ttu-id="92d4d-194">呼叫 toovarious 動作時，您可能會收到特定的回應。</span><span class="sxs-lookup"><span data-stu-id="92d4d-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="92d4d-195">下表概述對應的回應及說明。</span><span class="sxs-lookup"><span data-stu-id="92d4d-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="92d4d-196">名稱</span><span class="sxs-lookup"><span data-stu-id="92d4d-196">Name</span></span> | <span data-ttu-id="92d4d-197">說明</span><span class="sxs-lookup"><span data-stu-id="92d4d-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="92d4d-198">200</span><span class="sxs-lookup"><span data-stu-id="92d4d-198">200</span></span> |<span data-ttu-id="92d4d-199">OK</span><span class="sxs-lookup"><span data-stu-id="92d4d-199">OK</span></span> |
| <span data-ttu-id="92d4d-200">202</span><span class="sxs-lookup"><span data-stu-id="92d4d-200">202</span></span> |<span data-ttu-id="92d4d-201">已接受</span><span class="sxs-lookup"><span data-stu-id="92d4d-201">Accepted</span></span> |
| <span data-ttu-id="92d4d-202">400</span><span class="sxs-lookup"><span data-stu-id="92d4d-202">400</span></span> |<span data-ttu-id="92d4d-203">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="92d4d-203">Bad request</span></span> |
| <span data-ttu-id="92d4d-204">401</span><span class="sxs-lookup"><span data-stu-id="92d4d-204">401</span></span> |<span data-ttu-id="92d4d-205">未經授權</span><span class="sxs-lookup"><span data-stu-id="92d4d-205">Unauthorized</span></span> |
| <span data-ttu-id="92d4d-206">403</span><span class="sxs-lookup"><span data-stu-id="92d4d-206">403</span></span> |<span data-ttu-id="92d4d-207">禁止</span><span class="sxs-lookup"><span data-stu-id="92d4d-207">Forbidden</span></span> |
| <span data-ttu-id="92d4d-208">404</span><span class="sxs-lookup"><span data-stu-id="92d4d-208">404</span></span> |<span data-ttu-id="92d4d-209">找不到</span><span class="sxs-lookup"><span data-stu-id="92d4d-209">Not Found</span></span> |
| <span data-ttu-id="92d4d-210">500</span><span class="sxs-lookup"><span data-stu-id="92d4d-210">500</span></span> |<span data-ttu-id="92d4d-211">內部伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="92d4d-211">Internal server error.</span></span> <span data-ttu-id="92d4d-212">發生未知錯誤。</span><span class="sxs-lookup"><span data-stu-id="92d4d-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="92d4d-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92d4d-213">Next steps</span></span>

* [<span data-ttu-id="92d4d-214">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="92d4d-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="92d4d-215">尋找其他連接器</span><span class="sxs-lookup"><span data-stu-id="92d4d-215">Find other connectors</span></span>](apis-list.md)