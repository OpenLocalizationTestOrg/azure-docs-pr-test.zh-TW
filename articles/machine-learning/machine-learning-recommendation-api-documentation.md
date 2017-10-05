---
title: "Machine Learning 建議 API 文件 | Microsoft Docs"
description: "Microsoft Azure Marketplace 中提供適用於建議引擎的 Azure Machine Learning 建議 API 文件。"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 1fba64d78d779344e2895b0d54419186b7584865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="0fde5-103">Azure Machine Learning 建議 API 文件</span><span class="sxs-lookup"><span data-stu-id="0fde5-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="0fde5-104">您應該開始使用 Recommendations API 的 Cognitive Service，而不是此版本。</span><span class="sxs-lookup"><span data-stu-id="0fde5-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="0fde5-105">Recommendations 的 Cognitive Service 將會取代這個服務，而所有的新特徵都會在其中進行開發。</span><span class="sxs-lookup"><span data-stu-id="0fde5-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="0fde5-106">它會提供新功能，例如，批次支援、更好的 API 總管、更簡潔的 API 介面、更一致的註冊/計費體驗等。</span><span class="sxs-lookup"><span data-stu-id="0fde5-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="0fde5-107">深入了解 [移轉到新的 Cognitive Service](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="0fde5-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="0fde5-108">本文件說明 Microsoft Azure Machine Learning 建議 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="0fde5-109">1.一般概觀</span><span class="sxs-lookup"><span data-stu-id="0fde5-109">1. General overview</span></span>
<span data-ttu-id="0fde5-110">本文件是 API 參考。</span><span class="sxs-lookup"><span data-stu-id="0fde5-110">This document is an API reference.</span></span> <span data-ttu-id="0fde5-111">您應該從＜Azure Machine Learning 建議 – 快速入門＞文件開始。</span><span class="sxs-lookup"><span data-stu-id="0fde5-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="0fde5-112">Azure Machine Learning 建議 API 可分成下列邏輯群組：</span><span class="sxs-lookup"><span data-stu-id="0fde5-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="0fde5-113"><ins>限制</ins> - 建議 API 限制。</span><span class="sxs-lookup"><span data-stu-id="0fde5-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="0fde5-114"><ins>一般資訊</ins> - 驗證、服務 URI 和版本控制的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0fde5-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="0fde5-115"><ins>模型基本操作</ins> - 可讓您對模型執行基本操作 (例如建立、更新及刪除模型) 的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="0fde5-116"><ins>模型進階操作</ins> - 可讓您深入了解模型相關進階資料的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="0fde5-117"><ins>模型商務規則</ins> - 可讓您管理模型建議結果之相關商業規則的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="0fde5-118"><ins>目錄</ins> - 可讓您對模型目錄執行基本操作的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="0fde5-119">目錄包含使用狀況資料項目的相關中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="0fde5-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="0fde5-120"><ins>功能</ins> - 可讓您深入了解目錄中的項目，以及如何使用這項資訊來建立更佳建議的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="0fde5-121"><ins>使用狀況資料</ins> - 可讓您對模型使用狀況資料執行基本操作的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="0fde5-122">基本格式的使用狀況資料由資料列組成，這些資料列包含成對的 &#60;userId&#62;,&#60;itemId&#62;。</span><span class="sxs-lookup"><span data-stu-id="0fde5-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="0fde5-123"><ins>組建</ins> - 能夠讓您觸發模型組建並執行與此組建相關之基本操作的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="0fde5-124">您可以在獲得有價值的使用狀況資料之後，觸發模型組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="0fde5-125"><ins>建議</ins> - 模型組建結束之後，可讓您取用建議的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="0fde5-126"><ins>使用者資料</ins> - 可讓您擷取使用者使用方式資料之相關資訊的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="0fde5-127"><ins>通知</ins> - 可讓您接收與 API 操作相關之問題通知的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="0fde5-128">(例如，您透過資料擷取回報使用量資料，而大部分的事件處理都失敗了。</span><span class="sxs-lookup"><span data-stu-id="0fde5-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="0fde5-129">這將會引發錯誤通知。)</span><span class="sxs-lookup"><span data-stu-id="0fde5-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="0fde5-130">2.限制</span><span class="sxs-lookup"><span data-stu-id="0fde5-130">2. Limitations</span></span>
* <span data-ttu-id="0fde5-131">每個訂用帳戶的模型數上限是 10。</span><span class="sxs-lookup"><span data-stu-id="0fde5-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="0fde5-132">每個模型的組建數上限是 20。</span><span class="sxs-lookup"><span data-stu-id="0fde5-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="0fde5-133">一個目錄可以保留的項目數上限是 100,000。</span><span class="sxs-lookup"><span data-stu-id="0fde5-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="0fde5-134">保留的使用點數上限是 ~5,000,000。</span><span class="sxs-lookup"><span data-stu-id="0fde5-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="0fde5-135">如果將上傳或回報新的點，就會將最舊的點刪除。</span><span class="sxs-lookup"><span data-stu-id="0fde5-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="0fde5-136">POST 中可以傳送的資料大小上限 (例如：匯入目錄資料、匯入使用資料) 是 200 MB。</span><span class="sxs-lookup"><span data-stu-id="0fde5-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="0fde5-137">取得建議時可以要求的項目數目上限為 150 個。</span><span class="sxs-lookup"><span data-stu-id="0fde5-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="0fde5-138">3.API – 一般資訊</span><span class="sxs-lookup"><span data-stu-id="0fde5-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="0fde5-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-139">3.1.</span></span> <span data-ttu-id="0fde5-140">驗證</span><span class="sxs-lookup"><span data-stu-id="0fde5-140">Authentication</span></span>
<span data-ttu-id="0fde5-141">請遵循與驗證相關的 Microsoft Azure Marketplace 指導方針。</span><span class="sxs-lookup"><span data-stu-id="0fde5-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="0fde5-142">Marketplace 可支援基本或 OAuth 驗證方法。</span><span class="sxs-lookup"><span data-stu-id="0fde5-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="0fde5-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-143">3.2.</span></span> <span data-ttu-id="0fde5-144">服務 URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-144">Service URI</span></span>
<span data-ttu-id="0fde5-145">Azure Machine Learning 建議 API 的服務根 URI 在 [這裡。](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="0fde5-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="0fde5-146">完整服務 URI 是使用 OData 規格的元素來表示。</span><span class="sxs-lookup"><span data-stu-id="0fde5-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="0fde5-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-147">3.3.</span></span> <span data-ttu-id="0fde5-148">API 版本</span><span class="sxs-lookup"><span data-stu-id="0fde5-148">API version</span></span>
<span data-ttu-id="0fde5-149">每個 API 呼叫最後會有名為 apiVersion 的查詢參數 (應設為 1.0)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="0fde5-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-150">3.4.</span></span> <span data-ttu-id="0fde5-151">識別碼會區分大小寫</span><span class="sxs-lookup"><span data-stu-id="0fde5-151">IDs are case sensitive</span></span>
<span data-ttu-id="0fde5-152">任何 API 所傳回的識別碼都會區分大小寫，且在後續 API 呼叫中做為參數傳遞時，也應該如此使用。</span><span class="sxs-lookup"><span data-stu-id="0fde5-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="0fde5-153">例如，模型識別碼和目錄識別碼都會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="0fde5-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="0fde5-154">4.建議品質和冷項目</span><span class="sxs-lookup"><span data-stu-id="0fde5-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="0fde5-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-155">4.1.</span></span> <span data-ttu-id="0fde5-156">建議品質</span><span class="sxs-lookup"><span data-stu-id="0fde5-156">Recommendation quality</span></span>
<span data-ttu-id="0fde5-157">建立建議模型通常足以允許系統提供建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="0fde5-158">不過，建議品質取決於處理的使用量以及目錄的涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="0fde5-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="0fde5-159">例如，如果您有許多冷項目 (沒有高使用量的項目)，系統很難提供建議給這類項目，或使用這類項目做為建議項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="0fde5-160">為了克服冷項目的問題，系統允許使用項目的中繼資料增強建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="0fde5-161">中繼資料可稱為功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-161">This metadata is referred to as features.</span></span> <span data-ttu-id="0fde5-162">典型的功能是書籍的作者或電影的演員。</span><span class="sxs-lookup"><span data-stu-id="0fde5-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="0fde5-163">功能是透過目錄，以索引鍵/值字串的格式提供。</span><span class="sxs-lookup"><span data-stu-id="0fde5-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="0fde5-164">若需目錄檔案的完整格式，請參閱 [匯入目錄區段](#81-import-catalog-data)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="0fde5-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-165">4.2.</span></span> <span data-ttu-id="0fde5-166">排名組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-166">Rank build</span></span>
<span data-ttu-id="0fde5-167">功能可增強建議模型，但若要這樣做需要使用有意義的功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="0fde5-168">為了這個目的，引入新的組建 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="0fde5-169">此組建會對功能的效益進行排名。</span><span class="sxs-lookup"><span data-stu-id="0fde5-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="0fde5-170">有意義的功能為排名分數 2 以上的功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="0fde5-171">了解哪些是有意義的功能之後，會利用有意義功能的清單 (或子清單) 觸發建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="0fde5-172">這樣就可以使用這些功能同時增強暖項目和冷項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="0fde5-173">若要將它們用於暖項目，應設定 `UseFeatureInModel` 組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="0fde5-174">若要將它們用於冷項目，應啟用 `AllowColdItemPlacement` 組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="0fde5-175">注意：不可能啟用 `AllowColdItemPlacement` 而不啟用 `UseFeatureInModel`。</span><span class="sxs-lookup"><span data-stu-id="0fde5-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="0fde5-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-176">4.3.</span></span> <span data-ttu-id="0fde5-177">建議推論</span><span class="sxs-lookup"><span data-stu-id="0fde5-177">Recommendation reasoning</span></span>
<span data-ttu-id="0fde5-178">建議推論是功能使用方式的另一個層面。</span><span class="sxs-lookup"><span data-stu-id="0fde5-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="0fde5-179">的確，Azure Machine Learning 建議引擎可以使用功能來提供建議說明 (也稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="0fde5-180">推理)，讓建議取用者對建議項目產生更多信心。</span><span class="sxs-lookup"><span data-stu-id="0fde5-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="0fde5-181">若要啟用推論，應在要求建議組建之前設定 `AllowFeatureCorrelation` 和 `ReasoningFeatureList` 參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="0fde5-182">5.模型基本操作</span><span class="sxs-lookup"><span data-stu-id="0fde5-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="0fde5-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-183">5.1.</span></span> <span data-ttu-id="0fde5-184">建立模型</span><span class="sxs-lookup"><span data-stu-id="0fde5-184">Create Model</span></span>
<span data-ttu-id="0fde5-185">建立「建立模型」要求。</span><span class="sxs-lookup"><span data-stu-id="0fde5-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="0fde5-186">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-186">HTTP Method</span></span> | <span data-ttu-id="0fde5-187">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-188">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-189">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-190">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-190">Parameter Name</span></span> | <span data-ttu-id="0fde5-191">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-192">modelName</span><span class="sxs-lookup"><span data-stu-id="0fde5-192">modelName</span></span> |<span data-ttu-id="0fde5-193">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0fde5-194">最大長度：20</span><span class="sxs-lookup"><span data-stu-id="0fde5-194">Max length: 20</span></span> |
| <span data-ttu-id="0fde5-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-195">apiVersion</span></span> |<span data-ttu-id="0fde5-196">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-196">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-197">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-197">Request Body</span></span> |<span data-ttu-id="0fde5-198">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-198">NONE</span></span> |

<span data-ttu-id="0fde5-199">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-199">**Response**:</span></span>

<span data-ttu-id="0fde5-200">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="0fde5-201">`feed/entry/content/properties/id` – 包含模型識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="0fde5-202">**注意**：模型識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="0fde5-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="0fde5-203">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="0fde5-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-204">5.2.</span></span> <span data-ttu-id="0fde5-205">取得模型</span><span class="sxs-lookup"><span data-stu-id="0fde5-205">Get Model</span></span>
<span data-ttu-id="0fde5-206">建立一個「取得模型」要求。</span><span class="sxs-lookup"><span data-stu-id="0fde5-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="0fde5-207">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-207">HTTP Method</span></span> | <span data-ttu-id="0fde5-208">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-209">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-210">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-211">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-211">Parameter Name</span></span> | <span data-ttu-id="0fde5-212">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-213">id</span><span class="sxs-lookup"><span data-stu-id="0fde5-213">id</span></span> |<span data-ttu-id="0fde5-214">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="0fde5-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="0fde5-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-215">apiVersion</span></span> |<span data-ttu-id="0fde5-216">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-216">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-217">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-217">Request Body</span></span> |<span data-ttu-id="0fde5-218">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-218">NONE</span></span> |

<span data-ttu-id="0fde5-219">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-219">**Response**:</span></span>

<span data-ttu-id="0fde5-220">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-220">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-221">在下列項目之下，您可以找到模型資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="0fde5-222">`feed/entry/content/properties/Id` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="0fde5-223">`feed/entry/content/properties/Name` - 模型名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="0fde5-224">`feed/entry/content/properties/Date` - 模型建立日期。</span><span class="sxs-lookup"><span data-stu-id="0fde5-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="0fde5-225">`feed/entry/content/properties/Status` - 模型狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="0fde5-226">下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="0fde5-226">One of the following:</span></span>
  * <span data-ttu-id="0fde5-227">Created - 模型已建立且不包含目錄和使用方式。</span><span class="sxs-lookup"><span data-stu-id="0fde5-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="0fde5-228">ReadyForBuild - 模型已建立且包含目錄和使用狀況。</span><span class="sxs-lookup"><span data-stu-id="0fde5-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="0fde5-229">`feed/entry/content/properties/HasActiveBuild` - 表示模型是否已成功建置。</span><span class="sxs-lookup"><span data-stu-id="0fde5-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="0fde5-230">`feed/entry/content/properties/BuildId` - 模型的作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="0fde5-231">`feed/entry/content/properties/Mpr` - 模型的平均值百分位數排名 (MPR - 如需詳細資訊，請參閱 ModelInsight)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="0fde5-232">`feed/entry/content/properties/UserName` - 模型的內部使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="0fde5-233">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="0fde5-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-234">5.3.</span></span>    <span data-ttu-id="0fde5-235">取得所有模型</span><span class="sxs-lookup"><span data-stu-id="0fde5-235">Get All Models</span></span>
<span data-ttu-id="0fde5-236">擷取目前使用者的所有模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="0fde5-237">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-237">HTTP Method</span></span> | <span data-ttu-id="0fde5-238">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-239">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-240">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-241">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-241">Parameter Name</span></span> | <span data-ttu-id="0fde5-242">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-243">apiVersion</span></span> |<span data-ttu-id="0fde5-244">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-244">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-245">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-245">Request Body</span></span> |<span data-ttu-id="0fde5-246">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-246">NONE</span></span> |

<span data-ttu-id="0fde5-247">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-247">**Response**:</span></span>

<span data-ttu-id="0fde5-248">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="0fde5-249">`feed/entry/content/properties/Id` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="0fde5-250">`feed/entry/content/properties/Name` - 模型名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="0fde5-251">`feed/entry/content/properties/Date` - 模型建立日期。</span><span class="sxs-lookup"><span data-stu-id="0fde5-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="0fde5-252">`feed/entry/content/properties/Status` - 模型狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="0fde5-253">下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="0fde5-253">One of the following:</span></span>
  * <span data-ttu-id="0fde5-254">Created - 模型已建立且不包含目錄和使用方式。</span><span class="sxs-lookup"><span data-stu-id="0fde5-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="0fde5-255">ReadyForBuild - 模型已建立且包含目錄和使用狀況。</span><span class="sxs-lookup"><span data-stu-id="0fde5-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="0fde5-256">`feed/entry/content/properties/HasActiveBuild` - 表示模型是否已成功建置。</span><span class="sxs-lookup"><span data-stu-id="0fde5-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="0fde5-257">`feed/entry/content/properties/BuildId` - 模型的作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="0fde5-258">`feed/entry/content/properties/Mpr` - 模型 MPR (如需詳細資訊，請參閱 ModelInsight)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="0fde5-259">`feed/entry/content/properties/UserName` - 模型的內部使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="0fde5-260">`feed/entry/content/properties/UsageFileNames` - 逗號分隔的模型使用狀況檔案清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="0fde5-261">`feed/entry/content/properties/CatalogId` - 模型目錄識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="0fde5-262">`feed/entry/content/properties/Description` - 模型說明。</span><span class="sxs-lookup"><span data-stu-id="0fde5-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="0fde5-263">`feed/entry/content/properties/CatalogFileName` - 模型目錄檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="0fde5-264">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="0fde5-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-265">5.4.</span></span>    <span data-ttu-id="0fde5-266">更新模型</span><span class="sxs-lookup"><span data-stu-id="0fde5-266">Update Model</span></span>
<span data-ttu-id="0fde5-267">您可以更新模型描述或作用中組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-267">You can update the model description or the active build ID.</span></span><br><span data-ttu-id="0fde5-268">
<ins>作用中組建識別碼</ins> - 每個模型的每個組建都有組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="0fde5-269">作用中組建識別碼是每個新模型的第一個成功組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="0fde5-270">一旦您有作用中組建識別碼，而且您執行相同模型的其他組建，您必須是需要將它明確設為預設組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="0fde5-271">當您取用建議時，如果您未指定想要使用的組建識別碼，則會自動使用預設值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="0fde5-272">此機制可讓您在生產環境中有建議模型時建置新模型，並先加以測試，再將其提升至生產環境。</span><span class="sxs-lookup"><span data-stu-id="0fde5-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="0fde5-273">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-273">HTTP Method</span></span> | <span data-ttu-id="0fde5-274">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-275">PUT</span><span class="sxs-lookup"><span data-stu-id="0fde5-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-276">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-277">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-277">Parameter Name</span></span> | <span data-ttu-id="0fde5-278">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-279">id</span><span class="sxs-lookup"><span data-stu-id="0fde5-279">id</span></span> |<span data-ttu-id="0fde5-280">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="0fde5-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="0fde5-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-281">apiVersion</span></span> |<span data-ttu-id="0fde5-282">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-282">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-283">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="0fde5-284">請注意，XML 標籤說明和 ActiveBuildId 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="0fde5-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="0fde5-285">如果您不想設定 Description 或 ActiveBuildId，請移除整個標記。</span><span class="sxs-lookup"><span data-stu-id="0fde5-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="0fde5-286">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-286">**Response**:</span></span>

<span data-ttu-id="0fde5-287">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="0fde5-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="0fde5-288">5.5.</span></span>    <span data-ttu-id="0fde5-289">刪除模型</span><span class="sxs-lookup"><span data-stu-id="0fde5-289">Delete Model</span></span>
<span data-ttu-id="0fde5-290">根據識別碼刪除現有的模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="0fde5-291">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-291">HTTP Method</span></span> | <span data-ttu-id="0fde5-292">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-293">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-294">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-295">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-295">Parameter Name</span></span> | <span data-ttu-id="0fde5-296">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-297">id</span><span class="sxs-lookup"><span data-stu-id="0fde5-297">id</span></span> |<span data-ttu-id="0fde5-298">模型的唯一識別碼 (區分大小寫)</span><span class="sxs-lookup"><span data-stu-id="0fde5-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="0fde5-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-299">apiVersion</span></span> |<span data-ttu-id="0fde5-300">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-300">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-301">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-301">Request Body</span></span> |<span data-ttu-id="0fde5-302">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-302">NONE</span></span> |

<span data-ttu-id="0fde5-303">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-303">**Response**:</span></span>

<span data-ttu-id="0fde5-304">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-304">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-305">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="0fde5-306">6.模型進階操作</span><span class="sxs-lookup"><span data-stu-id="0fde5-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="0fde5-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-307">6.1.</span></span>    <span data-ttu-id="0fde5-308">模型資料深入了解</span><span class="sxs-lookup"><span data-stu-id="0fde5-308">Model Data Insight</span></span>
<span data-ttu-id="0fde5-309">傳回建置此模型時所用之使用狀況資料的相關統計資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="0fde5-310">僅適用於建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="0fde5-311">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-311">HTTP Method</span></span> | <span data-ttu-id="0fde5-312">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-313">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-314">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-315">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-315">Parameter Name</span></span> | <span data-ttu-id="0fde5-316">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-317">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-317">modelId</span></span> |<span data-ttu-id="0fde5-318">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-319">apiVersion</span></span> |<span data-ttu-id="0fde5-320">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-320">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-321">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-321">Request Body</span></span> |<span data-ttu-id="0fde5-322">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-322">NONE</span></span> |

<span data-ttu-id="0fde5-323">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-323">**Response**:</span></span>

<span data-ttu-id="0fde5-324">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-324">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-325">傳回資料做為屬性的集合。</span><span class="sxs-lookup"><span data-stu-id="0fde5-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="0fde5-326">`feed/entry/id/content/properties/key` - 保留屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="0fde5-327">`feed/entry/id/content/properties/value` - 保留屬性值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="0fde5-328">下表描述每個索引鍵表示的值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="0fde5-329">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-329">Key</span></span> | <span data-ttu-id="0fde5-330">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-331">AvgItemLength</span></span> |<span data-ttu-id="0fde5-332">每個項目不同使用者的平均數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="0fde5-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-333">AvgUserLength</span></span> |<span data-ttu-id="0fde5-334">每個使用者不同項目的平均數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="0fde5-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="0fde5-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="0fde5-336">剪除不能模型化的項目之後的項目數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="0fde5-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="0fde5-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="0fde5-338">剪除不能模型化的使用者和項目之後的始用點數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="0fde5-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="0fde5-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="0fde5-340">剪除不能模型化的使用者和項目之後的始用點數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="0fde5-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-341">MaxItemLength</span></span> |<span data-ttu-id="0fde5-342">最受歡迎項目的不同使用者數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="0fde5-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-343">MaxUserLength</span></span> |<span data-ttu-id="0fde5-344">使用者之不同項目的最大數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="0fde5-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-345">MinItemLength</span></span> |<span data-ttu-id="0fde5-346">項目之不同使用者的最大數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="0fde5-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="0fde5-347">MinUserLength</span></span> |<span data-ttu-id="0fde5-348">使用者之不同項目的最小數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="0fde5-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="0fde5-349">RawNumberOfItems</span></span> |<span data-ttu-id="0fde5-350">使用方式檔案中的項目數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="0fde5-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="0fde5-351">RawNumberOfUsers</span></span> |<span data-ttu-id="0fde5-352">任何剪除動作之前的使用點數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="0fde5-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="0fde5-353">RawNumberOfRecords</span></span> |<span data-ttu-id="0fde5-354">任何剪除動作之前的使用點數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="0fde5-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="0fde5-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="0fde5-356">N/A</span><span class="sxs-lookup"><span data-stu-id="0fde5-356">N/A</span></span> |
| <span data-ttu-id="0fde5-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="0fde5-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="0fde5-358">N/A</span><span class="sxs-lookup"><span data-stu-id="0fde5-358">N/A</span></span> |
| <span data-ttu-id="0fde5-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="0fde5-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="0fde5-360">N/A</span><span class="sxs-lookup"><span data-stu-id="0fde5-360">N/A</span></span> |

<span data-ttu-id="0fde5-361">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="0fde5-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-362">6.2.</span></span>    <span data-ttu-id="0fde5-363">模型深入了解</span><span class="sxs-lookup"><span data-stu-id="0fde5-363">Model Insight</span></span>
<span data-ttu-id="0fde5-364">傳回作用中組建或 (如果有) 特定組建上的模型深入了解。</span><span class="sxs-lookup"><span data-stu-id="0fde5-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="0fde5-365">僅適用於建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="0fde5-366">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-366">HTTP Method</span></span> | <span data-ttu-id="0fde5-367">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-368">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-368">GET</span></span> |<span data-ttu-id="0fde5-369">具有作用中組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="0fde5-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-370">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-371">具有特定組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="0fde5-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-372">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-372">Parameter Name</span></span> | <span data-ttu-id="0fde5-373">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-374">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-374">modelId</span></span> |<span data-ttu-id="0fde5-375">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-376">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-376">buildId</span></span> |<span data-ttu-id="0fde5-377">選擇性 – 識別成功組建的編號。</span><span class="sxs-lookup"><span data-stu-id="0fde5-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="0fde5-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-378">apiVersion</span></span> |<span data-ttu-id="0fde5-379">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-379">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-380">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-380">Request Body</span></span> |<span data-ttu-id="0fde5-381">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-381">NONE</span></span> |

<span data-ttu-id="0fde5-382">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-382">**Response**:</span></span>

<span data-ttu-id="0fde5-383">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-383">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-384">傳回資料做為屬性的集合。</span><span class="sxs-lookup"><span data-stu-id="0fde5-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="0fde5-385">下表描述每個索引鍵表示的值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="0fde5-386">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-386">Key</span></span> | <span data-ttu-id="0fde5-387">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="0fde5-388">CatalogCoverage</span></span> |<span data-ttu-id="0fde5-389">目錄的哪個部分可以利用使用模式進行模型化。</span><span class="sxs-lookup"><span data-stu-id="0fde5-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="0fde5-390">其餘的項目都需要以內容為基礎的功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="0fde5-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="0fde5-391">Mpr</span></span> |<span data-ttu-id="0fde5-392">模型的平均值百分位數排名。</span><span class="sxs-lookup"><span data-stu-id="0fde5-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="0fde5-393">越低越好。</span><span class="sxs-lookup"><span data-stu-id="0fde5-393">Lower is better.</span></span> |
| <span data-ttu-id="0fde5-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="0fde5-394">NumberOfDimensions</span></span> |<span data-ttu-id="0fde5-395">矩陣分解演算法所使用的維度數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="0fde5-396">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="0fde5-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-397">6.3.</span></span>    <span data-ttu-id="0fde5-398">取得模型範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-398">Get Model Sample</span></span>
<span data-ttu-id="0fde5-399">取得建議模型的範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="0fde5-400">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-400">HTTP Method</span></span> | <span data-ttu-id="0fde5-401">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-402">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-403">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-404">具有特定組建識別碼：</span><span class="sxs-lookup"><span data-stu-id="0fde5-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-405">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-406">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-406">Parameter Name</span></span> | <span data-ttu-id="0fde5-407">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-408">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-408">modelId</span></span> |<span data-ttu-id="0fde5-409">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-410">apiVersion</span></span> |<span data-ttu-id="0fde5-411">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-411">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-412">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-412">Request Body</span></span> |<span data-ttu-id="0fde5-413">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-413">NONE</span></span> |

<span data-ttu-id="0fde5-414">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-414">**Response**:</span></span>

<span data-ttu-id="0fde5-415">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-415">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-416">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-416">OData XML</span></span>

<span data-ttu-id="0fde5-417">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="0fde5-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="0fde5-418">7.模型商務規則</span><span class="sxs-lookup"><span data-stu-id="0fde5-418">7. Model Business Rules</span></span>
<span data-ttu-id="0fde5-419">以下是支援的規則類型：</span><span class="sxs-lookup"><span data-stu-id="0fde5-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="0fde5-420"><strong>BlockList</strong> -封鎖清單可讓您提供您不想在建議結果中傳回的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="0fde5-421"><strong>FeatureBlockList</strong> - 功能封鎖清單可讓您依據項目功能的值封鎖項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="0fde5-422">*請勿在單一封鎖清單規則中傳送超過 1000 個項目，否則您的呼叫可能會逾時。如果您需要封鎖超過 1000 個項目，可以呼叫幾個封鎖清單。*</span><span class="sxs-lookup"><span data-stu-id="0fde5-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="0fde5-423"><strong>Upsale</strong> - Upsale 可讓您強制在建議結果中傳回項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="0fde5-424"><strong>WhiteList</strong> - 允許清單可讓您只從項目的清單中建議建議項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="0fde5-425"><strong>FeatureWhiteList</strong> - 功能允許清單可讓您只建議具有特定功能值的項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="0fde5-426"><strong>PerSeedBlockList</strong> - PerSeedBlockList 可讓您提供無法做為建議結果傳回的項目清單給每個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="0fde5-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-427">7.1.</span></span>    <span data-ttu-id="0fde5-428">取得模型規則</span><span class="sxs-lookup"><span data-stu-id="0fde5-428">Get Model Rules</span></span>
| <span data-ttu-id="0fde5-429">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-429">HTTP Method</span></span> | <span data-ttu-id="0fde5-430">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-431">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="0fde5-432">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-433">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-433">Parameter Name</span></span> | <span data-ttu-id="0fde5-434">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-435">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-435">modelId</span></span> |<span data-ttu-id="0fde5-436">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-437">apiVersion</span></span> |<span data-ttu-id="0fde5-438">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-438">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-439">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-439">Request Body</span></span> |<span data-ttu-id="0fde5-440">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-440">NONE</span></span> |

<span data-ttu-id="0fde5-441">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-441">**Response**:</span></span>

<span data-ttu-id="0fde5-442">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="0fde5-443">`feed/entry/content/properties/Id` - 此規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="0fde5-444">`feed/entry/content/properties/Type` - 規則的類型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="0fde5-445">`feed/entry/content/properties/Parameter` - 規則參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="0fde5-446">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="0fde5-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-447">7.2.</span></span>    <span data-ttu-id="0fde5-448">新增規則</span><span class="sxs-lookup"><span data-stu-id="0fde5-448">Add Rule</span></span>
| <span data-ttu-id="0fde5-449">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-449">HTTP Method</span></span> | <span data-ttu-id="0fde5-450">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-451">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="0fde5-452">標頭</span><span class="sxs-lookup"><span data-stu-id="0fde5-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="0fde5-453">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-453">Parameter Name</span></span> | <span data-ttu-id="0fde5-454">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-455">apiVersion</span></span> |<span data-ttu-id="0fde5-456">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-456">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-457">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-457">Request Body</span></span> | |

<span data-ttu-id="0fde5-458"><ins>在提供商務規則的項目識別碼時，請務必使用項目的外部識別碼 (您用於類別目錄檔案的同一識別碼)</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br><span data-ttu-id="0fde5-459">
<ins>新增 BlockList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-459">
<ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="0fde5-460"><ins>
<ins>新增 FeatureBlockList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="0fde5-461"><ins> 新增 Upsale 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="0fde5-462">
<ins>新增 WhiteList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-462">
<ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="0fde5-463"><ins>
<ins>新增 FeatureWhiteList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="0fde5-464"><ins> 新增 PerSeedBlockList 規則：</ins></span><span class="sxs-lookup"><span data-stu-id="0fde5-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="0fde5-465">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-465">**Response**:</span></span>

<span data-ttu-id="0fde5-466">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-466">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-467">API 會傳回新建立的規則及其詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="0fde5-468">規則屬性可從下列路徑擷取：</span><span class="sxs-lookup"><span data-stu-id="0fde5-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="0fde5-469">`feed/entry/content/properties/Id` - 此規則的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="0fde5-470">`feed/entry/content/properties/Type` - 規則的類型：BlockList 或 Upsale。</span><span class="sxs-lookup"><span data-stu-id="0fde5-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="0fde5-471">`feed/entry/content/properties/Parameter` - 規則參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="0fde5-472">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="0fde5-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-473">7.3.</span></span>    <span data-ttu-id="0fde5-474">刪除規則</span><span class="sxs-lookup"><span data-stu-id="0fde5-474">Delete Rule</span></span>
| <span data-ttu-id="0fde5-475">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-475">HTTP Method</span></span> | <span data-ttu-id="0fde5-476">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-477">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-478">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-479">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-479">Parameter Name</span></span> | <span data-ttu-id="0fde5-480">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-481">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-481">modelId</span></span> |<span data-ttu-id="0fde5-482">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-483">filterId</span><span class="sxs-lookup"><span data-stu-id="0fde5-483">filterId</span></span> |<span data-ttu-id="0fde5-484">篩選器的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="0fde5-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-485">apiVersion</span></span> |<span data-ttu-id="0fde5-486">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-486">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-487">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-487">Request Body</span></span> |<span data-ttu-id="0fde5-488">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-488">NONE</span></span> |

<span data-ttu-id="0fde5-489">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-489">**Response**:</span></span>

<span data-ttu-id="0fde5-490">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="0fde5-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-491">7.4.</span></span>    <span data-ttu-id="0fde5-492">刪除所有規則</span><span class="sxs-lookup"><span data-stu-id="0fde5-492">Delete All Rules</span></span>
| <span data-ttu-id="0fde5-493">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-493">HTTP Method</span></span> | <span data-ttu-id="0fde5-494">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-495">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-496">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-497">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-497">Parameter Name</span></span> | <span data-ttu-id="0fde5-498">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-499">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-499">modelId</span></span> |<span data-ttu-id="0fde5-500">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-501">apiVersion</span></span> |<span data-ttu-id="0fde5-502">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-502">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-503">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-503">Request Body</span></span> |<span data-ttu-id="0fde5-504">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-504">NONE</span></span> |

<span data-ttu-id="0fde5-505">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-505">**Response**:</span></span>

<span data-ttu-id="0fde5-506">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="0fde5-507">8.目錄</span><span class="sxs-lookup"><span data-stu-id="0fde5-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="0fde5-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-508">8.1.</span></span>    <span data-ttu-id="0fde5-509">匯入目錄資料</span><span class="sxs-lookup"><span data-stu-id="0fde5-509">Import Catalog Data</span></span>
<span data-ttu-id="0fde5-510">如果您將數個目錄檔案上傳至具有多個呼叫的相同模型，我們只會插入新的目錄項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="0fde5-511">現有的項目會保留原始值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="0fde5-512">您無法使用這個方法更新目錄資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="0fde5-513">目錄資料應該遵循下列格式：</span><span class="sxs-lookup"><span data-stu-id="0fde5-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="0fde5-514">沒有功能 - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="0fde5-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="0fde5-515">具有功能 - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="0fde5-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="0fde5-516">注意：檔案大小上限為 200 MB。</span><span class="sxs-lookup"><span data-stu-id="0fde5-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="0fde5-517">** 格式詳細資料 **</span><span class="sxs-lookup"><span data-stu-id="0fde5-517">** Format details **</span></span>

| <span data-ttu-id="0fde5-518">名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-518">Name</span></span> | <span data-ttu-id="0fde5-519">強制</span><span class="sxs-lookup"><span data-stu-id="0fde5-519">Mandatory</span></span> | <span data-ttu-id="0fde5-520">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-520">Type</span></span> | <span data-ttu-id="0fde5-521">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0fde5-522">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-522">Item Id</span></span> |<span data-ttu-id="0fde5-523">是</span><span class="sxs-lookup"><span data-stu-id="0fde5-523">Yes</span></span> |<span data-ttu-id="0fde5-524">[A-z]、[a-z]、[0-9]、[_] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="0fde5-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="0fde5-525">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-525">Max length: 50</span></span> |<span data-ttu-id="0fde5-526">項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="0fde5-527">項目名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-527">Item Name</span></span> |<span data-ttu-id="0fde5-528">是</span><span class="sxs-lookup"><span data-stu-id="0fde5-528">Yes</span></span> |<span data-ttu-id="0fde5-529">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="0fde5-530">最大長度：255</span><span class="sxs-lookup"><span data-stu-id="0fde5-530">Max length: 255</span></span> |<span data-ttu-id="0fde5-531">項目名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-531">Item name.</span></span> |
| <span data-ttu-id="0fde5-532">項目類別</span><span class="sxs-lookup"><span data-stu-id="0fde5-532">Item Category</span></span> |<span data-ttu-id="0fde5-533">是</span><span class="sxs-lookup"><span data-stu-id="0fde5-533">Yes</span></span> |<span data-ttu-id="0fde5-534">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="0fde5-535">最大長度：255</span><span class="sxs-lookup"><span data-stu-id="0fde5-535">Max length: 255</span></span> |<span data-ttu-id="0fde5-536">此項目所屬類別 (例如烹飪書籍、劇本...) 可以是空的。</span><span class="sxs-lookup"><span data-stu-id="0fde5-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="0fde5-537">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-537">Description</span></span> |<span data-ttu-id="0fde5-538">否，除非顯示功能 (但可能是空的)</span><span class="sxs-lookup"><span data-stu-id="0fde5-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="0fde5-539">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="0fde5-540">最大長度：4000</span><span class="sxs-lookup"><span data-stu-id="0fde5-540">Max length: 4000</span></span> |<span data-ttu-id="0fde5-541">此項目的說明。</span><span class="sxs-lookup"><span data-stu-id="0fde5-541">Description of this item.</span></span> |
| <span data-ttu-id="0fde5-542">功能清單</span><span class="sxs-lookup"><span data-stu-id="0fde5-542">Features list</span></span> |<span data-ttu-id="0fde5-543">否</span><span class="sxs-lookup"><span data-stu-id="0fde5-543">No</span></span> |<span data-ttu-id="0fde5-544">任何英數字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="0fde5-545">最大長度：4000；功能數目上限：20</span><span class="sxs-lookup"><span data-stu-id="0fde5-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="0fde5-546">以逗號分隔的「功能名稱=功能值」清單，可用來增強模型建議；請參閱 [進階主題](#2-advanced-topics) 一節。</span><span class="sxs-lookup"><span data-stu-id="0fde5-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="0fde5-547">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-547">HTTP Method</span></span> | <span data-ttu-id="0fde5-548">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-549">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-550">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="0fde5-551">標頭</span><span class="sxs-lookup"><span data-stu-id="0fde5-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="0fde5-552">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-552">Parameter Name</span></span> | <span data-ttu-id="0fde5-553">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-554">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-554">modelId</span></span> |<span data-ttu-id="0fde5-555">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-556">檔名</span><span class="sxs-lookup"><span data-stu-id="0fde5-556">filename</span></span> |<span data-ttu-id="0fde5-557">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="0fde5-558">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0fde5-559">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-559">Max length: 50</span></span> |
| <span data-ttu-id="0fde5-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-560">apiVersion</span></span> |<span data-ttu-id="0fde5-561">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-561">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-562">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-562">Request Body</span></span> |<span data-ttu-id="0fde5-563">範例 (包含功能)：</span><span class="sxs-lookup"><span data-stu-id="0fde5-563">Example (with features):</span></span><br/><span data-ttu-id="0fde5-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="0fde5-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="0fde5-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="0fde5-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="0fde5-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="0fde5-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="0fde5-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="0fde5-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="0fde5-568">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-568">**Response**:</span></span>

<span data-ttu-id="0fde5-569">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-569">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-570">API 傳回匯入的報告。</span><span class="sxs-lookup"><span data-stu-id="0fde5-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="0fde5-571">`feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="0fde5-572">`feed\entry\content\properties\ErrorCount` - 因錯誤而未插入的行數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="0fde5-573">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="0fde5-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-574">8.2.</span></span>    <span data-ttu-id="0fde5-575">取得目錄</span><span class="sxs-lookup"><span data-stu-id="0fde5-575">Get Catalog</span></span>
<span data-ttu-id="0fde5-576">擷取所有目錄項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="0fde5-577">目錄會一次擷取一個頁面。</span><span class="sxs-lookup"><span data-stu-id="0fde5-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="0fde5-578">如果想要取得特定索引處的項目，您可以使用 $skip odata 參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="0fde5-579">例如，如果想要取得在位置 100 開始的項目，請將參數 $skip=100 加入至要求。</span><span class="sxs-lookup"><span data-stu-id="0fde5-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="0fde5-580">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-580">HTTP Method</span></span> | <span data-ttu-id="0fde5-581">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-582">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-583">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-584">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-584">Parameter Name</span></span> | <span data-ttu-id="0fde5-585">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-586">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-586">modelId</span></span> |<span data-ttu-id="0fde5-587">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-588">apiVersion</span></span> |<span data-ttu-id="0fde5-589">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-589">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-590">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-590">Request Body</span></span> |<span data-ttu-id="0fde5-591">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-591">NONE</span></span> |

<span data-ttu-id="0fde5-592">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-592">**Response**:</span></span>

<span data-ttu-id="0fde5-593">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-593">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-594">回應會包含每個目錄項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="0fde5-595">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-595">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-596">`feed/entry/content/properties/ExternalId` - 目錄項目外部識別碼，由客戶提供。</span><span class="sxs-lookup"><span data-stu-id="0fde5-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="0fde5-597">`feed/entry/content/properties/InternalId` - 目錄項目內部識別碼，由 Azure Machine Learning 建議產生。</span><span class="sxs-lookup"><span data-stu-id="0fde5-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="0fde5-598">`feed/entry/content/properties/Name` - 目錄項目名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="0fde5-599">`feed/entry/content/properties/Category` - 目錄項目類別。</span><span class="sxs-lookup"><span data-stu-id="0fde5-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="0fde5-600">`feed/entry/content/properties/Description` - 目錄項目說明。</span><span class="sxs-lookup"><span data-stu-id="0fde5-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="0fde5-601">`feed/entry/content/properties/Metadata` - 目錄項目中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="0fde5-602">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="0fde5-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-603">8.3.</span></span>    <span data-ttu-id="0fde5-604">依語彙基元取得目錄項目</span><span class="sxs-lookup"><span data-stu-id="0fde5-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="0fde5-605">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-605">HTTP Method</span></span> | <span data-ttu-id="0fde5-606">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-607">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-608">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-609">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-609">Parameter Name</span></span> | <span data-ttu-id="0fde5-610">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-611">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-611">modelId</span></span> |<span data-ttu-id="0fde5-612">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-613">token</span><span class="sxs-lookup"><span data-stu-id="0fde5-613">token</span></span> |<span data-ttu-id="0fde5-614">目錄項目名稱的 token。</span><span class="sxs-lookup"><span data-stu-id="0fde5-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="0fde5-615">應該至少包含 3 個字元。</span><span class="sxs-lookup"><span data-stu-id="0fde5-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="0fde5-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-616">apiVersion</span></span> |<span data-ttu-id="0fde5-617">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-617">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-618">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-618">Request Body</span></span> |<span data-ttu-id="0fde5-619">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-619">NONE</span></span> |

<span data-ttu-id="0fde5-620">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-620">**Response**:</span></span>

<span data-ttu-id="0fde5-621">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-621">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-622">回應會包含每個目錄項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="0fde5-623">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-623">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-624">`feed/entry/content/properties/InternalId` - 目錄項目內部識別碼，由 Azure Machine Learning 建議產生。</span><span class="sxs-lookup"><span data-stu-id="0fde5-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="0fde5-625">`feed/entry/content/properties/Name` - 目錄項目名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="0fde5-626">`feed/entry/content/properties/Rating` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="0fde5-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="0fde5-627">`feed/entry/content/properties/Reasoning` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="0fde5-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="0fde5-628">`feed/entry/content/properties/Metadata` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="0fde5-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="0fde5-629">`feed/entry/content/properties/FormattedRating` - (保留供日後使用)</span><span class="sxs-lookup"><span data-stu-id="0fde5-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="0fde5-630">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="0fde5-631">9.使用狀況資料</span><span class="sxs-lookup"><span data-stu-id="0fde5-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="0fde5-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-632">9.1.</span></span>    <span data-ttu-id="0fde5-633">匯入使用資料</span><span class="sxs-lookup"><span data-stu-id="0fde5-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="0fde5-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-634">9.1.1.</span></span> <span data-ttu-id="0fde5-635">上傳檔案</span><span class="sxs-lookup"><span data-stu-id="0fde5-635">Uploading File</span></span>
<span data-ttu-id="0fde5-636">本節試範如何使用檔案上傳使用資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="0fde5-637">您可以利用使用資料呼叫此 API 數次。</span><span class="sxs-lookup"><span data-stu-id="0fde5-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="0fde5-638">將會針對所有呼叫儲存所有使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="0fde5-639">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-639">HTTP Method</span></span> | <span data-ttu-id="0fde5-640">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-641">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-642">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-643">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-643">Parameter Name</span></span> | <span data-ttu-id="0fde5-644">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-645">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-645">modelId</span></span> |<span data-ttu-id="0fde5-646">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-647">檔名</span><span class="sxs-lookup"><span data-stu-id="0fde5-647">filename</span></span> |<span data-ttu-id="0fde5-648">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="0fde5-649">只允許使用字母 (A-Z、a-z)、數字 (0-9)、連字號 (-) 及底線 (_)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="0fde5-650">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-650">Max length: 50</span></span> |
| <span data-ttu-id="0fde5-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-651">apiVersion</span></span> |<span data-ttu-id="0fde5-652">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-652">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-653">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-653">Request Body</span></span> |<span data-ttu-id="0fde5-654">使用狀況資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-654">Usage data.</span></span> <span data-ttu-id="0fde5-655">格式：</span><span class="sxs-lookup"><span data-stu-id="0fde5-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="0fde5-656">名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-656">Name</span></span></th><th><span data-ttu-id="0fde5-657">強制</span><span class="sxs-lookup"><span data-stu-id="0fde5-657">Mandatory</span></span></th><th><span data-ttu-id="0fde5-658">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-658">Type</span></span></th><th><span data-ttu-id="0fde5-659">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-659">Description</span></span></th></tr><tr><td><span data-ttu-id="0fde5-660">使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-660">User Id</span></span></td><td><span data-ttu-id="0fde5-661">yes</span><span class="sxs-lookup"><span data-stu-id="0fde5-661">Yes</span></span></td><td><span data-ttu-id="0fde5-662">[A-z]、[a-z]、[0-9]、[_] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="0fde5-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="0fde5-663">最大長度：255</span><span class="sxs-lookup"><span data-stu-id="0fde5-663">Max length: 255</span></span> </td><td><span data-ttu-id="0fde5-664">使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="0fde5-665">項目識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-665">Item Id</span></span></td><td><span data-ttu-id="0fde5-666">是</span><span class="sxs-lookup"><span data-stu-id="0fde5-666">Yes</span></span></td><td><span data-ttu-id="0fde5-667">[A-z]、[a-z]、[0-9]、[&#95;] &#40;底線&#41;、[-] &#40;虛線&#41;</span><span class="sxs-lookup"><span data-stu-id="0fde5-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="0fde5-668">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-668">Max length: 50</span></span></td><td><span data-ttu-id="0fde5-669">項目的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="0fde5-670">時間</span><span class="sxs-lookup"><span data-stu-id="0fde5-670">Time</span></span></td><td><span data-ttu-id="0fde5-671">否</span><span class="sxs-lookup"><span data-stu-id="0fde5-671">No</span></span></td><td><span data-ttu-id="0fde5-672">日期格式：YYYY/MM/DDTHH:MM:SS (例如 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="0fde5-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="0fde5-673">資料的時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="0fde5-674">事件</span><span class="sxs-lookup"><span data-stu-id="0fde5-674">Event</span></span></td><td><span data-ttu-id="0fde5-675">否；如果提供，必須也提供日期</span><span class="sxs-lookup"><span data-stu-id="0fde5-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="0fde5-676">下列其中之一：</span><span class="sxs-lookup"><span data-stu-id="0fde5-676">One of the following:</span></span><br><span data-ttu-id="0fde5-677">• Click</span><span class="sxs-lookup"><span data-stu-id="0fde5-677">• Click</span></span><br><span data-ttu-id="0fde5-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="0fde5-678">• RecommendationClick</span></span><br><span data-ttu-id="0fde5-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="0fde5-679">•    AddShopCart</span></span><br><span data-ttu-id="0fde5-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="0fde5-680">• RemoveShopCart</span></span><br><span data-ttu-id="0fde5-681">• 購買</span><span class="sxs-lookup"><span data-stu-id="0fde5-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="0fde5-682">檔案大小上限：200MB</span><span class="sxs-lookup"><span data-stu-id="0fde5-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="0fde5-683">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="0fde5-684">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-684">**Response**:</span></span>

<span data-ttu-id="0fde5-685">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="0fde5-686">`Feed\entry\content\properties\LineCount` - 已接受的行數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="0fde5-687">`Feed\entry\content\properties\ErrorCount` - 因錯誤而未插入的行數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="0fde5-688">`Feed\entry\content\properties\FileId` - 檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="0fde5-689">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="0fde5-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-690">9.1.2.</span></span> <span data-ttu-id="0fde5-691">使用資料擷取</span><span class="sxs-lookup"><span data-stu-id="0fde5-691">Using Data Acquisition</span></span>
<span data-ttu-id="0fde5-692">本節示範如何將事件即時傳送到 Azure Machine Learning 建議 (通常是從您的網站)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="0fde5-693">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-693">HTTP Method</span></span> | <span data-ttu-id="0fde5-694">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-695">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="0fde5-696">標頭</span><span class="sxs-lookup"><span data-stu-id="0fde5-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="0fde5-697">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-697">Parameter Name</span></span> | <span data-ttu-id="0fde5-698">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-699">apiVersion</span></span> |<span data-ttu-id="0fde5-700">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-700">1.0</span></span> |
| <span data-ttu-id="0fde5-701">Request body</span><span class="sxs-lookup"><span data-stu-id="0fde5-701">Request body</span></span> |<span data-ttu-id="0fde5-702">您想要傳送的每個事件的事件資料項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="0fde5-703">您應該為相同的使用者或瀏覽器工作階段在 SessionId 欄位中傳送相同的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="0fde5-704">(請參閱下面的事件本文範例。)</span><span class="sxs-lookup"><span data-stu-id="0fde5-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="0fde5-705">事件 'Click' 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="0fde5-706">事件 'RecommendationClick' 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="0fde5-707">事件 'AddShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="0fde5-708">事件 'RemoveShopCart' 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="0fde5-709">事件 'Purchase' 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="0fde5-710">傳送 2 個事件 ('Click' 和 'AddShopCart') 的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="0fde5-711">**回應**：HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="0fde5-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-712">9.2.</span></span>    <span data-ttu-id="0fde5-713">列出模型使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="0fde5-713">List Model Usage Files</span></span>
<span data-ttu-id="0fde5-714">擷取所有模型使用方式檔案的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="0fde5-715">使用方式檔案會一次擷取一個頁面。</span><span class="sxs-lookup"><span data-stu-id="0fde5-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="0fde5-716">每個頁面包含 100 個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-716">Each page containes 100 items.</span></span> <span data-ttu-id="0fde5-717">如果想要取得特定索引處的項目，您可以使用 $skip odata 參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="0fde5-718">例如，如果想要取得在位置 100 開始的項目，請將參數 $skip=100 加入至要求。</span><span class="sxs-lookup"><span data-stu-id="0fde5-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="0fde5-719">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-719">HTTP Method</span></span> | <span data-ttu-id="0fde5-720">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-721">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-722">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-723">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-723">Parameter Name</span></span> | <span data-ttu-id="0fde5-724">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-725">forModelId</span></span> |<span data-ttu-id="0fde5-726">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-727">apiVersion</span></span> |<span data-ttu-id="0fde5-728">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-728">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-729">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-729">Request Body</span></span> |<span data-ttu-id="0fde5-730">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-730">NONE</span></span> |

<span data-ttu-id="0fde5-731">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-731">**Response**:</span></span>

<span data-ttu-id="0fde5-732">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-732">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-733">回應會包含每個使用方式檔案的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="0fde5-734">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-734">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-735">`feed\entry\content\properties\Id` - 使用狀況檔案識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="0fde5-736">`feed\entry\content\properties\Length` - 使用狀況檔案長度，以 MB 為單位。</span><span class="sxs-lookup"><span data-stu-id="0fde5-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="0fde5-737">`feed\entry\content\properties\DateModified` - 使用狀況檔案建立日期。</span><span class="sxs-lookup"><span data-stu-id="0fde5-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="0fde5-738">`feed\entry\content\properties\UseInModel` - 使用狀況檔案是否在模型中使用。</span><span class="sxs-lookup"><span data-stu-id="0fde5-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="0fde5-739">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="0fde5-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-740">9.3.</span></span>    <span data-ttu-id="0fde5-741">取得使用狀況統計資料</span><span class="sxs-lookup"><span data-stu-id="0fde5-741">Get Usage Statistics</span></span>
<span data-ttu-id="0fde5-742">取得使用狀況統計資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-742">Gets usage statistics.</span></span>

| <span data-ttu-id="0fde5-743">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-743">HTTP Method</span></span> | <span data-ttu-id="0fde5-744">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-745">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-746">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-747">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-747">Parameter Name</span></span> | <span data-ttu-id="0fde5-748">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-749">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-749">modelId</span></span> |<span data-ttu-id="0fde5-750">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-751">startDate</span><span class="sxs-lookup"><span data-stu-id="0fde5-751">startDate</span></span> |<span data-ttu-id="0fde5-752">開始日期。</span><span class="sxs-lookup"><span data-stu-id="0fde5-752">Start date.</span></span> <span data-ttu-id="0fde5-753">格式：yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="0fde5-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="0fde5-754">endDate</span><span class="sxs-lookup"><span data-stu-id="0fde5-754">endDate</span></span> |<span data-ttu-id="0fde5-755">結束日期。</span><span class="sxs-lookup"><span data-stu-id="0fde5-755">End date.</span></span> <span data-ttu-id="0fde5-756">格式：yyyy/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="0fde5-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="0fde5-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="0fde5-757">eventTypes</span></span> |<span data-ttu-id="0fde5-758">以逗號分隔的事件類型字串或是 null，可取得所有事件</span><span class="sxs-lookup"><span data-stu-id="0fde5-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="0fde5-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-759">apiVersion</span></span> |<span data-ttu-id="0fde5-760">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-760">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-761">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-761">Request Body</span></span> |<span data-ttu-id="0fde5-762">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-762">NONE</span></span> |

<span data-ttu-id="0fde5-763">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-763">**Response**:</span></span>

<span data-ttu-id="0fde5-764">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-764">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-765">索引鍵/值項目的集合。</span><span class="sxs-lookup"><span data-stu-id="0fde5-765">A collection of key/value elements.</span></span> <span data-ttu-id="0fde5-766">每個集合都包含以小時分組之特定事件類型的事件總和。</span><span class="sxs-lookup"><span data-stu-id="0fde5-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="0fde5-767">`feed\entry[i]\content\properties\Key` - 包含時間 (以小時分組) 和事件類型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="0fde5-768">`feed\entry[i]\content\properties\Value` - 事件總數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="0fde5-769">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="0fde5-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-770">9.4.</span></span>    <span data-ttu-id="0fde5-771">取得使用方式檔案範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-771">Get Usage File Sample</span></span>
<span data-ttu-id="0fde5-772">擷取前 2KB 的使用方式檔案內容。</span><span class="sxs-lookup"><span data-stu-id="0fde5-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="0fde5-773">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-773">HTTP Method</span></span> | <span data-ttu-id="0fde5-774">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-775">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-776">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-777">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-777">Parameter Name</span></span> | <span data-ttu-id="0fde5-778">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-779">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-779">modelId</span></span> |<span data-ttu-id="0fde5-780">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-781">fileId</span><span class="sxs-lookup"><span data-stu-id="0fde5-781">fileId</span></span> |<span data-ttu-id="0fde5-782">模型使用方式檔案的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="0fde5-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-783">apiVersion</span></span> |<span data-ttu-id="0fde5-784">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-784">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-785">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-785">Request Body</span></span> |<span data-ttu-id="0fde5-786">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-786">NONE</span></span> |

<span data-ttu-id="0fde5-787">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-787">**Response**:</span></span>

<span data-ttu-id="0fde5-788">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-788">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-789">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="0fde5-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="0fde5-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="0fde5-790">9.5.</span></span>    <span data-ttu-id="0fde5-791">取得模型使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="0fde5-791">Get Model Usage File</span></span>
<span data-ttu-id="0fde5-792">擷取使用方式檔案的完整內容。</span><span class="sxs-lookup"><span data-stu-id="0fde5-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="0fde5-793">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-793">HTTP Method</span></span> | <span data-ttu-id="0fde5-794">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-795">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-796">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-797">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-797">Parameter Name</span></span> | <span data-ttu-id="0fde5-798">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-799">mid</span><span class="sxs-lookup"><span data-stu-id="0fde5-799">mid</span></span> |<span data-ttu-id="0fde5-800">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-801">fid</span><span class="sxs-lookup"><span data-stu-id="0fde5-801">fid</span></span> |<span data-ttu-id="0fde5-802">模型使用方式檔案的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="0fde5-803">下載</span><span class="sxs-lookup"><span data-stu-id="0fde5-803">download</span></span> |<span data-ttu-id="0fde5-804">1</span><span class="sxs-lookup"><span data-stu-id="0fde5-804">1</span></span> |
| <span data-ttu-id="0fde5-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-805">apiVersion</span></span> |<span data-ttu-id="0fde5-806">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-806">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-807">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-807">Request Body</span></span> |<span data-ttu-id="0fde5-808">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-808">NONE</span></span> |

<span data-ttu-id="0fde5-809">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-809">**Response**:</span></span>

<span data-ttu-id="0fde5-810">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-810">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-811">以原始文字格式傳回的回應：</span><span class="sxs-lookup"><span data-stu-id="0fde5-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="0fde5-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="0fde5-812">9.6.</span></span>    <span data-ttu-id="0fde5-813">刪除使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="0fde5-813">Delete Usage File</span></span>
<span data-ttu-id="0fde5-814">刪除指定的模型使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="0fde5-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="0fde5-815">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-815">HTTP Method</span></span> | <span data-ttu-id="0fde5-816">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-817">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-818">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-819">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-819">Parameter Name</span></span> | <span data-ttu-id="0fde5-820">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-821">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-821">modelId</span></span> |<span data-ttu-id="0fde5-822">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-823">fileId</span><span class="sxs-lookup"><span data-stu-id="0fde5-823">fileId</span></span> |<span data-ttu-id="0fde5-824">要刪除之檔案的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="0fde5-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-825">apiVersion</span></span> |<span data-ttu-id="0fde5-826">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-826">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-827">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-827">Request Body</span></span> |<span data-ttu-id="0fde5-828">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-828">NONE</span></span> |

<span data-ttu-id="0fde5-829">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-829">**Response**:</span></span>

<span data-ttu-id="0fde5-830">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="0fde5-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="0fde5-831">9.7.</span></span>    <span data-ttu-id="0fde5-832">刪除所有使用方式檔案</span><span class="sxs-lookup"><span data-stu-id="0fde5-832">Delete All Usage Files</span></span>
<span data-ttu-id="0fde5-833">刪除所有模型使用方式檔案。</span><span class="sxs-lookup"><span data-stu-id="0fde5-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="0fde5-834">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-834">HTTP Method</span></span> | <span data-ttu-id="0fde5-835">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-836">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-837">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-838">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-838">Parameter Name</span></span> | <span data-ttu-id="0fde5-839">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-840">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-840">modelId</span></span> |<span data-ttu-id="0fde5-841">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-842">apiVersion</span></span> |<span data-ttu-id="0fde5-843">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-843">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-844">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-844">Request Body</span></span> |<span data-ttu-id="0fde5-845">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-845">NONE</span></span> |

<span data-ttu-id="0fde5-846">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-846">**Response**:</span></span>

<span data-ttu-id="0fde5-847">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="0fde5-848">10.特性</span><span class="sxs-lookup"><span data-stu-id="0fde5-848">10. Features</span></span>
<span data-ttu-id="0fde5-849">本節示範如何擷取功能資訊，例如匯入的功能和其值、其排名，以及此排名的配置時機。</span><span class="sxs-lookup"><span data-stu-id="0fde5-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="0fde5-850">匯入功能做為目錄資料的一部分，然後在排名組建完成時建立和其排名的關聯。</span><span class="sxs-lookup"><span data-stu-id="0fde5-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="0fde5-851">功能排名可根據使用狀況資料和項目類型而變更。</span><span class="sxs-lookup"><span data-stu-id="0fde5-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="0fde5-852">但是對於一致的使用量/項目，排名只能有小幅的起伏。</span><span class="sxs-lookup"><span data-stu-id="0fde5-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="0fde5-853">功能的排名為非負數的數字。</span><span class="sxs-lookup"><span data-stu-id="0fde5-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="0fde5-854">編號 0 表示未排名功能 (如果您在第一個排名組建完成之前叫用這個 API，就會發生這個情形)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="0fde5-855">配置排名的日期稱為分數有效時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="0fde5-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-856">10.1.</span></span> <span data-ttu-id="0fde5-857">取得功能資訊 (適用於上一個排名組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="0fde5-858">擷取最後一次成功排名組建的功能資訊，包括排名。</span><span class="sxs-lookup"><span data-stu-id="0fde5-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="0fde5-859">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-859">HTTP Method</span></span> | <span data-ttu-id="0fde5-860">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-861">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-862">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-863">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-863">Parameter Name</span></span> | <span data-ttu-id="0fde5-864">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-865">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-865">modelId</span></span> |<span data-ttu-id="0fde5-866">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="0fde5-867">samplingSize</span></span> |<span data-ttu-id="0fde5-868">每個功能要包含的值數目是根據出現在目錄中的資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="0fde5-869">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="0fde5-869">Possible values are:</span></span><br> <span data-ttu-id="0fde5-870">-1 - 所有範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-870">-1 - All samples.</span></span> <br><span data-ttu-id="0fde5-871">0 - 沒有取樣。</span><span class="sxs-lookup"><span data-stu-id="0fde5-871">0 - No sampling.</span></span> <br><span data-ttu-id="0fde5-872">N - 傳回每個功能名稱的 N 範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="0fde5-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-873">apiVersion</span></span> |<span data-ttu-id="0fde5-874">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-874">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-875">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-875">Request Body</span></span> |<span data-ttu-id="0fde5-876">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-876">NONE</span></span> |

<span data-ttu-id="0fde5-877">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-877">**Response**:</span></span>

<span data-ttu-id="0fde5-878">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-878">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-879">回應包含功能資訊項目的清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="0fde5-880">每個項目包含：</span><span class="sxs-lookup"><span data-stu-id="0fde5-880">Each entry contains:</span></span>

* <span data-ttu-id="0fde5-881">`feed/entry/content/m:properties/d:Name` - 功能名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="0fde5-882">`feed/entry/content/m:properties/d:RankUpdateDate` - 配置排名至此功能的日期，又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="0fde5-883">分數有效時間功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-883">score freshness feature.</span></span> <span data-ttu-id="0fde5-884">歷程記錄日期 ('0001-01-01T00:00:00') 表示未執行排名組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="0fde5-885">`feed/entry/content/m:properties/d:Rank` - 功能排名 (float)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="0fde5-886">排名 2.0 以上會被視為良好的功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="0fde5-887">`feed/entry/content/m:properties/d:SampleValues` - 逗號分隔的值清單高達要求的取樣大小。</span><span class="sxs-lookup"><span data-stu-id="0fde5-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="0fde5-888">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="0fde5-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-889">10.2.</span></span> <span data-ttu-id="0fde5-890">取得功能資訊 (適用於特定排名組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="0fde5-891">擷取功能資訊，包括特定排名組建的排名。</span><span class="sxs-lookup"><span data-stu-id="0fde5-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="0fde5-892">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-892">HTTP Method</span></span> | <span data-ttu-id="0fde5-893">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-894">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-895">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-896">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-896">Parameter Name</span></span> | <span data-ttu-id="0fde5-897">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-898">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-898">modelId</span></span> |<span data-ttu-id="0fde5-899">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="0fde5-900">samplingSize</span></span> |<span data-ttu-id="0fde5-901">每個功能要包含的值數目是根據出現在目錄中的資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="0fde5-902">可能的值包括：</span><span class="sxs-lookup"><span data-stu-id="0fde5-902">Possible values are:</span></span><br> <span data-ttu-id="0fde5-903">-1 - 所有範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-903">-1 - All samples.</span></span> <br><span data-ttu-id="0fde5-904">0 - 沒有取樣。</span><span class="sxs-lookup"><span data-stu-id="0fde5-904">0 - No sampling.</span></span> <br><span data-ttu-id="0fde5-905">N - 傳回每個功能名稱的 N 範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="0fde5-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-906">rankBuildId</span></span> |<span data-ttu-id="0fde5-907">排名組建的唯一識別碼或代表上一個排名組建的 -1</span><span class="sxs-lookup"><span data-stu-id="0fde5-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="0fde5-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-908">apiVersion</span></span> |<span data-ttu-id="0fde5-909">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-909">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-910">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-910">Request Body</span></span> |<span data-ttu-id="0fde5-911">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-911">NONE</span></span> |

<span data-ttu-id="0fde5-912">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-912">**Response**:</span></span>

<span data-ttu-id="0fde5-913">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-913">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-914">回應包含功能資訊項目的清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="0fde5-915">每個項目包含：</span><span class="sxs-lookup"><span data-stu-id="0fde5-915">Each entry contains:</span></span>

* <span data-ttu-id="0fde5-916">`feed/entry/content/m:properties/d:Name` - 功能名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="0fde5-917">`feed/entry/content/m:properties/d:RankUpdateDate` - 配置排名至此功能的日期，又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="0fde5-918">分數有效時間功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-918">score freshness feature.</span></span> <span data-ttu-id="0fde5-919">歷程記錄日期 ('0001-01-01T00:00:00') 表示未執行排名組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="0fde5-920">`feed/entry/content/m:properties/d:Rank` - 功能排名 (float)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="0fde5-921">排名 2.0 以上會被視為良好的功能。</span><span class="sxs-lookup"><span data-stu-id="0fde5-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="0fde5-922">`feed/entry/content/m:properties/d:SampleValues` - 逗號分隔的值清單高達要求的取樣大小。</span><span class="sxs-lookup"><span data-stu-id="0fde5-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="0fde5-923">OData</span><span class="sxs-lookup"><span data-stu-id="0fde5-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="0fde5-924">11.建置</span><span class="sxs-lookup"><span data-stu-id="0fde5-924">11. Build</span></span>
  <span data-ttu-id="0fde5-925">本節說明和組建相關的不同 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="0fde5-926">有 3 個類型的組建：建議組建、排名組建和 FBT (通常會一起購買) 組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="0fde5-927">建議組建的用途是產生用於預測的建議模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="0fde5-928">這種組建類型的預測可分為兩種類別：</span><span class="sxs-lookup"><span data-stu-id="0fde5-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="0fde5-929">I2I - 又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-929">I2I - a.k.a.</span></span> <span data-ttu-id="0fde5-930">項目對項目的建議 - 這個選項會根據指定的一個項目或項目清單，來預測可能高度感興趣的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="0fde5-931">U2I - 又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-931">U2I - a.k.a.</span></span> <span data-ttu-id="0fde5-932">使用者對項目的建議 - 這個選項會根據指定的使用者識別碼 (及選擇性的項目清單)，來預測指定使用者 (及針對額外選擇的項目) 可能高度感興趣的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="0fde5-933">U2I 建議是根據使用者在建置模型前感興趣之項目的歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0fde5-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="0fde5-934">排名組建為技術組建，可讓您了解功能的效益。</span><span class="sxs-lookup"><span data-stu-id="0fde5-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="0fde5-935">通常，若要取得包含功能之建議模型的最佳結果，您應該採取下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0fde5-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="0fde5-936">觸發排名組建 (除非功能的分數很穩定) 並等待直到取得功能分數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="0fde5-937">藉由呼叫 [Get Features Info](#101-get-features-info-for-last-rank-build) API 來擷取功能的排名。</span><span class="sxs-lookup"><span data-stu-id="0fde5-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="0fde5-938">以下列參數設定建議組建：</span><span class="sxs-lookup"><span data-stu-id="0fde5-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="0fde5-939">`useFeatureInModel` - 設定為 True。</span><span class="sxs-lookup"><span data-stu-id="0fde5-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="0fde5-940">`ModelingFeatureList` - 設定為分數 2.0 或以上的逗號分隔功能清單 (以您在上一個步驟中擷取到的排名為根據)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="0fde5-941">`AllowColdItemPlacement` - 設定為 True。</span><span class="sxs-lookup"><span data-stu-id="0fde5-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="0fde5-942">您可以選擇性地將 `EnableFeatureCorrelation` 設定為 True，並將 `ReasoningFeatureList` 設定為您想要用於說明的功能清單 (通常是使用於模型化的相同功能清單或子清單)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="0fde5-943">以設定的參數觸發建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="0fde5-944">注意：如果您未設定任何參數 (例如叫用不含參數的建議組建) 或您沒有明確停用功能的使用方式 (例如 `UseFeatureInModel` 設為 False)，系統將會在排名組建存在時，將與功能相關的參數設定為上述的說明值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="0fde5-945">同時執行相同模行的排名組建和建議組建時並沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="0fde5-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="0fde5-946">不過，您無法在同一個模型上，以平行方式執行兩個相同類型的組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="0fde5-947">FBT (通常會一起購買) 組建也是另一種建議運算法，有時稱為「保守的」建議者，適用於本質上並不同質的目錄 (同質：書籍、電影、一些食物、流行；非同質：電腦與裝置、跨網域、高度差異)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="0fde5-948">注意：如果您上傳的使用方式檔案包含選擇性欄位 [事件類型]，則 FBT 模型只會使用 "Purchase" 事件。</span><span class="sxs-lookup"><span data-stu-id="0fde5-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="0fde5-949">如果沒有提供事件類型，所有事件都會視為 Purchase。</span><span class="sxs-lookup"><span data-stu-id="0fde5-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="0fde5-950">11.1 組建參數</span><span class="sxs-lookup"><span data-stu-id="0fde5-950">11.1 Build parameters</span></span>
<span data-ttu-id="0fde5-951">每個組建類型都可以透過一組參數 (如下所述) 進行設定。</span><span class="sxs-lookup"><span data-stu-id="0fde5-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="0fde5-952">如果您未設定參數，系統會自動根據您觸發組建時出現的資訊分配值給參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="0fde5-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-953">11.1.1.</span></span> <span data-ttu-id="0fde5-954">使用狀況冷凝器</span><span class="sxs-lookup"><span data-stu-id="0fde5-954">Usage condenser</span></span>
<span data-ttu-id="0fde5-955">附帶少數使用點的使用者或項目可能包含較多雜訊而非資訊。</span><span class="sxs-lookup"><span data-stu-id="0fde5-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="0fde5-956">系統會嘗試預測要用於模型之每個使用者/項目的使用點數目下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="0fde5-957">這個數字會在項目的 ItemCutoffLowerBound 和 ItemCutoffUpperBound 參數所定義的範圍內，也在使用者的 UserCutOffLowerBound 和 UserCutoffUpperBound 參數所定義的範圍內。</span><span class="sxs-lookup"><span data-stu-id="0fde5-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="0fde5-958">將至少一個對應的界限設為零，可以使冷凝器對項目或使用者的影響最小化。</span><span class="sxs-lookup"><span data-stu-id="0fde5-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="0fde5-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-959">11.1.2.</span></span> <span data-ttu-id="0fde5-960">排名組建參數</span><span class="sxs-lookup"><span data-stu-id="0fde5-960">Rank build parameters</span></span>
<span data-ttu-id="0fde5-961">下表描述排名組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="0fde5-962">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-962">Key</span></span> | <span data-ttu-id="0fde5-963">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-963">Description</span></span> | <span data-ttu-id="0fde5-964">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-964">Type</span></span> | <span data-ttu-id="0fde5-965">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0fde5-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="0fde5-966">NumberOfModelIterations</span></span> |<span data-ttu-id="0fde5-967">整體運算時間和模型精確度會反映模型執行反覆運算的次數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="0fde5-968">數字越高，得到的精確度就越高，但需要較久的運算時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="0fde5-969">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-969">Integer</span></span> |<span data-ttu-id="0fde5-970">10-50</span><span class="sxs-lookup"><span data-stu-id="0fde5-970">10-50</span></span> |
| <span data-ttu-id="0fde5-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="0fde5-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="0fde5-972">維度的數目與「功能」的數目相關，模型會嘗試尋找資料中的數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="0fde5-973">增加維度的數目將允許結果進一步微調成較小的叢集。</span><span class="sxs-lookup"><span data-stu-id="0fde5-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="0fde5-974">不過，太多維度會讓模型無法尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="0fde5-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="0fde5-975">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-975">Integer</span></span> |<span data-ttu-id="0fde5-976">10-40</span><span class="sxs-lookup"><span data-stu-id="0fde5-976">10-40</span></span> |
| <span data-ttu-id="0fde5-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-978">定義冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-979">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-979">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-980">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-980">Integer</span></span> |<span data-ttu-id="0fde5-981">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-983">定義冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-984">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-984">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-985">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-985">Integer</span></span> |<span data-ttu-id="0fde5-986">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-988">定義冷凝器的使用者下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-989">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-989">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-990">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-990">Integer</span></span> |<span data-ttu-id="0fde5-991">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-993">定義冷凝器的使用者上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-994">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-994">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-995">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-995">Integer</span></span> |<span data-ttu-id="0fde5-996">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="0fde5-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-997">11.1.3.</span></span> <span data-ttu-id="0fde5-998">建議組建參數</span><span class="sxs-lookup"><span data-stu-id="0fde5-998">Recommendation build parameters</span></span>
<span data-ttu-id="0fde5-999">下表描述建議組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="0fde5-1000">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-1000">Key</span></span> | <span data-ttu-id="0fde5-1001">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-1001">Description</span></span> | <span data-ttu-id="0fde5-1002">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-1002">Type</span></span> | <span data-ttu-id="0fde5-1003">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0fde5-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="0fde5-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="0fde5-1005">整體運算時間和模型精確度會反映模型執行反覆運算的次數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="0fde5-1006">數字越高，得到的精確度就越高，但需要較久的運算時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="0fde5-1007">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1007">Integer</span></span> |<span data-ttu-id="0fde5-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="0fde5-1008">10-50</span></span> |
| <span data-ttu-id="0fde5-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="0fde5-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="0fde5-1010">維度的數目與「功能」的數目相關，模型會嘗試尋找資料中的數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="0fde5-1011">增加維度的數目將允許結果進一步微調成較小的叢集。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="0fde5-1012">不過，太多維度會讓模型無法尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="0fde5-1013">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1013">Integer</span></span> |<span data-ttu-id="0fde5-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="0fde5-1014">10-40</span></span> |
| <span data-ttu-id="0fde5-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-1016">定義冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-1017">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1017">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1018">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1018">Integer</span></span> |<span data-ttu-id="0fde5-1019">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-1021">定義冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-1022">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1022">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1023">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1023">Integer</span></span> |<span data-ttu-id="0fde5-1024">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-1026">定義冷凝器的使用者下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-1027">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1027">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1028">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1028">Integer</span></span> |<span data-ttu-id="0fde5-1029">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-1031">定義冷凝器的使用者上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-1032">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1032">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1033">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1033">Integer</span></span> |<span data-ttu-id="0fde5-1034">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1035">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-1035">Description</span></span> |<span data-ttu-id="0fde5-1036">建置說明。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1036">Build description.</span></span> |<span data-ttu-id="0fde5-1037">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1037">String</span></span> |<span data-ttu-id="0fde5-1038">任何文字，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="0fde5-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="0fde5-1039">EnableModelingInsights</span></span> |<span data-ttu-id="0fde5-1040">可讓您計算建議模型上的度量。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="0fde5-1041">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1041">Boolean</span></span> |<span data-ttu-id="0fde5-1042">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1042">True/False</span></span> |
| <span data-ttu-id="0fde5-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="0fde5-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="0fde5-1044">指出是否可以使用功能以加強建議模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="0fde5-1045">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1045">Boolean</span></span> |<span data-ttu-id="0fde5-1046">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1046">True/False</span></span> |
| <span data-ttu-id="0fde5-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="0fde5-1047">ModelingFeatureList</span></span> |<span data-ttu-id="0fde5-1048">使用於建議組建中的功能名稱逗號分隔清單，可加強建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="0fde5-1049">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1049">String</span></span> |<span data-ttu-id="0fde5-1050">功能名稱，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="0fde5-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="0fde5-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="0fde5-1052">指出建議是否也應該透過功能相似度推入冷項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="0fde5-1053">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1053">Boolean</span></span> |<span data-ttu-id="0fde5-1054">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1054">True/False</span></span> |
| <span data-ttu-id="0fde5-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="0fde5-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="0fde5-1056">指出功能是否可用於推論。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="0fde5-1057">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1057">Boolean</span></span> |<span data-ttu-id="0fde5-1058">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1058">True/False</span></span> |
| <span data-ttu-id="0fde5-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="0fde5-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="0fde5-1060">用於推論句 (例如建議說明) 的功能名稱逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="0fde5-1061">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1061">String</span></span> |<span data-ttu-id="0fde5-1062">功能名稱，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="0fde5-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="0fde5-1063">EnableU2I</span></span> |<span data-ttu-id="0fde5-1064">允許個人化的建議，又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="0fde5-1065">U2I (使用者對項目的建議)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="0fde5-1066">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1066">Boolean</span></span> |<span data-ttu-id="0fde5-1067">True/False (預設值為 True)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="0fde5-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1068">11.1.4.</span></span> <span data-ttu-id="0fde5-1069">FBT 組建參數</span><span class="sxs-lookup"><span data-stu-id="0fde5-1069">FBT build parameters</span></span>
<span data-ttu-id="0fde5-1070">下表描述建議組建的組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="0fde5-1071">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-1071">Key</span></span> | <span data-ttu-id="0fde5-1072">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-1072">Description</span></span> | <span data-ttu-id="0fde5-1073">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-1073">Type</span></span> | <span data-ttu-id="0fde5-1074">有效的值 (預設值)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0fde5-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="0fde5-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="0fde5-1076">模型的保守程度。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1076">How conservative the model is.</span></span> <span data-ttu-id="0fde5-1077">模型化時要考量項目的共同出現次數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="0fde5-1078">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1078">Integer</span></span> |<span data-ttu-id="0fde5-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1079">3-50 (6)</span></span> |
| <span data-ttu-id="0fde5-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="0fde5-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="0fde5-1081">頻繁集合中的項目數界限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="0fde5-1082">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1082">Integer</span></span> |<span data-ttu-id="0fde5-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1083">2-3 (2)</span></span> |
| <span data-ttu-id="0fde5-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="0fde5-1084">FbtMinimalScore</span></span> |<span data-ttu-id="0fde5-1085">頻繁集合應該具有的最低分數，以包含在傳回的結果中。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="0fde5-1086">愈高愈好。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1086">The higher the better.</span></span> |<span data-ttu-id="0fde5-1087">兩倍</span><span class="sxs-lookup"><span data-stu-id="0fde5-1087">Double</span></span> |<span data-ttu-id="0fde5-1088">0 以上 (0)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1088">0 and above (0)</span></span> |
| <span data-ttu-id="0fde5-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="0fde5-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="0fde5-1090">定義組建所使用的相似度函式。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="0fde5-1091">Lift 有利於機緣巧合、Co-occurrence 有助於可預測性，而 Jaccard 可在兩者間取得一個很好的平衡。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="0fde5-1092">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1092">String</span></span> |<span data-ttu-id="0fde5-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="0fde5-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1094">11.2.</span></span> <span data-ttu-id="0fde5-1095">觸發建議組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="0fde5-1096">根據預設，此 API 會觸發建議模型組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="0fde5-1097">若要觸發排名組建 (以評分功能)，應使用附帶組建類型參數的組建 API 變數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="0fde5-1098">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1098">HTTP Method</span></span> | <span data-ttu-id="0fde5-1099">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1100">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1101">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="0fde5-1102">標頭</span><span class="sxs-lookup"><span data-stu-id="0fde5-1102">HEADER</span></span> |<span data-ttu-id="0fde5-1103">`"Content-Type", "text/xml"` (如果傳送要求本文)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="0fde5-1104">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1104">Parameter Name</span></span> | <span data-ttu-id="0fde5-1105">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1106">modelId</span></span> |<span data-ttu-id="0fde5-1107">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="0fde5-1108">userDescription</span></span> |<span data-ttu-id="0fde5-1109">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="0fde5-1110">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="0fde5-1111">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1111">See example above.</span></span><br><span data-ttu-id="0fde5-1112">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-1112">Max length: 50</span></span> |
| <span data-ttu-id="0fde5-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1113">apiVersion</span></span> |<span data-ttu-id="0fde5-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-1115">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-1115">Request Body</span></span> |<span data-ttu-id="0fde5-1116">如果留白，將會使用預設的組建參數來執行組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="0fde5-1117">如果您想要設定組建參數，請在主體中將參數傳送為 XML (如下列範例所示)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="0fde5-1118">(如需參數的說明，請參閱＜組建參數＞一節。)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="0fde5-1119">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1119">**Response**:</span></span>

<span data-ttu-id="0fde5-1120">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1121">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1121">This is an asynchronous API.</span></span> <span data-ttu-id="0fde5-1122">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="0fde5-1123">若要知道組建何時結束，您應該呼叫「取得模型的組建狀態」API，並在回應中找出這個組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="0fde5-1124">請注意，組建可能會花數分鐘到數小時的時間，視資料的大小而定。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="0fde5-1125">您無法取用建議直到組建結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="0fde5-1126">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1126">Valid build status:</span></span>

* <span data-ttu-id="0fde5-1127">建立 - 組建要求已建立。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="0fde5-1128">已排入佇列 - 組建要求已傳送並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="0fde5-1129">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="0fde5-1130">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="0fde5-1131">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="0fde5-1132">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="0fde5-1133">取消中 - 組建的取消要求已傳送。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="0fde5-1134">請注意，組建識別碼可以在下列路徑下找到： `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="0fde5-1135">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="0fde5-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1136">11.3.</span></span> <span data-ttu-id="0fde5-1137">觸發組建 (建議、排名或 FBT)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="0fde5-1138">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1138">HTTP Method</span></span> | <span data-ttu-id="0fde5-1139">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1140">POST</span><span class="sxs-lookup"><span data-stu-id="0fde5-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1141">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="0fde5-1142">標頭</span><span class="sxs-lookup"><span data-stu-id="0fde5-1142">HEADER</span></span> |<span data-ttu-id="0fde5-1143">`"Content-Type", "text/xml"` (如果傳送要求本文)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="0fde5-1144">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1144">Parameter Name</span></span> | <span data-ttu-id="0fde5-1145">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1146">modelId</span></span> |<span data-ttu-id="0fde5-1147">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="0fde5-1148">userDescription</span></span> |<span data-ttu-id="0fde5-1149">目錄的文字識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="0fde5-1150">請注意，如果您使用空格，必須將其編碼改成 %20。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="0fde5-1151">請參閱上面的範例。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1151">See example above.</span></span><br><span data-ttu-id="0fde5-1152">最大長度：50</span><span class="sxs-lookup"><span data-stu-id="0fde5-1152">Max length: 50</span></span> |
| <span data-ttu-id="0fde5-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="0fde5-1153">buildType</span></span> |<span data-ttu-id="0fde5-1154">要叫用的組建類型：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="0fde5-1155">- 'Recommendation' 為建議組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="0fde5-1156">- 'Ranking' 為排名組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="0fde5-1157">- 'Fbt' 為 FBT 組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="0fde5-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1158">apiVersion</span></span> |<span data-ttu-id="0fde5-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-1160">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-1160">Request Body</span></span> |<span data-ttu-id="0fde5-1161">如果留白，將會使用預設的組建參數來執行組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="0fde5-1162">如果您想要設定組建參數，請在主體中將它們傳送為 XML (如下列範例所示)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="0fde5-1163">(如需參數的說明和完整清單，請參閱＜組建參數＞一節。)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="0fde5-1164">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1164">**Response**:</span></span>

<span data-ttu-id="0fde5-1165">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1166">這是非同步的 API。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1166">This is an asynchronous API.</span></span> <span data-ttu-id="0fde5-1167">您會得到一個組建識別碼做為回應。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="0fde5-1168">若要知道組建何時結束，您應該呼叫「取得模型的組建狀態」API，並在回應中找出這個組建識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="0fde5-1169">請注意，組建可能會花數分鐘到數小時的時間，視資料的大小而定。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="0fde5-1170">您無法取用建議直到組建結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="0fde5-1171">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1171">Valid build status:</span></span>

* <span data-ttu-id="0fde5-1172">建立 - 模型已建立。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1172">Create - Model was created.</span></span>
* <span data-ttu-id="0fde5-1173">已排入佇列 - 已觸發模型組建，並已排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="0fde5-1174">建置中 - 模型正在建置中。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="0fde5-1175">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="0fde5-1176">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="0fde5-1177">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="0fde5-1178">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="0fde5-1179">請注意，組建識別碼可以在下列路徑下找到： `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="0fde5-1180">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="0fde5-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1181">11.4.</span></span> <span data-ttu-id="0fde5-1182">取得模型的組建狀態</span><span class="sxs-lookup"><span data-stu-id="0fde5-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="0fde5-1183">擷取指定之模型的組建及其狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="0fde5-1184">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1184">HTTP Method</span></span> | <span data-ttu-id="0fde5-1185">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1186">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1187">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1188">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1188">Parameter Name</span></span> | <span data-ttu-id="0fde5-1189">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1190">modelId</span></span> |<span data-ttu-id="0fde5-1191">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="0fde5-1192">onlyLastBuild</span></span> |<span data-ttu-id="0fde5-1193">指出是要傳回模型的所有組建歷程記錄，還是只傳回最近一個組建的狀態</span><span class="sxs-lookup"><span data-stu-id="0fde5-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="0fde5-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1194">apiVersion</span></span> |<span data-ttu-id="0fde5-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1195">1.0</span></span> |

<span data-ttu-id="0fde5-1196">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1196">**Response**:</span></span>

<span data-ttu-id="0fde5-1197">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1198">回應會包含每個組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1198">The response includes one entry per build.</span></span> <span data-ttu-id="0fde5-1199">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1200">`feed/entry/content/properties/UserName` - 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="0fde5-1201">`feed/entry/content/properties/ModelName` - 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="0fde5-1202">`feed/entry/content/properties/ModelId` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="0fde5-1203">`feed/entry/content/properties/IsDeployed` - 組建是否已部署 (又稱為</span><span class="sxs-lookup"><span data-stu-id="0fde5-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="0fde5-1204">作用中組建)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1204">active build).</span></span>
* <span data-ttu-id="0fde5-1205">`feed/entry/content/properties/BuildId` - 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="0fde5-1206">`feed/entry/content/properties/BuildType` - 組建類型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="0fde5-1207">`feed/entry/content/properties/Status` - 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="0fde5-1208">可以是下列其中之一：錯誤、建置中、已排入佇列、取消中、已取消、成功。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="0fde5-1209">`feed/entry/content/properties/StatusMessage` - 詳細狀態訊息 (僅適用於特定狀態)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="0fde5-1210">`feed/entry/content/properties/Progress` - 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="0fde5-1211">`feed/entry/content/properties/StartTime` - 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="0fde5-1212">`feed/entry/content/properties/EndTime` - 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="0fde5-1213">`feed/entry/content/properties/ExecutionTime` - 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="0fde5-1214">`feed/entry/content/properties/ProgressStep` - 正在進行中組建的目前階段相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="0fde5-1215">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1215">Valid build status:</span></span>

* <span data-ttu-id="0fde5-1216">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="0fde5-1217">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="0fde5-1218">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="0fde5-1219">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="0fde5-1220">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="0fde5-1221">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="0fde5-1222">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="0fde5-1223">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1223">Valid values for build type:</span></span>

* <span data-ttu-id="0fde5-1224">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="0fde5-1225">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="0fde5-1226">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="0fde5-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1227">11.5.</span></span> <span data-ttu-id="0fde5-1228">取得組建狀態</span><span class="sxs-lookup"><span data-stu-id="0fde5-1228">Get Builds Status</span></span>
<span data-ttu-id="0fde5-1229">擷取使用者之所有模型的組建狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="0fde5-1230">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1230">HTTP Method</span></span> | <span data-ttu-id="0fde5-1231">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1232">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1233">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1234">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1234">Parameter Name</span></span> | <span data-ttu-id="0fde5-1235">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="0fde5-1236">onlyLastBuild</span></span> |<span data-ttu-id="0fde5-1237">指出是要傳回模型的所有組建歷程記錄，還是只傳回最近一個組建的狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="0fde5-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1238">apiVersion</span></span> |<span data-ttu-id="0fde5-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1239">1.0</span></span> |

<span data-ttu-id="0fde5-1240">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1240">**Response**:</span></span>

<span data-ttu-id="0fde5-1241">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1242">回應會包含每個組建的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1242">The response includes one entry per build.</span></span> <span data-ttu-id="0fde5-1243">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1244">`feed/entry/content/properties/UserName` - 使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="0fde5-1245">`feed/entry/content/properties/ModelName` - 模型的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="0fde5-1246">`feed/entry/content/properties/ModelId` - 模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="0fde5-1247">`feed/entry/content/properties/IsDeployed` - 組建是否已部署。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="0fde5-1248">`feed/entry/content/properties/BuildId` - 組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="0fde5-1249">`feed/entry/content/properties/BuildType` - 組建類型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="0fde5-1250">`feed/entry/content/properties/Status` - 組建狀態。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="0fde5-1251">可以是下列其中之一：錯誤、建置中、已排入佇列、已取消、取消中、成功。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="0fde5-1252">`feed/entry/content/properties/StatusMessage` - 詳細狀態訊息 (僅適用於特定狀態)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="0fde5-1253">`feed/entry/content/properties/Progress` - 組建進度 (%)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="0fde5-1254">`feed/entry/content/properties/StartTime` - 組建開始時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="0fde5-1255">`feed/entry/content/properties/EndTime` - 組建結束時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="0fde5-1256">`feed/entry/content/properties/ExecutionTime` - 組建持續時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="0fde5-1257">`feed/entry/content/properties/ProgressStep` - 正在進行中組建的目前階段相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="0fde5-1258">有效的組建狀態：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1258">Valid build status:</span></span>

* <span data-ttu-id="0fde5-1259">建立 - 組建要求項目已建立。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="0fde5-1260">已排入佇列 - 組建要求已觸發並排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="0fde5-1261">建置中 - 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="0fde5-1262">成功 - 組建已成功結束。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="0fde5-1263">錯誤 - 組建已結束但發生失敗。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="0fde5-1264">已取消 - 組建已取消。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="0fde5-1265">取消中 - 正在取消組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="0fde5-1266">組建類型的有效值：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1266">Valid values for build type:</span></span>

* <span data-ttu-id="0fde5-1267">排名 - 排名組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="0fde5-1268">建議 - 建議組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="0fde5-1269">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="0fde5-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1270">11.6.</span></span> <span data-ttu-id="0fde5-1271">刪除組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1271">Delete Build</span></span>
<span data-ttu-id="0fde5-1272">刪除組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1272">Deletes a build.</span></span>

<span data-ttu-id="0fde5-1273">注意：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1273">NOTE:</span></span> <br><span data-ttu-id="0fde5-1274">您無法刪除使用中組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1274">You cannot delete an active build.</span></span> <span data-ttu-id="0fde5-1275">應該先將模型更新至不同的使用中組建，再刪除模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="0fde5-1276">您無法刪除進行中組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="0fde5-1277">您應該先藉由呼叫 <strong>取消組建</strong> 來取消組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="0fde5-1278">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1278">HTTP Method</span></span> | <span data-ttu-id="0fde5-1279">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1280">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1281">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1282">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1282">Parameter Name</span></span> | <span data-ttu-id="0fde5-1283">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1284">buildId</span></span> |<span data-ttu-id="0fde5-1285">組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="0fde5-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1286">apiVersion</span></span> |<span data-ttu-id="0fde5-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1287">1.0</span></span> |

<span data-ttu-id="0fde5-1288">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1288">**Response:**</span></span>

<span data-ttu-id="0fde5-1289">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="0fde5-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1290">11.7.</span></span> <span data-ttu-id="0fde5-1291">取消組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1291">Cancel Build</span></span>
<span data-ttu-id="0fde5-1292">取消狀態為建置中的組建。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="0fde5-1293">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1293">HTTP Method</span></span> | <span data-ttu-id="0fde5-1294">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="0fde5-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1296">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1297">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1297">Parameter Name</span></span> | <span data-ttu-id="0fde5-1298">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1299">buildId</span></span> |<span data-ttu-id="0fde5-1300">組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="0fde5-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1301">apiVersion</span></span> |<span data-ttu-id="0fde5-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1302">1.0</span></span> |

<span data-ttu-id="0fde5-1303">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1303">**Response:**</span></span>

<span data-ttu-id="0fde5-1304">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="0fde5-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1305">11.8.</span></span> <span data-ttu-id="0fde5-1306">取得組建參數</span><span class="sxs-lookup"><span data-stu-id="0fde5-1306">Get Build Parameters</span></span>
<span data-ttu-id="0fde5-1307">擷取組建參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="0fde5-1308">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1308">HTTP Method</span></span> | <span data-ttu-id="0fde5-1309">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1310">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1311">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1312">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1312">Parameter Name</span></span> | <span data-ttu-id="0fde5-1313">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1314">buildId</span></span> |<span data-ttu-id="0fde5-1315">組建的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="0fde5-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1316">apiVersion</span></span> |<span data-ttu-id="0fde5-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1317">1.0</span></span> |

<span data-ttu-id="0fde5-1318">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1318">**Response:**</span></span>

<span data-ttu-id="0fde5-1319">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1320">此 API 會傳回索引鍵/值項目的集合。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="0fde5-1321">每個元素都代表參數和它的值：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="0fde5-1322">`feed/entry/content/properties/Key` - 組建參數名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="0fde5-1323">`feed/entry/content/properties/Value` - 組建參數值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="0fde5-1324">下表描述每個索引鍵表示的值。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="0fde5-1325">金鑰</span><span class="sxs-lookup"><span data-stu-id="0fde5-1325">Key</span></span> | <span data-ttu-id="0fde5-1326">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-1326">Description</span></span> | <span data-ttu-id="0fde5-1327">類型</span><span class="sxs-lookup"><span data-stu-id="0fde5-1327">Type</span></span> | <span data-ttu-id="0fde5-1328">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0fde5-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="0fde5-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="0fde5-1330">整體運算時間和模型精確度會反映模型執行反覆運算的次數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="0fde5-1331">數字越高，得到的精確度就越高，但需要較久的運算時間。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="0fde5-1332">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1332">Integer</span></span> |<span data-ttu-id="0fde5-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="0fde5-1333">10-50</span></span> |
| <span data-ttu-id="0fde5-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="0fde5-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="0fde5-1335">維度的數目與「功能」的數目相關，模型會嘗試尋找資料中的數目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="0fde5-1336">增加維度的數目將允許結果進一步微調成較小的叢集。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="0fde5-1337">不過，太多維度會讓模型無法尋找項目之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="0fde5-1338">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1338">Integer</span></span> |<span data-ttu-id="0fde5-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="0fde5-1339">10-40</span></span> |
| <span data-ttu-id="0fde5-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-1341">定義冷凝器的項目下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-1342">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1342">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1343">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1343">Integer</span></span> |<span data-ttu-id="0fde5-1344">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-1346">定義冷凝器的項目上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-1347">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1347">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1348">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1348">Integer</span></span> |<span data-ttu-id="0fde5-1349">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="0fde5-1351">定義冷凝器的使用者下限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="0fde5-1352">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1352">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1353">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1353">Integer</span></span> |<span data-ttu-id="0fde5-1354">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="0fde5-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="0fde5-1356">定義冷凝器的使用者上限。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="0fde5-1357">請參閱上述的使用狀況冷凝器。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1357">See usage condenser above.</span></span> |<span data-ttu-id="0fde5-1358">Integer</span><span class="sxs-lookup"><span data-stu-id="0fde5-1358">Integer</span></span> |<span data-ttu-id="0fde5-1359">2 個以上 (0 代表停用冷凝器)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="0fde5-1360">說明</span><span class="sxs-lookup"><span data-stu-id="0fde5-1360">Description</span></span> |<span data-ttu-id="0fde5-1361">建置說明。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1361">Build description.</span></span> |<span data-ttu-id="0fde5-1362">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1362">String</span></span> |<span data-ttu-id="0fde5-1363">任何文字，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="0fde5-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="0fde5-1364">EnableModelingInsights</span></span> |<span data-ttu-id="0fde5-1365">可讓您計算建議模型上的度量。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="0fde5-1366">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1366">Boolean</span></span> |<span data-ttu-id="0fde5-1367">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1367">True/False</span></span> |
| <span data-ttu-id="0fde5-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="0fde5-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="0fde5-1369">指出是否可以使用功能以加強建議模型。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="0fde5-1370">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1370">Boolean</span></span> |<span data-ttu-id="0fde5-1371">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1371">True/False</span></span> |
| <span data-ttu-id="0fde5-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="0fde5-1372">ModelingFeatureList</span></span> |<span data-ttu-id="0fde5-1373">使用於建議組建中的功能名稱逗號分隔清單，可加強建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="0fde5-1374">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1374">String</span></span> |<span data-ttu-id="0fde5-1375">功能名稱，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="0fde5-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="0fde5-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="0fde5-1377">指出建議是否也應該透過功能相似度推入冷項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="0fde5-1378">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1378">Boolean</span></span> |<span data-ttu-id="0fde5-1379">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1379">True/False</span></span> |
| <span data-ttu-id="0fde5-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="0fde5-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="0fde5-1381">指出功能是否可用於推論。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="0fde5-1382">Boolean</span><span class="sxs-lookup"><span data-stu-id="0fde5-1382">Boolean</span></span> |<span data-ttu-id="0fde5-1383">True/False</span><span class="sxs-lookup"><span data-stu-id="0fde5-1383">True/False</span></span> |
| <span data-ttu-id="0fde5-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="0fde5-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="0fde5-1385">用於推論句 (例如建議說明) 的功能名稱逗號分隔清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="0fde5-1386">String</span><span class="sxs-lookup"><span data-stu-id="0fde5-1386">String</span></span> |<span data-ttu-id="0fde5-1387">功能名稱，最多 512 個字元</span><span class="sxs-lookup"><span data-stu-id="0fde5-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="0fde5-1388">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="0fde5-1389">12.建議</span><span class="sxs-lookup"><span data-stu-id="0fde5-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="0fde5-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1390">12.1.</span></span> <span data-ttu-id="0fde5-1391">取得項目建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="0fde5-1392">根據種子 (輸入) 項目的清單，取得 "Recommendation" 或 "Fbt" 類型之作用中組建的建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="0fde5-1393">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1393">HTTP Method</span></span> | <span data-ttu-id="0fde5-1394">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1395">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1396">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1397">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1397">Parameter Name</span></span> | <span data-ttu-id="0fde5-1398">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1399">modelId</span></span> |<span data-ttu-id="0fde5-1400">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="0fde5-1401">itemIds</span></span> |<span data-ttu-id="0fde5-1402">要建議的以逗號分隔項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="0fde5-1403">如果作用中組建的類型是 FBT，您可以只傳送一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="0fde5-1404">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1404">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1405">numberOfResults</span></span> |<span data-ttu-id="0fde5-1406">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1406">Number of required results</span></span> <br> <span data-ttu-id="0fde5-1407">最大值：150</span><span class="sxs-lookup"><span data-stu-id="0fde5-1407">Max: 150</span></span> |
| <span data-ttu-id="0fde5-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1408">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1409">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1409">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1410">apiVersion</span></span> |<span data-ttu-id="0fde5-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1411">1.0</span></span> |

<span data-ttu-id="0fde5-1412">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1412">**Response:**</span></span>

<span data-ttu-id="0fde5-1413">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1414">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1415">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1416">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1417">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1418">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1419">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1420">以下範例回應包含 10 個建議項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="0fde5-1421">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="0fde5-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1422">12.2.</span></span> <span data-ttu-id="0fde5-1423">取得項目建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="0fde5-1424">取得 "Recommendation" 或 "Fbt" 等類型之特定組建的建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="0fde5-1425">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1425">HTTP Method</span></span> | <span data-ttu-id="0fde5-1426">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1427">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1428">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1429">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1429">Parameter Name</span></span> | <span data-ttu-id="0fde5-1430">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1431">modelId</span></span> |<span data-ttu-id="0fde5-1432">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="0fde5-1433">itemIds</span></span> |<span data-ttu-id="0fde5-1434">要建議的以逗號分隔項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="0fde5-1435">如果作用中組建的類型是 FBT，您可以只傳送一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="0fde5-1436">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1436">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1437">numberOfResults</span></span> |<span data-ttu-id="0fde5-1438">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1438">Number of required results</span></span> <br> <span data-ttu-id="0fde5-1439">最大值：150</span><span class="sxs-lookup"><span data-stu-id="0fde5-1439">Max: 150</span></span> |
| <span data-ttu-id="0fde5-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1440">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1441">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1441">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1442">buildId</span></span> |<span data-ttu-id="0fde5-1443">要用於此建議要求的組建識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="0fde5-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1444">apiVersion</span></span> |<span data-ttu-id="0fde5-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1445">1.0</span></span> |

<span data-ttu-id="0fde5-1446">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1446">**Response:**</span></span>

<span data-ttu-id="0fde5-1447">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1448">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1449">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1450">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1451">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1452">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1453">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1454">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="0fde5-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1455">12.3.</span></span> <span data-ttu-id="0fde5-1456">取得 FBT 建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="0fde5-1457">根據種子 (輸入) 項目，取得 "Fbt" 類型之作用中組建的建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="0fde5-1458">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1458">HTTP Method</span></span> | <span data-ttu-id="0fde5-1459">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1460">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1461">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1462">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1462">Parameter Name</span></span> | <span data-ttu-id="0fde5-1463">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1464">modelId</span></span> |<span data-ttu-id="0fde5-1465">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1466">itemId</span></span> |<span data-ttu-id="0fde5-1467">建議的項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1467">Item to recommend for.</span></span> <br><span data-ttu-id="0fde5-1468">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1468">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1469">numberOfResults</span></span> |<span data-ttu-id="0fde5-1470">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1470">Number of required results</span></span> <br><span data-ttu-id="0fde5-1471">最大值：150</span><span class="sxs-lookup"><span data-stu-id="0fde5-1471">Max: 150</span></span> |
| <span data-ttu-id="0fde5-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="0fde5-1472">minimalScore</span></span> |<span data-ttu-id="0fde5-1473">頻繁集合應該具有的最低分數，以包含在傳回的結果中</span><span class="sxs-lookup"><span data-stu-id="0fde5-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="0fde5-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1474">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1475">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1475">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1476">apiVersion</span></span> |<span data-ttu-id="0fde5-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1477">1.0</span></span> |

<span data-ttu-id="0fde5-1478">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1478">**Response:**</span></span>

<span data-ttu-id="0fde5-1479">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1480">回應會包含每個建議項目集 (通常會與種子/輸入項目一起購買的一組項目) 的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="0fde5-1481">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1482">`Feed\entry\content\properties\Id1` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1483">`Feed\entry\content\properties\Name1` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1484">`Feed\entry\content\properties\Id2` - 第二個建議項目的識別碼 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="0fde5-1485">`Feed\entry\content\properties\Name2` - 第二個項目的名稱 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="0fde5-1486">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1487">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1488">以下範例回應包含 3 個建議項目集。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="0fde5-1489">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="0fde5-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1490">12.4.</span></span> <span data-ttu-id="0fde5-1491">取得 FBT 建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="0fde5-1492">取得 "Fbt" 類型之特定組建的建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="0fde5-1493">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1493">HTTP Method</span></span> | <span data-ttu-id="0fde5-1494">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1495">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1496">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1497">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1497">Parameter Name</span></span> | <span data-ttu-id="0fde5-1498">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1499">modelId</span></span> |<span data-ttu-id="0fde5-1500">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1501">itemId</span></span> |<span data-ttu-id="0fde5-1502">建議的項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1502">Item to recommend for.</span></span> <br><span data-ttu-id="0fde5-1503">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1503">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1504">numberOfResults</span></span> |<span data-ttu-id="0fde5-1505">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1505">Number of required results</span></span> <br><span data-ttu-id="0fde5-1506">最大值：150</span><span class="sxs-lookup"><span data-stu-id="0fde5-1506">Max: 150</span></span> |
| <span data-ttu-id="0fde5-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="0fde5-1507">minimalScore</span></span> |<span data-ttu-id="0fde5-1508">頻繁集合應該具有的最低分數，以包含在傳回的結果中</span><span class="sxs-lookup"><span data-stu-id="0fde5-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="0fde5-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1509">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1510">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1510">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1511">buildId</span></span> |<span data-ttu-id="0fde5-1512">要用於此建議要求的組建識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="0fde5-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1513">apiVersion</span></span> |<span data-ttu-id="0fde5-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1514">1.0</span></span> |

<span data-ttu-id="0fde5-1515">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1515">**Response:**</span></span>

<span data-ttu-id="0fde5-1516">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1517">回應會包含每個建議項目集 (通常會與種子/輸入項目一起購買的一組項目) 的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="0fde5-1518">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1519">`Feed\entry\content\properties\Id1` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1520">`Feed\entry\content\properties\Name1` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1521">`Feed\entry\content\properties\Id2` - 第二個建議項目的識別碼 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="0fde5-1522">`Feed\entry\content\properties\Name2` - 第二個項目的名稱 (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="0fde5-1523">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1524">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1525">請參閱 12.3 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="0fde5-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1526">12.5.</span></span> <span data-ttu-id="0fde5-1527">取得使用者建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="0fde5-1528">取得標示為作用中組建之 "Recommendation" 類型之組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="0fde5-1529">這個 API 會根據使用者的使用歷程記錄，傳回預測的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="0fde5-1530">注意：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1530">Notes:</span></span> 

1. <span data-ttu-id="0fde5-1531">FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="0fde5-1532">如果作用中組建是 FBT，這個方法會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="0fde5-1533">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1533">HTTP Method</span></span> | <span data-ttu-id="0fde5-1534">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1535">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1536">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1537">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1537">Parameter Name</span></span> | <span data-ttu-id="0fde5-1538">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1539">modelId</span></span> |<span data-ttu-id="0fde5-1540">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1541">userId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1541">userId</span></span> |<span data-ttu-id="0fde5-1542">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="0fde5-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1543">numberOfResults</span></span> |<span data-ttu-id="0fde5-1544">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1544">Number of required results</span></span> |
| <span data-ttu-id="0fde5-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1545">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1546">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1546">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1547">apiVersion</span></span> |<span data-ttu-id="0fde5-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1548">1.0</span></span> |

<span data-ttu-id="0fde5-1549">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1549">**Response:**</span></span>

<span data-ttu-id="0fde5-1550">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1551">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1552">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1553">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1554">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1555">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1556">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1557">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="0fde5-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1558">12.6.</span></span> <span data-ttu-id="0fde5-1559">使用項目清單取得使用者建議 (適用於作用中組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="0fde5-1560">使用額外的項目清單，取得標示為作用中組建之 "Recommendation" 類型之組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="0fde5-1561">這個 API 會根據使用者的使用歷程記錄和額外提供的項目，傳回預測的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="0fde5-1562">注意：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1562">Notes:</span></span> 

1. <span data-ttu-id="0fde5-1563">FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="0fde5-1564">如果作用中組建是 FBT，這個方法會傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="0fde5-1565">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1565">HTTP Method</span></span> | <span data-ttu-id="0fde5-1566">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1567">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1568">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1569">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1569">Parameter Name</span></span> | <span data-ttu-id="0fde5-1570">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1571">modelId</span></span> |<span data-ttu-id="0fde5-1572">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1573">userId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1573">userId</span></span> |<span data-ttu-id="0fde5-1574">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="0fde5-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="0fde5-1575">itemsIds</span></span> |<span data-ttu-id="0fde5-1576">要建議的以逗號分隔項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="0fde5-1577">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1577">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1578">numberOfResults</span></span> |<span data-ttu-id="0fde5-1579">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1579">Number of required results</span></span> |
| <span data-ttu-id="0fde5-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1580">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1581">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1581">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1582">apiVersion</span></span> |<span data-ttu-id="0fde5-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1583">1.0</span></span> |

<span data-ttu-id="0fde5-1584">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1584">**Response:**</span></span>

<span data-ttu-id="0fde5-1585">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1586">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1587">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1588">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1589">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1590">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1591">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1592">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="0fde5-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1593">12.7.</span></span> <span data-ttu-id="0fde5-1594">取得使用者建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="0fde5-1595">取得 "Recommendation" 類型之特定組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="0fde5-1596">這個 API 會根據使用者的使用歷程記錄 (用於特定組建)，傳回預測的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="0fde5-1597">注意：FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="0fde5-1598">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1598">HTTP Method</span></span> | <span data-ttu-id="0fde5-1599">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1600">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1601">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1602">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1602">Parameter Name</span></span> | <span data-ttu-id="0fde5-1603">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1604">modelId</span></span> |<span data-ttu-id="0fde5-1605">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1606">userId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1606">userId</span></span> |<span data-ttu-id="0fde5-1607">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="0fde5-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1608">numberOfResults</span></span> |<span data-ttu-id="0fde5-1609">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1609">Number of required results</span></span> |
| <span data-ttu-id="0fde5-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1610">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1611">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1611">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1612">buildId</span></span> |<span data-ttu-id="0fde5-1613">要用於此建議要求的組建識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="0fde5-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1614">apiVersion</span></span> |<span data-ttu-id="0fde5-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1615">1.0</span></span> |

<span data-ttu-id="0fde5-1616">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1616">**Response:**</span></span>

<span data-ttu-id="0fde5-1617">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1618">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1619">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1620">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1621">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1622">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1623">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1624">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="0fde5-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1625">12.8.</span></span> <span data-ttu-id="0fde5-1626">使用項目清單取得使用者建議 (屬於特定組建)</span><span class="sxs-lookup"><span data-stu-id="0fde5-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="0fde5-1627">取得 "Recommendation" 類型和額外的項目清單之特定組建的使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="0fde5-1628">這個 API 會根據使用者的使用歷程記錄和額外的項目清單，傳回預測的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="0fde5-1629">注意：FBT 組建沒有使用者建議。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="0fde5-1630">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1630">HTTP Method</span></span> | <span data-ttu-id="0fde5-1631">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1632">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1633">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1634">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1634">Parameter Name</span></span> | <span data-ttu-id="0fde5-1635">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1636">modelId</span></span> |<span data-ttu-id="0fde5-1637">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1638">userId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1638">userId</span></span> |<span data-ttu-id="0fde5-1639">使用者的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="0fde5-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="0fde5-1640">itemIds</span></span> |<span data-ttu-id="0fde5-1641">要建議的以逗號分隔項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="0fde5-1642">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="0fde5-1642">Max length: 1024</span></span> |
| <span data-ttu-id="0fde5-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="0fde5-1643">numberOfResults</span></span> |<span data-ttu-id="0fde5-1644">必要結果的數目 </span><span class="sxs-lookup"><span data-stu-id="0fde5-1644">Number of required results</span></span> |
| <span data-ttu-id="0fde5-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="0fde5-1645">includeMetatadata</span></span> |<span data-ttu-id="0fde5-1646">未來使用，永遠為 false</span><span class="sxs-lookup"><span data-stu-id="0fde5-1646">Future use, always false</span></span> |
| <span data-ttu-id="0fde5-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1647">buildId</span></span> |<span data-ttu-id="0fde5-1648">要用於此建議要求的組建識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="0fde5-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1649">apiVersion</span></span> |<span data-ttu-id="0fde5-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1650">1.0</span></span> |

<span data-ttu-id="0fde5-1651">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1651">**Response:**</span></span>

<span data-ttu-id="0fde5-1652">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1653">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1654">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1655">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1656">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1657">`Feed\entry\content\properties\Rating` - 建議的評等，數字愈高表示信賴度愈高。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="0fde5-1658">`Feed\entry\content\properties\Reasoning` - 建議推論 (例如建議說明)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="0fde5-1659">請參閱 12.1 中的回應範例</span><span class="sxs-lookup"><span data-stu-id="0fde5-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="0fde5-1660">13.使用者使用歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0fde5-1660">13. User Usage History</span></span>
<span data-ttu-id="0fde5-1661">一旦建置建議模型，系統即會允許擷取用於組建的使用者歷程記錄 (與特定使用者相關聯的項目)。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="0fde5-1662">這個 API 可擷取使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0fde5-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="0fde5-1663">注意：目前只有建議組建可使用使用者歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="0fde5-1664">13.1 擷取使用者歷程記錄</span><span class="sxs-lookup"><span data-stu-id="0fde5-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="0fde5-1665">擷取用於作用中組建或指定使用者識別碼之指定組建中的項目清單。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="0fde5-1666">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1666">HTTP Method</span></span> | <span data-ttu-id="0fde5-1667">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1668">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1668">GET</span></span> |<span data-ttu-id="0fde5-1669">取得使用中組建的使用者歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="0fde5-1670">取得指定組建的使用者歷程記錄 `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="0fde5-1671">範例：`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="0fde5-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="0fde5-1672">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1672">Parameter Name</span></span> | <span data-ttu-id="0fde5-1673">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1674">modelId</span></span> |<span data-ttu-id="0fde5-1675">模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="0fde5-1676">userId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1676">userId</span></span> |<span data-ttu-id="0fde5-1677">使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="0fde5-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1678">buildId</span></span> |<span data-ttu-id="0fde5-1679">選擇性參數，可用來表示應從中擷取使用者歷程記錄的組建</span><span class="sxs-lookup"><span data-stu-id="0fde5-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="0fde5-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1680">apiVersion</span></span> |<span data-ttu-id="0fde5-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1681">1.0</span></span> |

<span data-ttu-id="0fde5-1682">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1682">**Response:**</span></span>

<span data-ttu-id="0fde5-1683">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1684">回應會包含每個建議項目的一個項目。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="0fde5-1685">每個項目都有下列資料：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="0fde5-1686">`Feed\entry\content\properties\Id` - 建議項目識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="0fde5-1687">`Feed\entry\content\properties\Name` - 項目的名稱。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="0fde5-1688">`Feed\entry\content\properties\Rating` - N/A。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="0fde5-1689">`Feed\entry\content\properties\Reasoning` - N/A。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="0fde5-1690">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="0fde5-1691">14.通知</span><span class="sxs-lookup"><span data-stu-id="0fde5-1691">14. Notifications</span></span>
<span data-ttu-id="0fde5-1692">Azure Machine Learning 建議會在系統中持續發生錯誤時建立通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="0fde5-1693">有 3 種類型的通知：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="0fde5-1694">組建失敗 – 每個組建失敗都會觸發此通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="0fde5-1695">資料擷取處理失敗 - 當我們在處理每一模型的使用事件時，如果最後 5 分鐘有超過 100 個錯誤，就會觸發此通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="0fde5-1696">建議取用失敗 - 當我們在處理每一模型的建議要求時，如果最後 5 分鐘有超過 100 個錯誤，就會觸發此通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="0fde5-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1697">14.1.</span></span> <span data-ttu-id="0fde5-1698">取得通知</span><span class="sxs-lookup"><span data-stu-id="0fde5-1698">Get Notifications</span></span>
<span data-ttu-id="0fde5-1699">擷取所有模型或單一模型的所有通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="0fde5-1700">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1700">HTTP Method</span></span> | <span data-ttu-id="0fde5-1701">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1702">GET</span><span class="sxs-lookup"><span data-stu-id="0fde5-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1703">取得所有模型的所有通知：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1704">取得特定模型之通知的範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="0fde5-1705">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1705">Parameter Name</span></span> | <span data-ttu-id="0fde5-1706">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1707">modelId</span></span> |<span data-ttu-id="0fde5-1708">選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1708">Optional parameter.</span></span> <span data-ttu-id="0fde5-1709">如果省略此參數，您將會取得所有模型的所有通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="0fde5-1710">有效值：模型的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="0fde5-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1711">apiVersion</span></span> |<span data-ttu-id="0fde5-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-1713">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-1713">Request Body</span></span> |<span data-ttu-id="0fde5-1714">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-1714">NONE</span></span> |

<span data-ttu-id="0fde5-1715">**回應：**</span><span class="sxs-lookup"><span data-stu-id="0fde5-1715">**Response:**</span></span>

<span data-ttu-id="0fde5-1716">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="0fde5-1717">OData XML</span><span class="sxs-lookup"><span data-stu-id="0fde5-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="0fde5-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1718">14.2.</span></span> <span data-ttu-id="0fde5-1719">刪除模型通知</span><span class="sxs-lookup"><span data-stu-id="0fde5-1719">Delete Model Notifications</span></span>
<span data-ttu-id="0fde5-1720">刪除模型的所有已讀通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="0fde5-1721">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1721">HTTP Method</span></span> | <span data-ttu-id="0fde5-1722">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1723">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="0fde5-1724">範例：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1725">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1725">Parameter Name</span></span> | <span data-ttu-id="0fde5-1726">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="0fde5-1727">modelId</span></span> |<span data-ttu-id="0fde5-1728">模型的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="0fde5-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="0fde5-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1729">apiVersion</span></span> |<span data-ttu-id="0fde5-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-1731">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-1731">Request Body</span></span> |<span data-ttu-id="0fde5-1732">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-1732">NONE</span></span> |

<span data-ttu-id="0fde5-1733">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1733">**Response**:</span></span>

<span data-ttu-id="0fde5-1734">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="0fde5-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1735">14.3.</span></span> <span data-ttu-id="0fde5-1736">刪除使用者通知</span><span class="sxs-lookup"><span data-stu-id="0fde5-1736">Delete User Notifications</span></span>
<span data-ttu-id="0fde5-1737">刪除所有模型的所有通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="0fde5-1738">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="0fde5-1738">HTTP Method</span></span> | <span data-ttu-id="0fde5-1739">URI</span><span class="sxs-lookup"><span data-stu-id="0fde5-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1740">刪除</span><span class="sxs-lookup"><span data-stu-id="0fde5-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="0fde5-1741">參數名稱</span><span class="sxs-lookup"><span data-stu-id="0fde5-1741">Parameter Name</span></span> | <span data-ttu-id="0fde5-1742">有效值</span><span class="sxs-lookup"><span data-stu-id="0fde5-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="0fde5-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0fde5-1743">apiVersion</span></span> |<span data-ttu-id="0fde5-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="0fde5-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="0fde5-1745">要求本文</span><span class="sxs-lookup"><span data-stu-id="0fde5-1745">Request Body</span></span> |<span data-ttu-id="0fde5-1746">無</span><span class="sxs-lookup"><span data-stu-id="0fde5-1746">NONE</span></span> |

<span data-ttu-id="0fde5-1747">**回應**：</span><span class="sxs-lookup"><span data-stu-id="0fde5-1747">**Response**:</span></span>

<span data-ttu-id="0fde5-1748">HTTP 狀態碼：200</span><span class="sxs-lookup"><span data-stu-id="0fde5-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="0fde5-1749">15.法律</span><span class="sxs-lookup"><span data-stu-id="0fde5-1749">15. Legal</span></span>
<span data-ttu-id="0fde5-1750">這份文件係依「現狀」提供。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="0fde5-1751">本文件中提供的資訊與畫面 (包括 URL 及其他網際網路網站參考資料) 如有變更，恕不另行通知。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="0fde5-1752">此處描述的一些範例僅供說明之用，純屬虛構。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="0fde5-1753">並未影射或關聯任何真實的人、事、物。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="0fde5-1754">本文件未提供給您任何 Microsoft 產品中任何智慧財產的任何法定權利。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="0fde5-1755">您可以複製並使用這份文件，供內部參考之用。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="0fde5-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0fde5-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="0fde5-1757">著作權所有，並保留一切權利。</span><span class="sxs-lookup"><span data-stu-id="0fde5-1757">All rights reserved.</span></span>

