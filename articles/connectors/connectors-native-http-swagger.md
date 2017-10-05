---
title: "透過適用於 Azure Logic Apps 的 HTTP + Swagger 連接器呼叫 REST 端點 | Microsoft Docs"
description: "透過 Swagger 搭配 HTTP + Swagger 連接器，從邏輯應用程式連線至 REST 端點"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="3b59f-103">開始使用 HTTP + Swagger 動作</span><span class="sxs-lookup"><span data-stu-id="3b59f-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="3b59f-104">當您在邏輯應用程式工作流程中使用 HTTP + Swagger 動作時，可以透過 [Swagger 文件](https://swagger.io)在任一 REST 端點建立第一級的連接器。</span><span class="sxs-lookup"><span data-stu-id="3b59f-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="3b59f-105">您也可以使用第一級的邏輯應用程式設計工具體驗，擴充邏輯應用程式以呼叫任何 REST 端點。</span><span class="sxs-lookup"><span data-stu-id="3b59f-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="3b59f-106">若要了解如何利用連接器建立邏輯應用程式，請參閱[建立新的邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="3b59f-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="3b59f-107">使用 HTTP + Swagger 做為觸發程序或動作</span><span class="sxs-lookup"><span data-stu-id="3b59f-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="3b59f-108">HTTP + Swagger 觸發程序和動作的功能與 [HTTP 動作](connectors-native-http.md)相同，但能從 [Swagger 中繼資料](https://swagger.io)公開 API 的結構和輸出，因此可以提供較佳的邏輯應用程式設計工具體驗。</span><span class="sxs-lookup"><span data-stu-id="3b59f-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="3b59f-109">您也可以使用 HTTP + Swagger 連接器作為觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3b59f-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="3b59f-110">如果您想要實作輪詢觸發程序，請依照[建立自訂 API 來呼叫邏輯應用程式的其他 API、服務和系統](../logic-apps/logic-apps-create-api-app.md#polling-triggers)中所述的輪詢模式進行。</span><span class="sxs-lookup"><span data-stu-id="3b59f-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="3b59f-111">深入了解 [邏輯應用程式觸發程序和動作](connectors-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3b59f-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="3b59f-112">以下是如何使用 HTTP + Swagger 作業做為邏輯應用程式中工作流程動作的範例。</span><span class="sxs-lookup"><span data-stu-id="3b59f-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="3b59f-113">選取 [新增步驟]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="3b59f-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="3b59f-114">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="3b59f-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="3b59f-115">在動作搜尋方塊中，輸入 **swagger** 以列出 HTTP + Swagger 動作。</span><span class="sxs-lookup"><span data-stu-id="3b59f-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![選取 HTTP + Swagger 動作](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="3b59f-117">輸入 Swagger 文件的 URL：</span><span class="sxs-lookup"><span data-stu-id="3b59f-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="3b59f-118">若要從邏輯應用程式設計工具使用，此 URL 必須是 HTTPS 端點並已啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="3b59f-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="3b59f-119">如果 Swagger 文件不符合此需求，您可以使用 [已啟用 CORS 的 Azure 儲存體](#hosting-swagger-from-storage) 來儲存文件。</span><span class="sxs-lookup"><span data-stu-id="3b59f-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="3b59f-120">按一下 [下一步]  以從 Swagger 文件讀取和轉譯。</span><span class="sxs-lookup"><span data-stu-id="3b59f-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="3b59f-121">新增 HTTP 呼叫所需的任何參數。</span><span class="sxs-lookup"><span data-stu-id="3b59f-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![完成 HTTP 動作](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="3b59f-123">若要儲存並發佈您的邏輯應用程式，請按一下設計工具工具列中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="3b59f-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="3b59f-124">從 Azure 儲存體託管 Swagger</span><span class="sxs-lookup"><span data-stu-id="3b59f-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="3b59f-125">您可能想要參考未託管的 Swagger 文件，但這並不符合設計工具的安全性及跨原始來源需求。</span><span class="sxs-lookup"><span data-stu-id="3b59f-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="3b59f-126">為解決這個問題，您可以將 Swagger 文件儲存在 Azure 儲存體並啟用 CORS 來參考該文件。</span><span class="sxs-lookup"><span data-stu-id="3b59f-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="3b59f-127">以下是在 Azure 儲存體中建立、設定和儲存 Swagger 文件的步驟：</span><span class="sxs-lookup"><span data-stu-id="3b59f-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="3b59f-128">[使用 Azure Blob 儲存體建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)</span><span class="sxs-lookup"><span data-stu-id="3b59f-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="3b59f-129">若要執行此步驟，請將權限設為 [公用存取]。</span><span class="sxs-lookup"><span data-stu-id="3b59f-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="3b59f-130">在 Blob 啟用 CORS。</span><span class="sxs-lookup"><span data-stu-id="3b59f-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="3b59f-131">您可以使用 [這個 PowerShell 指令碼](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1) 自動設定此設定。</span><span class="sxs-lookup"><span data-stu-id="3b59f-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="3b59f-132">將 Swagger 檔案上傳至 Blob。</span><span class="sxs-lookup"><span data-stu-id="3b59f-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="3b59f-133">您可以從 [Azure 入口網站](https://portal.azure.com)或 [Azure 儲存體總管](http://storageexplorer.com/)等工具執行這個步驟。</span><span class="sxs-lookup"><span data-stu-id="3b59f-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="3b59f-134">參考 Azure Blob 儲存體中文件的 HTTPS 連結。</span><span class="sxs-lookup"><span data-stu-id="3b59f-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="3b59f-135">此連結用此格式：</span><span class="sxs-lookup"><span data-stu-id="3b59f-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="3b59f-136">技術詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3b59f-136">Technical details</span></span>
<span data-ttu-id="3b59f-137">以下是此 HTTP + Swagger 連接器所支援觸發程序和動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3b59f-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="3b59f-138">HTTP + Swagger 觸發程序</span><span class="sxs-lookup"><span data-stu-id="3b59f-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="3b59f-139">觸發程序是一個事件，可用來啟動邏輯應用程式中定義的工作流程。</span><span class="sxs-lookup"><span data-stu-id="3b59f-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3b59f-140">深入了解觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3b59f-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="3b59f-141">HTTP + Swagger 連接器有一個觸發程序。</span><span class="sxs-lookup"><span data-stu-id="3b59f-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="3b59f-142">觸發程序</span><span class="sxs-lookup"><span data-stu-id="3b59f-142">Trigger</span></span> | <span data-ttu-id="3b59f-143">說明</span><span class="sxs-lookup"><span data-stu-id="3b59f-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b59f-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3b59f-144">HTTP + Swagger</span></span> |<span data-ttu-id="3b59f-145">進行 HTTP 呼叫並傳回回應內容</span><span class="sxs-lookup"><span data-stu-id="3b59f-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="3b59f-146">HTTP + Swagger 動作</span><span class="sxs-lookup"><span data-stu-id="3b59f-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="3b59f-147">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="3b59f-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3b59f-148">深入了解動作。</span><span class="sxs-lookup"><span data-stu-id="3b59f-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="3b59f-149">HTTP + Swagger 連接器有一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="3b59f-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="3b59f-150">動作</span><span class="sxs-lookup"><span data-stu-id="3b59f-150">Action</span></span> | <span data-ttu-id="3b59f-151">說明</span><span class="sxs-lookup"><span data-stu-id="3b59f-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b59f-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3b59f-152">HTTP + Swagger</span></span> |<span data-ttu-id="3b59f-153">進行 HTTP 呼叫並傳回回應內容</span><span class="sxs-lookup"><span data-stu-id="3b59f-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="3b59f-154">動作詳細資料</span><span class="sxs-lookup"><span data-stu-id="3b59f-154">Action details</span></span>
<span data-ttu-id="3b59f-155">HTTP + Swagger 連接器隨附一個可能的動作。</span><span class="sxs-lookup"><span data-stu-id="3b59f-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="3b59f-156">以下是關於每個動作、其必要和選擇性輸入欄位，以及與其使用方式相關聯的對應輸出詳細資料的資訊。</span><span class="sxs-lookup"><span data-stu-id="3b59f-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="3b59f-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3b59f-157">HTTP + Swagger</span></span>
<span data-ttu-id="3b59f-158">在 Swagger 中繼資料的協助下提出 HTTP 輸出要求。</span><span class="sxs-lookup"><span data-stu-id="3b59f-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="3b59f-159">星號 (*) 表示必要的欄位。</span><span class="sxs-lookup"><span data-stu-id="3b59f-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="3b59f-160">顯示名稱</span><span class="sxs-lookup"><span data-stu-id="3b59f-160">Display name</span></span> | <span data-ttu-id="3b59f-161">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="3b59f-161">Property name</span></span> | <span data-ttu-id="3b59f-162">說明</span><span class="sxs-lookup"><span data-stu-id="3b59f-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b59f-163">方法 *</span><span class="sxs-lookup"><span data-stu-id="3b59f-163">Method*</span></span> |<span data-ttu-id="3b59f-164">method</span><span class="sxs-lookup"><span data-stu-id="3b59f-164">method</span></span> |<span data-ttu-id="3b59f-165">要使用的 HTTP 指令動詞。</span><span class="sxs-lookup"><span data-stu-id="3b59f-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="3b59f-166">URI*</span><span class="sxs-lookup"><span data-stu-id="3b59f-166">URI*</span></span> |<span data-ttu-id="3b59f-167">uri</span><span class="sxs-lookup"><span data-stu-id="3b59f-167">uri</span></span> |<span data-ttu-id="3b59f-168">HTTP 要求的 URI。</span><span class="sxs-lookup"><span data-stu-id="3b59f-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="3b59f-169">標頭</span><span class="sxs-lookup"><span data-stu-id="3b59f-169">Headers</span></span> |<span data-ttu-id="3b59f-170">標頭</span><span class="sxs-lookup"><span data-stu-id="3b59f-170">headers</span></span> |<span data-ttu-id="3b59f-171">要包含之 HTTP 標頭的 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="3b59f-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="3b59f-172">內文</span><span class="sxs-lookup"><span data-stu-id="3b59f-172">Body</span></span> |<span data-ttu-id="3b59f-173">內文</span><span class="sxs-lookup"><span data-stu-id="3b59f-173">body</span></span> |<span data-ttu-id="3b59f-174">HTTP 要求本文。</span><span class="sxs-lookup"><span data-stu-id="3b59f-174">The HTTP request body.</span></span> |
| <span data-ttu-id="3b59f-175">驗證</span><span class="sxs-lookup"><span data-stu-id="3b59f-175">Authentication</span></span> |<span data-ttu-id="3b59f-176">驗證</span><span class="sxs-lookup"><span data-stu-id="3b59f-176">authentication</span></span> |<span data-ttu-id="3b59f-177">用於要求的驗證。</span><span class="sxs-lookup"><span data-stu-id="3b59f-177">Authentication to use for request.</span></span> <span data-ttu-id="3b59f-178">如需詳細資訊，請參閱 [HTTP 連接器](connectors-native-http.md#authentication)。</span><span class="sxs-lookup"><span data-stu-id="3b59f-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="3b59f-179">**輸出詳細資料**</span><span class="sxs-lookup"><span data-stu-id="3b59f-179">**Output details**</span></span>

<span data-ttu-id="3b59f-180">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="3b59f-180">HTTP response</span></span>

| <span data-ttu-id="3b59f-181">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="3b59f-181">Property Name</span></span> | <span data-ttu-id="3b59f-182">資料類型</span><span class="sxs-lookup"><span data-stu-id="3b59f-182">Data type</span></span> | <span data-ttu-id="3b59f-183">說明</span><span class="sxs-lookup"><span data-stu-id="3b59f-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3b59f-184">headers</span><span class="sxs-lookup"><span data-stu-id="3b59f-184">Headers</span></span> |<span data-ttu-id="3b59f-185">物件</span><span class="sxs-lookup"><span data-stu-id="3b59f-185">object</span></span> |<span data-ttu-id="3b59f-186">回應標頭</span><span class="sxs-lookup"><span data-stu-id="3b59f-186">Response headers</span></span> |
| <span data-ttu-id="3b59f-187">內文</span><span class="sxs-lookup"><span data-stu-id="3b59f-187">Body</span></span> |<span data-ttu-id="3b59f-188">物件</span><span class="sxs-lookup"><span data-stu-id="3b59f-188">object</span></span> |<span data-ttu-id="3b59f-189">回應物件</span><span class="sxs-lookup"><span data-stu-id="3b59f-189">Response object</span></span> |
| <span data-ttu-id="3b59f-190">Status Code</span><span class="sxs-lookup"><span data-stu-id="3b59f-190">Status Code</span></span> |<span data-ttu-id="3b59f-191">整數</span><span class="sxs-lookup"><span data-stu-id="3b59f-191">int</span></span> |<span data-ttu-id="3b59f-192">HTTP 狀態碼</span><span class="sxs-lookup"><span data-stu-id="3b59f-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="3b59f-193">HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="3b59f-193">HTTP responses</span></span>
<span data-ttu-id="3b59f-194">呼叫不同動作時，您可能會收到特定回應。</span><span class="sxs-lookup"><span data-stu-id="3b59f-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="3b59f-195">下表概述對應的回應及說明。</span><span class="sxs-lookup"><span data-stu-id="3b59f-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="3b59f-196">名稱</span><span class="sxs-lookup"><span data-stu-id="3b59f-196">Name</span></span> | <span data-ttu-id="3b59f-197">說明</span><span class="sxs-lookup"><span data-stu-id="3b59f-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b59f-198">200</span><span class="sxs-lookup"><span data-stu-id="3b59f-198">200</span></span> |<span data-ttu-id="3b59f-199">OK</span><span class="sxs-lookup"><span data-stu-id="3b59f-199">OK</span></span> |
| <span data-ttu-id="3b59f-200">202</span><span class="sxs-lookup"><span data-stu-id="3b59f-200">202</span></span> |<span data-ttu-id="3b59f-201">已接受</span><span class="sxs-lookup"><span data-stu-id="3b59f-201">Accepted</span></span> |
| <span data-ttu-id="3b59f-202">400</span><span class="sxs-lookup"><span data-stu-id="3b59f-202">400</span></span> |<span data-ttu-id="3b59f-203">不正確的要求</span><span class="sxs-lookup"><span data-stu-id="3b59f-203">Bad request</span></span> |
| <span data-ttu-id="3b59f-204">401</span><span class="sxs-lookup"><span data-stu-id="3b59f-204">401</span></span> |<span data-ttu-id="3b59f-205">未經授權</span><span class="sxs-lookup"><span data-stu-id="3b59f-205">Unauthorized</span></span> |
| <span data-ttu-id="3b59f-206">403</span><span class="sxs-lookup"><span data-stu-id="3b59f-206">403</span></span> |<span data-ttu-id="3b59f-207">禁止</span><span class="sxs-lookup"><span data-stu-id="3b59f-207">Forbidden</span></span> |
| <span data-ttu-id="3b59f-208">404</span><span class="sxs-lookup"><span data-stu-id="3b59f-208">404</span></span> |<span data-ttu-id="3b59f-209">找不到</span><span class="sxs-lookup"><span data-stu-id="3b59f-209">Not Found</span></span> |
| <span data-ttu-id="3b59f-210">500</span><span class="sxs-lookup"><span data-stu-id="3b59f-210">500</span></span> |<span data-ttu-id="3b59f-211">內部伺服器錯誤。</span><span class="sxs-lookup"><span data-stu-id="3b59f-211">Internal server error.</span></span> <span data-ttu-id="3b59f-212">發生未知錯誤。</span><span class="sxs-lookup"><span data-stu-id="3b59f-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="3b59f-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b59f-213">Next steps</span></span>

* [<span data-ttu-id="3b59f-214">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="3b59f-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="3b59f-215">尋找其他連接器</span><span class="sxs-lookup"><span data-stu-id="3b59f-215">Find other connectors</span></span>](apis-list.md)