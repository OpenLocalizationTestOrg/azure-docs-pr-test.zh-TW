---
title: "快速入門︰Azure Machine Learning 建議 API (版本 1)| Microsoft Docs"
description: "Azure Machine Learning Recommendations - 快速入門手冊"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="dbc41-104">快速入門指南 hello 機器學習建議應用程式開發介面 （第 1 版）</span><span class="sxs-lookup"><span data-stu-id="dbc41-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="dbc41-105">您應該開始使用 hello[建議 API 認知服務](https://www.microsoft.com/cognitive-services/recommendations-api)而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="dbc41-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="dbc41-106">hello 建議認知服務將會取代此服務，並將那里開發所有 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="dbc41-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="dbc41-107">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="dbc41-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="dbc41-108">深入了解[移轉 toohello 新認知服務](http://aka.ms/recomigrate)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="dbc41-109">本文件說明如何 tooonboard 您服務或應用程式的 toouse Microsoft Azure 機器學習建議。</span><span class="sxs-lookup"><span data-stu-id="dbc41-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="dbc41-110">您可以在 hello 建議 API hello 中找到更多詳細資料[Cortana 智慧組件庫](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="dbc41-111">一般概觀</span><span class="sxs-lookup"><span data-stu-id="dbc41-111">General overview</span></span>
<span data-ttu-id="dbc41-112">toouse Azure 機器學習建議，您需要下列步驟 tootake hello:</span><span class="sxs-lookup"><span data-stu-id="dbc41-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="dbc41-113">建立模型-模型是您的使用量資料、 目錄資料和 hello 建議模型的容器。</span><span class="sxs-lookup"><span data-stu-id="dbc41-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="dbc41-114">匯入類別目錄資料的類別目錄包含 hello 項目上的中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="dbc41-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="dbc41-115">匯入使用狀況資料 - 上傳使用狀況資料的方式有 2 種 (使用其中一種或兩種皆用)：</span><span class="sxs-lookup"><span data-stu-id="dbc41-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="dbc41-116">上傳包含 hello 使用量資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="dbc41-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="dbc41-117">傳送資料擷取事件。</span><span class="sxs-lookup"><span data-stu-id="dbc41-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="dbc41-118">通常您上傳使用方式中的檔案順序 toobe 無法 toocreate （啟動程序） 的初始的建議模型，並使用它，直到 hello 系統收集資料不足，無法使用 hello 資料擷取的格式。</span><span class="sxs-lookup"><span data-stu-id="dbc41-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="dbc41-119">建立建議模型-這是非同步作業中的 hello 建議系統採用所有 hello 使用量資料，並建立推薦模型。</span><span class="sxs-lookup"><span data-stu-id="dbc41-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="dbc41-120">這項作業可能需要數分鐘或幾小時的時間視 hello hello 資料大小以及 hello 建置組態參數。</span><span class="sxs-lookup"><span data-stu-id="dbc41-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="dbc41-121">觸發 hello 組建，您會收到組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="dbc41-122">當使用它 toocheck hello 建置程序已啟動 tooconsume 建議之前結束。</span><span class="sxs-lookup"><span data-stu-id="dbc41-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="dbc41-123">取用建議 - 取得特定項目或項目清單的建議。</span><span class="sxs-lookup"><span data-stu-id="dbc41-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="dbc41-124">上述所有 hello 步驟都是透過 hello Azure 機器學習建議 API 都完成。</span><span class="sxs-lookup"><span data-stu-id="dbc41-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="dbc41-125">您可以下載範例應用程式實作每個步驟從 hello[以及組件庫。](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="dbc41-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="dbc41-126">限制</span><span class="sxs-lookup"><span data-stu-id="dbc41-126">Limitations</span></span>
* <span data-ttu-id="dbc41-127">hello 的模型，每個訂用帳戶數目上限為 10。</span><span class="sxs-lookup"><span data-stu-id="dbc41-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="dbc41-128">hello 類別目錄可以保存的項目數目上限為 100000。</span><span class="sxs-lookup"><span data-stu-id="dbc41-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="dbc41-129">hello 會保留的使用方式點數目上限是 ~ 5,000,000。</span><span class="sxs-lookup"><span data-stu-id="dbc41-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="dbc41-130">如果要上傳新的或報告，將會刪除最舊的 hello。</span><span class="sxs-lookup"><span data-stu-id="dbc41-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="dbc41-131">hello 可以傳送 POST （例如，匯入類別目錄資料，匯入使用量資料） 中的資料大小上限為 200 MB。</span><span class="sxs-lookup"><span data-stu-id="dbc41-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="dbc41-132">hello 的建議模型組建時，不在作用中的每秒交易數為 ~ 2TPS。</span><span class="sxs-lookup"><span data-stu-id="dbc41-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="dbc41-133">作用中的建議模型組建可以阻擋 too20TPS。</span><span class="sxs-lookup"><span data-stu-id="dbc41-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="dbc41-134">整合</span><span class="sxs-lookup"><span data-stu-id="dbc41-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="dbc41-135">驗證</span><span class="sxs-lookup"><span data-stu-id="dbc41-135">Authentication</span></span>
<span data-ttu-id="dbc41-136">Microsoft Azure Marketplace 支援任一 hello 基本或 OAuth 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="dbc41-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="dbc41-137">您可以輕鬆找到 hello 帳戶金鑰 」，瀏覽 toohello hello marketplace 的 [索引鍵[您的帳戶設定](https://datamarket.azure.com/account/keys)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="dbc41-138">基本驗證</span><span class="sxs-lookup"><span data-stu-id="dbc41-138">Basic Authentication</span></span>
<span data-ttu-id="dbc41-139">加入 hello 授權標頭：</span><span class="sxs-lookup"><span data-stu-id="dbc41-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="dbc41-140">轉換 tooBase64 (C#)</span><span class="sxs-lookup"><span data-stu-id="dbc41-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="dbc41-141">轉換 tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="dbc41-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="dbc41-142">服務 URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-142">Service URI</span></span>
<span data-ttu-id="dbc41-143">hello Azure 機器學習建議 Api 的 hello 服務根目錄 URI 是[這裡。](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="dbc41-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="dbc41-144">hello 完整服務 URI 表示使用 hello OData 規格的項目。</span><span class="sxs-lookup"><span data-stu-id="dbc41-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="dbc41-145">API 版本</span><span class="sxs-lookup"><span data-stu-id="dbc41-145">API version</span></span>
<span data-ttu-id="dbc41-146">每個 API 呼叫將會有，在 hello 結束時，呼叫應該設定的 api 版本查詢參數太"1.0 的"。</span><span class="sxs-lookup"><span data-stu-id="dbc41-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="dbc41-147">識別碼會區分大小寫</span><span class="sxs-lookup"><span data-stu-id="dbc41-147">IDs are case-sensitive</span></span>
<span data-ttu-id="dbc41-148">任何 hello Api，所傳回的識別碼會區分大小寫和後續的 API 呼叫中當做參數傳遞時應該如此使用。</span><span class="sxs-lookup"><span data-stu-id="dbc41-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="dbc41-149">例如，模型識別碼和目錄識別碼都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="dbc41-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="dbc41-150">建立模型</span><span class="sxs-lookup"><span data-stu-id="dbc41-150">Create a model</span></span>
<span data-ttu-id="dbc41-151">建立「製作模型」要求：</span><span class="sxs-lookup"><span data-stu-id="dbc41-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="dbc41-152">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-152">HTTP Method</span></span> | <span data-ttu-id="dbc41-153">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-154">POST</span><span class="sxs-lookup"><span data-stu-id="dbc41-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-155">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-156">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-156">Parameter Name</span></span> | <span data-ttu-id="dbc41-157">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-158">modelName</span><span class="sxs-lookup"><span data-stu-id="dbc41-158">modelName</span></span> |<span data-ttu-id="dbc41-159">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="dbc41-160">最大長度：20</span><span class="sxs-lookup"><span data-stu-id="dbc41-160">Max length: 20</span></span> |
| <span data-ttu-id="dbc41-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-161">apiVersion</span></span> |<span data-ttu-id="dbc41-162">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-162">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-163">要求本文</span><span class="sxs-lookup"><span data-stu-id="dbc41-163">Request Body</span></span> |<span data-ttu-id="dbc41-164">無</span><span class="sxs-lookup"><span data-stu-id="dbc41-164">NONE</span></span> |

<span data-ttu-id="dbc41-165">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-165">**Response**:</span></span>

<span data-ttu-id="dbc41-166">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="dbc41-167">`feed/entry/content/properties/id`-包含 hello 模型識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="dbc41-168">請注意 hello 模型識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="dbc41-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="dbc41-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="dbc41-170">匯入目錄資料</span><span class="sxs-lookup"><span data-stu-id="dbc41-170">Import catalog data</span></span>
<span data-ttu-id="dbc41-171">如果您上傳數個類別目錄檔案 toohello 相同模型的數次呼叫時，我們將會插入只有 hello 新目錄項目。</span><span class="sxs-lookup"><span data-stu-id="dbc41-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="dbc41-172">現有的項目仍會與 hello 原始值。</span><span class="sxs-lookup"><span data-stu-id="dbc41-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="dbc41-173">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-173">HTTP Method</span></span> | <span data-ttu-id="dbc41-174">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-175">POST</span><span class="sxs-lookup"><span data-stu-id="dbc41-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-176">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-177">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-177">Parameter Name</span></span> | <span data-ttu-id="dbc41-178">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-179">modelId</span><span class="sxs-lookup"><span data-stu-id="dbc41-179">modelId</span></span> |<span data-ttu-id="dbc41-180">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-181">檔名</span><span class="sxs-lookup"><span data-stu-id="dbc41-181">filename</span></span> |<span data-ttu-id="dbc41-182">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="dbc41-183">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="dbc41-184"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="dbc41-184">Max length: 50</span></span> |
| <span data-ttu-id="dbc41-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-185">apiVersion</span></span> |<span data-ttu-id="dbc41-186">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-186">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-187">要求本文</span><span class="sxs-lookup"><span data-stu-id="dbc41-187">Request Body</span></span> |<span data-ttu-id="dbc41-188">目錄資料。</span><span class="sxs-lookup"><span data-stu-id="dbc41-188">Catalog data.</span></span> <span data-ttu-id="dbc41-189">格式：</span><span class="sxs-lookup"><span data-stu-id="dbc41-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="dbc41-190">名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-190">Name</span></span></th><th><span data-ttu-id="dbc41-191">強制</span><span class="sxs-lookup"><span data-stu-id="dbc41-191">Mandatory</span></span></th><th><span data-ttu-id="dbc41-192">類型</span><span class="sxs-lookup"><span data-stu-id="dbc41-192">Type</span></span></th><th><span data-ttu-id="dbc41-193">說明</span><span class="sxs-lookup"><span data-stu-id="dbc41-193">Description</span></span></th></tr><tr><td><span data-ttu-id="dbc41-194">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-194">Item Id</span></span></td><td><span data-ttu-id="dbc41-195">是</span><span class="sxs-lookup"><span data-stu-id="dbc41-195">Yes</span></span></td><td><span data-ttu-id="dbc41-196">英數字元，最大長度 50</span><span class="sxs-lookup"><span data-stu-id="dbc41-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="dbc41-197">項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="dbc41-198">項目名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-198">Item Name</span></span></td><td><span data-ttu-id="dbc41-199">是</span><span class="sxs-lookup"><span data-stu-id="dbc41-199">Yes</span></span></td><td><span data-ttu-id="dbc41-200">英數字元，最大長度 255</span><span class="sxs-lookup"><span data-stu-id="dbc41-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="dbc41-201">項目名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="dbc41-202">項目類別</span><span class="sxs-lookup"><span data-stu-id="dbc41-202">Item Category</span></span></td><td><span data-ttu-id="dbc41-203">是</span><span class="sxs-lookup"><span data-stu-id="dbc41-203">Yes</span></span></td><td><span data-ttu-id="dbc41-204">英數字元，最大長度 255</span><span class="sxs-lookup"><span data-stu-id="dbc41-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="dbc41-205">這項目 （例如烹飪的書籍，戲劇...） 所屬的類別目錄 toowhich</span><span class="sxs-lookup"><span data-stu-id="dbc41-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="dbc41-206">說明</span><span class="sxs-lookup"><span data-stu-id="dbc41-206">Description</span></span></td><td><span data-ttu-id="dbc41-207">否</span><span class="sxs-lookup"><span data-stu-id="dbc41-207">No</span></span></td><td><span data-ttu-id="dbc41-208">英數字元，最大長度 4000</span><span class="sxs-lookup"><span data-stu-id="dbc41-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="dbc41-209">此項目的說明</span><span class="sxs-lookup"><span data-stu-id="dbc41-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="dbc41-210">檔案大小上限為 200MB。</span><span class="sxs-lookup"><span data-stu-id="dbc41-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="dbc41-211">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="dbc41-212">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-212">**Response**:</span></span>

<span data-ttu-id="dbc41-213">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="dbc41-214">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="dbc41-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="dbc41-215">`Feed\entry\content\properties\ErrorCount`-不因為 tooan 錯誤插入的行數。</span><span class="sxs-lookup"><span data-stu-id="dbc41-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="dbc41-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="dbc41-217">匯入使用資料</span><span class="sxs-lookup"><span data-stu-id="dbc41-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="dbc41-218">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="dbc41-218">Uploading a file</span></span>
<span data-ttu-id="dbc41-219">本節說明如何使用檔案 tooupload 使用量資料。</span><span class="sxs-lookup"><span data-stu-id="dbc41-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="dbc41-220">您可以利用使用資料呼叫此 API 數次。</span><span class="sxs-lookup"><span data-stu-id="dbc41-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="dbc41-221">將會針對所有呼叫儲存所有使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="dbc41-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="dbc41-222">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-222">HTTP Method</span></span> | <span data-ttu-id="dbc41-223">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-224">POST</span><span class="sxs-lookup"><span data-stu-id="dbc41-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-225">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-226">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-226">Parameter Name</span></span> | <span data-ttu-id="dbc41-227">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-228">modelId</span><span class="sxs-lookup"><span data-stu-id="dbc41-228">modelId</span></span> |<span data-ttu-id="dbc41-229">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-230">檔名</span><span class="sxs-lookup"><span data-stu-id="dbc41-230">filename</span></span> |<span data-ttu-id="dbc41-231">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="dbc41-232">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="dbc41-233"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="dbc41-233">Max length: 50</span></span> |
| <span data-ttu-id="dbc41-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-234">apiVersion</span></span> |<span data-ttu-id="dbc41-235">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-235">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-236">要求本文</span><span class="sxs-lookup"><span data-stu-id="dbc41-236">Request Body</span></span> |<span data-ttu-id="dbc41-237">使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="dbc41-237">Usage data.</span></span> <span data-ttu-id="dbc41-238">格式：</span><span class="sxs-lookup"><span data-stu-id="dbc41-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="dbc41-239">名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-239">Name</span></span></th><th><span data-ttu-id="dbc41-240">強制</span><span class="sxs-lookup"><span data-stu-id="dbc41-240">Mandatory</span></span></th><th><span data-ttu-id="dbc41-241">類型</span><span class="sxs-lookup"><span data-stu-id="dbc41-241">Type</span></span></th><th><span data-ttu-id="dbc41-242">說明</span><span class="sxs-lookup"><span data-stu-id="dbc41-242">Description</span></span></th></tr><tr><td><span data-ttu-id="dbc41-243">使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-243">User Id</span></span></td><td><span data-ttu-id="dbc41-244">是</span><span class="sxs-lookup"><span data-stu-id="dbc41-244">Yes</span></span></td><td><span data-ttu-id="dbc41-245">英數字元</span><span class="sxs-lookup"><span data-stu-id="dbc41-245">Alphanumeric</span></span></td><td><span data-ttu-id="dbc41-246">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="dbc41-247">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-247">Item Id</span></span></td><td><span data-ttu-id="dbc41-248">是</span><span class="sxs-lookup"><span data-stu-id="dbc41-248">Yes</span></span></td><td><span data-ttu-id="dbc41-249">英數字元，最大長度 50</span><span class="sxs-lookup"><span data-stu-id="dbc41-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="dbc41-250">項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="dbc41-251">時間</span><span class="sxs-lookup"><span data-stu-id="dbc41-251">Time</span></span></td><td><span data-ttu-id="dbc41-252">否</span><span class="sxs-lookup"><span data-stu-id="dbc41-252">No</span></span></td><td><span data-ttu-id="dbc41-253">日期格式：YYYY/MM/DDTHH:MM:SS (例如 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="dbc41-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="dbc41-254">資料的時間</span><span class="sxs-lookup"><span data-stu-id="dbc41-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="dbc41-255">Event</span><span class="sxs-lookup"><span data-stu-id="dbc41-255">Event</span></span></td><td><span data-ttu-id="dbc41-256">否，如果提供，必須也提供日期</span><span class="sxs-lookup"><span data-stu-id="dbc41-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="dbc41-257">下列其中一種 hello:</span><span class="sxs-lookup"><span data-stu-id="dbc41-257">One of hello following:</span></span><br><span data-ttu-id="dbc41-258">• Click</span><span class="sxs-lookup"><span data-stu-id="dbc41-258">• Click</span></span><br><span data-ttu-id="dbc41-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="dbc41-259">• RecommendationClick</span></span><br><span data-ttu-id="dbc41-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="dbc41-260">•    AddShopCart</span></span><br><span data-ttu-id="dbc41-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="dbc41-261">• RemoveShopCart</span></span><br><span data-ttu-id="dbc41-262">• 購買</span><span class="sxs-lookup"><span data-stu-id="dbc41-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="dbc41-263">檔案大小上限為 200MB。</span><span class="sxs-lookup"><span data-stu-id="dbc41-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="dbc41-264">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="dbc41-265">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-265">**Response**:</span></span>

<span data-ttu-id="dbc41-266">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="dbc41-267">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="dbc41-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="dbc41-268">`Feed\entry\content\properties\ErrorCount`-不因為 tooan 錯誤插入的行數。</span><span class="sxs-lookup"><span data-stu-id="dbc41-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="dbc41-269">`Feed\entry\content\properties\FileId` - 檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="dbc41-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="dbc41-271">使用資料擷取</span><span class="sxs-lookup"><span data-stu-id="dbc41-271">Using data acquisition</span></span>
<span data-ttu-id="dbc41-272">本節說明如何在真實 toosend 事件時間 tooAzure 機器學習的建議事項，通常是從您的網站。</span><span class="sxs-lookup"><span data-stu-id="dbc41-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="dbc41-273">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-273">HTTP Method</span></span> | <span data-ttu-id="dbc41-274">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-275">POST</span><span class="sxs-lookup"><span data-stu-id="dbc41-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-276">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-276">Parameter Name</span></span> | <span data-ttu-id="dbc41-277">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-278">apiVersion</span></span> |<span data-ttu-id="dbc41-279">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-279">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-280">Request body</span><span class="sxs-lookup"><span data-stu-id="dbc41-280">Request body</span></span> |<span data-ttu-id="dbc41-281">事件資料輸入您要為每個事件 toosend。</span><span class="sxs-lookup"><span data-stu-id="dbc41-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="dbc41-282">您應該傳送的 hello 相同的使用者或瀏覽器工作階段 hello hello SessionId 欄位中的相同識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="dbc41-283">(請參閱下面的事件本文範例。)</span><span class="sxs-lookup"><span data-stu-id="dbc41-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="dbc41-284">事件 'Click' 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="dbc41-285">事件 'RecommendationClick' 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="dbc41-286">事件 'AddShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="dbc41-287">事件 'RemoveShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="dbc41-288">事件 'Purchase' 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="dbc41-289">傳送 2 個事件 ('Click' 和 'AddShopCart') 的範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="dbc41-290">**回應**：HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="dbc41-291">建立建議模型</span><span class="sxs-lookup"><span data-stu-id="dbc41-291">Build a recommendation model</span></span>
| <span data-ttu-id="dbc41-292">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-292">HTTP Method</span></span> | <span data-ttu-id="dbc41-293">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-294">POST</span><span class="sxs-lookup"><span data-stu-id="dbc41-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-295">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-296">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-296">Parameter Name</span></span> | <span data-ttu-id="dbc41-297">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-298">modelId</span><span class="sxs-lookup"><span data-stu-id="dbc41-298">modelId</span></span> |<span data-ttu-id="dbc41-299">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="dbc41-300">userDescription</span></span> |<span data-ttu-id="dbc41-301">文字 hello 目錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="dbc41-302">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="dbc41-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="dbc41-303">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="dbc41-303">See example above.</span></span><br><span data-ttu-id="dbc41-304"> 最大長度：50</span><span class="sxs-lookup"><span data-stu-id="dbc41-304">Max length: 50</span></span> |
| <span data-ttu-id="dbc41-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-305">apiVersion</span></span> |<span data-ttu-id="dbc41-306">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-306">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-307">要求本文</span><span class="sxs-lookup"><span data-stu-id="dbc41-307">Request Body</span></span> |<span data-ttu-id="dbc41-308">無</span><span class="sxs-lookup"><span data-stu-id="dbc41-308">NONE</span></span> |

<span data-ttu-id="dbc41-309">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-309">**Response**:</span></span>

<span data-ttu-id="dbc41-310">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-310">HTTP Status code: 200</span></span>

<span data-ttu-id="dbc41-311">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="dbc41-311">This is an asynchronous API.</span></span> <span data-ttu-id="dbc41-312">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="dbc41-312">You will get a build ID as a response.</span></span> <span data-ttu-id="dbc41-313">tooknow hello 建置結束時，您應該呼叫 hello 「 取得組建狀態的模型 」 應用程式開發介面，並找出這個組建 ID hello 回應中。</span><span class="sxs-lookup"><span data-stu-id="dbc41-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="dbc41-314">請注意，組建可以從分鐘 toohours hello hello 資料大小而定。</span><span class="sxs-lookup"><span data-stu-id="dbc41-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="dbc41-315">您無法使用建議，直到 hello 建置結束。</span><span class="sxs-lookup"><span data-stu-id="dbc41-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="dbc41-316">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="dbc41-316">Valid build status:</span></span>

* <span data-ttu-id="dbc41-317">建立 – 模型已建立。</span><span class="sxs-lookup"><span data-stu-id="dbc41-317">Create – Model was created.</span></span>
* <span data-ttu-id="dbc41-318">已排入佇列 – 已觸發模型組建，並已排入佇列。</span><span class="sxs-lookup"><span data-stu-id="dbc41-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="dbc41-319">建置中 – 模型正在建置中。</span><span class="sxs-lookup"><span data-stu-id="dbc41-319">Building – Model is being built.</span></span>
* <span data-ttu-id="dbc41-320">成功 – 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="dbc41-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="dbc41-321">錯誤 – 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="dbc41-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="dbc41-322">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="dbc41-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="dbc41-323">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="dbc41-324">請注意可以在 hello 下列路徑下找到 ID 該 hello 組建：`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="dbc41-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="dbc41-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="dbc41-326">取得模型的組建狀態</span><span class="sxs-lookup"><span data-stu-id="dbc41-326">Get build status of a model</span></span>
| <span data-ttu-id="dbc41-327">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-327">HTTP Method</span></span> | <span data-ttu-id="dbc41-328">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-329">GET</span><span class="sxs-lookup"><span data-stu-id="dbc41-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-330">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-331">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-331">Parameter Name</span></span> | <span data-ttu-id="dbc41-332">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-333">modelId</span><span class="sxs-lookup"><span data-stu-id="dbc41-333">modelId</span></span> |<span data-ttu-id="dbc41-334">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="dbc41-335">onlyLastBuild</span></span> |<span data-ttu-id="dbc41-336">表示所有 hello 的 tooreturn 建置 hello 模型的歷程記錄] 或 [僅 hello 狀態的 hello 最新的組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="dbc41-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-337">apiVersion</span></span> |<span data-ttu-id="dbc41-338">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-338">1.0</span></span> |

<span data-ttu-id="dbc41-339">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-339">**Response**:</span></span>

<span data-ttu-id="dbc41-340">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-340">HTTP Status code: 200</span></span>

<span data-ttu-id="dbc41-341">hello 回應會包含每一組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="dbc41-341">hello response includes one entry per build.</span></span> <span data-ttu-id="dbc41-342">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="dbc41-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="dbc41-343">`feed/entry/content/properties/UserName`– Hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="dbc41-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="dbc41-344">`feed/entry/content/properties/ModelName`– Hello 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="dbc41-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="dbc41-345">`feed/entry/content/properties/ModelId` – 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="dbc41-346">`feed/entry/content/properties/IsDeployed`– Hello 建置是否部署 （也稱為</span><span class="sxs-lookup"><span data-stu-id="dbc41-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="dbc41-347">作用中組建)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-347">active build).</span></span>
* <span data-ttu-id="dbc41-348">`feed/entry/content/properties/BuildId` – 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="dbc41-349">`feed/entry/content/properties/BuildType`Hello 組建的型別。</span><span class="sxs-lookup"><span data-stu-id="dbc41-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="dbc41-350">`feed/entry/content/properties/Status` – 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="dbc41-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="dbc41-351">可以是 hello 下列其中一種： 錯誤、 建置、 已佇列、 取消、 Canceled、 成功</span><span class="sxs-lookup"><span data-stu-id="dbc41-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="dbc41-352">`feed/entry/content/properties/StatusMessage`– 詳細狀態訊息 （適用於僅 toospecific 狀態）。</span><span class="sxs-lookup"><span data-stu-id="dbc41-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="dbc41-353">`feed/entry/content/properties/Progress` – 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="dbc41-354">`feed/entry/content/properties/StartTime` – 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="dbc41-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="dbc41-355">`feed/entry/content/properties/EndTime` – 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="dbc41-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="dbc41-356">`feed/entry/content/properties/ExecutionTime` – 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="dbc41-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="dbc41-357">`feed/entry/content/properties/ProgressStep`– Hello 正在建置進行中的目前階段有關的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dbc41-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="dbc41-358">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="dbc41-358">Valid build status:</span></span>

* <span data-ttu-id="dbc41-359">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="dbc41-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="dbc41-360">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="dbc41-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="dbc41-361">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="dbc41-361">Building – Build is in process.</span></span>
* <span data-ttu-id="dbc41-362">成功 – 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="dbc41-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="dbc41-363">錯誤 – 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="dbc41-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="dbc41-364">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="dbc41-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="dbc41-365">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="dbc41-366">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="dbc41-366">Valid values for build type:</span></span>

* <span data-ttu-id="dbc41-367">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-367">Rank - Rank build.</span></span> <span data-ttu-id="dbc41-368">（順位的組建詳細資料，請參閱 toohello"機器學習建議 API 文件集 」 文件。）</span><span class="sxs-lookup"><span data-stu-id="dbc41-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="dbc41-369">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="dbc41-370">Fbt - 經常一起購買的組建。</span><span class="sxs-lookup"><span data-stu-id="dbc41-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="dbc41-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="dbc41-372">取得建議</span><span class="sxs-lookup"><span data-stu-id="dbc41-372">Get recommendations</span></span>
| <span data-ttu-id="dbc41-373">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-373">HTTP Method</span></span> | <span data-ttu-id="dbc41-374">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-375">GET</span><span class="sxs-lookup"><span data-stu-id="dbc41-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-376">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-377">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-377">Parameter Name</span></span> | <span data-ttu-id="dbc41-378">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-379">modelId</span><span class="sxs-lookup"><span data-stu-id="dbc41-379">modelId</span></span> |<span data-ttu-id="dbc41-380">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="dbc41-381">itemIds</span></span> |<span data-ttu-id="dbc41-382">以逗號分隔的 hello 項目 toorecommend 的清單。</span><span class="sxs-lookup"><span data-stu-id="dbc41-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="dbc41-383">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="dbc41-383">Max length: 1024</span></span> |
| <span data-ttu-id="dbc41-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="dbc41-384">numberOfResults</span></span> |<span data-ttu-id="dbc41-385">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="dbc41-385">Number of required results</span></span> |
| <span data-ttu-id="dbc41-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="dbc41-386">includeMetatadata</span></span> |<span data-ttu-id="dbc41-387">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="dbc41-387">Future use, always false</span></span> |
| <span data-ttu-id="dbc41-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-388">apiVersion</span></span> |<span data-ttu-id="dbc41-389">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-389">1.0</span></span> |

<span data-ttu-id="dbc41-390">**回應：**</span><span class="sxs-lookup"><span data-stu-id="dbc41-390">**Response:**</span></span>

<span data-ttu-id="dbc41-391">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-391">HTTP Status code: 200</span></span>

<span data-ttu-id="dbc41-392">hello 回應包含一個項目，每個建議的項目。</span><span class="sxs-lookup"><span data-stu-id="dbc41-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="dbc41-393">每個項目具有下列資料的 hello:</span><span class="sxs-lookup"><span data-stu-id="dbc41-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="dbc41-394">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="dbc41-395">`Feed\entry\content\properties\Name`-Hello 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="dbc41-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="dbc41-396">`Feed\entry\content\properties\Rating`-Hello 建議; 的評等較高的數字表示較高信心。</span><span class="sxs-lookup"><span data-stu-id="dbc41-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="dbc41-397">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="dbc41-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="dbc41-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-398">OData XML</span></span>

<span data-ttu-id="dbc41-399">以下的 hello 範例回應會包含 10 個建議的項目：</span><span class="sxs-lookup"><span data-stu-id="dbc41-399">hello example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="dbc41-400">更新模型</span><span class="sxs-lookup"><span data-stu-id="dbc41-400">Update model</span></span>
<span data-ttu-id="dbc41-401">您可以更新 hello 模型描述或 hello 作用中的組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="dbc41-402">*作用中組建識別碼* - 每個模型的每個組建都有組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="dbc41-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="dbc41-403">hello 作用中的組建識別碼是模型的 hello 第一個成功的組建的每個新。</span><span class="sxs-lookup"><span data-stu-id="dbc41-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="dbc41-404">當您有使用中的組建 ID，而且請勿 hello 的其他組建相同的模型，您需要 tooexplicitly hello 預設組建識別碼如果您想要將它設定。</span><span class="sxs-lookup"><span data-stu-id="dbc41-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="dbc41-405">當您使用的建議事項，如果未指定您想 toouse，將會自動使用其中一種 hello 預設 hello 組建 ID。</span><span class="sxs-lookup"><span data-stu-id="dbc41-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="dbc41-406">這項機制可讓您的生產環境-toobuild 新模型中有推薦模型並測試它們，才能將它們提升 tooproduction 之後。</span><span class="sxs-lookup"><span data-stu-id="dbc41-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="dbc41-407">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="dbc41-407">HTTP Method</span></span> | <span data-ttu-id="dbc41-408">URI</span><span class="sxs-lookup"><span data-stu-id="dbc41-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-409">PUT</span><span class="sxs-lookup"><span data-stu-id="dbc41-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="dbc41-410">範例：</span><span class="sxs-lookup"><span data-stu-id="dbc41-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="dbc41-411">參數名稱</span><span class="sxs-lookup"><span data-stu-id="dbc41-411">Parameter Name</span></span> | <span data-ttu-id="dbc41-412">有效值</span><span class="sxs-lookup"><span data-stu-id="dbc41-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="dbc41-413">id</span><span class="sxs-lookup"><span data-stu-id="dbc41-413">id</span></span> |<span data-ttu-id="dbc41-414">Hello 模型 （區分大小寫） 的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="dbc41-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="dbc41-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="dbc41-415">apiVersion</span></span> |<span data-ttu-id="dbc41-416">1.0</span><span class="sxs-lookup"><span data-stu-id="dbc41-416">1.0</span></span> |
|  | |
| <span data-ttu-id="dbc41-417">要求本文</span><span class="sxs-lookup"><span data-stu-id="dbc41-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="dbc41-418">請注意 hello XML 標記的描述，並將 ActiveBuildId 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="dbc41-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="dbc41-419">如果您不想 tooset 描述或 ActiveBuildId，移除 hello 整個標記。</span><span class="sxs-lookup"><span data-stu-id="dbc41-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="dbc41-420">**回應**：</span><span class="sxs-lookup"><span data-stu-id="dbc41-420">**Response**:</span></span>

<span data-ttu-id="dbc41-421">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="dbc41-421">HTTP Status code: 200</span></span>

<span data-ttu-id="dbc41-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="dbc41-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="dbc41-423">法律</span><span class="sxs-lookup"><span data-stu-id="dbc41-423">Legal</span></span>
<span data-ttu-id="dbc41-424">這份文件依「現狀」提供。</span><span class="sxs-lookup"><span data-stu-id="dbc41-424">This document is provided "as-is".</span></span> <span data-ttu-id="dbc41-425">本文件中說明的資訊與畫面 (包括 URL 及其他網際網路網站參考資料) 如有變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="dbc41-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="dbc41-426">此處描述的一些範例僅供說明之用，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="dbc41-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="dbc41-427">並未影射或關聯任何真實的人、事、物。</span><span class="sxs-lookup"><span data-stu-id="dbc41-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="dbc41-428">本文件不會提供您任何法律權限 tooany 智慧財產權的任何 Microsoft 產品。</span><span class="sxs-lookup"><span data-stu-id="dbc41-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="dbc41-429">您可以複製並使用這份文件，供內部參考之用。</span><span class="sxs-lookup"><span data-stu-id="dbc41-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="dbc41-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dbc41-430">© 2014 Microsoft.</span></span> <span data-ttu-id="dbc41-431">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="dbc41-431">All rights reserved.</span></span> 

