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
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="4e1cb-104">Machine Learning 建議 API 的快速入門指南 (版本 1)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="4e1cb-105">您應該開始使用[建議 API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api)，而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="4e1cb-106">Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="4e1cb-107">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="4e1cb-108">深入了解[移轉到新的 Cognitive Service](http://aka.ms/recomigrate)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="4e1cb-109">本文說明如何準備您的服務或應用程式來開始使用 Microsoft Azure Machine Learning 建議。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="4e1cb-110">您可以在 [Cortana 智慧資源庫 (英文)](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2) 中找到建議 API 的更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="4e1cb-111">一般概觀</span><span class="sxs-lookup"><span data-stu-id="4e1cb-111">General overview</span></span>
<span data-ttu-id="4e1cb-112">若要使用 Azure Machine Learning 建議，您需要執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="4e1cb-113">建立模型 - 模型是使用狀況資料、目錄資料和建議模型的容器。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="4e1cb-114">匯入目錄資料 - 目錄包含項目的中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="4e1cb-115">匯入使用狀況資料 - 上傳使用狀況資料的方式有 2 種 (使用其中一種或兩種皆用)：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="4e1cb-116">上傳包含使用資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="4e1cb-117">傳送資料擷取事件。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="4e1cb-118">通常您會上傳使用方式檔案以便建立初始建議模型 (啟動程序)，並使用這個模型，直到系統收集採用資料擷取格式的足夠資料為止。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="4e1cb-119">建置建議模型 - 這是非同步作業，建議系統會接受所有使用資料並建立建議模型。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="4e1cb-120">視資料大小和組建組態參數而定，這項作業可能需要數分鐘或數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="4e1cb-121">當觸發組建時，您會取得一個組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="4e1cb-122">請在開始取用建議之前，使用它來查看建置流程何時結束。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="4e1cb-123">取用建議 - 取得特定項目或項目清單的建議。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="4e1cb-124">上述所有步驟都是透過 Azure Machine Learning 建議 API 完成。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="4e1cb-125">您可下載也從 [資源庫](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="4e1cb-126">限制</span><span class="sxs-lookup"><span data-stu-id="4e1cb-126">Limitations</span></span>
* <span data-ttu-id="4e1cb-127">每個訂用帳戶的模型數上限是 10。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="4e1cb-128">一個目錄可以保留的項目數上限是 100,000。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="4e1cb-129">保留的使用點數上限是 ~5,000,000。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="4e1cb-130">如果將上傳或回報新的點，就會將最舊的點刪除。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="4e1cb-131">POST 中可以傳送的資料大小上限 (例如，匯入目錄資料、匯入使用狀況資料) 是 200MB。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="4e1cb-132">非作用中建議模型組建的每秒交易數目是 ~ 2TPS。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="4e1cb-133">作用中建議模型組建可以保留高達 20TPS。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="4e1cb-134">整合</span><span class="sxs-lookup"><span data-stu-id="4e1cb-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="4e1cb-135">驗證</span><span class="sxs-lookup"><span data-stu-id="4e1cb-135">Authentication</span></span>
<span data-ttu-id="4e1cb-136">Microsoft Azure Marketplace 支援基本或 OAuth 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="4e1cb-137">巡覽至 [帳戶設定](https://datamarket.azure.com/account/keys)下 Marketplace 中的金鑰，即可輕鬆地找到帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="4e1cb-138">基本驗證</span><span class="sxs-lookup"><span data-stu-id="4e1cb-138">Basic Authentication</span></span>
<span data-ttu-id="4e1cb-139">加入驗證標頭：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="4e1cb-140">轉換成 Base64 (C#)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="4e1cb-141">轉換成 Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="4e1cb-142">服務 URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-142">Service URI</span></span>
<span data-ttu-id="4e1cb-143">Azure Machine Learning 建議 API 的服務根 URI 在 [這裡。](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="4e1cb-144">完整服務 URI 是使用 OData 規格的元素來表示。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="4e1cb-145">API 版本</span><span class="sxs-lookup"><span data-stu-id="4e1cb-145">API version</span></span>
<span data-ttu-id="4e1cb-146">每個 API 呼叫最後會有名為 apiVersion 的查詢參數 (應設定為 "1.0")。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="4e1cb-147">識別碼會區分大小寫</span><span class="sxs-lookup"><span data-stu-id="4e1cb-147">IDs are case-sensitive</span></span>
<span data-ttu-id="4e1cb-148">任何 API 所傳回的識別碼都會區分大小寫，且在後續 API 呼叫中做為參數傳遞時，也應該如此使用。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="4e1cb-149">例如，模型識別碼和目錄識別碼都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="4e1cb-150">建立模型</span><span class="sxs-lookup"><span data-stu-id="4e1cb-150">Create a model</span></span>
<span data-ttu-id="4e1cb-151">建立「製作模型」要求：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="4e1cb-152">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-152">HTTP Method</span></span> | <span data-ttu-id="4e1cb-153">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-154">POST</span><span class="sxs-lookup"><span data-stu-id="4e1cb-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-155">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-156">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-156">Parameter Name</span></span> | <span data-ttu-id="4e1cb-157">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-158">modelName</span><span class="sxs-lookup"><span data-stu-id="4e1cb-158">modelName</span></span> |<span data-ttu-id="4e1cb-159">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4e1cb-160">最大長度：20</span><span class="sxs-lookup"><span data-stu-id="4e1cb-160">Max length: 20</span></span> |
| <span data-ttu-id="4e1cb-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-161">apiVersion</span></span> |<span data-ttu-id="4e1cb-162">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-162">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-163">要求本文</span><span class="sxs-lookup"><span data-stu-id="4e1cb-163">Request Body</span></span> |<span data-ttu-id="4e1cb-164">無</span><span class="sxs-lookup"><span data-stu-id="4e1cb-164">NONE</span></span> |

<span data-ttu-id="4e1cb-165">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-165">**Response**:</span></span>

<span data-ttu-id="4e1cb-166">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="4e1cb-167">`feed/entry/content/properties/id` – 包含模型識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="4e1cb-168">請注意，模型識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="4e1cb-169">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="4e1cb-170">匯入目錄資料</span><span class="sxs-lookup"><span data-stu-id="4e1cb-170">Import catalog data</span></span>
<span data-ttu-id="4e1cb-171">如果您將數個目錄檔案上傳至具有多個呼叫的相同模型，我們只會插入新的目錄項目。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="4e1cb-172">現有的項目會保留原始值。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="4e1cb-173">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-173">HTTP Method</span></span> | <span data-ttu-id="4e1cb-174">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-175">POST</span><span class="sxs-lookup"><span data-stu-id="4e1cb-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-176">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-177">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-177">Parameter Name</span></span> | <span data-ttu-id="4e1cb-178">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-179">modelId</span><span class="sxs-lookup"><span data-stu-id="4e1cb-179">modelId</span></span> |<span data-ttu-id="4e1cb-180">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-181">檔名</span><span class="sxs-lookup"><span data-stu-id="4e1cb-181">filename</span></span> |<span data-ttu-id="4e1cb-182">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="4e1cb-183">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4e1cb-184">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="4e1cb-184">Max length: 50</span></span> |
| <span data-ttu-id="4e1cb-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-185">apiVersion</span></span> |<span data-ttu-id="4e1cb-186">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-186">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-187">要求本文</span><span class="sxs-lookup"><span data-stu-id="4e1cb-187">Request Body</span></span> |<span data-ttu-id="4e1cb-188">目錄資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-188">Catalog data.</span></span> <span data-ttu-id="4e1cb-189">格式：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="4e1cb-190">名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-190">Name</span></span></th><th><span data-ttu-id="4e1cb-191">強制</span><span class="sxs-lookup"><span data-stu-id="4e1cb-191">Mandatory</span></span></th><th><span data-ttu-id="4e1cb-192">類型</span><span class="sxs-lookup"><span data-stu-id="4e1cb-192">Type</span></span></th><th><span data-ttu-id="4e1cb-193">說明</span><span class="sxs-lookup"><span data-stu-id="4e1cb-193">Description</span></span></th></tr><tr><td><span data-ttu-id="4e1cb-194">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-194">Item Id</span></span></td><td><span data-ttu-id="4e1cb-195">是</span><span class="sxs-lookup"><span data-stu-id="4e1cb-195">Yes</span></span></td><td><span data-ttu-id="4e1cb-196">英數字元，最大長度 50</span><span class="sxs-lookup"><span data-stu-id="4e1cb-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="4e1cb-197">項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-198">項目名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-198">Item Name</span></span></td><td><span data-ttu-id="4e1cb-199">是</span><span class="sxs-lookup"><span data-stu-id="4e1cb-199">Yes</span></span></td><td><span data-ttu-id="4e1cb-200">英數字元，最大長度 255</span><span class="sxs-lookup"><span data-stu-id="4e1cb-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="4e1cb-201">項目名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-202">項目類別</span><span class="sxs-lookup"><span data-stu-id="4e1cb-202">Item Category</span></span></td><td><span data-ttu-id="4e1cb-203">是</span><span class="sxs-lookup"><span data-stu-id="4e1cb-203">Yes</span></span></td><td><span data-ttu-id="4e1cb-204">英數字元，最大長度 255</span><span class="sxs-lookup"><span data-stu-id="4e1cb-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="4e1cb-205">此項目所屬類別 (例如烹飪書籍、劇本...)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-206">說明</span><span class="sxs-lookup"><span data-stu-id="4e1cb-206">Description</span></span></td><td><span data-ttu-id="4e1cb-207">否</span><span class="sxs-lookup"><span data-stu-id="4e1cb-207">No</span></span></td><td><span data-ttu-id="4e1cb-208">英數字元，最大長度 4000</span><span class="sxs-lookup"><span data-stu-id="4e1cb-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="4e1cb-209">此項目的說明</span><span class="sxs-lookup"><span data-stu-id="4e1cb-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="4e1cb-210">檔案大小上限為 200MB。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="4e1cb-211">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="4e1cb-212">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-212">**Response**:</span></span>

<span data-ttu-id="4e1cb-213">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="4e1cb-214">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4e1cb-215">`Feed\entry\content\properties\ErrorCount` - 因錯誤而未插入的行數。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="4e1cb-216">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="4e1cb-217">匯入使用資料</span><span class="sxs-lookup"><span data-stu-id="4e1cb-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="4e1cb-218">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="4e1cb-218">Uploading a file</span></span>
<span data-ttu-id="4e1cb-219">本節試範如何使用檔案上傳使用資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="4e1cb-220">您可以利用使用資料呼叫此 API 數次。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="4e1cb-221">將會針對所有呼叫儲存所有使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="4e1cb-222">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-222">HTTP Method</span></span> | <span data-ttu-id="4e1cb-223">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-224">POST</span><span class="sxs-lookup"><span data-stu-id="4e1cb-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-225">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-226">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-226">Parameter Name</span></span> | <span data-ttu-id="4e1cb-227">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-228">modelId</span><span class="sxs-lookup"><span data-stu-id="4e1cb-228">modelId</span></span> |<span data-ttu-id="4e1cb-229">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-230">檔名</span><span class="sxs-lookup"><span data-stu-id="4e1cb-230">filename</span></span> |<span data-ttu-id="4e1cb-231">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="4e1cb-232">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="4e1cb-233">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="4e1cb-233">Max length: 50</span></span> |
| <span data-ttu-id="4e1cb-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-234">apiVersion</span></span> |<span data-ttu-id="4e1cb-235">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-235">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-236">要求本文</span><span class="sxs-lookup"><span data-stu-id="4e1cb-236">Request Body</span></span> |<span data-ttu-id="4e1cb-237">使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-237">Usage data.</span></span> <span data-ttu-id="4e1cb-238">格式：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="4e1cb-239">名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-239">Name</span></span></th><th><span data-ttu-id="4e1cb-240">強制</span><span class="sxs-lookup"><span data-stu-id="4e1cb-240">Mandatory</span></span></th><th><span data-ttu-id="4e1cb-241">類型</span><span class="sxs-lookup"><span data-stu-id="4e1cb-241">Type</span></span></th><th><span data-ttu-id="4e1cb-242">說明</span><span class="sxs-lookup"><span data-stu-id="4e1cb-242">Description</span></span></th></tr><tr><td><span data-ttu-id="4e1cb-243">使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-243">User Id</span></span></td><td><span data-ttu-id="4e1cb-244">是</span><span class="sxs-lookup"><span data-stu-id="4e1cb-244">Yes</span></span></td><td><span data-ttu-id="4e1cb-245">英數字元</span><span class="sxs-lookup"><span data-stu-id="4e1cb-245">Alphanumeric</span></span></td><td><span data-ttu-id="4e1cb-246">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-247">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-247">Item Id</span></span></td><td><span data-ttu-id="4e1cb-248">是</span><span class="sxs-lookup"><span data-stu-id="4e1cb-248">Yes</span></span></td><td><span data-ttu-id="4e1cb-249">英數字元，最大長度 50</span><span class="sxs-lookup"><span data-stu-id="4e1cb-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="4e1cb-250">項目的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="4e1cb-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-251">時間</span><span class="sxs-lookup"><span data-stu-id="4e1cb-251">Time</span></span></td><td><span data-ttu-id="4e1cb-252">否</span><span class="sxs-lookup"><span data-stu-id="4e1cb-252">No</span></span></td><td><span data-ttu-id="4e1cb-253">日期格式：YYYY/MM/DDTHH:MM:SS (例如 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="4e1cb-254">資料的時間</span><span class="sxs-lookup"><span data-stu-id="4e1cb-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="4e1cb-255">Event</span><span class="sxs-lookup"><span data-stu-id="4e1cb-255">Event</span></span></td><td><span data-ttu-id="4e1cb-256">否，如果提供，必須也提供日期</span><span class="sxs-lookup"><span data-stu-id="4e1cb-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="4e1cb-257">下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-257">One of the following:</span></span><br><span data-ttu-id="4e1cb-258">• Click</span><span class="sxs-lookup"><span data-stu-id="4e1cb-258">• Click</span></span><br><span data-ttu-id="4e1cb-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="4e1cb-259">• RecommendationClick</span></span><br><span data-ttu-id="4e1cb-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="4e1cb-260">•    AddShopCart</span></span><br><span data-ttu-id="4e1cb-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="4e1cb-261">• RemoveShopCart</span></span><br><span data-ttu-id="4e1cb-262">• 購買</span><span class="sxs-lookup"><span data-stu-id="4e1cb-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="4e1cb-263">檔案大小上限為 200MB。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="4e1cb-264">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="4e1cb-265">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-265">**Response**:</span></span>

<span data-ttu-id="4e1cb-266">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="4e1cb-267">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="4e1cb-268">`Feed\entry\content\properties\ErrorCount` - 因錯誤而未插入的行數。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="4e1cb-269">`Feed\entry\content\properties\FileId` - 檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="4e1cb-270">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="4e1cb-271">使用資料擷取</span><span class="sxs-lookup"><span data-stu-id="4e1cb-271">Using data acquisition</span></span>
<span data-ttu-id="4e1cb-272">本節示範如何將事件即時傳送到 Azure Machine Learning 建議 (通常是從您的網站)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="4e1cb-273">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-273">HTTP Method</span></span> | <span data-ttu-id="4e1cb-274">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-275">POST</span><span class="sxs-lookup"><span data-stu-id="4e1cb-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-276">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-276">Parameter Name</span></span> | <span data-ttu-id="4e1cb-277">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-278">apiVersion</span></span> |<span data-ttu-id="4e1cb-279">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-279">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-280">Request body</span><span class="sxs-lookup"><span data-stu-id="4e1cb-280">Request body</span></span> |<span data-ttu-id="4e1cb-281">您想要傳送的每個事件的事件資料項目。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="4e1cb-282">您應該為相同的使用者或瀏覽器工作階段在 SessionId 欄位中傳送相同的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="4e1cb-283">(請參閱下面的事件本文範例。)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="4e1cb-284">事件 'Click' 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="4e1cb-285">事件 'RecommendationClick' 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="4e1cb-286">事件 'AddShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="4e1cb-287">事件 'RemoveShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="4e1cb-288">事件 'Purchase' 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="4e1cb-289">傳送 2 個事件 ('Click' 和 'AddShopCart') 的範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="4e1cb-290">**回應**：HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="4e1cb-291">建立建議模型</span><span class="sxs-lookup"><span data-stu-id="4e1cb-291">Build a recommendation model</span></span>
| <span data-ttu-id="4e1cb-292">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-292">HTTP Method</span></span> | <span data-ttu-id="4e1cb-293">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-294">POST</span><span class="sxs-lookup"><span data-stu-id="4e1cb-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-295">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-296">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-296">Parameter Name</span></span> | <span data-ttu-id="4e1cb-297">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-298">modelId</span><span class="sxs-lookup"><span data-stu-id="4e1cb-298">modelId</span></span> |<span data-ttu-id="4e1cb-299">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="4e1cb-300">userDescription</span></span> |<span data-ttu-id="4e1cb-301">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="4e1cb-302">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="4e1cb-303">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-303">See example above.</span></span><br><span data-ttu-id="4e1cb-304">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="4e1cb-304">Max length: 50</span></span> |
| <span data-ttu-id="4e1cb-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-305">apiVersion</span></span> |<span data-ttu-id="4e1cb-306">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-306">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-307">要求本文</span><span class="sxs-lookup"><span data-stu-id="4e1cb-307">Request Body</span></span> |<span data-ttu-id="4e1cb-308">無</span><span class="sxs-lookup"><span data-stu-id="4e1cb-308">NONE</span></span> |

<span data-ttu-id="4e1cb-309">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-309">**Response**:</span></span>

<span data-ttu-id="4e1cb-310">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-310">HTTP Status code: 200</span></span>

<span data-ttu-id="4e1cb-311">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-311">This is an asynchronous API.</span></span> <span data-ttu-id="4e1cb-312">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-312">You will get a build ID as a response.</span></span> <span data-ttu-id="4e1cb-313">若要知道組建何時結束，您應該呼叫「取得模型的組建狀態」API，並在回應中找出這個組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="4e1cb-314">請注意，組建可能會花數分鐘到數小時的時間，視資料的大小而定。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="4e1cb-315">您無法取用建議直到組建結束。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="4e1cb-316">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-316">Valid build status:</span></span>

* <span data-ttu-id="4e1cb-317">建立 – 模型已建立。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-317">Create – Model was created.</span></span>
* <span data-ttu-id="4e1cb-318">已排入佇列 – 已觸發模型組建，並已排入佇列。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="4e1cb-319">建置中 – 模型正在建置中。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-319">Building – Model is being built.</span></span>
* <span data-ttu-id="4e1cb-320">成功 – 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="4e1cb-321">錯誤 – 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="4e1cb-322">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="4e1cb-323">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="4e1cb-324">請注意，組建識別碼可以在下列路徑下找到： `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="4e1cb-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="4e1cb-325">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="4e1cb-326">取得模型的組建狀態</span><span class="sxs-lookup"><span data-stu-id="4e1cb-326">Get build status of a model</span></span>
| <span data-ttu-id="4e1cb-327">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-327">HTTP Method</span></span> | <span data-ttu-id="4e1cb-328">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-329">GET</span><span class="sxs-lookup"><span data-stu-id="4e1cb-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-330">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-331">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-331">Parameter Name</span></span> | <span data-ttu-id="4e1cb-332">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-333">modelId</span><span class="sxs-lookup"><span data-stu-id="4e1cb-333">modelId</span></span> |<span data-ttu-id="4e1cb-334">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="4e1cb-335">onlyLastBuild</span></span> |<span data-ttu-id="4e1cb-336">指出是要傳回模型的所有組建歷程記錄，還是只傳回最近一個組建的狀態。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="4e1cb-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-337">apiVersion</span></span> |<span data-ttu-id="4e1cb-338">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-338">1.0</span></span> |

<span data-ttu-id="4e1cb-339">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-339">**Response**:</span></span>

<span data-ttu-id="4e1cb-340">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-340">HTTP Status code: 200</span></span>

<span data-ttu-id="4e1cb-341">回應會包含每個組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-341">The response includes one entry per build.</span></span> <span data-ttu-id="4e1cb-342">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-342">Each entry has the following data:</span></span>

* <span data-ttu-id="4e1cb-343">`feed/entry/content/properties/UserName` – 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="4e1cb-344">`feed/entry/content/properties/ModelName` – 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="4e1cb-345">`feed/entry/content/properties/ModelId` – 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="4e1cb-346">`feed/entry/content/properties/IsDeployed` - 組建是否已部署 (又稱為</span><span class="sxs-lookup"><span data-stu-id="4e1cb-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="4e1cb-347">作用中組建)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-347">active build).</span></span>
* <span data-ttu-id="4e1cb-348">`feed/entry/content/properties/BuildId` – 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="4e1cb-349">`feed/entry/content/properties/BuildType` - 組建類型。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="4e1cb-350">`feed/entry/content/properties/Status` – 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="4e1cb-351">可以是下列其中之一：錯誤、建置中、已排入佇列、取消中、已取消、成功</span><span class="sxs-lookup"><span data-stu-id="4e1cb-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="4e1cb-352">`feed/entry/content/properties/StatusMessage` – 詳細狀態訊息 (僅適用於特定狀態)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="4e1cb-353">`feed/entry/content/properties/Progress` – 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="4e1cb-354">`feed/entry/content/properties/StartTime` – 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="4e1cb-355">`feed/entry/content/properties/EndTime` – 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="4e1cb-356">`feed/entry/content/properties/ExecutionTime` – 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="4e1cb-357">`feed/entry/content/properties/ProgressStep` - 正在進行建置之目前階段的相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="4e1cb-358">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-358">Valid build status:</span></span>

* <span data-ttu-id="4e1cb-359">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="4e1cb-360">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="4e1cb-361">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-361">Building – Build is in process.</span></span>
* <span data-ttu-id="4e1cb-362">成功 – 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="4e1cb-363">錯誤 – 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="4e1cb-364">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="4e1cb-365">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="4e1cb-366">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-366">Valid values for build type:</span></span>

* <span data-ttu-id="4e1cb-367">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-367">Rank - Rank build.</span></span> <span data-ttu-id="4e1cb-368">(如需排名組建的詳細資訊，請參閱＜機器學習服務建議 API 文件＞一文)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="4e1cb-369">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="4e1cb-370">Fbt - 經常一起購買的組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="4e1cb-371">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="4e1cb-372">取得建議</span><span class="sxs-lookup"><span data-stu-id="4e1cb-372">Get recommendations</span></span>
| <span data-ttu-id="4e1cb-373">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-373">HTTP Method</span></span> | <span data-ttu-id="4e1cb-374">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-375">GET</span><span class="sxs-lookup"><span data-stu-id="4e1cb-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-376">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-377">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-377">Parameter Name</span></span> | <span data-ttu-id="4e1cb-378">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-379">modelId</span><span class="sxs-lookup"><span data-stu-id="4e1cb-379">modelId</span></span> |<span data-ttu-id="4e1cb-380">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="4e1cb-381">itemIds</span></span> |<span data-ttu-id="4e1cb-382">要建議的以逗號分隔項目清單。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="4e1cb-383">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="4e1cb-383">Max length: 1024</span></span> |
| <span data-ttu-id="4e1cb-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="4e1cb-384">numberOfResults</span></span> |<span data-ttu-id="4e1cb-385">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="4e1cb-385">Number of required results</span></span> |
| <span data-ttu-id="4e1cb-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="4e1cb-386">includeMetatadata</span></span> |<span data-ttu-id="4e1cb-387">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="4e1cb-387">Future use, always false</span></span> |
| <span data-ttu-id="4e1cb-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-388">apiVersion</span></span> |<span data-ttu-id="4e1cb-389">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-389">1.0</span></span> |

<span data-ttu-id="4e1cb-390">**回應：**</span><span class="sxs-lookup"><span data-stu-id="4e1cb-390">**Response:**</span></span>

<span data-ttu-id="4e1cb-391">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-391">HTTP Status code: 200</span></span>

<span data-ttu-id="4e1cb-392">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="4e1cb-393">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-393">Each entry has the following data:</span></span>

* <span data-ttu-id="4e1cb-394">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="4e1cb-395">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="4e1cb-396">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="4e1cb-397">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="4e1cb-398">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-398">OData XML</span></span>

<span data-ttu-id="4e1cb-399">以下範例回應包含 10 個建議項目：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-399">The example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="4e1cb-400">更新模型</span><span class="sxs-lookup"><span data-stu-id="4e1cb-400">Update model</span></span>
<span data-ttu-id="4e1cb-401">您可以更新模型描述或作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="4e1cb-402">*作用中組建識別碼* - 每個模型的每個組建都有組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="4e1cb-403">作用中組建識別碼是每個新模型的第一個成功組建。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="4e1cb-404">一旦您有作用中組建識別碼，而且您執行相同模型的其他組建，您必須是需要將它明確設為預設組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="4e1cb-405">當您取用建議時，如果您未指定想要使用的組建識別碼，則會自動使用預設值。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="4e1cb-406">此機制可讓您在生產環境中有建議模型時建置新模型，並先加以測試，再將其提升至生產環境。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="4e1cb-407">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="4e1cb-407">HTTP Method</span></span> | <span data-ttu-id="4e1cb-408">URI</span><span class="sxs-lookup"><span data-stu-id="4e1cb-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-409">PUT</span><span class="sxs-lookup"><span data-stu-id="4e1cb-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="4e1cb-410">範例：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="4e1cb-411">參數名稱</span><span class="sxs-lookup"><span data-stu-id="4e1cb-411">Parameter Name</span></span> | <span data-ttu-id="4e1cb-412">有效值</span><span class="sxs-lookup"><span data-stu-id="4e1cb-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e1cb-413">id</span><span class="sxs-lookup"><span data-stu-id="4e1cb-413">id</span></span> |<span data-ttu-id="4e1cb-414">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="4e1cb-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="4e1cb-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="4e1cb-415">apiVersion</span></span> |<span data-ttu-id="4e1cb-416">1.0</span><span class="sxs-lookup"><span data-stu-id="4e1cb-416">1.0</span></span> |
|  | |
| <span data-ttu-id="4e1cb-417">要求本文</span><span class="sxs-lookup"><span data-stu-id="4e1cb-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="4e1cb-418">請注意，XML 標籤說明和 ActiveBuildId 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="4e1cb-419">如果您不想設定 Description 或 ActiveBuildId，請移除整個標記。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="4e1cb-420">**回應**：</span><span class="sxs-lookup"><span data-stu-id="4e1cb-420">**Response**:</span></span>

<span data-ttu-id="4e1cb-421">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="4e1cb-421">HTTP Status code: 200</span></span>

<span data-ttu-id="4e1cb-422">OData XML</span><span class="sxs-lookup"><span data-stu-id="4e1cb-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="4e1cb-423">法律</span><span class="sxs-lookup"><span data-stu-id="4e1cb-423">Legal</span></span>
<span data-ttu-id="4e1cb-424">這份文件依「現狀」提供。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-424">This document is provided "as-is".</span></span> <span data-ttu-id="4e1cb-425">本文件中說明的資訊與畫面 (包括 URL 及其他網際網路網站參考資料) 如有變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="4e1cb-426">此處描述的一些範例僅供說明之用，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="4e1cb-427">並未影射或關聯任何真實的人、事、物。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="4e1cb-428">本文件未提供給您任何 Microsoft 產品中任何智慧財產的任何法定權利。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="4e1cb-429">您可以複製並使用這份文件，供內部參考之用。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="4e1cb-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4e1cb-430">© 2014 Microsoft.</span></span> <span data-ttu-id="4e1cb-431">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="4e1cb-431">All rights reserved.</span></span> 

